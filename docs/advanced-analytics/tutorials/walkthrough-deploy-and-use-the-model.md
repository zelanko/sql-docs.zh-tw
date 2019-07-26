---
title: 在 SQL Server 上部署 R 模型以進行預測
description: 本教學課程示範如何在資料庫內部分析的 SQL Server 上部署 R 模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 96744b15bef03b7d8badc803b1fa5f5de382e64f
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470550"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>部署 R 模型, 並在 SQL Server 中使用 (逐步解說)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在這一課, 您將瞭解如何藉由從預存程式呼叫定型模型, 在生產環境中部署 R 模型。 您可以從 R 或任何支援[!INCLUDE[tsql](../../includes/tsql-md.md)]的應用程式設計語言 (例如C#JAVA、Python 等) 叫用預存程式, 並使用模型來對新的觀察進行預測。

本文示範在計分中使用模型的兩個最常見方式:

> [!div class="checklist"]
> * **批次評分模式**會產生多個預測
> * **個別評分模式**一次產生一個預測

## <a name="batch-scoring"></a>批次評分

建立一個預存程式*PredictTipBatchMode*, 它會產生多個預測, 並傳遞 SQL 查詢或資料表做為輸入。 傳回結果的資料表, 您可以直接插入資料表或寫入檔案。

- 取一組輸入資料做為 SQL 查詢
- 呼叫您在上一課中儲存的定型羅吉斯迴歸模型
- 預測驅動程式取得任何非零提示的機率

1. 在 Management Studio 中, 開啟新的 [查詢] 視窗, 然後執行下列 T-sql 腳本來建立 PredictTipBatchMode 預存程式。
  
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

    + 您可以使用 SELECT 語句, 從 SQL 資料表呼叫預存模型。 此模型會從資料表中取出為**Varbinary (max)** 資料, 並儲存在 SQL 變數 _\@lmodel2_中, 並當做參數*mod*傳遞至系統預存程式[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 當做計分輸入使用的資料會定義為 SQL 查詢, 並在 sql 變數 _\@輸入_中儲存為字串。 從資料庫擷取資料時，它會儲存在名為資料框架*InputDataSet*，這是預設名稱的輸入資料來[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)程序，您可以定義另一個變數的名稱視使用的參數 *_\@input_data_1_name_* 。

    + 為了產生分數, 預存程式會從**RevoScaleR**程式庫呼叫 rxPredict 函數。

    + 傳回值 [*分數*] 是指定模型時, 該驅動程式會取得提示的機率。 (選擇性) 您可以輕鬆地將某種類型的篩選套用至傳回的值, 將傳回值分類為 "tip" 和 "no tip" 群組。  例如, 小於0.5 的機率表示不太可能出現提示。
  
2.  若要在批次模式中呼叫預存程式, 您可以將所需的查詢定義為預存程式的輸入。 以下是 SQL 查詢, 您可以在 SSMS 中執行它來確認它是否正常運作。

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

3. 使用此 R 程式碼, 從 SQL 查詢建立輸入字串:

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @inquery = ", input, sep="");
    ```

4. 若要從 R 執行預存程式, 請呼叫**RODBC**封裝的**sqlQuery**方法, 並使用您稍`conn`早定義的 SQL 連接:

    ```R
    sqlQuery (conn, q);
    ```

    如果您收到 ODBC 錯誤, 請檢查是否有語法錯誤, 以及是否有正確的引號數目。 
    
    如果您收到許可權錯誤, 請確定登入能夠執行預存程式。

## <a name="single-row-scoring"></a>單一資料列計分

個別計分模式一次會產生一個預測, 將一組個別值當做輸入傳遞給預存程式。 這些值會對應至模型中的功能, 而模型會使用它來建立預測, 或產生另一個結果, 例如機率值。 然後, 您可以將該值傳回給應用程式或使用者。

以逐列方式呼叫模型進行預測時, 您會傳遞一組值來代表每個個別案例的功能。 然後, 預存程式會傳回單一預測或機率。 

預存程式*PredictTipSingleMode*會示範這種方法。 它會接受多個代表功能值的參數 (例如, 乘客計數和行程距離)、使用預存 R 模型對這些功能評分, 並輸出 tip 機率。

1. 執行下列 Transact-sql 語句來建立預存程式。

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

2. 在 SQL Server Management Studio 中, 您可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC**程式 (或**執行**) 來呼叫預存程式, 並將必要的輸入傳遞給它。 例如, 請嘗試在 Management Studio 中執行此語句:

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    此處傳入的值分別為變數 _\_乘客 count_、   _\_ \_trip_distance、旅程時間\_(秒_)、  _\_pickup 緯度_、 _pickup\_經度_、 _下車\_緯度_和_下車\_緯度_。

3. 若要從 R 程式碼執行這個相同的呼叫, 您只需要定義包含整個預存程序呼叫的 R 變數, 如下所示:

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    此處傳入的值分別適用于變數_乘客\_計數_、_路程\_距離_、_旅程\_時間\_ \_(秒_)、_取貨\_緯度_、 _pickup\_經度_、_下車\_緯度_和_下車\__ 緯度。

4. 呼叫`sqlQuery` (從**RODBC**封裝) 並傳遞連接字串, 以及包含預存程序呼叫的字串變數。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > Visual Studio R 工具 (RTVS) 提供與 SQL Server 和 R 的絕佳整合。如需更多使用 RODBC 與 SQL Server 連線的範例, 請參閱這篇文章:[使用 SQL Server 和 R](https://docs.microsoft.com/visualstudio/rtvs/sql-server)

## <a name="next-steps"></a>後續步驟

既然您已瞭解如何使用資料並將[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]定型的 R 模型保存至[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 您就應該相對輕鬆地根據此資料集建立新的模型。 例如, 您可能會嘗試建立這些額外的模型:

+ 可預測小費金額的迴歸模型
+ 多元分類模型, 可預測提示為大、中或小型

您可能也會想要探索這些額外的範例和資源:

+ [資料科學案例和解決方案範本](data-science-scenarios-and-solution-templates.md)
+ [資料庫內的進階分析](sqldev-in-database-r-for-sql-developers.md)
+ [Machine Learning Server 操作指南](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server 其他資源](https://docs.microsoft.com//machine-learning-server/resources-more)
