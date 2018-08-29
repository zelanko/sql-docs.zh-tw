---
title: sys.dm_db_column_store_row_group_operational_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 73c83151f27338d8d96046e11d9406d751f5aa17
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43100624"
---
# <a name="sysdmdbcolumnstorerowgroupoperationalstats-transact-sql"></a>sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  傳回目前資料列層級 I/O、 鎖定和存取方法活動中的資料行存放區索引的壓縮資料列群組。 使用**sys.dm_db_column_store_row_group_operational_stats**追蹤的時間長度使用者查詢必須等待讀取或寫入壓縮資料列群組或資料行存放區索引的分割區，並識別發生的資料列群組大量 I/O 活動或作用點。  
  
 這個 DMV 中看不到記憶體中資料行存放區索引。  
 
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|資料行存放區索引之資料表的識別碼。|  
|**index_id**|**int**|資料行存放區索引的識別碼。|  
|**partition_number**|**int**|在索引或堆積內，以 1 為基底的資料分割編號。|  
|**row_group_id**|**int**|資料行存放區索引中之 rowgroup 的識別碼。 這是資料分割內唯一的。|  
|**scan_count**|**int**|透過資料列群組在上次的 SQL 重新啟動的掃描數目。|  
|**delete_buffer_scan_count**|**int**|用來判斷此資料列群組中刪除的資料列的刪除緩衝區的次數。 這包括存取記憶體中雜湊表和基礎 btree。|  
|**index_scan_count**|**int**|資料行存放區索引資料分割掃描次數。 這是相同的分割區中的所有資料列群組。|  
|**rowgroup_lock_count**|**bigint**|自上次 SQL 重新啟動這個資料列群組的鎖定要求的累計計數。|  
|**rowgroup_lock_wait_count**|**bigint**|累加次數 database engine 等候這個資料列群組鎖定在上次的 SQL 重新啟動。|  
|**rowgroup_lock_wait_in_ms**|**bigint**|累加毫秒數，資料庫引擎等候這個資料列群組鎖定在上次的 SQL 重新啟動。|  
  
## <a name="permissions"></a>Permissions  
 需要下列權限：  
  
-   Object_id 所指定資料表的 CONTROL 權限。  
  
-   傳回在資料庫中的所有物件的相關資訊，利用物件萬用字元 @ 的 VIEW DATABASE STATE 權限*object_id* = NULL  
  
 授與 VIEW DATABASE STATE 可以傳回資料庫中的所有物件，不論特定物件是否拒絕任何 CONTROL 權限。  
  
 拒絕 VIEW DATABASE STATE 會造成不允許傳回資料庫中的所有物件 (不論是否授與特定物件任何 CONTROL 權限)。 也，當資料庫萬用字元 @*database_id*= 指定 NULL，則會省略資料庫。  
  
 如需詳細資訊，請參閱 <<c0> [ 動態管理檢視和函式&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。</c0>  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [索引相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

