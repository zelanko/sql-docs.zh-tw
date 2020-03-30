---
title: Python + T-SQL：定型模型
description: Python 教學課程示範如何在 SQL Server 上使用 Transact-SQL 來定型和儲存模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 87194c1a77964f0e5aef3d0fae008d14cbfb8eb2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2020
ms.locfileid: "74901800"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>使用 T-SQL 定型及儲存 Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是[適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)教學課程的一部分。 

在此步驟中，您將瞭解如何使用 Python 套件來定型機器學習模型 **scikit-learn** 和 **revoscalepy**。 這些 Python 程式庫已經與 SQL Server 機器學習服務一起安裝。

您可以載入模組，並呼叫所需的函數，以使用 SQL Server 預存程序來建立和定型模型。 此模型需要您在先前課程中設計的資料特徵。 最後，您會將定型的模型儲存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>將樣本資料分割成定型集和測試集

1. 建立名為 **PyTrainTestSplit** 的預存程序，將 nyctaxi_sample 資料表中的資料分割成兩個部分：nyctaxi_sample_training 和 nyctaxi_sample_testing。 

    這個預存程序應該已經為您建立，但是您可以執行下列程式碼來建立：

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainTestSplit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainTestSplit] (@pct int)
    AS
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_training
    SELECT * into nyctaxi_sample_training FROM nyctaxi_sample WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) < @pct
    
    DROP TABLE IF EXISTS dbo.nyctaxi_sample_testing
    SELECT * into nyctaxi_sample_testing FROM nyctaxi_sample
    WHERE (ABS(CAST(BINARY_CHECKSUM(medallion,hack_license)  as int)) % 100) > @pct
    GO
    ```

2. 若要使用自訂分割來分割您的資料，請執行預存程序，然後輸入整數，代表配置給定型集的資料百分比。 例如，下列陳述式會將 60% 的資料配置到定型集。

    ```sql
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="build-a-logistic-regression-model"></a>建立羅吉斯迴歸模型

資料備妥之後，您就可以用它來定型模型。 若要這麼做，您可以呼叫執行一些 Python 程式碼的預存程序，並接受定型資料表的輸入。 在本教學課程中，您會建立兩個模型，兩個都是二元分類模型：

+ **PyTrainScikit 的預存程序**會使用 **scikit-learn** 套件建立小費預測模型。
+ 預存程序 **TrainTipPredictionModelRxPy** 會使用 **revoscalepy** 套件建立小費預測模型。

每個預存程序都會使用您提供的輸入資料來建立和定型羅吉斯迴歸模型。 所有 Python 程式碼都會包裝在系統預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 中。

為了讓您更輕鬆地針對新資料重新定型模型，您可以將 sp_execute_external_script 的呼叫包裝在另一個預存程序中，並以參數的形式傳入新的定型資料。 此節將逐步說明該流程。

### <a name="pytrainscikit"></a>PyTrainScikit

1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，開啟新的 [查詢]  視窗，然後執行下列陳述式來建立預存程序 **PyTrainScikit**。  預存程序包含輸入資料的定義，因此您不需要提供輸入查詢。

    ```sql
    DROP PROCEDURE IF EXISTS PyTrainScikit;
    GO

    CREATE PROCEDURE [dbo].[PyTrainScikit] (@trained_model varbinary(max) OUTPUT)
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

2. 執行下列 SQL 陳述式，將定型的模型插入資料表 nyc\_taxi_models 中。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    資料處理和模型調整可能需要幾分鐘的時間。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [訊息]  視窗會顯示經由管道輸出至 Python 的 **stdout** 資料流的訊息。 例如：

    *來自外部指令碼的 STDOUT 訊息：* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. 開啟資料表 *nyc\_taxi_models*。 您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561....*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

這個預存程序使用新的 **revoscalepy** 套件，這是適用於 Python 的新套件。 其中包含物件、轉換和演算法，類似於針對 R 語言的 **RevoScaleR** 套件提供的演算法。 

藉由使用 **revoscalepy**，您可以建立遠端計算內容、在計算內容之間移動資料、轉換資料，以及使用常用的演算法 (例如羅吉斯和線性迴歸、決策樹等等) 定型預測模型。 如需詳細資訊，請參閱 [SQL Server 中的 revoscalepy 模組](../python/ref-py-revoscalepy.md)和 [revoscalepy 函數參考](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) \(英文\)。

1. 在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，開啟新的 [查詢]  視窗，然後執行下列陳述式來建立預存程序 _TrainTipPredictionModelRxPy_。  因為預存程序已經包含輸入資料的定義，因此您不需要提供輸入查詢。

    ```sql
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

    這個預存程序會在模型定型同時執行下列兩個步驟︰

    - SELECT 查詢會套用自訂的純量函數 _fnCalculateDistance_ 計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設的 Python 輸入變數 `InputDataset`中。
    - 二進位變數 _tipped_ 可做為「標籤」  或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。
    - 定型的模型會序列化並儲存在 Python 變數 `logitObj` 中。 藉由新增 T-SQL 關鍵字輸出，您可以加入變數做為預存程序的輸出。 在下一個步驟中，該變數是用來將模型的二進位代碼插入資料庫資料表 _nyc_taxi_models_ 中。 這種機制可讓您輕鬆地儲存和重複使用模型。

2. 如下所示執行預存程序，將定型的 **revoscalepy** 模型插入資料表 *nyc_taxi_models* 中。

    ```sql
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    資料處理和模型調整可能需要一些時間。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [訊息]  視窗會顯示經由管道輸出至 Python 的 **stdout** 資料流的訊息。 例如：

    *來自外部指令碼的 STDOUT 訊息：* 
  *C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\revoscalepy*

3. 開啟 *nyc_taxi_models*資料表。 您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    *revoscalepy_model* *0x8003637265766F7363616c....*

在下一個步驟中，您將使用定型的模型來建立預測。

## <a name="next-step"></a>後續步驟

[在預存程序中使用 Python 內嵌執行預測](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一個步驟

[使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)
