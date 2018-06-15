---
title: sp_helppublication (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 532c1d371596cff80a547414a316ed0ec401728a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "33003475"
---
# <a name="sphelppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關發行集的資訊。 如[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行集，此預存程序在發行集資料庫的發行者上執行。 如果是 Oracle 發行集，這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
 [ **@publication =** ] **'***publication***'**  
 這是要檢視的發行集名稱。 *發行集*是 sysname，預設值是**%**，它會傳回有關所有發行集的資訊。  
  
 [  **@found =** ] **'***找到***'** 輸出  
 這是表示傳回資料列的旗標。 *找到*是**int**和一個 OUTPUT 參數，預設值是**23456**。 **1**表示找到發行集。 **0**指出找不到發行集。  
  
 [ **@publisher** = ] **'***publisher***'**  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *發行者*是 sysname，預設值是 NULL。  
  
> [!NOTE]  
>  *發行者*應要求從發行集資訊時未指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]發行者。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|pubid|**int**|發行集的識別碼。|  
|name|**sysname**|發行集的名稱。|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|發行集的目前狀態。<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用。|  
|工作 (task)||使用這個項目的目的，是為了與舊版相容。|  
|replication frequency|**tinyint**|複寫頻率的類型：<br /><br /> **0** = 交易式<br /><br /> **1** = 快照集|  
|synchronization method|**tinyint**|同步模式：<br /><br /> **0** = 原生大量複製程式 (**bcp**公用程式)<br /><br /> **1** = 字元大量複製<br /><br /> **3** = concurrent，表示該原生大量複製 (**bcp**公用程式) 使用，但在快照集期間，不鎖定資料表<br /><br /> **4** = Concurrent_c，表示使用字元大量複製，但在快照集期間，不鎖定資料表|  
|description|**nvarchar(255)**|發行集的選擇性描述。|  
|immediate_sync|**bit**|每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案。|  
|enabled_for_internet|**bit**|是否利用檔案傳輸通訊協定 (FTP) 和其他服務，在網際網路中公開發行集的同步處理檔案。|  
|allow_push|**bit**|發行集是否允許發送訂閱。|  
|allow_pull|**bit**|發行集是否允許提取訂閱。|  
|allow_anonymous|**bit**|發行集是否允許匿名訂閱。|  
|independent_agent|**bit**|這個發行集是否有獨立的散發代理程式。|  
|immediate_sync_ready|**bit**|快照代理程式是否要產生快照集供新訂閱使用。 只有在發行集設定成隨時都有快照供新的訂閱或重新初始化的訂閱使用時，才會定義這個參數。|  
|allow_sync_tran|**bit**|發行集是否允許立即更新訂閱。|  
|autogen_sync_procs|**bit**|是否要自動產生預存程序，以支援立即更新訂閱。|  
|snapshot_jobid|**binary(16)**|排程工作識別碼。|  
|retention|**int**|給定發行集的變更儲存量 (以小時為單位)。|  
|has subscription|**bit**|發行集是否有使用中的訂閱。 **1**表示發行集有使用中的訂閱和**0**表示發行集沒有訂閱。|  
|allow_queued_tran|**bit**|指定是否停用在訂閱者端將變更放入佇列中，直到可以在發行者端套用這些變更為止。 如果**0**，「 訂閱者 」 端的變更不會排入佇列。|  
|snapshot_in_defaultfolder|**bit**|指定是否將快照集檔案儲存在預設資料夾中。 如果**0**，快照集檔案已儲存在所指定的替代位置*alternate_snapshot_folder*。 如果**1**，可以在預設資料夾中找到快照集檔案。|  
|alt_snapshot_folder|**nvarchar(255)**|指定快照集替代資料夾的位置。|  
|pre_snapshot_script|**nvarchar(255)**|指定指向 **.sql**檔案位置。 在訂閱者端套用快照集時，散發代理程式會在執行任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。|  
|post_snapshot_script|**nvarchar(255)**|指定指向 **.sql**檔案位置。 在初始同步處理期間，散發代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。|  
|compress_snapshot|**bit**|指定可寫入快照集*alt_snapshot_folder*位置是壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 **0**指定不壓縮快照集。|  
|ftp_address|**sysname**|散發者之 FTP 服務的網路位址。 指定發行集快照集檔案所在的位置，以便訂閱者的散發代理程式或合併代理程式能夠加以收取。|  
|ftp_port|**int**|散發者的 FTP 服務通訊埠編號。|  
|ftp_subdirectory|**nvarchar(255)**|指定在發行集支援利用 FTP 來傳播快照集時，供訂閱者的散發代理程式或合併代理程式從中收取快照集檔案的位置。|  
|ftp_login|**sysname**|用於連接到 FTP 服務的使用者名稱。|  
|allow_dts|**bit**|指定發行集允許資料轉換。 **0**指定不允許 DTS 轉換。|  
|allow_subscription_copy|**bit**|指定是否已啟用複製訂閱這個發行集之訂閱資料庫的能力。 **0**表示不允許複製。|  
|centralized_conflicts|**bit**|指定是否將衝突記錄儲存在發行者端：<br /><br /> **0** = 將衝突記錄儲存在發行者端和造成衝突的訂閱者端。<br /><br /> **1** = 將衝突記錄儲存在發行者端。|  
|conflict_retention|**int**|指定衝突保留週期 (以天為單位)。|  
|conflict_policy|**int**|指定使用佇列更新訂閱者選項時，所遵照的衝突解決原則。 它可以是下列值之一：<br /><br /> **1** = 發行者優先衝突。<br /><br /> **2** = 訂閱者優先衝突。<br /><br /> **3** = 重新初始化訂閱。|  
|queue_type||指定所用的佇列類型。 它可以是下列值之一：<br /><br /> **msmq** = 使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]Message Queuing 來儲存交易。<br /><br /> **sql** = 使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來儲存交易。<br /><br /> 注意： 已不再支援訊息佇列。|  
|backward_comp_level||資料庫相容性層級，它可以是下列項目之一：<br /><br /> **90** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100** = [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|指定發行集是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory™ 中發行。 值為**1**表示它會發行，而值為**0**表示不發行。|  
|allow_initialize_from_backup|**bit**|指出訂閱者是否能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 **1**表示，從備份初始化訂閱並**0**表示無法。 如需詳細資訊，請參閱[初始化交易式訂閱不使用快照集](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)不使用快照集的交易式訂閱者。|  
|replicate_ddl|**int**|指出是否支援發行集的結構描述複寫。 **1**表示複寫在發行者端執行的資料定義語言 (DDL) 陳述式，和**0**表示不複寫 DDL 陳述式。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|enabled_for_p2p|**int**|發行集是否可用於點對點複寫拓撲中。 **1**表示發行集支援端對端複寫。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|指定發行集是否支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 值為**1**表示非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援訂閱者。 值為**0**即表示只有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]支援訂閱者。 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。|  
|enabled_for_p2p_conflictdetection|**int**|指定散發代理程式是否會偵測啟用點對點複寫之發行集的衝突。 值為**1**表示會偵測衝突。 如需詳細資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|originator_id|**int**|針對點對點拓撲中的節點指定識別碼。 此識別碼用於衝突偵測，如果**enabled_for_p2p_conflictdetection**設**1**。 如需已經使用的識別碼清單，請查詢 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系統資料表。|  
|p2p_continue_onconflict|**int**|指定散發代理程式是否會在偵測到衝突時繼續處理變更。 值為**1**表示代理程式會繼續處理變更。<br /><br /> **\*\* 注意： \* \*** 我們建議您使用的預設值**0**。 當此選項設定為**1**，散發代理程式嘗試聚合拓撲中的資料，藉由套用衝突的資料列從節點具有最高訂閱者識別碼。 但是，這個方法無法保證聚合。 您應該確定在偵測到衝突之後，拓撲是一致的。 如需詳細資訊，請參閱＜ [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)＞中的「處理衝突」。|  
|alllow_partition_switch|**int**|指定 ALTER TABLE…SWITCH 陳述式是否可以針對發行的資料庫來執行。 如需詳細資訊，請參閱[複寫資料分割資料表及索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
|replicate_partition_switch|**int**|指定針對發行資料庫執行的 ALTER TABLE…SWITCH 陳述式是否應該複寫到訂閱者。 這個選項才有效才*allow_partition_switch*設**1**。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** （成功） 或**1** （失敗）  
  
## <a name="remarks"></a>備註  
 sp_helppublication 用於快照式和異動複寫中。  
  
 sp_helppublication 會傳回執行這個程序之使用者所擁有的所有發行集資訊。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有發行者端的系統管理員 (sysadmin) 固定伺服器角色成員、發行集資料庫的 db_owner 固定資料庫角色成員，或發行集存取清單 (PAL) 中的使用者，才能夠執行 sp_helppublication。  
  
 如果是非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者，只有散發者端的系統管理員 (sysadmin) 固定伺服器角色成員、散發資料庫的 db_owner 固定資料庫角色成員，或 PAL 中的使用者，才能夠執行 sp_helppublication。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
