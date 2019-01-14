---
title: 透過 FTP 傳遞快照集 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d1a8989492c9efb670b00bda00dbfa757c549fca
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/09/2019
ms.locfileid: "54130268"
---
# <a name="deliver-a-snapshot-through-ftp"></a>透過 FTP 傳遞快照集
  本主題描述如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ，在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中透過 FTP 傳遞快照集。  
  
##  <a name="Restrictions"></a> 限制事項  
  
-   快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，則您必須指定共用目錄為通用命名慣例 (UNC) 路徑，例如 \\\ftpserver\home\snapshots。 如需詳細資訊，請參閱[保護快照集資料夾](../security/secure-the-snapshot-folder.md)。  
  
###  <a name="Prerequisites"></a> 必要條件  
  
-   若要使用「檔案傳輸通訊協定」(FTP) 傳送快照集檔案，您必須先設定 FTP 伺服器。 如需詳細資訊，請參閱 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Internet Information Services (IIS) 文件集。  
  
###  <a name="Security"></a> 安全性  
 若要改善安全性，我們建議您在透過網際網路使用 FTP 快照集傳遞時，實作虛擬私人網路 (VPN)。 如需詳細資訊，請參閱[使用 VPN 透過網際網路發行資料](../publish-data-over-the-internet-using-vpn.md)。  
  
 最佳安全性作法是不允許匿名登入 FTP 伺服器。 快照集代理程式必須有您指定之目錄的寫入權限，而散發代理程式或合併代理程式則必須有讀取權限。 如果使用提取訂閱，則您必須指定共用目錄為通用命名慣例 (UNC) 路徑，例如 \\\ftpserver\home\snapshots。 如需詳細資訊，請參閱[保護快照集資料夾](../security/secure-the-snapshot-folder.md)。  
  
 可能的話，會在執行階段提示使用者輸入其認證。 如果將認證儲存在指令碼檔案中，您必須維護此檔案的安全。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 設定 FTP 伺服器之後，請在 [發行集屬性 \<發行集>] 對話方塊中，指定此伺服器的目錄和安全性資訊。 如需有關存取這個對話方塊的詳細資訊，請參閱＜ [View and Modify Publication Properties](view-and-modify-publication-properties.md)＞。  
  
#### <a name="to-specify-ftp-information"></a>若要指定 FTP 資訊  
  
1.  從以下頁面之一的 [發行集屬性 - \<發行集>]  對話方塊中，選取 [允許訂閱者使用 FTP 下載快照集檔案]：   
    -    **[FTP 快照集]** 頁面，適用於快照式和交易式發行集，以及執行 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]之前版本的「發行者」所用的合併式發行集。    
    -   **[FTP 快照集和網際網路]** 頁面，適用於執行 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 或更新版本「發行者」的合併式發行集。    
2.  指定 **[FTP 伺服器名稱]**、 **[通訊埠編號]**、 **[FTP 根資料夾的路徑]**、 **[登入]** 以及 **[密碼]** 的值。    
     例如，如果 FTP 伺服器根目錄為 \\\ftpserver\home，而您想將快照集儲存在 \\\ftpserver\home\snapshots 中，請將 [FTP 根資料夾的路徑] 屬性指定為 \snapshots\ftp (複寫會在建立快照集檔案時，在快照集資料夾路徑後加上 'ftp')。    
3.  指定快照集代理程式應該將快照集檔案複製到步驟 2 中指定的目錄。 例如，若要讓快照集代理程式將快照集檔案寫入到 \\\ftpserver\home\snapshots\ftp 中，您必須在以下兩處位置的其中一處指定路徑 \\\ftpserver\home\snapshots：    
    -   與此發行集相關的「散發者」的預設快照集位置。    
         如需指定預設快照集位置的詳細資訊，請參閱[指定預設快照集位置](../snapshot-options.md#snapshot-folder-locations)。    
    -   此發行集的替代快照集資料夾位置。 如果壓縮快照集，則需要替代位置。    
         在 [發行集屬性 - \<發行集>] 對話方塊 [快照集] 頁面上的 [將檔案放在下列資料夾中] 文字方塊中，輸入路徑。   
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以設定讓快照集檔案可在 FTP 伺服器上使用的選項，而且可以透過程式設計方式使用複寫預存程序來修改這些 FTP 設定。 使用的程序取決於發行集的類型而定。 FTP 快照集傳遞只會搭配提取訂閱一起使用。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集啟用 FTP 快照集傳遞  
  
1.  在發行集資料庫的發行者上，執行 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)。 指定**@publication**，值為`true`for **@enabled_for_internet**，以及下列參數的適當值：    
    -   **@ftp_address** - 用於傳遞快照集之 FTP 伺服器的位址。    
    -   (選擇性) **@ftp_port** - FTP 伺服器所使用的通訊埠。    
    -   (選擇性) **@ftp_subdirectory** - 指派給 FTP 登入之預設 FTP 目錄的子目錄。 例如，若 FTP 伺服器根目錄為 \\\ftpserver\home，而您想將快照集儲存在 \\\ftpserver\home\snapshots 中，請為 **@ftp_subdirectory** 指定 **\snapshots\ftp** (複寫會在建立快照集檔案時，在快照集資料夾路徑後加上 'ftp')。    
    -   (選擇性) **@ftp_login** - 連接到 FTP 伺服器時所使用的登入帳戶。    
    -   (選擇性) **@ftp_password** - FTP 登入的密碼。  
  
     這會建立使用 FTP 的發行集。 如需詳細資訊，請參閱 [Create a Publication](create-a-publication.md)。  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>針對合併式發行集啟用 FTP 快照集傳遞  
  
