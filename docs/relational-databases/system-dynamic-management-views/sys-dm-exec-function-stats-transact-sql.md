---
title: _exec_function_stats (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_function_stats
- sys.dm_exec_function_stats_tsql
- dm_exec_function_stats
- dm_exec_function_stats_tsql
helpviewer_keywords:
- sys.dm_exec_function_stats dynamic management view
ms.assetid: 4c3d6a02-08e4-414b-90be-36b89a0e5a3a
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 89d66217536d5cd552eb11de67d6d97d21ec9f6e
ms.sourcegitcommit: c5e2aa3e4c3f7fd51140727277243cd05e249f78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/02/2019
ms.locfileid: "68742828"
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys.databases _exec_function_stats (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  傳回快取函數的匯總效能統計資料。 此視圖會針對每個快取函數計畫傳回一個資料列, 而且資料列的存留期只要函式維持快取。 從快取中移除函式時, 會從這個視圖中去除對應的資料列。 此時, 會引發效能統計資料 SQL 追蹤事件, 類似于**sys.databases**的執行。 傳回純量函數的相關資訊, 包括記憶體內建函式和 CLR 純量函數。 不會傳回資料表值函式的相關資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為避免公開此資訊, 包含不屬於連接租使用者之資料的每個資料列都會被篩選掉。  
  
> [!NOTE]
> **_Exec_function_stats**的結果可能會隨著每次執行而不同, 因為資料只會反映完成的查詢, 而不是仍在進行中的查詢。 

  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|函數所在的資料庫識別碼。|  
|**object_id**|**int**|函數的物件識別碼。|  
|**type**|**char(2)**|物件的類型： FN = 純量值函式|  
|**type_desc**|**nvarchar(60)**|物件類型的描述：SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|這可以用來與在此函式中執行的**sys.databases**中的查詢相互關聯。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 這個值可與 **_exec_cached_plans**動態管理檢視搭配使用。<br /><br /> 當原生編譯的函數查詢記憶體優化資料表時, 一律會0x000。|  
|**cached_time**|**datetime**|函數新增至快取的時間。|  
|**last_execution_time**|**datetime**|上次執行函數的時間。|  
|**execution_count**|**bigint**|函式自上次編譯以來執行的次數。|  
|**total_worker_time**|**bigint**|此函式在編譯以來執行所耗用的 CPU 時間總量 (以微秒為單位)。<br /><br /> 對於原生編譯的函式, 如果有多個執行花費的時間少於1毫秒, **total_worker_time**可能就不正確。|  
|**last_worker_time**|**bigint**|上次執行函數時所耗用的 CPU 時間 (以微秒為單位)。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|此函式在單次執行期間曾耗用的最小 CPU 時間 (以微秒為單位)。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|此函式在單次執行期間曾耗用的最大 CPU 時間 (以微秒為單位)。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|此函式在編譯以來執行所執行的實體讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_physical_reads**|**bigint**|上次執行函數時所執行的實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_physical_reads**|**bigint**|此函式在單次執行期間曾執行的最小實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_physical_reads**|**bigint**|此函式在單次執行期間曾執行的最大實體讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_writes**|**bigint**|這個函式在編譯後執行的邏輯寫入總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_writes**|**bigint**|上次執行計畫時修改的緩衝集區頁數。 如果已修改頁面，則不會計算寫入。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_writes**|**bigint**|這個函數在單次執行期間曾執行的最小邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_writes**|**bigint**|這個函數在單次執行期間曾執行的最大邏輯寫入數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_reads**|**bigint**|此函式在編譯以來執行所執行的邏輯讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_reads**|**bigint**|上次執行函數時所執行的邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_reads**|**bigint**|此函式在單次執行期間曾執行的最小邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_reads**|**bigint**|此函式在單次執行期間曾執行的最大邏輯讀取數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_elapsed_time**|**bigint**|此函式的完成執行經歷的總時間 (以微秒為單位)。|  
|**last_elapsed_time**|**bigint**|最近完成執行此函式的經過時間 (以微秒為單位)。|  
|**min_elapsed_time**|**bigint**|此函式已完成執行的最小經過時間 (以微秒為單位)。|  
|**max_elapsed_time**|**bigint**|此函式已完成執行的已耗用時間上限 (以微秒為單位)。|  
|**total_page_server_reads**|**bigint**|此函式在編譯以來執行所執行的頁面伺服器讀取總數。<br /><br /> **適用物件:** Azure SQL Database 超大規模資料庫。|  
|**last_page_server_reads**|**bigint**|上次執行函數時所執行的頁面伺服器讀取數目。<br /><br /> **適用物件:** Azure SQL Database 超大規模資料庫。|  
|**min_page_server_reads**|**bigint**|這個函式在單次執行期間曾執行的最小頁面伺服器讀取數。<br /><br /> **適用物件:** Azure SQL Database 超大規模資料庫。|  
|**max_page_server_reads**|**bigint**|這個函式在單次執行期間曾執行的最大頁面伺服器讀取數。<br /><br /> **適用物件:** Azure SQL Database 超大規模資料庫。|
  
## <a name="permissions"></a>Permissions  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上, `VIEW SERVER STATE`需要許可權。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高階層級上, `VIEW DATABASE STATE`需要資料庫的許可權。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] [標準] 和 [基本] 層上, 需要**伺服器管理員**或**Azure Active Directory 系統管理員**帳戶。   
  
## <a name="examples"></a>範例  
 下列範例會傳回平均經過時間所識別的前十個函數的相關資訊。  
  
```  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
 [執行相關的動態管理檢視和&#40;函數 transact-sql&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.databases _exec_trigger_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
