---
title: 執行區塊處理分析使用 RevoScaleR rxDataStep-SQL Server Machine Learning
description: 教學課程逐步解說如何將 SQL Server 上使用 R 語言的分散式分析的資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ccc64c98f0519b33b6ba9da180c01e4478492f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962200"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>執行區塊處理分析使用 rxDataStep （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課，您可以使用**rxDataStep**函式的區塊，以處理資料，而不需要整個資料集是載入至記憶體，並一次處理像傳統 r 一樣**RxDataStep**函式讀取區塊中的資料會套用至每個資料區塊的 R 函數，並再將每個區塊的摘要結果儲存至通用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料來源。 當已經讀取所有資料時，結果會結合。

> [!TIP]
> 這一課，您必須計算列聯表利用**資料表**函式此範例適用於僅限教學用途。 
> 
> 如果您需要在真實世界的資料集製成表格，我們建議您使用**內**或**rxCube**中的函式**RevoScaleR**，其中最適合用於這種作業。

## <a name="partition-data-by-values"></a>依值分割資料

1. 建立自訂的 R 函式呼叫 R**表格**函式上的資料，每個區塊，並命名新的函式**ProcessChunk**。
  
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
    rxSetComputeContext(sqlCompute)
    ```
  
3. 定義 SQL Server 資料來源來保存正在處理的資料。 一開始先指派 SQL 查詢給變數。 然後，使用該變數中的*sqlQuery*引數的新的 SQL Server 資料來源。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. （選擇性） 您可以執行**rxGetVarInfo**上此資料來源。 到目前為止，它包含單一資料行：*Var 1:DayOfWeek，Type： 因數，沒有可用的因素層級*
     
5. 將此因素變數套用至來源資料之前，請建立個別的資料表來保存中繼結果。 同樣地，您只使用**RxSqlServerData**函式定義的資料，確定刪除相同名稱的任何現有的資料表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  呼叫自訂函數**ProcessChunk**來轉換資料，它是讀取，使用它作為*transformFunc*引數**rxDataStep**函式。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要檢視的中繼結果**ProcessChunk**，將指派的結果**rxImport**給變數，然後輸出至主控台的結果。
  
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

10. 若要移除中繼結果資料表，請呼叫**rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)