---
title: "第 5 課︰部署和使用模型 (資料科學端對端逐步解說) | Microsoft Docs"
ms.custom: ""
ms.date: "11/22/2016"
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
ms.assetid: f28a7aac-6d08-4781-ad28-b48d18cc16a0
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 17
---
# 第 5 課︰部署和使用模型 (資料科學端對端逐步解說)
在本課程中，您將藉由包裝預存程序的保存模型，在實際執行環境中使用 R 模型。 接著，您即可從 R 或任何支援 [!INCLUDE[tsql](../../includes/tsql-md.md)] 的應用程式設計語言 (如 C#、Java、Python 等) 叫用預存程序，以使用模型進行新的觀察預測。  
  
您可以使用下列兩種不同的方式，來呼叫用於評分的模型︰  
  
-   **批次評分模式** ：可讓您透過 SELECT 查詢建立多個以輸入為基礎的預測。  
  
-   **個別評分模式** ：可讓您將個別案例的一組功能值傳遞給預存程序，以便一次建立一個預測，結果即會傳回單一預測或其他值。  
  
您將學習如何使用個別評分和批次評分方法來建立預測。  
  
## <a name="batch-scoring"></a>批次評分  
為了方便起見，您可以使用您在第 1 課中，一開始執行 PowerShell 指令碼時所建立的預存程序。 這個預存程序會執行下列動作：  
  
-   取一組輸入資料做為 SQL 查詢    
-   呼叫您在上一課中儲存的定型羅吉斯迴歸模型    
-   預測司機可收到小費的機率  
  
### <a name="use-the-stored-procedure-predicttipbatchmode"></a>使用預存程序 PredictTipBatchMode

1. 請先花點時間查看定義預存程序 *PredictTipBatchMode* 的指令碼 。 它說明如何使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]來運作模型的數個層面。  
  
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

    + 請注意，SELECT 陳述式會呼叫預存的模型。 您可以使用 **varbinary(max)**類型的資料行，在 SQL 資料表中儲存任何定型模型。 這段程式碼會從資料表擷取模型 (儲存在 SQL 變數 _@lmodel2_ 中)，並將其當做 *mod* 參數傳遞給系統預存程序 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
    + 用於評分的輸入資料會以字串形式傳遞給預存程序。  
  
        若要定義這個特定模型的輸入資料，請建立查詢使其傳回有效的資料。 從資料庫擷取資料時，會將其儲存在名為 *InputDataSet*的資料框架中。 此資料框架中的所有資料列皆會用於批次評分。
        + *InputDataSet* 是針對 [sp_execute_external_script &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 程序的輸入資料預設名稱；您可以視需要定義其他的變數名稱。
        + 預存程序會從 **RevoScaleR** 程式庫呼叫 *rxPredict* 函數來產生分數。
    + 預存程序傳回的 *Score*值，即為司機獲得小費的預測機率。  
  
2.  (選擇性) 您可以輕鬆地套用某種篩選條件，將傳回的值分類成「有小費」或「沒小費」群組。  例如，機率小於 0.5 表示不太可能有小費。  
  
3.  在批次模式中呼叫預存程序：  
  
    ```R  
    input = "N' 
      SELECT TOP 10 
          a.passenger_count AS passenger_count,   
          a.trip_time_in_secs AS trip_time_in_secs,  
          a.trip_distance AS trip_distance,  
          a.dropoff_datetime AS dropoff_datetime,    
          dbo.fnCalculateDistance(
            pickup_latitude, 
            pickup_longitude, 
            dropoff_latitude,
            dropoff_longitude) AS direct_distance   
      FROM  
      
      (SELECT medallion, hack_license, pickup_datetime,   
      passenger_count,trip_time_in_secs,trip_distance,    
      dropoff_datetime, pickup_latitude, pickup_longitude,   
      dropoff_latitude, dropoff_longitude from nyctaxi_sample)a  
      
      LEFT OUTER JOIN  
 
      ( SELECT medallion, hack_license, pickup_datetime 
        FROM nyctaxi_sample  tablesample (1 percent) repeatable (98052)  )b  

      ON a.medallion=b.medallion 
        AND a.hack_license=b.hack_license 
        AND a.pickup_datetime=b.pickup_datetime  

      WHERE b.medallion is null  
    '"  
    q<-paste("EXEC PredictTipBatchMode @inquery = ", input, sep="")  
    sqlQuery (conn, q)  
  
    ```  
  
## <a name="single-row-scoring"></a>單一資料列評分  

您可能想要將功能提供為預存程序的引數，而不是使用查詢，將輸入的值傳遞至已儲存的 R 模型。  

### <a name="use-the-stored-procedure-predicttipsinglemode"></a>使用預存程序 PredictTipSingleMode
1.  請花點時間來檢閱下列程式碼適用於預存程序 *PredictTipSingleMode*，您應該已經在資料庫中建立此預存程序。  
  
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
        SELECT * FROM [dbo].[fnEngineerFeatures](@passenger_count, 
            @trip_distance,  
            @trip_time_in_secs,  
            @pickup_latitude,  
            @pickup_longitude,  
            @dropoff_latitude,  
            @dropoff_longitude)  
        '  
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
      @params = N'@model varbinary(max),
                @passenger_count int,
                @trip_distance float,
                @trip_time_in_secs int ,  
                @pickup_latitude float ,
                @pickup_longitude float ,
                @dropoff_latitude float ,
                @dropoff_longitude float',  
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
  
    此預存程序會採用功能值做為輸入 (例如乘客計數和車程距離)，並使用預存的 R 模型來評分，然後輸出分數。  
  
### <a name="call-the-stored-procedure-and-pass-parameters"></a>呼叫預存程序並傳遞參數

1. 在 SQL Server Management Studio 中，您可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] **EXEC** 來呼叫預存程序，並將必要的輸入傳遞給它。 。  
    ```tsql  
    EXEC [dbo].[PredictTipSingleMode] 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303   
    ```  
  
    此處所傳遞的值分別是 _passenger_count_、 _trip_distance_、 _trip_time_in_secs_、 _pickup_latitude_、 _pickup_longitude_、 _dropoff_latitude_和 _dropoff_longitude_變數。  
  
