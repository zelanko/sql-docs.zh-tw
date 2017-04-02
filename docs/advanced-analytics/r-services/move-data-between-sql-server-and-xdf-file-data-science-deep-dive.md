---
title: "在 SQL Server 與 XDF 檔案之間移動資料 (資料科學深入探討) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 在 SQL Server 與 XDF 檔案之間移動資料 (資料科學深入探討)
當您在本機計算內容中工作時，您可以存取本機資料檔案和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫 (定義為 *RxSqlServerData* 資料來源)。  
  
在本節中，您將了解如何取得資料，並將它儲存在本機電腦的檔案中，以便您可以對資料執行轉換。 完成時，您將透過 *rxDataStep*，使用檔案中的資料來建立新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料表。  
  
## 從 XDF 檔案建立 SQL Server 資料表  

*rxImport* 函數可讓您將資料從任何支援的資料來源匯入到本機 XDF 檔案。 如果您想要對儲存在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資料庫中的資料執行許多不同的分析，而且想要避免反覆執行相同的查詢，使用本機檔案會很方便。  
  
針對此練習，您將再次使用信用卡詐騙資料。 在此案例中，您需要對加州、奧勒崗州和華盛頓州的使用者執行一些額外的分析。 為了提升效率，您決定只將這些州的資料儲存至本機電腦，並使用性別、持卡人、州和餘額等變數。  
  
1.  重複使用您稍早建立的 *stateAbb* 向量，以識別要包含的層級，然後顯示新的變數 *statesToKeep*。  
  
    ```  
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)   
  
    statesToKeep  
  
    ```  
 **結果**
CA |  OR  | WA 
-- | -- | --
 5 |  38  | 48 
  
2.  現在您將定義想要使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查詢從 SQL Server 帶過來的資料。  稍後您將使用此變數作為 *rxImport* 的 *inData* 引數。  
  
    ```R  
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")  
  
    ```  
  
    請確定查詢中沒有隱藏的字元，例如換行字元或定位字元。  
  
3.  接下來，您將定義在 R 中使用資料時要使用的資料行。  
  例如，在較小的資料集中，您只需要三個因素層級，因為查詢只會傳回三個州的資料。  您可以重複使用 *statesToKeep* 變數來識別要包含的正確層級。  
  
    ```R  
    importColInfo <- list(   
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),       
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),     
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))   
            )  
  
    ```  
  
4.  將計算內容設定為 [本機]，因為您想要讓所有資料都可在本機電腦上使用。  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
5.  將您剛才定義為引數的所有變數傳遞至 *RxSqlServerData*，以建立資料來源物件。  
  
    ```R  
    sqlServerImportDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        sqlQuery = importQuery,   
        colInfo = importColInfo)  
  
    ```  
  
6.  然後，呼叫 *rxImport* 來將資料儲存在目前工作目錄中名為 `ccFraudSub.xdf` 的檔案。  
  
    ```R  
    localDS <- rxImport(inData = sqlServerImportDS,   
        outFile = "ccFraudSub.xdf",    
        overwrite = TRUE)  
  
    ```  
  
    *rxImport* 函數傳回的 *localDs* 物件是輕量型 *RxXdfData* 資料來源物件，代表儲存在本機磁碟上的資料檔案 ccFraud.xdf。  
  
7.  對 XDF 檔案呼叫 *rxGetVarInfo*，確認資料結構描述相同。  
  
    ```R  
    rxGetVarInfo(data = localDS)   
    ```  
    **結果**
    
    *rxGetVarInfo(data = localDS)*    
    *Var 1: gender, Type: factor, no factor levels available*    
    *Var 2: cardholder, Type: factor, no factor levels available*    
    *Var 3: balance, Type: integer, Low/High: (0, 22463)*    
    *Var 4: state, Type: factor, no factor levels available*
  
8.  您現在可以呼叫各種 R 函數來分析 *localDs* 物件，就像是對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的資料來源一樣。 例如：  
  
    ```R  
    rxSummary(~gender + cardholder + balance + state, data = localDS)    
    ```  
  
現在您已經熟悉如何使用計算內容和各種資料來源，接下來可嘗試一些有趣的作業。  
  
在下一課和最後一課，您將使用自訂 R 函數建立簡單的模擬，並在遠端伺服器上執行。  
  
## 下一個步驟  
[第 5 課︰建立簡單的模擬 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  
  
## 上一個步驟  
[第 4 課︰分析本機計算內容中的資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## 另請參閱  
[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
