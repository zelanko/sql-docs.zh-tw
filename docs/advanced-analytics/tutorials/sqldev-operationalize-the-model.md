---
title: "第 6 課： 實施 R 模型 |Microsoft 文件"
ms.custom: 
ms.date: 11/10/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs:
- R
- TSQL
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: dd1ea47b8b687f371e4f4656e5953f72654e153d
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/11/2017
---
# <a name="lesson-6-operationalize-the-r-model"></a>第 6 課： 實施 R 模型

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在此步驟中，您學會*實施*使用預存程序的模型。 您可以透過其他應用程式直接呼叫此預存程序，對新的觀察值進行預測。 逐步解說將示範兩種執行預存程序中使用 R 模型的計分方式：

- **批次計分模式**: SELECT 查詢做為預存程序的輸入。 此預存程序會傳回對應至輸入案例的觀察值資料表。

- **個別計分模式**︰傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。

首先，讓我們來看看計分的一般運作方式。

## <a name="basic-scoring"></a>基本分數

預存程序 _PredictTip_ 說明將預測呼叫包裝在預存程序中的基本語法。

```SQL
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max) 
AS 
BEGIN 
  
DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);  
EXEC sp_execute_external_script @language = N'R',
  @script = N' 
    mod <- unserialize(as.raw(model)); 
    print(summary(mod)) 
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE); 
    str(OutputDataSet) 
    print(OutputDataSet) 
    ', 
  @input_data_1 = @inquery, 
  @params = N'@model varbinary(max)',
  @model = @lmodel2 
  WITH RESULT SETS ((Score float));
END
GO
```

+ SELECT 陳述式從資料庫中，取得序列化的模型，並將模型存放至 R 變數`mod`做進一步的處理使用。

+ 計分的新案例所取自[!INCLUDE[tsql](../../includes/tsql-md.md)]中指定查詢`@inquery`，預存程序的第一個參數。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。 此資料框架會傳遞至 R 中的 `rxPredict` 函數，再由此函數產生分數。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    因為 data.frame 可以包含單一資料列，所以您可以使用相同的程式碼進行批次或單一計分。
  
+ 所傳回的值`rxPredict`函式是**float**表示驅動程式取得尖端任何數量的機率。

## <a name="batch-scoring"></a>批次計分

現在讓我們來看看批次計分的運作方式。

1.  請先取得要使用的一小組輸入資料。 此查詢會建立「前 10 趟」車程的清單，其中包含乘客計數及進行預測所需的其他特徵。
  
    ```SQL
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **範例結果**
    
    ```
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

    此查詢可以做為預存程序中，輸入_PredictTipBatchMode_下載的一部分提供。

2. 花點時間檢閱程式碼的預存程序_PredictTipBatchMode_中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

    ```SQL
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
    EXEC sp_execute_external_script 
      @language = N'R',
      @script = N'
        mod <- unserialize(as.raw(model));
        print(summary(mod))
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);
        str(OutputDataSet)
        print(OutputDataSet)
      ',
      @input_data_1 = @inquery,
      @params = N'@model varbinary(max)',
      @model = @lmodel2
      WITH RESULT SETS ((Score float));
    END
    ```

3.  提供在變數中的查詢文字，並將它當做參數傳遞至預存程序：

    ```SQL
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'

    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[PredictTip] @inquery = @query_string;
    ```
  
4. 預存程序傳回一連串的數值，代表前 10 個往返的每個預測。 不過，最上層往返也是相對較短的旅行距離，驅動程式是不太可能取得秘訣與單一旅客往返。
  

> [!TIP]
> 
> 而不是傳回"yes 提示 」 和 「 無提示 」 結果，您可能也會傳回預測的機率分數，然後套用 WHERE 子句，以_分數_資料行值來分類將分數視為 「 可能會提示"或"不太可能提示 」，使用的臨界值，例如 0.5 或 0.7。 雖然此步驟未包含在預存程序中，但實作起來並不難。

## <a name="single-row-scoring"></a>單一資料列計分

有時候，您會想要從應用程式傳入個別值，並根據這些值取得單一結果。 例如，您可以設定 Excel 工作表、Web 應用程式或 Reporting Services 報表來呼叫預存程序，並提供使用者鍵入或選取的輸入。

在本節中，您可以了解如何建立單一預測使用預存程序。

1. 請花幾分鐘檢閱下載時已隨附之預存程序 _PredictTipSingleMode_的程式碼。
  
    ```SQL
    CREATE PROCEDURE [dbo].[PredictTipSingleMode] @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model FROM nyc_taxi_models);
    EXEC sp_execute_external_script  
      @language = N'R',
      @script = N'  
        mod <- unserialize(as.raw(model));  
        print(summary(mod));  
        OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
        str(OutputDataSet);
        print(OutputDataSet); 
        ',  
      @input_data_1 = @inquery,  
      @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float', @model = @lmodel2, @passenger_count =@passenger_count, @trip_distance=@trip_distance, @trip_time_in_secs=@trip_time_in_secs, @pickup_latitude=@pickup_latitude, @pickup_longitude=@pickup_longitude, @dropoff_latitude=@dropoff_latitude, @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
    END
    ```
  
    - 此預存程序接受多個單一值作為輸入，例如乘客計數、車程距離等等。
  
        如果您從外部應用程式呼叫預存程序，請確定符合需求的 R 模型的資料。 這可能包括確保輸入資料可轉型或轉換成 R 資料類型，或是驗證資料類型和資料長度。 
  
    -   此預存程序會根據儲存的 R 模型建立分數。
  
2. 請以手動方式提供值來試試看。
  
    開啟新**查詢**視窗中，並呼叫預存程序，針對每個參數提供值。 參數代表模型所使用的特徵資料行，而且不需要。

    ```
    EXEC [dbo].[PredictTipSingleMode] @passenger_count = 0,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = 73.977303
    ```

    或者，您也可以使用此較短的表單支援[預存程序的參數](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```SQL
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 結果會指出取得提示的機率是低這些前 10 個往返的因為所有透過相對較短的距離是單一旅客往返。

## <a name="conclusions"></a>結論

這總結教學課程。 既然您已經學會如何將 R 程式碼內嵌在預存程序，您可以擴充這些作法來建立您自己的模型。 與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的整合可讓您更輕鬆地部署 R 模型進行預測，並納入模型重新定型作為企業資料工作流程的一部分。

## <a name="previous-lesson"></a>上一課

[第 5 課： 訓練並儲存使用 T-SQL R 模型](../r/sqldev-train-and-save-a-model-using-t-sql.md)
