---
title: "SQL Server 2012 版本資訊 | Microsoft Docs"
ms.prod: sql-server-2012
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Release Notes, SQL Server
ms.assetid: 9ccb390a-67a9-4593-85ea-2b4c41c4620f
caps.latest.revision: 21
author: byham
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 08b3cca7b4f22423177eaa0dbaed48715dbeaed2
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-2012-release-notes"></a>SQL Server 2012 版本資訊
這份版本資訊文件將描述有關您安裝或疑難排解 Microsoft SQL Server 2012 ([請按一下這裡下載](http://go.microsoft.com/fwlink/?LinkId=238647)) 之前應該閱讀的已知問題。 這份版本資訊文件僅於線上提供，安裝媒體中並不提供，而且會定期更新。  
  
如需有關如何開始使用和安裝 SQL Server 2012 的詳細資訊，請參閱 SQL Server 2012 讀我檔案。 您可以從安裝媒體與 [讀我檔案](http://download.microsoft.com/download/3/B/D/3BD9DD65-D3E3-43C3-BB50-0ED850A82AD5/ENU/Readme.htm) 下載頁面，取得讀我檔案文件。 您也可以在 [SQL Server 線上叢書](http://go.microsoft.com/fwlink/?LinkId=190948) 和 [SQL Server 論壇](http://go.microsoft.com/fwlink/?LinkId=213599)中尋找更多資訊。  
  
## <a name="Install"></a>1.0 安裝之前  
在安裝 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]之前，請考量以下資訊。  
  
### <a name="11-rules-documentation-for-sql-server-2012-setup"></a>1.1 SQL Server 2012 安裝程式的規則文件集  
**問題** ：SQL Server 安裝程式的作業完成之前會驗證您的電腦組態。 SQL Server 安裝程式作業期間執行的各種規則會使用系統組態檢查 (SCC) 報告加以擷取。 MSDN Library 上不再提供有關這些安裝程式規則的文件集。  
  
**因應措施** ：您可以參考系統組態檢查報告，深入了解這些安裝程式規則。 系統組態檢查會產生報告，其中包含每個已執行之規則以及執行狀態的簡短描述。 系統組態檢查報告位於 %programfiles%\Microsoft SQL Server\110\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\。  
  
### <a name="12-adding-a-local-user-account-for-the-distributed-replay-controller-service-might-terminate-setup-unexpectedly"></a>1.2 加入 Distributed Replay Controller 服務的本機使用者帳戶可能會非預期地終止安裝程式  
**問題** ：在 SQL Server 安裝程式的 [Distributed Replay Controller]  頁面中，當您嘗試加入 Distributed Replay Controller 服務的本機使用者帳戶時，安裝程式將會非預期地終止並顯示「SQL Server 安裝程式失敗」錯誤訊息。  
  
**因應措施** ：在安裝 SQL 期間，請勿經由 [加入目前使用者] 或 [加入] 加入本機使用者帳戶。 請在安裝之後，依照下列步驟手動加入本機使用者帳戶：  
  
1.  停止 SQL Server Distributed Replay Controller 服務。  
  
2.  在安裝控制器服務的控制器電腦上，於命令提示字元中輸入 dcomcnfg。  
  
3.  在 [元件服務] 視窗中，導覽至 [主控台根目錄] -> [元件服務] -> [電腦] -> [我的電腦] -> [Dconfig] ->[DReplayController]。  
  
4.  以滑鼠右鍵按一下 [DReplayController]，然後按一下 [內容]。  
  
5.  在 [DReplayController 內容]  視窗的 [安全性]  索引標籤上，按一下 [啟動和啟用權限]  區段中的 [編輯]  。  
  
6.  將 [本機和遠端啟用]  權限授與本機使用者帳戶，然後按一下 [確定] 。  
  
7.  按一下 [存取權限] 區段中的 [編輯]  將 [本機和遠端存取]  權限授與本機使用者帳戶，然後按一下 [確定] 。  
  
8.  按一下 [確定]  關閉 [DReplayController 內容]  視窗。  
  
9. 在控制器電腦上，將本機使用者帳戶加入至 [Distributed COM Users]  群組。  
  
10. 啟動 SQL Server Distributed Replay Controller 服務。  
  
### <a name="13-sql-server-setup-might-fail-while-trying-to-start-the-sql-server-browser-service"></a>1.3 SQL Server 安裝程式可能會在嘗試啟動 SQL Server Browser 服務時失敗  
**問題** ：SQL Server 安裝程式可能會在嘗試啟動 SQL Server Browser 服務時失敗，並出現類似下面的錯誤：  
  
<pre>The following error has occurred:  
Service 'SQLBrowser' start request failed. Click 'Retry' to retry the failed action, or click 'Cancel' to cancel this action and continue setup.</pre>  
  
或  
  
<pre>The following error has occurred:  
SQL Server Browser configuration for feature 'SQL_Browser_Redist_SqlBrowser_Cpu32' was cancelled by user after a previous installation failure. The last attempted step: Starting the SQL Server Browser service 'SQLBrowser', and waiting for up to '900' seconds for the process to complete.</pre>  
  
**因應措施** ：當 SQL Server 引擎或 Analysis Services 無法安裝時，就可能會發生這種情況。 若要修正此問題，請參閱 SQL Server 安裝程式記錄檔，然後疑難排解 SQL Server 引擎和 Analysis Services 失敗。 如需詳細資訊，請參閱＜檢視與讀取 SQL Server 安裝程式記錄檔＞。 如需詳細資訊，請參閱＜ [View and Read SQL Server Setup Log Files](http://msdn.microsoft.com/library/ms143702(SQL.110).aspx)＞。  
  
### <a name="14-sql-server-2008-2008-r2-analysis-services-failover-cluster-upgrade-to-sql-server-2012-might-fail-after-renaming-the-network-name"></a>1.4 在重新命名網路名稱之後，SQL Server 2008、2008 R2 Analysis Services 容錯移轉叢集升級到 SQL Server 2012 可能會失敗  
**問題** ：在您使用 Windows 叢集系統管理員工具來變更 Microsoft SQL Server 2008 或 2008 R2 Analysis Services 容錯移轉叢集執行個體的網路名稱之後，升級作業可能會失敗。  
  
**因應措施** ：若要解決這個問題，請根據 [這份知識庫文章](http://support.microsoft.com/kb/955784)中解決方法章節的指示來更新 ClusterName 登錄項目。  
  
### <a name="15-installing-sql-server-2012-on-windows-server-2008-r2-server-core-service-pack-1"></a>1.5 在 Windows Server 2008 R2 Server Core Service Pack 1 上安裝 SQL Server 2012  
您可以在 Windows Server 2008 R2 Server Core SP1 上安裝 SQL Server，但有以下限制：  
  
-   Microsoft SQL Server 2012 不支援在 Server Core 作業系統上使用安裝精靈進行安裝。 在 Server Core 上安裝時，SQL Server 安裝程式支援使用 /Q 參數的完整無訊息模式或使用 /QS 參數的簡單無訊息模式。  
  
-   在執行 Windows Server 2008 R2 Server Core SP1 的電腦上，不支援將舊版 SQL Server 升級為 Microsoft SQL Server 2012。  
  
-   不支援在執行 Windows Server 2008 R2 Server Core SP1 的電腦上安裝 32 位元版 Microsoft SQL Server 2012。  
  
-   在執行 Windows Server 2008 R2 Server Core SP1 的電腦上，Microsoft SQL Server 2012 無法與舊版 SQL Server 並存安裝。  
  
-   並非所有 SQL Server 2012 功能都可在 Server Core 作業系統上受到支援。 如需有關支援的功能以及在 Server Core 上安裝 SQL Server 2012 的詳細資訊，請參閱 [在 Server Core 上安裝 SQL Server 2012](http://msdn.microsoft.com/library/hh231669(SQL.110).aspx)。  
  
### <a name="16-semantic-search-requires-you-to-install-an-additional-dependency"></a>1.6 語意搜尋需要您安裝其他相依關係  
**問題** ：統計語意搜尋有其他必要條件，即語意語言統計資料庫，不是由 SQL Server 安裝程式進行安裝。  
  
**因應措施** ：若要將語意語言統計資料庫設定為語意索引的必要元件，請執行下列工作：  
  
1.  在 SQL Server 安裝媒體上，找到並執行名稱為 SemanticLanguageDatabase.msi 的 Windows Installer 套件，以擷取資料庫。 若為 SQL Server 2012 Express，請從 [Microsoft 下載中心](https://www.microsoft.com/download/details.aspx?id=35582) (http://go.microsoft.com/fwlink/?LinkId=221787) 下載語意語言統計資料庫，然後執行 Windows Installer 套件。  
  
2.  將資料庫移至適當的資料夾。 若將資料庫保留在預設位置，則必須要變更權限，才能順利地進行附加。  
  
3.  附加已擷取的資料庫。  
  
4.  呼叫 **sp_fulltext_semantic_register_language_statistics_db** 預存程序註冊資料庫，並在附加資料庫時提供您為資料庫命名的名稱。  
  
若未完成這些工作，則在您嘗試建立語意索引時，將會看到以下的錯誤訊息。  
  
<pre>Msg 41209, Level 16, State 3, Line 1  
A semantic language statistics database is not registered. Full-text indexes using 'STATISTICAL_SEMANTICS' cannot be created or populated.</pre>  
  
### <a name="17-installation-prerequisite-handling-during-sql-server-2012-setup"></a>1.7 在安裝 SQL Server 2012 期間處理安裝必要條件  
下列項目描述在安裝 SQL Server 2012 期間必要的安裝行為：  
  
-   只支援在 Windows 7 SP1 或 Windows Server 2008 R2 SP1 上安裝 SQL Server 2012， 但在 Windows 7 或 Windows Server 2008 R2 上，安裝程式不會封鎖安裝 SQL Server 2012。  
  
-   當您選取 Database Engine、Replication、Master Data Services、Reporting Services、Data Quality Services (DQS) 或 SQL Server Management Studio 時，.NET Framework 3.5 SP1 是 SQL Server 2012 的必要條件，但是 SQL Server 安裝程式已不再安裝 Framework。  
  
    -   如果您在 Windows Vista SP2 或 Windows Server 2008 SP2 作業系統電腦上執行安裝程式，且未安裝 .NET Framework 3.5 SP1，SQL Server 安裝程式會要求您下載及安裝 .NET Framework 3.5 SP1，再繼續進行 SQL Server 安裝。 您可以從 Windows Update 下載 .NET Framework 3.5 SP1，也可以直接從 [這裡](https://www.microsoft.com/download/details.aspx?id=25150)下載。 若要避免安裝 SQL Server 期間中斷，您可以先下載及安裝 .NET Framework 3.5 SP1，再執行 SQL Server 安裝程式。  
  
    -   如果您在 Windows 7 SP1 或 Windows Server 2008 R2 SP1 作業系統電腦上執行安裝程式，您必須啟用 .NET Framework 3.5 SP1，再安裝 SQL Server 2012。  
  
        **使用下列其中一種方法，在 Windows Server 2008 R2 SP1 上啟用 .NET Framework 3.5 SP1：**  
  
        方法 1：使用伺服器管理員  
  
        1.  在 [伺服器管理員] 中，按一下 [加入功能]  顯示可能的功能清單。  
  
        2.  在 [選取功能]  介面中，展開 [.NET Framework 3.5.1 功能]  項目。  
  
        3.  展開 [.NET Framework 3.5.1 功能] 之後，您會看見兩個核取方塊。 一個是 .NET Framework 3.5.1 的核取方塊，另一個則是 WCF 啟動的核取方塊。 選取 [.NET Framework 3.5.1] ，然後按 [下一步] 。 除非您也安裝了必要的角色服務和功能，否則無法安裝 .NET Framework 3.5.1 功能。  
  
        4.  在 [確認安裝選項] 中檢閱選項，然後按一下 [安裝]。  
  
        5.  讓安裝程序完成，然後按一下 [關閉] 。  
  
        方法 2：使用 Windows PowerShell  
  
        1.  按一下 [開始] | [所有程式] | [附屬應用程式]  
  
        2.  展開 [Windows PowerShell]以滑鼠右鍵按一下 [Windows PowerShell]，然後按一下 [以系統管理員身分執行]。 請在 [使用者帳戶控制]  方塊中按一下 [是]  。  
  
        3.  在 PowerShell 命令提示字元中，輸入下列命令，然後在每個命令後面按下 ENTER：  
  
            ```  
            Import-Module ServerManager  
            Add-WindowsFeature as-net-framework  
            ```  
  
        **使用以下方法，在 Windows 7 SP1 上啟用 .NET Framework 3.5 SP1：**  
  
        1.  按一下 [開始] | [控制台] | [程式]，然後按一下 [開啟或關閉 Windows 功能]。 如果系統提示需要系統管理員密碼或確認，請輸入密碼或提供確認。  
  
        2.  若要啟用 [Microsoft .NET Framework 3.5.1] ，請選取此功能旁的核取方塊。 若要關閉某項 Windows 功能，請清除核取方塊。  
  
        3.  按一下 **[確定]**。  
  
        **使用部署映像服務與管理 (DISM.exe) 來啟用 .NET Framework 3.5 SP1：**  
  
        您也可以使用部署映像服務與管理 (DISM.exe) 來啟用 .NET Framework 3.5 SP1。 如需有關在線上啟用 Windows 功能的詳細資訊，請參閱 [在線上啟用或停用 Windows 功能](http://technet.microsoft.com/library/dd744582(WS.10).aspx)。 以下是啟用 .NET Framework 3.5 SP1 的指示：  
  
        1.  在命令提示字元輸入下列命令，列出作業系統中提供的所有功能。  
  
            ```  
            sm /online /Get-Features  
            ```  
  
        2.  選擇性：在命令提示字元輸入下列命令，列出您感興趣之特定功能的資訊。  
  
            ```  
            Dism /online /Get-FeatureInfo /FeatureName:NetFx3  
            ```  
  
        3.  輸入以下命令來啟用 Microsoft .NET Framework 3.5.1。  
  
            ```  
            Dism /online /Enable-Feature /FeatureName:NetFx3  
            ```  
  
-   .NET Framework 4 是 SQL Server 2012 的必要條件。 SQL Server 安裝程式會在功能安裝步驟期間安裝 .NET Framework 4。  
  
    在 Windows Server 2008 R2 SP1 Server Core 作業系統上安裝時，SQL Server 2012 Express 不會安裝 .NET Framework 4。 在安裝 SQL Server 2012 Express (僅資料庫) 時，如果有 .NET Framework 3.5 SP1 就不需要 .NET Framework 4。 當 .NET Framework 3.5 SP1 不存在或是安裝 SQL Server 2012 Management Studio Express、SQL Server 2012 Express with Tools 或 SQL Server 2012 Express with Advanced Services 時，您必須先安裝 .NET Framework 4，然後才能在 Windows Server 2008 R2 SP1 Server Core 作業系統上安裝 SQL Server 2012 Express。  
  
-   為確保 Visual Studio 元件可以正確安裝，您需要為 SQL Server 安裝更新。 SQL Server 安裝程式會檢查此更新的狀態，然後需要您下載並安裝更新才可繼續安裝 SQL Server。 為避免安裝 SQL Server 期間發生中斷，您可以先如下所述下載並安裝更新，然後執行 SQL Server 安裝程式 (或安裝 Windows Update 上所提供的 .NET Framework 3.5 SP1 之所有更新)：  
  
    -   如果您將 SQL Server 2012 安裝於 Windows Vista SP2 或 Windows Server 2008 SP2 作業系統的電腦上，可以從 [這裡](http://support.microsoft.com/?kbid=956250)取得所需的更新。  
  
    -   如果您在 Windows 7 SP1 或 Windows Server 2008 R2 SP1 作業系統電腦上安裝 SQL Server 2012，即已在電腦上安裝此更新。  
  
-   Windows PowerShell 2.0 是安裝 SQL Server 2012 Database Engine 元件和 SQL Server Management Studio 的必要條件，但是 SQL Server 安裝程式已不再安裝 Windows PowerShell。 如果您的電腦沒有 PowerShell 2.0，可以遵循 [Windows Management Framework](http://support.microsoft.com/kb/968929) 頁面上的指示啟用此元件。 您取得 Windows PowerShell 2.0 的方式取決於您在哪一個作業系統執行：  
  
    -   Windows Server 2008 -- Windows PowerShell 1.0 是一項功能，而且可以加入。 下載及安裝 Windows PowerShell 2.0 版本 (以 OS 修補程式的形式生效)。  
  
    -   Windows 7/Windows Server 2008 R2 -- 預設會安裝 Windows PowerShell 2.0。  
  
-   如果您打算在 SharePoint 環境中使用 SQL Server 2012 功能，則需要 SharePoint Server 2010 Service Pack 1 (SP1) 和 SharePoint 8 月份累計更新。 您必須先安裝 SP1、SharePoint [8 月份累計更新](http://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx)並完整修補伺服器陣列，然後再將 SQL Server 2012 功能加入至伺服器陣列。 此需求適用於下列 SQL Server 2012 功能：使用 Database Engine 的執行個體做為伺服器陣列的資料庫伺服器、設定 PowerPivot for SharePoint，或在 SharePoint 模式中部署 Reporting Services。  
  
### <a name="18-supported-operating-systems-for-sql-server-2012"></a>1.8 SQL Server 2012 支援的作業系統  
Windows Vista SP2、Windows Server 2008 SP2、Windows 2008 R2 SP1 和 Windows 7 SP1 作業系統都支援 SQL Server 2012。  
  
### <a name="19-sync-framework-is-not-included-in-the-installation-package"></a>1.9 Sync Framework 未包含在安裝套件中  
**問題** ：Sync Framework 未包含在 SQL Server 2012 安裝套件中。  
  
**因應措施** ：從 [這個 Microsoft 下載中心頁面](http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=23217)下載適當的 Sync Framework 版本。  
  
### <a name="110-if-visual-studio-2010-service-pack-1-is-uninstalled-the-sql-server-2012-instance-must-be-repaired-to-restore-certain-components"></a>1.10 如果您解除安裝 Visual Studio 2010 Service Pack 1，就必須修復 SQL Server 2012 執行個體才能還原特定元件  
**問題**：[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 安裝相依於 Visual Studio 2010 Service Pack 1 的某些元件。 如果您解除安裝 Service Pack 1，某些共用元件就會降級為其原始版本，而且系統會從電腦中完全移除幾個其他元件。  
  
**因應措施** ：從原始來源媒體或網路安裝位置修復 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 的執行個體。  
  
1.  從 SQL Server 安裝媒體啟動 SQL Server 安裝程式 (setup.exe)。  
  
2.  驗證必要元件和系統之後，安裝程式將會顯示 [SQL Server 安裝中心]  頁面。  
  
3.  按一下左側導覽區域中的 [維護]  ，然後按一下 [修復]  啟動修復作業。 如果使用 [開始]  功能表啟動安裝中心，您將需要在這個階段提供安裝媒體的位置。  
  
4.  安裝程式支援規則和檔案常式將會執行，以便確保您的系統已安裝必要元件而且電腦通過安裝程式驗證規則。 按一下 **[確定]** 或 **[安裝]** 繼續進行。  
  
5.  在 [選取執行個體]  頁面上，選取要修復的執行個體，然後按一下 [下一步]  繼續進行。  
  
6.  修復規則將會執行，以便驗證作業。 若要繼續進行，請按 **[下一步]**。  
  
7.  [已完成修復準備工作]  頁面會指出作業準備繼續進行。 若要繼續，請按一下 [修復] 。  
  
8.  [修復進度]  頁面會顯示修復作業的狀態。 [完成]  頁面會指出作業已完成。  
  
如需有關如何修復 SQL Server 執行個體的詳細資訊，請參閱 [修復失敗的 SQL Server 2012 安裝](http://msdn.microsoft.com/library/cc646006(SQL.110).aspx)。  
  
### <a name="111-an-instance-of-sql-server-2012-might-fail-after-an-os-upgrade"></a>1.11 SQL Server 2012 的執行個體可能會在作業系統升級之後失敗  
**問題** ：當您將作業系統從 Windows Vista 升級為 Windows 7 SP1 之後，SQL Server 2012 的執行個體可能會失敗並出現下列錯誤。  
  
`Setup has detected that the .NET Framework version 4 needs to be repaired. Do not restart your computer until Setup is complete.`  
  
**因應措施**：在您升級作業系統之後，請修復 .NET Framework 4 的安裝。 如需詳細資訊，請參閱 [如何修復現有的 .NET Framework 安裝](http://support.microsoft.com/kb/306160)。  
  
### <a name="112-sql-server-edition-upgrade-requires-a-restart"></a>1.12 SQL Server 版本升級需要重新啟動  
**問題**：當您針對 SQL Server 2012 執行個體進行版本升級時，與新版本相關聯的某些功能可能無法立即啟動。  
  
**因應措施**：在 SQL Server 2012 執行個體的版本升級完成之後重新啟動電腦。 如需有關 SQL Server 2012 支援之升級方式的詳細資訊，請參閱 [支援的版本與版本升級](http://msdn.microsoft.com/library/ms143393.aspx)。  
  
### <a name="113-database-with-read-only-filegroup-or-files-cannot-be-upgraded"></a>1.13 無法升級具有唯讀檔案群組或檔案的資料庫  
**問題**：如果資料庫或其檔案/檔案群組設定為唯讀，您就無法透過附加資料庫或從備份還原資料庫，升級資料庫。  此時，系統會傳回錯誤 3415。  當您執行 SQL Server 執行個體的就地升級時，也會發生這個問題。 也就是說，您嘗試透過安裝 SQL Server 2012 來取代現有的 SQL Server 執行個體，而且一個或多個現有的資料庫設定為唯讀。  
  
**因應措施** ：升級之前，請確定資料庫及其檔案/檔案群組設定為可讀寫。  
  
### <a name="114-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.14 如果您使用相同的 IP 位址，重新安裝 SQL Server 容錯移轉叢集的執行個體會失敗  
**問題：** 如果您在安裝 SQL Server 容錯移轉叢集執行個體期間指定不正確的 IP 位址，安裝就會失敗。 解除安裝失敗的執行個體之後，如果您嘗試使用相同的執行個體名稱和正確的 IP 位址來重新安裝 SQL Server 容錯移轉叢集執行個體，安裝仍會失敗。 發生失敗的原因是先前的安裝遺留了重複的資源群組。  
  
**因應措施** ：若要解決此問題，請在重新安裝期間使用不同的執行個體名稱，或在重新安裝之前手動刪除資源群組。 如需詳細資訊，請參閱 [在 SQL Server 容錯移轉叢集中加入或移除節點](http://msdn.microsoft.com/library/ms191545)。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="AS"></a>2.0 Analysis Services  
  
### <a name="21-sql-editor-and-as-editor-cannot-connect-to-their-respective-server-instances-in-the-same-ssms-instance"></a>2.1 SQL 編輯器和 AS 編輯器無法在相同 SSMS 執行個體中連接到其各自的伺服器執行個體  
**問題** ：已連接 SQL 編輯器時，無法使用 MDX/DMX 編輯器連接到 Analysis Services 伺服器。  
  
使用 SQL Server Management Studio 2012 (SSMS) 時，如果 .sql 檔案已在編輯器中開啟而且連接到 SQL Server 執行個體，則相同 SSMS 執行個體中開啟的 MDX 或 DMX 檔案就無法連接到 AS 伺服器執行個體。 同樣地，如果 MDX 或 DMX 檔案已在 SSMS 的編輯器中開啟，並連接到 AS 伺服器執行個體，則相同 SSMS 執行個體中開啟的 .sql 檔案就無法連接到 SQL Server 執行個體。  
  
**因應措施**：若要解決這個問題，請使用下列其中一個選項。  
  
-   啟動另一個 SSMS 執行個體，開啟 MDX / DMX 檔案。  
  
-   中斷連接 SQL 編輯器，然後將 MDX / DMX 編輯器連接到 AS 伺服器。  
  
### <a name="22-cannot-create-or-open-tabular-projects-when-builtinadministrators-group-name-cannot-be-resolved"></a>2.2 無法解析 BUILTIN\Administrators 群組名稱時，無法建立或開啟表格式專案  
**問題** ：您必須是工作空間資料庫伺服器上的系統管理員，才能建立或開啟表格式專案。 您可以透過新增使用者名稱或群組名稱，將使用者新增至伺服器系統管理員群組。 如果您是 BUILTIN\Administrator 群組的成員，就不能建立或編輯 BIM 檔案，除非工作空間資料庫伺服器聯結至其原始佈建的網域。 如果您開啟或建立 BIM 檔案，作業將會失敗並出現下列錯誤訊息：  
  
`"The BIM file cannot be opened. The server connected to is not valid. Reason: You are not an administrator of server [server name]."`  
  
**因應措施：**  
  
-   重新聯結工作空間資料庫伺服器與 SQL Server Data Tools (SSDT) 電腦至網域。  
  
-   如果工作空間資料庫伺服器及/或 SSDT 電腦不會隨時聯結網域，請加入個別使用者名稱而不要加入 BUILTIN\Administrators 群組做為工作空間資料庫伺服器上的系統管理員。  
  
### <a name="23-ssis-components-for-as-tabular-models-do-not-work-as-expected"></a>2.3 AS 表格式模型的 SSIS 元件未如預期運作  
Analysis Services (AS) 的 SQL Server Integration Services (SSIS) 元件未以預期方式針對表格式模型運作。 以下是當您嘗試為搭配表格式模型運作而撰寫 SSIS 套件時，可能發生的已知問題。  
  
**問題** ：AS 連接管理員無法在與資料來源相同的方案中使用表格式模型。  
  
**因應措施** ：您必須明確地連接到 AS 伺服器，再設定 AS 處理工作或 AS 執行 DDL 工作。  
  
當您使用表格式模型時，AS 處理工作有一些問題存在：  
  
**問題** ：您不是看到資料庫、資料表和資料分割，而是看到 Cube、量值群組和維度。 這是工作的限制。  
  
**因應措施** ：您仍然可以使用 Cube/量值群組/維度結構來處理表格式模型。  
  
**問題** ：由表格式模式中執行之 AS 支援的一些處理選項並未在 AS 處理工作中公開，如處理重組。  
  
**因應措施** ：請改用 Analysis Services 執行 DDL 工作來執行包含 ProcessDefrag 命令的 XMLA 指令碼。  
  
**問題** ：工具中有些組態選項不適用。 例如，處理資料分割時不應該使用「處理相關物件」，而「平行處理」組態選項則包含無效錯誤訊息，說明標準 SKU 上不支援平行處理。  
  
**因應措施** ：無  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="BOL"></a>3.0 線上叢書  
  
### <a name="31-help-viewer-for-sql-server-crashes-in-environments-configured-to-run-only-ipv6"></a>3.1 在設定為只執行 IPv6 的環境中，SQL Server 的說明檢視器會當機  
**問題**：如果您的環境設定為只執行 IPv6，SQL Server 2012 的說明檢視器會當機，並出現下列錯誤訊息：  
  
`HelpLibAgent.exe has stopped working.`  
  
> [!IMPORTANT]  
> 適用於只啟用 IPv6 的所有環境。 IPv4 (以及混合 IPv4 與 IPv6) 啟用的環境不受影響。  
  
**因應措施**：若要避免這個問題，請啟用 IPv4，或使用下列步驟加入登錄項目，並建立 ACL 以針對 IPv6 啟用說明檢視器：  
  
1.  在 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Help\v1.0 底下建立名為 “IPv6” 且具有 “1 (DWORD(32 bit))” 值的登錄機碼。  
  
2.  從管理員 CMD 視窗執行下列命令，為 IPv6 通訊埠設定安全性 ACL：  
  
    ```  
    netsh http add urlacl url=http://[::1]:47873/help/ sddl=D:(A;;GX;;;WD)  
    ```  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-not-supported-in-a-cluster"></a>4.1 叢集中不支援 DQS  
**問題** ：SQL Server 叢集安裝中不支援 DQS。 如果您正在安裝 SQL Server 的叢集執行個體，就不得在 [特徵選取]  頁面上選取 [Data Quality Services]  和 [Data Quality Client]  核取方塊。 如果您在叢集執行個體安裝期間選取這兩個核取方塊 (而且您藉由執行 DQSInstaller.exe 檔案完成 Data Quality Server 安裝)，DQS 將會安裝在這個節點上，但是當您在叢集中加入其他節點時無法在其他節點上使用，因此 DQS 無法在其他節點上運作。  
  
**因應措施** ：安裝 SQL Server 2012 累計更新 1 可解決此問題。 如需相關指示，請參閱 [http://support.microsoft.com/kb/2674817](http://support.microsoft.com/kb/2674817)。  
  
### <a name="42-to-reinstall-data-quality-server-delete-the-dqs-objects-after-uninstalling-data-quality-server"></a>4.2 若要重新安裝 Data Quality Server，請在解除安裝資料品質伺服器之後刪除 DQS 物件  
**問題** ：如果您解除安裝 Data Quality Server，並不會自 SQL Server 執行個體刪除 DQS 物件 (DQS 資料庫、DQS 登入和 DQS 預存程序)。  
  
**因應措施**：若要在相同電腦的同一個 SQL Server 執行個體中重新安裝 Data Quality Server，您必須手動從該 SQL Server 執行個體中刪除 DQS 物件。 此外，您也必須從電腦上的 C:\Program Files\Microsoft SQL Server\MSSQL11.<SQL_Server_Instance>\MSSQL\DATA 資料夾中刪除 DQS 資料庫 (DQS_MAIN、DQS_PROJECTS 和 DQS_STAGING_DATA) 檔案，然後再重新安裝資料品質伺服器。 否則，Data Quality Server 安裝會失敗。 若要保留資料 (如知識庫或資料品質專案)，請移動資料庫檔案而不要刪除。 如需有關解除安裝程序完成之後移除 DQS 物件的詳細資訊，請參閱 [移除 Data Quality Server 物件](http://msdn.microsoft.com/library/hh231667.aspx)。  
  
### <a name="43-indication-of-a-terminated-knowledge-discovery-or-interactive-cleansing-activity-is-delayed"></a>4.3 指示知識探索已終止或互動式清理活動已延遲  
**問題** ：如果系統管理員在 [活動監控] 畫面上終止活動，則執行知識探索、網域管理或互動式清理活動的互動式使用者在執行下一項作業之前，不會接到任何資訊指出活動已被終止。  
  
**因應措施** ：無  
  
### <a name="44-a-cancel-operation-discards-work-from-multiple-activities"></a>4.4 取消作業會捨棄多項活動的工作  
**問題** ：如果您針對執行中的知識探索或網域管理活動按一下 [取消]  ，而在該活動執行時，先前已完成其他活動但未執行發行作業，則從上次發行以來所執行的所有活動工作都會被捨棄，而不只是捨棄目前的活動。  
  
**因應措施** ：若要避免這種狀況，請發行您需要保存在知識探索中的工作，再啟動新的活動。  
  
### <a name="45-controls-do-not-scale-properly-on-large-font-sizes"></a>4.5 控制項無法針對大字型適當縮放  
**問題** ：如果您將文字大小變更為 [大 - 150%] (在 Windows Server 2008 或 Windows 7 中)，或將 [自訂 DPI 設定] 變更為 200% (在 Windows 7 中)，便無法存取 [新增知識庫]  頁面上的 [取消]  和 [建立]  按鈕。  
  
**因應措施**：若要解決這個問題，請將字型設定為較小的大小。  
  
### <a name="46-screen-resolution-of-800x600-is-not-supported"></a>4.6 不支援 800x600 螢幕解析度  
**問題** ：如果螢幕解析度設定為 800x600，Data Quality Client 應用程式不會正確顯示。  
  
**因應措施** ：若要解決這個問題，請將螢幕解析度設定為較高的值。  
  
### <a name="47-map-bigint-column-in-the-source-data-to-a-decimal-domain-to-prevent-data-loss"></a>4.7 將來源資料中的 Bigint 資料行對應至 Decimal 定義域以防止資料遺失  
**問題** ：如果來源資料中的資料行是 **bigint** 資料類型，您必須在 DQS 中將該資料行對應至 **decimal** 資料類型的定義域，而不是 **integer** 資料類型的定義域。 這是因為 **decimal** 資料類型代表比 **int** 資料類型更大範圍的值，因此可以保存較大的值。  
  
### <a name="48-nvarcharmax-and-varcharmax-data-types-are-not-supported-in-the-dqs-cleansing-component-in-integration-services"></a>4.8 Integration Services 中的 DQS 清理元件不支援 NVARCHAR(MAX) 和 VARCHAR(MAX) 資料類型  
**問題** ：Integration Services 中的 DQS 清理元件不支援 **nvarchar(max)** 和 **varchar(max)** 資料類型的資料行。 因此，這些資料行無法在 DQS 清理轉換編輯器的 [對應] 索引標籤中用於對應，所以無法進行清理。  
  
**因應措施** ：使用 DQS 清理元件來處理這些資料行之前，您必須先使用資料轉換，將它們轉換成 **DT_STR** 或 **DT_WSTR** 資料類型。  
  
### <a name="49-the-item-to-run-dqsinstallerexe-on-the-start-menu-is-overwritten-on-new-sql-server-instance-installation"></a>4.9 新的 SQL Server 執行個體安裝會覆寫開始功能表上執行 DQSInstaller.exe 的項目  
**問題：** 如果您選擇在 SQL Server 執行個體中安裝 Data Quality Services，完成 SQL Server 安裝程式之後，系統會在 [開始]  功能表的 [Data Quality Services]  程式群組底下建立名為 [Data Quality Server 安裝程式]  的項目。 不過，如果您在相同的電腦上安裝多個 SQL Server 執行個體，[開始]  功能表上仍會只有單一 [Data Quality Server 安裝程式]  項目。 只要按一下這個項目，就會在最近安裝的 SQL Server 執行個體中執行 DQSInstaller.exe 檔案。  
  
### <a name="410-activity-monitoring-displays-incorrect-status-for-failed-integration-services-cleansing-activities"></a>4.10 活動監控針對失敗的 Integration Services 清理活動顯示不正確的狀態  
即使 Integration Services 清理活動失敗，[活動監控] 畫面仍然會在 [目前狀態]  資料行中不正確地顯示 [成功]  。  
  
### <a name="411-schema-name-is-not-displayed-as-part-of-tableview-name"></a>4.11 結構描述名稱並未顯示成資料表/檢視表名稱的一部分  
在 Data Quality Client 的對應階段期間，當您在任何 DQS 活動中選取 SQL Server 資料來源時，就會顯示不含結構描述名稱的資料表和檢視表清單。 因此，如果存在許多名稱相同但結構描述不同的資料表/檢視表，您就只能查看資料預覽，或是選取它們，然後查看要對應的可用欄位，藉以進行區別。  
  
### <a name="412-issue-with-cleansing-output-and-export-if-data-source-is-mapped-to-a-composite-domain-containing-a-child-domain-of-date-type"></a>4.12 如果資料來源對應至包含日期類型之子定義域的複合定義域，清理輸出和匯出就會發生問題  
在清理資料品質專案中，如果您將來源資料中的欄位對應至具有日期資料類型之子定義域的複合定義域，清理結果的子定義域輸出就會具有不正確的日期格式，而且匯出至資料庫的作業會失敗。  
  
### <a name="413-error-when-mapping-to-an-excel-sheet-that-contains-a--semicolon-in-its-name"></a>4.13 對應至名稱包含 ; (分號) 的 Excel 工作表時發生錯誤  
**問題** ：在 Data Quality Client 中任何 DQS 活動的 [對應]  頁面上，如果您對應至名稱包含 ; (分號) 的來源 Excel 工作表，則在 [對應]  頁面上按 [下一步]  時，就會顯示無法處理的例外狀況訊息。  
  
**因應措施** ：在包含要對應之來源資料的 Excel 檔案中，移除工作表名稱中的 ; (分號)，然後再試一次。  
  
### <a name="414-issue-with-date-or-datetime-values-in-unmapped-source-fields-in-excel-during-cleansing-and-matching"></a>4.14 在清理和比對期間，Excel 中未對應之來源欄位的 Date 或 DateTime 值發生問題  
**問題**：如果您的來源資料是 Excel，而且您尚未對應包含 **Date** 或 **DateTime** 資料類型值的來源欄位，則清理和比對活動期間會發生下列狀況：  
  
-   未對應的 **Date** 值會以 yyyymmdd 格式顯示並匯出。  
  
-   未對應之 **DateTime** 值的時間值會遺失，而且它們會以 yyyymmdd 格式顯示並匯出。  
  
**因應措施** ：您可以在清理活動的 [管理和檢視結果]  頁面以及比對活動的 [比對]  頁面上，於右下角的窗格中檢視未對應的欄位值。  
  
### <a name="415-cannot-import-domain-values-from-an-excel-file-xls-containing-more-than-255-columns-of-data"></a>4.15 無法從包含超過 255 個資料行的 Excel 檔案 (.xls) 匯入定義域值  
**問題** ：如果您從包含超過 255 個資料行的 Excel 97-2003 檔案 (.xls)，將值匯入定義域中，就會出現例外狀況訊息，而且匯入會失敗。  
  
**因應措施** ：若要修正此問題，您可以進行下列其中一項作業：  
  
-   將 .xls 檔案另存為 .xlsx 檔案，然後將 .xlsx 檔案的值匯入定義域中。  
  
-   在 .xls 檔案中，移除超過第 255 個資料行之所有資料行的資料、儲存檔案，然後將 .xls 檔案的值匯入定義域中。  
  
### <a name="416-activity-monitoring-feature-is-unavailable-for-roles-other-than-dqsadministrator"></a>4.16 dqs_administrator 以外的角色無法使用活動監控功能  
活動監控功能只適用於擁有 dqs_administrator 角色的使用者。 如果您的使用者帳戶具有 dqs_kb_editor 或 dqs_kb_operator 角色，則 Data Quality Client 應用程式中將無法使用活動監控功能。  
  
### <a name="417-error-on-opening-a-knowledge-base-in-the-recent-knowledge-base-list-for-domain-management"></a>4.17 在最近使用的知識庫清單中針對定義域管理開啟知識庫時發生錯誤  
問題：如果您在 Data Quality Client 首頁畫面中，於 [最近使用的知識庫]  清單中針對定義域管理活動開啟知識庫，您可能會收到以下錯誤：  
  
`"A configuration with name 'RecentList:KB:<domain>\<username>' already exists in the database."`  
  
發生此錯誤是因為 DQS 在 SQL Server 資料庫中與在 C# 中比較字串的方式不同。 SQL Server 資料庫中的字串比較不區分大小寫，但是在 C# 中則區分大小寫。  
  
我們使用範例來說明。 假設有使用者 Domain\user1。 此使用者使用 “user1” 帳戶登入 Data Quality Client 電腦，並處理知識庫。 DQS 會針對每一位使用者將最近使用的知識庫儲存為 DQS_MAIN 資料庫中 A_CONFIGURATION 資料表內的記錄。 在此情況下，此記錄將會以下列名稱儲存：RecentList:KB:Domain\user1。 之後，使用者以 “User1” 身分 (請注意 U 為大寫) 登入 Data Quality Client 電腦，並嘗試在 [最近使用的知識庫]  清單中針對定義域管理活動開啟此知識庫。 DQS 中的基礎程式碼將會比較兩個字串 RecentList:KB:DOMAIN\user1 和 DOMAIN\User1，而 C# 中會進行區分大小寫的字串比較，因為這兩個字串不相符，所以 DQS 會嘗試在 DQS_MAIN 資料庫的 A_CONFIGURATION 資料表中為使用者 (User1) 插入一筆新的記錄。 但是，由於 SQL 資料庫中的字串比較不區分大小寫，所以導致該字串已經存在於 DQS_MAIN 資料庫的 A_CONFIGURATION 資料表中，因此插入作業將會失敗。  
  
**因應措施** ：若要修正此問題，您可以進行下列其中一項作業：  
  
-   執行下列陳述式來確認是否有重複的項目存在：  
  
    ```  
    SELECT * FROM DQS_MAIN.dbo.A_CONFIGURATION WHERE NAME like 'RecentList%'  
    ```  
  
    接下來，您可以執行以下陳述式，只針對受影響的使用者刪除此記錄，方法是變更 WHERE 子句中的值，以符合受影響的定義域和使用者名稱。  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%<domain>\<username>'  
    ```  
  
    另外，您也可以針對 DQS 中的所有使用者移除所有最近項目：  
  
    ```  
    DELETE DQS_MAIN.dbo.A_Configuration WHERE NAME LIKE 'RecentList%'  
    ```  
  
-   在登入 Data Quality Client 電腦時，使用與上次相同的大小寫來指定您的使用者帳戶。  
  
> [!NOTE]  
> 若要避免此問題，請在登入 Data Quality Client 電腦時，使用一致的大小寫規則來指定您的使用者帳戶。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="DE"></a>5.0 Database Engine  
  
### <a name="51-use-of-distributed-replay-controller-and-distributed-replay-client-features"></a>5.1 使用 Distributed Replay Controller 和 Distributed Replay Client 功能  
**問題** ：Windows Server 2008、Windows Server 2008 R2 和 Windows Server 7 的 Server Core SKU 中有提供 Distributed Replay Controller 和 Distributed Replay Client 功能，但是 Server Core SKU 中不支援這兩個功能。  
  
**因應措施** ：請勿在 Windows Server 2008、Windows Server 2008 R2 和 Windows Server 7 的 Server Core SKU 中安裝或使用這兩個功能。  
  
### <a name="52-sql-server-management-studio-depends-on-visual-studio-2010-sp1"></a>5.2 SQL Server Management Studio 與 Visual Studio 2010 SP1 相依  
**問題**：SQL Server 2012 Management Studio 有賴於 Visual Studio 2010 SP1 才能正確運作。 解除安裝 Visual Studio 2010 SP1 可能會導致 SQL Server Management Studio 中的功能遺失並讓 Management Studio 處於不支援的狀態。 在此情況下，可能會看到以下問題：  
  
-   ssms.exe 的命令列參數無法正確運作。  
  
-   嘗試使用 /? 參數執行 ssms.exe 時， 顯示的說明資訊不正確。  
  
-   針對在 [Windows 檔案總管] 中按兩下所開啟的每一個檔案，都會啟動新的 SSMS 執行個體來開啟檔案。  
  
-   正常使用者模式下無法偵錯查詢。  
  
**因應措施**：再次安裝 Visual Studio 2010 SP1，並重新啟動 Management Studio。  
  
### <a name="53-x64-operating-systems-require-64-bit-powershell-20"></a>5.3 x64 作業系統需要 64 位元 PowerShell 2.0  
**問題** ：64 位元作業系統上的 SQL Server 2012 執行個體不支援 32 位元的 Windows PowerShell Extensions for SQL Server 安裝。  
  
**因應措施：**  
  
-   安裝具有 64 位元管理工具和 64 位元 Windows PowerShell Extensions for SQL Server 的 64 位元 SQL Server 2012。  
  
-   或從 32 位元 Windows PowerShell 2.0 提示匯入 SQLPS 模組。  
  
### <a name="54-an-error-might-occur-when-navigating-in-the-generate-script-wizard"></a>5.4 在產生指令碼精靈中導覽時可能會發生錯誤  
**問題** ：在產生指令碼精靈中，按一下 [儲存或發佈指令碼] 產生指令碼，然後按一下 [選擇選項]  或 [設定指令碼編寫選項] 進行導覽之後，再次按一下 [儲存或發佈指令碼]  可能會產生下列錯誤：  
  
<a name="prean-exception-occurred-while-executing-a-transact-sql-statement-or-batch-microsoftsqlserverconnectioninfo"></a><pre>An exception occurred while executing a Transact-SQL statement or batch. (Microsoft.SqlServer.ConnectionInfo)  
------------------------------  
其他資訊:  
無效的物件名稱 'sys.federations'。 (Microsoft SQL Server 錯誤：208)</pre>  
  
**因應措施** ：關閉產生指令碼精靈，並重新開啟。  
  
### <a name="55-new-maintenance-plan-layout-not-compatible-with-earlier-sql-server-tools"></a>5.5 新的維護計畫配置與舊版的 SQL Server 工具不相容  
**問題** ：當 SQL Server 2012 管理工具用來修改舊版 SQL Server 管理工具 (SQL Server 2008 R2、SQL Server 2008 或 SQL Server 2005) 所建立的現有維護計畫時，會以新格式儲存維護計畫。 舊版 SQL Server 管理工具不支援此新格式。  
  
**因應措施**：無  
  
### <a name="56-intellisense-has-limitations-when-logged-in-to-a-contained-database"></a>5.6 登入自主資料庫時，Intellisense 有限制  
問題：當自主使用者登入自主資料庫時，SQL Server Management Studio (SSMS) 和 SQL Server Data Tools (SSDT) 中的 Intellisense 無法如預期般運作。 在這類情況下會看到以下行為：  
  
1.  無效物件的底線不會出現。  
  
2.  自動完成清單不會出現。  
  
3.  內建函數的工具提示說明無效。  
  
**因應措施**：無  
  
### <a name="57-alwayson-availability-groups"></a>5.7 AlwaysOn 可用性群組  
在您嘗試建立可用性群組之前，請參閱線上叢書中的 [AlwaysOn 可用性群組的必要條件、限制和建議 (SQL Server)](http://go.microsoft.com/?linkid=9753168) 。 如需 AlwaysOn 可用性群組的簡介，請參閱線上叢書中的 [AlwaysOn 可用性群組 (SQL Server)](http://go.microsoft.com/?linkid=9753166)。  
  
#### <a name="571-client-connectivity-for-alwayson-availability-groups"></a>5.7.1 AlwaysOn 可用性群組的用戶端連接  
**更新日期** ：2012 年 8 月 13 日  
  
本節說明 AlwaysOn 可用性群組的驅動程式支援，以及不受支援之驅動程式的因應措施。  
  
**驅動程式支援**  
  
下表摘要列出 AlwaysOn 可用性群組的驅動程式支援：  
  
|驅動程式|多重子網路容錯移轉|應用程式的意圖|唯讀路由|多重子網路容錯移轉：快速單一子網路端點容錯移轉|多重子網路容錯移轉：SQL 叢集執行個體的具名執行個體解析|  
|----------|--------------------------|----------------------|----------------------|------------------------------------------------------------------|---------------------------------------------------------------------------------|  
|SQL Native Client 11.0 ODBC|是|是|是|是|是|  
|SQL Native Client 11.0 OLEDB|否|是|是|否|否|  
|具有連接修補程式的 ADO.NET 與 .NET Framework 4.0**\&#42;**|是|是|是|是|是|  
|具有連接修補程式的 ADO.NET 與 .NET Framework 3.5 SP1 **\&#42;\&#42;**|是|是|是|是|是|  
|Microsoft JDBC Driver 4.0 for SQL Server|是|是|是|是|是|  
  
**\&#42;** 下載 ADO.NET 與 .NET Framework 4.0 連接修補程式： [http://support.microsoft.com/kb/2600211](http://support.microsoft.com/kb/2600211)。  
  
**\&#42;\&#42;** 下載 ADO.NET 與 .NET Framework 3.5 SP1 連接修補程式： [http://support.microsoft.com/kb/2654347](http://support.microsoft.com/kb/2654347)。  
  
**MultiSubnetFailover 關鍵字和已建立關聯的功能**  
  
MultiSubnetFailover 是新的連接字串關鍵字，可用來加快 SQL Server 2012 中 AlwaysOn 可用性群組和 AlwaysOn 容錯移轉叢集執行個體的容錯移轉速度。 當您在連接字串中設定 MultiSubnetFailover=True 時，就會啟用下列三項子功能：  
  
-   將多重子網路快速容錯移轉至 AlwaysOn 可用性群組或容錯移轉叢集執行個體的多重子網路接聽程式。  
  
    -   將具名執行個體解析為多重子網路 AlwaysOn 容錯移轉叢集執行個體。  
  
-   將單一子網路快速容錯移轉至 AlwaysOn 可用性群組或容錯移轉叢集執行個體的單一子網路接聽程式。  
  
    -   這項功能是在連接至具有單一子網路中單一 IP 的接聽程式時使用。 它會執行更積極的 TCP 連接重試，加快單一子網路容錯移轉的速度。  
  
-   將具名執行個體解析為多重子網路 AlwaysOn 容錯移轉叢集執行個體。  
  
    -   這項功能可針對具有多個子網路端點的 AlwaysOn 容錯移轉叢集執行個體加入具名執行個體解析支援。  
  
**NET Framework 3.5 或 OLEDB 不支援 MultiSubnetFailover=True**  
  
**問題** ：如果您的可用性群組或容錯移轉叢集執行個體具有相依於不同子網路中多個 IP 位址的接聽程式名稱 (WSFC 叢集管理員中稱為網路名稱或用戶端存取點)，而且您使用 ADO.NET 搭配 .NET Framework 3.5 SP1 或使用 SQL Native Client 11.0 OLEDB，對可用性群組接聽程式的 50% 用戶端連接要求可能會達到連接逾時。  
  
**因應措施** ：建議您執行下列其中一項工作。  
  
-   如果您沒有操作叢集資源的權限，請將連接逾時變更為 30 秒 (此值會產生 20 秒 TCP 逾時期間加上 10 秒緩衝時間)。  
  
    **優點**：如果發生跨子網路容錯移轉，用戶端復原時間很短。  
  
    **缺點**：一半的用戶端連接需要 20 秒以上。  
  
-   如果您有操作叢集資源的權限，比較建議的作法是將可用性群組接聽程式的網路名稱設定為 **RegisterAllProvidersIP**=0。 如需詳細資訊，請參閱本節後面的＜停用 RegisterAllProvidersIP 和減少 TTL 的範例 PowerShell 指令碼＞。  
  
    **優點** ：您不需要增加用戶端連接逾時值。  
  
    **缺點** ：如果發生跨子網路容錯移轉，用戶端復原時間可能是 15 分鐘以上，視您的 HostRecordTTL 設定和跨網站 DNS/AD 複寫排程的設定而定。  
  
**停用 RegisterAllProvidersIP 和減少 TTL 的範例 PowerShell 指令碼**  
  
下列範例 PowerShell 指令碼示範如何停用 `RegisterAllProvidersIP` 和減少 TTL。 請使用您要變更的接聽程式名稱來取代 `yourListenerName` 。  
  
```  
Import-Module FailoverClusters  
Get-ClusterResource yourListenerName|Set-ClusterParameter RegisterAllProvidersIP 0  
Get-ClusterResource yourListenerName|Set-ClusterParameter HostRecordTTL 300  
```  
  
#### <a name="572-upgrading-from-ctp3-with-availability-group-configured-is-not-supported"></a>5.7.2 不支援從設定可用性群組的 CTP3 升級  
升級之前，請卸除可用性群組，然後重新建立它。 這種行為是基於 CTP3 組建的限制。 未來的組建將沒有這項限制。  
  
#### <a name="573-side-by-side-installation-of-ctp3-with-later-versions-is-not-supported-if-you-have-an-availability-group-configured-in-your-instance"></a>5.7.3 如果您的執行個體已經設定可用性群組，就不支援 CTP3 與更新版本的並存安裝  
這種行為是基於 CTP3 組建的限制。 未來的組建將沒有這項限制。  
  
#### <a name="574-side-by-side-installation-of-ctp3-with-later-versions-of-failover-cluster-instances-is-not-supported"></a>5.7.4 不支援 CTP3 與新版容錯移轉叢集執行個體的並存安裝  
這種行為是基於 CTP3 組建的限制。 未來的組建將沒有這項限制。 若要從 CTP3 升級容錯移轉叢集執行個體，請務必同時升級節點上的所有執行個體。  
  
#### <a name="575--timeouts-may-occur-when-using-multi-ips-in-the-same-subnet-with-alwayson"></a>5.7.5 當您在具有 AlwaysOn 的相同子網路中使用多個 IP 時，可能會發生逾時  
**問題** ：當您在具有 AlwaysOn 的相同子網路中使用多個 IP 時，有時客戶可能會看到逾時。 如果清單中的首要 IP 無效，就會發生這個情況。  
  
**因應措施** ：在連接字串中使用 'multisubnetfailover = true'。  
  
#### <a name="576-failure-to-create-new-availability-group-listeners-because-of-active-directory-quotas"></a>5.7.6 由於 Active Directory 配額而無法建立新的可用性群組接聽程式  
**問題** ：新可用性群組接聽程式的建立作業可能會在建立時失敗，因為您已達到參與叢集節點電腦帳戶的 Active Directory 配額。 如需詳細資訊，請參閱 [如何排解叢集服務帳戶修改電腦物件時所遇到的疑難](http://support.microsoft.com/kb/307532) 和 [Active Directory 配額](http://technet.microsoft.com/library/cc904295(WS.10).aspx)。  
  
#### <a name="577-netbios-conflicts-because-availability-group-listener-names-use-an-identical-15-character-prefix"></a>5.7.7 NetBIOS 發生衝突，因為可用性群組接聽程式的名稱使用完全相同的 15 個字元前置詞  
如果您有兩個由相同 Active Directory 所控制的 WSFC 叢集，而且嘗試使用超過 15 個字元的名稱以及完全相同的 15 個字元前置詞，在這兩個叢集中建立可用性群組接聽程式，就會收到一則錯誤，指出系統無法讓虛擬網路名稱資源上線。 如需有關 DNS 名稱之前置詞命名規則的詳細資訊，請參閱 [指派網域名稱](http://technet.microsoft.com/library/cc731265(WS.10).aspx)  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="IS"></a>6.0 Integration Services  
  
### <a name="61-the-change-data-capture-service-for-oracle-and-the-change-data-capture-designer-console-for-oracle"></a>6.1 Oracle 適用的異動資料擷取服務和異動資料擷取設計工具主控台  
Oracle CDC 服務是一種 Windows 服務，可掃描 Oracle 交易記錄，並將相關 Oracle 資料表的變更擷取到 SQL Server 變更資料表中。 CDC 設計工具主控台是用來開發及維護 Oracle CDC 執行個體。 CDC 設計工具主控台是一種 Microsoft Management Console (MMC) 嵌入式管理單元。  
  
#### <a name="611-install-the-cdc-service-for-oracle-and-the-cdc-designer-for-oracle"></a>6.1.1 安裝 Oracle CDC 服務和 Oracle CDC 設計工具  
**問題** ：SQL Server 安裝程式不會安裝 CDC 服務和 CDC 設計工具。 您必須依照更新說明檔的描述，在符合需求和必要條件的電腦上手動安裝 CDC 服務或 CDD 設計工具。  
  
**因應措施** ：若要安裝 Oracle CDC 服務，請從 SQL Server 安裝媒體手動執行 AttunityOracleCdcService.msi。 若要安裝 CDC 設計工具主控台，請從 SQL Server 安裝媒體手動執行 AttunityOracleCdcDesigner.msi。  x86 和 x64 的安裝套件位於 SQL Server 安裝媒體的 .\Tools\AttunityCDCOracle\ 中。  
  
#### <a name="612-f1-help-functionality-points-to-incorrect-documentation-files"></a>6.1.2 F1 說明功能指向不正確的文件檔  
**問題** ：當您使用 F1 說明下拉式清單或在 Attunity 主控台中按一下 "?" 時，無法存取正確的說明文件。 這些方法指向不正確的 chm 檔案。  
  
**因應措施** ：當安裝 Oracle CDC 服務或 Oracle CDC 設計工具時，便會安裝正確的 chm 檔案。 若要檢視正確的說明內容，請直接從這個位置啟動 chm 檔案： `%Program Files%\Change Data Capture for Oracle by Attunity\*.chm`。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="MDS"></a>7.0 Master Data Services  
  
### <a name="71-fixing-an-mds-installation-in-a-cluster"></a>7.1 修正叢集中的 MDS 安裝  
**問題** ：如果您在選取 [Master Data Services]  核取方塊的情況下安裝 RTM 版本的 SQL Server 2012 叢集執行個體，將會在單一節點上安裝 MDS，但是 MDS 將無法在您加入至叢集的其他節點上使用及運作。  
  
**因應措施**：若要解決此問題，您必須安裝 SQL Server 2012 Cumulative Release 1 (CU1) 並執行下列步驟：  
  
1.  確定沒有任何現有的 SQL/MDS 安裝。  
  
2.  將 SQL Server 2012 CU1 下載至本機目錄中。  
  
3.  在主要叢集節點上安裝具有 MDS 功能的 SQL Server 2012，然後在任何其他叢集節點上安裝具有 MDS 功能的 SQL Server 2012。  
  
如需有關這些問題的詳細資訊，以及如何執行上述步驟的詳細資訊，請參閱 [http://support.microsoft.com/kb/2683467](http://support.microsoft.com/kb/2683467)。  
  
### <a name="72-microsoft-silverlight-5-required"></a>7.2 需要 Microsoft Silverlight 5  
若要在主資料管理員 Web 應用程式中工作，用戶端電腦必須安裝 Silverlight 5.0。 如果您沒有必要的 Silverlight 版本，系統將會在您導覽至需要 Silverlight 的 Web 應用程式區域時提示安裝 Silverlight。 您可以從 [http://go.microsoft.com/fwlink/?LinkId=243096](http://go.microsoft.com/fwlink/?LinkId=243096)安裝 Silverlight 5。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="RS"></a>8.0 Reporting Services  
  
### <a name="81-reporting-services-connectivity-to-sql-server-pdw-requires-updated-drivers"></a>8.1 Reporting Services 與 SQL Server PDW 的連接需要更新的驅動程式  
從 SQL Server 2012 Reporting Services 連接到 Microsoft SQL Server PDW Appliance Update 2 及更新的版本需要 PDW 連接驅動程式的更新。 如需詳細資訊，SQL Server PDW 客戶應該連絡 Microsoft 支援人員。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="SI"></a>9.0 StreamInsight  
SQL Server 2012 包括 StreamInsight 2.0。 StreamInsight 2.0 需要 Microsoft SQL Server 2012 授權和 .NET Framework 4.0。 其中包含許多效能改良和幾個錯誤修正。 如需詳細資訊，請參閱 [Microsoft StreamInsight 2.0 版本資訊](http://social.technet.microsoft.com/wiki/contents/articles/6539.aspx)。 若要個別下載 StreamInsight 2.0，請瀏覽 Microsoft 下載中心的 [Microsoft StreamInsight 2.0 下載頁面](http://go.microsoft.com/fwlink/?LinkId=241593) 。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  
## <a name="UA"></a>10.0 Upgrade Advisor  
  
### <a name="101-link-to-install-upgrade-advisor-is-not-enabled-on-chinese-hk-operating-systems"></a>10.1 在中文 (HK) 作業系統上並未啟用安裝 Upgrade Advisor 的連結  
問題：當您嘗試在任何支援的中文 (香港) 作業系統 (OS) Windows 版本上安裝 Upgrade Advisor 時，可能會發現安裝 Upgrade Advisor 的連結並未啟用。  
  
**因應措施**：根據您的作業系統架構，在 SQL Server 2012 媒體上的下列位置找出 **SQLUA.msi** 檔案： `\1028_CHT_LP\x64\redist\Upgrade Advisor` 或 `\1028_CHT_LP\x86\redist\Upgrade Advisor`。  
  
![horizontal_bar](../release-notes/media/horizontal-bar.png "horizontal_bar")  
  

