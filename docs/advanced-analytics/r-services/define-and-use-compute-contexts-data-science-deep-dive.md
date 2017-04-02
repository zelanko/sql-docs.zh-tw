---
title: "定義及使用計算內容 (資料科學深入探討) | Microsoft Docs"
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
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 定義及使用計算內容 (資料科學深入探討)
您已決定要在伺服器 (而不是本機電腦) 上執行一些更複雜的計算。 若要這樣做，您必須建立可讓您在伺服器上執行 R 程式碼的計算內容。  
  
[RxInSqlServer](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver) 函數是 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 套件中提供的其中一個增強型 R 函數。 此函數可處理下列工作：建立資料庫連接，以及在本機電腦和遠端執行內容之間傳遞物件。  
  
在此步驟中，您將了解如何使用 *RxInSqlServer* 函數，透過 R 程式碼來定義計算內容。  


  
## 建立及設定計算內容  
若要建立計算內容，需要下列有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的基本資訊：  
  
-   執行個體的連接字串  
-   輸出應該如何處理的規格  
-   用於啟用追蹤或用於指定共用目錄的選擇性引數


 讓我們開始吧。

1.  指定要進行計算之執行個體的連接字串。  這只是您要傳遞至 *RxInSqlServer* 函數以建立計算內容的幾個變數之一。 

    **使用 SQL 登入**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>" 
      ```

    **使用整合式 Windows 驗證**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"" 
      ```
2.  指定您要如何處理輸出。 在下列程式碼中，您將指定工作站上的 R 工作階段應該永一律等候 R 工作結果，而不會從遠端計算傳回主控台輸出。  
  
    ```R  
    sqlWait <- TRUE   
    sqlConsoleOutput <- FALSE   
    ```  
  
    *RxInSqlServer* 的 *wait* 引數支援下列選項：  
  
    -   **TRUE**： 工作將會被封鎖，而且在完成或失敗之前都不會傳回。  如需封鎖和非封鎖工作的詳細資訊，請參閱 
  
    -   **FALSE**： 工作將不會被封鎖，而且會立即傳回，讓您繼續執行其他 R 程式碼。 不過，即使在非封鎖模式中，也必須在執行工作時保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與用戶端的連線。  

3. 您可以選擇性地指定本機 R 工作階段以及遠端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦和其帳戶共同使用之本機目錄的位置。
    
    ```R  
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")   
    
    ## Add this line to create directory if it does not exist
    dir.create(sqlShareDir, recursive = TRUE) 
    ```  
    建議您使用預設值，而不是手動為這個引數指定資料夾。 如需詳細資訊，請參閱 [ScaleR 參考](https://msdn.microsoft.com/microsoft-r/scaler/rxinsqlserver)。
    
    如果您只是想要知道正在使用的資料夾，可以執行 `rxGetComputeContext` 檢視目前計算內容的詳細資料。 
  

4.  準備好所有變數之後，請將這些變數當作引數提供給 `RxInSqlServer` 建構函式，以定義計算內容物件。  
  
    ```R  
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,        
         #shareDir = sqlShareDir,       
         wait = sqlWait,   
         consoleOutput = sqlConsoleOutput)  
    ```  
  
    您可能會觀察到 *RxInSqlServer* 的語法，幾乎與先前用來定義資料來源之 *RxSqlServerData* 函數的語法相同。 但是，有一些重要的差異。  
  
    -   資料來源物件 (使用 *RxSqlServerData* 函數所定義) 指定資料的儲存位置。  
  
    -   相反地，計算內容 (使用 *RxInSqlServer* 函數所定義) 表示進行彙總和其他計算的位置。  
  
    定義計算內容不會影響您可能會在工作站上執行的任何其他泛型 R 計算，而且不會變更資料的來源。 例如，您可以將本機文字檔定義為資料來源，但將計算內容變更為 SQL Server，並且執行 SQL Server 電腦上資料的所有讀取和摘要。 
  
## 啟用計算內容的追蹤  
處理本機內容的作業有時會在特定遠端計算內容中執行時遇到問題。 如果您想要分析問題或監視效能，則可以在計算內容中啟用追蹤，以支援執行階段疑難排解。  
  
1. 建立使用相同連接字串的新計算內容，但將 *traceEnabled* 和 *traceLevel* 引數新增至 *RxInSqlServer* 建構函式。  
  
    ```R  
    sqlComputeTrace <- RxInSqlServer(   
        connectionString = sqlConnString,        
        #shareDir = sqlShareDir,  
        wait = sqlWait,   
        consoleOutput = sqlConsoleOutput,       
        traceEnabled = TRUE,
        traceLevel = 7)  
    ```  
  
    在此範例中，*traceLevel* 屬性會設定為 7，表示「顯示所有追蹤資訊」。  

2. 若要隨時切換至這個計算內容，請使用 *rxSetComputeContext* 函數，並依名稱指定內容。

    ```R  
    rxSetComputeContext( sqlComputeTrace)
    ```

    在本教學課程中，我們將使用未啟用追蹤的計算內容。 所有作業都未測試已啟用追蹤之選項的效能，而且您的體驗可能會因網路連線能力而異。  
  
現在，您已建立遠端計算內容，您將了解如何變更計算內容，以在伺服器上或在本機執行 R 程式碼。  
  
## 下一個步驟  
[第 2 課︰建立及執行 R 指令碼 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## 上一個步驟  
[查詢及修改 SQL Server 資料 &#40;資料科學深入探討&#41;](../../advanced-analytics/r-services/query-and-modify-the-sql-server-data-data-science-deep-dive.md)  
  
## 另請參閱  
[資料科學深入探討︰使用 RevoScaleR 套件](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
