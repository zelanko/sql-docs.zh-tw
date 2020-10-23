---
title: RevoScaleR 中的摘要統計資料
description: RevoScaleR 教學課程 5：如何在 SQL Server 上使用 R 語言計算統計摘要統計資料。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3d8b04d384d7ee5f846197ff3465b9c0914ca94c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196312"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>使用 R 計算摘要統計資料 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

這是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的教學課程 5；此教學課程系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

此教學課程會使用在先前教學課程中建立的資料來源和計算內容，來執行高效能的 R 指令碼。 在此教學課程中，您將會使用本機和遠端伺服器計算內容來執行下列工作：

> [!div class="checklist"]
> * 將計算內容切換為 SQL Server
> * 取得遠端資料物件的摘要統計資料
> * 計算本機摘要

如果您已完成先前的教學課程，應該會有這些遠端計算內容：sqlCompute 和 sqlComputeTrace。 之後，您將會使用 sqlCompute 和本機計算內容來繼續進行未來的教學課程。

使用 R IDE 或 **Rgui** 來執行此教學課程中的 R 指令碼。

## <a name="compute-summary-statistics-on-remote-data"></a>計算遠端資料的摘要統計資料

執行任何遠端的 R 程式碼之前，您必須指定遠端計算內容。 所有後續計算工作都會在 sqlCompute  參數中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦上進行。

計算內容會保持在作用中的狀態，直到您進行變更為止。 不過，任何「無法」  在遠端伺服器內容中執行的 R 指令碼都將在本機上自動執行。

若要查看計算內容的運作方式，請在遠端 SQL Server 上產生 sqlFraudDS 資料來源的摘要統計資料。 此資料來源物件是在[教學課程二](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)中建立，並代表 RevoDeepDive 資料庫中的 ccFraudSmall 資料表。 

1. 將計算內容切換為在上一個教學課程中建立的 sqlCompute：
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. 呼叫 [rxSummary](/machine-learning-server/r-reference/revoscaler/rxsummary) 函式並傳遞必要引數，例如公式及資料來源，以及將結果指派給變數 `sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 語言提供許多彙總函式，但 **RevoScaleR** 中的 **rxSummary** 支援在各種遠端計算內容上執行，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需類似函式的詳細資訊，請參閱[使用 RevoScaleR 建立資料摘要](/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
3. 將 sumOut 的內容列印到主控台。
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 如果您收到錯誤，請等候幾分鐘讓執行完成，然後再重試命令。

**結果**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>建立本機摘要

1. 變更計算內容，以在本機執行所有工作。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. 從 SQL Server 解壓縮資料時，您通常可以藉由增加每次讀取時解壓縮的資料列數來取得較佳效能 (假設記憶體可容納增加的區塊大小)。 執行下列命令，即可在資料來源上增加 rowsPerRead  參數的值。 之前， *rowsPerRead* 的值已設為 5000。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 請針對新的資料來源呼叫 **rxSummary**。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   實際的結果應該與您在 **電腦的內容中執行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時相同。 不過，作業可能會更快或更慢。 大部分取決於資料庫連線，因為正在將資料傳輸至本機電腦進行分析。

4. 在接下來的幾個教學課程中，我們將切換回遠端計算內容。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 製作 SQL Server 資料的圖表](../../machine-learning/tutorials/deepdive-visualize-sql-server-data-using-r.md)