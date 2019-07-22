---
title: 透過 FTP 傳遞快照集 | Microsoft 文件
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3d39fcd8df1f62bd089361a9a32ef7a59aa113a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907694"
---
# <a name="deliver-a-snapshot-through-ftp"></a>透過 FTP 傳遞快照集
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中透過 FTP 傳遞快照集。  

依預設，快照集儲存在定義為「通用命名慣例」(UNC) 共用的資料夾中。 複寫還允許您指定「檔案傳輸通訊協定」(FTP) 共用，而不是 UNC 共用。 若要使用 FTP，您必須設定 FTP 伺服器，然後設定使用 FTP 的一個發行集和一個或多個訂閱。 如需有關如何設定 FTP 伺服器的詳細資訊，請參閱 Internet Information Services (IIS) 文件集。 如果您為發行集指定 FTP 資訊，依預設，該發行集的訂閱會使用 FTP。 只有當執行 IIS 的電腦與「散發者」之間被防火牆隔開時，Web 同步處理才會使用 FTP。 在此情況下，可以使用 FTP，從散發者和執行 IIS 的電腦來傳送快照集 (快照集一定會使用 HTTPS 傳送到訂閱者)。  
  
> [!IMPORTANT]  
>  建議您使用「Microsoft Windows 驗證」和 UNC 共用，而不要使用 FTP 共用，因為系統必須儲存 FTP 密碼，而該密碼會以純文字格式從「訂閱者」或執行 IIS 的電腦 (使用 Web 同步處理時) 傳送到 FTP 伺服器。 此外，因為對快照集共用的存取由單一帳戶控制，所以無法確定已篩選的合併式發行集之「訂閱者」僅從其資料分割存取快照集檔案。  
  

## <a name="limitations-and-restrictions"></a>限制事項  
  
