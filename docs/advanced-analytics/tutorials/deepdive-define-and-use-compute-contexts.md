---
title: "定義和使用的計算內容 （SQL 與 R 深入探討） |Microsoft 文件"
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
ms.assetid: b13058d0-9c6a-44e1-849b-72189d9050ba
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: a5cf351eeccbfb6ed019bf330e1d236e8576c982
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/11/2018
---
# <a name="define-and-use-compute-contexts-sql-and-r-deep-dive"></a>定義和使用 （SQL 與 R 深入探討） 的計算內容
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是資料科學深入探討教學課程中，有關如何使用一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

本課程中介紹[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函式，可讓您為 SQL Server 中定義的計算內容，然後在伺服器上，而不是本機電腦上執行複雜的計算。 

RevoScaleR 支援多個計算內容，以便在 Hadoop、 Spark 或在資料庫中執行 R 程式碼。 針對 SQL Server，定義在伺服器上，並函式處理建立資料庫連接，並傳遞物件之間在本機電腦和遠端執行內容的工作。

函式會建立 SQL Server 計算內容會使用下列資訊：

- 連接字串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體
- 指定的輸出應該如何處理
- 啟用追蹤，或指定追蹤層級的選擇性引數
- 共用的資料目錄的選用規格

## <a name="create-and-set-a-compute-context"></a>建立並設定計算內容

1. 指定會在執行計算的執行個體的連接字串。  您可以重新使用您稍早建立的連接字串。 如果您想要將這些運算移至不同的伺服器，或使用不同的登入來執行一些工作，您可以建立不同的連接字串。

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
  
    -   **TRUE**： 工作設定為封鎖，直到它已完成或失敗不會傳回。  如需詳細資訊，請參閱[分散式和機器學習 Server 中的平行運算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**： 作業會設定為非封鎖，並立即傳回，讓您繼續執行其他 R 程式碼。 不過，即使在非封鎖模式中，也必須在執行工作時保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與用戶端的連線。

3. 您可以選擇性地指定的本機目錄，以由本機的 R 工作階段和遠端共用位置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦和其帳戶。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
4. 如果您想要以手動方式建立共用的特定目錄，您可以加入類似下列一行：

    ```
    dir.create(sqlShareDir, recursive = TRUE)
    ```

    若要判斷目前正在使用哪一個資料夾的共用，請執行`rxGetComputeContext()`，它會傳回有關目前詳細資料的計算內容。 如需詳細資訊，請參閱 [ScaleR 參考](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/)。

4. 已準備好所有變數，做為引數提供**RxInSqlServer**建構函式，建立*計算內容物件*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    語法**RxInSqlServer**看起來幾乎完全相同的**RxSqlServerData**您先前用來定義資料來源的函式。 但是，有一些重要的差異。
      
    - 資料來源物件 (使用 [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函數所定義) 指定資料的儲存位置。
    
    - 計算內容中，使用函數的定義相較之下， [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)指出彙總和其他計算的位置進行。
    
    定義計算內容不會影響您可能會在工作站上執行的任何其他泛型 R 計算，而且不會變更資料的來源。 例如，您可以將本機文字檔定義為資料來源，但將計算內容變更為 SQL Server，並且執行 SQL Server 電腦上資料的所有讀取和摘要。

## <a name="enable-tracing-on-the-compute-context"></a>啟用追蹤計算內容

有時候作業可在您的本機內容上運作，但在遠端計算內容中執行時則發生問題。 如果您想要分析問題或監視效能，則可以在計算內容中啟用追蹤，以支援執行階段疑難排解。

1. 建立新的計算內容使用相同的連接字串，但加入引數*traceEnabled*和*traceLevel*至**RxInSqlServer**建構函式。

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
    > 此教學課程中，使用計算內容，但是沒有啟用追蹤。 
    > 
    > 不過，如果您決定要使用追蹤，請注意您的體驗可能會受到網路連線。 還必須注意，因為尚未經過啟用追蹤選項的效能測試的所有作業。

了解如何使用下一個步驟中計算內容，若要執行 R 程式碼，在伺服器上的或在本機。

## <a name="next-step"></a>下一步

[建立及執行 R 指令碼](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)

## <a name="previous-step"></a>上一個步驟

[查詢及修改 SQL Server 資料](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)
