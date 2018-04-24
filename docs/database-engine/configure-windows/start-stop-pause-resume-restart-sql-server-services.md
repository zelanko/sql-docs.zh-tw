---
title: 啟動、停止、暫停、繼續、重新啟動 SQL Server 服務 | Microsoft Docs
ms.custom: ''
ms.date: 02/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Configuration Manager, start and stop services
- stopping SQL Server Agent
- parameters [SQL Server], startup options
- SQL Server, startup options
- Database Engine [SQL Server], starting and stopping services
- pausing SQL Server
- PowerShell [SQL Server], starting and stopping services
- single-user mode [SQL Server], starting in
- SQL Server Management Studio [SQL Server], starting or stopping services
- stopping SQL Server Browser service
- starting SQL Server Agent
- default instances [SQL Server], starting and stopping
- SQL Server Agent, starting and stopping
- command prompt [SQL Server], starting and stopping SQL Server services
- continuing SQL Server
- starting SQL Server Database Engine
- net stop commands [SQL Server]
- command prompt [SQL Server], SQL Browser service
- Configuration Manager, start and stop services
- resuming SQL Server
- startup options [SQL Server]
- named instances [SQL Server], starting and stopping
- net start commands [SQL Server]
- SQL Server, starting and stopping
- stopping SQL Server
- starting SQL Server Browser service
- SQL Server Database Engine setting startup options
- administering SQL Server, starting and stopping services
- Management Studio [SQL Server], starting or stopping services
ms.assetid: 32660a02-e5a1-411a-9e57-7066ca459df6
caps.latest.revision: 20
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Active
ms.openlocfilehash: f2bbc2491cce3638712be0ceb152a6ccc5a63684
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="start-stop-pause-resume-restart-sql-server-services"></a>啟動、停止、暫停、繼續、重新啟動 SQL Server 服務
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > 如需舊版 SQL Server 的相關內容，請參閱[啟動、停止、暫停、繼續、重新啟動資料庫引擎、SQL Server Agent 或 SQL Server Browser 服務](https://msdn.microsoft.com/en-US/library/hh403394(SQL.120).aspx)。

  本主題說明如何啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務，方法是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員、  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、命令提示字元中的 **net** 命令、 [!INCLUDE[tsql](../../includes/tsql-md.md)]或 PowerShell。  
  
-   **開始之前：**  
  
    -   [這些是什麼服務？](#Services)  
  
    -   [其他資訊](#MoreInformation)  
  
    -   [Security](#Security)  
  
-   **使用指示：**  
  
    -   [SQL Server 組態管理員](#SSCMProcedure)  
  
    -   [Transact-SQL](#SSMSProcedure)  
  
    -   [命令提示字元視窗中的 net 命令](#CommandPrompt)  
  
    -   [Transact-SQL](#TsqlProcedure)  
  
    -   [PowerShell](#PowerShellProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Services"></a> 什麼是 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務？  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 元件是當做 Windows 服務執行的可執行程式。 當做 Windows 服務執行的程式可以繼續操作，而不會在電腦螢幕上顯示任何活動。  
  
 **[!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務**  
 當做 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的可執行處理序。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 可以是預設執行個體 (每部電腦只限一個執行個體)，或者可以是許多具名 [!INCLUDE[ssDE](../../includes/ssde-md.md)]執行個體的其中一個。 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員來判斷哪些 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體會安裝在電腦上。 預設執行個體 (如果安裝的話) 會列為 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER)**。 具名執行個體 (如果安裝的話) 會列為 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (<執行個體名稱>)**。 依預設， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express 會安裝為 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLEXPRESS)**。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務**  
 一種 Windows 服務，它會執行排程的管理工作 (稱為作業和警示)。 如需詳細資訊，請參閱 [SQL Server Agent](http://msdn.microsoft.com/library/8d1dc600-aabb-416f-b3af-fbc9fccfd0ec)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本都可使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如需 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]版本支援的功能清單，請參閱 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務**  
 一種 Windows 服務，它會接聽 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 資源的內送要求，並為用戶端提供有關電腦上所安裝之 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體的資訊。 單一 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務執行個體會用於電腦上所安裝的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
###  <a name="MoreInformation"></a> 其他資訊  
  
-   暫停 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務會阻止新的使用者連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，但是已連接的使用者可以繼續工作，直到連接中斷為止。 當您希望在停止服務之前等待使用者完成工作時，請使用暫停。 這樣可讓他們完成正在進行的交易。 「繼續」可讓 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 再次接受新的連接。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 服務無法暫停或繼續。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員和 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 會使用以下圖示來顯示目前的服務狀態。  
  
     **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員**  
  
    -   服務名稱旁圖示上的綠色箭頭，表示服務已啟動。  
  
    -   服務名稱旁圖示上的紅色方塊，表示服務已停止。  
  
    -   服務名稱旁圖示上的兩條垂直藍線，表示服務已暫停。  
  
    -   重新啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]時，紅色方塊表示服務已停止，綠色箭頭則表示服務已順利啟動。  
  
     **[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
    -   服務名稱旁綠色圓形圖示上的白色箭頭，表示服務已啟動。  
  
    -   服務名稱旁紅色圓形圖示上的白色方塊，表示服務已停止。  
  
    -   服務名稱旁藍色圓形圖示上的兩條垂直白線，表示服務已暫停。  
  
-   當使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員或 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]時，只能使用可能的選項。 例如，如果此服務已啟動，則無法使用 **[啟動]** 。  
  
-   在叢集上執行時，使用叢集管理員來管理 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 服務的效果最佳。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> 權限  
 根據預設，只有本機 Administrators 群組的成員能夠啟動、停止、暫停、繼續或重新啟動服務。 若要將管理服務的能力授與非系統管理員，請參閱 [How to grant users rights to manage services in Windows Server 2003](http://support.microsoft.com/kb/325349)(如何在 Windows Server 2003 中，將管理服務的權限授與使用者)。 (其他 Windows 版本的程序都很相似)。  
  
 使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] SHUTDOWN [!INCLUDE[tsql](../../includes/tsql-md.md)]**命令停止** 需要 **sysadmin** 或 **serveradmin** 固定伺服器角色的成員資格，而且無法移轉。  
  
##  <a name="SSCMProcedure"></a> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員  
  
#### <a name="starting-includessnoversionincludesssnoversion-mdmd-configuration-manager"></a>啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員  
  
1.  指向 **[開始]** 功能表上的 **[所有程式]**，然後依序指向 [ [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]] 和 **[組態工具]**，再按一下 **[SQL Server 組態管理員]**。  
  
     由於 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console 程式的嵌入式管理單元，而不是獨立的程式，因此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員在較新版本的 Windows 中不會作為應用程式出現。 以下是將 Windows 安裝在 C 磁碟機時的最近四個版本路徑。  
  
    |||  
    |-|-|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|C:\Windows\SysWOW64\SQLServerManager10.msc|  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>若要啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  使用上述指示啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態工具。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]**。  
  
3.  在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員] 中，按一下左窗格中的 **[SQL Server 服務]**。  
  
4.  在結果窗格中，以滑鼠右鍵按一下 [SQL Server (MSSQLServer)] 或具名執行個體，然後按一下 [啟動]、[停止]、[暫停]、[繼續] 或 [重新啟動]。  
  
5.  按一下 **[確定]** ，即可關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
> [!NOTE]  
>  若要使用啟動選項啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的執行個體，請參閱[設定伺服器啟動選項 &#40;SQL Server 組態管理員&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)。  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-includessnoversionincludesssnoversion-mdmd-browser-or-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>若要啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 或是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的執行個體  
  
1.  使用上述指示啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態工具。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]**。  
  
3.  在 [ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員] 中，按一下左窗格中的 **[SQL Server 服務]**。  
  
4.  在結果窗格中，以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 瀏覽器] 或具名執行個體的 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (MSSQLServer)] 或 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (<執行個體名稱>)]，然後按一下 [啟動]、[停止]、[暫停]、[繼續] 或 [重新啟動]。  
  
5.  按一下 **[確定]** ，即可關閉 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員。  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 無法暫停。  
  
##  <a name="SSMSProcedure"></a> 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio  
  
#### <a name="to-start-stop-pause-resume-or-restart-the-an-instance-of-the-includessdenoversionincludesssdenoversion-mdmd"></a>若要啟動、停止、暫停、繼續或重新啟動 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]  
  
1.  在物件總管中，連接至 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，並以滑鼠右鍵按一下您要啟動的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，然後按一下 [啟動]、[停止]、[暫停]、[繼續] 或 [重新啟動]。  
  
     或者在 [已註冊的伺服器] 中，以滑鼠右鍵按一下您要啟動的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體、並指向 [服務控制]，然後按一下 [啟動]、[停止]、[暫停]、[繼續] 或 [重新啟動]。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]**。  
  
3.  當系統提示您是否要執行動作時，請按一下 **[是]**。  
  
#### <a name="to-start-stop-or-restart-the-an-instance-of-the-includessnoversionincludesssnoversion-mdmd-agent"></a>若要啟動、停止或重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 的執行個體  
  
1.  在物件總管中，連接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的執行個體，並以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent]，然後按一下 [啟動]、[停止] 或 [重新啟動]。  
  
2.  如果出現 **[使用者帳戶控制]** 對話方塊，請按一下 **[是]**。  
  
3.  當系統提示您是否要執行動作時，請按一下 **[是]**。  
  
##  <a name="CommandPrompt"></a> 從命令提示字元視窗使用 net 命令  
 可以使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] net [!INCLUDE[msCoName](../../includes/msconame-md.md)] 命令來啟動、停止或暫停 **net** 服務。  
  