1.  在發行集資料庫的發行者上，執行 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)。 指定**@publication**，值為`true`for **@enabled_for_internet**以及下列參數的適當值：  
  
    -   **@ftp_address** - 用於傳遞快照集之 FTP 伺服器的位址。    
    -   (選擇性) **@ftp_port** - FTP 伺服器所使用的通訊埠。    
    -   (選擇性) **@ftp_subdirectory** - 指派給 FTP 登入之預設 FTP 目錄的子目錄。 例如，若 FTP 伺服器根目錄為 \\\ftpserver\home，而您想將快照集儲存在 \\\ftpserver\home\snapshots 中，請為 **@ftp_subdirectory** 指定 **\snapshots\ftp** (複寫會在建立快照集檔案時，在快照集資料夾路徑後加上 'ftp')。    
    -   (選擇性) **@ftp_login** - 連接到 FTP 伺服器時所使用的登入帳戶。    
    -   (選擇性) **@ftp_password** - FTP 登入的密碼。  
  
     這會建立使用 FTP 的發行集。 如需詳細資訊，請參閱 [Create a Publication](create-a-publication.md)。  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>針對使用 FTP 快照集傳遞的快照式或交易式發行集建立提取訂閱  
  
1.  在訂閱資料庫的訂閱者上，執行 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)。 指定 **@publisher** 和 **@publication**中透過 FTP 傳遞快照集。  
  
    -   在訂閱資料庫的訂閱者上，執行 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)。 指定**@publisher**， **@publisher_db**， **@publication**，[!INCLUDE[msCoName](../../../includes/msconame-md.md)]所在的 Windows 認證 「 散發代理程式訂閱者 」 執行時會針對**@job_login**並**@job_password**，而值為`true`如**@use_ftp**。  
  
2.  在發行集資料庫的發行者上，執行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) ，以註冊提取訂閱。 如需詳細資訊，請參閱 [建立提取訂閱](../create-a-pull-subscription.md)。  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>針對使用 FTP 快照集傳遞的合併式發行集建立提取訂閱  
  
1.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)。 指定 **@publisher** 和 **@publication**中透過 FTP 傳遞快照集。   
2.  在訂閱資料庫的訂閱者上，執行 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)。 指定**@publisher**， **@publisher_db**， **@publication**，「 Windows 認證的 「 訂閱者端的散發代理程式執行**@job_login**並**@job_password**，而值為`true`如**@use_ftp**。    
3.  在發行集資料庫的發行者上，執行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) ，以註冊提取訂閱。 如需詳細資訊，請參閱 [建立提取訂閱](../create-a-pull-subscription.md)。  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>針對快照式或交易式發行集變更一個或多個 FTP 快照集傳遞設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)。 針對 **@property** 指定下列其中一個值，並針對 **@value**指定此設定的新值：    
    -   `ftp_address` - 用於傳遞快照集之 FTP 伺服器的位址。    
    -   `ftp_port` - FTP 伺服器所使用的通訊埠。    
    -   `ftp_subdirectory` - 用於 FTP 快照集之預設 FTP 目錄的子目錄。    
    -   `ftp_login` - 用於連接 FTP 伺服器的登入。    
    -   `ftp_password` - FTP 登入的密碼。  
  
2.  (選擇性) 針對變更的每一個 FTP 設定重複步驟 1。    
3.  (選擇性) 若要停用 FTP 快照集傳遞，請在發行集資料庫的發行者上執行 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) 。 指定的值為`enabled_for_internet`for **@property**值，並針對`false`如**@value**。  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>針對合併式發行集變更 FTP 快照集傳遞設定  
  
1.  在發行集資料庫的發行者上，執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)。 針對 **@property** 指定下列其中一個值，並針對 **@value**指定此設定的新值：  
  
    -   `ftp_address` - 用於傳遞快照集之 FTP 伺服器的位址。    
    -   `ftp_port` - FTP 伺服器所使用的通訊埠。    
    -   `ftp_subdirectory` - 用於 FTP 快照集之預設 FTP 目錄的子目錄。   
    -   `ftp_login` - 用於連接 FTP 伺服器的登入。    
    -   `ftp_password` - FTP 登入的密碼。    
2.  (選擇性) 針對變更的每一個 FTP 設定重複步驟 1。    
3.  (選擇性) 若要停用 FTP 快照集傳遞，請在發行集資料庫的發行者上執行 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) 。 指定的值為`enabled_for_internet`for **@property**值，並針對`false`如**@value**。  
  
###  <a name="TsqlExample"></a> 範例 (Transact-SQL)  
 下列範例會建立允許訂閱者的合併式發行集，以使用 FTP 存取快照集資料。 當訂閱者存取 FTP 共用位置時，應該使用安全 VPN 連接。 **sqlcmd** 指令碼變數是用來提供登入和密碼值。 如需詳細資訊，請參閱[以指令碼變數使用 sqlcmd](../../scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubftp.sql#sp_createmergepub_ftp)]  
  
 下列範例會建立合併式發行集的訂閱，其中的訂閱者會使用 FTP 取得快照集。 當訂閱者存取 FTP 共用位置時，應該使用安全 VPN 連接。 **sqlcmd** 指令碼變數是用來提供登入和密碼值。 如需詳細資訊，請參閱[以指令碼變數使用 sqlcmd](../../scripting/sqlcmd-use-with-scripting-variables.md)。  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsub_ftp)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsubagent_ftp)]  
  
## <a name="see-also"></a>另請參閱  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [透過 FTP 傳送快照集](../transfer-snapshots-through-ftp.md)   
 [變更發行集與發行項屬性](change-publication-and-article-properties.md)   
 [使用快照集初始化訂閱](../initialize-a-subscription-with-a-snapshot.md)  
  
  
