---
description: sp_helppublication (Transact-SQL)
title: sp_helppublication (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helppublication_TSQL
- sp_helppublication
helpviewer_keywords:
- sp_helppublication
ms.assetid: e801c3f0-dcbd-4b4a-b254-949a05f63518
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: dd5452439cc3467cc840ac11dd9ce3cf880a4ce8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489301"
---
# <a name="sp_helppublication-transact-sql"></a>sp_helppublication (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  傳回有關發行集的資訊。 針對 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行集，這個預存程式會在發行集資料庫的發行者上執行。 如果是 Oracle 發行集，這個預存程序執行於任何資料庫中的散發者端。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
sp_helppublication [ [ @publication = ] 'publication' ]  
    [ , [ @found=] found OUTPUT]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>引數  
`[ @publication = ] 'publication'` 這是要查看的發行集名稱。 *發行* 集是 sysname，預設值是，它會傳回所有發行集的 **%** 相關資訊。  
  
`[ @found = ] 'found' OUTPUT` 這是表示傳回資料列的旗標。 *找到* **int** 和 OUTPUT 參數，預設值是 **23456**。 **1** 表示找到發行集。 **0** 表示找不到發行集。  
  
`[ @publisher = ] 'publisher'` 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者。 *publisher* 是 sysname，預設值是 Null。  
  
> [!NOTE]  
>  當要求發行者的發行集資訊時，不應指定*發行者* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
## <a name="result-sets"></a>結果集  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|pubid|**int**|發行集的識別碼。|  
|NAME|**sysname**|發行集的名稱。|  
|restricted|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**tinyint**|發行集的目前狀態。<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用中。|  
|工作 (task)||使用這個項目的目的，是為了與舊版相容。|  
|replication frequency|**tinyint**|複寫頻率的類型：<br /><br /> **0** = 交易式<br /><br /> **1** = 快照集|  
|synchronization method|**tinyint**|同步模式：<br /><br /> **0** = 原生大量複製程式 (**bcp** 公用程式) <br /><br /> **1** = 字元大量複製<br /><br /> **3** = 並行，表示使用原生大量複製 (**bcp**公用程式) ，但在快照集期間，不鎖定資料表<br /><br /> **4** = Concurrent_c，這表示使用的是字元大量複製，但在快照集期間，不鎖定資料表|  
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
|has subscription|**bit**|發行集是否有使用中的訂閱。 **1** 表示發行集有使用中的訂閱，而 **0** 表示發行集沒有訂閱。|  
|allow_queued_tran|**bit**|指定是否停用在訂閱者端將變更放入佇列中，直到可以在發行者端套用這些變更為止。 如果是 **0**，就不會將訂閱者端的變更排入佇列。|  
|snapshot_in_defaultfolder|**bit**|指定是否將快照集檔案儲存在預設資料夾中。 如果是 **0**，快照集檔案會儲存在 *alternate_snapshot_folder*所指定的替代位置。 如果是 **1**，便可以在預設資料夾中找到快照集檔案。|  
|alt_snapshot_folder|**nvarchar(255)**|指定快照集替代資料夾的位置。|  
|pre_snapshot_script|**nvarchar(255)**|指定 **.sql** 檔案位置的指標。 在訂閱者端套用快照集時，散發代理程式會在執行任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。|  
|post_snapshot_script|**nvarchar(255)**|指定 **.sql** 檔案位置的指標。 在初始同步處理期間，散發代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。|  
|compress_snapshot|**bit**|指定將寫入 *alt_snapshot_folder* 位置的快照集壓縮成 [!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 格式。 **0** 指定不壓縮快照集。|  
|ftp_address|**sysname**|散發者之 FTP 服務的網路位址。 指定發行集快照集檔案所在的位置，以便訂閱者的散發代理程式或合併代理程式能夠加以收取。|  
|ftp_port|**int**|散發者的 FTP 服務通訊埠編號。|  
|ftp_subdirectory|**nvarchar(255)**|指定在發行集支援利用 FTP 來傳播快照集時，供訂閱者的散發代理程式或合併代理程式從中收取快照集檔案的位置。|  
|ftp_login|**sysname**|用於連接到 FTP 服務的使用者名稱。|  
|allow_dts|**bit**|指定發行集允許資料轉換。 **0** 指定不允許 DTS 轉換。|  
|allow_subscription_copy|**bit**|指定是否已啟用複製訂閱這個發行集之訂閱資料庫的能力。 **0** 表示不允許複製。|  
|centralized_conflicts|**bit**|指定是否將衝突記錄儲存在發行者端：<br /><br /> **0** = 衝突記錄同時儲存在發行者端和造成衝突的訂閱者端。<br /><br /> **1** = 將衝突記錄儲存在發行者端。|  
|conflict_retention|**int**|指定衝突保留週期 (以天為單位)。|  
|conflict_policy|**int**|指定使用佇列更新訂閱者選項時，所遵照的衝突解決原則。 它可以是下列值之一：<br /><br /> **1** = 發行者在衝突中獲勝。<br /><br /> **2** = 訂閱者在衝突中獲勝。<br /><br /> **3** = 重新初始化訂閱。|  
|queue_type||指定所用的佇列類型。 它可以是下列值之一：<br /><br /> **msmq** = 使用 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 訊息佇列來儲存交易。<br /><br /> **sql** = 用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 來儲存交易。<br /><br /> 注意：已停止支援訊息佇列。|  
|backward_comp_level||資料庫相容性層級，它可以是下列項目之一：<br /><br /> **90**  =  90 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]<br /><br /> **100**  =  100 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
|publish_to_AD|**bit**|指定發行集是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中發行。 值為 **1** 表示已發佈，值為 **0** 表示不會發行。|  
|allow_initialize_from_backup|**bit**|指出訂閱者是否能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 **1** 表示可以從備份初始化訂閱， **0** 表示它們不能。 如需詳細資訊，請參閱在不含快照集的情況下初始化交易式 [訂閱（不](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) 含快照集）。|  
|replicate_ddl|**int**|指出是否支援發行集的結構描述複寫。 **1** 表示複寫在發行者端執行的資料定義語言 (DDL) 語句， **0** 表示不復寫 ddl 語句。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|enabled_for_p2p|**int**|發行集是否可用於點對點複寫拓撲中。 **1** 表示發行集支援點對點複寫。 如需相關資訊，請參閱 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)。|  
|publish_local_changes_only|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|enabled_for_het_sub|**int**|指定發行集是否支援非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 訂閱者。 **1**值表示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援非訂閱者。 值為 **0** 表示只 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支援訂閱者。 如需詳細資訊，請參閱 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)。|  
|enabled_for_p2p_conflictdetection|**int**|指定散發代理程式是否會偵測啟用點對點複寫之發行集的衝突。 **1**值表示偵測到衝突。 如需相關資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
|originator_id|**int**|針對點對點拓撲中的節點指定識別碼。 如果 **enabled_for_p2p_conflictdetection** 設定為 **1**，此識別碼就會用於衝突偵測。 如需已經使用的識別碼清單，請查詢 [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md) 系統資料表。|  
|p2p_continue_onconflict|**int**|指定散發代理程式是否會在偵測到衝突時繼續處理變更。 **1**值表示代理程式會繼續處理變更。<br /><br /> 請**0** ** \* \* \* 注意 \* ** ，我們建議您使用預設值0。 當這個選項設定為 **1**時，散發代理程式會嘗試從具有最高擁有者識別碼的節點套用衝突資料列，藉以在拓撲中將資料聚合。 但是，這個方法無法保證聚合。 您應該確定在偵測到衝突之後，拓撲是一致的。 如需詳細資訊，請參閱＜ [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)＞中的「處理衝突」。|  
|allow_partition_switch|**int**|指定 ALTER TABLE .。。SWITCH 語句可以針對已發行的資料庫執行。 如需詳細資訊，請參閱[複寫資料分割資料表及索引](../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md)。|  
|replicate_partition_switch|**int**|指定 ALTER TABLE .。。針對已發行資料庫執行的 SWITCH 語句應複寫至「訂閱者」。 只有當 *allow_partition_switch* 設定為 **1**時，此選項才有效。|  
  
## <a name="return-code-values"></a>傳回碼值  
 **0** (成功) 或 **1** (失敗)   
  
## <a name="remarks"></a>備註  
 sp_helppublication 用於快照式和異動複寫中。  
  
 sp_helppublication 會傳回執行這個程序之使用者所擁有的所有發行集資訊。  
  
## <a name="example"></a>範例  
 [!code-sql[HowTo#sp_helppublication](../../relational-databases/replication/codesnippet/tsql/sp-helppublication-trans_1.sql)]  
  
## <a name="permissions"></a>權限  
 只有發行者端的系統管理員 (sysadmin) 固定伺服器角色成員、發行集資料庫的 db_owner 固定資料庫角色成員，或發行集存取清單 (PAL) 中的使用者，才能夠執行 sp_helppublication。  
  
 如果是非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 發行者，只有散發者端之系統管理員（sysadmin）固定伺服器角色的成員，或是散發資料庫上 db_owner 固定資料庫角色的成員，或 PAL 中的使用者，才能夠執行 sp_helppublication。  
  
## <a name="see-also"></a>另請參閱  
 [檢視及修改發行集屬性](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_droppublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
