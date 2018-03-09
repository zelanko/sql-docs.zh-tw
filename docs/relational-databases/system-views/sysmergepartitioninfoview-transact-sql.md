---
title: "sysmergepartitioninfoview (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergepartitioninfoview
- sysmergepartitioninfoview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergepartitioninfoview view
ms.assetid: 714e2935-1bc7-4901-aea2-64b1bbda03d6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee0a46b7ec48d16bb2af2d528b4e832298c36a39
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysmergepartitioninfoview-transact-sql"></a>sysmergepartitioninfoview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysmergepartitioninfoview**檢視會公開資料表發行項的資料分割資訊。 這份檢視儲存在發行者端的發行集資料庫以及訂閱者端的訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|發行項的名稱。|  
|**type**|**tinyint**|指出發行項類型，它可以是下列項目之一：<br /><br /> **0x0a** = 資料表。<br /><br /> **0x20** = 僅限程序結構描述。<br /><br /> **0x40** = 僅限檢視結構描述或僅限索引檢視表結構描述。<br /><br /> **0x80** = 僅限函數結構描述。|  
|**objid**|**int**|已發行的物件之識別碼。|  
|**sync_objid**|**int**|代表同步處理資料集的檢視之物件識別碼。|  
|**view_type**|**tinyint**|檢視的類型：<br /><br /> **0** = 不是檢視; 使用所有基底物件。<br /><br /> **1** = 永久檢視。<br /><br /> **2** = 暫存檢視。|  
|**artid**|**uniqueidentifier**|給定發行項的唯一識別碼。|  
|**描述**|**nvarchar(255)**|發行項的簡要描述。|  
|**pre_creation_command**|**tinyint**|當在訂閱資料庫中建立發行項時，所採取的預設動作。<br /><br /> **0** = 無-如果訂閱者端已有資料表，會採取任何動作。<br /><br /> **1** = drop-卸除資料表，然後再重新建立它。<br /><br /> **2** = delete-刪除根據子集篩選中的 WHERE 子句的問題。<br /><br /> **3** = 截斷-與 2，但刪除頁面而非資料列相同。 不過，它不用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|目前發行項所屬發行集的識別碼。|  
|**nickname**|**int**|發行項識別的暱稱對應。|  
|**column_tracking**|**int**|指出是否實作發行項的資料行追蹤。|  
|**status**|**tinyint**|指出發行項的狀態，它可以是下列項目之一：<br /><br /> **1** = 未同步-下次發行資料表的初始處理指令碼會執行下一次執行快照集代理程式。<br /><br /> **2** = active-已執行發行資料表的初始處理指令碼。|  
|**conflict_table**|**sysname**|包含目前發行項的衝突記錄之本機資料表的名稱。 提供這份資料表只供參考，自訂衝突解決常式可以修改或刪除它的內容，管理員也可以直接修改或刪除它的內容。|  
|**creation_script**|**nvarchar(255)**|這個發行項的建立指令碼。|  
|**conflict_script**|**nvarchar(255)**|這個發行項的衝突指令碼。|  
|**article_resolver**|**nvarchar(255)**|這個發行項的衝突解析程式。|  
|**ins_conflict_proc**|**sysname**|用來將衝突資訊寫入衝突資料表的程序。|  
|**insert_proc**|**sysname**|在同步處理期間，用來插入資料列的程序。|  
|**update_proc**|**sysname**|在同步處理期間，用來更新資料列的程序。|  
|**select_proc**|**sysname**|合併代理程式用來實現鎖定以及尋找發行項的資料行和資料列之自動產生預存程序的名稱。|  
|**metadata_select_proc**|**sysname**|用來存取合併式複寫系統資料表中的中繼資料之自動產生預存程序的名稱。|  
|**delete_proc**|**sysname**|在同步處理期間，用來刪除資料列的程序。|  
|**schema_option**|**binary(8)**|給定發行項之結構描述產生選項的點陣圖。 如需支援*schema_option*值，請參閱[sp_addmergearticle &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
|**destination_object**|**sysname**|在訂閱者端建立之資料表的名稱。|  
|**destination_owner**|**sysname**|目的地物件的擁有者名稱。|  
|**resolver_clsid**|**nvarchar(50)**|自訂衝突解析程式的識別碼。 如果是商務邏輯處理常式，這個值便是 NULL。|  
|**subset_filterclause**|**nvarchar(1000)**|這個發行項的篩選子句。|  
|**missing_col_count**|**int**|發行項所遺漏的已發行資料行數目。|  
|**missing_cols**|**varbinary(128)**|描述發行項所遺漏之資料行的點陣圖。|  
|**excluded_cols**|**varbinary(128)**|發行項所排除之資料行的點陣圖。|  
|**excluded_col_count**|**int**|發行項所排除的資料行數目。|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**deleted_cols**|**varbinary(128)**|描述發行項所刪除之資料行的點陣圖。|  
|**resolver_info**|**nvarchar(255)**|自訂衝突解析程式所需要之其他資訊的儲存體。|  
|**view_sel_proc**|**nvarchar(290)**|合併代理程式用來初始擴展動態篩選發行集的發行項以及列舉任何篩選發行集中已變更之資料列的預存程序名稱。|  
|**gen_cur**|**bigint**|產生發行項基底資料表的本機變更數目。|  
|**vertical_partition**|**int**|指定是否啟用資料表發行項的資料行篩選。 **0**表示沒有垂直篩選，會發行所有資料行。|  
|**identity_support**|**int**|指定是否啟用自動識別範圍處理。 **1**表示啟用識別範圍處理，以及**0**表示沒有識別範圍支援。|  
|**before_image_objid**|**int**|追蹤資料表物件識別碼。 當啟用了發行集的資料分割變更最佳化時，追蹤資料表包含特定索引鍵資料行值。|  
|**before_view_objid**|**int**|檢視資料表的物件識別碼。 檢視所在的資料表會追蹤是否刪除或更新了在它之前屬於特定訂閱者的資料列。 只有在啟用了發行集的資料分割變更最佳化時才適用。|  
|**verify_resolver_signature**|**int**|指定在合併式複寫中使用解析程式之前，是否要驗證數位簽章：<br /><br /> **0** = 不驗證簽章。<br /><br /> **1** = 驗證簽章來查看它是否來自信任的來源。|  
|**allow_interactive_resolver**|**bit**|指定是否啟用發行項的互動式解析程式。 **1**表示互動式解決器可以用於文件。|  
|**fast_multicol_updateproc**|**bit**|指定是否已啟用合併代理程式，以在 UPDATE 陳述式中，將變更套用相同資料列的多個資料行中。<br /><br /> **0** = 變更為個別更新每個資料行的問題。<br /><br /> **1** = 在 UPDATE 陳述式，會使多個資料行在單一陳述式的更新發行。|  
|**check_permissions**|**int**|合併代理程式將變更套用在發行者時，將驗證之資料表層級權限的點陣圖。 *check_permissions*可以有下列值之一：<br /><br /> **0x00** = 不檢查權限。<br /><br /> **0x10** = 可上傳在訂閱者端進行插入之前，「 發行者 」 的權限檢查。<br /><br /> **0x20** = 在發行者端檢查權限，在上傳在訂閱者端進行更新之前。<br /><br /> **0x40** = 在發行者端檢查權限，在上傳在訂閱者端所作的刪除之前。|  
|**maxversion_at_cleanup**|**int**|下次執行合併代理程式時，所清除的最大層代 (Generation)。|  
|**processing_order**|**int**|指出合併式發行集; 集中之發行項的處理順序值**0**表示發行項並未排序，而且發行項的處理順序從最低到最高的值。 如果兩個發行項有相同的值，就會同時處理它們。 如需詳細資訊，請參閱[指定合併發行項的處理順序](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。|  
|**upload_options**|**tinyint**|定義是否能在訂閱者端進行變更或從訂閱者上傳變更，它可以是下列值之一。<br /><br /> **0** = 訂閱者端進行的更新沒有限制; 所有的變更會上傳到 「 發行者 」。<br /><br /> **1** = 允許在 「 訂閱者 」 進行變更，但未上傳到 「 發行者 」。<br /><br /> **2** = 不允許在訂閱者端進行變更。|  
|**published_in_tran_pub**|**bit**|指出合併式發行集中的發行項也在交易式發行集中發行。<br /><br /> **0** = 發行項不發行在交易式發行項中。<br /><br /> **1** = 發行項也發行在交易式發行項中。|  
|**lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**procname_postfix**|**nchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**well_partitioned_lightweight**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**before_upd_view_objid**|**int**|在更新之前，資料表的檢視之識別碼。|  
|**delete_tracking**|**bit**|指出是否複寫刪除。<br /><br /> **0** = 不複寫刪除。<br /><br /> **1** = 複寫刪除，這是合併式複寫的預設行為。<br /><br /> 當值*delete_tracking*是**0**、 訂閱者端刪除的資料列必須手動移除在 「 發行者 」 和 「 訂閱者 」 必須手動移除在發行者端刪除的資料列。<br /><br /> 附註： 值為**0**導致無法聚合。|  
|**compensate_for_errors**|**bit**|指出在同步處理期間發現錯誤時，是否採取補償動作。<br /><br /> **0** = Compensating 動作會停用。<br /><br /> **1** = 無法套用在 「 訂閱者 」 或 「 發行者 」 一定會導致發生補償動作恢復這些變更，這是合併式複寫的預設行為的變更。<br /><br /> 附註： 值為**0**導致無法聚合。|  
|**pub_range**|**bigint**|發行者識別範圍大小。|  
|**range**|**bigint**|將在調整中指派給訂閱者的連續識別值大小。|  
|**threshold**|**int**|識別範圍臨界值百分比。|  
|**stream_blob_columns**|**bit**|指出是否使用二進位大型物件資料行的資料流最佳化。 **1**表示會嘗試最佳化。|  
|**preserve_rowguidcol**|**bit**|指出複寫是否使用現有的 rowguid 資料行。 值為**1**表示會使用現有的 ROWGUIDCOL 資料行。 **0**表示複寫加入了 ROWGUIDCOL 資料行。|  
|**partition_view_id**|**int**|識別用來定義訂閱者資料分割的檢視。|  
|**repl_view_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**partition_deleted_view_rule**|**sysname**|在合併式複寫觸發程序內，用來根據舊資料行值擷取每個已刪除或更新的資料列之資料分割識別碼的陳述式。|  
|**partition_inserted_view_rule**|**Sysname**|在合併式複寫觸發程序內，用來根據新資料行值擷取每個已插入或更新的資料列之資料分割識別碼的陳述式。|  
|**membership_eval_proc_name**|**sysname**|評估目前的資料分割識別碼中的資料列的程序名稱[MSmerge_contents &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/msmerge-contents-transact-sql.md).|  
|**column_list**|**sysname**|發行項中已發行的資料行清單 (以逗號分隔)。|  
|**column_list_blob**|**sysname**|發行項中已發行的資料行清單 (以逗號分隔)，其中包括二進位大型物件資料行。|  
|**expand_proc**|**sysname**|這是用來重新評估「新插入的父資料列之所有子資料列的資料分割識別碼」及「已經歷資料分割變更或已被刪除之父資料列的資料分割識別碼」的程序名稱。|  
|**logical_record_parent_nickname**|**int**|邏輯記錄中給定發行項最上層父系的暱稱。|  
|**logical_record_view**|**int**|輸出對應於每個子系 rowguid 之最上層父發行項 rowguid 的檢視。|  
|**logical_record_deleted_view_rule**|**sysname**|類似於**logical_record_view**，只不過它會顯示"deleted"資料表中的子資料列更新和刪除觸發程序。|  
|**logical_record_level_conflict_detection**|**bit**|指出應該在邏輯記錄層級或資料列或資料行層級偵測衝突。<br /><br /> **0** = 資料列或資料行層級衝突偵測。<br /><br /> **1** = 邏輯記錄衝突偵測，則在 「 發行者 」 端的資料列的變更，以及變更個別資料列的相同邏輯處理 「 訂閱者 」 的記錄為衝突。<br /><br /> 當這個值是 1 時，只能使用邏輯記錄層級的衝突解決。|  
|**logical_record_level_conflict_resolution**|**bit**|指出應該在邏輯記錄層級或資料列或資料行層級解決衝突。<br /><br /> **0** = 資料列或資料行層級會使用的解析度。<br /><br /> **1** = 萬一發生衝突時，成功者的整個邏輯記錄會覆寫上失敗的一方的整個邏輯記錄。<br /><br /> 1 值可用來搭配邏輯記錄層級的偵測及資料列或資料行層級的偵測。|  
|**partition_options**|**tinyint**|定義發行項資料進行資料分割的方式，當所有資料列只屬於單一資料分割或單一訂閱時，能夠使效能最佳化。 *Partition_options*可以是下列值之一。<br /><br /> **0** = 發行項篩選是靜態或不會產生唯一的子集之資料的每個資料分割，也就是 「 重疊 」 的資料分割。<br /><br /> **1** = 資料分割重疊，而且訂閱者端進行的 DML 更新無法變更資料列所屬的資料分割。<br /><br /> **2** = 發行項會產生非重疊資料分割，但多個訂閱者可以接收相同的資料分割的篩選。<br /><br /> **3** = 篩選發行項會產生對每個訂閱而言是唯一的非重疊資料分割。|  
|**name**|**sysname**|資料分割的名稱。|  
  
## <a name="see-also"></a>另請參閱  
 [管理合併式發行集使用參數化篩選的資料分割](../../relational-databases/replication/publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)   
 [複寫資料表 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergepartition &#40;TRANSACT-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addmergepartition-transact-sql.md)   
 [sp_helpmergepartition &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepartition-transact-sql.md)  
  
  
