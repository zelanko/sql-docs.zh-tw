---
title: "執行區塊處理的分析，使用 rxDataStep |Microsoft 文件"
ms.custom: 
ms.date: 05/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: af375ddf99794b748699355203becd137227fbcd
ms.contentlocale: zh-tw
ms.lasthandoff: 09/01/2017

---
# <a name="perform-chunking-analysis-using-rxdatastep"></a>使用 rxDataStep 執行區塊處理分析

**RxDataStep** 函數可用來處理資料區塊，而不需要像傳統 R 一樣將整個資料集載入至記憶體，並一次處理。它的運作方式，是您以區塊讀取資料，並使用 R 函數依次處理每個區塊的資料，然後將每個區塊的摘要結果寫入共同的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源。

在這一課，您會使用練習這項技術`table`R，計算應變資料表中的函式。

> [!TIP]
> 此範例僅供說明之用。 如果您需要製成表格真實世界的資料集，我們建議您使用**rxCrossTabs**或**rxCube**函式的**RevoScaleR**，這種最佳化這個作業。

## <a name="partition-data-by-values"></a>依值分割資料

1. 首先，建立自訂的 R 函式呼叫*資料表*函式的資料，每個區塊，並命名為`ProcessChunk`。
  
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

2. 將計算內容設定為伺服器。
  
    ```R
    rxSetComputeContext( sqlCompute )
    ```
  
3. 您將定義 SQL Server 資料來源來保存正在處理的資料。 一開始先指派 SQL 查詢給變數。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    ```

4. 將該變數插入到新 *資料來源的* sqlQuery [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引數。
  
    ```R
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
     如果您對此資料來源執行 *rxGetVarInfo* ，您會看到它只包含單一資料行： *Var 1: DayOfWeek, Type: factor, no factor levels available*
     
5. 將此因素變數套用至來源資料之前，請建立個別的資料表來保存中繼結果。 同樣地，只需要使用 RxSqlServerData 函式定義的資料，並刪除相同名稱的任何現有的資料表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  現在您會呼叫自訂函式`ProcessChunk`讀取時，使用它做為轉換資料*transformFunc* rxDataStep 函式引數。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要檢視的中繼結果`ProcessChunk`rxImport 的結果指派給變數，，然後將結果輸出至主控台。
  
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

10. 若要移除的中繼結果資料表，請 rxSqlServerDropTable 另一個呼叫。
  
    ```R
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)
    ```

## <a name="next-step"></a>下一個步驟

[分析本機計算內容; 中的資料](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>上一個步驟

[建立新的 SQL Server 資料表，使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)