###  <a name="dbDefault"></a> 若要啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令：  
  
     **net start "SQL Server (MSSQLSERVER)"**  
  
     -或-  
  
     **net start MSSQLSERVER**  
  
###  <a name="dbNamed"></a> 若要啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令。 以您要管理之執行個體的名稱取代 \<執行個體名稱>。  
  
     **net start "SQL Server (** *instancename* **)"**  
  
     -或-  
  
     **net start MSSQL$** *instancename*  
  
###  <a name="dbStartup"></a> 若要使用啟動選項來啟動 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   將啟動選項加入 **net start "SQL Server (MSSQLSERVER)"** 陳述式結尾，並間隔一個空格。 使用 **net start**啟動時，啟動選項會使用斜線 (/)，而非連字號 (-)。  
  
     **net start "SQL Server (MSSQLSERVER)" /f /m**  
  
     -或-  
  
     **net start MSSQLSERVER /f /m**  
  
    > [!NOTE]  
    >  如需啟動選項的詳細資訊，請參閱 [Database Engine 服務啟動選項](../../database-engine/configure-windows/database-engine-service-startup-options.md)。  
  
###  <a name="agDefault"></a> 若要使用啟動選項來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的預設執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令：  
  
     **net start "SQL Server Agent (MSSQLSERVER)"**  
  
     -或-  
  
     **net start SQLSERVERAGENT**  
  