-   快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，則您必須指定共用目錄為通用命名慣例 (UNC) 路徑，例如 \\\ftpserver\home\snapshots。 如需詳細資訊，請參閱[保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   若要使用「檔案傳輸通訊協定」(FTP) 傳送快照集檔案，您必須先設定 FTP 伺服器。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 文件集。  
  
###  <a name="Security"></a> 安全性  
 若要改善安全性，我們建議您在透過網際網路使用 FTP 快照集傳遞時，實作虛擬私人網路 (VPN)。 如需詳細資訊，請參閱[使用 VPN 透過網際網路發行資料](../../../relational-databases/replication/publish-data-over-the-internet-using-vpn.md)。  
  
 最佳安全性作法是不允許匿名登入 FTP 伺服器。 快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，則您必須指定共用目錄為通用命名慣例 (UNC) 路徑，例如 \\\ftpserver\home\snapshots。 如需詳細資訊，請參閱[保護快照集資料夾](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
 可能的話，會在執行階段提示使用者輸入其認證。 如果將認證儲存在指令碼檔案中，您必須維護此檔案的安全。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 設定 FTP 伺服器之後，請在 [發行集屬性 \<發行集>]  對話方塊中，指定此伺服器的目錄和安全性資訊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)＞。  
  
#### <a name="to-specify-ftp-information"></a>若要指定 FTP 資訊  
  
1.  從以下頁面之一的 [發行集屬性 - \<發行集>]  對話方塊中，選取 [允許訂閱者使用 FTP 下載快照集檔案]  ：  
  
    -   **[FTP 快照集]** 頁面，適用於快照式和交易式發行集，以及執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的「發行者」所用的合併式發行集。  
  
    -   **[FTP 快照集和網際網路]** 頁面，適用於執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本「發行者」的合併式發行集。  
  
2.  指定 **[FTP 伺服器名稱]** 、 **[通訊埠編號]** 、 **[FTP 根資料夾的路徑]** 、 **[登入]** 以及 **[密碼]** 的值。  
  
     例如，如果 FTP 伺服器根目錄為 \\\ftpserver\home，而您想將快照集儲存在 \\\ftpserver\home\snapshots 中，請將 [FTP 根資料夾的路徑]  屬性指定為 \snapshots\ftp (複寫會在建立快照集檔案時，在快照集資料夾路徑後加上 'ftp')。  
  
3.  指定快照集代理程式應該將快照集檔案複製到步驟 2 中指定的目錄。 例如，若要讓快照集代理程式將快照集檔案寫入到 \\\ftpserver\home\snapshots\ftp 中，您必須在以下兩處位置的其中一處指定路徑 \\\ftpserver\home\snapshots：  
  
    -   與此發行集相關的「散發者」的預設快照集位置。    
    -   此發行集的替代快照集資料夾位置。 如果壓縮快照集，則需要替代位置。  

如需有關修改快照集資料夾位置屬性的詳細資訊，請參閱[快照集選項](../snapshot-options.md)。
  

4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以設定讓快照集檔案可在 FTP 伺服器上使用的選項，而且可以透過程式設計方式使用複寫預存程序來修改這些 FTP 設定。 使用的程序取決於發行集的類型而定。 FTP 快照集傳遞只會搭配提取訂閱一起使用。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集啟用 FTP 快照集傳遞  
  
1.  在發行集資料庫的發行者上，執行 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定 **@publication** 、 **@enabled_for_internet** @enabled_for_internet **@enabled_for_internet** 值，以及下列參數的適當值：  
  
    -   **@ftp_address** - 用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   (選擇性) **@ftp_port** - FTP 伺服器所使用的通訊埠。  
  
    -   (選擇性) **@ftp_subdirectory** - 指派給 FTP 登入之預設 FTP 目錄的子目錄。 例如，若 FTP 伺服器根目錄為 \\\ftpserver\home，而您想將快照集儲存在 \\\ftpserver\home\snapshots 中，請為 **@ftp_subdirectory** 指定 **\snapshots\ftp** (複寫會在建立快照集檔案時，在快照集資料夾路徑後加上 'ftp')。  
  
    -   (選擇性) **@ftp_login** - 連接到 FTP 伺服器時所使用的登入帳戶。  
  
    -   (選擇性) **@ftp_password** - FTP 登入的密碼。  
  
     這會建立使用 FTP 的發行集。 如需詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>針對合併式發行集啟用 FTP 快照集傳遞  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 指定 **@publication** 、 **@enabled_for_internet** @enabled_for_internet **@enabled_for_internet** 值，以及下列參數的適當值：  
  
    -   **@ftp_address** - 用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   (選擇性) **@ftp_port** - FTP 伺服器所使用的通訊埠。  
  
    -   (選擇性) **@ftp_subdirectory** - 指派給 FTP 登入之預設 FTP 目錄的子目錄。 例如，若 FTP 伺服器根目錄為 \\\ftpserver\home，而您想將快照集儲存在 \\\ftpserver\home\snapshots 中，請為 **@ftp_subdirectory** 指定 **\snapshots\ftp** (複寫會在建立快照集檔案時，在快照集資料夾路徑後加上 'ftp')。  
  
    -   (選擇性) **@ftp_login** - 連接到 FTP 伺服器時所使用的登入帳戶。  
  
    -   (選擇性) **@ftp_password** - FTP 登入的密碼。  
  
     這會建立使用 FTP 的發行集。 如需詳細資訊，請參閱[建立發行集](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>針對使用 FTP 快照集傳遞的快照式或交易式發行集建立提取訂閱  
  
1.  在訂閱資料庫的訂閱者上，執行 [sp_addpullsubscription](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication** 中透過 FTP 傳遞快照集。  
  
    -   在訂閱資料庫的訂閱者上，執行 [sp_addpullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** 、針對 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] @job_login **@job_login** 和 **@job_password** Windows 認證 (散發代理程式在訂閱者上執行時會使用此認證)、 **@enabled_for_internet** @enabled_for_internet **@use_ftp** 中透過 FTP 傳遞快照集。  
  
2.  在發行集資料庫的發行者上，執行 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) ，以註冊提取訂閱。 如需詳細資訊，請參閱 [建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>針對使用 FTP 快照集傳遞的合併式發行集建立提取訂閱  
  
1.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)。 指定 **@publisher** 和 **@publication** 中透過 FTP 傳遞快照集。  
  
2.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription_agent](../../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)。 指定 **@publisher** 、 **@publisher_db** 、 **@publication** 、針對 **@job_login** 和 **@job_password** Windows 認證 (散發代理程式在訂閱者上執行時會使用此認證)、 **@enabled_for_internet** @enabled_for_internet **@use_ftp** 中透過 FTP 傳遞快照集。  
  
3.  在發行集資料庫的發行者上，執行 [sp_addmergesubscription](../../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) ，以註冊提取訂閱。 如需詳細資訊，請參閱 [建立提取訂閱](../../../relational-databases/replication/create-a-pull-subscription.md)。  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集變更一個或多個 FTP 快照集傳遞設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)。 針對 **@property** 指定下列其中一個值，並針對 **@value** 指定此設定的新值：  
  
    -   **ftp_address** - 用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   **ftp_port** - FTP 伺服器所使用的通訊埠。  
  
    -   **ftp_subdirectory** - 用於 FTP 快照集之預設 FTP 目錄的子目錄。  
  
    -   **ftp_login** - 用於連接 FTP 伺服器的登入。  
  
    -   **ftp_password** - FTP 登入的密碼。  
  
