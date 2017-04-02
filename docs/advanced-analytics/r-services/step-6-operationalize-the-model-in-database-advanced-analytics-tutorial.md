---
title: "步驟 6︰操作模型 (資料庫內進階分析教學課程) | Microsoft Docs"
ms.custom: ""
ms.date: "04/19/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
  - "TSQL"
ms.assetid: 52b05828-11f5-4ce3-9010-59c213a674d1
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 步驟 6︰操作模型 (資料庫內進階分析教學課程)
在此步驟中，您將了解如何使用預存程序來「操作」模型。 您可以透過其他應用程式直接呼叫此預存程序，對新的觀察值進行預測。  
  
在此步驟中，您將了解可從預存程序呼叫 R 模型的兩個方法：  
  
-   **批次計分模式**︰使用 SELECT 查詢來提供多個資料列。 此預存程序會傳回對應至輸入案例的觀察值資料表。  
  
-   **個別計分模式**︰傳遞一組個別參數值作為輸入。  此預存程序會傳回單一資料列或值。  
  
首先，讓我們來看看計分的一般運作方式。  
  
## 基本計分  
預存程序 _PredictTip_ 說明將預測呼叫包裝在預存程序中的基本語法。  
  
```  
CREATE PROCEDURE [dbo].[PredictTip] @inquery nvarchar(max)  
AS  
BEGIN  
  
  DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
  FROM nyc_taxi_models);  
  EXEC sp_execute_external_script @language = N'R',  
                                  @script = N'  
mod <- unserialize(as.raw(model));  
print(summary(mod))  
OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
          predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
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
  
-   此 SELECT 陳述式可從資料庫取得序列化模型，並將模型儲存在 R 變數 `mod` 中，以使用 R 進一步處理。  
  
-   您可以從預存程序的第一個參數 `@inquery` 中指定的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢，取得要計分的新案例。 讀取查詢資料之後，這些資料列會儲存在預設資料框架 `InputDataSet` 中。 此資料框架會傳遞至 R 中的 `rxPredict` 函數，再由此函數產生分數。  
  
    `OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,            predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);`  
  
    因為 data.frame 可以包含單一資料列，所以您可以使用相同的程式碼進行批次或單一計分。  
  
-   `rxPredict` 函數所傳回的值是**浮點數**，代表給小費 (任何金額) 的機率。  
  
## 使用 SELECT 查詢的批次計分  
現在讓我們來看看批次計分的運作方式。  
  
1.  請先取得要使用的一小組輸入資料。  
  
    ```  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
    (  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null  
    ```  
  
    此查詢會建立「前 10 趟」車程的清單，其中包含乘客計數及進行預測所需的其他特徵。  
  
 **結果**  
  
*passenger_count   trip_time_in_secs    trip_distance  dropoff_datetime   direct_distance*  
*1  283 0.7 2013-03-27 14:54:50.000   0.5427964547*  
*1  289 0.7 2013-02-24 12:55:29.000   0.3797099614*  
*1  214 0.7 2013-06-26 13:28:10.000   0.6970098661*  
*1  276 0.7 2013-06-27 06:53:04.000   0.4478814362*  
*1  282 0.7 2013-02-21 07:59:54.000   0.5340645749*  
*1  260 0.7 2013-03-27 15:40:49.000   0.5513900727*  
*1  230 0.7 2013-02-05 09:47:59.000   0.5161578519*  
*1  250 0.7 2013-05-08 14:35:51.000   0.5626440915*  
*1  280 0.7 2013-05-11 12:22:01.000   0.5598517959*  
*1  308 0.7 2013-04-10 08:06:00.000   0.4478814362*  
  
您將使用此查詢作為下載時所提供之預存程序 _PredictTipBatchMode_ 的輸入。  
  
2.  首先，請花幾分鐘檢閱 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中預存程序 _PredictTipBatchMode_ 的程式碼。  
  
    ```  
    /****** Object:  StoredProcedure [dbo].[PredictTipBatchMode]  ******/  
    SET ANSI_NULLS ON  
    GO  
    SET QUOTED_IDENTIFIER ON  
    GO  
  
    CREATE PROCEDURE [dbo].[PredictTipBatchMode] @inquery nvarchar(max)  
    AS  
    BEGIN  
  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
                                      @input_data_1 = @inquery,  
                                      @params = N'@model varbinary(max)',  
                                      @model = @lmodel2  
      WITH RESULT SETS ((Score float));  
  
    END  
    ```  
  
3.  若要建立預測，您將使用類似如下的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式，在變數中提供查詢文字並當作參數傳遞至預存程序。  
  
    ```  
    -- Specify input query  
  
    DECLARE @query_string nvarchar(max)  
    SET @query_string='  
    select top 10 a.passenger_count as passenger_count,   
        a.trip_time_in_secs as trip_time_in_secs,  
        a.trip_distance as trip_distance,  
        a.dropoff_datetime as dropoff_datetime,    
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude,dropoff_longitude) as direct_distance   
    from  
        select medallion, hack_license, pickup_datetime, passenger_count,trip_time_in_secs,trip_distance,    
            dropoff_datetime, pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude  
        from nyctaxi_sample  
    )a  
    left outer join  
    (  
    select medallion, hack_license, pickup_datetime  
    from nyctaxi_sample  
    tablesample (70 percent) repeatable (98052)  
    )b  
    on a.medallion=b.medallion and a.hack_license=b.hack_license and a.pickup_datetime=b.pickup_datetime  
    where b.medallion is null'  
  
    -- Call stored procedure for scoring  
    EXEC [dbo].[PredictTip] @inquery = @query_string;  
  
    ```  
  
4.  此預存程序會傳回一系列的值，代表「前 10 趟車程」之每趟車程的預測。 回頭看這些輸入值，「前 10 趟車程」全部都是單一乘客的車程，而且車程距離相對較短。 根據此資料，駕駛不太可能從這類車程獲得小費。  
  
    除了只傳回有小費/無小費的結果，您也可以傳回預測的機率分數，然後將 WHERE 子句套用至 [分數] 資料行值，使用 0.5 或 0.7 等臨界值，將分數分類為「可能給小費」或「不可能給小費」。 雖然此步驟未包含在預存程序中，但實作起來並不難。  
  
## 對個別資料列計分  
有時候，您會想要從應用程式傳入個別值，並根據這些值取得單一結果。 例如，您可以設定 Excel 工作表、Web 應用程式或 Reporting Services 報表來呼叫預存程序，並提供使用者鍵入或選取的輸入。  
  
在本節中，您將了解如何使用預存程序來建立單一預測。  
  
1.  請花幾分鐘檢閱下載時已隨附之預存程序 _PredictTipSingleMode_ 的程式碼。  
  
    ```  
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
      SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count,  
    @trip_distance,  
    @trip_time_in_secs,  
    @pickup_latitude,  
    @pickup_longitude,  
    @dropoff_latitude,  
    @dropoff_longitude)  
        '  
      DECLARE @lmodel2 varbinary(max) = (SELECT TOP 1 model  
      FROM nyc_taxi_models);  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
    mod <- unserialize(as.raw(model));  
    print(summary(mod))  
    OutputDataSet<-rxPredict(modelObject = mod, data = InputDataSet, outData = NULL,   
              predVarNames = "Score", type = "response", writeModelVars = FALSE, overwrite = TRUE);  
    str(OutputDataSet)  
    print(OutputDataSet)  
    ',  
    @input_data_1 = @inquery,  
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,@trip_time_in_secs int ,  
    @pickup_latitude float ,@pickup_longitude float ,@dropoff_latitude float ,@dropoff_longitude float',  
    @model = @lmodel2,  
    @passenger_count =@passenger_count ,  
    @trip_distance=@trip_distance,  
    @trip_time_in_secs=@trip_time_in_secs,    
    @pickup_latitude=@pickup_latitude,  
    @pickup_longitude=@pickup_longitude,  
    @dropoff_latitude=@dropoff_latitude,  
    @dropoff_longitude=@dropoff_longitude  
      WITH RESULT SETS ((Score float));  
  
    END  
  
    ```  
  
    -   此預存程序接受多個單一值作為輸入，例如乘客計數、車程距離等等。  
  
        如果您從外部應用程式呼叫預存程序，請確定資料符合 R 模型的需求。 這可能包括確保輸入資料可轉型或轉換成 R 資料類型，或是驗證資料類型和資料長度。 如需詳細資訊，請參閱[使用 R 資料類型](https://msdn.microsoft.com/library/mt590948.aspx)。  
  
    -   此預存程序會根據儲存的 R 模型建立分數。  
  
2.  請以手動方式提供值來試試看。  
  
    開啟新的 [查詢] 視窗，然後呼叫預存程序，並針對每個特徵資料行輸入參數。  
  
    ```  
  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303  
  
    ```  
  
    這些特徵資料行的值依序為：  
  
    -   *trip_time_in_secs*  
    -   *pickup_latitude*  
    -   *pickup_longitude*  
    -   *dropoff_latitude*  
    -   *dropoff_longitude*  
  
3.  結果指出，從這前 10 趟車程獲得小費的機率很低，因為全部都是單一乘客且距離相對較短的車程。  
  
## 結論  
在本教學課程中，您已了解如何使用內嵌在預存程序中的 R 程式碼。 與 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的整合可讓您更輕鬆地部署 R 模型進行預測，並納入模型重新定型作為企業資料工作流程的一部分。  
  
  
## 上一個步驟  
[步驟 4︰使用 T-SQL 建立資料特徵](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## 另請參閱  
[適用於 SQL 開發人員的資料庫內進階分析 &#40;教學課程&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
