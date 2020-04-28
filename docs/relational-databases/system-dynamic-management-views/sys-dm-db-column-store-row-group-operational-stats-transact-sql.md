---
title: sys.databases dm_db_column_store_row_group_operational_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31b71c68-50a0-4fd8-a7fe-2d2292be1163
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 03e97e38eb396aa24c9779d07f269a60f117ab09
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "68005047"
---
# <a name="sysdm_db_column_store_row_group_operational_stats-transact-sql"></a>sys.databases dm_db_column_store_row_group_operational_stats （Transact-sql）
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  針對資料行存放區索引中的壓縮資料列群組，傳回目前的資料列層級 i/o、鎖定和存取方法活動。 使用**dm_db_column_store_row_group_operational_stats sys.databases**來追蹤使用者查詢必須等候讀取或寫入到資料行存放區索引之壓縮資料列群組或資料分割的時間長度，並找出遇到重要 i/o 活動或作用點的資料列群組。  
  
 記憶體內部資料行存放區索引不會出現在這個 DMV 中。  
 
 
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|具有資料行存放區索引之資料表的識別碼。|  
|**index_id**|**int**|資料行存放區索引的識別碼。|  
|**partition_number**|**int**|在索引或堆積內，以 1 為基底的資料分割編號。|  
|**row_group_id**|**int**|資料行存放區索引中資料列群組的識別碼。 這在資料分割內是唯一的。|  
|**scan_count**|**int**|自上次 SQL 重新開機後通過資料列群組的掃描次數。|  
|**delete_buffer_scan_count**|**int**|刪除緩衝區用來判斷此資料列群組中已刪除資料列的次數。 這包括存取記憶體中的雜湊表和基礎 btree。|  
|**index_scan_count**|**int**|掃描資料行存放區索引資料分割的次數。 這對資料分割中的所有資料列群組都是相同的。|  
|**rowgroup_lock_count**|**bigint**|自上次 SQL 重新開機之後，此資料列群組的鎖定要求累計計數。|  
|**rowgroup_lock_wait_count**|**bigint**|自從上次 SQL 重新開機之後，資料庫引擎在此資料列群組鎖定上等候的累計次數。|  
|**rowgroup_lock_wait_in_ms**|**bigint**|自從上次 SQL 重新開機之後，資料庫引擎在這個資料列群組鎖定上等候的累計毫秒數。|  
  
## <a name="permissions"></a>權限  
 需要下列權限：  
  
-   Object_id 所指定之資料表的 CONTROL 許可權。  
  
-   VIEW DATABASE STATE 許可權，藉由使用物件萬用字元 @*object_id* = Null，傳回資料庫中所有物件的相關資訊  
  
 授與 VIEW DATABASE STATE 可以傳回資料庫中的所有物件，不論特定物件是否拒絕任何 CONTROL 權限。  
  
 拒絕 VIEW DATABASE STATE 會造成不允許傳回資料庫中的所有物件 (不論是否授與特定物件任何 CONTROL 權限)。 此外，當指定資料庫萬用字元 @*database_id*= Null 時，就會省略資料庫。  
  
 如需詳細資訊，請參閱[動態管理檢視和函數 &#40;transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="see-also"></a>另請參閱  
 [動態管理 Views 和函數 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [索引相關的動態管理檢視和函數 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [效能的監視與微調](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [dm_db_index_usage_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [dm_os_latch_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [dm_db_partition_stats &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [allocation_units &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

