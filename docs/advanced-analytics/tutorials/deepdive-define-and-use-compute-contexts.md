---
title: 定義及使用計算內容 （SQL 和 R 深入探討） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6a76e07cb2ecd03a59112f6c39e3fa2f7895e0a2
ms.sourcegitcommit: aa9d2826e3c451f4699c0e69c9fcc8a2781c6213
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/17/2018
ms.locfileid: "45975637"
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>定義及使用計算內容 （SQL 和 R 深入探討）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這篇文章是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

本課程中介紹[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函式，可讓您定義適用於 SQL Server 的計算內容，然後在伺服器上，而不是本機電腦上執行複雜的計算。 

RevoScaleR 支援多個計算內容，讓您可以在 Hadoop、 Spark 或在資料庫中執行 R 程式碼。 針對 SQL Server，您定義的伺服器，並函式處理建立資料庫的本機電腦和遠端執行內容之間的連線，並傳遞物件的工作。

建立 SQL Server 的函式會計算內容會使用下列資訊：

- 連接字串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體
- 輸出應該如何處理的規格
- 啟用追蹤，或指定追蹤層級的選擇性引數
- 共用的資料目錄的選用規格

## <a name="create-and-set-a-compute-context"></a>建立和設定計算內容

1. 指定執行計算的執行個體的連接字串。  您可以重複使用您稍早建立的連接字串。 如果您想要將計算移到不同的伺服器，或使用不同的登入來執行一些工作，您可以建立不同的連接字串。

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
  
    *RxInSqlServer* 的 **wait** 引數支援下列選項：
  
    -   **TRUE**： 作業會設定為封鎖，並不會傳回直到完成或失敗為止。  如需詳細資訊，請參閱 <<c0> [ 分散式和 Machine Learning Server 的 parallel computing](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**： 作業會設定為非封鎖式，並立即傳回，讓您繼續執行其他的 R 程式碼。 不過，即使在非封鎖模式中，也必須在執行工作時保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與用戶端的連線。

3. 您可以選擇性地指定為本機的 R 工作階段以及遠端共用的本機目錄的位置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦和其帳戶。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 如果您想要以手動方式建立共用的特定目錄，您可以新增一行，如下所示：

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    若要判斷目前正在使用哪一個資料夾的共用，請執行`rxGetComputeContext()`，它會傳回有關目前詳細資料的計算內容。 如需詳細資訊，請參閱 [ScaleR 參考](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/)。

4. 準備好所有變數，提供它們做為引數**RxInSqlServer**建構函式，來建立*計算內容物件*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    語法**RxInSqlServer**看起來幾乎完全相同的**RxSqlServerData**您稍早用來定義資料來源的函式。 但是，有一些重要的差異。
      
    - 資料來源物件 (使用 [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函數所定義) 指定資料的儲存位置。
    
    - 相反地，計算內容中，使用定義的函式[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)表示進行彙總和其他計算的進行。
    
    定義計算內容不會影響您可能會在工作站上執行的任何其他泛型 R 計算，而且不會變更資料的來源。 例如，您可以將本機文字檔定義為資料來源，但將計算內容變更為 SQL Server，並且執行 SQL Server 電腦上資料的所有讀取和摘要。

## <a name="enable-tracing-on-the-compute-context"></a>啟用計算內容的追蹤

有時候作業可在您的本機內容上運作，但在遠端計算內容中執行時則發生問題。 如果您想要分析問題，或監視效能，您可以啟用追蹤，在計算內容中，以支援執行階段疑難排解。

1. 建立新的計算內容，會使用相同的連接字串，但加入引數*traceEnabled*並*traceLevel*來**RxInSqlServer**建構函式。

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

2. 若要變更計算內容，請使用 [rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext) 函數並依名稱指定內容。

    ```R
    rxSetComputeContext( sqlComputeTrace)
    ```

    > [!NOTE]
    > 
    > 本教學課程中，使用計算內容，並沒有啟用追蹤。 
    > 
    > 不過，如果您決定要使用追蹤，請注意，您的體驗可能會受到網路連線。 同時了解，因為已啟用追蹤之選項的效能尚未經過測試的所有作業。

您將了解如何使用下一個步驟中計算內容，以執行伺服器上的 R 程式碼，或在本機。

## <a name="next-step"></a>下一步

[建立及執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>上一個步驟

[查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
