---
title: 計算摘要統計資料 RevoScaleR 教學課程
description: 有關如何在 SQL Server 上使用 R 語言計算統計摘要統計資料的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 90a674057845427fe60fd3c62268bf0fb3d18688
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715576"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>R 中的計算摘要統計資料 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

它會使用先前課程中建立的資料來源和計算內容, 在這一課中執行高驅動的 R 腳本。 在這一課, 您將使用本機和遠端伺服器計算內容來執行下列工作:

> [!div class="checklist"]
> * 將計算內容切換至 SQL Server
> * 取得遠端資料物件的摘要統計資料
> * 計算本機摘要

如果您已完成先前的課程, 您應該會有下列遠端計算內容: sqlCompute 和 sqlComputeTrace。 在未來的課程中, 您將使用 sqlCompute 和本機計算內容來繼續進行。

使用 R IDE 或**rgui.exe**來執行本課程中的 r 腳本。

## <a name="compute-summary-statistics-on-remote-data"></a>計算遠端資料的摘要統計資料

您必須先指定遠端計算內容, 才可以從遠端執行任何 R 程式碼。 所有後續計算都是在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *sqlCompute*參數所指定的電腦上進行。

計算內容會維持作用中狀態, 直到您變更它為止。 不過, 任何*無法*在遠端伺服器內容中執行的 R 腳本都將自動在本機執行。

若要查看計算內容的運作方式, 請在遠端 SQL Server 上產生 sqlFraudDS 資料來源的摘要統計資料。 這個資料來源物件是在第[二課](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)建立的, 代表 RevoDeepDive 資料庫中的 ccFraudSmall 資料表。 

1. 將計算內容切換至在上一課中建立的 sqlCompute:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. 呼叫[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)函數並傳遞必要引數, 例如公式和資料來源, 然後將結果指派給變數`sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 語言提供許多摘要功能, 但**RevoScaleR**中的**rxSummary**支援在各種遠端計算內容上執行, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]包括。 如需類似功能的詳細資訊, 請參閱[使用 RevoScaleR 的資料摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
3. 將 sumOut 的內容列印到主控台。
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 如果您收到錯誤, 請等候幾分鐘讓執行完成, 然後再重試命令。

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
  
2. 從 SQL Server 解壓縮資料時, 您通常可以藉由增加針對每個讀取所解壓縮的資料列數目來取得較佳的效能, 假設增加的區塊大小可在記憶體中容納。 執行下列命令, 以增加資料來源上*rowsPerRead*參數的值。 之前， *rowsPerRead* 的值已設為 5000。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 在新的資料來源上呼叫**rxSummary** 。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   實際的結果應該與您在 **電腦的內容中執行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時相同。 不過，作業可能會更快或更慢。 大部分取決於資料庫連線，因為正在將資料傳輸至本機電腦進行分析。

4. 在接下來的幾個課程中, 切換回遠端計算內容。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 製作 SQL Server 資料的圖表](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)