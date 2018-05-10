---
title: sys.dm_exec_function_stats (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a28d58f611307792307c30161e20257b86ea66cf
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys.dm_exec_function_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  傳回的彙總效能統計資料的快取的函式。 此檢視會傳回一個資料列，對於每個快取的函式計劃，而且資料列的存留期只要函式維持快取。 當從快取移除函式時，對應的資料列也會從刪除此檢視。 在這段時間，效能統計資料 SQL 追蹤事件就會引發類似**sys.dm_exec_query_stats**。 傳回純量函數，包括記憶體中的函式和 CLR 純量函數的相關資訊。 不會傳回資料表值函式的相關資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  
  
> [!NOTE]
> 初始查詢**sys.dm_exec_function_stats**工作負載正在執行伺服器上是否可能會產生不正確的結果。 您可以重複執行查詢，以找出較精確的結果。  
  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|此函式所在的資料庫識別碼。|  
|**object_id**|**int**|函式的物件識別碼。|  
|**type**|**char(2)**|物件的類型： FN = 純量值函式|  
|**type_desc**|**nvarchar(60)**|物件類型的描述： SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|這可用來建立相互關聯中的查詢**sys.dm_exec_query_stats** ，從內部執行此函式。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 此值可搭配**sys.dm_exec_cached_plans**動態管理檢視。<br /><br /> 一律為 0x000 時的原生編譯的函式的查詢記憶體最佳化資料表。|  
|**cached_time**|**datetime**|此函式加入快取時間。|  
|**last_execution_time**|**datetime**|上次執行的函式的時間。|  
|**execution_count**|**bigint**|從上次編譯以來被執行的函式的次數。|  
|**total_worker_time**|**bigint**|總 CPU 時間量以百萬分之一秒為單位，從編譯以來執行此函式所耗用。<br /><br /> 對於原生編譯的函式， **total_worker_time**可能不正確，如果執行採用少於 1 毫秒。|  
|**last_worker_time**|**bigint**|CPU 時間 （毫秒），以耗用的上次執行的函式。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|最小 CPU 時間，以毫秒為單位，在單次執行期間曾耗用的這個函式。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|最大 CPU 時間，以毫秒為單位，在單次執行期間曾耗用的這個函式。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|編譯以來，此函式的執行所執行的實體讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_physical_reads**|**bigint**|上次執行的函式執行的實體讀取次數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_physical_reads**|**bigint**|最小的單次執行期間曾執行此函式的實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_physical_reads**|**bigint**|此函式單次執行期間曾執行的實體讀取的最大數目。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_writes**|**bigint**|編譯以來，此函式的執行所執行的邏輯寫入總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_writes**|**bigint**|上次執行計畫時修改的緩衝集區頁數。 如果已修改頁面，則不會計算寫入。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_writes**|**bigint**|最小的單次執行期間曾執行此函式的邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_writes**|**bigint**|此函式單次執行期間曾執行的邏輯寫入的數目上限。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_reads**|**bigint**|編譯以來，此函式的執行所執行的邏輯讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_reads**|**bigint**|上次執行的函式執行的邏輯讀取次數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_reads**|**bigint**|最小的單次執行期間曾執行此函式的邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_reads**|**bigint**|此函式單次執行期間曾執行的邏輯讀取的最大數目。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_elapsed_time**|**bigint**|已耗用時間總和，以毫秒為單位，此函式完成執行。|  
|**last_elapsed_time**|**bigint**|經過時間 （毫秒），此函式為最近完成執行。|  
|**min_elapsed_time**|**bigint**|最小耗用時間，以百萬分之一秒為單位，任何在完成執行的這個函式。|  
|**max_elapsed_time**|**bigint**|最大耗用時間，以百萬分之一秒為單位，任何在完成執行的這個函式。|  
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
## <a name="examples"></a>範例  
 下列範例會傳回平均經過時間所識別的前十個函式的相關資訊。  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行相關動態管理檢視和函數&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
