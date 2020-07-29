---
title: 使用 rxDataStep 建立資料表
description: RevoScaleR 教學課程 11：如何在 SQL Server 上使用 R 語言建立 SQL Server 資料表。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0550c90807328cf89d8d533ac583c8410c79f5c2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728592"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>使用 rxDataStep 建立新的 SQL Server 資料表 (SQL Server 和 RevoScaleR 教學課程)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 11 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將會了解如何在記憶體內部資料框架、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 內容與本機檔案之間移動資料。

> [!NOTE]
> 此教學課程使用不同的資料集。 航空公司誤點資料集是廣泛用於機器學習實驗的公用資料集。 這個範例中使用的資料檔案提供也可以在與其他產品範例相同的目錄中取得。

## <a name="load-data-from-a-local-xdf-file"></a>從本機 XDF 檔案載入資料

在此教學課程系列的前半部中，您已經使用 **RxTextData** 函式將資料從文字檔匯入到 R，並使用 **RxDataStep** 函式將資料移入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

此教學課程採用不同的方法，並使用以 [XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format) \(英文\) 所儲存檔案中的資料。 使用 XDF 檔案對資料執行一些輕量型轉換之後，您會將轉換的資料儲存至新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。

**什麼是 XDF？**

XDF 格式是針對高維度資料所開發的 XML 標準，而且是 [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf) 所使用的原生檔案格式。 它是最佳化資料列和資料行處理與分析之 R 介面的二進位檔案格式。  您可以使用它來移動資料以及儲存對分析有用的資料子集。

1. 將計算內容設為您的本機工作站。 **此步驟需要 DDL 權限。**

    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 **RxXdfData** 函數，來定義新的資料來源物件。 若要定義 XDF 資料來源，請指定資料檔案的路徑。  

    您可以使用文字變數指定檔案的路徑。 不過，在此情況下，有一個方便的快捷方式，就是使用 **rxGetOption** 函式，並從範例資料目錄取得檔案 (AirlineDemoSmall.xdf)。
  
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
> 是否注意到不需要呼叫任何其他函數就可以將資料載入至 XDF 檔案，而且可以立即對資料呼叫 **rxGetVarInfo** 嗎？ 這是因為 XDF 是 **RevoScaleR** 的預設暫時儲存方法。 除了 XDF 檔案以外，**rxGetVarInfo** 函式現在支援多個來源類型。

## <a name="move-contents-to-sql-server"></a>將內容移至 SQL Server

在本機 R 工作階段中建立 XDF 資料來源之後，您現在可以將此資料移至資料庫資料表，並將 DayOfWeek  儲存為值為 1 到 7 的整數。

1. 定義 SQL Server 資料來源物件、指定要包含資料的資料表，以及與遠端伺服器的連線。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 基於謹慎起見，請加入一個步驟來檢查是否已有相同名稱的資料表存在；如果有的話，則刪除該資料表。 若已存在具有相同名稱的現有資料表，則無法建立新的資料表。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. 使用 **rxDataStep**，將資料載入資料表。 此函式會在兩個已定義的資料來源之間移動資料，而且可以選擇性地轉換途中的資料。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    這個資料表相當大，請稍候片刻，直到看到如下的最終狀態訊息：*讀取的資料列：200000，已處理的資料列總數：600000*。
     
## <a name="load-data-from-a-sql-table"></a>從 SQL 資料表載入資料

一旦資料存在於資料表中，您就可以使用簡單的 SQL 查詢來加以載入。 

1. 建立新的 SQL Server 資料來源。 輸入是您剛建立並載入資料的新資料表上的查詢。 此定義會使用 **RxSqlServerData**的 colInfo  引數，為 DayOfWeek  資料行加入因數層級。
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. 再次呼叫 **rxSummary** 以檢閱查詢中的資料摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxDataStep 執行區塊處理分析](../../machine-learning/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)