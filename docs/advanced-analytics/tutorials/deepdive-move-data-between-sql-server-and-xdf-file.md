---
title: "SQL Server 和 XDF 檔案 （SQL 與 R 深入探討） 之間移動資料 |Microsoft 文件"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs:
- R
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 19502fbed507fff36c038145d0e4dbd683d7acdc
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-and-r-deep-dive"></a>SQL Server 和 XDF 檔案 （SQL 與 R 深入探討） 之間移動資料
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在此步驟中，您了解如何使用 XDF 檔案之間的遠端和本機計算內容傳輸資料。 XDF 檔案中儲存資料，可讓您的資料上執行轉換。

當您完成時，您使用資料檔案中建立新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表。 此函式[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)可以將轉換套用至資料，並執行資料框架和.xdf 檔案之間的轉換。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>建立 XDF 檔案從 SQL Server 資料表

針對此練習，您的信用卡詐欺資料再次使用。 在此案例中，您需要對加州、奧勒崗州和華盛頓州的使用者執行一些額外的分析。 為多個有效，您已決定將只有這兩種狀態的資料儲存在本機電腦，並使用只變數性別、 持卡人、 狀態和平衡。

1. 重複使用`stateAbb`您先前識別包含此項目，並將它們寫入至新的變數，層級建立的變數`statesToKeep`。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **結果**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. 定義您想要透過從 SQL Server 整合的資料使用[!INCLUDE[tsql](../../includes/tsql-md.md)]查詢。  稍後您可以使用這個變數做為*inData*引數**rxImport**。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    請確定查詢中沒有隱藏的字元，例如換行字元或定位字元。
  
3. 接下來，定義要使用 r 中的資料時使用的資料行例如，在較小的資料集，您需要只有三個因素層級，因為查詢會傳回只有三個狀態的資料。  套用`statesToKeep`來識別要包含正確的層級的變數。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 計算內容設為**本機**，因為您要在本機電腦上的所有可用的資料。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函式可以從匯入資料的任何支援的資料來源到本機 XDF 檔案。 使用資料的本機複本時，方便您想要怎麼做許多不同的分析資料，但是想要避免一再執行相同的查詢。

5. 藉由傳遞做為引數之前定義變數建立資料來源物件**RxSqlServerData**。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 呼叫**rxImport**將資料寫入至名為`ccFraudSub.xdf`，目前工作目錄中。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    `localDs`所傳回物件**rxImport**函式是輕量級**RxXdfData**資料來源物件，代表`ccFraud.xdf`資料檔案儲存在本機磁碟上。
  
7. 對 XDF 檔案呼叫 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) ，確認資料結構描述相同。
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **結果**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. 您現在可以呼叫各種 R 函數來分析 `localDs` 物件，就像是對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的資料來源一樣。 例如，您可能會依性別的總結：
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

現在您已經熟悉如何使用計算內容和各種資料來源，接下來可嘗試一些有趣的作業。 在下一個和最後一課，您可以建立在遠端伺服器執行自訂的 R 函數的簡單模擬。

## <a name="next-step"></a>下一步

[建立簡單的模擬](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>上一個步驟

[分析本機計算內容中的資料](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