2.  (選擇性) 針對變更的每一個 FTP 設定重複步驟 1。  
  
3.  (選擇性) 若要停用 FTP 快照集傳遞，請在發行集資料庫的發行者上執行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 。 針對 **@property** @enabled_for_internet **@property** 值及針對 **@value** @enabled_for_internet **@value** 中透過 FTP 傳遞快照集。  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>針對合併式發行集變更 FTP 快照集傳遞設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)。 針對 **@property** 指定下列其中一個值，並針對 **@value** 指定此設定的新值：  
  
    -   **ftp_address** - 用於傳遞快照集之 FTP 伺服器的位址。  
  
    -   **ftp_port** - FTP 伺服器所使用的通訊埠。  
  
    -   **ftp_subdirectory** - 用於 FTP 快照集之預設 FTP 目錄的子目錄。  
  
    -   **ftp_login** - 用於連接 FTP 伺服器的登入。  
  
    -   **ftp_password** - FTP 登入的密碼。  
  
2.  (選擇性) 針對變更的每一個 FTP 設定重複步驟 1。  
  
3.  (選擇性) 若要停用 FTP 快照集傳遞，請在發行集資料庫的發行者上執行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md) 。 針對 **@property** @enabled_for_internet **@property** 值及針對 **@value** @enabled_for_internet **@value** 中透過 FTP 傳遞快照集。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立允許訂閱者的合併式發行集，以使用 FTP 存取快照集資料。 當訂閱者存取 FTP 共用位置時，應該使用安全 VPN 連接。 **sqlcmd** 指令碼變數是用來提供登入和密碼值。 如需詳細資訊，請參閱[以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_1.sql)]  
  
 下列範例會建立合併式發行集的訂閱，其中的訂閱者會使用 FTP 取得快照集。 當訂閱者存取 FTP 共用位置時，應該使用安全 VPN 連接。 **sqlcmd** 指令碼變數是用來提供登入和密碼值。 如需詳細資訊，請參閱[以指令碼變數使用 sqlcmd](../../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_2.sql)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../relational-databases/replication/codesnippet/tsql/deliver-a-snapshot-throu_3.sql)]  
  
## <a name="see-also"></a>另請參閱  
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [變更發行集與發行項屬性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [使用快照集初始化訂閱](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
