---
title: 第4課使用 R 模型預測潛在結果
description: 示範如何使用 T-sql 函式在 SQL Server 預存程式中讓內嵌 R 腳本的教學課程
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abacf3c384430417dbf0630f2f8dcd8adff68259
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714732"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>第 4 課：在預存程式中使用 R embedded 執行預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是有關如何在 SQL Server 中使用 R 的 SQL 開發人員教學課程的一部分。

在此步驟中, 您將瞭解如何針對新的觀察使用模型來預測潛在的結果。 此模型會包裝在預存程式中, 可由其他應用程式直接呼叫。 本逐步解說將示範數種執行計分的方式:

- **批次評分模式**:使用 SELECT 查詢做為預存程式的輸入。 此預存程序會傳回對應至輸入案例的觀察值資料表。

- **個別評分模式**:傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。

首先，讓我們來看看計分的一般運作方式。

## <a name="basic-scoring"></a>基本評分

預存程式**RxPredict**說明將 RevoScaleR RxPredict 呼叫包裝在預存程式中的基本語法。

```sql
CREATE PROCEDURE [dbo].[RxPredict] (@model varchar(250), @inquery nvarchar(max))
AS 
BEGIN 

DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);  
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

+ SELECT 語句會從資料庫取得序列化模型, 並將模型儲存在 r 變數`mod`中, 以使用 r 進行進一步的處理。

+ 計分的新案例是從[!INCLUDE[tsql](../../includes/tsql-md.md)]中`@inquery`指定的查詢取得, 這是預存程式的第一個參數。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。 此資料框架會傳遞至[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)中的[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函數, 以產生分數。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    因為 data.frame 可以包含單一資料列，所以您可以使用相同的程式碼進行批次或單一計分。
  
+ `rxPredict`函數所傳回的值為**float** , 代表驅動程式取得任何數量之秘訣的機率。

## <a name="batch-scoring-a-list-of-predictions"></a>批次評分 (預測清單)

較常見的案例是在批次模式中產生多個觀察的預測。 在此步驟中, 我們將瞭解批次計分的運作方式。

1.  一開始請先取得較小的輸入資料集來使用。 此查詢會建立「前 10 趟」車程的清單，其中包含乘客計數及進行預測所需的其他特徵。
  
    ```sql
    SELECT TOP 10 a.passenger_count AS passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance
    
    FROM (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample)a

    LEFT OUTER JOIN

    (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052)    )b

    ON a.medallion=b.medallion AND a.hack_license=b.hack_license 
    AND a.pickup_datetime=b.pickup_datetime
    WHERE b.medallion IS NULL
    ```

    **範例結果**
    
    ```sql
    passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance
    1  283 0.7 2013-03-27 14:54:50.000   0.5427964547
    1  289 0.7 2013-02-24 12:55:29.000   0.3797099614
    1  214 0.7 2013-06-26 13:28:10.000   0.6970098661
    ```

2. 在中[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], 建立名為**RxPredictBatchOutput**的預存程式。

    ```sql
    CREATE PROCEDURE [dbo].[RxPredictBatchOutput] (@model varchar(250), @inquery nvarchar(max))
    AS
    BEGIN
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
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

3.  在變數中提供查詢文字, 並將它當做參數傳遞給預存程式:

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
預存程式會傳回一系列的值, 代表前10次行程的預測。 不過, 頂尖行程也是以相對較短的行程距離進行的單次乘客行程, 驅動程式不太可能會收到提示。
  

> [!TIP]
> 
> 您也可以傳回預測的機率分數, 然後將 WHERE 子句套用至 [_分數_] 資料行值, 將分數分類為「可能是秘訣」或「不太可能提示」, 而不只是傳回「是-提示」和「無提示」結果, 而是使用臨界值, 例如0.5 或0.7。 雖然此步驟未包含在預存程序中，但實作起來並不難。

## <a name="single-row-scoring-of-multiple-inputs"></a>多個輸入的單一資料列評分

有時候您會想要傳入多個輸入值, 並根據這些值取得單一預測。 例如, 您可以將 Excel 工作表、web 應用程式或 Reporting Services 報表設定為呼叫預存程式, 並提供這些應用程式的使用者輸入或選取的輸入。

在本節中, 您將瞭解如何使用接受多個輸入的預存程式 (例如乘客計數、路程距離等等) 來建立單一預測。 預存程式會根據先前儲存的 R 模型來建立分數。
  
如果您從外部應用程式呼叫預存程式, 請確定資料符合 R 模型的需求。 這可能包括確保輸入資料可轉型或轉換成 R 資料類型，或是驗證資料類型和資料長度。 

1. 建立預存程式**RxPredictSingleRow**。
  
    ```sql
    CREATE PROCEDURE [dbo].[RxPredictSingleRow] @model varchar(50), @passenger_count int = 0, @trip_distance float = 0, @trip_time_in_secs int = 0, @pickup_latitude float = 0, @pickup_longitude float = 0, @dropoff_latitude float = 0, @dropoff_longitude float = 0
    AS
    BEGIN
    DECLARE @inquery nvarchar(max) = N'SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, @trip_distance, @trip_time_in_secs,  @pickup_latitude, @pickup_longitude, @dropoff_latitude, @dropoff_longitude)';
    DECLARE @lmodel2 varbinary(max) = (SELECT model FROM nyc_taxi_models WHERE name = @model);
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

2. 請以手動方式提供值來試試看。
  
    開啟新的**查詢**視窗, 並呼叫預存程式, 並提供每個參數的值。 這些參數代表模型所使用的功能資料行, 而且是必要的。

    ```sql
    EXEC [dbo].[RxPredictSingleRow] @model = 'RxTrainLogit_model',
    @passenger_count = 1,
    @trip_distance = 2.5,
    @trip_time_in_secs = 631,
    @pickup_latitude = 40.763958,
    @pickup_longitude = -73.973373,
    @dropoff_latitude =  40.782139,
    @dropoff_longitude = -73.977303
    ```

    或者,[在預存](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters)程式中使用這個較短的形式支援參數:
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 結果表示在這些前10次行程中取得提示的機率很低 (零), 因為所有的乘客都是相對較短的距離。

## <a name="conclusions"></a>結論

這總結教學課程。 既然您已瞭解如何在預存程式中內嵌 R 程式碼, 您可以擴充這些實務來建立自己的模型。 與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的整合可讓您更輕鬆地部署 R 模型進行預測，並納入模型重新定型作為企業資料工作流程的一部分。

## <a name="previous-lesson"></a>上一課

[第 3 課：使用 T-sql 定型及儲存 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
