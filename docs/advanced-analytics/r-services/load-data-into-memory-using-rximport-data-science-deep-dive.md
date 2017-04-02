---
title: "使用 rxImport 將資料載入記憶體 (資料科學深入探討) | Microsoft Docs"
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
ms.assetid: 47a42e9a-05a0-4a50-871d-de73253cf070
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 rxImport 將資料載入記憶體 (資料科學深入探討)
您可以使用 *rxImport* 函數，將資料來源中的資料移至 R 工作階段記憶體中的資料框架，或移至磁碟上的 XDF 檔案。 如果您未指定檔案作為目的地，系統會將資料放入記憶體作為資料框架。  
  
在此步驟中，您將了解如何從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取得資料，然後使用 *rxImport* 函數將感興趣的資料放入本機檔案。 這樣一來，您就可以在本機計算內容中重複分析資料，而不必重新查詢資料庫。  
  
## 將資料子集從 SQL Server 擷取到本機記憶體  
您已決定只要更詳細地查看高風險的人員。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的來源資料表很大，因此您只會取得高風險客戶的相關資訊，並將該資訊載入本機工作站記憶體內的資料框架。  
  
1.  將計算內容重設為您的本機工作站。  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  建立新 SQL Server 資料來源物件，並在 *sqlQuery* 參數中提供有效的 SQL 陳述式。 這個範例會取得具有最高風險分數的觀察值子集。 這樣一來，只有您真正需要的資料才會放在本機記憶體中。  
  
    ```R    
    sqlServerProbDS <- RxSqlServerData(       
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",  
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)   
    ```  
  
3.  您使用函數 *rxImport* 來實際將資料載入至本機 R 工作階段中的資料框架。  
  
    ```R  
    highRisk <- rxImport(sqlServerProbDS)   
    ```  
     如果作業成功，您應該會看到狀態訊息︰Rows Read: 35, Total Rows Processed: 35, Total Chunk Time: 0.036 seconds 
   
4.  既然您在記憶體內的資料框架中已有高風險的觀察值，您可以使用各種 R 函數來操作資料框架。 例如，您可以依其客戶的風險分數來排序客戶，並列印具有最高風險的客戶。  
  
    ```R  
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]   
    row.names(orderedHighRisk) <- NULL    
    head(orderedHighRisk)  
  
    ```  
  
 **結果**  
  
 *ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*  
*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*  
*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*  
*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*  
*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*  
*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*  
*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*  
  
## 進一步了解 rxImport  
您不僅可以使用 *rxImport* 來移動資料，也在讀取過程中轉換資料。 例如，您可以指定固定寬度資料行的字元數、提供變數的描述、設定因素層級資料行，甚至建立要在匯入後使用的新層級。  
  
*rxImport* 函數會在匯入程序中將變數名稱指派給資料行，但您可以使用 *colInfo* 參數表示新的變數，或者可以使用 *colClasses* 參數變更資料類型。  
  
藉由在 *transforms* 參數中指定其他運算，您可以對所讀取的每個資料區塊執行基本處理。  
  
## 下一個步驟  
[使用 rxDataStep 建立新的 SQL Server 資料表 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/create-new-sql-server-table-using-rxdatastep-data-science-deep-dive.md)  
  
## 上一個步驟  
[第 3 課：使用 R 轉換資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## 另請參閱  
[SQL Server R Services 教學課程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)  
  
  
  
