---
title: RevoScaleR 中的區塊化分析
description: RevoScaleR 教學課程 12：如何在 SQL Server 上使用 R 語言將資料區塊化以進行分散式分析。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0ad082c3a21292b782d5888b48b698c986c0b5b2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947205"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>使用 rxDataStep 執行區塊化分析 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 12 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將會使用 **rxDataStep** 函式以區塊形式處理資料，而不需要將整個資料集載入記憶體並且一次處理，就像傳統的 R 一樣。**rxDataStep** 函式會以區塊形式讀取資料、依序將 R 函式套用至每個資料區塊，然後將每個區塊的摘要結果儲存到通用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料來源。 當所有資料都已讀取時，會合併結果。

> [!TIP]
> 在此教學課程中，您會使用 R 中的 **table** 函式來計算應變資料表。這個範例僅供教學之用。 
> 
> 如果您需要將實際的資料集製成表格，建議您使用 **RevoScaleR** 中的 **rxCrossTabs** 或 **rxCube** 函式，它們已針對這類的作業進行最佳化。

## <a name="partition-data-by-values"></a>依值分割資料

1. 建立一個自訂 R 函式，在每個資料區塊上呼叫 R **table** 函式，並將新的函式命名為 **ProcessChunk**。
  
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
  
3. 定義 SQL Server 資料來源來保存正在處理的資料。 一開始先指派 SQL 查詢給變數。 然後，在新 SQL Server 資料來源的 sqlQuery  引數中使用該變數。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. 您可以選擇性地在此資料來源上執行 **rxGetVarInfo**。 此時，它包含單一資料行：*Var 1：DayOfWeek, Type: factor, no factor levels available*
     
5. 將此因素變數套用至來源資料之前，請建立個別的資料表來保存中繼結果。 同樣地，您只要使用 **RxSqlServerData** 函式定義資料，確定刪除相同名稱的任何現有資料表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  藉由使用自訂函式 **ProcessChunk** 作為 **rxDataStep** 函式的 transformFunc  引數，呼叫該自訂函式以在讀取資料時轉換資料。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要檢視 **ProcessChunk** 的中繼結果，請將 **rxImport** 的結果指派給變數，然後再將結果輸出至主控台。
  
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

10. 若要移除中繼結果資料表，請呼叫 **rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)