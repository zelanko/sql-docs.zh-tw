---
title: "步驟 5： 訓練並儲存使用 T-SQL Python 模型 |Microsoft 文件"
ms.custom: 
ms.date: 10/17/2017
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
ms.sourcegitcommit: 2f28400200105e8e63f787cbcda58c183ba00da5
ms.openlocfilehash: 11fa031229d8bc08a9091c3fa6f85e81468d7379
ms.contentlocale: zh-tw
ms.lasthandoff: 10/18/2017

---
# <a name="step-5-train-and-save-a-python-model-using-t-sql"></a>步驟 5： 訓練並儲存使用 T-SQL Python 模型

這篇文章的教學課程中，屬於[SQL 開發人員的資料庫中的 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，您會學習如何訓練機器學習模型使用 Python 封裝**scikit-了解**和**revoscalepy**。 這些 Python 程式庫中已安裝 SQL Server 機器學習服務。

您載入的模組，並呼叫來建立及定型的模型使用的 SQL Server 預存程序必要的功能。 模型會需要您在先前課程所設計的資料功能。 最後，您將儲存已定型的模型來[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。

> [!IMPORTANT]
> 已有幾項變更**revoscalepy**封裝，本教學課程需要小變更的程式碼。 請參閱[變更清單](sqldev-py6-operationalize-the-model.md#changes)在本教學課程結尾處。 
> 
> 如果您安裝 Python 的服務使用發行前版本的 Sql Server 2017，我們建議您升級至最新版本。 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>將範例資料分割成定型和測試集

1. 您可以使用預存程序**TrainTestSplit**將 nyctaxi 中的資料分割\_分成兩個部分的範例資料表： nyctaxi\_範例\_訓練和 nyctaxi\_範例\_測試。 

    這個預存程序應該已經建立，但您可以執行下列程式碼來建立它：

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

2. 若要將使用自訂的分割資料，執行預存程序，並輸入整數，表示百分比的資料配置至定型集。 例如，下列陳述式會配置 60%的定型集的資料。

    ```SQL
    EXEC TrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>建立羅吉斯迴歸模型

已備妥資料後，您可以使用它來定型模型。 您可以呼叫預存程序執行一些 Python 程式碼，取得做為輸入的定型資料的資料表。 此教學課程中，您可以建立兩個模型，這兩個二元分類模型：

+ 預存程序**TrainTipPredictionModelRxPy**建立提示預測模型使用**revoscalepy**封裝。
+ 預存程序**TrainTipPredictionModelSciKitPy**建立提示預測模型使用**scikit-了解**封裝。

每個預存程序會使用輸入的資料您提供給建立並定型羅吉斯迴歸模型。 所有的 Python 程式碼會包裝在系統預存程序中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

為了讓您更輕鬆地進行重新培訓模型的新資料，您將呼叫包裝至 sp_execute_exernal_script 在另一個預存程序，並在新的定型資料，做為參數傳遞。 本節將引導您完成該程序。

### <a name="traintippredictionmodelscikitpy"></a>TrainTipPredictionModelSciKitPy

1.  在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModelSciKitPy_。  預存程序包含的輸入資料的定義，因此您不必提供輸入的查詢。

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

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

這個預存程序會使用新**revoscalepy**套件，也就是新的 Python 的封裝。 它包含的物件、 轉換和演算法所提供的 R 語言的類似**RevoScaleR**封裝。 

使用**revoscalepy**，您可以建立遠端計算內容、 之間移動資料計算內容、 轉換資料及定型使用熱門例如羅吉斯和線性迴歸，決策樹演算法的預測模型和更多。 如需詳細資訊，請參閱[revoscalepy 是什麼？](../python/what-is-revoscalepy.md)

1. 在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModelRxPy_。  因為預存程序已經包含輸入資料的定義，您不必提供輸入的查詢。

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
    from revoscalepy.functions.RxLogit import rx_logit
    
    ## Create a logistic regression model using rx_logit function from revoscalepy package
    logitObj = rx_logit("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
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

    - SELECT 查詢適用於自訂的純量函數_fnCalculateDistance_以計算收取和下車位置之間的直接距離。 查詢的結果會儲存在預設 Python 輸入變數， `InputDataset`。
    - 二進位變數_傾斜_做*標籤*或結果資料行和模型就適合使用這些特徵資料行： _passenger_count_， _trip_距離_， _trip_time_in_secs_，和_direct_distance_。
    - 定型的模型會序列化並儲存在 Python 變數`logitObj`。 藉由加入 T-SQL OUTPUT 關鍵字，您可以加入做為輸出的預存程序的變數。 在下一個步驟中，該變數用於插入資料庫資料表中的二進位的程式碼模型的_nyc_taxi_models_。 這個機制可讓您輕鬆地儲存它，並重複使用的模型。

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

[步驟 6： 實施 Python 模型使用 SQL Server](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一個步驟

[步驟 4︰使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)

