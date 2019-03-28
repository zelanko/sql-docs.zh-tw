---
title: 使用 R 模型-SQL Server 機器學習的第 4 課預測潛在結果
description: 教學課程示範如何實作 SQL Server 中的內嵌的 R 指令碼預存程序的 T-SQL 函數
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/16/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4e74f587177c31f55c952eb06ccb8a7e8960c93a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511585"
---
# <a name="lesson-4-run-predictions-using-r-embedded-in-a-stored-procedure"></a>第 4 課：執行使用內嵌在預存程序中 R 的預測
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是有關如何在 SQL Server 中使用 R 的 SQL 開發人員的教學課程的一部分。

在此步驟中，您了解如何使用針對新的觀察模型來預測可能的結果。 模型被包裝在其他應用程式可以直接呼叫此預存程序。 本逐步解說示範數種方式可執行評分：

- **批次評分模式**:使用 SELECT 查詢做為預存程序的輸入。 此預存程序會傳回對應至輸入案例的觀察值資料表。

- **個別計分模式**:將一組個別參數值傳遞做為輸入。  此預存程序會傳回單一資料列或值。

首先，讓我們來看看計分的一般運作方式。

## <a name="basic-scoring"></a>基本計分

預存程序**RxPredict**說明 RevoScaleR rxPredict 呼叫包裝在預存程序的基本語法。

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

+ SELECT 陳述式從資料庫取得序列化的模型，並將模型儲存在 R 變數`mod`針對使用 r 進一步處理

+ 用於評分的新案例所取自[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢中指定`@inquery`，預存程序的第一個參數。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet`中。 此資料框架會傳遞至[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函式中[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)，如此就會產生分數。
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL, predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`
  
    因為 data.frame 可以包含單一資料列，所以您可以使用相同的程式碼進行批次或單一計分。
  
+ 所傳回的值`rxPredict`函式**float**表示驅動程式取得任何數量的小費的機率。

## <a name="batch-scoring-a-list-of-predictions"></a>批次評分 （預測的清單）

更常見的案例是以批次模式產生多個觀察值的預測。 在此步驟中，我們來看批次計分的運作方式。

1.  從取得較小的要使用的輸入資料集開始。 此查詢會建立「前 10 趟」車程的清單，其中包含乘客計數及進行預測所需的其他特徵。
  
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

2. 建立呼叫預存程序**RxPredictBatchOutput**在[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]。

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

3.  提供在變數中的查詢文字，並將它做為參數傳遞至預存程序：

    ```sql
    -- Define the input data
    DECLARE @query_string nvarchar(max)
    SET @query_string='SELECT TOP 10 a.passenger_count as passenger_count, a.trip_time_in_secs AS trip_time_in_secs, a.trip_distance AS trip_distance, a.dropoff_datetime AS dropoff_datetime, dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) AS direct_distance FROM  (SELECT medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance, dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude FROM nyctaxi_sample  )a   LEFT OUTER JOIN (SELECT medallion, hack_license, pickup_datetime FROM nyctaxi_sample TABLESAMPLE (70 percent) REPEATABLE (98052))b ON a.medallion=b.medallion AND a.hack_license=b.hack_license AND a.pickup_datetime=b.pickup_datetime WHERE b.medallion is null'
    
    -- Call the stored procedure for scoring and pass the input data
    EXEC [dbo].[RxPredictBatchOutput] @model = 'RxTrainLogit_model', @inquery = @query_string;
    ```
  
預存程序會傳回一系列的值，表示前 10 趟車程的每個預測。 不過前, 趟車程也是單一乘客的車程，而且相對較短的車程距離，驅動程式是不太可能獲得小費。
  

> [!TIP]
> 
> 而不會傳回"yes 提示 」 和 「 無小費 」 的結果，您可能也會傳回預測的機率分數，然後套用 WHERE 子句_分數_資料行的值分類將分數視為 「 可能給小費 」 或 「不可能給小費 」，使用 0.5 或 0.7 等臨界值。 雖然此步驟未包含在預存程序中，但實作起來並不難。

## <a name="single-row-scoring-of-multiple-inputs"></a>為多個輸入的單一資料列評分

有時您想要在多個輸入的值傳遞，並取得這些值為基礎的單一預測。 例如，您可以設定 Excel 工作表、 web 應用程式或 Reporting Services 報表來呼叫預存程序，並提供輸入鍵入或選取的使用者與這些應用程式。

在本節中，您會學習如何建立單一預測使用多個輸入，例如乘客計數、 車程距離等等的預存程序。 預存程序會建立先前儲存的 R 模型為基礎的分數。
  
如果您從外部應用程式呼叫預存程序，請確定資料符合 R 模型的需求。 這可能包括確保輸入資料可轉型或轉換成 R 資料類型，或是驗證資料類型和資料長度。 

1. 建立預存程序**RxPredictSingleRow**。
  
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
  
    開啟新**查詢** 視窗中，並呼叫預存程序，為每個參數提供值。 參數代表模型所使用的特徵資料行，而且不需要。

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

    或者，您也可以使用支援此較簡短形式[預存程序的參數](https://docs.microsoft.com/sql/relational-databases/stored-procedures/specify-parameters):
  
    ```sql
    EXEC [dbo].[RxPredictSingleRow] 'RxTrainLogit_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

3. 結果會指出，獲得小費的機率是低 （零） 在這些前 10 趟車程，因為所有透過相對較短的距離是單一乘客的車程。

## <a name="conclusions"></a>結論

這總結教學課程。 既然您已經學會如何將 R 程式碼內嵌在預存程序，您可以擴充這些作法來建立您自己的模型。 與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的整合可讓您更輕鬆地部署 R 模型進行預測，並納入模型重新定型作為企業資料工作流程的一部分。

## <a name="previous-lesson"></a>上一課

[第 3 課：訓練及儲存使用 T-SQL 的 R 模型](sqldev-train-and-save-a-model-using-t-sql.md)
