---
title: sys.dm_exec_trigger_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80222e4619ffc9e13b9d38e6f92e197cd2834813
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回快取觸發程序的彙總效能統計資料。 此檢視會針對每個觸發程序包含一個資料列，而且資料列的存留期間與觸發程序維持快取狀態的時間一樣長。 從快取中移除觸發程序時，對應的資料列也會從這個檢視中刪除。 在這段時間，效能統計資料 SQL 追蹤事件就會引發類似**sys.dm_exec_query_stats**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|觸發程序所在的資料庫識別碼。|  
|**object_id**|**int**|觸發程序的物件識別碼。|  
|**type**|**char(2)**|物件的類型：<br /><br /> TA = 組件 (CLR) 觸發程序<br /><br /> TR = SQL 觸發程序|  
|**Type_desc**|**nvarchar(60)**|物件類型的描述：<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|這可用來建立相互關聯中的查詢**sys.dm_exec_query_stats** ，已從這個觸發程序內執行。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 此值可搭配**sys.dm_exec_cached_plans**動態管理檢視。|  
|**cached_time**|**datetime**|在快取中加入觸發程序的時間。|  
|**last_execution_time**|**datetime**|上次執行觸發程序的時間。|  
|**execution_count**|**bigint**|從上次編譯以來被執行觸發程序的次數。|  
|**total_worker_time**|**bigint**|CPU 時間 （毫秒），以編譯以來執行這個觸發程序所耗用的總金額。|  
|**last_worker_time**|**bigint**|觸發程序上次執行所耗用的 CPU 時間 (以微秒為單位)。|  
|**min_worker_time**|**bigint**|最大 CPU 時間，以毫秒為單位，在單次執行期間曾耗用的這個觸發程序。|  
|**max_worker_time**|**bigint**|最大 CPU 時間，以毫秒為單位，在單次執行期間曾耗用的這個觸發程序。|  
|**total_physical_reads**|**bigint**|編譯以來，這個觸發程序的執行所執行的實體讀取總數。|  
|**last_physical_reads**|**bigint**|上次執行觸發程序執行的實體讀取次數。|  
|**min_physical_reads**|**bigint**|這個觸發程序單次執行期間曾執行的實體讀取的最小數目。|  
|**max_physical_reads**|**bigint**|這個觸發程序單次執行期間曾執行的實體讀取的數目上限。|  
|**total_logical_writes**|**bigint**|編譯以來，這個觸發程序的執行所執行的邏輯寫入總數。|  
|**last_logical_writes**|**bigint**|上次執行觸發程序執行的邏輯寫入次數。|  
|**min_logical_writes**|**bigint**|這個觸發程序單次執行期間曾執行的邏輯寫入的最小數目。|  
|**max_logical_writes**|**bigint**|這個觸發程序單次執行期間曾執行的邏輯寫入的數目上限。|  
|**total_logical_reads**|**bigint**|編譯以來，這個觸發程序的執行所執行的邏輯讀取總數。|  
|**last_logical_reads**|**bigint**|上次執行觸發程序執行的邏輯讀取數目。|  
|**min_logical_reads**|**bigint**|這個觸發程序單次執行期間曾執行的邏輯讀取的最小數目。|  
|**max_logical_reads**|**bigint**|這個觸發程序單次執行期間曾執行的邏輯讀取的數目上限。|  
|**total_elapsed_time**|**bigint**|已耗用時間總和，以毫秒為單位，這個觸發程序完成執行。|  
|**last_elapsed_time**|**bigint**|這個觸發程序最近完成執行經歷的時間 (以微秒為單位)。|  
|**min_elapsed_time**|**bigint**|最小耗用時間 （毫秒），如這個觸發程序完成執行。|  
|**max_elapsed_time**|**bigint**|最大耗用時間 （毫秒），如這個觸發程序完成執行。| 
|**total_spills**|**bigint**|編譯以來執行此觸發程序所溢出的頁面總數。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|頁數溢出的上次執行觸發程序。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|這個觸發程序曾有在單次執行期間溢出的頁面最小數目。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|這個觸發程序曾有在單次執行期間溢出的頁面的數目上限。<br /><br /> **適用於**： 開頭為[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
  
## <a name="remarks"></a>備註  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  

完成查詢時，會更新檢視中的統計資料。  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="examples"></a>範例  
 下列範例會傳回平均經過時間所識別之前五項觸發程序的相關資訊。  
  
```sql  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
[執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
