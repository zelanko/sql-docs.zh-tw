---
title: 使用 XDF 檔案移動資料
description: RevoScaleR 教學課程 13：如何在 SQL Server 上使用 XDF 與 R 語言移動資料。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9c7e5ce4cbe995fd677acd406187dfaf264a7461
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85680008"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>在 SQL Server 與 XDF 檔案之間移動資料 (SQL Server 和 RevoScaleR 教學課程)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

此教學課程是 [RevoScaleR 教學課程系列](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的第 13 個，該系列說明如何搭配 SQL Server 使用 [RevoScaleR 函式](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) \(英文\)。

在此教學課程中，您將了解如何使用 XDF 檔案，在遠端與本機計算內容之間傳輸資料。 將資料儲存在 XDF 檔案中，可讓您對資料執行轉換。

完成時，使用檔案中的資料來建立新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 函式可以將轉換套用至資料，並執行資料框架與 .xdf 檔案之間的轉換。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>從 XDF 檔案建立 SQL Server 資料表

您要再次使用信用卡詐騙資料才能進行本練習。 在此案例中，您需要對加州、奧勒崗州和華盛頓州的使用者執行一些額外的分析。 為了提升效率，您決定只將這些州的資料儲存至本機電腦，並且僅使用性別、持卡人、州和餘額等變數。

1. 重複使用您稍早建立的 `stateAbb` 變數，以識別要包含的層級，並且將它們寫入新變數 `statesToKeep`。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **結果**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. 定義想要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢從 SQL Server 帶過來的資料。  稍後您將使用此變數作為 **rxImport** 的 inData  引數。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    請確定查詢中沒有隱藏的字元，例如換行字元或定位字元。
  
3. 接下來，定義在 R 中使用資料時要使用的資料行。例如，在較小的資料集中，您只需要三個因素層級，因為查詢只會傳回三個州的資料。  套用 `statesToKeep` 變數來識別要包含的正確層級。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 將計算內容設定為 [本機]  ，因為您想要讓所有資料都可在本機電腦上使用。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata) 函式可以將資料從任何支援的資料來源匯入到本機 XDF 檔案。 當您想要對資料執行許多不同的分析，但想要避免一再地執行相同的查詢時，使用資料的本機複本會很方便。

5. 藉由將先前定義為引數的變數傳遞給 **RxSqlServerData**，以建立資料來源物件。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 呼叫 **rxImport**，將資料寫入至目前工作目錄中名為 `ccFraudSub.xdf` 的檔案。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    **rxImport** 函式傳回的 `localDs` 物件是輕量型 **RxXdfData** 資料來源物件，代表儲存在本機磁碟上的資料檔案 `ccFraud.xdf`。
  
7. 對 XDF 檔案呼叫 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) ，確認資料結構描述相同。
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **結果**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. 您現在可以呼叫各種 R 函式來分析 **localDs** 物件，就像是對 SQL Server 上的來源資料一樣。 例如，您可能會依性別進行摘要：
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>後續步驟

此教學課程為 **RevoScaleR** 與 SQL Server 的多部分教學課程系列作總結。 它為您介紹了許多與資料相關和計算的概念，讓您能夠以自己的資料和專案需求作為基礎繼續進行。

若要加深對於 **RevoScaleR** 的知識，您可以返回 R 教學課程清單，逐步執行您可能錯過的任何練習。 或者，請檢閱目錄中的操作說明文章，以取得一般工作的相關資訊。

> [!div class="nextstepaction"]
> [適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)