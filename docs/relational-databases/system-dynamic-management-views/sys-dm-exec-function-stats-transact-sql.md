---
title: sys.dm_exec_function_stats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse
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
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 51f94535dcc29e1da3156d661ff9e1f6bdc2cf2a
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39537078"
---
# <a name="sysdmexecfunctionstats-transact-sql"></a>sys.dm_exec_function_stats & Amp;#40;transact-SQL&AMP;#41;
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  傳回彙總快取的函式的效能統計資料。 此檢視會傳回一個資料列，每個快取的函式計畫，而且資料列的存留期，只要函式保持快取。 從快取移除函式時，也會刪除對應的資料列從這個檢視。 此時，效能統計資料 SQL 追蹤事件會引發類似**sys.dm_exec_query_stats**。 傳回純量函式，包括記憶體中的函式和 CLR 純量函式的相關資訊。 不會傳回資料表值函式的相關資訊。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  
  
> [!NOTE]
> 初始查詢**sys.dm_exec_function_stats**可能會產生不正確的結果，如果沒有目前在伺服器上執行的工作負載。 您可以重複執行查詢，以找出較精確的結果。  
  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|此函式所在的資料庫識別碼。|  
|**object_id**|**int**|函式的物件識別碼。|  
|**type**|**char(2)**|物件的型別： FN = 純量值函式|  
|**type_desc**|**nvarchar(60)**|物件類型的描述： SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|這可用來將查詢中相互關聯**sys.dm_exec_query_stats** ，從內部執行此函式。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 此值可搭配**sys.dm_exec_cached_plans**動態管理檢視。<br /><br /> 一律為 0x000 時的原生編譯的函式的查詢記憶體最佳化資料表。|  
|**cached_time**|**datetime**|此函式加入快取的時間。|  
|**last_execution_time**|**datetime**|函式執行了過去的時間。|  
|**execution_count**|**bigint**|從上次編譯以來被執行的函式的次數。|  
|**total_worker_time**|**bigint**|總 CPU 時間量以百萬分之一秒為單位，從編譯以來所執行的這個函式耗用。<br /><br /> 針對原生編譯的函式， **total_worker_time**可能不正確，如果執行採用少於 1 毫秒。|  
|**last_worker_time**|**bigint**|CPU 時間，以百萬分之一秒為單位，已耗用的函式執行了。 <sup>1</sup>|  
|**min_worker_time**|**bigint**|最小 CPU 時間，以百萬分之一秒為單位，在單次執行期間曾耗用此函式。 <sup>1</sup>|  
|**max_worker_time**|**bigint**|最大 CPU 時間，以百萬分之一秒為單位，在單次執行期間曾耗用此函式。 <sup>1</sup>|  
|**total_physical_reads**|**bigint**|編譯以來執行所執行此函式的實體讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_physical_reads**|**bigint**|實體讀取數執行的上次執行的函式。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_physical_reads**|**bigint**|此函式在單次執行期間曾執行的實體讀取的最小數目。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_physical_reads**|**bigint**|此函式在單次執行期間曾執行的實體讀取的最大數目。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_writes**|**bigint**|編譯以來執行所執行此函式的邏輯寫入總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_writes**|**bigint**|上次執行計畫時修改的緩衝集區頁數。 如果已修改頁面，則不會計算寫入。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_writes**|**bigint**|此函式在單次執行期間曾執行的邏輯寫入的最小數目。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_writes**|**bigint**|此函式在單次執行期間曾執行的邏輯寫入的數目上限。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_logical_reads**|**bigint**|編譯以來執行所執行此函式的邏輯讀取總數。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**last_logical_reads**|**bigint**|邏輯讀取數執行的上次執行的函式。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**min_logical_reads**|**bigint**|此函式在單次執行期間曾執行的邏輯讀取次數的最小數目。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**max_logical_reads**|**bigint**|此函式在單次執行期間曾執行的邏輯讀取次數的數目上限。<br /><br /> 查詢記憶體最佳化的資料表時一律為 0。|  
|**total_elapsed_time**|**bigint**|總耗用時間，以百萬分之一秒為單位，屬於此函式完成執行。|  
|**last_elapsed_time**|**bigint**|經過時間，以百萬分之一秒為單位，最近完成執行此函式中。|  
|**min_elapsed_time**|**bigint**|耗用時間下限，以百萬分之一秒為單位，任何在完成執行此函式。|  
|**max_elapsed_time**|**bigint**|耗用時間上限，以百萬分之一秒為單位，任何在完成執行此函式。|  
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
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
 [執行相關動態管理檢視和函式&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
  
