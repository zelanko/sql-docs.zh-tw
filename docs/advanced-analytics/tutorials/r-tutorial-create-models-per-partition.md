---
title: 在 R 中建立、定型和評分以資料分割為基礎之模型的教學課程
description: 瞭解如何在使用 SQL Server 機器學習服務的分割型模型化能力時, 針對動態建立的資料分割、定型和使用。
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/27/2019
ms.topic: tutorial
ms.author: davidph
author: dphansen
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 024ddc72ae2b0a2c443546148a66d0fa85060cb6
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469192"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>教學課程：在 SQL Server 上的 R 中建立以資料分割為基礎的模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在 SQL Server 2019 中, 分割型模型化是透過分割資料建立模型並將其定型的能力。 針對自然分割成指定分類配置的分層資料 (例如地理區域、日期和時間、年齡或性別), 您可以在整個資料集上執行腳本, 並能夠對維持不變的分割區進行模型、定型和評分所有這些作業。 

以分割為基礎的模型會透過[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)上的兩個新參數來啟用:

+ **input_data_1_partition_by_columns**, 指定要做為分割依據的資料行。
+ **input_data_1_order_by_columns**指定排序依據的資料行。 

在本教學課程中, 您將瞭解使用傳統 NYC 計程車範例資料和 R 腳本的資料分割型模型化。 資料分割資料行是付款方法。

> [!div class="checklist"]
> * 磁碟分割是以付款類型 (5) 為基礎。
> * 在每個資料分割上建立和定型模型, 並將物件儲存在資料庫中。
> * 使用針對該用途保留的範例資料, 預測每個資料分割模型的 tip 結果機率。

## <a name="prerequisites"></a>先決條件
 
若要完成本教學課程, 您必須具備下列各項:

+ 足夠的系統資源。 資料集很大, 而定型作業會耗用大量資源。 可能的話, 請使用至少具有 8 GB RAM 的系統。 或者, 您可以使用較小的資料集來解決資源條件約束。 縮減資料集的指示是內嵌的。 

