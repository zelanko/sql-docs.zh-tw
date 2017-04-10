---
title: "步驟 5︰使用 T-SQL 定型及儲存模型 (資料庫內進階分析教學課程) | Microsoft Docs"
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
ms.assetid: 3282e8ed-b515-4ed5-8543-fcef68629a92
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 步驟 5︰使用 T-SQL 定型及儲存模型 (資料庫內進階分析教學課程)
在此步驟中，您將學習如何使用 R 來定型機器學習模型。R 套件已隨附於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝，因此您可以透過預存程序來呼叫演算法。 您將使用剛才建立的資料功能來定型模型，然後將定型的模型儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表中。  
  
## 使用預存程序建立 R 模型  
只要使用系統預存程序 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)，即可進行所有 R 執行階段 (隨附於 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 安裝) 的呼叫。 不過，如果需要重新定型模型，更輕鬆的方式可能是封裝另一個預存程序 sp_execute_exernal_script 的呼叫。  
  
在本節中，您將使用剛才準備好的資料來建立用於建置模型的預存程序。 這個預存程序會定義輸入資料，並使用 R 套件來建立羅吉斯迴歸模型。  
  
#### 若要建立預存程序  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，開啟新的查詢視窗，然後執行下列陳述式來建立預存程序 _TrainTipPredictionModel_。  
  
    請注意，因為預存程序已經包含輸入資料的定義，因此您不需要提供輸入查詢。  
  
    ```  
    CREATE PROCEDURE [dbo].[TrainTipPredictionModel]  
  
    AS  
    BEGIN  
      DECLARE @inquery nvarchar(max) = N'  
        select tipped, fare_amount, passenger_count,trip_time_in_secs,trip_distance,   
        pickup_datetime, dropoff_datetime,   
        dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance  
        from nyctaxi_sample  
        tablesample (70 percent) repeatable (98052)  
    '  
      -- Insert the trained model into a database table  
      INSERT INTO nyc_taxi_models  
      EXEC sp_execute_external_script @language = N'R',  
                                      @script = N'  
  
    ## Create model  
    logitObj <- rxLogit(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = InputDataSet)  
    summary(logitObj)  
  
    ## Serialize model and put it in data frame  
    trained_model <- data.frame(model=as.raw(serialize(logitObj, NULL)));  
    ',  
                                      @input_data_1 = @inquery,  
                                      @output_data_1_name = N'trained_model'  
      ;  
  
    END  
    GO  
  
    ```  
  
    這個預存程序會在模型定型同時執行下列活動︰  
  
    -   為了確保會剩下一些資料來測試模型，系統會從計程車資料表隨機選取 70% 的資料。  
  
    -   SELECT 查詢會使用自訂的純量函數 _fnCalculateDistance_ 計算上車和下車位置之間的直線距離。  查詢的結果會儲存在預設的 R 輸入變數 `InputDataset` 中。  
  
    -   R 指令碼會呼叫 `rxLogit` 函數 (其為 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 隨附的其中一個增強 R 函數)，以建立羅吉斯迴歸模型。  
  
        二進位變數 _tipped_ 可做為「標籤」或結果資料行，而模型則是使用下列功能資料行進行調整︰_passenger_count_、_trip_distance_、_trip_time_in_secs_和 _direct_distance_。  
  
    -   系統會序列化儲存在 R 變數 `logitObj` 中的定型模型，並將其放入資料框架以輸出至 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 系統會將該輸出插入至資料庫資料表 _nyc_taxi_models_，以供您用於未來的預測。  
  
2.  請執行陳述式以建立預存程序。  
  
#### 若要使用預存程序建立 R 模型  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 中，執行以下陳述式：  
  
    ```  
    EXEC TrainTipPredictionModel  
    ```  
  
    資料處理和模型調整可能需要一些時間。 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 的 [訊息] 視窗會顯示經由管道輸出至 R 的 **stdout** 資料流的訊息。 例如：  
  
  
*來自外部指令碼的 STDOUT 訊息︰Rows Read: 1193025, Total Rows Processed: 1193025, Total Chunk Time: 0.093 seconds*       
  
系統可以讀取和處理連續資料區塊。 您也可能會看到個別 `rxLogit` 函數的特定訊息，其指出變數與測試度量。  
  
2.  開啟 *nyc_taxi_models* 資料表。 您可以看到當中已新增一個新的資料列，其 _model_ 資料行中包含序列化的模型。  
  
  
  
*model*  
*0x580A00000002000302020....*  
  
在下一個步驟中，您將使用定型的模型來建立預測。  
  
## 下一個步驟  
[步驟 6︰操作模型](../../advanced-analytics/r-services/step-6-operationalize-the-model-in-database-advanced-analytics-tutorial.md)  
  
## 上一個步驟  
[步驟 4︰使用 T-SQL 建立資料功能](../../advanced-analytics/r-services/step-4-create-data-features-using-t-sql-in-database-advanced-analytics-tutorial.md)  
  
## 另請參閱  
[適用於 SQL 開發人員的資料庫內進階分析 &#40;教學課程&#41;](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
