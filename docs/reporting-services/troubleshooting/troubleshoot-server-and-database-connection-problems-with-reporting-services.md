---
title: "伺服器與 Reporting Services 的資料庫連線問題疑難排解 |Microsoft 文件"
ms.custom: 
ms.date: 02/28/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8bbb88df-72fd-4c27-91b7-b255afedd345
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1b901ec323ee3aa021d9e581cb8a1aedbde3116b
ms.contentlocale: zh-tw
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-server-and-database-connection-problems-with-reporting-services"></a>伺服器與 Reporting Services 的資料庫連線問題疑難排解
使用此主題，即可對在連接到報表伺服器時遇到的問題進行疑難排解。 此主題也提供有關「意外的錯誤」訊息的資訊。 如需資料來源組態和設定報表伺服器連接的詳細資訊，請參閱 [指定報表資料來源的認證和連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) 和 [設定報表伺服器資料庫連接 (SSRS 組態管理員)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="cannot-create-a-connection-to-data-source-datasourcename-rserroropeningconnection"></a>無法與資料來源 'datasourcename' 建立連接。 (rsErrorOpeningConnection)  
這是一般錯誤，當報表伺服器無法開啟提供報表資料的外部資料來源時，就會發生此錯誤。 這個錯誤會和另一則指出根本原因的錯誤訊息一起顯示。 **rsErrorOpeningConnection**可能會和下列其他錯誤一起顯示。  
  
### <a name="login-failed-for-user-username"></a>使用者 'UserName' 的登入失敗  
使用者沒有存取資料來源的權限。 若您使用 SQL Server 資料庫，請驗證使用者擁有有效的資料庫使用者登入。 如需如何建立資料庫使用者或 SQL Server 登入的詳細資訊，請參閱 [建立資料庫使用者](../../relational-databases/security/authentication-access/create-a-database-user.md) 和 [建立 SQL Server 登入](../../relational-databases/security/authentication-access/create-a-login.md)。  
  
### <a name="login-failed-for-user-nt-authorityanonymous-logon"></a>使用者 'NT AUTHORITY\ANONYMOUS LOGON' 的登入失敗  
傳遞認證跨越多部電腦的連接時，會發生此錯誤。 如果您是使用 Windows 驗證，而且未啟用 Kerberos 版本 5 通訊協定，則在認證傳遞跨越一個以上的電腦連接時，就會發生此錯誤。 若要解決此錯誤，請考慮使用預存認證或提示認證。 如需如何解決這個問題的詳細資訊，請參閱 [指定報表資料來源的認證和連接資訊](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)。  
  
### <a name="an-error-has-occurred-while-establishing-a-connection-to-the-server"></a>建立伺服器的連接時發生錯誤。  
連接到 SQL Server 時，可能因為在預設的設定下 SQL Server 不允許遠端連接而引起此失敗。 (提供者：具名管道提供者，錯誤：40 - 無法開啟 SQL Server 的連接)。 這項錯誤是由主控報表伺服器資料庫的 Database Engine 執行個體所傳回。 在大部分情況下，發生這項錯誤的原因是 SQL Server 服務已停止。 或者，若您正在使用 SQL Server Express with Advanced Services 或具名執行個體，當報表伺服器 URL 或報表伺服器資料庫的連接字串不正確時，就會發生這項錯誤。 若要解決這些問題，請進行下列動作：  
  
* 驗證 SQL Server (**MSSQLSERVER**) 服務已啟動。 在主控 Database Engine 執行個體的電腦上，依序按一下 [開始]、[系統管理工具] 和 [服務]，然後捲動至 [SQL Server (**MSSQLSERVER)**]。 若這項服務未啟動，請在此服務上按一下滑鼠右鍵，選取 [內容]，在 [啟動類型] 中選取 [自動]，然後依序按一下 [套用]、[啟動] 和 [確定]。   
* 確認報表伺服器 URL 和報表伺服器資料庫的連接字串正確無誤。 若 Reporting Services 或 Database Engine 已安裝成具名執行個體，在安裝期間建立的預設連接字串將會包含執行個體名稱。 例如，若您在名為 DEVSRV01 的伺服器上安裝了 SQL Server Express with Advanced Services 的預設執行個體，報表管理員 URL 就是 DEVSRV01\Reports$SQLEXPRESS。 此外，連接字串中的資料庫伺服器名稱將類似於 DEVSRV01\SQLEXPRESS。 如需 SQL Server Express 的 URL 和資料來源連接字串的相關資訊，請參閱 [SQL Server Express with Advanced Services 中的 Reporting Services](http://technet.microsoft.com/library/ms365166(v=sql.105).aspx)。 若要驗證報表伺服器資料庫的連接字串，請啟動 Reporting Services 組態工具，然後檢視 [資料庫安裝] 頁面。  
  
### <a name="a-connection-cannot-be-made-ensure-that-the-server-is-running"></a>無法建立連接。 請確定該伺服器正在執行。  
這是 ADOMD.NET 提供者傳回的錯誤。 發生這個錯誤的可能原因有幾個。 如果您已將伺服器指定為 "localhost"，請試著指定伺服器名稱來取代。 如果無法將記憶體配置給新連接，也會發生此錯誤。 如需詳細資訊，請參閱 [Knowledge Base Article 912017 - Error message when you connect to an instance of SQL Server 2005 Analysis Services:](http://support.microsoft.com/kb/912017)(知識庫文章 912017 - 當您連接到 SQL Server 2005 Analysis Services 的執行個體時的錯誤訊息︰)。  
  
若錯誤訊息也包含「無法識別這部主機」，則表示 Analysis Services 伺服器無法使用或拒絕連接。 若您將 Analysis Services 伺服器安裝成遠端電腦上的具名執行個體，您可能必須執行 SQL Server Browser 服務，以便取得該執行個體所使用的連接埠號碼。  
  
### <a name="report-services-soap-proxy-source"></a>(報表服務 SOAP Proxy 來源)  
如果您在報表模型產生期間發現此錯誤，且其他資訊區段包含「SQL Server 不存在或拒絕存取」，表示您可能遇到下列狀況：  
* 資料來源的連接字串包含 "localhost"。  
* 已停用 SQL Server 服務的 TCP/IP。  
  
若要解決此錯誤，您可以修改連接字串來使用伺服器名稱，或者，您也可以啟用該服務的 TCP/IP。 請依照下列步驟啟用 TCP/IP：  
  
1. 啟動 SQL Server 組態管理員。  
2. 展開 [SQL Server 網路組態] 。  
3. 選取 [MSSQLSERVER 的通訊協定] 。  
4. 在 [TCP/IP] 上按一下滑鼠右鍵，然後選取 [啟用] 。  
5. 選取 [SQL Server 服務] 。  
6. 在 [SQL Server (MSSQLSERVER)] 上按一下滑鼠右鍵，然後選取 [重新啟動] 。  
  
## <a name="wmi-error-when-connecting-to-a-report-server-in-management-studio"></a>在 Management Studio 中連接至報表伺服器時發生 WMI 錯誤  
根據預設，Management Studio 會使用 Reporting Services Windows Management Instrumentation (WMI) 提供者來建立報表伺服器的連接。 如果未正確安裝 WMI 提供者，當您嘗試連接至報表伺服器時，將會收到下列錯誤：  
  
無法連線到\<您的伺服器名稱 >。 未安裝報表服務 Reporting Services WMI 提供者，或設定錯誤 (Microsoft.SqlServer.Management.UI.RSClient)。  
  
若要解決這個錯誤，您應該重新安裝此軟體。 除此之外，您可以透過 SOAP 端點連接至報表伺服器，當做暫時的解決方法：  
  
* 在 Management Studio 的 [連接到伺服器]  對話方塊中，於 [伺服器名稱] 內輸入報表伺服器 URL。 依預設，此為 `http://<your server name>/reportserver`。 或者若您正在使用 SQL Server 2008 Express with Advanced Services，則為 `http://<your server name>/reportserver$sqlexpress`。  
  
若要解決此錯誤，以便使用 WMI 提供者進行連接，您應該執行安裝程式來修復 Reporting Services 或加以重新安裝。  
  
## <a name="connection-error-where-login-failed-due-to-unknown-user-name-or-bad-password"></a>連接錯誤，由於未知的使用者名稱或密碼錯誤而登入失敗  
若您是使用網域帳戶從報表伺服器連接到報表伺服器資料庫，而網域帳戶的密碼已經變更，就會發生 **rsReportServerDatabaseLogonFailed** 錯誤。   
  
錯誤文字全文為：「報表伺服器無法開啟到報表伺服器資料庫的連接。 登入失敗 (**rsReportServerDatabaseLogonFailed**)。 登入失敗: 未知的使用者名稱或密碼錯誤」。  
  
如果您重設密碼，則必須更新連接。 如需詳細資訊，請參閱 [設定報表伺服器資料庫連接 (SSRS 組態管理員)](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md)。  
  
## <a name="the-report-server-cannot-open-a-connection-to-the-report-server-database-rsreportserverdatabaseunavailable"></a>報表伺服器無法開啟到報表伺服器資料庫的連接。 (rsReportServerDatabaseUnavailable)。  
完整訊息：報表伺服器無法開啟報表伺服器資料庫的連接。 所有要求和處理都需要與資料庫連接。 (rsReportServerDatabaseUnavailable)  
當報表伺服器無法連接到為伺服器提供內部儲存區的 SQL Server 關聯式資料庫時，就會發生此錯誤。 報表伺服器資料庫的連接是透過 Reporting Services 組態工具所管理。 您可以執行此工具，移到 [資料庫安裝] 頁面，並更正連接資訊。 使用工具更新連接資訊是最好的作法，因為這項工具一定會更新相依設定，並重新啟動服務。 如需詳細資訊，請參閱 [設定報表伺服器資料庫連接](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md) 和 [設定報表伺服器服務帳戶](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)。  
  
若主控報表伺服器資料庫的 Database Engine 執行個體沒有設定遠端連接，也會發生此錯誤。 在某些 SQL Server 版本中，預設會啟用遠端連接。 若要驗證它是否在您使用的 SQL Server Database Engine 執行個體上啟用，請執行 SQL Server 組態管理員工具。 您必須同時啟用 TCP/IP 和具名管道。 報表伺服器會同時使用這兩種通訊協定。 如需有關如何啟用遠端連接的指示，請參閱 [設定報表伺服器來進行遠端管理](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)中的＜如何設定與報表伺服器資料庫的遠端連接＞一節。  
  
若錯誤中另外還包含下列文字，則表示用來執行 Database Engine 執行個體的帳戶其密碼已經過期：「建立伺服器的連線時發生錯誤。 連接到 SQL Server 時，可能因為在預設的設定下 SQL Server 不允許遠端連接而引起此失敗。 (**提供者：SQL Server 網路介面，錯誤：26 - 尋找指定的伺服器/執行個體時發生錯誤)**。」 若要解決此錯誤，請重新設定密碼。   
  
## <a name="rpc-server-is-not-listening"></a>「RPC 伺服器不在聽候」  
報表伺服器服務會使用遠端程序呼叫 (RPC) 伺服器執行某些作業。 如果您收到「RPC 伺服器不在聽候」錯誤，請確認報表伺服器服務正在執行。  
  
## <a name="unexpected-error-general-network-error"></a>意外的錯誤 (一般網路錯誤)  
此錯誤表示資料來源連接錯誤。 您應該檢查連接字串，並確認是否有存取資料來源的權限。 如果您是使用 Windows 驗證來存取資料來源，就必須有存取主控資料來源之電腦的權限。  
  
## <a name="unable-to-grant-database-access-in-sharepoint-central-administration"></a>無法在 SharePoint 管理中心內授與資料庫存取權  
當您已經將 Reporting Services 設定成與 Windows Vista 或 Windows Server 2008 上的 SharePoint 產品或技術整合時，若您嘗試在 SharePoint 管理中心的 [授與資料庫存取權]  頁面上授與存取權，可能會收到下列錯誤訊息：「無法建立與電腦的連接」。  
  
發生這項錯誤的原因是在執行需要管理員權限的工作時，Windows Vista 和 Windows Server 2008 中的使用者帳戶控制 (UAC) 需要管理員的明確接受，才能提高和使用管理員 Token。 不過，在此情況中，無法提高 Windows SharePoint Services 管理服務，因此無法將 SharePoint 組態和內容資料庫的存取權授與 Reporting Services 服務帳戶。  
  
在 SQL Server 2008 Reporting Services 中，只有報表伺服器服務帳戶需要資料庫存取權。在 SQL Server 2005 Reporting Services SP2 中，報表伺服器 Windows 服務帳戶和報表伺服器 Web 服務帳戶都需要資料庫存取權。 如需 SQL Server 2008 中報表伺服器服務帳戶的詳細資訊，請參閱服務帳戶 (Reporting Services 組態)。  
  
這個問題有兩種解決方法。   
1.  在第一種解決方法中，您可以暫時關閉 UAC，然後使用 SharePoint 管理中心來授與存取權。  
> [!IMPORTANT]  
> 如果您關閉 UAC 來解決這個問題，請特別小心，而且請務必在 SharePoint 管理中心內授與資料庫存取權之後立即開啟 UAC。 如果您不想要關閉 UAC，請使用本節提供的第二種解決方法。 如需有關 UAC 的詳細資訊，請參閱 Windows 產品文件集。  
2. 在第二種解決方法中，您可以手動將資料庫存取權授與 Reporting Services 服務帳戶。 您可以透過將 Reporting Services 服務帳戶加入正確的 Windows 群組和資料庫角色中，以使用下列程序來授與存取權。 此程序適用於 SQL Server 2008 Reporting Services 中的報表伺服器服務帳戶。若您正在執行 SQL Server 2005 Reporting Services，請針對報表伺服器 Windows 服務帳戶和報表伺服器 Web 服務帳戶執行此程序。   
  
### <a name="to-manually-grant-database-access"></a>手動授與資料庫存取權  
  
1. 將報表伺服器服務帳戶加入 Reporting Services 電腦上的 WSS_WPG Windows 群組中。  
2. 連接至主控 SharePoint 組態和內容資料庫的資料庫執行個體，然後建立報表伺服器服務帳戶的 SQL 資料庫登入。  
3. 將 SQL 資料庫登入加入至下列資料庫角色：  
  
* WSS 內容資料庫中的 db_owner 角色  
* SharePoint_Config 資料庫中的 WSS_Content_Application_Pools 角色  
  
## <a name="unable-to-connect-to-the-reports-and-reportserver-directories-when-the-report-server-databases-are-created-on-a-virtual-sql-server-that-runs-in-a-microsoft-cluster-services-mscs-cluster"></a>當報表伺服器資料庫是在執行於 Microsoft Cluster Services (MSCS) 叢集中的虛擬 SQL Server 上建立時，無法連接至 /reports 和 /reportserver 目錄  
當您在執行於 MSCS 叢集中的虛擬 SQL Server 上建立報表伺服器資料庫 **ReportServer** 和 **ReportServerTempDB**時，採用 `<domain>\<computer_name>$` 格式的遠端名稱可能無法向 SQL Server 註冊成登入。 若您已經將報表伺服器服務帳戶設定成需要這個遠端名稱進行連接的帳戶，使用者就無法連接至 Reporting Services 中的 /reports 和 /reportserver 目錄。 例如，內建的 Windows 帳戶 NetworkService 就需要這個遠端名稱。 若要避免這個問題發生，請使用明確網域帳戶或 SQL Server 登入來連接至報表伺服器資料庫。  
    
  ## <a name="see-also"></a>請參閱＜  
[Reporting Services 和 Power View 的瀏覽器支援](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[錯誤和事件 (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[搭配 Reporting Services 報表為資料擷取問題疑難排解](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[為 Reporting Services 訂閱與傳遞疑難排解](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect.md)]


