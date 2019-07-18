---
title: sys.dm_db_index_usage_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_usage_stats_TSQL
- sys.dm_db_index_usage_stats
- sys.dm_db_index_usage_stats_TSQL
- dm_db_index_usage_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_usage_stats dynamic management view
ms.assetid: d06a001f-0f72-4679-bc2f-66fff7958b86
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 491ec37d96cf6bdb2b074efb42a54406beb1fd20
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264399"
---
# <a name="sysdmdbindexusagestats-transact-sql"></a>sys.dm_db_index_usage_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回不同類型索引作業的計數，以及每種類型作業上次執行的時間。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 若要避免公開此資訊，每個資料列，其中包含不屬於連接租用戶的資料會被篩選掉。  
  
> [!NOTE]  
>  **sys.dm_db_index_usage_stats**不會傳回記憶體最佳化索引的相關資訊。 記憶體最佳化索引用法的相關資訊，請參閱[sys.dm_db_xtp_index_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)。  
  
> [!NOTE]  
>  若要呼叫這個檢視從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用**sys.dm_pdw_nodes_db_index_usage_stats**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|定義資料表或檢視的資料庫識別碼。|  
|**object_id**|**int**|定義索引之資料表或檢視的識別碼。|  
|**index_id**|**int**|索引的識別碼。|  
|**user_seeks**|**bigint**|由使用者查詢所進行的搜尋數。|  
|**user_scans**|**bigint**|未使用的使用者查詢所掃描的數目 '搜尋' 述詞。|  
|**user_lookups**|**bigint**|由使用者查詢所進行的書籤查閱數。|  
|**user_updates**|**bigint**|由使用者查詢所進行的更新數。 其中包括 Insert、 Delete，以及更新代表完成不受影響的實際資料列的作業數目。 例如，如果您刪除 1000 個資料列，在單一陳述式時，此計數遞增量為 1|  
|**last_user_seek**|**datetime**|上次使用者搜尋的時間|  
|**last_user_scan**|**datetime**|上次使用者掃描的時間。|  
|**last_user_lookup**|**datetime**|上次使用者查閱的時間。|  
|**last_user_update**|**datetime**|上次使用者更新的時間。|  
|**system_seeks**|**bigint**|由系統查詢所進行的搜尋數。|  
|**system_scans**|**bigint**|由系統查詢所進行的掃描數。|  
|**system_lookups**|**bigint**|由系統查詢所進行的查閱數。|  
|**system_updates**|**bigint**|由系統查詢所進行的更新數。|  
|**last_system_seek**|**datetime**|上次系統搜尋的時間。|  
|**last_system_scan**|**datetime**|上次系統掃描的時間。|  
|**last_system_lookup**|**datetime**|上次系統查閱的時間。|  
|**last_system_update**|**datetime**|上次系統更新的時間。|  
|pdw_node_id|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 這個分佈是在節點的識別碼。|  
  
## <a name="remarks"></a>備註  
 在指定索引上由一項查詢執行所進行的每個個別搜尋、掃描、查閱或更新，在這份檢視都被當作使用一次該索引，並且累加對應的計數器。 它會針對由使用者提交之查詢所導致的作業，以及由內部產生之查詢所導致的作業 (例如，掃描以收集統計資料)，來報告資訊。  
  
 **User_updates**計數器指出因插入的索引維護的層級、 更新或刪除基礎資料表或檢視上的作業。 您可以利用這份檢視來判斷應用程式根本很少用到的索引。 您也可以利用這份檢視，判斷哪些索引會產生維護上的額外負擔。 您可能會考慮卸除不用於查詢或不常用於查詢，卻會造成維護上額外負擔的索引。  
  
 只要一啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服務，計數器就會初始化為空值。 此外，每當卸離或關閉資料庫時 (例如，因為 AUTO_CLOSE 設為 ON)，就會移除所有與資料庫關聯的資料列。  
  
 使用索引時，會加入一個資料列**sys.dm_db_index_usage_stats**如果資料列不存在的索引。 加入資料列後，其計數器的初始設定為零。  
  
 若要在升級期間[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，或[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，而且移除了 sys.dm_db_index_usage_stats 中的項目。 開頭[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，如之前保留的項目[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。  
  
## <a name="permissions"></a>Permissions  
在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，則需要**伺服器系統管理員**該**Azure Active Directory 管理員**帳戶。  
  
## <a name="see-also"></a>另請參閱  

 [索引相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


