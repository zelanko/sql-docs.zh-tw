---
title: "SQL Server 和 XDF 檔案之間移動資料 |Microsoft 文件"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a140cc358afab1f1ff324e0a47ed67501ee75e23
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="move-data-between-sql-server-and-xdf-file"></a>在 SQL Server 與 XDF 檔案之間移動資料

當您使用的本機計算內容時，您可以存取這兩個本機資料檔案和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（定義為 RxSqlServerData 資料來源） 的資料庫。

在本節中，您將了解如何取得資料，並將它儲存在本機電腦的檔案中，以便您可以對資料執行轉換。 當您完成時，您會使用檔案的資料來建立新的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]資料表中的，使用 rxDataStep。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>從 XDF 檔案建立 SQL Server 資料表

RxImport 函式可讓您從任何支援的資料來源匯入資料到本機 XDF 檔案。 如果您想要對儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料執行許多不同的分析，而且想要避免反覆執行相同的查詢，使用本機檔案會很方便。

針對此練習，您將再次使用信用卡詐騙資料。 在此案例中，您需要對加州、奧勒崗州和華盛頓州的使用者執行一些額外的分析。 為了提升效率，您決定只將這些州的資料儲存至本機電腦，並使用性別、持卡人、州和餘額等變數。

1. 重複使用您稍早建立的 *stateAbb* 向量，以識別要包含的層級，然後顯示新的變數 *statesToKeep*。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **結果**
    
    CA|OR|WA
    ----|----|----
    5|38|48
    
2. 現在您將定義想要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢從 SQL Server 帶過來的資料。  稍後您將使用此變數作為 *rxImport* 的 *inData*引數。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    請確定查詢中沒有隱藏的字元，例如換行字元或定位字元。
  
3. 接下來，您將在其中定義要使用 r 中的資料時使用的資料行例如，在較小的資料集，您需要只有三個因素層級，因為查詢會傳回只有三個狀態的資料。  您可以重複使用 *statesToKeep* 變數來識別要包含的正確層級。
  
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
  
5. 藉由傳遞您做為 RxSqlServerData 引數中所定義的所有變數建立資料來源物件。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 然後，呼叫**rxImport**將資料寫入至名為`ccFraudSub.xdf`，目前工作目錄中。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    *LocalDs* rxImport 函數所傳回的物件是輕量級 RxXdfData 資料來源物件，代表 ccFraud.xdf 資料檔案儲存在本機磁碟上。
  
7. 呼叫 rxGetVarInfo XDF 檔案加以確認資料結構描述相同。
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **結果**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1: gender, Type: factor, no factor levels available*

    *Var 2: cardholder, Type: factor, no factor levels available*

    *Var 3: balance, Type: integer, Low/High: (0, 22463)*

    *Var 4: state, Type: factor, no factor levels available*
  
8. 您現在可以呼叫各種 R 函數來分析 *localDs* 物件，就像是對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的資料來源一樣。 例如：
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

現在您已經熟悉如何使用計算內容和各種資料來源，接下來可嘗試一些有趣的作業。 在下一課和最後一課，您將使用自訂 R 函數建立簡單的模擬，並在遠端伺服器上執行。

## <a name="next-step"></a>下一個步驟

[建立簡單的模擬](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>上一個步驟

[在本機計算內容中分析資料](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



