---
title: 在 Server Core 安裝上設定 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- IsHadrEnabled server property
- Server Core Installation [SQL Server]
ms.assetid: ed6e5e94-4b8d-422a-a17e-61b05a4df903
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0c2a82aac84777c0601d234162135f9404184c39
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797914"
---
# <a name="configure-sql-server-on-a-server-core-installation"></a>在 Server Core 安裝上設定 SQL Server
  本主題涵蓋有關在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SP1 的 Server Core 安裝上設定 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的詳細資料。 
  
##  <a name="configure-and-manage-server-core-on-windows-server"></a>在 Windows Server 上設定及管理 Server Core  
 本節提供有助於設定及管理 Server Core 安裝的主題參考。  
  
 並非所有 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 功能都在 Server Core 模式中受到支援。  部分功能可以安裝在用戶端電腦或是未執行 Server Core 的另一部伺服器上，並且連接到 Server Core 上安裝的 Database Engine 服務。  
  
 如需有關在遠端設定及管理 Server Core 安裝的詳細資訊，請參閱以下主題：  
  
-   [Windows server 2008 R2： Server Core 部署的最佳作法](https://go.microsoft.com/fwlink/?LinkID=245957)（ https://go.microsoft.com/fwlink/?LinkID=245957)  
  
-   設定[Server Core 安裝：總覽](https://go.microsoft.com/fwlink/?LinkId=245958)（ https://go.microsoft.com/fwlink/?LinkId=245958)  
  
-   [使用 Sconfig 設定 Windows server 2008 R2 的 Server Core 安裝](https://go.microsoft.com/fwlink/?LinkId=245959)（ https://go.microsoft.com/fwlink/?LinkId=245959)  
  
-   [在執行 Windows server 2008 R2 之 Server Core 安裝的伺服器上安裝伺服器角色：總覽](https://go.microsoft.com/fwlink/?LinkId=245960)（ https://go.microsoft.com/fwlink/?LinkId=245960)  
  
-   [在執行 Windows server 2008 R2 之 Server Core 安裝的伺服器上安裝 Windows 功能：總覽](https://go.microsoft.com/fwlink/?LinkId=245961)（ https://go.microsoft.com/fwlink/?LinkId=245961)  
  
-   [管理 Server Core 安裝：總覽](https://go.microsoft.com/fwlink/?LinkId=245962)（ https://go.microsoft.com/fwlink/?LinkId=245962)  
  
-   [管理 Server Core 安裝](https://go.microsoft.com/fwlink/?LinkId=245963)（ https://go.microsoft.com/fwlink/?LinkId=245963)  
  
##  <a name="install-updates"></a>安裝 更新  
 本節提供有關在 Windows Server Core 機器上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 更新的資訊。 我們建議客戶及時評估並安裝最新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新，以便確保系統保持在最新狀態而且具有最新的安全性更新。 如需有關在 Windows Server Core 機器上安裝 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 的詳細資訊，請參閱[在 Server core 上安裝 SQL Server 2014](install-sql-server-on-server-core.md)。  
  
 以下是安裝產品更新的兩種狀況：  
  
-   [在新安裝期間安裝 SQL Server 2014 的更新](#installing-updates-during-a-new-installation) 
  
-   [安裝之後安裝 SQL Server 2014 的更新](#installing-updates-after-installation) 
  
### <a name="installing-updates-during-a-new-installation"></a>在新安裝期間安裝更新  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式只支援 Server Core 作業系統上的命令提示字元安裝。 如需詳細資訊，請參閱[從命令提示字元安裝 SQL Server 2014](install-sql-server-from-the-command-prompt.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程式會整合最新產品更新與主要產品安裝，因此主要產品及其適用的更新可同時安裝。  
  
 安裝程式找到最新版本的可用更新後，會使用目前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝程序進行下載與整合。 產品更新可以引入累計更新、Service Pack，或 Service Pack 加上累計更新。  
  
 指定 UpdateEnabled 和 UpdateSource 參數在主要產品安裝中包含最新的產品更新。 請參考以下範例，了解如何在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝期間啟用產品更新：  
  
```cmd 
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /UpdateEnabled=True /UpdateSource="<SourcePath>" /IACCEPTSQLSERVERLICENSETERMS  
```  
  
### <a name="installing-updates-after-installation"></a>安裝之後安裝更新 
 在已安裝的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 執行個體上，建議您套用最新的安全性更新和重大更新，包括一般發行版本 (GDR) 和 Service Pack (SP)。 您應該視需要並依案例採用個別的累計更新和安全性更新。 請評估更新，如有需要，則套用它。  
  
 在命令提示字元中套用更新，並以您的更新封裝名稱取代 <package_name>：  
  
-   更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的單一執行個體和所有共用元件。 您可以使用 InstanceName 參數或 InstanceID 參數指定執行個體。  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance  
    ```  
  
-   只更新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共用元件：  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch  
    ```  
  
-   更新電腦上的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和所有共用元件：  
  
    ```  
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances  
    ```  
  
##  <a name="startstop-sql-server-service"></a>啟動/停止 SQL Server 服務  
 [sqlservr 應用程式](../../tools/sqlservr-application.md)應用程式會在命令提示字元之下，啟動、停止、暫停和繼續執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體。  
  
 您也可以使用 Net 服務來啟動及停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。  
  
## <a name="enable-alwayson-availability-groups"></a>啟用 AlwaysOn 可用性群組  
 啟用 AlwaysOn 可用性群組是伺服器執行個體將可用性群組做為高可用性和災害復原方案的必要條件。 如需有關管理 AlwaysOn 可用性群組的詳細資訊，請參閱[啟用和停用 AlwaysOn 可用性群組 &#40;SQL Server&#41;](../availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md)。  
  
### <a name="using-sql-server-configuration-manager-remotely"></a>遠端使用 SQL Server 組態管理員  
 這些步驟是為了在執行用戶端版的 [!INCLUDE[win7](../../includes/win7-md.md)] 或更新版本的電腦上以及已安裝伺服器圖形化介面的另一部伺服器上執行 (也就是 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 的完整安裝，或是已啟用伺服器圖形化介面功能的 Windows Server 8 安裝)。  
  
1.  開啟 [電腦管理]。 若要開啟 [電腦管理]，請執行下列其中一項作業：  
  
    1.  在 [!INCLUDE[win7](../../includes/win7-md.md)]、Windows Server 2008 或 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 上：  
  
        1.  依序按一下 [開始]、[所有程式]、[系統管理工具]，然後按一下 [電腦管理]。  
  
        2.  依序按一下 [開始] 和 [執行]，並輸入 COMPMGMT.MSC，然後按一下 [確定]。  
  
    2.  在啟用伺服器圖形化介面的 Windows 8 上：  
  
        1.  將滑鼠移到畫面的左下角，然後在看到 [開始] 覆疊時，按一下滑鼠右鍵。  
  
        2.  從操作功能表選取 [電腦管理]。  
  
2.  在主控台樹狀目錄中，以滑鼠右鍵按一下 [電腦管理]，然後按一下 [連線到另一台電腦]。  
  
3.  在 [選取電腦] 對話方塊中，輸入要管理的 Server Core 電腦名稱，或按一下 [瀏覽] 尋找此電腦，然後按一下 [確定]。  
  
4.  在主控台樹狀目錄中，於 Server Core 電腦的 [電腦管理] 底下按一下 [服務與應用程式]。  
  
5.  按兩下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員]。  
  
6.  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager 中，按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務]，以滑鼠右鍵按一下 [[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （\<實例名稱 >）]，其中 \<實例名稱 > 是您要啟用 AlwaysOn 可用性群組的本機伺服器實例名稱，然後按一下 [屬性]。  
  
7.  選取 [AlwaysOn 高可用性] 索引標籤。  
  
8.  確認 [Windows 容錯移轉叢集名稱] 欄位包含本機容錯移轉叢集節點的名稱。 如果此欄位為空白，表示此伺服器執行個體目前不支援 AlwaysOn 可用性群組。 有可能本機電腦不是叢集節點、WSFC 叢集已經關閉，或者此 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 版本不支援 AlwaysOn 可用性群組。  
  
9. 選取 [啟用 AlwaysOn 可用性群組] 核取方塊，然後按一下 [確定]。  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 組態管理員會儲存您的變更。 然後您必須手動重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務。 這讓您可以選擇最適合您業務需求的重新啟動時間。 當 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務重新啟動時，AlwaysOn 就會啟用，而且 IsHadrEnabled 伺服器屬性會設定為 1。  
  
> [!NOTE]
>  -   您必須擁有適當的使用者權限，或者必須已被委派目標電腦的適當權限，才能連接該部電腦。  
> -   您要管理的電腦名稱會出現在主控台樹狀目錄中 [電腦管理] 旁邊的括號內。  
  
### <a name="using-powershell-cmdlets-to-enable-alwayson-availability-groups"></a>使用 PowerShell 指令程式來啟用 AlwaysOn 可用性群組

 PowerShell 指令程式 Enable-SqlAlwaysOn 是用來在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體上啟用 AlwaysOn 可用性群組。 如果在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服務執行時啟用 AlwaysOn 可用性群組，就必須重新啟動 Database Engine 服務，才能完成變更。 除非您指定 -Force 參數，否則此 Cmdlet 會詢問您是否想要重新啟動服務。如果取消，就不會進行任何作業。  
  
 您必須擁有系統管理員權限，才能執行這個 Cmdlet。  
  
 您可以使用下列其中一個語法來針對 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]執行個體啟用 AlwaysOn 可用性群組：  
  
```  
Enable-SqlAlwaysOn [-Path <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn -InputObject <Server> [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
```  
Enable-SqlAlwaysOn [-ServerInstance <string>] [-Credential <PSCredential>] [-Force] [-NoServiceRestart] [-Confirm] [-WhatIf] [<Commom Parameters>]  
```  
  
 下列 PowerShell 命令會在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的執行個體 (機器\執行個體) 上啟用 AlwaysOn 可用性群組：  
  
```powershell
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Machine\Instance  
```  
  
## <a name="configuring-remote-access-of-sql-server-running-on-server-core"></a>設定在 Server Core 上執行之 SQL Server 的遠端存取  
 您可以執行下面描述的動作，來設定在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Server Core SP1 上執行之 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 執行個體的遠端存取。  
  
### <a name="enable-remote-connections-on-an-instance-of-sql-server"></a>在 SQL Server 的實例上啟用遠端連線 
 若要啟用遠端連接，請在本機使用 SQLCMD.exe，然後針對 Server Core 執行個體執行下列陳述式：  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-sql-server-browser-service"></a>啟用及啟動 SQL Server Browser 服務  
 根據預設，Browser 服務是停用的。  如果在 Server Core 上執行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體已停用此服務，請從命令提示字元執行下列命令，以啟用服務：  
  
 `sc config SQLBROWSER start= auto`  
  
 啟用後，請從命令提示字元執行下列命令，以啟動服務：  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>在 Windows 防火牆中建立例外狀況  
 若要在 Windows 防火牆中建立 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 存取的例外狀況，請遵循[設定 Windows 防火牆以允許 SQL Server 存取](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)中指定的步驟。  
  
### <a name="enable-tcpip-on-an-instance-of-sql-server"></a>在 SQL Server 的實例上啟用 TCP/IP
 您可以針對 Server Core 上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體，透過 Windows PowerShell 啟用 TCP/IP 通訊協定。 請遵循下列步驟：  
  
1.  在執行 Windows Server 2008 R2 Server Core SP1 的電腦上，啟動 [工作管理員]。  
  
2.  在 [應用程式] 索引標籤上，按一下 [新工作]。  
  
3.  在 [建立新工作] 對話方塊的 [開啟] 欄位中輸入 **sqlps.exe**，然後按一下 [確定]。 隨即開啟 [**Microsoft[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**] 視窗。  
  
4.  在 [Microsoft  **Powershell][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** 視窗中，執行下列指令碼以啟用 TCP/IP 通訊協定：  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = new-object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
##  <a name="sql-server-profiler"></a>[SQL Server Profiler]  
 在遠端電腦上啟動 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，且從 [檔案] 功能表中選取 [新增追蹤] 時，應用程式會顯示一個 [連接到伺服器] 對話方塊，供您指定要連接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體 (位於 Server Core 電腦上)。 如需詳細資訊，請參閱 [啟動 SQL Server Profiler](../../tools/sql-server-profiler/start-sql-server-profiler.md)。  
  
 如需有關執行 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]所需權限的資訊，請參閱 [執行 SQL Server Profiler 所需的權限](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)。  
  
 如需有關 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 的其他詳細資料，請參閱 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)。  
  
##  <a name="sql-server-auditing"></a>SQL Server 稽核  
 您可以在遠端使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 定義稽核。 在建立及啟用稽核之後，目標將會收到項目。 如需有關建立和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 稽核，請參閱 [SQL Server Audit &#40;Database Engine&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
##  <a name="sql-servevr-command-prompt-utilities"></a>SQL Servevr 命令提示字元公用程式  
 您可以使用下列命令提示字元公用程式，好讓您在 Server Core 電腦上編寫 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 作業的指令碼。 下表列出 Server Core 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 隨附的命令提示字元公用程式清單：  
  
|**公用程式**|**描述**|**安裝位置**|  
|-----------------|---------------------|----------------------|  
|[bcp Utility](../../tools/bcp-utility.md)|在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 執行個體和使用者指定之格式的資料檔案之間，用來複製資料。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec 公用程式](../../integration-services/packages/dtexec-utility.md)|用以設定及執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Encrypt](../../integration-services/dtutil-utility.md)|用來管理 SSIS 封裝。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[osql 公用程式](../../tools/osql-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 應用程式](../../tools/sqlagent90-application.md)|用來從命令提示字元啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent。|\<磁碟機>:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<執行個體名稱>\MSSQL\Binn|  
|[sqlcmd 公用程式](../../tools/sqlcmd-utility.md)|可讓您在命令提示字元之下，輸入 [!INCLUDE[tsql](../../includes/tsql-md.md)] 陳述式、系統程序和指令碼檔案。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SQLdiag 公用程式](../../tools/sqldiag-utility.md)|用以收集可供 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶服務與支援部門使用的診斷資訊。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint 公用程式](../../tools/sqlmaint-utility.md)|用來執行舊版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]所建立的資料庫維護計畫。|\<磁片磁碟機 >： \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。MSSQLSERVER\MSSQL\Binn|  
|[sqlps 公用程式](../../tools/sqlps-utility.md)|用來執行 PowerShell 命令和指令碼。 載入並註冊 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供者和 cmdlet。|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr 應用程式](../../tools/sqlservr-application.md)|用來從命令提示字元啟動和停止 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 執行個體，以進行疑難排解。|\<磁片磁碟機 >： \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12。MSSQLSERVER\MSSQL\Binn|  
  
##  <a name="use-troubleshooting-tools"></a>使用疑難排解工具  
 您可以使用 [SQLdiag 公用程式](../../tools/sqldiag-utility.md)，從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和其他類型的伺服器收集記錄檔案和資料檔案，並使用其監視您的伺服器一段時間，或為伺服器的特定問題疑難排解。 SQLdiag 用於加速和簡化 Microsoft 客戶支援服務部門對診斷資訊的收集過程。  
  
 您可以在 Server Core 上的系統管理員命令提示字元中，使用 [SQLdiag 公用程式](../../tools/sqldiag-utility.md)主題中指定的語法啟動此公用程式。  
  
## <a name="see-also"></a>另請參閱  
 [在 Server Core 上安裝 SQL Server 2014](install-sql-server-on-server-core.md)   
 [安裝的使用說明主題](../../sql-server/install/installation-how-to-topics.md)  
