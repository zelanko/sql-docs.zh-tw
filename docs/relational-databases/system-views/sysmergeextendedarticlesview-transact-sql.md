---
title: sysmergeextendedarticlesview (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysmergeextendedarticlesview
- sysmergeextendedarticlesview_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergeextendedarticlesview view
ms.assetid: bd5c8414-5292-41fd-80aa-b55a50ced7e2
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4b00bf27f0daaa42ef534208629bfac58f326c57
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sysmergeextendedarticlesview-transact-sql"></a>sysmergeextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **Sysmergeextendedarticlesview**檢視會公開發行項資訊。 這份檢視儲存在發行者端的發行集資料庫以及訂閱者端的訂閱資料庫中。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|發行項的名稱。|  
|**type**|**tinyint**|指出發行項類型，它可以是下列項目之一：<br /><br /> **10** = 資料表。<br /><br /> **32** = 僅限程序結構描述。<br /><br /> **64** = 僅限檢視結構描述或僅限索引檢視表結構描述。<br /><br /> **128** = 僅限函數結構描述。<br /><br /> **160** = 僅限同義字結構描述。|  
|**objid**|**int**|發行者物件的識別碼。|  
|**sync_objid**|**int**|代表同步處理資料集檢視的識別碼。|  
|**view_type**|**tinyint**|檢視的類型：<br /><br /> **0** = 不是檢視; 使用所有基底物件。<br /><br /> **1** = 永久檢視。<br /><br /> **2** = 暫存檢視。|  
|**artid**|**uniqueidentifier**|給定發行項的唯一識別碼。|  
|**描述**|**nvarchar(255)**|發行項的簡要描述。|  
|**pre_creation_command**|**tinyint**|當在訂閱資料庫中建立發行項時，所採取的預設動作。<br /><br /> **0** = 無-如果訂閱者端已有資料表，會採取任何動作。<br /><br /> **1** = drop-卸除再重新建立它的資料表。<br /><br /> **2** = delete-刪除根據子集篩選中的 WHERE 子句的問題。<br /><br /> **3** = 截斷-與 2，但刪除頁面而非資料列相同。 不過，它不用 WHERE 子句。|  
|**pubid**|**uniqueidentifier**|目前發行項所屬發行集的識別碼。|  
|**別名**|**int**|發行項識別的暱稱對應。|  
|**column_tracking**|**int**|指出是否實作發行項的資料行追蹤。|  
|**status**|**tinyint**|指出發行項的狀態，它可以是下列項目之一：<br /><br /> **1** = 未同步-下次發行資料表的初始處理指令碼會執行下一次執行快照集代理程式。<br /><br /> **2** = active-已執行發行資料表的初始處理指令碼。<br /><br /> **5** = New_inactive-加入。<br /><br /> **6** = New_active-加入。|  
|**conflict_table**|**sysname**|包含目前發行項的衝突記錄之本機資料表的名稱。 提供這份資料表只供參考，自訂衝突解決常式可以修改或刪除它的內容，管理員也可以直接修改或刪除它的內容。|  
|**creation_script**|**nvarchar(255)**|這個發行項的建立指令碼。|  
|**conflict_script**|**nvarchar(255)**|這個發行項的衝突指令碼。|  
|**article_resolver**|**nvarchar(255)**|這個發行項的自訂資料列層級衝突解析程式。|  
|**ins_conflict_proc**|**sysname**|用來寫入衝突，此程序**conflict_table**。|  
|**insert_proc**|**sysname**|預設衝突解析程式在同步處理期間插入資料列所使用的程序。|  
|**update_proc**|**sysname**|預設衝突解析程式在同步處理期間更新資料列所使用的程序。|  
|**select_proc**|**sysname**|合併代理程式用來實現鎖定以及尋找發行項的資料行和資料列之自動產生預存程序的名稱。|  
|**schema_option**|**binary(8)**|支援的值*schema_option*，請參閱[sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。|  
|**destination_object**|**sysname**|在訂閱者端建立之資料表的名稱。|  
|**resolver_clsid**|**nvarchar(50)**|自訂衝突解析程式的識別碼。|  
|**subset_filterclause**|**nvarchar(1000)**|這個發行項的篩選子句。|  
|**missing_col_count**|**int**|遺漏的資料行數。|  
|**missing_cols**|**varbinary(128)**|遺漏資料行的點陣圖。|  
|**columns**|**varbinary(128)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resolver_info**|**nvarchar(255)**|自訂衝突解析程式所需要之其他資訊的儲存體。|  
|**view_sel_proc**|**nvarchar(290)**|合併代理程式用來初始擴展動態篩選發行集的發行項以及列舉任何篩選發行集中已變更之資料列的預存程序名稱。|  
|**gen_cur**|**int**|發行項基底資料表的本機變更產生數目。|  
|**excluded_cols**|**varbinary(128)**|在傳送給訂閱者的發行項中排除資料行的點陣圖。|  
|**excluded_col_count**|**int**|排除的資料行數。|  
|**vertical_partition**|**int**|指定是否啟用資料表發行項的資料行篩選。 **0**表示沒有垂直篩選，會發行所有資料行。|  
|**identity_support**|**int**|指定是否啟用自動識別範圍處理。 **1**表示啟用識別範圍處理，以及**0**表示沒有識別範圍支援。|  
|**destination_owner**|**sysname**|目的地物件的擁有者名稱。|  
|**before_image_objid**|**int**|追蹤資料表物件識別碼。 發行集設定為啟用資料分割變更最佳化時，追蹤資料表會包含某些索引鍵資料行值。|  
|**before_view_objid**|**int**|檢視資料表的物件識別碼。 檢視所在的資料表會追蹤是否刪除或更新了在它之前屬於特定訂閱者的資料列。 適用於僅發行集建立時與*@keep_partition_changes*  =  **true**。|  
|**verify_resolver_signature**|**int**|指定在合併式複寫中使用解析程式之前，是否要驗證數位簽章：<br /><br /> **0** = 不驗證簽章。<br /><br /> **1** = 驗證簽章來查看它是否來自信任的來源。|  
|**allow_interactive_resolver**|**bit**|指定是否啟用發行項的互動式解析程式。 **1**指定發行項上使用互動式解析程式。|  
|**fast_multicol_updateproc**|**bit**|指定是否已啟用合併代理程式，以在 UPDATE 陳述式中，將變更套用相同資料列的多個資料行中。<br /><br /> **0** = 變更為個別更新每個資料行的問題。<br /><br /> **1** = 在 UPDATE 陳述式，會使多個資料行在單一陳述式的更新發行。|  
|**check_permissions**|**int**|合併代理程式將變更套用在發行者時，將驗證之資料表層級權限的點陣圖。 *check_permissions*可以有下列值之一：<br /><br /> **0x00** = 不檢查權限。<br /><br /> **0x10** = 在發行者端檢查權限，在上傳在訂閱者端進行的 Insert 之前。<br /><br /> **0x20** = 在發行者端檢查權限，在上傳在訂閱者端進行更新之前。<br /><br /> **0x40** = 在發行者端檢查權限，在上傳在訂閱者端所作的刪除之前。|  
|**maxversion_at_cleanup**|**int**|清除中繼資料的最高層代 (Generation)。|  
|**processing_order**|**int**|指出合併式發行集; 集中之發行項的處理順序值**0**指出發行項並未排序，，和發行項的處理順序從最低到最高的值。 如果兩個發行項有相同的值，就會同時處理它們。 如需詳細資訊，請參閱[指定合併發行項的處理順序](../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)。|  
|**published_in_tran_pub**|**bit**|指出合併式發行集中的發行項也在交易式發行集中發行。<br /><br /> **0** = 發行項不發行在交易式發行項中。<br /><br /> **1** = 發行項也發行在交易式發行項中。|  
|**upload_options**|**tinyiny**|定義是否能在訂閱者端進行變更或從訂閱者上傳變更，它可以是下列值之一。<br /><br /> **0** = 訂閱者端進行的更新沒有限制; 所有的變更會上傳到 「 發行者 」。<br /><br /> **1** = 允許在 「 訂閱者 」 進行變更，但未上傳到 「 發行者 」。<br /><br /> **2** = 不允許在訂閱者端進行變更。|  
|**輕量型**|**bit**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**delete_proc**|**sysname**|預設衝突解析程式在同步處理期間刪除資料列所使用的程序。|  
|**before_upd_view_objid**|**int**|在更新之前，資料表的檢視之識別碼。|  
|**delete_tracking**|**bit**|指出是否複寫刪除。<br /><br /> **0** = 不複寫刪除。<br /><br /> **1** = 複寫刪除，這是合併式複寫的預設行為。<br /><br /> 當值*delete_tracking*是**0**、 訂閱者端刪除的資料列必須手動移除在 「 發行者 」 和 「 訂閱者 」 必須手動移除在發行者端刪除的資料列。<br /><br /> 附註： 值為**0**導致無法聚合。|  
|**compensate_for_errors**|**bit**|指出在同步處理期間發現錯誤時，是否採取補償動作。<br /><br /> **0** = Compensating 動作會停用。<br /><br /> **1** = 無法套用在 「 訂閱者 」 或 「 發行者 」 一定會導致發生補償動作恢復這些變更，這是合併式複寫的預設行為的變更。<br /><br /> 附註： 值為**0**導致無法聚合。|  
|**pub_range**|**bigint**|發行者識別範圍大小。|  
|**範圍**|**bigint**|將在調整中指派給訂閱者的連續識別值大小。|  
|**threshold**|**int**|識別範圍臨界值百分比。|  
|**metadata_select_proc**|**sysname**|用來存取合併式複寫系統資料表中的中繼資料之自動產生預存程序的名稱。|  
|**stream_blob_columns**|**bit**|指定當複寫二進位大型物件資料行時，是否使用資料流最佳化。 **1**表示嘗試最佳化。|  
|**preserve_rowguidcol**|**bit**|指出複寫是否使用現有的 rowguid 資料行。 值為**1**表示會使用現有的 ROWGUIDCOL 資料行。 **0**表示複寫加入了 ROWGUIDCOL 資料行。|  
  
## <a name="see-also"></a>另請參閱  
 [複寫資料表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [複寫檢視&#40;Transact SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_addmergearticle &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [sysmergearticles &#40;Transact SQL&#41;](../../relational-databases/system-tables/sysmergearticles-transact-sql.md)  
  
  
