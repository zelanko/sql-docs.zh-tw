---
title: 使用 RevoScaleR rxDataStep 執行區塊處理分析
description: 有關如何在 SQL Server 上使用 R 語言來為分散式分析區塊資料的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed22020b162bfac9f35eb8328ea6409903191a4c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714888"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>使用 rxDataStep 執行區塊處理分析 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在這一課, 您會使用**rxDataStep**函數來處理區塊中的資料, 而不需要將整個資料集載入記憶體並一次處理, 如同傳統的 R 一樣。**RxDataStep**函式會讀取區塊中的資料、依序將 R 函數套用至每個資料區塊, 然後將每個區塊的摘要結果儲存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通用資料來源。 當所有資料都已讀取時, 會合並結果。

> [!TIP]
> 在這一課, 您會使用 R 中的**table**函數來計算應變數據表。這個範例僅供教學之用。 
> 
> 如果您需要表格真實世界的資料集, 建議您在**RevoScaleR**中使用**rxCrossTabs**或**rxCube**函式, 這些函式已針對這類作業進行優化。

## <a name="partition-data-by-values"></a>依值分割資料

1. 建立在每個資料區塊上呼叫 R**資料表**函數的自訂 r 函數, 並將新的函式命名為**ProcessChunk**。
  
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
  
3. 定義 SQL Server 的資料來源, 以保存您要處理的資料。 一開始先指派 SQL 查詢給變數。 然後, 在新 SQL Server 資料來源的*sqlQuery*引數中使用該變數。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. (選擇性) 您可以在此資料來源上執行**rxGetVarInfo** 。 此時, 它包含單一資料行:*Var 1:DayOfWeek, 類型: 因素, 沒有可用的因素層級*
     
5. 將此因素變數套用至來源資料之前，請建立個別的資料表來保存中繼結果。 同樣地, 您只需要使用**RxSqlServerData**函式定義資料, 請務必刪除任何同名的現有資料表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  呼叫自訂函數**ProcessChunk** , 以在讀取資料時加以轉換, 方法是使用它作為**RxDataStep**函數的*transformFunc*引數。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要查看**ProcessChunk**的中繼結果, 請將**rxImport**的結果指派給變數, 然後將結果輸出至主控台。
  
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

10. 若要移除中繼結果資料表, 請呼叫**rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)