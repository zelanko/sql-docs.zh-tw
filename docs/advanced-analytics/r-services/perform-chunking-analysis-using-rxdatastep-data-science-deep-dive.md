---
title: "使用 rxDataStep 執行區塊處理分析 (資料科學深入探討) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 rxDataStep 執行區塊處理分析 (資料科學深入探討)
*RxDataStep* 函數可用來處理資料區塊，而不需要像傳統 R 一樣將整個資料集載入至記憶體，並一次處理。它的運作方式，是您以區塊讀取資料，並使用 R 函數依次處理每個區塊的資料，然後將每個區塊的摘要結果寫入共同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源。  
  
在這一課，您將練習這項技術，使用 R 中的 *table* 函數來計算列聯表。  
  
> [!TIP]  
> 此範例僅供說明之用。 如果您需要將真實世界的資料集製成表格，我們建議您使用內建在 **RevoScaleR** 的 *rxCrossTabs* 或 *rxCube* 內建函數，它們已針對這類的作業進行最佳化。  
  
## 依值分割資料  
  
1.  首先，建立自訂的 R 函數，名為 *ProcessChunk*，它對每個資料區塊呼叫 *table* 函數。  
  
    ```R  
    ProcessChunk <- function( dataList) {      
    # Convert the input list to a data frame and compute contingency table      
    chunkTable <- table(as.data.frame(dataList))   
  
    # Convert table output to a data frame with a single row      
    varNames <- names(chunkTable)     
    varValues <- as.vector(chunkTable)        
    dim(varValues) <- c(1, length(varNames))      
    chunkDF <- as.data.frame(varValues)       
    names(chunkDF) <- varNames   
  
    # Return the data frame, which has a single row   
    return( chunkDF )   
    }    
    ```  
 
  
2.  將計算內容設定為伺服器。  
  
    ```R  
    rxSetComputeContext( sqlCompute )   
    ```  
  
3.  您將定義 SQL Server 資料來源來保存正在處理的資料。 一開始先指派 SQL 查詢給變數。   
  
    ```R  
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"   
    ```  

4.  將該變數插入到新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源的 *sqlQuery* 引數。  
  
    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,  
        connectionString = sqlConnString,    
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",   
            levels = as.character(1:7))))    
    ```  
     如果您對此資料來源執行 *rxGetVarInfo*，您會看到它只包含單一資料行：*Var 1: DayOfWeek, Type: factor, no factor levels available*
     
5.  將此因素變數套用至來源資料之前，請建立個別的資料表來保存中繼結果。 同樣地，您只要使用 *RxSqlServerData* 函數定義資料，並刪除相同名稱的任何現有的資料表。   
  
    ```R  
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)   
    # Check whether the table already exists.  
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }   
    ```  
  
7.  現在您將呼叫自訂函數 *ProcessChunk* 函數在讀取資料時進行轉換資料，方法是使用它作為 *rxDataStep* 函數的 *transformFunc* 引數。  
  
    ```R  
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)   
    ```  
  
8.  若要檢視 *ProcessChunk* 的中繼結果，請將 *rxImport* 的結果指派給變數，然後再將結果輸出至主控台。  
  
    ```R  
    iroResults <- rxImport(iroDataSource)   
  
    iroResults   
    ```  

**部分結果**

|      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |
  
9. 若要計算所有區塊的最終結果，請加總資料行，然後在主控台中顯示結果。  
  
    ```R  
    finalResults <- colSums(iroResults)   
  
    finalResults   
    ```  
 **結果**
  1  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 
  
10. 若要移除中繼結果資料表，請再呼叫一次 *rxSqlServerDropTable*。  
  
    ```R  
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)    
    ```  
  
## 下一個步驟  
[第 4 課︰分析本機計算內容中的資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## 上一個步驟  
[使用 rxDataStep 建立新的 SQL Server 資料表 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## 另請參閱  
[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
