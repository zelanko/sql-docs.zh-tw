---
title: 使用 RevoScaleR rxDataStep 建立新的 SQL Server 資料表
description: 有關如何在 SQL Server 上使用 R 語言建立 SQL Server 資料表的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b18f2bd42070746551d21ff7508e7fce58b49037
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714917"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>使用 rxDataStep 建立新的 SQL Server 資料表 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在這一課, 您將瞭解如何在記憶體中的資料框架、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]內容和本機檔案之間移動資料。

> [!NOTE]
> 本課程使用不同的資料集。 航空公司延遲資料集是廣泛用於機器學習實驗的公用資料集。 此範例中使用的資料檔案可在與其他產品範例相同的目錄中取得。

## <a name="load-data-from-a-local-xdf-file"></a>從本機 XDF 檔案載入資料

在本教學課程的前半部, 您已使用**RxTextData**函式, 將資料從文字檔匯入 R, 然後使用**RxDataStep**函數將資料移入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

這一課會採用不同的方法, 並使用以[XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)儲存之檔案中的資料。 使用 XDF 檔案對資料執行一些輕量轉換之後, 您會將轉換的資料儲存至新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料表。

**什麼是 XDF？**

XDF 格式是針對高維度資料所開發的 XML 標準, 而且是[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)所使用的原生檔案格式。 它是最佳化資料列和資料行處理與分析之 R 介面的二進位檔案格式。  您可以使用它來移動資料以及儲存對分析有用的資料子集。

1. 將計算內容設為您的本機工作站。 **此步驟需要 DDL 許可權。**

    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 **RxXdfData** 函數，來定義新的資料來源物件。 若要定義 XDF 資料來源, 請指定資料檔案的路徑。  

    您可以使用文字變數指定檔案的路徑。 不過, 在這種情況下, 有一個方便的快捷方式, 也就是使用**rxGetOption**函式, 並從範例資料目錄取得檔案 (airlinedemosmall.xdf. xdf)。
  
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
> 是否注意到不需要呼叫任何其他函數就可以將資料載入至 XDF 檔案，而且可以立即對資料呼叫 **rxGetVarInfo** 嗎？ 這是因為 XDF 是**RevoScaleR**的預設過渡儲存方法。 除了 XDF 檔案外, **rxGetVarInfo**函式現在也支援多個來源類型。

## <a name="move-contents-to-sql-server"></a>將內容移至 SQL Server

使用在本機 R 會話中建立的 XDF 資料來源時, 您現在可以將此資料移至資料庫資料表, 並將*DayOfWeek*儲存為值為1到7的整數。

1. 定義 SQL Server 的資料來源物件、指定要包含資料的資料表, 以及與遠端伺服器的連接。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 作為預防措施, 請加入一個步驟來檢查是否已有相同名稱的資料表存在, 並刪除資料表 (如果有的話)。 具有相同名稱的現有資料表會防止建立新的資料表。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. 使用**rxDataStep**將資料載入資料表。 此函式會在兩個已定義的資料來源之間移動資料, 而且可以選擇性地轉換資料的路由。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    這是相當大的資料表, 因此請等候直到看到如下的最終狀態消息:*讀取的資料列:200000, 已處理的資料列總數:600000*。
     
## <a name="load-data-from-a-sql-table"></a>從 SQL 資料表載入資料

一旦資料存在於資料表中, 您就可以使用簡單的 SQL 查詢來加以載入。 

1. 建立新的 SQL Server 資料來源。 輸入是您剛建立並載入資料的新資料表上的查詢。 這個定義會使用**RxSqlServerData**的*colInfo*引數, 加入*DayOfWeek*資料行的因數層級。
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. 再次呼叫**rxSummary**以檢查查詢中的資料摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [使用 rxDataStep 執行區塊處理分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)