---
title: "針對 Web 同步處理設定 IIS | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IIS server configuration [SQL Server replication]
- websync.log
- Web synchronization, IIS servers
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
caps.latest.revision: 88
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 5ac612d72c1a82d49a7cfcf41aa9aa2989ee25b2
ms.lasthandoff: 04/11/2017

---
# <a name="configure-iis-for-web-synchronization"></a>針對 Web 同步處理設定 IIS
  本主題中的程序，會構成設定合併式複寫之 Web 同步處理時所採取的第二個步驟。 請在啟用 Web 同步處理的發行集之後執行這個步驟。 如需組態處理序的概觀，請參閱＜ [[設定 Web 同步處理]](../../relational-databases/replication/configure-web-synchronization.md)＞。 完成本主題中的程序之後，請繼續執行第三個步驟，即設定訂閱來使用 Web 同步處理。 第三個步驟在下列主題中描述：  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [How to: Configure a Subscription to Use Web Synchronization \(SQL Server Management Studio\)](http://msdn.microsoft.com/library/ms345214.aspx)  
  
-   複寫 [!INCLUDE[tsql](../../includes/tsql-md.md)] 程式設計： [如何：將訂閱設定為使用 Web 同步處理 (複寫 Transact-SQL 程式設計)](http://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO： [如何：設定訂閱使用 Web 同步處理 (RMO 程式設計)](http://msdn.microsoft.com/library/ms345207.aspx)  
  
 Web 同步處理利用執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 的電腦，來同步處理合併式發行集的提取訂閱。 支援 IIS 5.0 版、IIS 6.0 版和 [!INCLUDE[iisver](../../includes/iisver-md.md)] 。 [!INCLUDE[iisver](../../includes/iisver-md.md)]不支援設定 Web 同步處理精靈。  
  
> [!IMPORTANT]  
>  確定您的應用程式只使用 [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] 或更新版本，而且 IIS 伺服器上未安裝較早版本的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 。 較早版本的 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 可能導致錯誤。 其中包括下列項目：「Web 同步處理期間，訊息的格式無效。 請確認已在 Web 伺服器正確地設定複寫元件」。  
  
> [!CAUTION]  
>  請勿同時使用 WebSync 和替代快照集資料夾位置。  
  
 若要使用 Web 同步處理，您必須完成下列步驟來設定 IIS。 本主題中有每個步驟的詳細描述。  
  
1.  設定安全通訊端層 (SSL)。 IIS 與所有訂閱者之間的通訊需要 SSL。  
  
2.  您可以利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈，將 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 連接元件安裝在執行 IIS 的電腦上。 如果您打算使用步驟 3 提到的「設定 Web 同步處理精靈」，您也必須將 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 安裝在執行 IIS 的電腦上。  
  
3.  設定執行 IIS 的電腦來進行 Web 同步處理。 您可以手動設定電腦，或使用「設定 Web 同步處理精靈」。 我們建議您使用精靈。  
  
    > [!NOTE]  
    >  如果執行 IIS 的電腦在 Windows 的 64 位元版本上執行，您必須執行下列命令，確定該伺服器已正確設定，才可執行 Internet Server API (ISAPI) 應用程式。 如需詳細資訊，請參閱 IIS 文件集。  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  為 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener 設定適當的權限。  
  
5.  在診斷模式下執行 Web 同步處理，以測試執行 IIS 的電腦連接，並確定 SSL 憑證已正確安裝。  
  
## <a name="configuring-secure-sockets-layer"></a>設定安全通訊端層  
 若要設定 SSL，請為所要使用之執行 IIS 的電腦指定一個憑證。 合併式複寫的 Web 同步處理支援使用伺服器憑證，但不支援用戶端憑證。 若要設定 IIS 以進行部署，必須先從憑證授權中心 (CA) 獲得憑證。 憑證授權單位是負責建立及保證屬於使用者、電腦或其他憑證授權中心之公開加密金鑰真實性的實體。 如需有關憑證的詳細資訊，請參閱 IIS 文件集。 在您安裝憑證之後，必須將憑證與 Web 同步處理所使用的網站相關聯。  
  
#### <a name="to-specify-a-certificate-for-deployment"></a>若要指定部署憑證  
  
1.  以管理員身分登入執行 IIS 的電腦。  
  
2.  啟動 **[Internet Information Services (IIS) 管理員]**：  
  
    1.  按一下 **[開始]**，然後按一下 **[執行]**。  
  
    2.  在 **[開啟]** 方塊中，輸入 **inetmgr**，然後按一下 **[確定]**。  
  
3.  執行 IIS 憑證精靈：  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**中，展開 **[本機電腦]** 節點，然後展開 **[網站]** 資料夾。  
  
    2.  以滑鼠右鍵按一下 **[預設網站]**，然後按一下 **[屬性]**。  
  
    3.  在 **[預設網站屬性]** 對話方塊的 **[目錄安全性]** 索引標籤中，按一下 **[伺服器憑證]**。  
  
    4.  完成「Web 伺服器憑證精靈」。  
  
4.  按一下 **[確定]**。  
  
 如果您無法從 CA 取得伺服器憑證，您可以指定憑證來進行測試。 若要設定 IIS 6.0 來進行測試，請利用 SelfSSL 公用程式來安裝憑證。 IIS 6.0 資源套件中有提供此公用程式。 您可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=30958)下載這些工具。 如需 IIS 5.0，請移至 [Microsoft 說明及支援](http://go.microsoft.com/fwlink/?LinkId=46229)。  
  
> [!NOTE]  
>  憑證必須先與網站相關聯，該網站才能夠使用 SSL。 SelfSSL 會自動將憑證與預設網站相關聯。 如果您已擁有憑證或稍後從 CA 安裝憑證，則必須明確地將憑證與 Web 同步處理所使用的網站相關聯。 請確定只有一個與用於同步處理訂閱之網站相關聯的憑證。 如果有多個憑證，訂閱者將使用第一個可用的網站。  
  
#### <a name="to-specify-a-certificate-for-testing-in-iis-60"></a>若要指定憑證以在 IIS 6.0 中進行測試  
  
1.  以管理員身分登入執行 IIS 的電腦。  
  
2.  下載並安裝 SelfSSL。 依預設，應用程式會安裝到 \<*磁碟機*>:\Program Files\IIS Resources\SelfSSL。 應用程式與文件集快速鍵會複製到 \<*磁碟機*>:\Documents and Settings\All Users\Start Menu\Programs\IIS Resources\SelfSSL。  
  
3.  執行 SelfSSL：  
  
    -   若要利用所有參數的預設值來執行 SelfSSL，請找出應用程式的安裝目錄，然後按兩下 SelfSSL.exe。  
  
        > [!NOTE]  
        >  依預設，SelfSSL 安裝的憑證在七天內有效。  
  
    -   若要指定一或多個參數值：請按一下 **[開始]**，然後按一下 **[執行]**。 在 [開啟]  方塊中，輸入 **cmd**，然後按一下 [確定] 。 找出 SelfSSL 安裝目錄，輸入 `SelfSSL`，然後指定一或多個參數的值。 如需參數列表，請輸入 `SelfSSL -?`。  
  
## <a name="installing-connectivity-components-and-sql-server-management-studio"></a>安裝連接元件和 SQL Server Management Studio  
  
#### <a name="to-install-sql-server-connectivity-components-and-sql-server-management-studio"></a>若要安裝 SQL Server 連接元件和 SQL Server Management Studio  
  
1.  以管理員身分登入執行 IIS 的電腦。  
  
2.  從 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 安裝磁碟，啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安裝精靈。 如需如何使用此精靈的詳細資訊，請參閱[從安裝精靈安裝 SQL Server 2016 &#40;安裝程式&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)。  
  
3.  在 **[特徵選取]** 頁面中，選取 **[用戶端工具連接性]**。  
  
4.  如果您打算使用 [設定 Web 同步處理精靈]，請選取 **[管理工具 - 基本]**。  
  
5.  完成精靈，然後重新啟動電腦。  
  
    > [!NOTE]  
    >  您可以安裝其他元件，但 Web 同步處理只需要連接元件。  
  
## <a name="configuring-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>利用「設定 Web 同步處理精靈」來設定執行 IIS 的電腦  
 利用「設定 Web 同步處理精靈」或以手動方式來設定 IIS 伺服器。 我們建議您使用精靈，不過，在下一節中，我們也提供手動組態的步驟。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 所提供的「Web 同步處理精靈」只能用於在執行 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之發行者或升級為 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]之發行者上建立的發行集。 此精靈無法用於 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]的發行集。 此精靈可搭配 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 和更新版本以及 [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 和更新版本的訂閱使用。  
  
 這個組態具有下列特性：  
  
-   在 IIS 中使用預設網站。 不過，您也可以使用其他網站。 如需有關如何建立網站的詳細資訊，請參閱 IIS 文件集。  
  
    > [!NOTE]  
    >  您指定的網站提供 Web 同步處理所使用之元件的存取權。 網站不提供其他資料或網頁的存取權，除非您將網站設定為必須提供。  
  
-   建立虛擬目錄及其相關聯的別名。 別名在存取 Web 同步處理元件時使用。 例如，如果 IIS 位址為 https://*server.domain.com* ，且您指定別名 'websync1'，則存取 replisapi.dll 元件的位址便為 https://*server.domain.com*/websync1/replisapi.dll。  
  
-   使用基本驗證。 我們建議您使用基本驗證，因為，基本驗證可讓您在不同的電腦上執行 IIS 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者/散發者 (建議的組態)，而不需要 Kerberos 委派。 搭配基本驗證使用 SSL，可以確保登入、密碼及所有資料在傳輸中時都會加密。 (不論採用哪一種驗證類型，都需要 SSL。)如需 Web 同步處理的最佳作法詳細資訊，請參閱[設定 Web 同步處理](../../relational-databases/replication/configure-web-synchronization.md)中的＜Web 同步處理安全性最佳作法＞一節。  
  
#### <a name="to-configure-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>若要利用「設定 Web 同步處理精靈」來設定執行 IIS 的電腦  
  
1.  在執行 IIS 的電腦上啟動 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
2.  連接到發行者，然後展開伺服器節點。  
  
3.  展開 **[本機發行集]** 資料夾，以滑鼠右鍵按一下發行集，然後按一下 **[設定 Web 同步處理]**。  
  
4.  在「設定 Web 同步處理精靈」的 **[訂閱者類型]** 頁面中，選取 **[SQL Server]**。  
  
5.  在 **[Web 伺服器]** 頁面中：  
  
    1.  選取將同步處理訂閱的 IIS 執行個體。  
  
    2.  選取 **[建立新的虛擬目錄]**。  
  
    3.  在頁面的下方窗格中，依序展開 IIS 執行個體和 **[網站]**，然後按一下 **[預設網站]**。  
  
6.  在 **[虛擬目錄資訊]** 頁面中：  
  
    1.  在 **[別名]** 方塊中輸入虛擬目錄的別名。  
  
    2.  在 **[路徑]** 方塊中輸入虛擬目錄的路徑。 例如，如果您在 [別名]  方塊中輸入 **websync1** ，請在 [路徑]  方塊中輸入 **C:\Inetpub\wwwroot\websync1** 。 按一下 **[下一步]**。  
  
    3.  在兩個對話方塊中，按一下 **[是]**。 這會指定您要建立新資料夾，並指定您要複製 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Internet Server API (ISAPI) DLL。 ＞。  
  
7.  在 **[驗證的存取]** 頁面中：  
  
    1.  確定清除了 **[整合式 Windows 驗證]** 和 **[Windows 網域伺服器的摘要式驗證]** 。  
  
    2.  選取 **[基本驗證]**。  
  
    3.  在 **[預設網域]** 和 **[範圍]** 方塊中，輸入執行 IIS 之電腦的網域。  
  
8.  在 **[目錄存取]** 頁面中：  
  
    1.  按一下 **[加入]**，然後在 **[選取使用者或群組]** 對話方塊中，新增訂閱者將用於連接 IIS 的帳戶。 您可以在 [新增訂閱精靈] 的 [Web 伺服器資訊] 頁面中指定這些帳戶，或者將其指定為 [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)*@internet_login* 參數的值。  
  
9. 在 **[快照集共用存取]** 頁面中，輸入快照集共用。 在此共用上設定適當的權限，以便訂閱者可以存取快照集檔案。 如需共用權限的詳細資訊，請參閱[保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
10. 在 **[正在完成精靈]** 頁面中，按一下 **[完成]**。  
  
     如果出現失敗，例如在嘗試設定執行 IIS 的遠端電腦時出現網路錯誤，則會回復所有完成的動作並取消所有剩餘動作。 如果已完成的動作無法回復，精靈最終頁面中的狀態將顯示 **[成功]** ，並仍然認可完成的動作。  
  
11. 如果執行 IIS 的電腦執行於 64 位元版本的 Windows 上，則必須將 replisapi.dll 複製到適當的目錄：  
  
    1.  按一下 **[開始]**，然後按一下 **[執行]**。 在 [開啟]  方塊中，輸入 **iisreset**，然後按一下 [確定] 。  
  
    2.  停止並重新啟動 IIS 之後，請將 replisapi.dll 從 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\replisapi 複製到步驟 6b 中指定的目錄。  
  
    3.  按一下 **[開始]**，然後按一下 **[執行]**。 在 [開啟]  方塊中，輸入 **cmd**，然後按一下 [確定] 。  
  
    4.  於您在步驟 6b 中指定的目錄中，執行下列命令：  
  
         **regsvr32 replisapi.dll**  
  
## <a name="manually-configuring-the-computer-that-is-running-iis"></a>手動設定執行 IIS 的電腦  
 若要手動設定執行 IIS 的電腦，您必須安裝及設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener，然後為要連接 IIS 的訂閱者設定授權。  
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>若要安裝和設定 SQL Server Replication Listener  
  
1.  在執行 IIS 的電腦上建立檔案目錄來容納 replisapi.dll。 您可以在任何位置建立該目錄，不過，建議您在 \<*磁碟機*>:\Inetpub 目錄底下建立該目錄。 例如，您可以建立 \<*磁碟機*>:\Inetpub\SQLReplication\\ 目錄。  
  
    > [!IMPORTANT]  
    >  強烈建議您在 NTFS 檔案系統資料分割 (而非 FAT 檔案系統) 上建立此目錄。 使用 NTFS 檔案系統時，可使用 NTFS 檔案系統權限，來準確控制可存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫的使用者。  
  
2.  將 replisapi.dll 從目錄 [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ 複製到步驟 1 中建立的檔案目錄。  
  
3.  註冊 replisapi.dll：  
  
    1.  按一下 **[開始]**，然後按一下 **[執行]**。 在 [開啟]  方塊中，輸入 **cmd**，然後按一下 [確定] 。  
  
    2.  於您在步驟 1 中建立的目錄中，執行下列命令：  
  
         **regsvr32 replisapi.dll**  
  
4.  為複寫建立新網站，或使用現有的站台。 網站在同步處理期間可由複寫元件存取。 如需有關如何建立網站的詳細資訊，請參閱 IIS 文件集。  
  
5.  在 IIS 中建立虛擬目錄。 虛擬目錄應該在步驟 4 所建立的網站之下建立，且應該對應至步驟 1 所建立的目錄。 如需有關如何建立虛擬目錄的詳細資訊，請參閱 IIS 文件集。 我們建議您在指派權限給此目錄時愈嚴格愈好。 您必須選取 **讀取** 和 **執行** 權限，但是可以清除 **執行指令碼**、 **寫入**和 **瀏覽** 權限。  
  
6.  設定 IIS，使 replisapi.dll 能夠執行。 步驟 4 中指派的權限對於舊版 IIS 而言已經足夠；不過，IIS 6.0 版要求啟用 Internet Server API (ISAPI) 延伸模組。 如需詳細資訊，請參閱 IIS 6.0 文件集中的＜設定 ISAPI 延伸模組＞和＜啟用和停用動態內容＞。  
  
#### <a name="to-configure-iis-authentication"></a>若要設定 IIS 驗證  
  
-   當訂閱者連接到 IIS 時，訂閱者必須經過 IIS 驗證才能存取資源和處理序。 IIS 提供三種類型的驗證：匿名、基本和整合式。 驗證可套用至整個網站或您建立的虛擬目錄。  
  
     我們建議您搭配 SSL 使用基本驗證。 不論採用哪一種驗證類型，都需要 SSL。 如需有關如何設定驗證的詳細資訊，請參閱 IIS 文件集。  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>設定 SQL Server Replication Listener 的權限  
 當訂閱者連接到執行 IIS 的電腦時，系統會利用您先前設定 IIS 時所指定的驗證類型來驗證訂閱者。 IIS 驗證訂閱者之後，IIS 會檢查訂閱者是否獲授權叫用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。 您可藉由設定 replisapi.dll 的權限來控制可以叫用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫的使用者。 您必須適當地設定權限，才能避免未經授權的使用者存取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫。  
  
 若要設定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener 執行時所用帳戶的最小權限，請完成下列程序。 此程序中的步驟適用於執行 IIS 6.0 的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 。  
  
 除了執行下列步驟之外，請確保所需的登入位於發行集存取清單 (PAL) 中。 如需 PAL 的詳細資訊，請參閱[保護發行者](../../relational-databases/replication/security/secure-the-publisher.md)。  
  
#### <a name="to-configure-the-account-and-permissions"></a>若要設定帳戶和權限  
  
1.  在執行 IIS 的電腦上建立本機帳戶：  
  
    1.  以滑鼠右鍵按一下 **[我的電腦]**，然後按一下 **[管理]**。  
  
    2.  在 **[電腦管理]**中，展開 **[本機使用者和群組]**。  
  
    3.  以滑鼠右鍵按一下 **[使用者]**，然後按一下 **[新增使用者]**。  
  
    4.  輸入使用者名稱與增強式密碼。  
  
    5.  按一下 **[建立]**，然後按一下 **[關閉]**。  
  
2.  將帳戶加入 IIS_WPG 群組：  
  
    1.  在 **[電腦管理]**中展開 **[本機使用者和群組]**，然後按一下 **[群組]**。  
  
    2.  以滑鼠右鍵按一下 **[IIS_WPG]**，然後按一下 **[加入群組]**。  
  
    3.  在 **[IIS_WPG 屬性]** 對話方塊中，按一下 **[加入]**。  
  
    4.  在 **[選取使用者、電腦或群組]** 對話方塊中，加入在步驟 1 建立的帳戶。  
  
    5.  確定 **[從這個位置]** 欄位中的名稱是本機電腦的名稱，而不是網域。 如果該名稱不是本機電腦，請按一下 **[位置]**。 在 **[位置]** 對話方塊中，選取本機電腦，然後按一下 **[確定]**。  
  
    6.  在 **[選取使用者]** 對話方塊和 **[IIS_WPG 屬性]** 對話方塊中，按一下 **[確定]**。  
  
3.  將包含 replisapi.dll 之資料夾的最小權限授與帳戶：  
  
    1.  找出您先前為 replisapi.dll 建立的資料夾，以滑鼠右鍵按一下該資料夾，然後按一下 **[共用和安全性]**。  
  
    2.  在 **[安全性]** 索引標籤上，按一下 **[加入]**。  
  
    3.  在 **[選取使用者、電腦或群組]** 對話方塊中，加入在步驟 1 建立的帳戶。  
  
    4.  確定 **[從這個位置]** 欄位中的名稱是本機電腦的名稱，而不是網域。 如果該名稱不是本機電腦，請按一下 **[位置]**。 在 **[位置]** 對話方塊中，選取本機電腦，然後按一下 **[確定]**。  
  
    5.  確認只將**讀取**、**讀取與執行**和**列出資料夾內容**權限授與這個帳戶。  
  
    6.  選取不需要存取目錄的使用者或群組，然後按一下 **[移除]**。  
  
    7.  按一下 **[確定]**。  
  
4.  在 **[Internet Information Services (IIS) 管理員]**中建立應用程式集區：  
  
    1.  按一下 **[開始]**，然後按一下 **[執行]**。  
  
    2.  在 **[開啟]** 方塊中，輸入 **inetmgr**，然後按一下 **[確定]**。  
  
    3.  在 **[Internet Information Services (IIS) 管理員]**中，展開 **[本機電腦]** 節點。  
  
    4.  以滑鼠右鍵按一下 **[應用程式集區]**，指向 **[新增]** ，然後按一下 **[應用程式集區]**。  
  
    5.  在 **[應用程式集區身分識別]** 欄位中輸入集區的名稱，然後按一下 **[確定]**。  
  
5.  將帳戶與應用程式集區相關聯：  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**中展開 **[本機電腦]** 節點，然後展開 **[應用程式集區]**。  
  
    2.  以滑鼠右鍵按一下您先前建立的應用程式集區，然後按一下 **[屬性]**。  
  
    3.  在 [\<ApplicationPoolName> 屬性] 對話方塊中的 [識別] 索引標籤上，按一下 [可設定]。  
  
    4.  在 **[使用者名稱]** 和 **[密碼]** 欄位中，輸入步驟 1 中建立的帳戶和密碼。  
  
    5.  按一下 **[確定]**。  
  
6.  將應用程式集區與 Web 同步處理所使用的虛擬目錄相關聯：  
  
    1.  在 **[Internet Information Services (IIS) 管理員]**中展開 **[本機電腦]** 節點，然後展開 **[網站]**。  
  
    2.  展開您用於 Web 同步處理的網站，以滑鼠右鍵按一下您為 Web 同步處理建立的虛擬目錄，然後按一下 **[屬性]**。  
  
    3.  在 [\<VirtualDirectoryName> 屬性] 對話方塊的 [虛擬目錄] 索引標籤上，從 [應用程式集區] 下拉式清單選取步驟 5 中建立的應用程式集區。  
  
    4.  按一下 **[確定]**。  
  
## <a name="testing-the-connection-to-replisapidll"></a>測試與 replisapi.dll 的連接  
 在診斷模式下執行 Web 同步處理，以測試執行 IIS 之電腦的連接，並確定安全通訊端層 (SSL) 憑證已正確安裝。 若要在診斷模式下執行 Web 同步處理，您必須是執行 IIS 之電腦上的管理員。  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>若要測試與 replisapi.dll 的連接  
  
1.  確定訂閱者端的區域網路 (LAN) 設定正確：  
  
    1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer 的 **[工具]** 功能表中，按一下 **[網際網路選項]**。  
  
    2.  在 **[連接]** 索引標籤中，按一下 **[LAN 設定]**。  
  
    3.  如果 LAN 上未使用 Proxy 伺服器，請清除 **[自動偵測設定]** 與 **[在 LAN 中使用 Proxy 伺服器]**。  
  
    4.  如果使用 Proxy 伺服器，請選取 **[在 LAN 中使用 Proxy 伺服器]** 和 **[本機位址不使用 Proxy 伺服器]**。  
  
    5.  按一下 **[確定]**。  
  
2.  在訂閱者端的 Internet Explorer 中，將 `?diag` 附加至 replisapi.dll 的位址，以便在診斷模式下連接伺服器。 例如：https://server.domain.com/directory/replisapi.dll?diag。  
  
3.  如果 Windows 作業系統無法辨識您先前為 IIS 指定的憑證，則會出現 **[安全性警示]** 對話方塊。 發生此警示的可能是因為該憑證是測試憑證，或者該憑證是由 Windows 無法辨識的憑證授權單位 (CA) 所發行。  
  
    > [!NOTE]  
    >  如果未出現此對話方塊，請確定您要存取之伺服器的憑證已做為信任憑證加入訂閱者端的憑證存放區中。 如需有關匯入憑證的詳細資訊，請參閱 IIS 文件集。  
  
    1.  在 **[安全性警示]** 對話方塊中，按一下 **[檢視憑證]**。  
  
    2.  在 **[憑證]** 對話方塊的 **[一般]** 索引標籤上，按一下 **[安裝憑證]**。  
  
    3.  完成「憑證匯入精靈」，以接受預設值。  
  
    4.  在 **[安全性警告]** 對話方塊中，按一下 **[是]**。  
  
    5.  在「憑證匯入精靈」確認對話方塊中，按一下 **[確定]**。  
  
    6.  關閉 **[憑證]** 對話方塊。  
  
    7.  在 **[安全性警示]** 對話方塊中，按一下 **[是]**。  
  
    > [!NOTE]  
    >  將為使用者安裝憑證。 這項處理序必須針對將與 IIS 同步處理的每位使用者執行。  
  
4.  在 [連接到 \<伺服器名稱>] 對話方塊中，指定合併代理程式要用來連接 IIS 的登入和密碼。 也可以在「新增訂閱精靈」中指定這些認證。  
  
5.  在稱為 **[SQL Websync 診斷資訊]**的 Internet Explorer 視窗中，確認頁面中每個 **[狀態]** 資料行中的值都是 **[SUCCESS]**。  
  
6.  確定憑證已正確安裝於訂閱者端：  
  
    1.  關閉 Internet Explorer，然後再重新開啟。  
  
    2.  在診斷模式下連接到伺服器。 如果憑證已正確安裝，就不會出現 **[安全性警示]** 對話方塊。 如果出現此對話方塊，合併代理程式將在嘗試連接到執行 IIS 的電腦時失敗。 您必須確定要存取的伺服器憑證已做為信任憑證加入訂閱者端的憑證存放區中。 如需有關匯入憑證的詳細資訊，請參閱 IIS 文件集。  
  
## <a name="see-also"></a>另請參閱  
 [[設定 Web 同步處理]](../../relational-databases/replication/configure-web-synchronization.md)  
  
  
