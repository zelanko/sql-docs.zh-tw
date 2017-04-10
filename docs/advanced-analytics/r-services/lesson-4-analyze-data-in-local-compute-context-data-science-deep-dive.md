---
title: "第 4 課︰分析本機計算內容中的資料 (資料科學深入探討) | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 第 4 課︰分析本機計算內容中的資料 (資料科學深入探討)
一般而言，雖然使用伺服器內容執行複雜 R 程式碼會較為快速，但是有時從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 取得資料並在私人工作站上進行分析會更為方便。  
  
在本節中，您將了解如何切換回本機計算內容，並在內容之間移動資料，以最佳化效能。  
  
## 建立本機摘要  
  
1.  變更計算內容，以在本機執行所有工作。  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
2.  從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 擷取資料時，增加針對每次讀取所擷取的資料列數目，通常就可以取得更佳效能。  若要這樣做，請在資料來源上增加 *rowsPerRead* 參數的值。  
  
    ```R  
    sqlServerDS1 <- RxSqlServerData(  
       connectionString = sqlConnString,        
       table = sqlFraudTable,   
       colInfo = ccColInfo,   
       rowsPerRead = 10000)  
    ```  
  
    之前，*rowsPerRead* 的值已設為 5000。  
  
3.  現在，請對新的資料來源呼叫 *rxSummary*。  
  
    ```R  
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)    
    ```  
  
    實際的結果應該與您在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦的內容中執行 *rxSummary* 時相同。  不過，作業可能會更快或更慢。 大部分取決於資料庫連線，因為正在將資料傳輸至本機電腦進行分析。  
  

## 下一個步驟  
[在 SQL Server 與 XDF 檔案之間移動資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
## 上一個步驟  
[使用 rxDataStep 執行區塊處理分析 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
  
  
