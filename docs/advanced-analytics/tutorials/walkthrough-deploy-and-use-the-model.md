---
title: "部署 R 模型，並將它用於 SQL （逐步解說） |Microsoft 文件"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e1f0d2f1a003b54856645dd4ec740de64464436b
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="deploy-the-r-model-and-use-it-in-sql"></a>部署 R 模型，並將它用於 SQL

在這一課，您使用 R 模型在實際執行環境中，從預存程序呼叫已定型的模型。 您可以再叫用預存程序，從 R 或任何支援的應用程式設計語言[!INCLUDE[tsql](../../includes/tsql-md.md)]（例如 C#、 Java、 Python 等），要使用模型來做出新的觀察值。

這個範例示範兩個最常見方式，並使用計分模型：

- **批次計分模式**您需要建立多個預測的速度非常快，藉由傳遞 SQL 查詢或資料表做為輸入時，會使用。 的結果會傳回資料表，您可能會直接插入資料表，或寫入至檔案。

- **個別的計分模式**您需要一次建立一個預測時，會使用。 您將一組個別的值傳遞至預存程序時。 值會對應至功能，在模型中，此模型會使用來建立預測，或產生另一個結果，例如機率值。 您接著可以將該值傳回給應用程式或使用者。

## <a name="batch-scoring"></a>批次計分

您一開始執行 PowerShell 指令碼時，所建立的批次計分的預存程序。 這個預存程序， *PredictTipBatchMode*，會進行下列作業：

- 取一組輸入資料做為 SQL 查詢
- 呼叫您在上一課中儲存的定型羅吉斯迴歸模型
- 預測的機率，驅動程式會取得任何非零的秘訣

1. 請花幾分鐘的指令碼的預存程序中，瀏覽*PredictTipBatchMode*。 它說明如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]來運作模型的數個層面。
  
    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipBatchMode]
    @input nvarchar(max)
    AS
    BEGIN
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  FROM nyc_taxi_models);
      EXEC sp_execute_external_script @language = N'R',
         @script = N'
           mod <- unserialize(as.raw(model));
           print(summary(mod))
           OutputDataSet<-rxPredict(modelObject = mod,
             data = InputDataSet,
             outData = NULL,
             predVarNames = "Score", type = "response",
             writeModelVars = FALSE, overwrite = TRUE);
           str(OutputDataSet)
           print(OutputDataSet)',
      @input_data_1 = @input,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

    + 您可以使用 SELECT 陳述式來呼叫預存的模型，從 SQL 資料表。 模型會從資料表擷取**varbinary （max)** SQL 變數中儲存的資料 _@lmodel2_ ，並做為參數傳遞*mod*儲存系統程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 當做輸入使用的計分做為 SQL 查詢定義及儲存 SQL 變數以字串形式的資料 _@input_ 。 從資料庫擷取資料時，它會儲存在資料框架稱為*InputDataSet*，這是預設名稱的輸入資料與[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)程序，您可以定義如果需要使用參數的其他變數名稱  *_@input_data_1_name_*  。

    + 預存程序會從 `rxPredict` RevoScaleR **程式庫呼叫** 函數以產生分數。

    + 傳回值，*分數*，機率給定模型，該驅動程式會取得提示。 （選擇性） 可以輕鬆地套用某種類型的篩選器來分類成 「 提示 」 和 「 不提示 」 群組的傳回值傳回的值。  例如，機率小於 0.5 表示提示不太可能。
  
2.  若要在批次模式中呼叫預存程序，您可以定義的查詢需要做為預存程序的輸入。 以下是 SQL 查詢。您可以確認它運作的 SSMS 中執行它。

    ```SQL
    SELECT TOP 10
      a.passenger_count AS passenger_count,
      a.trip_time_in_secs AS trip_time_in_secs,
      a.trip_distance AS trip_distance,
      a.dropoff_datetime AS dropoff_datetime,
      dbo.fnCalculateDistance( pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance
      FROM 
        (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude 
        FROM nyctaxi_sample)a 
      LEFT OUTER JOIN
      ( SELECT medallion, hack_license, pickup_datetime
      FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b
      ON a.medallion=b.medallion
      AND a.hack_license=b.hack_license
      AND a.pickup_datetime=b.pickup_datetime
      WHERE b.medallion is null
    ```

