---
title: 建立新的 SQL Server 資料表使用 rxDataStep （SQL 與 R 深入探討） |Microsoft 文件
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 2fe521908e34afc1ae3ec23d56cb9d5cea801f1b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202320"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-and-r-deep-dive"></a>建立新的 SQL Server 資料表使用 rxDataStep （SQL 與 R 深入探討）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在這一課，您會學習如何記憶體中的資料框架之間移動資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內容，以及本機檔案。

> [!NOTE]
> 這一課使用不同的資料集。 Airline 延遲 dataset 是廣泛用於機器學習實驗的公用資料集。 此範例中使用資料檔案皆可與其他產品範例相同的目錄中。

## <a name="create-sql-server-table-from-local-data"></a>從本機的資料建立 SQL Server 資料表

在本教學課程的第一個部分，您已經使用**RxTextData** R 從文字檔案，將資料匯入函式，並接著使用**RxDataStep**函式將資料插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

這一課會採用不同的方式，並從檔案將會使用資料儲存在[XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)。 使用 XDF 檔案的資料部分輕量型轉換之後，您已轉換的資料儲存到新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。

**什麼是 XDF？**

XDF 格式是針對高維度資料開發 XML 標準和原生檔案格式是由[Server 機器學習](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 它是最佳化資料列和資料行處理與分析之 R 介面的二進位檔案格式。  您可以使用它來移動資料以及儲存對分析有用的資料子集。

1. 將計算內容設為您的本機工作站。 **此步驟需要 DDL 權限。**

  
    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 **RxXdfData** 函數，來定義新的資料來源物件。 若要定義 XDF 資料來源時，指定資料檔案的路徑。  

    您可以指定要使用的文字變數的檔案路徑。 不過，在此情況下，沒有便利捷徑，就是使用**rxGetOption**函式，並從範例資料目錄中取得的檔案 (AirlineDemoSmall.xdf)。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 對記憶體中的資料呼叫 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) ，即可檢視資料集的摘要。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**結果**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> 是否注意到不需要呼叫任何其他函數就可以將資料載入至 XDF 檔案，而且可以立即對資料呼叫 **rxGetVarInfo** 嗎？ 原因是 XDF 是 RevoScaleR 的預設暫時儲存方法。 除了 XDF 檔案**rxGetVarInfo**函式現在支援多個來源的類型。
  
4. 將放入此資料[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表，儲存_DayOfWeek_為整數的值從 1 到 7。
  
    若要這樣做，請先定義 SQL Server 資料來源。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. 檢查是否有相同名稱的資料表存在，並刪除存在的資料表。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. 建立資料表，然後使用 **rxDataStep**的各種產品範例。 此函式會移動資料，兩個已定義資料來源，並可以選擇性地轉換資料路由。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    這是相當大的資料表，您會看到與下列類似的最終狀態訊息，因此等待： *Rows Read: 200000，資料列處理的總數： 600000*。
     
7. 將計算內容設定回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦。

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. 在新的資料表上使用簡單 SQL 查詢，建立新的 SQL Server 資料來源。 此定義將係數等級*DayOfWeek*資料行中，使用*colInfo*引數**RxSqlServerData**。
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. 呼叫**rxSummary**一次，以檢閱您在查詢中資料的摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>下一步

[使用 rxDataStep 執行區塊處理分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>上一個步驟

[使用 rxImport 將資料載入記憶體](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