###  <a name="agNamed"></a> 若要使用啟動選項來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的具名執行個體上啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   從命令提示字元，輸入下列其中一個命令。 以您要管理之執行個體的名稱取代 *執行個體名稱* 。  
  
     **net start "SQL Server Agent(** *instancename* **)"**  
  
     -或-  
  
     **net start SQLAgent$** *instancename*  
  
 如需如何以詳細資訊模式執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 來進行疑難排解的相關資訊，請參閱 [sqlagent90 應用程式](../../tools/sqlagent90-application.md)。  
  
###  <a name="Browser"></a> 若要啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
  
-   從命令提示字元，輸入下列其中一個命令：  
  
     **net start "SQL Server Browser"**  
  
     -或-  
  
     **net start SQLBrowser**  
  
###  <a name="pauseStop"></a> 若要從命令提示字元視窗暫停或停止服務  
  
-   若要暫停或停止服務，請使用以下方式來修改命令。  
  
    -   若要暫停服務，請以 **net pause** 取代 **net start**。  
  
    -   若要停止服務，請以 **net stop** 取代 **net start**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] SHUTDOWN **陳述式來停止** 。  
  
#### <a name="to-stop-the-includessdeincludesssde-mdmd-using-includetsqlincludestsql-mdmd"></a>若要使用 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 停止 [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
-   若要等待目前執行的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式和預存程序完成，然後停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，請執行下列陳述式。  
  
    ```sql  
    SHUTDOWN;   
    ```  
  
