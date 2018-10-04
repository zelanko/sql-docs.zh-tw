---
title: 建立、 定型和計分 R （SQL Server Machine Learning 服務） 中的資料分割為基礎的模型教學課程 |Microsoft Docs
description: 了解如何建立模型、 定型和使用資料分割使用資料分割為基礎的模型化功能，SQL Server 機器學習時以動態方式建立的資料。
ms.custom: sqlseattle
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/02/2018
ms.topic: tutorial
ms.author: heidist
author: HeidiSteen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3289e9f7493b7e5a6377de3491bd5726d557fdf7
ms.sourcegitcommit: 615f8b5063aed679495d92a04ffbe00451d34a11
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48232562"
---
# <a name="tutorial-create-partition-based-models-in-r-on-sql-server"></a>教學課程： 在 SQL Server 上的 R 中建立分割區為基礎的模型
[!INCLUDE[appliesto-ssvnex-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

在 SQL Server 2019，分割區為基礎的模型會是能夠建立並定型模型對資料分割的資料。 分層資料自然地分割成指定的分類配置-例如地區、 日期和時間、 年齡或性別-您可以執行指令碼透過整個資料集，模型、 訓練及評分仍維持不變的資料分割上的能力透過上述所有作業。 

資料分割為基礎的模型上啟用透過兩個新參數[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql):

+ **input_data_1_partition_by_columns**，指定用於資料分割的資料行。
+ **input_data_1_order_by_columns**指定要排序依據的資料行。 

在本教學課程，了解資料分割為基礎的模型，使用傳統的 NYC 計程車範例資料和 R 指令碼。 資料分割資料行是付款方法。

> [!div class="checklist"]
> * 資料分割根據付款類型 (5)。
> * 建立並定型的模型，每個磁碟分割，儲存在資料庫中的物件。
> * 透過每個磁碟分割模型，使用針對該用途保留的範例資料預測小費的結果的機率。

## <a name="prerequisites"></a>先決條件
 
若要完成本教學課程中，您必須擁有下列項目：

+ 足夠的系統資源。 資料集很大，並訓練作業相當耗費資源。 可能的話，請使用具有至少 8 GB RAM 的系統。 或者，您可以使用較小的資料集以解決資源限制。 減少資料集的指示會以內嵌方式。 

+ T-SQL 的工具執行查詢，例如[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。

+ [NYCTaxi_Sample.bak](https://sqlmldoccontent.blob.core.windows.net/sqlml/NYCTaxi_Sample.bak)，您可以[下載並還原](sqldev-download-the-sample-data.md)至您的本機資料庫引擎執行個體。 檔案大小大約是 90 MB。

+ SQL Server 2019 預覽資料庫引擎執行個體，與機器學習服務和 R 的整合。

檢查版本，藉由執行**`SELECT @@Version`** 為 T-SQL 查詢中的查詢工具。 輸出應該是 「 Microsoft SQL Server 2019 (CTP 2.0)-15.0.x"。

檢查可用性的 R 套件，藉由傳回格式正確的所有目前已安裝與您的資料庫引擎執行個體的 R 封裝清單：

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

啟動 Management Studio 並連接到 database engine 執行個體。 在 [物件總管] 中，確認[NYCTaxi_Sample 資料庫](sqldev-download-the-sample-data.md)存在。 

## <a name="create-calculatedistance"></a>建立 CalculateDistance

示範資料庫，隨附於計算距離，但我們更好的預存程序適用於純量函數使用資料表值函式。 執行下列程式碼來建立**CalculateDistance**中所使用的函式[訓練步驟](#training-step)稍後。

若要確認已建立函式，請檢查 \Programmability\Functions\Table-valued 函式，在**NYCTaxi_Sample**物件總管 中的資料庫。

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

## <a name="define-a-procedure-for-creating-and-training-per-partition-models"></a>定義用於建立和每個磁碟分割的定型模型的程序

本教學課程中包裝在預存程序中的 R 指令碼。 在此步驟中，您可以建立的預存程序來建立輸入資料集、 建立分類模型來預測小費的結果，使用 R，然後再將模型儲存在資料庫中。

此指令碼所使用的參數輸入，您會看到**input_data_1_partition_by_columns**並**input_data_1_order_by_columns**。 回想一下，這些參數是所機制分割模型就會發生。 將參數傳遞做為輸入[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)外部指令碼執行一次的每個資料分割的處理序資料分割。 

這個預存程序，[使用平行處理原則](#parallel)更快的時間，以完成。

執行此指令碼之後，您應該會看到**train_rxLogIt_per_partition**下方 \Programmability\Stored 程序中**NYCTaxi_Sample**物件總管 中的資料庫。 您也應該會看到新的資料表，用來儲存模型： **dbo.nyctaxi_models**。

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

請注意， [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)輸入包括 **@parallel= 1**，用來平行處理。 相對於舊版，在 SQL Server 2019，設定 **@parallel= 1**來進行平行執行更有可能的結果，查詢最佳化工具提供更強的提示。

根據預設，查詢最佳化工具通常會進行運作 **@parallel= 1**超過 256 個資料列，但如果您可以處理此明確設定的資料表上 **@parallel= 1**在此所示指令碼。

> [!Tip]
> 您可以使用訓練 workoads **@parallel**任何任意的訓練指令碼，甚至是使用非 Microsoft rx 演算法。 通常，只有 RevoScaleR 演算法 （具有 rx 前置詞） 會提供 SQL Server 中的定型案例中的平行處理原則。 但是，新的參數，您可以平行處理呼叫函式，包括開放原始碼 R 函數，不是明確地使用這項功能設計的指令碼。 這是因為資料分割有特定的執行緒親和性，因此以每個分割區為基礎，在指定的執行緒上執行的指令碼中呼叫的所有作業。

<a name="training-step"></a>

## <a name="run-the-procedure-and-train-the-model"></a>執行程序和定型模型

在本節中，指令碼來定型模型，您建立及儲存上一個步驟中。 下列範例會示範兩種方法來定型您的模型： 使用整個資料集或部分的資料。 

預期此步驟，需要一些時間。 定型會耗用大量運算資源，花幾分鐘才能完成。 如果系統資源，尤其是記憶體不足，無法載入，請使用 資料的子集。 第二個範例提供的語法。

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
> 如果您正在執行其他工作負載，您可以將附加`OPTION(MAXDOP 2)`SELECT 陳述式，如果您想要限制為只是 2 個核心的查詢處理。

## <a name="check-results"></a>檢查結果

在模型資料表中的結果應該是五個不同的模型，根據 依五個的付款類型的五個資料分割。 模型會位於**ml_models**資料來源。

```sql
SELECT *
FROM ml_models
```
 
## <a name="define-a-procedure-for-predicting-outcomes"></a>定義預測結果的程序

您可以使用相同的參數進行評分。 下列範例包含 R 指令碼，將目前正在處理的資料分割使用正確的模型進行評分。

同樣地，建立預存的程序，以包裝您的 R 程式碼。

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

## <a name="run-the-procedure-and-save-predictions"></a>執行程序，並儲存預測

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

因為儲存預測，您可以執行簡單的查詢，以傳回結果集。

```sql
SELECT *
FROM prediction_results;
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已使用[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)至資料分割的資料上反覆運算作業。 針對得更仔細看看呼叫預存程序的外部指令碼，並使用 RevoScaleR 函式，繼續下列教學課程。

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
