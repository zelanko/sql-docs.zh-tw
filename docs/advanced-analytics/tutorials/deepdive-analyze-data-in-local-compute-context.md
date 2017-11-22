---
title: "在本機計算內容中分析資料 |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 514cc855af010347006054ad30fc5e5c36b16322
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/09/2017
---
# <a name="analyze-data-in-local-compute-context-data-science-deep-dive"></a>分析本機計算內容 （資料科學深入探討） 中的資料

雖然它可能有助於更快速地執行複雜的 R 程式碼會使用伺服器的內容，有時候是只更方便地取得您的資料超出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]及分析您私人的工作站上。

在本節中，您將了解如何切換回本機計算內容，並在內容之間移動資料，以最佳化效能。

## <a name="create-a-local-summary"></a>建立本機摘要

1. 變更計算內容，以在本機執行所有工作。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]擷取資料時，增加針對每次讀取所擷取的資料列數目，通常就可以取得更佳效能。  若要這樣做，請在資料來源上增加 *rowsPerRead* 參數的值。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```
  
    之前， *rowsPerRead* 的值已設為 5000。
  
3. 現在，請對新的資料來源呼叫 **rxSummary** 。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    實際的結果應該是相同的內容中執行 rxSummary 時[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦。  不過，作業可能會更快或更慢。 大部分取決於資料庫連線，因為正在將資料傳輸至本機電腦進行分析。


## <a name="next--step"></a>下一個步驟

[SQL Server 和 XDF 檔案之間移動資料](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>上一個步驟

[執行區塊使用 rxDataStep 分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)


