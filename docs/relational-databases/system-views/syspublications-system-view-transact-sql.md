---
title: syspublications （系統檢視）（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- syspublications
- syspublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syspublications view
ms.assetid: e5f57c32-efc0-4455-a74f-684dc2ae51f8
author: stevestein
ms.author: sstein
ms.openlocfilehash: f1724f86f9bfc34e505b9ba6ecddae4104270cd0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094773"
---
# <a name="syspublications-system-view-transact-sql"></a>syspublications (系統檢視) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Syspublications** view 會公開發行集資訊。 這份檢視儲存在散發資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**描述**|**nvarchar(255)**|發行集的描述性項目。|  
|**name**|**sysname**|與發行集相關聯的唯一名稱。|  
|**pubid**|**int**|提供發行集唯一識別碼的識別欄位。|  
|**repl_freq**|**tinyint**|複寫頻率：<br /><br /> **0** = 以交易為基礎（交易式）。<br /><br /> **1** = 已排程的資料表重新整理（快照集）。|  
|**狀態**|**tinyint**|發行集狀態：<br /><br /> **0** = 非使用中。<br /><br /> **1** = 使用中。|  
|**sync_method**|**tinyint**|同步處理方法：<br /><br /> **0** = 原生大量複製程式公用程式（BCP）。<br /><br /> **1** = 字元 BCP。<br /><br /> **3** = 並行，這表示會使用原生 BCP，但在快照集期間，不會鎖定資料表。<br /><br /> **4** = Concurrent_c，這表示會使用字元 BCP，但在快照集期間，不會鎖定資料表。|  
|**snapshot_jobid**|**binary （16）**|識別已排程要產生初始快照集的代理程式作業。|  
|**independent_agent**|**bit**|指定這個發行集是否有獨立的散發代理程式。<br /><br /> **0** = 發行集使用共用的散發代理程式，而且每個發行者資料庫/訂閱者資料庫配對都有單一的共用代理程式。<br /><br /> **1** = 此發行集有一個獨立的散發代理程式。|  
|**immediate_sync**|**bit**|指出每次執行快照集代理程式時，是否要建立或重新建立同步處理檔案， **1**表示每次執行代理程式時都會建立它們。|  
|**enabled_for_internet**|**bit**|指出發行集的同步處理檔案是否透過檔案傳輸協定（FTP）和其他服務公開到網際網路，其中**1**表示可以從網際網路存取。|  
|**allow_push**|**bit**|指出發行集是否允許發送訂閱， **1**表示允許。|  
|**allow_pull**|**bit**|指出發行集是否允許提取訂閱，其中**1**表示允許。|  
|**allow_anonymous**|**bit**|指出發行集是否允許匿名訂閱， **1**表示允許。|  
|**immediate_sync_ready**|**bit**|指出快照集代理程式是否已產生快照集，且快照集是否已備妥，可供新的訂閱使用。 它只對立即更新發行集有意義。 **1**表示快照集已就緒。|  
|**allow_sync_tran**|**bit**|指定是否允許發行集使用立即更新訂閱。 **1**表示允許立即更新訂閱。|  
|**autogen_sync_procs**|**bit**|指定是否在發行者端產生立即更新訂閱的同步處理預存程序。 **1**表示它是在發行者端產生。|  
|**保存**|**int**|在散發資料庫中維護發行集變更的時間量 (以小時為單位)。|  
|**allow_queued_tran**|**bit**|指定是否已啟用在訂閱者端將變更放入佇列中，直到可以在發行者端套用這些變更為止。 如果是**1**，就會將訂閱者端的變更排入佇列。|  
|**snapshot_in_defaultfolder**|**bit**|指定是否將快照集檔案儲存在預設資料夾中。 如果是**0**，快照集檔案就會儲存在*alternate_snapshot_folder*所指定的替代位置中。 如果是 1，便可以在預設資料夾中找到快照集檔案。|  
|**alt_snapshot_folder**|**Nvarchar （510）**|指定快照集替代資料夾的位置。|  
|**pre_snapshot_script**|**Nvarchar （510）**|指定 **.sql**檔案位置的指標。 在訂閱者端套用快照集時，散發代理程式會在執行任何複寫的物件指令碼之前，先執行前快照集 (pre-snapshot) 指令碼。|  
|**post_snapshot_script**|**Nvarchar （510）**|指定 **.sql**檔案位置的指標。 在初始同步處理期間，散發代理程式會先套用所有其他複寫的物件指令碼和資料，然後才執行後快照集 (post-snapshot) 指令碼。|  
|**compress_snapshot**|**bit**|指定要將寫入*alt_snapshot_folder*位置的快照集壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)] CAB 格式。 **1**表示將壓縮快照集。|  
|**ftp_address**|**sysname**|散發者之 FTP 服務的網路位址。 指定發行集快照集檔案所在的位置，以便散發代理程式能夠加以收取。|  
|**ftp_port**|**int**|散發者的 FTP 服務通訊埠編號。 指定發行集快照集檔案所在的位置，以便散發代理程式能夠加以收取。|  
|**ftp_subdirectory**|**Nvarchar （510）**|指定在發行集支援利用 FTP 來傳播快照集時，散發代理程式能夠從中收取快照集檔案的位置。|  
|**ftp_login**|**nvarchar(256)**|用於連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**Nvarchar （1048）**|用來連接到 FTP 服務的使用者密碼。|  
|**allow_dts**|**bit**|指定發行集是否允許進行 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] Data Transformation Services (DTS) 轉換。 **1**指定允許 DTS 轉換。|  
|**allow_subscription_copy**|**bit**|指定是否已啟用複製訂閱這個發行集之訂閱資料庫的能力。 **1**表示允許複製。|  
|**centralized_conflicts**|**bit**|指定是否將衝突記錄儲存在發行者端：<br /><br /> **0** = 衝突記錄會同時儲存在發行者端和造成衝突的訂閱者端。<br /><br /> **1** = 衝突記錄儲存在發行者端。|  
|**conflict_retention**|**int**|指定衝突記錄的保留期限 (以天為單位)。|  
|**conflict_policy**|**int**|指定使用佇列更新訂閱者選項時，所遵照的衝突解決原則。 它可以是下列值之一：<br /><br /> **1** = 發行者在衝突中獲勝。<br /><br /> **2** = 訂閱者在衝突中獲勝。<br /><br /> **3** = 重新初始化訂閱。|  
|**queue_type**|**int**|指定所用的佇列類型。 它可以是下列值之一：<br /><br /> **1** =. msmq，使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]訊息佇列來儲存交易。<br /><br /> **2** = .sql，用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]來儲存交易。<br /><br /> 注意：使用[!INCLUDE[msCoName](../../includes/msconame-md.md)]訊息佇列已被取代，不再受到支援。|  
|**ad_guidname**|**sysname**|指定發行集是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中發行。 有效的全域唯一識別碼 (GUID) 指定發行集發行在 Active Directory 中，GUID 是對應的 Active Directory 發行集物件 objectGUID。 如果是 NULL，發行集就不會發行在 Active Directory 中。<br /><br /> 注意：不再支援發行至 Active Directory。|  
|**backward_comp_level**|**int**|資料庫相容性層級，它可以是下列值之一：<br /><br /> ****  = 90[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。<br /><br /> ****  = 100[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]。|  
|**allow_initialize_from_backup**|**bit**|指出訂閱者是否能夠從備份中，而不是從初始快照集中，對這個發行集的訂閱進行初始化。 **1**表示可以從備份初始化訂閱，而**0**表示它們不能。 如需詳細資訊，請參閱 [不使用快照集初始化交易式訂閱](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)中手動初始化訂閱。|  
|**min_autonosync_lsn**|**二進位（1）**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**replicate_ddl**|**int**|指出是否支援發行集的結構描述複寫。<br /><br /> **1** = 複寫在發行者端執行的 DDL 語句。<br /><br /> **0** = 表示不復寫 DDL 語句。 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|**選項**|**int**|指定其他發行選項的點陣圖，位元選項值如下：<br /><br /> **0x1** -啟用點對點複寫。<br /><br /> **0x2** -僅發行對等複寫的本機變更。<br /><br /> **0x4** -針對非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]訂閱者啟用。<br /><br /> **0x8** -啟用點對點衝突偵測。|  
|**originator_id**|**smallint**|針對衝突偵測的目的，識別點對點複寫拓撲中的每個節點。 如需相關資訊，請參閱 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表 &#40;Transact-sql&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addpublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)   
 [sp_helppublication &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)  
  
  