+ 適用于 T-SQL 查詢執行的工具, 例如[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

+ [NYCTaxi_Sample](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak), 您可以[下載並還原](demo-data-nyctaxi-in-sql.md)至您的本機資料庫引擎實例。 檔案大小大約是 90 MB。

+ SQL Server 2019 preview 資料庫引擎實例, 具有 Machine Learning 服務和 R 整合。

藉由在查詢 **`SELECT @@Version`** 工具中以 t-SQL 查詢的形式執行來檢查版本。 輸出應該是 "Microsoft SQL Server 2019 (CTP 2.4)-15.0. x"。

藉由傳回目前與您的 database engine 實例一起安裝的所有 R 套件格式正確的清單, 檢查 R 封裝的可用性:

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

## <a name="connect-to-the-database"></a>連接到資料庫

啟動 Management Studio 並連接到 database engine 實例。 在物件總管中, 確認[NYCTaxi_Sample 資料庫](demo-data-nyctaxi-in-sql.md)存在。 

## <a name="create-calculatedistance"></a>建立 CalculateDistance

示範資料庫隨附用來計算距離的純量函數, 但我們的預存程式更適合使用資料表值函式。 執行下列腳本, 以建立稍後在[定型步驟](#training-step)中使用的**CalculateDistance**函數。

若要確認已建立函式, 請在物件總管中, 檢查**NYCTaxi_Sample**資料庫下的 \Programmability\Functions\Table-valued 函數。

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

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>定義建立和定型每個資料分割模型的程式

本教學課程會將 R 腳本包裝在預存程式中。 在此步驟中, 您會建立使用 R 建立輸入資料集的預存程式、建立用於預測 tip 結果的分類模型, 然後將模型儲存在資料庫中。

在此腳本使用的參數輸入中, 您會看到**input_data_1_partition_by_columns**和**input_data_1_order_by_columns**。 回想一下, 這些參數是進行分割模型化所使用的機制。 參數會當做輸入傳遞至[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) , 以處理每個分割區執行一次之外部腳本的資料分割。 

針對此預存程式, 請[使用平行](#parallel)處理來加快完成的時間。

執行此腳本之後, 您應該會在物件總管的**NYCTaxi_Sample**資料庫下的 \Programmability\Stored 程式中看到**train_rxLogIt_per_partition** 。 您也應該會看到用來儲存模型的新資料表: **dbo. nyctaxi_models**。

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

請注意, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)輸入包括 **@parallel= 1**, 用來啟用平行處理。 與舊版不同的是, 在 SQL Server 2019 中, 設定 **@parallel= 1**會對查詢最佳化工具提供更強的提示, 讓平行執行更有可能的結果。

根據預設, 查詢最佳化工具通常會在具有超過256個數據列的資料表上操作 **@parallel= 1** , 但如果您可以藉由設定 **@parallel= 1**明確處理此作業, 如此腳本所示。

> [!Tip]
> 針對定型 workoads, 您可以使用 **@parallel** 搭配任何任意定型腳本, 甚至是使用非 Microsoft rx 演算法的程式碼。 一般來說, 只有 RevoScaleR 演算法 (具有 rx 前置詞) 在 SQL Server 的定型案例中提供平行處理。 但是有了新的參數, 您就可以平行處理呼叫函式的腳本, 包括開放原始碼 R 函數, 而不是特別使用該功能進行設計。 這是因為分割區與特定執行緒具有相似性, 因此在腳本中呼叫的所有作業都會在指定的執行緒上以每個分割區為基礎執行。

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>執行程式並訓練模型

在本節中, 腳本會訓練您在上一個步驟中建立並儲存的模型。 下列範例示範兩種用來定型模型的方法: 使用整個資料集或部分資料。 

預期此步驟需要一些時間。 訓練需要大量運算, 花費數分鐘的時間才能完成。 如果系統資源 (特別是記憶體) 不足以進行負載, 請使用資料的子集。 第二個範例會提供語法。

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
> 如果您正在執行其他工作負載, 如果您`OPTION(MAXDOP 2)`想要將查詢處理限制為只有2個核心, 您可以附加至 SELECT 語句。

## <a name="check-results"></a>檢查結果

[模型] 資料表中的結果應該是五個不同的模型, 以五個付款類型分割的五個數據分割為基礎。 模型位於**ml_models**資料來源中。

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>定義預測結果的程式

您可以使用相同的參數來進行計分。 下列範例包含 R 腳本, 它會針對目前正在處理的資料分割, 使用正確的模型進行評分。

如先前所述, 建立預存程式來包裝 R 程式碼。

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

## <a name="run-the-procedure-and-save-predictions"></a>執行程式並儲存預測

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

## <a name="view-predictions"></a>查看預測

因為會儲存預測, 所以您可以執行簡單的查詢來傳回結果集。

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>後續步驟

在本教學課程中, 您已使用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)來反覆運算分割資料的作業。 如需深入瞭解如何在預存程式中呼叫外部腳本, 以及如何使用 RevoScaleR 函數, 請繼續進行下列教學課程。

> [!div class="nextstepaction"]
> [R 和 SQL Server 的逐步解說](walkthrough-data-science-end-to-end-walkthrough.md)

<!--
## Old intro

**(Not for production workloads)**

One of the more common approaches for executing R or Python code on SQL data is providing script as an input parameter to the [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) stored procedure. In this CTP release, SQL Server 2019 adds new parameters to `sp_execute_external_script` to process partitions with the external script executing once for every partition:

| Parameter | Usage |
|-----------|-------|
| **input_data_1_partition_by_columns** | Specifies which columns to partition by. |
| **input_data_1_order_by_columns** | Specifies which columns to order by.  |

Partitions are an organizational mechanism for stratified data that naturally segments into a given classification scheme. Common examples include partitioning by geographic region, by date and time, by age or gender, and so forth. Given the existence of partitioned data, you might want to execute script over the entire data set, with the ability to model, train, and score partitions that remain intact over all these operations. Calling `sp_execute_external_script` with the new parameters allows you to do just that.

You can run this operation in parallel by combining `partition_by` with `@parallel`. If the input query can be parallelized, set `@parallel=1` as part of your arguments to `sp_execute_external_script`. By default, the query optimizer operates under `@parallel=1` on tables having more than 256 rows.

When the scenario is training, one advantage is that any arbitrary training script, even those using non-Microsoft-rx algorithms, can be parallelized by also using the @parallel parameter. Typically, you would have to use RevoScaleR algorithms (with the rx prefix) to obtain parallelism in training scenarios in SQL Server. But with the new parameter, you can parallelize a script that calls functions not specifically engineered with that capability.
-->
