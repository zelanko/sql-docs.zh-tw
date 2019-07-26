---
title: 定義和使用 RevoScaleR 計算內容
description: 有關如何在 SQL Server 上使用 R 語言定義計算內容的教學課程逐步解說。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 053fc48c4117372eb3e3bebb715b4176ec1dd828
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469722"
---
# <a name="define-and-use-compute-contexts-sql-server-and-revoscaler-tutorial"></a>定義和使用計算內容 (SQL Server 和 RevoScaleR 教學課程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

這一課是[RevoScaleR 教學](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)課程的一部分, 說明如何搭配 SQL Server 使用[RevoScaleR 函數](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)。

在上一課中, 您使用了**RevoScaleR**函數來檢查資料物件。 本課程介紹[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)函式, 此函數可讓您定義遠端 SQL Server 的計算內容。 使用遠端計算內容, 您可以將 R 執行從本機會話轉移到伺服器上的遠端會話。 

> [!div class="checklist"]
> * 瞭解遠端 SQL Server 計算內容的元素
> * 啟用計算內容物件的追蹤

**RevoScaleR**支援多個計算內容:Hadoop、HDFS 上的 Spark, 以及資料庫中的 SQL Server。 若為 SQL Server, **RxInSqlServer**函數會用於伺服器連接, 並在本機電腦與遠端執行內容之間傳遞物件。

## <a name="create-and-set-a-compute-context"></a>建立和設定計算內容

建立 SQL Server 計算內容的**RxInSqlServer**函數會使用下列資訊:

+ 實例的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]連接字串
+ 應如何處理輸出的規格
+ 選擇性的共用資料目錄規格
+ 啟用追蹤或指定追蹤層級的選擇性引數

本節將逐步引導您完成每個部分。

1. 針對執行計算的實例指定連接字串。 您可以重複使用您稍早建立的連接字串。

    **使用 SQL 登入**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=<SQL Server instance name>; Database=<database name>;Uid=<SQL user nme>;Pwd=<password>"
      ```

    **使用 Windows 驗證**

    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=RevoDeepDive;Trusted_Connection=True"
    ```
    
2. 指定您要如何處理輸出。 下列腳本會指示本機 R 會話在處理下一個作業之前, 等候伺服器上的 R 工作結果。 它也會抑制遠端計算的輸出不會出現在本機會話中。
  
    ```R
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    ```
  
    *RxInSqlServer* 的 **wait** 引數支援下列選項：
  
    -   **TRUE**： 作業會設定為封鎖, 且在完成或失敗之前不會傳回。  如需詳細資訊, 請參閱[Machine Learning Server 中的分散式和平行計算](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing)。
  
    -   **FALSE**： 作業會設定為非封鎖並立即返回, 讓您繼續執行其他 R 程式碼。 不過，即使在非封鎖模式中，也必須在執行工作時保持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 與用戶端的連線。

3. (選擇性) 指定本機 R 會話以及遠端[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]電腦及其帳戶的共用使用本機目錄的位置。

    ```R
    sqlShareDir <- paste("c:\\AllShare\\", Sys.getenv("USERNAME"), sep="")
    ```
    
   如果您想要手動建立要共用的特定目錄, 您可以新增類似下列的程式程式碼:

    ```R
    dir.create(sqlShareDir, recursive = TRUE)
    ```

4. 將引數傳遞至**RxInSqlServer**的函式, 以建立*計算內容物件*。

    ```R
    sqlCompute <- RxInSqlServer(  
         connectionString = sqlConnString,
         wait = sqlWait,
         consoleOutput = sqlConsoleOutput)
    ```
    
    **RxInSqlServer**的語法看起來幾乎與您稍早用來定義資料來源的**RxSqlServerData**函數相同。 但是，有一些重要的差異。
      
    - 資料來源物件 (使用 [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函數所定義) 指定資料的儲存位置。
    
    - 相反地, 使用函式[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver)所定義的計算內容, 表示要進行匯總和其他計算的位置。
    
    定義計算內容不會影響您可能會在工作站上執行的任何其他泛型 R 計算，而且不會變更資料的來源。 例如，您可以將本機文字檔定義為資料來源，但將計算內容變更為 SQL Server，並且執行 SQL Server 電腦上資料的所有讀取和摘要。

5. 啟用遠端計算內容。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

6. 傳回計算內容的相關資訊, 包括其屬性。

    ```R
    rxGetComputeContext()
    ```

7. 指定 "local" 關鍵字 (下一課示範使用遠端計算內容), 將計算內容重設回本機電腦。

    ```R
    rxSetComputeContext("local")
    ```

> [!Tip]
> 如需此函數支援之其他關鍵字的清單，請從 R 命令列輸入 `help("rxSetComputeContext")` 。

## <a name="enable-tracing"></a>啟用追蹤

有時候作業可在您的本機內容上運作，但在遠端計算內容中執行時則發生問題。 如果您想要分析問題或監視效能, 您可以在計算內容中啟用追蹤, 以支援執行時間疑難排解。

1. 建立使用相同連接字串的新計算內容, 但將*traceEnabled*和*traceLevel*引數新增至**RxInSqlServer**的函式。

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

2. 使用[rxSetComputeCoNtext](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsetcomputecontext)函數, 依名稱指定啟用追蹤的計算內容。

    ```R
    rxSetComputeContext(sqlComputeTrace)
    ```

## <a name="next-steps"></a>後續步驟

瞭解如何切換計算內容, 以在伺服器或本機上執行 R 程式碼。

> [!div class="nextstepaction"]
> [計算本機和遠端計算內容中的摘要統計資料](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)