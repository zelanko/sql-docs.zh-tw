---
title: 計算摘要統計資料 RevoScaleR 教學課程-SQL Server Machine Learning
description: 教學課程逐步解說，如何計算 SQL Server 上使用 R 語言的統計摘要統計資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 945b7cb32c64c343ca7bb5ab2aab4169fd7bea24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962282"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>計算摘要統計資料，在 R 中 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

它會使用已建立的資料來源與先前的課程中建立的計算內容，在此影片中執行強大的 R 指令碼。 在這一課，您將使用本機和遠端伺服器計算內容，來執行下列工作：

> [!div class="checklist"]
> * 將計算內容切換至 SQL Server
> * 取得遠端資料物件上的摘要統計資料
> * 計算本機摘要

如果您已完成先前的課程，您應該有這些遠端計算內容： sqlCompute 和 sqlComputeTrace。 邁向未來，您使用將 sqlCompute 和本機計算內容在後續課程中。

使用 R IDE 或**Rgui**在這一課中執行 R 指令碼。

## <a name="compute-summary-statistics-on-remote-data"></a>計算對遠端資料的摘要統計資料

您可以從遠端執行所有 R 程式碼之前，您需要指定遠端計算內容。 所有後續的計算上進行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定的電腦*sqlCompute*參數。

計算內容保持作用中，直到您變更為止。 不過，任何 R 指令碼都*無法*執行遠端伺服器內容中的將會自動在本機執行。

若要查看計算內容的運作方式，產生 sqlFraudDS 資料來源上的遠端 SQL Server 上的摘要統計資料。 在建立此資料來源物件[兩個課程](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)和代表 ccFraudSmall 資料庫中的資料表 RevoDeepDive。 

1. 若要在上一課中建立的 sqlCompute 切換計算內容：
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. 呼叫[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)函式，並傳遞必要引數，例如公式、 資料來源，並將結果指派給變數`sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 語言提供許多摘要函式，但**rxSummary**中**RevoScaleR**支援在各種遠端計算內容，包括上執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需類似函數的詳細資訊，請參閱[資料摘要使用 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
3. 列印到主控台 sumOut 的內容。
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 如果您收到錯誤，請等候幾分鐘的時間才能完成，然後再重試此命令執行。

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
  
2. 當從 SQL Server 擷取資料，通常就可以取得較佳的效能增加每個讀取，擷取的資料列數假設增加的區塊大小可以容納在記憶體中。 執行下列命令，以增加的值*rowsPerRead*資料來源上的參數。 之前， *rowsPerRead* 的值已設為 5000。
  
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
  
   實際的結果應該與您在 **電腦的內容中執行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 時相同。 不過，作業可能會更快或更慢。 大部分取決於資料庫連線，因為正在將資料傳輸至本機電腦進行分析。

4. 切換回遠端計算內容的 [下一步] 的數個課程。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 R 製作 SQL Server 資料的圖表](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)