-   若要立即停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)]，請執行下列陳述式。  
  
    ```sql  
    SHUTDOWN WITH NOWAIT;   
    ```  
  
 如需 **SHUTDOWN** 陳述式的詳細資訊，請參閱 [SHUTDOWN &#40;Transact-SQL&#41;](../../t-sql/language-elements/shutdown-transact-sql.md)。  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
  
#### <a name="to-start-and-stop-includessdeincludesssde-mdmd-services"></a>若要啟動及停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 服務  
  
1.  在 [命令提示字元] 視窗中，執行下列命令來啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell。  
  
    ```ms-dos  
    sqlps  
    ```  
  
2.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 命令提示字元中，執行下列命令。 以電腦的名稱取代 `computername` 。  
  
    ```powershell  
    # Get a reference to the ManagedComputer class.  
    CD SQLSERVER:\SQL\computername  
    $Wmi = (get-item .).ManagedComputer  
  
    ```  
  
3.  識別您想要停止或啟動的服務。 挑選下列其中一行。 使用具名執行個體的名稱取代 `instancename` 。  
  
    -   取得 [!INCLUDE[ssDE](../../includes/ssde-md.md)]預設執行個體的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQLSERVER']  
        ```  
  
    -   取得 [!INCLUDE[ssDE](../../includes/ssde-md.md)]具名執行個體的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['MSSQL$instancename']  
        ```  
  
    -   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 預設執行個體上 [!INCLUDE[ssDE](../../includes/ssde-md.md)]Agent 服務的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLSERVERAGENT']  
        ```  
  
    -   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 具名執行個體上 [!INCLUDE[ssDE](../../includes/ssde-md.md)]Agent 服務的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLAGENT$instancename']  
        ```  
  
    -   取得 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服務的參考。  
  
        ```powershell  
        $DfltInstance = $Wmi.Services['SQLBROWSER']  
        ```  
  
4.  完成範例，以啟動然後停止選取的服務。  
  
    ```powershell  
    # Display the state of the service.  
    $DfltInstance  
    # Start the service.  
    $DfltInstance.Start();  
    # Wait until the service has time to start.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    # Stop the service.  
    $DfltInstance.Stop();  
    # Wait until the service has time to stop.  
    # Refresh the cache.  
    $DfltInstance.Refresh();   
    # Display the state of the service.  
    $DfltInstance  
    ```  
  
## <a name="see-also"></a>另請參閱  
 [SQL Server 安裝程式文件集的概觀](http://msdn.microsoft.com/library/2620439a-f9d3-4b3c-9968-48f60b4bb9a5)   
 [檢視與讀取 SQL Server 安裝程式記錄檔](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [SQL Server 組態管理員](../../relational-databases/sql-server-configuration-manager.md)   
 [以最低組態啟動 SQL Server](../../database-engine/configure-windows/start-sql-server-with-minimal-configuration.md)   
 [SQL Server 2016 版本支援的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)  
  
  

