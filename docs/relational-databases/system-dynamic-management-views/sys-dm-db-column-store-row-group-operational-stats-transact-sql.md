---
title: sys.dm_db_column_store_row_group_operational_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: db5154b1b99b548a0757b83c3f79c39c23b777e3
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回目前資料列層級 I/O、 鎖定、 和存取方法活動中的資料行存放區索引的壓縮資料列。 使用**sys.dm_db_column_store_row_group_operational_stats**追蹤的時間長度，使用者查詢必須等待讀取或寫入壓縮資料列群組或資料分割的資料行存放區索引，並識別所遇到的資料列群組重大 I/O 活動或作用點。  
  
 記憶體中資料行存放區索引不會出現在這個 DMV 中。  
 
 
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|資料行存放區索引的資料表的識別碼。|  
|**index_id**|**int**|資料行存放區索引的識別碼。|  
|**partition_number**|**int**|在索引或堆積內，以 1 為基底的資料分割編號。|  
|**row_group_id**|**int**|資料行存放區索引中資料列群組的識別碼。 這是資料分割內唯一的。|  
|**scan_count**|**int**|透過在最後一個的 SQL 重新啟動後資料列群組掃描的數目。|  
|**delete_buffer_scan_count**|**int**|用來判斷此資料列群組中刪除的資料列的刪除緩衝區的次數。 這包括存取記憶體中雜湊表和基礎 btree。|  
|**index_scan_count**|**int**|資料行存放區索引資料分割掃描次數。 這是相同的資料分割中的所有資料列群組。|  
|**rowgroup_lock_count**|**bigint**|自上次 SQL 重新啟動此資料列群組的鎖定要求的累計計數。|  
|**rowgroup_lock_wait_count**|**bigint**|累加次數 database engine 在此資料列群組鎖定等候上次 SQL 啟動。|  
|**rowgroup_lock_wait_in_ms**|**bigint**|累加毫秒數的 database engine 在此資料列群組鎖定等候上次 SQL 啟動。|  
  
## <a name="permissions"></a>Permissions  
 需要下列權限：  
  
-   Object_id 所指定的資料表上的 [控制] 權限。  
  
-   VIEW DATABASE STATE 權限傳回在資料庫中的所有物件的相關資訊，利用物件萬用字元 @*object_id* = NULL  
  
 授與 VIEW DATABASE STATE 可以傳回資料庫中的所有物件，不論特定物件是否拒絕任何 CONTROL 權限。  
  
 拒絕 VIEW DATABASE STATE 會造成不允許傳回資料庫中的所有物件 (不論是否授與特定物件任何 CONTROL 權限)。 也，當資料庫萬用字元 @*database_id*= 指定 NULL，則會省略資料庫。  
  
 如需詳細資訊，請參閱[動態管理檢視和函數&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [索引相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

