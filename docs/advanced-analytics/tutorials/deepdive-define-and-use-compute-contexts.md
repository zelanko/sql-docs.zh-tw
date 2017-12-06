---
title: "定義及使用計算內容 (資料科學深入探討) | Microsoft Docs"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a682a40a9a62af3e1ff18ec0cc777ac9c1da7a9e
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/01/2017
---
# <a name="define-and-use-compute-contexts"></a>定義及使用計算內容


假設您要在伺服器 (而不是本機電腦) 上執行一些更複雜的計算。 若要這麼做，您可以建立計算內容，使 R 程式碼在伺服器上執行。

**RxInSqlServer** 函數是 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 套件中提供的其中一個增強型 R 函數。 此函數可處理下列工作：建立資料庫連接，以及在本機電腦和遠端執行內容之間傳遞物件。

在此步驟中，您將了解如何使用 **RxInSqlServer** 函數，透過 R 程式碼來定義計算內容。

若要建立計算內容，需要下列有關 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的基本資訊：

- 執行個體的連接字串
- 輸出應該如何處理的規格
- 用於啟用追蹤或用於指定共用目錄的選擇性引數

## <a name="create-and-set-a-compute-context"></a>建立及設定計算內容

1. 指定要進行計算之執行個體的連接字串。  這只是您要傳遞至 *RxInSqlServer* 函數以建立計算內容的幾個變數之一。 您可以重複使用稍早建立的連接字串，或如果您要將計算移動到其他伺服器或使用不同的身分識別，則建立不同的連接字串。

    **使用 SQL 登入**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user name>;Pwd=<password>"
      ```

    **使用 Windows 驗證**

      ```R
      sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
      ```
2. 指定您要如何處理輸出。 在下列程式碼中，您將指定工作站上的 R 工作階段應該永一律等候 R 工作結果，而不會從遠端計算傳回主控台輸出。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 的 *wait* 引數支援下列選項：
  
    -   **TRUE**： 工作將會被封鎖，而且在完成或失敗之前都不會傳回。  如需詳細資訊，請參閱[分散式和 Microsoft R 中的平行運算](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)。
  
    -   **FALSE**： 工作將不會被封鎖，而且會立即傳回，讓您繼續執行其他 R 程式碼。 不過，即使在非封鎖模式中，也必須在執行工作時保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與用戶端的連線。

3. 您可以選擇性地指定本機 R 工作階段以及遠端  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 電腦和其帳戶共同使用之本機目錄的位置。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 如果您想要以手動方式建立共用的特定目錄，您可以加入類似下列一行。 若要判斷目前正在使用哪一個資料夾的共用，請執行`rxGetComputeContext`，它會傳回有關目前詳細資料的計算內容。 如需詳細資訊，請參閱 [ScaleR 參考](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinsqlserver)。

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 已準備好所有變數，做為建立 RxInSqlServer 建構函式引數提供*計算內容物件*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    您可能會發現 RxInSqlServer * 的語法是與您先前用來定義資料來源的 RxSqlServerData 函式的幾乎完全相同。 但是，有一些重要的差異。
      
    - 資料來源物件，定義使用函式 RxSqlServerData，指定儲存資料。
    
    - 相反地，（使用 RxInSqlServer 的函式定義） 的計算內容會指出彙總和其他計算的位置進行。
    
    定義計算內容不會影響您可能會在工作站上執行的任何其他泛型 R 計算，而且不會變更資料的來源。 例如，您可以將本機文字檔定義為資料來源，但將計算內容變更為 SQL Server，並且執行 SQL Server 電腦上資料的所有讀取和摘要。

## <a name="enable-tracing-on-the-compute-context"></a>啟用計算內容的追蹤

有時候作業可在您的本機內容上運作，但在遠端計算內容中執行時則發生問題。 如果您想要分析問題或監視效能，則可以在計算內容中啟用追蹤，以支援執行階段疑難排解。

1. 建立新的計算內容使用相同的連接字串，但加入引數*traceEnabled*和*traceLevel*至*RxInSqlServer*建構函式。

    ```R
    sqlComputeTrace <- RxInSqlServer(
        connectionString = sqlConnString,
        #shareDir = sqlShareDir,
        wait = sqlWait,
        consoleOutput = sqlConsoleOutput,
        traceEnabled = TRUE,
        traceLevel = 7)
    ```
  
    在此範例中，*traceLevel* 屬性設定為 7，表示「顯示所有追蹤資訊」。

2. 若要變更計算內容，請使用 rxSetComputeContext 函數，並依名稱指定的內容。

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > 在本教學課程中，我們將使用未啟用追蹤的計算內容。 這是因為尚未經過啟用追蹤選項的效能測試的所有作業。
    > 
    > 不過，如果您決定要使用追蹤，請注意您的體驗可能會受到網路連線。

現在，您已建立遠端計算內容，您將了解如何變更計算內容，以在伺服器上或在本機執行 R 程式碼。

## <a name="next-step"></a>下一個步驟

[建立和執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


## <a name="previous-step"></a>上一個步驟

[查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)


