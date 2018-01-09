---
title: "分析資料，在本機計算內容 （SQL 與 R 深入探討） |Microsoft 文件"
ms.date: 12/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0705d7253979dd5b688a0ca5f78720304a368e3d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="analyze-data-in-local-compute-context-sql-and-r-deep-dive"></a>分析本機計算內容 （SQL 與 R 深入探討） 中的資料

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在本節中，您可以了解如何切換回本機計算內容中，並以最佳化效能的內容之間移動資料。

雖然 i 可能有助於更快速地執行複雜的 R 程式碼會使用伺服器的內容，有時候是更方便地取得您的資料超出[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和分析在本機工作站。

## <a name="create-a-local-summary"></a>建立本機摘要

1. 變更計算內容，以在本機執行所有工作。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. 從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]擷取資料時，增加針對每次讀取所擷取的資料列數目，通常就可以取得更佳效能。  若要這樣做，請在資料來源上增加 *rowsPerRead* 參數的值。 之前， *rowsPerRead* 的值已設為 5000。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 呼叫**rxSummary**上新的資料來源。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    實際的結果應該與您在 **電腦的內容中執行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時相同。  不過，作業可能會更快或更慢。 大部分取決於資料庫連線，因為正在將資料傳輸至本機電腦進行分析。

## <a name="next-step"></a>下一步

[SQL Server 和 XDF 檔案之間移動資料](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>上一個步驟

[使用 rxDataStep 執行區塊處理分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)
