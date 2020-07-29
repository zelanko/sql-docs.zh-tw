---
title: R 教學課程：部署模型
description: 本教學課程示範如何在資料庫內分析的 SQL Server 上部署 R 模型。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bdf7446497d242d3cc2773daad0adfa8d3a700e3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781787"
---
# <a name="deploy-the-r-model-and-use-it-in-sql-server-walkthrough"></a>部署 R 模型，並將其用於 SQL Server (逐步解說)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

在本課中，您將了解如何從預存程序呼叫定型模型，以便在實際執行環境中部署 R 模型。 您可以從 R 或任何支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的應用程式設計語言 (如 C#、Java、Python 等) 叫用預存程序，並使用模型進行新的觀察預測。

本文示範在評分中使用模型的兩個最常見方式：

> [!div class="checklist"]
> * **批次評分模式**會產生多個預測
> * **個別評分模式**一次產生一個預測

## <a name="batch-scoring"></a>批次評分

建立一個預存程序 *PredictTipBatchMode*，它會透過傳遞 SQL 查詢或資料表作為輸入，產生多個預測。 系統會傳回結果的資料表，您可以將其直接插入資料表或寫入至檔案。

- 取一組輸入資料做為 SQL 查詢
- 呼叫您在上一課中儲存的定型羅吉斯迴歸模型
- 預測司機獲得非零小費的機率

1. 在 Management Studio 中，開啟新的查詢視窗，然後執行下列 T-SQL 指令碼來建立 PredictTipBatchMode 預存程序。
  
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

    + 您可以使用 SELECT 陳述式，從 SQL 資料表呼叫預存模型。 系統會從資料表擷取模型作為 **varbinary(max)** 資料，儲存在 SQL 變數 _\@lmodel2_ 中，並將其當作 *mod* 參數，傳遞到系統預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

    + 當作評分輸入使用的資料會定義為 SQL 查詢，並以字串形式儲存在 SQL 變數 _\@輸入_中。 從資料庫擷取資料時，它會儲存在名為 *InputDataSet* 的資料框架中，其只是 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 程序中輸入資料的預設名稱；您可以視需要使用參數 _\@input_data_1_name_ 來定義另一個變數名稱。

    + 預存程序會從 **RevoScaleR** 程式庫呼叫 rxPredict 函式來產生分數。

    + 傳回值 *Score* 是在模型已知時，司機獲得小費的機率。 (選擇性) 您可以輕鬆地將某種篩選條件套用到傳回的值，以便將傳回值分類成「有小費」和「沒小費」群組。  例如，機率小於 0.5 表示不太可能有小費。
  
2.  若要在批次模式下呼叫預存程序，您可以將所需的查詢定義為預存程序的輸入。 以下是 SQL 查詢，您可以在 SSMS 中執行該查詢來確認它是否正常運作。

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

3. 使用此 R 程式碼，從 SQL 查詢建立輸入字串：

    ```R
    input <- "N'SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS direct_distance FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a LEFT OUTER JOIN ( SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND  a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'";
    q <- paste("EXEC PredictTipBatchMode @input = ", input, sep="");
    ```

4. 若要從 R 執行預存程序，呼叫 **RODBC** 封裝的 **sqlQuery** 方法，並使用您稍早定義的 SQL 連線 `conn`：

    ```R
    sqlQuery (conn, q);
    ```

    如果您收到 ODBC 錯誤，請檢查是否有語法錯誤，以及是否有正確的引號數目。 
    
    如果您收到權限錯誤，請確定登入能夠執行預存程序。

## <a name="single-row-scoring"></a>單一資料列評分

個別評分模式會將一組個別的值當作輸入傳遞至預存程式，藉此一次會產生一個預測。 這些值會對應至模型中的功能，而模型會使用這些功能來建立預測，或產生另一個結果，例如機率值。 接著，您可以將該值傳回給應用程式或使用者。

以逐列方式呼叫模型進行預測時，您要針對每個個別案例，傳遞一組代表功能的值。 接著，預存程序會傳回單一預測或機率。 

預存程序 *PredictTipSingleMode* 會示範這種方法。 它會採用代表功能值的多個參數 (例如，乘客計數和行程距離) 當作輸入、使用預存 R 模型對這些功能評分，並輸出小費機率。

1. 執行下列 Transact-SQL 陳述式來建立預存程序。

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

2. 在 SQL Server Management Studio 中，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** 程序 (或 **EXECUTE**) 來呼叫預存程序，並將必要的輸入傳遞給它。 例如，請嘗試在 Management Studio 中執行此陳述式：

    ```sql
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

    傳入此處的值分別供 _passenger\_count_、_trip_distance_、_trip\_time\_in\_secs_、_pickup\_latitude_、_pickup\_longitude_、_dropoff\_latitude_ 和 _dropoff\_longitude_ 變數使用。

3. 若要從 R 程式碼執行這個相同的呼叫，您只需定義包含整個預存程序呼叫的 R 變數，如下所示：

    ```R
    q2 = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 ";
    ```

    傳入此處的值分別供 _passenger\_count_、_trip\_distance_、_trip\_time\_in\_secs_、_pickup\_latitude_、_pickup\_longitude_、_dropoff\_latitude_ 和 _dropoff\_longitude_ 變數使用。

4. 呼叫 `sqlQuery` (從 **RODBC** 封裝)，並傳遞連接字串以及包含預存程序呼叫的字串變數。

    ```R
    # predict with stored procedure in single mode
    sqlQuery (conn, q2);
    ```

    >[!TIP]
    > 適用於 Visual Studio 的 R 工具 (RTVS) 提供與 SQL Server 和 R 的絕佳整合。如需使用 RODBC 搭配 SQL Server 連線的其他範例，請參閱以下文章：[使用 SQL Server 和 R](https://docs.microsoft.com/visualstudio/rtvs/sql-server) \(部分機器翻譯\)

## <a name="next-steps"></a>後續步驟

既然您已經了解如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料並將定型的 R 模型保存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，對您來說，根據此資料集建立新的模型應該相對輕鬆。 例如，您可以嘗試建立下列額外的模型︰

+ 可預測小費金額的迴歸模型
+ 預測小費金額為高、中或低的多元分類模型

您也可以探索下列額外的範例和資源：

+ [資料科學案例和解決方案範本](data-science-scenarios-and-solution-templates.md)
+ [資料庫內的進階分析](sqldev-in-database-r-for-sql-developers.md)
+ [Machine Learning Server 操作指南](https://docs.microsoft.com/machine-learning-server/r/how-to-introduction)
+ [Machine Learning Server 其他資源](https://docs.microsoft.com//machine-learning-server/resources-more)
