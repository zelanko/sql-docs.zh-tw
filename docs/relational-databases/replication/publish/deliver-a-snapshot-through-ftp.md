---
title: "透過 FTP 傳遞快照集 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "snapshots [SQL Server replication], FTP snapshots"
  - "FTP snapshots [SQL Server replication]"
  - "快照式複寫 [SQL Server], FTP"
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 透過 FTP 傳遞快照集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中透過 FTP 傳遞快照集。  
  
 **本主題內容**  
  
-   **開始之前：**  
  
     [限制事項](#Restrictions)  
  
     [必要條件](#Prerequisites)  
  
     [安全性](#Security)  
  
-   **若要透過 FTP 傳遞快照集，請使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 開始之前  
  
###  <a name="Restrictions"></a> 限制事項  
  
-   快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定共用的目錄做為通用的命名慣例 (UNC) 路徑，例如 \\\ftpserver\home\snapshots。 如需詳細資訊，請參閱 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   若要使用「檔案傳輸通訊協定」(FTP) 傳送快照集檔案，您必須先設定 FTP 伺服器。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 文件集。  
  
###  <a name="Security"></a> 安全性  
 若要改善安全性，我們建議您在透過網際網路使用 FTP 快照集傳遞時，實作虛擬私人網路 (VPN)。 如需詳細資訊，請參閱 [發行的資料，透過網際網路使用 VPN](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)。  
  
 最佳安全性作法是不允許匿名登入 FTP 伺服器。 快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，您必須指定共用的目錄做為通用的命名慣例 (UNC) 路徑，例如 \\\ftpserver\home\snapshots。 如需詳細資訊，請參閱 [保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
 可能的話，會在執行階段提示使用者輸入其認證。 如果將認證儲存在指令碼檔案中，您必須維護此檔案的安全。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 FTP 伺服器設定之後，指定此伺服器的目錄和安全性資訊 **發行集屬性 \< 發行集>** 對話方塊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
#### 若要指定 FTP 資訊  
  
1.  在 **發行集屬性-\< 發行集>** 對話方塊中，選取 **允許訂閱者下載使用 FTP 快照集檔案** 中的下列網頁︰  
  
    -    **[FTP 快照集]** 頁面，適用於快照式和交易式發行集，以及執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的「發行者」所用的合併式發行集。  
  
    -   **[FTP 快照集和網際網路]** 頁面，適用於執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本「發行者」的合併式發行集。  
  
2.  指定 **[FTP 伺服器名稱]**、 **[通訊埠編號]**、 **[FTP 根資料夾的路徑]**、 **[登入]**以及 **[密碼]**的值。  
  
     比方說，如果 FTP 伺服器根目錄為 \\\ftpserver\home，而且您想將快照集儲存在 \\\ftpserver\home\snapshots，指定屬性的 \snapshots\ftp **FTP 根資料夾路徑** （複寫會附加 'ftp' 快照集資料夾路徑會在建立快照集檔案時）。  
  
3.  指定快照集代理程式應該將快照集檔案複製到步驟 2 中指定的目錄。 例如，將快照集代理程式寫入快照集檔案 \\\ftpserver\home\snapshots\ftp，您必須指定路徑 \\\ftpserver\home\snapshots 兩個位置其中之一︰  
  
    -   與此發行集相關的「散發者」的預設快照集位置。  
  
         如需指定預設快照集位置的詳細資訊，請參閱 [指定預設快照集位置 & #40。SQL Server Management Studio & #41;](../../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)。  
  
    -   此發行集的替代快照集資料夾位置。 如果壓縮快照集，則需要替代位置。  
  
         輸入的路徑， **檔案放入下列資料夾** 的快照集] 頁面上的文字方塊 **發行集屬性-\< 發行集>** 對話方塊。 如需替代快照集資料夾位置的詳細資訊，請參閱＜ [Alternate Snapshot Folder Locations](../../../relational-databases/replication/alternate-snapshot-folder-locations.md)＞。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以設定讓快照集檔案可在 FTP 伺服器上使用的選項，而且可以透過程式設計方式使用複寫預存程序來修改這些 FTP 設定。 使用的程序取決於發行集的類型而定。 FTP 快照集傳遞只會搭配提取訂閱一起使用。  
  
#### 針對快照式或交易式發行集啟用 FTP 快照集傳遞  
  
1.  在發行集資料庫的發行者，執行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定 **@publication**, ，值為 **true** 的 **@enabled_for_internet**, ，並適當的下列參數的值︰  
  
    -   **@ftp_address** -用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   （選擇性） **@ftp_port** -FTP 伺服器所使用的連接埠。  
  
    -   （選擇性） **@ftp_subdirectory** -指派給 FTP 登入之預設 FTP 目錄的子目錄。 比方說，如果 FTP 伺服器根目錄為 \\\ftpserver\home，而且您想將快照集儲存在 \\\ftpserver\home\snapshots，指定 **\snapshots\ftp** 的 **@ftp_subdirectory** （複寫會附加 'ftp' 快照集資料夾路徑會在建立快照集檔案時）。  
  
    -   （選擇性） **@ftp_login** -連接到 FTP 伺服器時使用的登入帳戶。  
  
    -   （選擇性） **@ftp_password** -FTP 登入的密碼。  
  
     這會建立使用 FTP 的發行集。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 針對合併式發行集啟用 FTP 快照集傳遞  
  
1.  在發行集資料庫的發行者，執行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定 **@publication**, ，值為 **true** 的 **@enabled_for_internet** 和下列參數的適當值︰  
  
    -   **@ftp_address** -用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   （選擇性） **@ftp_port** -FTP 伺服器所使用的連接埠。  
  
    -   （選擇性） **@ftp_subdirectory** -指派給 FTP 登入之預設 FTP 目錄的子目錄。 比方說，如果 FTP 伺服器根目錄為 \\\ftpserver\home，而且您想將快照集儲存在 \\\ftpserver\home\snapshots，指定 **\snapshots\ftp** 的 **@ftp_subdirectory** （複寫會附加 'ftp' 快照集資料夾路徑會在建立快照集檔案時）。  
  
    -   （選擇性） **@ftp_login** -連接到 FTP 伺服器時使用的登入帳戶。  
  
    -   （選擇性） **@ftp_password** -FTP 登入的密碼。  
  
     這會建立使用 FTP 的發行集。 如需詳細資訊，請參閱 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 針對使用 FTP 快照集傳遞的快照式或交易式發行集建立提取訂閱  
  
1.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication**。  
  
    -   在訂閱資料庫上的 「 訂閱者 」 執行 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, 、 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 「 訂閱者 」 的 「 散發代理程式執行的 Windows 認證 **@job_login** 和 **@job_password**, ，而值為 **true** 的 **@use_ftp**。  
  
2.  在發行集資料庫的發行者，執行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 以註冊提取訂閱。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
#### 針對使用 FTP 快照集傳遞的合併式發行集建立提取訂閱  
  
1.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication**。  
  
2.  在訂閱資料庫上的 「 訂閱者 」 執行 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，Windows 認證的 「 訂閱者 」 的 「 散發代理程式執行 **@job_login** 和 **@job_password**, ，而值為 **true** 的 **@use_ftp**。  
  
3.  在發行集資料庫的發行者，執行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) 以註冊提取訂閱。 如需詳細資訊，請參閱 [Create a Pull Subscription](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
#### 針對快照式或交易式發行集變更一個或多個 FTP 快照集傳遞設定  
  
1.  在發行集資料庫的發行者，執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 針對 **@property** 指定下列其中一個值，並針對 **@value**指定此設定的新值：  
  
    -   **ftp_address** -用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   **ftp_port** -FTP 伺服器所使用的連接埠。  
  
    -   **ftp_subdirectory** -用於 FTP 快照集之預設 FTP 目錄的子目錄。  
  
    -   **ftp_login** -用來連接到 FTP 伺服器的登入。  
  
    -   **ftp_password** -FTP 登入的密碼。  
  
2.  (選擇性) 針對變更的每一個 FTP 設定重複步驟 1。  
  
3.  （選擇性）若要停用 FTP 快照集傳遞，請執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **enabled_for_internet** 的 **@property** 且值為 **false** 的 **@value**。  
  
#### 針對合併式發行集變更 FTP 快照集傳遞設定  
  
1.  在發行集資料庫的發行者，執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 針對 **@property** 指定下列其中一個值，並針對 **@value**指定此設定的新值：  
  
    -   **ftp_address** -用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   **ftp_port** -FTP 伺服器所使用的連接埠。  
  
    -   **ftp_subdirectory** -用於 FTP 快照集之預設 FTP 目錄的子目錄。  
  
    -   **ftp_login** -用來連接到 FTP 伺服器的登入。  
  
    -   **ftp_password** -FTP 登入的密碼。  
  
2.  (選擇性) 針對變更的每一個 FTP 設定重複步驟 1。  
  
3.  （選擇性）若要停用 FTP 快照集傳遞，請執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 於發行集資料庫的發行者端。 指定的值為 **enabled_for_internet** 的 **@property** 且值為 **false** 的 **@value**。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立允許訂閱者的合併式發行集，以使用 FTP 存取快照集資料。 當訂閱者存取 FTP 共用位置時，應該使用安全 VPN 連接。 **sqlcmd** 指令碼變數是用來提供登入和密碼值。 如需詳細資訊，請參閱 [以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 下列範例會建立合併式發行集的訂閱，其中的訂閱者會使用 FTP 取得快照集。 當訂閱者存取 FTP 共用位置時，應該使用安全 VPN 連接。 **sqlcmd** 指令碼變數是用來提供登入和密碼值。 如需詳細資訊，請參閱 [以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## 另請參閱  
 [複寫系統預存程序概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [透過 FTP 傳送快照集](../../../relational-databases/replication/transfer-snapshots-through-ftp.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照集初始化訂閱](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  