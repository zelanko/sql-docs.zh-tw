---
title: "sys.dm_exec_trigger_stats (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_exec_trigger_stats
- dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats_TSQL
- sys.dm_exec_trigger_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_trigger_stats dynamic management function
ms.assetid: 863498b4-849c-434d-b748-837411458738
caps.latest.revision: "14"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67c6d5765ee5259134f6d9985a88bf94768490cf
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回快取觸發程序的彙總效能統計資料。 此檢視會針對每個觸發程序包含一個資料列，而且資料列的存留期間與觸發程序維持快取狀態的時間一樣長。 從快取中移除觸發程序時，對應的資料列也會從這個檢視中刪除。 在這段時間，效能統計資料 SQL 追蹤事件就會引發類似**sys.dm_exec_query_stats**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|觸發程序所在的資料庫識別碼。|  
|**object_id**|**int**|觸發程序的物件識別碼。|  
|**型別**|**char(2)**|物件的類型：<br /><br /> TA = 組件 (CLR) 觸發程序<br /><br /> TR = SQL 觸發程序|  
|**Type_desc**|**nvarchar （60)**|物件類型的描述：<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|這可用來建立相互關聯中的查詢**sys.dm_exec_query_stats** ，已從這個觸發程序內執行。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 此值可搭配**sys.dm_exec_cached_plans**動態管理檢視。|  
|**cached_time**|**datetime**|在快取中加入觸發程序的時間。|  
|**last_execution_time**|**datetime**|上次執行觸發程序的時間。|  
|**execution_count**|**bigint**|觸發程序從上次編譯以來被執行的次數。|  
|**total_worker_time**|**bigint**|這個觸發程序從編譯以來執行所耗用的 CPU 時間總量 (以微秒為單位)。|  
|**last_worker_time**|**bigint**|觸發程序上次執行所耗用的 CPU 時間 (以微秒為單位)。|  
|**min_worker_time**|**bigint**|這個觸發程序在單次執行期間曾耗用的最大 CPU 時間 (以微秒為單位)。|  
|**max_worker_time**|**bigint**|這個觸發程序在單次執行期間曾耗用的最大 CPU 時間 (以微秒為單位)。|  
|**total_physical_reads**|**bigint**|這個觸發程序在編譯以來執行所執行的實體讀取總數。|  
|**last_physical_reads**|**bigint**|觸發程序上次執行所執行的實體讀取數。|  
|**min_physical_reads**|**bigint**|這個觸發程序在單次期間曾執行的最小實體讀取數。|  
|**max_physical_reads**|**bigint**|這個觸發程序在單次期間曾執行的最大實體讀取數。|  
|**total_logical_writes**|**bigint**|這個觸發程序在編譯以來執行所執行的邏輯寫入總數。|  
|**last_logical_writes**|**bigint**|**total_physical_reads**執行的上次執行觸發程序的邏輯寫入次數。|  
|**min_logical_writes**|**bigint**|這個觸發程序在單次執行期間曾執行的最小邏輯寫入數。|  
|**max_logical_writes**|**bigint**|這個觸發程序在單次執行期間曾執行的最大邏輯寫入數。|  
|**total_logical_reads**|**bigint**|這個觸發程序在編譯以來執行所執行的邏輯讀取總數。|  
|**last_logical_reads**|**bigint**|觸發程序上次執行所執行的邏輯讀取數。|  
|**min_logical_reads**|**bigint**|這個觸發程序在單次期間曾執行的最小邏輯讀取數。|  
|**max_logical_reads**|**bigint**|這個觸發程序在單次期間曾執行的最大邏輯讀取數。|  
|**total_elapsed_time**|**bigint**|這個觸發程序完成執行經歷的總時間 (以微秒為單位)。|  
|**last_elapsed_time**|**bigint**|這個觸發程序最近完成執行經歷的時間 (以微秒為單位)。|  
|**min_elapsed_time**|**bigint**|這個觸發程序完成執行經歷的最小時間 (以微秒為單位)。|  
|**max_elapsed_time**|**bigint**|這個觸發程序完成執行經歷的最大時間 (以微秒為單位)。|  
  
## <a name="remarks"></a>備註  
 在 Windows Azure SQL Database 中，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  

完成查詢時，會更新檢視中的統計資料。  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。
  
  
## <a name="examples"></a>範例  
 下列範例會傳回平均經過時間所識別之前五項觸發程序的相關資訊。  
  
```sql  
PRINT '--top 5 CPU consuming triggers '  
  
SELECT TOP 5 d.object_id, d.database_id, DB_NAME(database_id) AS 'database_name',   
    OBJECT_NAME(object_id, database_id) AS 'trigger_name', d.cached_time,  
    d.last_execution_time, d.total_elapsed_time,   
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],   
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_trigger_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [執行相關動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text (） &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
  [sys.dm_exec_procedure_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
 [sys.dm_exec_cached_plans &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
