---
title: 建立新的 SQL Server 資料表使用 RevoScaleR rxDataStep-SQL Server Machine Learning
description: 教學課程逐步解說如何建立 SQL Server 上使用 R 語言的 SQL Server 資料表。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 484f238e53db21030b04cdf46b86271236509989
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962260"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>新 SQL Server 使用 rxDataStep 建立資料表 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課，您了解如何在記憶體中的資料框架之間移動資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內容，以及本機檔案。

> [!NOTE]
> 這一課使用不同的資料集。 航班延遲資料集是廣泛用於機器學習服務實驗的公用資料集。 此範例中使用的資料檔案可與其他產品範例相同的目錄中。

## <a name="load-data-from-a-local-xdf-file"></a>從本機 XDF 檔案載入資料

在本教學課程的第一個部分，您已使用**RxTextData**函式，從文字檔中，R 將資料匯入，並接著使用**RxDataStep**函式來將資料移入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

這一課會採用不同的方式，並使用資料，從檔案儲存在[XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)。 執行一些輕量型轉換使用 XDF 檔案對資料之後，您必須儲存已轉換的資料到新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。

**什麼是 XDF？**

XDF 格式是針對高維度資料開發的 XML 標準，而且原生檔案格式是由[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 它是最佳化資料列和資料行處理與分析之 R 介面的二進位檔案格式。  您可以使用它來移動資料以及儲存對分析有用的資料子集。

1. 將計算內容設為您的本機工作站。 **在此步驟會需要 DDL 權限。**

    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 **RxXdfData** 函數，來定義新的資料來源物件。 若要定義 XDF 資料來源，指定資料檔案的路徑。  

    您可以指定使用文字變數檔案的路徑。 不過，在此情況下，有一個很好用捷徑，就是使用**rxGetOption**函式，並從範例資料目錄中取得檔案 (AirlineDemoSmall.xdf)。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 對記憶體中的資料呼叫 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) ，即可檢視資料集的摘要。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**結果**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> 是否注意到不需要呼叫任何其他函數就可以將資料載入至 XDF 檔案，而且可以立即對資料呼叫 **rxGetVarInfo** 嗎？ 這是因為 XDF 是預設暫時儲存方法**RevoScaleR**。 XDF 檔案，除了**rxGetVarInfo**函式現在支援多個來源的類型。

## <a name="move-contents-to-sql-server"></a>將內容移到 SQL Server

與在本機 R 工作階段中建立 XDF 資料來源，您現在可以繼續這項資料到資料庫資料表時，儲存*DayOfWeek*作為值從 1 到 7 的整數。

1. 定義 SQL Server 資料來源物件，指定要包含資料，以及遠端伺服器連接的資料表。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 為求安全起見，包含一個步驟，以檢查是否具有相同名稱的資料表已經存在，而且如果存在的話，請刪除資料表。 相同名稱的現有資料表可防止建立新的資源。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. 將資料載入至使用表**rxDataStep**。 此函式會移動資料兩個已定義資料來源，並可以選擇性地轉換資料移動。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    這是相當大的資料表，，因此請等候直至您看見類似這一個最終狀態訊息：*Rows Read:200000，total 處理的資料列：600000*。
     
## <a name="load-data-from-a-sql-table"></a>從 SQL 資料表載入資料

一旦資料存在於資料表中，您可以使用簡單 SQL 查詢來載入。 

1. 建立新的 SQL Server 資料來源。 輸入是您剛建立並載入資料的新資料表上的查詢。 此定義加入因數層級*DayOfWeek*資料行中，使用*colInfo*引數**RxSqlServerData**。
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. 呼叫**rxSummary**一次，以檢閱您的查詢中的資料摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxDataStep 執行區塊處理分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)