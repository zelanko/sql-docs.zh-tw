---
title: sysmergepublications (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergepublications
- sysmergepublications_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepublications system table
ms.assetid: 7f82c6c3-22d1-47c0-a92b-4d64b98cc455
author: stevestein
ms.author: sstein
ms.openlocfilehash: 9a2c2802f0bd077c64800225590b2346205fb30a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68029786"
---
# <a name="sysmergepublications-transact-sql"></a>sysmergepublications (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對資料庫中每個已定義的合併式發行集，各包含一個資料列。 這份資料表儲存在發行集和訂閱資料庫中。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**發行者**|**sysname**|預設伺服器的名稱。|  
|**publisher_db**|**sysname**|預設發行者資料庫的名稱。|  
|**name**|**sysname**|發行集的名稱。|  
|**description**|**nvarchar(255)**|發行集的簡要描述。|  
|**retention**|**int**|整個發行集，其中單元會以值的保留期限**retention_period_unit**資料行。|  
|**publication_type**|**tinyint**|指出發行集的篩選：<br /><br /> **0** = 未篩選。<br /><br /> **1** = 篩選。|  
|**pubid**|**uniqueidentifier**|這個發行集的唯一識別碼。 這是加入發行集時產生的識別碼。|  
|**designmasterid**|**uniqueidentifier**|保留供日後使用。|  
|**parentid**|**uniqueidentifier**|指出從中建立目前的對等或子集發行集 (用於階層式發行拓撲) 的父發行集。|  
|**sync_mode**|**tinyint**|這個發行集的同步處理模式：<br /><br /> **0** = native。<br /><br /> **1** = 字元。|  
|**allow_push**|**int**|指出發行集是否允許發送訂閱。<br /><br /> **0** = 不允許發送訂閱。<br /><br /> **1** = 允許的發送訂閱。|  
|**allow_pull**|**int**|指出發行集是否允許提取訂閱。<br /><br /> **0** = 不允許提取訂閱。<br /><br /> **1** = 允許的提取訂閱。|  
|**allow_anonymous**|**int**|指出發行集是否允許匿名訂閱。<br /><br /> **0** = 不允許匿名訂閱。<br /><br /> **1** = 匿名允許訂用帳戶。|  
|**centralized_conflicts**|**int**|指出衝突記錄是否會儲存在發行者端：<br /><br /> **0** = 將衝突記錄不會儲存在 「 發行者 」。<br /><br /> **1** = 將衝突記錄儲存在 「 發行者 」。|  
|**status**|**tinyint**|保留供日後使用。|  
|**snapshot_ready**|**tinyint**|指出發行集快照集的狀態：<br /><br /> **0** = 快照集未備妥可用。<br /><br /> **1** = 快照集可供使用。<br /><br /> **2** = 這個發行集必須先建立新的快照集。|  
|**enabled_for_internet**|**bit**|指出是否利用 FTP 和其他服務，在網際網路中公開發行集的同步處理檔案。<br /><br /> **0** = 檔案可以從網際網路存取的同步處理。<br /><br /> **1** = 同步處理無法從網際網路存取的檔案。|  
|**dynamic_filters**|**bit**|指出是否利用參數化資料列篩選器來篩選發行集。<br /><br /> **0** = 發行集未篩選資料列。<br /><br /> **1** = 發行集篩選資料列。|  
|**snapshot_in_defaultfolder**|**bit**|指定是否將快照集檔案儲存在預設資料夾中。<br /><br /> **0** = 快照集檔案的預設資料夾中。<br /><br /> **1** = 快照集檔案會儲存在所指定的位置**alt_snapshot_folder**。|  
|**alt_snapshot_folder**|**nvarchar(255)**|快照集替代資料夾的位置。|  
|**pre_snapshot_script**|**nvarchar(255)**|指標。**sql**套用在訂閱者的快照集時，指令碼檔案，「 合併代理程式之前，執行任何複寫的物件。|  
|**post_snapshot_script**|**nvarchar(255)**|指標。**sql**執行合併代理程式在所有其他複寫物件指令碼，並在初始同步處理期間，套用資料的檔案。|  
|**compress_snapshot**|**bit**|指定是否寫入快照集**alt_snapshot_folder**位置壓縮成[!INCLUDE[msCoName](../../includes/msconame-md.md)]CAB 格式。 **0**指定不壓縮檔案。|  
|**ftp_address**|**sysname**|散發者的檔案傳輸通訊協定 (FTP) 服務的網路位址。 指定發行集快照集檔案所在的位置，以便在啟用 FTP 的情況下，合併代理程式能夠加以收取。|  
|**ftp_port**|**int**|散發者的 FTP 服務通訊埠編號。|  
|**ftp_subdirectory**|**nvarchar(255)**|合併代理程式能夠從中收取快照集檔案的子目錄。|  
|**ftp_login**|**sysname**|用來連接到 FTP 服務的使用者名稱。|  
|**ftp_password**|**nvarchar(524)**|用來連接到 FTP 服務的使用者密碼。|  
|**conflict_retention**|**int**|指定衝突的保留期限 (以天為單位)。 在這段時間之後，會從衝突資料表中清除衝突資料列。|  
|**keep_before_values**|**int**|指定這個發行集是否進行最佳化的同步處理：<br /><br /> **0** = 同步處理未最佳化，並將驗證傳送給所有訂閱者資料分割，資料分割中的資料變更時。<br /><br /> **1** = 同步處理最佳化，且只有擁有已變更的資料分割中的資料列的訂閱者會受到影響。|  
|**allow_subscription_copy**|**bit**|指定是否已啟用複製訂閱資料庫的能力。 **0**表示不允許複製。|  
|**allow_synctoalternate**|**bit**|指定是否允許替代的同步處理夥伴與這個發行者同步。 **0**表示不允許同步夥伴。|  
|**validate_subscriber_info**|**nvarchar(500)**|列出用於擷取訂閱者資訊以及驗證訂閱者參數化資料列篩選器準則的函數。|  
|**ad_guidname**|**sysname**|指定發行集是否在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Active Directory 中發行。 有效的 GUID 指定發行集發行在 Active Directory 中，GUID 是對應的 Active Directory 發行集物件**objectGUID**。 如果是 NULL，發行集就不會發行在 Active Directory 中。|  
|**backward_comp_level**|**int**|資料庫相容性層級。 可為下列其中一個值：<br /><br /> **90** = [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].<br /><br /> **100** = [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].|  
|**max_concurrent_merge**|**int**|允許使用的最大並行合併處理序數目。 值為**0**的這個屬性表示會在任何給定時間執行的並行合併處理序數目沒有限制。 這個屬性會設定能夠針對合併式發行集來同時執行的並行合併處理序的數目限制。 如果排程同時執行的快照集處理序數目超出允許執行的值，超出的作業便會放在佇列中，等到目前在執行中的合併處理序完成為止。|  
|**max_concurrent_dynamic_snapshots**|**int**|允許針對合併式發行集來執行的最大並行已篩選資料快照集工作階段數目。 如果**0**，能夠同時針對的發行集之任何指定時間執行的並行已篩選的資料快照集工作階段最大數目沒有限制。 這個屬性會設定能夠針對合併式發行集來同時執行的並行快照集處理序的數目限制。 如果排程同時執行的快照集處理序數目超出允許執行的值，超出的作業便會放在佇列中，等到目前在執行中的合併處理序完成為止。|  
|**use_partition_groups**|**smallint**|指定發行集是否使用預先計算的資料分割。|  
|**dynamic_filters_function_list**|**nvarchar(500)**|發行集的參數化資料列篩選器所用的函數清單 (用分號分隔)。|  
|**partition_id_eval_proc**|**sysname**|指定訂閱者的合併代理程式為了判斷指派的資料分割識別碼而執行的程序名稱。|  
|**publication_number**|**smallint**|指定識別欄位來提供與的 2 位元組對應**pubid**。 **pubid**是全域唯一識別碼是發行集，但發行集號碼是唯一只在指定的資料庫。|  
|**replicate_ddl**|**int**|指出是否支援發行集的結構描述複寫。<br /><br /> **0** = DDL 陳述式不會複寫。<br /><br /> **1** = DDL 複寫在發行者端執行的陳述式。<br /><br /> 如需詳細資訊，請參閱[對發行集資料庫進行結構描述變更](../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)。|  
|**allow_subscriber_initiated_snapshot**|**bit**|指出訂閱者能夠起始利用參數化篩選來產生發行集快照集的處理序。 **1**指出訂閱者可以起始快照集處理。|  
|**dynamic_snapshot_queue_timeout**|**int**|指定在使用參數化篩選時，訂閱者必須在佇列中等待快照集產生程序開始的分鐘數。|  
|**dynamic_snapshot_ready_timeout**|**int**|指定在使用參數化篩選時，訂閱者等待快照集產生程序完成的分鐘數。|  
|**散發者**|**sysname**|發行集散發者的名稱。|  
|**snapshot_jobid**|**binary(16)**|識別在訂閱者能夠起始快照集產生程序時，產生快照集的代理程式作業。|  
|**allow_web_synchronization**|**bit**|指定是否要將發行集啟用 Web 同步處理，其中**1**表示發行集啟用 Web 同步處理。|  
|**web_synchronization_url**|**nvarchar(500)**|指定 Web 同步處理所用的網際網路 URL 預設值。|  
|**allow_partition_realignment**|**bit**|指出當修改發行者的資料列造成資料分割的變更時，是否要將刪除動作傳給訂閱者。<br /><br /> **0** = 資料從舊分割區會保留在 「 訂閱者 」，其中這項資料在 「 發行者 」 上所做的變更將不會複寫到這個訂閱者，但在 「 訂閱者 」 上所做的變更會複寫到 「 發行者 」 上。<br /><br /> **1** = 刪除導引到 「 訂閱者 」，以反映資料分割變更的結果來移除已不在訂閱者資料分割的資料。<br /><br /> 如需詳細資訊，請參閱 < [sp_addmergepublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。<br /><br /> 注意:此值時，會保持在 「 訂閱者 」 的資料**0**應該視為如同它是唯讀狀態; 不過，這不會嚴格強制執行複寫系統。|  
|**retention_period_unit**|**tinyint**|定義用來定義時的單位*保留*，它可以是下列值之一：<br /><br /> **0** = 日。<br /><br /> **1** = 週。<br /><br /> **2** = 月。<br /><br /> **3** = 年。|  
|**decentralized_conflicts**|**int**|指出是否將衝突記錄儲存在造成衝突的訂閱者端：<br /><br /> **0** = 將衝突記錄不會儲存在 「 訂閱者 」。<br /><br /> **1** = 將衝突記錄儲存在 「 訂閱者 」。|  
|**generation_leveling_threshold**|**int**|指定某個層代中包含的變更數目。 層代是指傳遞給發行者或訂閱者的變更集合。|  
|**automatic_reinitialization_policy**|**bit**|指出在自動重新初始化之前，是否從訂閱者上傳變更。<br /><br /> **1** = 上傳變更從訂閱者的自動重新初始化發生之前。<br /><br /> **0** = 在自動重新初始化之前將不會上傳變更。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_changemergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)  
  
  
