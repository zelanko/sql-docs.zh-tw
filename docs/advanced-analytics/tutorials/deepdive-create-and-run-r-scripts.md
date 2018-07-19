---
title: 建立和執行 R 指令碼 （SQL 與 R 深入探討） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1ff4b72b535f97ba0132dd5e2712b56f90effb10
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204690"
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>建立和執行 R 指令碼 （SQL 與 R 深入探討）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

現在您已設定資料來源並建立一或數個計算內容，您已準備好要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來執行一些強大的 R 指令碼。  在這一課，您可以使用 server 計算內容來執行一些常見的機器學習服務工作：

- 將資料視覺化，並產生一些摘要統計資料
- 建立線性迴歸模型
- 建立羅吉斯迴歸模型
- 對新資料計分，並建立分數的長條圖

## <a name="change-compute-context-to-the-server"></a>變更計算至伺服器的內容

執行任何 R 程式碼之前，您必須指定「目前」或「使用中」的計算內容。

1. 若要啟用您已使用 R 定義的計算內容，請使用 **rxSetComputeContext** 函數，如下所示：
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    當您執行此陳述式時，所有後續的計算發生在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定電腦*sqlCompute*參數。
  
2. 如果您決定在工作站上執行 R 程式碼，您可以使用  **local** 關鍵字，將計算內容切換回本機電腦。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    如需此函數支援之其他關鍵字的清單，請從 R 命令列輸入 `help("rxSetComputeContext")` 。
  
3. 指定計算內容之後，它會保持使用中，直到您變更為止。 不過，任何「無法」在遠端伺服器內容中執行的 R 指令碼都將在本機執行。

## <a name="compute-some-summary-statistics"></a>計算部分的摘要統計資料

若要查看計算內容的運作方式，請嘗試產生某些摘要統計資料使用`sqlFraudDS`資料來源。  請記住，資料來源物件只定義使用; 的資料它不會變更計算內容。

+ 若要執行的摘要在本機，使用**rxSetComputeContext**並指定_本機_關鍵字。
+ 若要在 SQL Server 電腦上建立相同的計算，請切換至您稍早定義的 SQL 計算內容。

1. 呼叫[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)函式，並傳遞必要的引數，例如公式和資料來源，並將結果指派給變數`sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 語言提供許多摘要函式，但**rxSummary**支援在各種遠端計算內容，包括上執行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 類似功能的相關資訊，請參閱[資料摘要使用 RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
2. 當處理完成時，您可以列印的內容`sumOut`變數至主控台。
  
    ```R
    sumOut
    ```
  
    > [!NOTE]
    > 請勿嘗試在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦傳回結果之前就列印結果，否則可能會收到錯誤。

**結果**

*Summary Statistics Results for: ~gender + balance + numTrans +*

 *numIntlTrans + creditLine*

 *Data: sqlFraudDS (RxSqlServerData Data Source)*

 *Number of valid observations: 10000*

 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*

 *balance       4075.0318 3926.558714            0   25626 100000*

 *numTrans        29.1061   26.619923 0     100 10000    0           100000*

 *numIntlTrans     4.0868    8.726757 0      60 10000    0           100000*

 *creditLine       9.1856    9.870364 1      75 10000    0          100000*

 *性別類別計數*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male   6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>加入最大和最小值

根據計算的摘要統計資料，您發現與資料相關的一些實用資訊，並想要放入資料來源，以供進一步計算使用。 例如，最小和最大值可以用來計算長條圖。 基於這個理由，讓我們加入的高低值**RxSqlServerData**資料來源。

幸運的是[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]包含最佳化的函式可以有效率地轉換成類別因數資料的整數資料。

1. 一開始先設定一些暫存變數。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用稍早建立的變數 `ccColInfo` 來定義資料來源中的資料行。
  
    此外，請加入一些新的計算資料行 (`numTrans`， `numIntlTrans`，和`creditLine`) 資料行集合。
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. 具有更新的資料行集合中，套用下列陳述式來建立更新的版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]先前定義的資料來源。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    `sqlFraudDS`資料來源現在包含新的資料行加入使用`ccColInfo`。
  

此時，所做的修改會影響只有資料來源物件中 R;任何新資料寫入資料庫資料表尚未。 不過，您可以使用所擷取的資料`sumOut`變數來建立視覺效果和摘要。 下一個步驟中，您會學習如何執行此動作時切換計算內容。

> [!TIP]
> 如果您忘記您所使用的計算內容，執行`rxGetComputeContext()`。  [RxLocalSeq 計算內容] 的傳回值會指出您在本機計算內容執行。

## <a name="next-step"></a>下一步

[使用 R 製作 SQL Server 資料的圖表](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>上一個步驟

[定義及使用計算內容](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
