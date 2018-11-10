---
title: 訓練及儲存使用 T-SQL Python 模型 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/01/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d3917678cb16462f065754dd389be53ae8cd6016
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032715"
---
# <a name="train-and-save-a-python-model-using-t-sql"></a>訓練及儲存使用 T-SQL Python 模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是教學課程中，部分[適用於 SQL 開發人員的資料庫內 Python 分析](sqldev-in-database-python-for-sql-developers.md)。 

在此步驟中，了解如何使用來定型機器學習服務模型的 Python 套件**scikit-learn-了解**並**revoscalepy**。 使用 SQL Server 機器學習服務，必須已經安裝這些 Python 程式庫。

您載入的模組，並呼叫所需的函式，來建立和使用 SQL Server 預存程序來定型模型。 模型需要您在先前課程所設計的資料功能。 最後，您將儲存為定型的模型以[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。
 

## <a name="split-the-sample-data-into-training-and-testing-sets"></a>將範例資料分割成定型和測試集

1. 建立呼叫預存程序**PyTrainTestSplit**將 nyctaxi_sample 資料表中的資料分成兩個部分： nyctaxi_sample_training 和 nyctaxi_sample_testing。 

    這個預存程序應該已建立，但您可以執行下列程式碼來建立它：

    ```SQL
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

2. 若要將使用自訂的分割資料，請執行預存程序中，並輸入整數，表示至定型集的資料配置的百分比。 例如，下列陳述式會配置 60%的定型集的資料。

    ```SQL
    EXEC PyTrainTestSplit 60
    GO
    ```

## <a name="add-a-name-column-in-nyctaximodels"></a>Nyc_taxi_models 中加入名稱資料行

在本教學課程中的指令碼儲存成產生的模型標籤的模型名稱。 模型名稱用於查詢中，選取 revoscalepy 或 Scikit-learn 模型。

1. 在 Management Studio 中開啟**nyc_taxi_models**資料表。

2. 以滑鼠右鍵按一下**資料行**然後按一下**新的資料行**。 若要設定的資料行名稱*名稱*，與型別**nchar(250)**，並允許 null 值。

    ![名稱資料行，以儲存模型名稱](media/sqldev-python-newcolumn.png)

## <a name="build-a-logistic-regression-model"></a>建立羅吉斯迴歸模型

已備妥資料後，您可以使用它來定型模型。 您可以呼叫預存程序，執行一些 Python 程式碼，將作為輸入的定型資料的資料表。 本教學課程中，您會建立兩個模型，這兩種二元分類模型：

+ 預存程序**PyTrainScikit**建立提示預測模型 using **scikit-learn-了解**封裝。
+ 預存程序**TrainTipPredictionModelRxPy**建立提示預測模型 using **revoscalepy**封裝。

每個預存程序會使用輸入的資料您提供給建立並定型的羅吉斯迴歸模型。 所有的 Python 程式碼會包裝在系統預存程序中， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

為了讓您更輕鬆地重新定型新的資料模型，您可以將 sp_execute_exernal_script 的呼叫包裝在另一個預存程序，並傳入新的定型資料，做為參數。 本節將逐步引導您完成該程序。

### <a name="pytrainscikit"></a>PyTrainScikit

1.  在  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序**PyTrainScikit**。  預存程序包含輸入資料，的定義，因此您不必提供輸入的查詢。

    ```SQL
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

2. 執行下列 SQL 陳述式來插入到定型的模型資料表 nyc\_taxi_models。

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC PyTrainScikit @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('SciKit_model', @model);
    ```

    資料處理和模型調整可能需要幾分鐘。 會使用管線傳送至 Python 的訊息**stdout**串流會顯示在**訊息**視窗[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *來自外部指令碼的 STDOUT 訊息︰*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 開啟資料表*nyc\_taxi_models*。 您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    *SciKit_model* *0x800363736B6C6561726E2E6C696E6561...*

### <a name="traintippredictionmodelrxpy"></a>TrainTipPredictionModelRxPy

這個預存程序會使用新**revoscalepy**封裝，也就是適用於 Python 的新封裝。 它包含的物件、 轉換及所提供的 R 語言的類似的演算法**RevoScaleR**封裝。 

藉由使用**revoscalepy**，您可以建立遠端計算內容之間移動資料計算內容，轉換資料，並訓練預測模型使用熱門的演算法，例如羅吉斯和線性迴歸、 決策樹和更多。 如需詳細資訊，請參閱[revoscalepy 是什麼？](../python/what-is-revoscalepy.md)

1. 在  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]，開啟新**查詢**視窗，然後執行下列陳述式來建立預存程序_TrainTipPredictionModelRxPy_。  預存程序已經包含輸入資料的定義，因為您不必提供輸入的查詢。

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

    這個預存程序做為模型定型的一部分，執行下列步驟：

    - SELECT 查詢適用於自訂的純量函式_fnCalculateDistance_來計算上車和下車位置之間的直線距離。 查詢的結果會儲存在預設 Python 輸入變數， `InputDataset`。
    - 二進位變數_tipped_作為*標籤*或結果資料行，與模型就適合使用這些特徵資料行： _passenger_count_， _trip_距離_， _trip_time_in_secs_，以及_direct_distance_。
    - 定型的模型會序列化並儲存在 Python 變數`logitObj`。 藉由新增 T-SQL 關鍵字輸出，您可以新增變數做為預存程序的輸出。 在下一個步驟中，該變數用來將模型的二進位程式碼插入資料庫資料表_nyc_taxi_models_。 這個機制可讓您輕鬆地儲存和重複使用的模型。

2. 執行預存程序，如下所示插入定型**revoscalepy**模型到資料表*nyc_taxi_models*。

    ```SQL
    DECLARE @model VARBINARY(MAX);
    EXEC TrainTipPredictionModelRxPy @model OUTPUT;
    INSERT INTO nyc_taxi_models (name, model) VALUES('revoscalepy_model', @model);
    ```

    資料處理和模型調整可能需要一段時間。 會使用管線傳送至 Python 的訊息**stdout**串流會顯示在**訊息**視窗[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。 例如：

    *來自外部指令碼的 STDOUT 訊息︰*
  *C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\PYTHON_SERVICES\lib\site packages\revoscalepy*

3. 開啟 *nyc_taxi_models*資料表。 您可以看到當中已新增一個新的資料列，其 _model_資料行中包含序列化的模型。

    *revoscalepy_model* *0x8003637265766F7363616c...*

在下一個步驟中，您可以使用定型的模型來建立預測。

## <a name="next-step"></a>下一步

[執行預測使用內嵌在預存程序中的 Python](sqldev-py6-operationalize-the-model.md)

## <a name="previous-step"></a>上一個步驟

[使用 T-SQL 建立資料特徵](sqldev-py5-train-and-save-a-model-using-t-sql.md)
