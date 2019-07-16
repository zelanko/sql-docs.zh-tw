---
title: SQL Server 與 XDF 檔案使用 RevoScaleR-SQL Server Machine Learning 之間移動資料
description: 教學課程逐步解說如何使用 XDF 和 R 語言，在 SQL Server 移動資料。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f5800f315ee09328908b612c18faf6c77a7ac13c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962216"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>SQL Server 與 XDF 檔案 （SQL Server 和 RevoScaleR 教學課程） 之間移動資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在此步驟中，了解如何使用 XDF 檔案遠端和本機計算內容之間傳輸資料。 將資料儲存在 XDF 檔案，可讓您對資料執行轉換。

當您完成時，您使用中的資料檔案來建立新的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 此函式[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)可以將轉換套用至資料，並執行資料框架和.xdf 檔案之間的轉換。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>從 XDF 檔案建立 SQL Server 資料表

針對此練習中，您的信用卡詐騙資料再次使用。 在此案例中，您需要對加州、奧勒崗州和華盛頓州的使用者執行一些額外的分析。 若要更有效率，您已經決定要儲存在您的本機電腦上的只有這些州的資料和使用的只有變數性別、 持卡人、 狀態和平衡。

1. 重複使用`stateAbb`稍早識別包含此項目，並將它們寫入至新的變數，層級建立的變數`statesToKeep`。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **結果**
    
    CA|或|WA
    ----|----|----
    5|38|48
    
2. 定義您想要從 SQL Server，透過整合的資料使用[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。  稍後您可以使用此變數作為*inData*引數**rxImport**。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    請確定查詢中沒有隱藏的字元，例如換行字元或定位字元。
  
3. 接下來，定義要使用 r 中的資料時使用的資料行比方說，在較小的資料集，您需要只有三個因素層級，因為查詢會傳回三個州的資料。  套用`statesToKeep`變數來識別要包含正確的層級。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 若要設定計算內容**本機**，因為您想在您的本機電腦上的所有可用的資料。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函式可以匯入資料從任何支援的資料來源到本機 XDF 檔案。 當您想要執行許多不同的分析資料，但想要避免反覆執行相同的查詢時，使用資料的本機複本是方便。

5. 建立資料來源物件，先前定義為引數的變數傳遞**RxSqlServerData**。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 呼叫**rxImport**將資料寫入檔案，名為`ccFraudSub.xdf`，目前的工作目錄中。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    `localDs`所傳回的物件**rxImport**函式是輕量級**RxXdfData**資料來源物件，代表`ccFraud.xdf`資料檔案儲存在本機磁碟上。
  
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

8. 您現在可以呼叫各種 R 函數來分析**localDs**物件，就如同在 SQL Server 上的資料來源。 例如，您可能會依性別的總結：
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>後續步驟

在這一課到結束的多部分的教學課程系列**RevoScaleR**和 SQL Server。 它引進許多相關的資料和計算概念，讓您為基礎來繼續使用您自己的資料和專案的需求。

若要加強您對**RevoScaleR**，您可以傳回至 R 教學課程清單，以逐步執行您可能會遺失任何練習。 或者，檢視操作說明文章資料表中的一般工作的相關資訊的目錄。

> [!div class="nextstepaction"]
> [適用於 SQL Server 的 R 教學課程](sql-server-r-tutorials.md)