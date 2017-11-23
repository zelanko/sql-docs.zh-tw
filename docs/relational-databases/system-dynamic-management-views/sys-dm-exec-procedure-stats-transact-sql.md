---
title: "sys.dm_exec_procedure_stats (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats_TSQL
- dm_exec_procedure_stats
- sys.dm_exec_procedure_stats
dev_langs: TSQL
helpviewer_keywords: sys.dm_exec_procedure_stats dynamic management view
ms.assetid: ab8ddde8-1cea-4b41-a7e4-697e6ddd785a
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: f935b0e9a4c150830a03ecb2ea1f67a4cd270d3f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmexecprocedurestats-transact-sql"></a>sys.dm_exec_procedure_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  傳回快取預存程序的彙總效能統計資料。 此檢視會針對每個快取預存程序計畫傳回一個資料列，而且資料列的存留期間與預存程序維持快取狀態的時間一樣長。 從快取中移除預存程序時，對應的資料列也會從這個檢視中刪除。 在這段時間，效能統計資料 SQL 追蹤事件就會引發類似**sys.dm_exec_query_stats**。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  
  
> **注意：**的初始查詢**sys.dm_exec_procedure_stats**工作負載正在執行伺服器上是否可能會產生不正確的結果。 您可以重複執行查詢，以找出較精確的結果。  
  
> **Azure SQL 資料倉儲的注意 ！** 若要呼叫從[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名稱**sys.dm_pdw_nodes_exec_procedure_stats**。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|預存程序所在的資料庫識別碼。|  
|**object_id**|**int**|預存程序的物件識別碼。|  
|**型別**|**char(2)**|物件的類型：<br /><br /> P = SQL 預存程序<br /><br /> PC = 組件 (CLR) 預存程序<br /><br /> X = 擴充預存程序|  
|**type_desc**|**nvarchar （60)**|物件類型的描述：<br /><br /> SQL_STORED_PROCEDURE<br /><br /> CLR_STORED_PROCEDURE<br /><br /> EXTENDED_STORED_PROCEDURE|  
|**sql_handle**|**varbinary(64)**|這可用來建立相互關聯中的查詢**sys.dm_exec_query_stats** ，從內部執行此預存程序。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 此值可搭配**sys.dm_exec_cached_plans**動態管理檢視。<br /><br /> 當原生編譯的預存程序查詢記憶體最佳化的資料表時，一律為 0x000。|  
|**cached_time**|**datetime**|在快取中加入預存程序的時間。|  
|**last_execution_time**|**datetime**|上次執行預存程序的時間。|  
|**execution_count**|**bigint**|預存程序從上次編譯以來被執行的次數。|  
|**total_worker_time**|**bigint**|這個預存程序從編譯以來執行所耗用的 CPU 時間總量 (以微秒為單位)。<br /><br /> 如果原生編譯預存程序執行數次的時間都少於 1 毫秒， **total_worker_time** 可能就不準確。|  
|**last_worker_time**|**bigint**|預存程序上次執行所耗用的 CPU 時間 (以微秒為單位)。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|這個預存程序在單次執行期間曾耗用的最小 CPU 時間 (以微秒為單位)。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|這個預存程序在單次執行期間曾耗用的最大 CPU 時間 (以微秒為單位)。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|這個預存程序在編譯以來執行所執行的實體讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_physical_reads**|**bigint**|預存程序上次執行所執行的實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_physical_reads**|**bigint**|這個預存程序在單次期間曾執行的最小實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_physical_reads**|**bigint**|這個預存程序在單次期間曾執行的最大實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_writes**|**bigint**|這個預存程序在編譯以來執行所執行的邏輯寫入總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_writes**|**bigint**|上次執行計畫時修改的緩衝集區頁數。 如果已修改頁面，則不會計算寫入。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_writes**|**bigint**|這個預存程序在單次執行期間曾執行的最小邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_writes**|**bigint**|這個預存程序在單次執行期間曾執行的最大邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_reads**|**bigint**|這個預存程序在編譯以來執行所執行的邏輯讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_reads**|**bigint**|預存程序上次執行所執行的邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_reads**|**bigint**|這個預存程序在單次期間曾執行的最小邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_reads**|**bigint**|這個預存程序在單次期間曾執行的最大邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_elapsed_time**|**bigint**|這個預存程序完成執行經歷的總時間 (以微秒為單位)。|  
|**last_elapsed_time**|**bigint**|這個預存程序最近完成執行經歷的時間 (以微秒為單位)。|  
|**min_elapsed_time**|**bigint**|這個預存程序完成執行經歷的最小時間 (以微秒為單位)。|  
|**max_elapsed_time**|**bigint**|這個預存程序完成執行經歷的最大時間 (以微秒為單位)。|  
|**pdw_node_id**|**int**|**適用於**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]，[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此發行版本上的節點識別碼。|  
  
 <sup>1</sup>原生編譯的預存程序啟用統計資料收集時，會收集的工作者時間以毫秒為單位。 若查詢的執行時間少於一毫秒，其值將會是 0。  
  
## <a name="permissions"></a>Permissions  
在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。 
  
## <a name="remarks"></a>備註  
 預存程序執行完成時，就會更新檢視中的統計資料。  
  
## <a name="examples"></a>範例  
 下列範例會傳回平均經過時間所識別之前 10 項預存程序的相關資訊。  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'proc name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_procedure_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>請參閱＜  
 [執行相關動態管理檢視和函數 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text (） &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;TRANSACT-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)  
  
  


