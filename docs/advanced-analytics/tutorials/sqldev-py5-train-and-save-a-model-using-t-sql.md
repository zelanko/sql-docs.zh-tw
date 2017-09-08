---
title: "步驟 5︰使用 T-SQL 定型及儲存模型 | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- python-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2017
dev_langs:
- Python
- TSQL
ms.assetid: 
caps.latest.revision: 2
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 80a47819dfbb2e96162a49730e0dcf0b1b340f07
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="step-5-train-and-save-a-model-using-t-sql"></a>步驟 5： 定型和儲存模型，使用 T-SQL

在此步驟中，您會學習如何訓練機器學習模型使用 Python 封裝**scikit-了解**和**revoscalepy**。 這些 Python 程式庫已隨 SQL Server 機器學習服務，讓您可以載入的模組，並呼叫預存程序的必要函式。 您將使用剛才建立的資料功能來定型模型，然後將定型的模型儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>將範例資料分割成定型和測試集

1. 執行下列 T-SQL 命令來建立將 nyctaxi 中的資料分割的預存程序\_分成兩個部分的範例資料表： nyctaxi\_範例\_訓練和 nyctaxi\_範例\_測試。

    ```SQL
    CREATE PROCEDURE [dbo].[TrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 執行預存程序，並輸入整數，表示百分比的資料配置至定型集。 例如，下列陳述式會配置 60%的定型集的資料。 定型集和測試資料會儲存在兩個個別的資料表。

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model-using-scikit-learn"></a>建立羅吉斯迴歸模型使用 scikit-了解

在本節中，您可以建立可以用來定型模型，使用您剛才準備好定型資料的預存程序。 這個預存程序定義的輸入的資料，並使用**scikit-了解**函式來定型羅吉斯迴歸模型。 您可以呼叫 Python 執行階段使用的系統預存程序中，安裝 SQL server [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

若要讓您更輕鬆地重新定型模型，可以將呼叫包裝至 sp_execute_exernal_script 在另一個預存程序，並傳遞新的定型資料，做為參數。 本節將引導您完成該程序。

1.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModelSciKitPy_。  請注意，預存程序包含的輸入資料的定義，因此您不需要提供輸入的查詢。

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelSciKitPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelSciKitPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
      EXEC sp_execute_external_script
      @language = N'Python',
      @script = N'
      import numpy
      import pickle
      import pandas
      from sklearn.linear_model import LogisticRegression
      
      ##Create SciKit-Learn logistic regression model
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      SKLalgo = LogisticRegression()
      logitObj = SKLalgo.fit(X, y)
      
      ##Serialize model
      trained_model = pickle.dumps(logitObj)
      ',
      @input_data_1 = N'
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_training
      ',
      @input_data_1_name = N'InputDataSet',
      @params = N'@trained_model varbinary(max) OUTPUT',
      @trained_model = @trained_model OUTPUT;
      ;
    END;
    GO
    ```

2. 執行下列 SQL 陳述式來插入到定型的模型資料表 nyc\_taxi_models。

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelSciKitPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    資料處理，並配適模型可能需要數分鐘。 訊息會經由管道輸出至 Python 的**stdout**資料流也會顯示在**訊息**視窗[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *來自外部指令碼的 STDOUT 訊息：*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 開啟資料表*nyc\_taxi_models*。 您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    *linear_model* *0x800363736B6C6561726E2E6C696E6561...*

## <a name="build-a-logistic-model-using-the-revoscalepy-package"></a>建立羅吉斯模型使用_revoscalepy_封裝

現在，建立不同的預存程序，使用新**revoscalepy**定型羅吉斯迴歸模型的封裝。 **Revoscalepy**封裝物件、 轉換和演算法類似於所提供的 R 語言的報告功能包含 Python **RevoScaleR**封裝。 與此媒體櫃，您可以建立計算內容，移動之間的資料計算內容、 轉換資料，以及定型使用熱門的演算法，例如羅吉斯和線性迴歸、 決策樹，以及更多的預測模型。 如需詳細資訊，請參閱[revoscalepy 是什麼？](../python/what-is-revoscalepy.md)

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModelRxPy_。  此模型也會使用您剛才準備好定型資料。 因為預存程序已經包含輸入資料的定義，您不必提供輸入的查詢。

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    GO
    ```

    這個預存程序會執行下列步驟，做為模型定型的一部分：

    - 定型羅吉斯迴歸模型使用 revoscalepy 封裝上 nyctaxi\_範例\_定型資料。
    - SELECT 查詢會使用自訂的純量函數 _fnCalculateDistance_ 計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設 Python 輸入變數， `InputDataset`。
    - Python 指令碼呼叫 revoscalepy LogisticRegression 函式，它是隨附[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，以建立羅吉斯迴歸模型。
    - 二進位變數 _tipped_ 可做為「標籤」或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
    - 定型的模型，包含 Python 變數中`logitObj`序列化並將做為輸出參數、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 輸出會插入資料庫資料表_nyc_taxi_models_，以及其名稱，為新的資料列，使您可以擷取，並將它用於未來的預測。

2. 執行預存程序，如下所示插入定型**revoscalepy**模型到資料表 _nyc\_計程車\_模型。

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    資料處理，並配適模型可能需要一點時間。 訊息會經由管道輸出至 Python 的**stdout**資料流也會顯示在**訊息**視窗[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *來自外部指令碼的 STDOUT 訊息：*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 開啟 *nyc_taxi_models*資料表。 您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    *rx_model* *0x8003637265766F7363616c...*

在下一個步驟中，您可以使用 定型的模型來建立預測。

## <a name="next-step"></a>下一步

[步驟 6： 實施模型](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一個步驟

[步驟 4： 建立使用 T-SQL 資料功能](sqldev-py5-train-and-save-a-model-using-t-sql.md)

