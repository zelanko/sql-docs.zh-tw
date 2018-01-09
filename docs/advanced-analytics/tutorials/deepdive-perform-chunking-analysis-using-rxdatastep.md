---
title: "執行區塊處理的分析使用 rxDataStep （SQL 與 R 深入探討） |Microsoft 文件"
ms.custom: 
ms.date: 12/14/2017
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
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d80562b286c5e1051892a1b5d222e47483822e57
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-and-r-deep-dive"></a>執行區塊使用 rxDataStep （SQL 與 R 深入探討） 的分析

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課，您可以使用**rxDataStep**函式來處理的資料區塊 （chunk），而不是需要整個資料集是載入到記憶體，而且一次處理，如同傳統的。**RxDataStep**函式會讀取區塊中的資料，適用於資料的每個區塊的 R 函數，然後將每個區塊的摘要結果儲存至共同[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源。 當已經讀取所有資料時，結果會結合。

> [!TIP]
> 這一課，您必須計算應變資料表使用`table`函式此範例僅供說明之用。 
> 
> 如果您需要製成表格真實世界的資料集，我們建議您使用**rxCrossTabs**或**rxCube**函式的**RevoScaleR**，這種最佳化這個作業。

## <a name="partition-data-by-values"></a>值的資料分割資料

1. 建立自訂的 R 函式呼叫 R`table`函式的資料，每個區塊，並命名為新的函式`ProcessChunk`。
  
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
  
3. 定義 SQL Server 資料來源包含要處理的資料。 一開始先指派 SQL 查詢給變數。 然後，使用該變數在*sqlQuery*引數的新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源。
  
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
4. （選擇性） 您可以執行**rxGetVarInfo**此資料來源。 此時，它包含單一資料行： *Var 1: DayOfWeek、 型別： 因素，沒有可用的因素層級*
     
5. 將此因素變數套用至來源資料之前，請建立個別的資料表來保存中繼結果。 同樣地，您只使用 RxSqlServerData 函式定義的資料，makign 確定要刪除相同名稱的任何現有的資料表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  呼叫自訂函式`ProcessChunk`讀取時，使用它做為轉換資料*transformFunc*引數**rxDataStep**函式。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要檢視的中繼結果`ProcessChunk`，指派的結果**rxImport**變數，然後將結果輸出至主控台。
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

**部分結果**

|      |    @shouldalert  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| @shouldalert | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. 若要計算所有區塊的最終結果，請加總資料行，然後在主控台中顯示結果。

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

 **結果**
  @shouldalert  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 若要移除的中繼結果資料表，請呼叫**rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-step"></a>下一步

[分析本機計算內容中的資料](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>上一個步驟

[使用 rxDataStep 建立新的 SQL Server 資料表](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
