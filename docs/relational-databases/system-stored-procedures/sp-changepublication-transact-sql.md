---
title: sp_changepublication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changepublication
- sp_changepublication_TSQL
helpviewer_keywords:
- sp_changepublication
ms.assetid: c36e5865-25d5-42b7-b045-dc5036225081
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8db735195ad0667944ca3e3710e629791662fd7f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="spchangepublication-transact-sql"></a>sp_changepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  變更發行集的屬性。 這個預存程序執行於發行集資料庫的發行者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
sp_changepublication [ [ @publication = ] 'publication' ]  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication =** ] **'***publication***'**  
 這是發行集的名稱。 *發行集*是**sysname**，預設值是 NULL。  
  
 [  **@property =** ] **'***屬性***'**  
 這是要變更的發行集屬性。 *屬性*是**nvarchar （255)**。  
  
 [  **@value =** ] **'***值***'**  
 這是新的屬性值。 *值*是**nvarchar （255)**，預設值是 NULL。  
  
 下表描述可變更的發行集屬性及這些屬性值的限制。  
  
|屬性|Value|Description|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|可以針對給定的發行集建立匿名訂閱和*immediate_sync*也必須是**true**。 點對點發行集的這個項目不能變更。|  
||**false**|不能建立給定發行集的匿名訂閱。 點對點發行集的這個項目不能變更。|  
|**allow_initialize_from_backup**|**true**|訂閱者能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 這個屬性無法變更非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集。|  
||**false**|訂閱者必須使用初始快照集。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**allow_partition_switch**|**true**|ALTER TABLE…SWITCH 陳述式可以針對發行的資料庫來執行。 如需詳細資訊，請參閱[複寫資料分割資料表及索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
||**false**|ALTER TABLE…SWITCH 陳述式無法針對發行的資料庫來執行。|  
|**allow_pull**|**true**|允許給定發行集的提取訂閱。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
||**false**|不允許給定發行集的提取訂閱。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**allow_push**|**true**|允許給定發行集的發送訂閱。|  
||**false**|不允許給定發行集的發送訂閱。|  
|**allow_subscription_copy**|**true**|啟用複製訂閱這個發行集之資料庫的能力。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
||**false**|停用複製訂閱這個發行集之資料庫的能力。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**alt_snapshot_folder**||快照集替代資料夾的位置。|  
|**centralized_conflicts**|**true**|衝突記錄會儲存在發行者端。 只有在沒有使用中的訂閱時，這個項目才能改變。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
||**false**|衝突記錄會儲存在發行者端和造成衝突的訂閱者端。 只有在沒有使用中的訂閱時，這個項目才能改變。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**compress_snapshot**|**true**|將替代快照集資料夾中的快照集壓縮成 .cab 檔案格式。 預設快照集資料夾中的快照集無法壓縮。|  
||**false**|不壓縮快照集，這是複寫的預設行為。|  
|**conflict_policy**|**pub wins**|更新訂閱者的衝突解決原則，發行者在衝突中獲勝。 只有在沒有使用中的訂閱時，才能改變這個屬性。 不支援 Oracle 發行者使用這個值。|  
||**sub reinit**|對於更新訂閱者，如果發生衝突，訂閱就必須重新初始化。 只有在沒有使用中的訂閱時，才能改變這個屬性。 不支援 Oracle 發行者使用這個值。|  
||**sub wins**|更新訂閱者的衝突解決原則，訂閱者在衝突中獲勝。 只有在沒有使用中的訂閱時，才能改變這個屬性。 不支援 Oracle 發行者使用這個值。|  
|**conflict_retention**||**int**指定衝突保留期限，以天為單位。 預設保留 14 天。 **0**表示不需要進行清除任何衝突。 不支援 Oracle 發行者使用這個值。|  
|**描述**||描述發行集的選擇性項目。|  
|**enabled_for_het_sub**|**true**|啟用發行集以支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 **enabled_for_het_sub**有發行集的訂閱時，無法變更。 您可能需要執行[複寫預存程序 (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)遵守下列需求，才能設定**enabled_for_het_sub**為 true:<br /> - **allow_queued_tran**必須**false**。<br /> - **allow_sync_tran**必須**false**。<br /> 變更**enabled_for_het_sub**至**true**可能會變更現有的發行集設定。 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
||**false**|發行集不支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**enabled_for_internet**|**true**|啟用發行集的網際網路功能，以及可以利用檔案傳輸通訊協定 (FTP)，將快照集檔案傳送給訂閱者。 發行集的同步處理檔案會放在下列目錄中：C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp。 *ftp_address*不能是 NULL。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
||**false**|不啟用發行集的網際網路功能。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**enabled_for_p2p**|**true**|發行集支援點對點複寫。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。<br /> 若要設定**enabled_for_p2p**至**true**，適用下列限制：<br /> - **allow_anonymous**必須**false**<br /> - **allow_dts**必須**false**。<br /> - **allow_initialize_from_backup**必須**，則為 true**<br /> - **allow_queued_tran**必須**false**。<br /> - **allow_sync_tran**必須**false**。<br /> - **enabled_for_het_sub**必須**false**。<br /> - **independent_agent**必須**true**。<br /> - **repl_freq**必須**連續**。<br /> - **replicate_ddl**必須**1**。|  
||**false**|發行集不支援點對點複寫。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**ftp_address**||發行集快照集檔案的 FTP 存取位置。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**ftp_login**||用來連接到 FTP 服務的使用者名稱，允許使用 ANONYMOUS 值。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**ftp_password**||用來連接到 FTP 服務之使用者名稱的密碼。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**ftp_port**||散發者的 FTP 服務通訊埠編號。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**ftp_subdirectory**||指定在發行集支援利用 FTP 來傳播快照集時，要在哪裡建立快照集檔案。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
|**immediate_sync**|**true**|每次執行快照集代理程式時，都要建立或重新建立發行集的同步處理檔案。 如果在訂閱之前，快照集代理程式已完成一次，訂閱者便能在訂閱之後，立即收到同步處理檔案。 新的訂閱會取得最近執行快照集代理程式所產生的最新同步處理檔案。 *independent_agent*也必須是**true**。 請參閱以下的 < 備註 >，如需詳細資訊，關於**immediate_sync**。|  
||**false**|只有在新訂閱存在時，才會建立同步處理檔案。 在訂閱之後，快照集代理程式啟動和完成之前，訂閱者無法接收同步處理檔案。|  
|**independent_agent**|**true**|發行集有它自己專用的散發代理程式。|  
||**false**|發行集使用共用的散發代理程式，每一組發行者/訂閱資料庫都有共用的代理程式。|  
|**p2p_continue_onconflict**|**true**|散發代理程式會在偵測到衝突時繼續處理變更。<br /> **注意：**我們建議您使用的預設值`FALSE`。 當此選項設定為`TRUE`，散發代理程式嘗試聚合拓撲中的資料，藉由套用衝突的資料列從節點具有最高訂閱者識別碼。 但是，這個方法無法保證聚合。 您應該確定在偵測到衝突之後，拓撲是一致的。 如需詳細資訊，請參閱＜ [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)＞中的「處理衝突」。|  
||**false**|散發代理程式會在偵測到衝突時停止處理變更。|  
|**post_snapshot_script**||指定在初始同步處理期間，套用所有其他複寫的物件指令碼和資料之後，散發代理程式所執行之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案的位置。|  
|**pre_snapshot_script**||指定在初始同步處理期間，套用所有其他複寫的物件指令碼和資料之前，散發代理程式所執行之 [!INCLUDE[tsql](../../includes/tsql-md.md)] 指令碼檔案的位置。|  
|**publish_to_ActiveDirectory**|**true**|這個參數已被取代，支援它的目的，只是為了與舊版的指令碼相容。 您不能再將發行集資訊加入 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中。|  
||**false**|從 Active Directory 中移除發行集資訊。|  
|**queue_type**|**sql**|利用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來儲存交易。 只有在沒有使用中的訂閱時，才能改變這個屬性。<br /><br /> 注意： 支援使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]已停用訊息佇列。 指定的值是**msmq**如*值*會導致錯誤。|  
|**repl_freq**|**連續**|發行所有記錄式交易的輸出。|  
||**快照集**|只發行已排程的同步處理事件。|  
|**replicate_ddl**|**1**|複寫在發行者端執行的資料定義語言 (DDL) 陳述式。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。|  
||**0**|不複寫 DDL 陳述式。 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集的這個屬性不能變更。 使用點對點複寫時，不能停用結構描述變更的複寫。|  
|**replicate_partition_switch**|**true**|針對發行資料庫執行的 ALTER TABLE…SWITCH 陳述式應該複寫到訂閱者。 這個選項才有效才*allow_partition_switch*設為 TRUE。 如需詳細資訊，請參閱[複寫資料分割資料表及索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
||**false**|ALTER TABLE…SWITCH 陳述式不應該複寫到訂閱者。|  
|**保留**||**int**代表的保留期限，以小時為單位，訂閱活動。 如果在保留期限內，訂閱不在使用中，就會移除它。|  
|**snapshot_in_defaultfolder**|**true**|快照集檔案儲存在預設快照集資料夾中。 如果*alt_snapshot_folder*同時指定，快照集檔案會儲存在預設位置和替代位置。|  
||**false**|快照集檔案會儲存在所指定的替代位置*alt_snapshot_folder*。|  
|**status**|**使用中**|當建立發行集時，訂閱者可以立即使用發行集資料。 不支援 Oracle 發行者使用這個值。|  
||**非使用中**|當建立發行集時，訂閱者無法使用發行集資料。 不支援 Oracle 發行者使用這個值。|  
|**sync_method**|**native**|當同步處理訂閱時，使用所有資料表的原生模式大量複製輸出。|  
||**character**|當同步處理訂閱時，使用所有資料表的字元模式大量複製輸出。|  
||**並行**|使用所有資料表的原生模式大量複製程式輸出，但在快照集的產生程序中，不鎖定資料表。 這個項目對快照式複寫無效。|  
||**concurrent_c**|使用所有資料表的字元模式大量複製程式輸出，但在快照集的產生程序中，不鎖定資料表。 這個項目對快照式複寫無效。|  
|**taskid**||這個屬性已被取代，不再受到支援。|  
|**allow_drop**|**true**|可讓`DROP TABLE`DLL 支援屬於交易式複寫的發行項。 最低支援版本： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2 或以上版本和[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]Service Pack 1 或更新版本。 其他參考： [KB 3170123](https://support.microsoft.com/en-us/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactional-replication-in-sql-server-2014-or-in-sql-server-2016-sp1)|
||**false**|停用`DROP TABLE`DLL 支援屬於交易式複寫的發行項。 這是**預設**這個屬性的值。|
|**NULL** （預設值）||傳回支援的值清單*屬性*。|  
  
[  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 認可這個預存程序所採取的動作可能使現有的快照集失效。 *force_invalidate_snapshot*是**元**，預設值是**0**。  
  - **0**指定發行項的變更不會使快照集失效。 如果預存程序偵測到變更需要新的快照集，就會發生錯誤，且不會進行任何變更。  
  - **1**指定發行項的變更可能使快照集失效。 如果有現有的訂閱需要新的快照集，這個值會提供要標示為已棄用之現有快照集的權限，此時會產生新的快照集。   
請參閱＜備註＞一節，以了解在變更時需要產生新快照集的屬性。  
  
[ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 認可這個預存程序所採取的動作可能需要重新初始化現有的訂閱。 *force_reinit_subscription*是**元**預設值是**0**。  
  - **0**指定發行項的變更不會使訂閱重新初始化。 如果預存程序偵測到變更需要重新初始化現有的訂閱，就會發生錯誤，且不會進行任何變更。  
  - **1**指定發行項的變更會使現有的訂閱重新初始化，並提供發生訂閱重新初始化的權限。  
  
[ **@publisher** = ] **'***publisher***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是**sysname**，預設值是 NULL。  
  
  > [!NOTE]  
  >  *發行者*應該不在上變更發行項屬性時才使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 **sp_changepublication**用於快照式複寫和異動複寫。  
  
 在變更之後的任何下列的屬性，您必須產生新的快照集，而且您必須指定值為**1**如*force_invalidate_snapshot*參數。  
-   **alt_snapshot_folder**  
-   **compress_snapshot**  
-   **enabled_for_het_sub**  
-   **ftp_address**  
-   **ftp_login**  
-   **ftp_password**  
-   **ftp_port**  
-   **ftp_subdirectory**  
-   **post_snapshot_script**  
-   **pre_snapshot_script**  
-   **snapshot_in_defaultfolder**  
-   **sync_mode**  
  
在 Active Directory 中使用清單發行集物件**publish_to_active_directory**參數，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必須已在 Active Directory 中建立物件。  
  
## <a name="impact-of-immediate-sync"></a>立即同步的影響  
 立即同步時，即使沒有任何訂用帳戶產生初始快照集之後，立即追蹤記錄檔中的所有變更。 客戶在使用備份，若要加入新的對等節點時，會使用記錄的變更。 還原備份之後，對等會進行同步處理的任何備份之後發生的變更。 因為散發資料庫中追蹤命令，則同步處理邏輯可以查看上次備份 LSN，並以此做為起點，瞭解此命令使用備份的最大保留期限內。 (預設值的最小保留期限為 0 小時，而最大保留期限為 24 小時。)  
  
 當立即同步關閉時，變更就會至少保留的最小保留期限，然後立即清除所有已複寫的交易。 如果立即同步已關閉，而且設定了預設保留期限，系統可能會清除建立備份之後發生的必要變更，而且新的對等節點不會正確初始化。 剩下的唯一選項就是停止拓撲。 將立即同步設定為開啟可提供較大的彈性，建議您針對 P2P 複寫設定此選項。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_changepublication](../../relational-databases/replication/codesnippet/tsql/sp-changepublication-tra_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有成員**sysadmin**固定的伺服器角色或**db_owner**固定的資料庫角色可以執行**sp_changepublication**。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [變更發行集與發行項屬性](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addpublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_droppublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
