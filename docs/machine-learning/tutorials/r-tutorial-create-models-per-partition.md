---
title: 在 R 中建立資料分割型模型
description: 了解如何在使用 SQL Server 機器學習服務的資料分割模型功能時，模型、定型並使用以動態方式建立的資料分割。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 04/30/2020
ms.topic: tutorial
ms.author: davidph
author: dphansen
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bf294501b1cb613bf97b581a30a193469c78b9f6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756398"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>教學課程：在 SQL Server 上的 R 中建立資料分割模型
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在 SQL Server 2019 中，資料分割模型是透過分割資料來建立與定型模型的能力。 針對自然分割成指定分類配置的分層資料 (例如地理區域、日期和時間、年齡或性別)，您可以在整個資料集上執行指令碼，並能夠對維持不變的資料分割區進行模型化、定型並評分所有這些作業。 

資料分割模型會透過 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 上的兩個新參數來啟用：

+ **input_data_1_partition_by_columns**，指定要作為資料分割依據的資料行。
+ **input_data_1_order_by_columns** 指定要作為排序依據的資料行。 

在本教學課程中，您將了解使用傳統 NYC 計程車範例資料和 R 指令碼的資料分割模型。 資料分割資料行是付款方法。

> [!div class="checklist"]
> * 資料分割是以付款類型 (5) 為基礎。
> * 在每個資料分割上建立和定型模型，並將物件儲存在資料庫中。
> * 使用針對該用途保留的範例資料，預測每個資料分割模型的提示結果機率。

## <a name="prerequisites"></a>Prerequisites
 
若要完成本教學課程，必須具備下列項目：

+ 足夠的系統資源。 資料集很大，且定型作業會耗用大量資源。 可能的話，請使用至少具有 8 GB RAM 的系統。 或者，您可以使用較小的資料集來因應資源條件約束。 縮減資料集的指示是內嵌的。 

+ 適用於 T-SQL 查詢執行的工具，例如 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)，您可以[下載並還原](demo-data-nyctaxi-in-sql.md)至本機資料庫引擎執行個體。 檔案大小約為 90 MB。

+ SQL Server 2019 資料庫引擎執行個體，包含機器學習服務和 R 整合。

+ 本教學課程使用[透過 ODBC 從 R 指令碼對 SQL Server 的回送連線](../connect/loopback-connection.md)。 所以，您需要[為 SQLRUserGroup 建立登入](../security/create-a-login-for-sqlrusergroup.md)。

藉由執行 **`SELECT @@Version`** 作為查詢工具中的 T-SQL 查詢來檢查版本。

藉由傳回目前與您資料庫引擎執行個體一起安裝的所有 R 套件格式正確清單，以檢查 R 套件的可用性：

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

## <a name="connect-to-the-database"></a>連接至資料庫

啟動 Management Studio，並連接至資料庫引擎執行個體。 在 [物件總管] 中，確認 [NYCTaxi_Sample 資料庫](demo-data-nyctaxi-in-sql.md)存在。 

## <a name="create-calculatedistance"></a>建立 CalculateDistance

