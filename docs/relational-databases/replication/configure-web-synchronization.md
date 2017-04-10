---
title: "設定 Web 同步處理 | Microsoft Docs"
ms.custom: ""
ms.date: "01/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.SNAPSHARE.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.CLIENTAUTH.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.SUBTYPE.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.DIRACCESS.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.ANONACCESS.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1"
  - "SQL10.REP.CONFIGWEBSYNCWIZARD.AUTHACCESS.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.COMPLETEWIZ.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.VIRDIRINFO.F1"
  - "SQL13.REP.CONFIGWEBSYNCWIZARD.WEBSERV.F1"
helpviewer_keywords: 
  - "Web 同步處理, 安全性最佳作法"
  - "Web 同步處理, 設定"
ms.assetid: 21f8e4d4-cd07-4856-98f0-9c9890ebbc82
caps.latest.revision: 74
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 73
---
# 設定 Web 同步處理
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 合併式複寫的 Web 同步處理選項可讓您透過網際網路使用 HTTPS 通訊協定進行資料複寫。 若要使用 Web 同步處理，您必須先執行下列組態設定動作：  
  
1.  建立新的網域帳戶並對應 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登入。  
  
2.  將正在執行 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) 的電腦設定為同步處理訂閱。  
  
3.  將合併式發行集設定為允許 Web 同步處理。  
  
4.  將一個或多個訂閱設定為使用 Web 同步處理。  
  
> [!NOTE]  
>  如果您打算複寫大量資料，或使用大型資料類型，例如 **varchar （max)**, ，本主題中閱讀 「 複寫大量資料 」 一節。  
  
 為了順利設定 Web 同步處理，您必須決定如何設定安全性以符合特定需求和原則。 建議您最好先進行這些決定並建立必要的帳戶，然後再嘗試設定 IIS、發行集和訂閱。  
  
 為了簡潔起見，在下列程序中，我們將描述使用本機帳戶的簡化安全性組態。 這個簡化的組態適用於 IIS 與 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者和散發者在同一部電腦上執行的安裝，即使您比較可能會使用多伺服器拓撲進行實際執行安裝也一樣 (而且這是建議作法)。 在這些程序中，您可以用網域帳戶來取代本機帳戶。  
  
## 建立新的帳戶並對應 SQL Server 登入  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (replisapi.dll) 會透過模擬針對與複寫網站相關聯之應用程式集區指定的帳戶，連接至發行者。  
  
 使用的帳戶 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫接聽程式必須具有權限中所述 [合併代理程式安全性](../../relational-databases/replication/merge-agent-security.md), 下一節 「 連接到發行者或散發者 」。, 總而言之，此帳戶必須：  
  
-   是發行集存取清單 (PAL) 的成員。  
  
-   對應至與發行集資料庫中之使用者相關聯的登入。  
  
-   對應至與散發資料庫中之使用者相關聯的登入。  
  
-   擁有快照集共用的讀取權限。  
  
 如果這是您第一次使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 複寫，您也必須建立複寫代理程式的帳戶和登入。 如需詳細資訊，請參閱本主題中的＜設定發行集＞和＜設定訂閱＞章節。  
  
 在設定 Web 同步處理之前，我們建議您先閱讀本主題中的＜Web 同步處理安全性最佳作法＞一節。 如需有關 Web 同步處理安全性的詳細資訊，請參閱＜ [Security Architecture for Web Synchronization](../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)＞。  
  
## 設定正在執行 IIS 的電腦  
 Web 同步處理要求您安裝並設定 IIS。 您需要複寫網站的 URL，然後才能將發行集設定為使用 Web 同步處理。  
  
 IIS 5.0 版開始支援 web 同步處理。 但是，IIS 7.0 版不支援「設定 Web 同步處理精靈」。 我們建議使用者安裝 SQL Server 複寫與 SQL Server 2012、 IIS 伺服器上使用 web 同步處理元件開始。 這可以是免費的 SQL Server Express edition。  
  
 Web 同步處理需要使用 SSL。 您需要擁有憑證授權單位所核發的安全性憑證。 如果只是為了測試，您可以使用自行核發的安全性憑證。  
   
  
 **若要設定 Web 同步處理的 IIS**  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configure IIS for Web Synchronization](../../relational-databases/replication/configure-iis-for-web-synchronization.md)  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Configure IIS 7 for Web Synchronization](../../relational-databases/replication/configure-iis-7-for-web-synchronization.md)  
  