3. 若要建立 SQL 查詢從輸入的字串中使用此 R 程式碼：

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. 若要從 R 執行預存程序，呼叫**sqlQuery**方法**RODBC**封裝，並使用 SQL 連線`conn`先前定義：

    ```R
    sqlQuery (conn, q);
    ```

    如果您收到發生 ODBC 錯誤，請檢查查詢語法，以及您是否擁有正確的數量的引號。 
    
    如果您收到權限錯誤，請確定登入具有執行預存程序的能力。

## <a name="single-row-scoring"></a>單一資料列計分

在呼叫時以逐列為基礎的預測模型，您會傳遞一組值代表每個個別案例的功能。 單一預測或機率，然後傳回預存程序。 

預存程序*PredictTipSingleMode*示範這種方法。 它會採用做為輸入多個參數代表功能的值 （例如，旅客計數和旅行距離），分數使用預存的 R 模型，這些功能，並將輸出提示機率。

1. 如果預存程序*PredictTipSingleMode*未建立初始的 PowerShell 指令碼，您可以執行下列 TRANSACT-SQL 陳述式，立即建立。

    ```tsql
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0,
    @trip_distance float = 0,
    @trip_time_in_secs int = 0,
    @pickup_latitude float = 0,
    @pickup_longitude float = 0,
    @dropoff_latitude float = 0,
    @dropoff_longitude float = 0
    AS
    BEGIN
      DECLARE @inquery nvarchar(max) = N'
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs, @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)'
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);

      EXEC sp_execute_external_script @language = N'R',  @script = N'
            mod <- unserialize(as.raw(model));
            print(summary(mod))
            OutputDataSet<-rxPredict(
              modelObject = mod,
              data = InputDataSet,
              outData = NULL,
              predVarNames = "Score",
              type = "response",
              writeModelVars = FALSE,
              overwrite = TRUE);
            str(OutputDataSet)
            print(OutputDataSet)
            ',
      @input_data_1 = @inquery,
      @params = N'
      -- passthrough columns
      @model varbinary(max) ,
      @passenger_count int ,
      @trip_distance float ,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      -- mapped variables
      @model = @lmodel2 ,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance ,
      @trip_time_in_secs=@trip_time_in_secs ,
      @pickup_latitude=@pickup_latitude ,
      @pickup_longitude=@pickup_longitude ,
      @dropoff_latitude=@dropoff_latitude ,
      @dropoff_longitude=@dropoff_longitude
      WITH RESULT SETS ((Score float));
    END
    ```

2. 在 SQL Server Management Studio，您可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**程序 (或**EXECUTE**) 來呼叫預存程序，並將它傳遞必要的輸入。 例如，嘗試在 Management Studio 中執行此陳述式：

    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    在這裡傳遞的值分別是變數_旅客\_計數_， _trip_distance_，_路線\_時間\_中\_秒_，_收取\_緯度_，_收取\_經度_， _dropoff\_緯度_，和_dropoff\_經度_。

3. 若要執行這個相同的呼叫 R 程式碼，只需定義 R 變數包含整個預存程序呼叫，如下所示：

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    在這裡傳遞的值分別是變數_旅客\_計數_，_路線\_距離_，_路線\_時間\_中\_秒_，_收取\_緯度_，_收取\_經度_， _dropoff\_緯度_，和_dropoff\_經度_。

4. 呼叫`sqlQuery`(從**RODBC**封裝) 並傳遞連接字串，以及包含預存程序呼叫的字串變數。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R Tools for Visual Studio (RTVS) 提供絕佳的整合與 SQL Server 和。請參閱本文章的 SQL Server 連接搭配使用 RODBC 相關範例：[使用 R 與 SQL Server](https://docs.microsoft.com/en-us/visualstudio/rtvs/sql-server)

## <a name="summary"></a>摘要

既然您已經學會如何使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料，並將定型的 R 模型，以保存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它應該是相當容易為您建立新的模型根據此資料集。 例如，您可能會嘗試建立這些其他的模型：

- 可預測小費金額的迴歸模型

- 可預測之提示是大型、 中型或小型的多級分類模型

我們也建議您查看一些其他範例和資源：

+ [資料科學案例和解決方案範本](data-science-scenarios-and-solution-templates.md)

+ [資料庫內的進階分析](sqldev-in-database-r-for-sql-developers.md)

+ [Microsoft R - 深入探討資料分析](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)

+ [其他資源](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)

## <a name="previous-lesson"></a>上一課

[建立 R 模型，並將它儲存在 SQL Server](walkthrough-build-and-save-the-model.md)

## <a name="next-steps"></a>後續的步驟

[SQL Server R 教學課程](sql-server-r-tutorials.md)

[如何建立預存程序中使用 sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)