示範資料庫隨附用來計算距離的純量函式，但我們的預存程序更適合使用資料表值函式。 執行下列指令碼以建立稍後會在[定型步驟](#training-step)中使用的 **CalculateDistance** 函式。

若要確認已建立函式，請檢查 [物件總管] 中 **NYCTaxi_Sample** 資料庫下方的 \Programmability\Functions\Table-valued 函式。

```sql
USE NYCTaxi_sample
GO

SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [dbo].[CalculateDistance] (
    @Lat1 FLOAT
    ,@Long1 FLOAT
    ,@Lat2 FLOAT
    ,@Long2 FLOAT
    )
    -- User-defined function calculates the direct distance between two geographical coordinates.
RETURNS TABLE
AS
RETURN

SELECT COALESCE(3958.75 * ATAN(SQRT(1 - POWER(t.distance, 2)) / nullif(t.distance, 0)), 0) AS direct_distance
FROM (
    VALUES (CAST((SIN(@Lat1 / 57.2958) * SIN(@Lat2 / 57.2958)) + (COS(@Lat1 / 57.2958) * COS(@Lat2 / 57.2958) * COS((@Long2 / 57.2958) - (@Long1 / 57.2958))) AS DECIMAL(28, 10)))
    ) AS t(distance)
GO
 ```

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>定義建立和定型每個資料分割模型的程序

本教學課程會將 R 指令碼包裝在預存程序中。 在此步驟中，您會建立使用 R 建立輸入資料集的預存程序、建立用於預測提示結果的分類模型，然後將模型儲存在資料庫中。

在此指令碼使用的參數輸入中，您會看到 **input_data_1_partition_by_columns** 和 **input_data_1_order_by_columns**。 回想一下，這些參數是進行資料分割模型所使用的機制。 參數會作為輸入傳遞至 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 來處理資料分割，而外部指令碼會針對每個資料分割執行一次。 

針對此預存程序，[使用平行處理原則](#parallel)以加快完成的時間。

執行此指令碼之後，您應該會在 **NYCTaxi_Sample** [物件總管] 資料庫下方的 \Programmability\Stored 程序中，看到 **train_rxLogIt_per_partition**。 您也應該會看到用來儲存模型的新資料表：**dbo.nyctaxi_models**。

```sql
USE NYCTaxi_Sample
GO

CREATE
    OR

ALTER PROCEDURE [dbo].[train_rxLogIt_per_partition] (@input_query NVARCHAR(max))
AS
BEGIN
    DECLARE @start DATETIME2 = SYSDATETIME()
        ,@model_generation_duration FLOAT
        ,@model VARBINARY(max)
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name();

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    # Make sure InputDataSet is not empty. In parallel mode, if one thread gets zero data, an error occurs
    if (nrow(InputDataSet) > 0) {
    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    
    # build classification model to predict a tip outcome
    duration <- system.time(logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet))[3];

    # First, serialize a model to and put it into a database table
    modelbin <- as.raw(serialize(logitObj, NULL));

    # Create the data source. To reduce data size, add rowsPerRead=500000 to cut the dataset by half.
    ds <- RxOdbcData(table="ml_models", connectionString=connStr);

    # Store the model in the database
    model_name <- paste0("nyctaxi.", InputDataSet[1,]$payment_type);
    
    rxWriteObject(ds, model_name, modelbin, version = "v1",
    keyName = "model_name", valueName = "model_object", versionName = "model_version", overwrite = TRUE, serialize = FALSE);
    } 
    
    '
        ,@input_data_1 = @input_query
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@input_data_1_order_by_columns = N'passenger_count'
        ,@parallel = 1
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS NONE
END;
GO
```

<a name="parallel"></a>

### <a name="parallel-execution"></a>平行執行

請注意，[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 輸入包含用來啟用平行處理的 `@parallel=1`。 與舊版不同的是，在 SQL Server 2019 中，設定 `@parallel=1` 會對查詢最佳化工具提供更強的提示，讓平行執行成為更有可能的結果。

根據預設，查詢最佳化工具通常會在具有超過 256 個資料列的資料表上執行 `@parallel=1`，但如果您可以如本指令碼所示來藉由設定 `@parallel=1` 明確地處理此項作業。

> [!Tip]
> 針對定型工作負載，您可以使用 `@parallel` 搭配任何任意的定型指令碼，甚至是使用非 Microsoft-rx 演算法的指令碼。 一般來說，只有 RevoScaleR 演算法 (具有 rx 前置詞) 在 SQL Server 的定型案例中提供平行處理原則。 但是，透過新的參數，您可以平行化呼叫函式的指令碼 (包括開放原始碼 R 函式)，而不是特別使用該功能進行設計。 這是因為資料分割與特定執行緒具有同質性，因此在指令碼中呼叫的所有作業都是以每個資料分割為基礎來執行`thread.`<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>執行程序並定型模型

在本節中，指令碼會定型您在上一個步驟中建立與儲存的模型。 下列範例示範兩種用來定型模型的方法：使用整個資料集或部分資料。 

此步驟會需要一些時間。 定型需要大量運算，需花費數分鐘的時間才能完成。 如果系統資源 (特別是記憶體) 不足以用於負載，則請使用資料的子集。 第二個範例提供語法。

```sql
--Example 1: train on entire dataset
EXEC train_rxLogIt_per_partition N'
SELECT payment_type, tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

```sql
--Example 2: Train on 20 percent of the dataset to expedite processing.
EXEC train_rxLogIt_per_partition N'
  SELECT tipped, payment_type, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance
  FROM dbo.nyctaxi_sample TABLESAMPLE (20 PERCENT) REPEATABLE (98074)
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d
';
GO
```

> [!NOTE]
> 如果您正在執行其他工作負載，且如果您想要將查詢處理限制為只有 2 個核心，您可以將 `OPTION(MAXDOP 2)` 附加至 SELECT 陳述句。

## <a name="check-results"></a>檢查結果

模型資料表中的結果應該是五個不同模型，以五個付款類型所分割的五個資料分割為基礎。 模型位於 **ml_models** 資料來源中。

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>定義預測結果的程序

您可以使用相同的參數來進行評分。 下列範例包含 R 指令碼，該指令碼會針對目前正在處理的資料分割使用正確模型進行評分。

如先前所述，請建立預存程序來包裝 R 程式碼。

```sql
USE NYCTaxi_Sample
GO

-- Stored procedure that scores per partition. 
-- Depending on the partition being processed, a model specific to that partition will be used
CREATE
    OR

ALTER PROCEDURE [dbo].[predict_per_partition]
AS
BEGIN
    DECLARE @predict_duration FLOAT
        ,@instance_name NVARCHAR(100) = @@SERVERNAME
        ,@database_name NVARCHAR(128) = db_name()
        ,@input_query NVARCHAR(max);

    SET @input_query = 'SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance, payment_type
                          FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)
                          CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d'

    EXEC sp_execute_external_script @language = N'R'
        ,@script = 
        N'
    
    if (nrow(InputDataSet) > 0) {

    #Get the partition that is currently being processed
    current_partition <- InputDataSet[1,]$payment_type;

    #Create the SQL query to select the right model
    query_getModel <- paste0("select model_object from ml_models where model_name = ", "''", "nyctaxi.",InputDataSet[1,]$payment_type,"''", ";")
    

    # Define the connection string
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
        
    #Define data source to use for getting the model
    ds <- RxOdbcData(sqlQuery = query_getModel, connectionString = connStr)

    # Load the model
    modelbin <- rxReadObject(ds, deserialize = FALSE)
    # unserialize model
    logitObj <- unserialize(modelbin);

    # predict tipped or not based on model
    predictions <- rxPredict(logitObj, data = InputDataSet, overwrite = TRUE, type = "response", writeModelVars = TRUE
        , extraVarsToWrite = c("payment_type"));        
    OutputDataSet <- predictions
    
    } else {
        OutputDataSet <- data.frame(integer(), InputDataSet[,]);        
    }
    '
        ,@input_data_1 = @input_query
        ,@parallel = 1
        ,@input_data_1_partition_by_columns = N'payment_type'
        ,@params = N'@instance_name nvarchar(100), @database_name nvarchar(128)'
        ,@instance_name = @instance_name
        ,@database_name = @database_name
    WITH RESULT SETS((
                tipped_Pred INT
                ,payment_type VARCHAR(5)
                ,tipped INT
                ,passenger_count INT
                ,trip_distance FLOAT
                ,trip_time_in_secs INT
                ,direct_distance FLOAT
                ));
END;
GO
```

## <a name="create-a-table-to-store-predictions"></a>建立資料表來儲存預測

```sql
CREATE TABLE prediction_results (
    tipped_Pred INT
    ,payment_type VARCHAR(5)
    ,tipped INT
    ,passenger_count INT
    ,trip_distance FLOAT
    ,trip_time_in_secs INT
    ,direct_distance FLOAT
    );

TRUNCATE TABLE prediction_results
GO
```

## <a name="run-the-procedure-and-save-predictions"></a>執行程序並儲存預測

```sql
INSERT INTO prediction_results (
    tipped_Pred
    ,payment_type
    ,tipped
    ,passenger_count
    ,trip_distance
    ,trip_time_in_secs
    ,direct_distance
    )
EXECUTE [predict_per_partition]
GO
```

## <a name="view-predictions"></a>檢視預測

因為會儲存預測，所以可以執行簡單的查詢來傳回結果集。

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已使用 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 來反覆運算分割資料的作業。 如需深入了解如何在預存程序中呼叫外部指令碼，以及如何使用 RevoScaleR 函式，請繼續進行下列教學課程。

> [!div class="nextstepaction"]
> [R 和 SQL Server 的逐步解說](walkthrough-data-science-end-to-end-walkthrough.md)