2.  若要從 R 程式碼執行這個相同的呼叫，您只需定義包含整個預存程序呼叫的 R 變數。 
  
    ```R  
    q = "EXEC PredictTipSingleMode 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303 "  
    ```  
  
    此處所傳遞的值分別是 _passenger_count_、 _trip_distance_、 _trip_time_in_secs_、 _pickup_latitude_、 _pickup_longitude_、 _dropoff_latitude_和 _dropoff_longitude_變數。  
  
### <a name="generate-scores"></a>產生分數

1. 呼叫 **RODBC** 封裝的 *sqlQuery* 函數，並傳遞連接字串以及包含預存程序呼叫的字串變數。  
  
    ```R  
    # predict with stored procedure in single mode  
    sqlQuery (conn, q)   
    ```  
  
    如需 **RODBC** 的詳細資訊，請參閱 [http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery](http://www.inside-r.org/packages/cran/RODBC/docs/sqlQuery)。  
  
## <a name="conclusion"></a>結論  
現在，您已學到如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料並將定型的 R 模型保存至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，這麼做應該比依據此資料集而建立一些其他的模型來說相對輕鬆。 比方說，您可能會嘗試建立這類模型︰  
  
-   可預測小費金額的迴歸模型    
-   預測小費金額為高、中、低的多元分類模型。  

我們也建議您查看一些其他範例和資源： 
+ [資料科學案例和解決方案範本](../../advanced-analytics/r-services/data-science-scenarios-and-solution-templates.md)
+ [資料庫內的進階分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)
+ [Microsoft R - 深入探討資料分析](https://msdn.microsoft.com/microsoft-r/data-analysis-in-microsoft-r)
+ [其他資源](https://msdn.microsoft.com/microsoft-r/microsoft-r-more-resources)
## <a name="previous-lesson"></a>上一課  
[第 4 課︰建立和儲存模型 &#40;資料科學端對端逐步解說&#41;](../../advanced-analytics/r-services/lesson-4-build-and-save-the-model-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>另請參閱  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
