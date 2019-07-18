---
title: 部署 SQL Server-SQL Server 機器學習服務預測的 R 模型
description: 示範如何部署 SQL 伺服器上的 R 模型的資料庫內分析的教學課程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e79dd0bce559259863128de1d2490f0fd9197cf1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961690"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>部署 R 模型，並將它用於 SQL Server （逐步解說）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在這一課中，了解如何藉由呼叫預存程序的定型的模型部署在生產環境中的 R 模型。 您可以叫用預存程序，從 R 或任何支援的應用程式設計語言[!INCLUDE[tsql](../../includes/tsql-md.md)](例如C#，Java、 Python 等)，並使用新的觀察值進行預測的模型。

這篇文章會示範使用計分模型的兩個最常見方式：

> [!div class="checklist"]
> * **批次評分模式**會產生多個預測
> * **個別計分模式**一次產生一個預測

## <a name="batch-scoring"></a>批次評分

建立預存程序中， *PredictTipBatchMode*，產生多個預測，傳遞做為輸入的 SQL 查詢或資料表。 的結果會傳回資料表，您可能會直接插入資料表，或寫入檔案。

- 取一組輸入資料做為 SQL 查詢
- 呼叫您在上一課中儲存的定型羅吉斯迴歸模型
- 預測機率驅動程式取得任何非零的秘訣

1. 在 Management Studio 中，開啟新的查詢視窗並執行下列 T-SQL 指令碼建立 PredictTipBatchMode 預存程序。
  
    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipBatchMode')
    DROP PROCEDURE v
    GO

    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @input nvarchar(max)
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

    + 您可以使用 SELECT 陳述式來呼叫預存的模型，從 SQL 資料表。 從資料表擷取模型**varbinary （max)** 儲存在 SQL 變數的資料 _\@lmodel2_，並做為參數傳遞*mod*系統預存程序[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 計分是定義為 SQL 查詢，並儲存為字串，以在 SQL 變數，當做輸入使用的資料 _\@輸入_。 從資料庫擷取資料時，它會儲存在名為資料框架*InputDataSet*，這是預設名稱的輸入資料來[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)程序，您可以定義另一個變數的名稱視使用的參數 * _\@input_data_1_name_* 。

    + 若要產生分數，預存程序呼叫的 rxPredict 函式**RevoScaleR**程式庫。

    + 傳回值，*分數*，是機率，在模型已知時，該驅動程式取得的小費。 （選擇性） 您可以輕鬆地套用某種篩選條件，傳回的值，以將傳回的值分類成 「 提示 」 和 「 沒小費 」 群組中。  例如，機率小於 0.5 表示提示不太可能。
  
2.  若要以批次模式中呼叫預存程序，您可以定義的查詢需要做為預存程序的輸入。 以下是 SQL 查詢中，您可以執行 SSMS，確認它有效。

    ```sql
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

3. 若要建立 SQL 查詢的輸入的字串中使用此 R 程式碼：

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. 若要從 R 中執行預存程序，請呼叫**sqlQuery**方法**RODBC**封裝，然後使用 SQL 連接`conn`您稍早定義：

    ```R
    sqlQuery (conn, q);
    ```

    如果您取得發生 ODBC 錯誤，請檢查語法錯誤，以及是否有正確數目的引號。 
    
    如果您收到權限錯誤，請確定登入具有可執行預存程序。

## <a name="single-row-scoring"></a>單一資料列評分

個別計分模式產生一個預測一次將一組個別的值傳遞至預存程序，做為輸入。 值會對應至功能，在模型中，由模型用來建立預測，或產生其他的結果，例如機率值。 您接著可以將該值傳回給應用程式或使用者。

當呼叫以逐列為基礎的預測模型，您會傳遞一組值代表每個個別案例的功能。 單一預測或機率，則會傳回預存程序。 

預存程序*PredictTipSingleMode*示範此方法。 它會作為輸入多個參數代表特性值 （例如，乘客計數和車程距離）、 評分使用預存的 R 模型，這些功能，並將輸出的小費的機率。

1. 執行下列 TRANSACT-SQL 陳述式來建立預存程序。

    ```sql
    USE [NYCTaxi_Sample]
    GO

    SET ANSI_NULLS ON
    GO
    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type = 'P' AND name = 'PredictTipSingleMode')
    DROP PROCEDURE v
    GO

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

2. 在 SQL Server Management Studio，您可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**程序 (或**EXECUTE**) 來呼叫預存程序中，並將它傳遞必要的輸入。 例如，嘗試在 Management Studio 中執行此陳述式：

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    在這裡傳遞的值分別為變數_乘客\_計數_， _trip_distance_，_車程\_時間\_中\_秒_， _pickup\_緯度_， _pickup\_經度_，_下車\_緯度_，並_下車\_經度_。

3. 若要從 R 程式碼執行這個相同的呼叫，您只需定義 R 變數，其中包含整個預存程序呼叫中的，與下列類似：

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    在這裡傳遞的值分別為變數_乘客\_計數_， _trip\_距離_，_車程\_時間\_中\_秒_， _pickup\_緯度_， _pickup\_經度_，_下車\_緯度_，並_下車\_經度_。

4. 呼叫`sqlQuery`(從**RODBC**封裝) 並傳遞連接字串，以及包含預存程序呼叫的字串變數。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > R Tools for Visual Studio (RTVS) 提供絕佳的整合，使用 SQL Server 和。請參閱本文中的 SQL Server 連接中使用 RODBC 的更多的範例：[使用 SQL Server 和 R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>後續步驟

既然您已了解如何使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料，並將定型的 R 模型，以保存[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，它應該是您建立此資料集為基礎的新模型來說相對輕鬆。 例如，您可能會嘗試建立這些其他的模型：

+ 可預測小費金額的迴歸模型
+ 預測小費大型、 中型或小型的多元分類模型

您也可以探索這些其他範例和資源：

+ [資料科學案例和解決方案範本](data-science-scenarios-and-solution-templates.md)
+ [資料庫內的進階分析](sqldev-in-database-r-for-sql-developers.md)
+ [Machine Learning Server 使用說明指南](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [機器學習服務伺服器的其他資源](https://docs.microsoft.com//machine-learning-server/resources-more)