## 建立 Web 處理序區  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener 支援每個執行緒有兩個並行同步處理作業。 超過這個限制可能會導致 Replication Listener 停止回應。 配置給 replisapi.dll 的執行緒數目是由應用程式集區的 [工作者處理序數上限] 屬性所決定。 根據預設，這個屬性設定為 1。  
  
 您可以透過增加 [工作者處理序數上限] 屬性值，讓每個 CPU 支援較大的並行同步處理作業數目。 透過增加每個 CPU 的工作者處理序數目來進行向外延展的行為稱為建立「Web 處理序區」。  
  
 Web 處理序區會允許兩個以上的訂閱者同時訂閱。 此外，它也會增加 replisapi.dll 的 CPU 使用量，因此可能會對整體伺服器效能造成負面影響。 當您針對 [工作者處理序數上限] 選擇值時，請務必權衡這些考量。  
  
#### 若要在 IIS 7 中增加工作者處理序數上限  
  
1.  在 **網際網路資訊服務 (IIS) 管理員**, ，展開本機伺服器] 節點，然後按一下 [ **應用程式集區** 節點。  
  
2.  選取與 Web 同步處理網站相關聯的應用程式集區，然後按一下 **[動作]** 窗格上的 **[進階設定]** 。  
  
3.  在 [進階設定] 對話方塊的 **[處理序模型]** 標題底下，按一下標示為 **[工作者處理序數上限]**的列。 變更屬性值，然後按一下 **[確定]**。  
  
## 設定發行集  
 若要使用 Web 同步處理，請採用您建立標準合併拓撲的相同方式來建立發行集。 如需詳細資訊，請參閱 [發行資料和資料庫物件](../../relational-databases/replication/publish/publish-data-and-database-objects.md)。  
  
 在建立發行集之後，請啟用此選項將允許 Web 同步處理使用下列方法之一︰ [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], ，[!INCLUDE[tsql](../../includes/tsql-md.md)], ，或 Replication Management Objects (RMO)。 若要啟用 Web 同步處理，您必須提供訂閱者連接的 Web 伺服器位址。  
  
 如果您是第一次使用發行者，也必須設定散發者和快照集共用。 每個訂閱者的合併代理程式都必須具有快照集共用的讀取權限。 如需詳細資訊，請參閱 [設定散發](../../relational-databases/replication/configure-distribution.md) 和 [保護快照集資料夾](../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
 **gen** 是 websync XML 檔案中的保留字。 請勿嘗試發行包含資料行名稱 **gen**的資料表。  
  
## 設定訂閱  
 啟用發行集及設定 IIS 之後，請建立提取訂閱，並指定提取訂閱應利用 IIS 來同步處理。 (只有提取訂閱才支援 Web 同步處理。)  
  
## 從舊版 SQL Server 升級  
 如果您有設定好的現有 Web 同步處理拓撲，而且要升級 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，您必須確認已將最新版的 Replisapi.dll 複製到 Web 同步處理所使用的虛擬目錄。 根據預設，最新版的 Replisapi.dll 位於 C:\Program Files\Microsoft SQL Server\\< nnn\>\COM。  
  
## 複寫大量資料  
 為了避免訂閱者電腦上可能發生的記憶體問題，Web 同步處理會針對用於傳送變更的 XML 檔案使用 100 MB 的預設大小上限。 可以設定以下登錄機碼來設定此限制：  
  
 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\Replication**  
  
 **WebSyncMaxXmlSize DWORD 2000000**  
  
 此機碼的可接受值範圍是 100 MB 到 4GB。 該值會以 KB 來指定。 將這個參數設定為高的值並不保證您可以同步處理該數量的資料。 有效的限制是由訂閱者電腦上可用的連續記憶體數量所限制。 如果您的值必須大於 100 MB，我們建議您最好以累加方式增加這個值，並在訂閱者上使用一般的工作負載來測試記憶體耗用量。  
  
 XML 檔案的大小上限為 4 GB，不過複寫會分批次同步處理來自該檔案的變更。 資料和中繼資料的批次大小上限為 25 MB。 您必須確定各批次的資料未超過約 20 MB，以便允許中繼資料和任何其他負擔。 這項限制具有下列含意：  
  
-   您無法複寫任何導致資料和中繼資料超過 25 MB 的資料行。 這可能會有問題，當您要複寫資料列包含大型資料類型，例如 **varchar （max)**。  
  
-   如果您要複寫大量資料，可能必須調整合併代理程式的批次大小。  
  
 合併式複寫的批次大小是以 *「層代」*(Generation) 為測量單位，而這是每個發行項的變更集合。 使用指定的批次中的層代編號 –**DownloadGenerationsPerBatch** 和 –**UploadGenerationsPerBatch** 合併代理程式的參數。 如需詳細資訊，請參閱 [Replication Merge Agent](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
 若為大量資料，請針對每個批次參數指定一個少量數目。 我們建議您從 10 這個值開始，然後根據需求和效能進行微調。 一般而言，這些參數都指定於代理程式設定檔中。 如需有關設定檔的詳細資訊，請參閱＜ [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)＞。  
  
## Web 同步處理安全性最佳作法  
 Web 同步處理的安全性相關設定有多種選擇， 我們建議下列方式：  
  
-    [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 散發者和發行者可以位於同一部電腦 （用於合併式複寫的一般設定）。 不過，IIS 應該安裝在另一部電腦上。  
  
-   利用安全通訊端層 (SSL) 來加密訂閱者與執行 IIS 的電腦之間的連接。 Web 同步處理要求這一操作。  
  
-   對訂閱者與 IIS 之間的連接使用「基本驗證」。 IIS 可以利用基本驗證來代替「訂閱者」建立到「發行者」/「散發者」的連接，而不需要委派。 如果使用「整合式驗證」，則需要委派。  
  
    > [!NOTE]  
    >  基本驗證是將認證傳遞至 IIS 的方法。 針對建立到 IIS 的連接，基本驗證不會防止指定 Windows 網域帳戶。  
  
-   指定「快照集代理程式」應在 Windows 網域帳戶下執行，同時指定代理程式應依照該帳戶採用的方式來建立連接。 (此為預設組態)。指定每個「合併代理程式」應在使用「訂閱者」電腦之使用者的網域帳戶下執行，同時指定代理程式應依照該帳戶採用的方式來建立連接。  
  
     如需有關代理程式所需權限的詳細資訊，請參閱＜ [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)＞。  
  
-   相同的網域帳戶指定為在指定的帳戶和密碼時，會使用 「 合併代理程式的一個 **Web 伺服器資訊** 頁面新增訂閱精靈 」，或您指定的值 **@internet_url** 和 **@internet_login** 參數 [sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 此帳戶必須具有快照集共用的讀取權限。  
  
-   每個發行集應使用個別的 IIS 虛擬目錄。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replication Listener (Replisapi.dll) 執行時所使用的帳戶也是在同步處理期間連接至發行者和散發者的帳戶。 這個帳戶必須對應至發行者和散發者的 SQL 登入帳戶。 如需詳細資訊，請參閱 「 設定權限的 SQL Server 複寫接聽程式 」 一節 [將 IIS 設定 Web 同步處理](../../relational-databases/replication/configure-iis-for-web-synchronization.md)。  
  
-   您可以利用 FTP，將快照集從發行者傳遞到執行 IIS 的電腦。 快照集永遠是利用 HTTPS，從執行 IIS 的電腦傳遞到「訂閱者」。 如需詳細資訊，請參閱 [透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
-   如果複寫拓撲中的伺服器在防火牆後面，您可能需要在防火牆中開啟通訊埠，才能啟用 Web 同步處理。  
  
    -   訂閱者電腦會使用 SSL 透過 HTTPS 連接到執行 IIS 的電腦，而這部電腦通常設定為使用通訊埠 443。 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 訂閱者也可透過 HTTP 進行連接，這通常設定為使用通訊埠 80。  
  
    -   執行 IIS 的電腦通常會使用通訊埠 1433 連接到發行者或散發者 (預設執行個體)。 當發行者或散發者為伺服器上的具名執行個體 (此伺服器具有另一個預設執行個體) 時，通常會使用通訊埠 1500 來連接至此具名執行個體。  
  
    -   如果您使用防火牆來隔開執行 IIS 的電腦與散發者，而且使用 FTP 共用進行快照集傳遞，則必須開啟用於 FTP 的通訊埠。 如需詳細資訊，請參閱 [透過 FTP 傳送快照集](../../relational-databases/replication/transfer-snapshots-through-ftp.md)。  
  
> [!IMPORTANT]  
>  在防火牆中開啟通訊埠可能會讓您的伺服器面臨惡意攻擊的威脅。 請先確定您已了解防火牆系統，然後再開啟通訊埠。 如需詳細資訊，請參閱＜ [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)＞。  
  
## 另請參閱  
 [合併式複寫的 Web 同步處理](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  