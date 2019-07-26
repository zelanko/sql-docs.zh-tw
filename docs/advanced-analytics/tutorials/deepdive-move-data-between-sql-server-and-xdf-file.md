---
title: 使用 RevoScaleR 在 SQL Server 與 XDF 檔案之間移動資料
description: 有關如何在 SQL Server 上使用 XDF 和 R 語言移動資料的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4109399386f119123591bb917f81290eebe7476e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469714"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>在 SQL Server 與 XDF 檔案之間移動資料 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在此步驟中, 您將瞭解如何使用 XDF 檔案, 在遠端和本機計算內容之間傳輸資料。 將資料儲存在 XDF 檔案中, 可讓您對資料執行轉換。

當您完成時, 您會使用檔案中的資料來建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的資料表。 函數[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)可以將轉換套用至資料, 並執行資料框架和 xdf 檔案之間的轉換。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>從 XDF 檔案建立 SQL Server 資料表

在此練習中, 您會再次使用信用卡詐騙資料。 在此案例中，您需要對加州、奧勒崗州和華盛頓州的使用者執行一些額外的分析。 為了提高效率, 您已決定只將這些狀態的資料儲存在本機電腦上, 並且只使用性別、持卡人、州和餘額的變數。

1. 重複使用您稍`stateAbb`早建立的變數來識別要包含的層級, 並將它們寫入新的`statesToKeep`變數。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **結果**
    
    CA|或|WA
    ----|----|----
    5|38|48
    
2. 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢, 定義您想要從 SQL Server 中導入的資料。  稍後您會使用此變數做為**rxImport**的*inData*引數。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    請確定查詢中沒有隱藏的字元，例如換行字元或定位字元。
  
3. 接下來, 定義在 R 中使用資料時所要使用的資料行。例如, 在較小的資料集中, 您只需要三個因素層級, 因為查詢只會傳回三個狀態的資料。  `statesToKeep`套用變數以識別要包含的正確層級。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 將計算內容設定為 [**本機**], 因為您想要在本機電腦上使用所有的資料。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函數可以將資料從任何支援的資料來源匯入到本機 XDF 檔案。 當您想要對資料執行許多不同的分析, 但想要避免在相同的情況下執行相同的查詢時, 使用資料的本機複本會很方便。

5. 將先前定義為引數的變數傳遞至**RxSqlServerData**, 以建立資料來源物件。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 呼叫**rxImport** , 將資料寫入至目前工作目錄`ccFraudSub.xdf`中名為的檔案。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    RxImport `localDs`函數所傳回的物件是輕量的**RxXdfData**資料來源物件, 代表儲存在本機`ccFraud.xdf`磁片上的資料檔案。
  
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

8. 您現在可以呼叫各種 R 函數來分析**localDs**物件, 就像您在 SQL Server 上的來源資料一樣。 例如, 您可能會依性別總結:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>後續步驟

這一課將介紹**RevoScaleR**和 SQL Server 上的多部分教學課程系列。 它為您介紹了許多與資料相關和計算的概念, 讓您能夠以自己的資料和專案需求做為基礎來繼續進行。

若要加深您對**RevoScaleR**的知識, 您可以返回 R 教學課程清單, 逐步執行您可能錯過的任何練習。 或者, 請參閱目錄中的操作說明文章, 以取得一般工作的相關資訊。

> [!div class="nextstepaction"]
> [適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)