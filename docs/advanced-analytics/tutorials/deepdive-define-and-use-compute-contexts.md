---
title: 定義及使用 RevoScaleR 計算內容-SQL Server Machine Learning
description: 有關如何定義計算內容，在 SQL Server 上使用 R 語言的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3131dfc65d8964232073d37aba697f62de9fcc2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962233"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>定義及使用計算內容 （SQL Server 和 RevoScaleR 教學課程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

這一課是屬於[RevoScaleR 教學課程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)與 SQL Server。

在上一課，您已使用**RevoScaleR**函式來檢查資料的物件。 本課程中介紹[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函式，可讓您為遠端的 SQL Server 中定義的計算內容。 使用遠端計算內容，您可以在伺服器上轉移從本機工作階段的 R 執行遠端工作階段。 

> [!div class="checklist"]
> * 了解的項目，遠端 SQL server 計算內容
> * 啟用計算內容物件的追蹤

**RevoScaleR**支援多個計算內容：Hadoop、 Spark 在 HDFS 與 SQL Server 資料庫。 SQL server **RxInSqlServer**函式用於伺服器連接和本機電腦和遠端執行內容之間傳遞物件。

## <a name="create-and-set-a-compute-context"></a>建立和設定計算內容

**RxInSqlServer**建立 SQL Server 計算內容的函式會使用下列資訊：

+ 連接字串[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體
+ 輸出應該如何處理的規格
+ 共用的資料目錄的選用規格
+ 啟用追蹤，或指定追蹤層級的選擇性引數

本節會引導您完成每個組件。

1. 指定執行計算的執行個體的連接字串。 您可以重複使用您稍早建立的連接字串。

    **使用 SQL 登入**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **使用 Windows 驗證**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 指定您要如何處理輸出。 下列指令碼會指示等候 R 工作結果在伺服器上處理下一個作業之前，先在本機 R 工作階段。 它也會隱藏輸出，從遠端計算不會出現在本機工作階段。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 的 **wait** 引數支援下列選項：
  
    -   **TRUE**： 作業會設定為封鎖，並不會傳回直到完成或失敗為止。  如需詳細資訊，請參閱 <<c0> [ 分散式和 Machine Learning Server 的 parallel computing](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**： 作業會設定為非封鎖式，並立即傳回，讓您繼續執行其他的 R 程式碼。 不過，即使在非封鎖模式中，也必須在執行工作時保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與用戶端的連線。

3. （選擇性） 指定的本機目錄為本機的 R 工作階段以及遠端共用位置[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦和其帳戶。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   如果您想要以手動方式建立共用的特定目錄，您可以新增一行，如下所示：

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 引數傳遞給**RxInSqlServer**建構函式建立*計算內容物件*。

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

5. 啟用遠端計算內容。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. 傳回計算內容，包括其屬性的詳細資訊。

    ```R
    rxGetComputeContext()
    ```

7. 計算內容來重新設定本機電腦指定"local"關鍵字 （下一課示範如何使用遠端計算內容）。

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> 如需此函數支援之其他關鍵字的清單，請從 R 命令列輸入 `help("rxSetComputeContext")` 。

## <a name="enable-tracing"></a>啟用追蹤

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

2. 使用[rxSetComputeContext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)依名稱指定啟用追蹤的計算內容的函式。

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>後續步驟

了解如何切換計算內容執行伺服器上的 R 程式碼，或在本機。

> [!div class="nextstepaction"]
> [計算摘要統計資料，在本機和遠端計算內容](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)