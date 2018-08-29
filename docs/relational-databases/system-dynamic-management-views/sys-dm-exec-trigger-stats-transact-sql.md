---
title: sys.dm_exec_trigger_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 01/10/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e4fafc4fb5f082c5be3c3c66537a5ff6d8e7d0f7
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085759"
---
# <a name="sysdmexectriggerstats-transact-sql"></a>sys.dm_exec_trigger_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回快取觸發程序的彙總效能統計資料。 此檢視會針對每個觸發程序包含一個資料列，而且資料列的存留期間與觸發程序維持快取狀態的時間一樣長。 從快取中移除觸發程序時，對應的資料列也會從這個檢視中刪除。 此時，效能統計資料 SQL 追蹤事件會引發類似**sys.dm_exec_query_stats**。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|觸發程序所在的資料庫識別碼。|  
|**object_id**|**int**|觸發程序的物件識別碼。|  
|**type**|**char(2)**|物件的類型：<br /><br /> TA = 組件 (CLR) 觸發程序<br /><br /> TR = SQL 觸發程序|  
|**Type_desc**|**nvarchar(60)**|物件類型的描述：<br /><br /> CLR_TRIGGER<br /><br /> SQL_TRIGGER|  
|**sql_handle**|**varbinary(64)**|這可用來將查詢中相互關聯**sys.dm_exec_query_stats**從執行的此觸發程序內。|  
|**plan_handle**|**varbinary(64)**|記憶體中計畫的識別碼。 這個識別碼是暫時性的，只有當計畫留在快取時才會保留。 此值可搭配**sys.dm_exec_cached_plans**動態管理檢視。|  
|**cached_time**|**datetime**|在快取中加入觸發程序的時間。|  
|**last_execution_time**|**datetime**|上次執行觸發程序的時間。|  
|**execution_count**|**bigint**|從上次編譯以來被執行觸發程序的次數。|  
|**total_worker_time**|**bigint**|CPU 時間，以百萬分之一秒為單位，編譯以來執行這個觸發程序所耗用的總金額。|  
|**last_worker_time**|**bigint**|觸發程序上次執行所耗用的 CPU 時間 (以微秒為單位)。|  
|**min_worker_time**|**bigint**|最大 CPU 時間，以百萬分之一秒為單位，此觸發程序在單次執行期間曾耗用。|  
|**max_worker_time**|**bigint**|最大 CPU 時間，以百萬分之一秒為單位，此觸發程序在單次執行期間曾耗用。|  
|**total_physical_reads**|**bigint**|編譯以來執行所執行的此觸發程序的實體讀取總數。|  
|**last_physical_reads**|**bigint**|實體讀取數執行最後一個觸發程序執行的時間。|  
|**min_physical_reads**|**bigint**|此觸發程序在單次執行期間曾執行的實體讀取的最小數目。|  
|**max_physical_reads**|**bigint**|此觸發程序在單次執行期間曾執行的實體讀取次數的數目上限。|  
|**total_logical_writes**|**bigint**|編譯以來執行所執行的此觸發程序的邏輯寫入總數。|  
|**last_logical_writes**|**bigint**|邏輯寫入數執行最後一個觸發程序執行的時間。|  
|**min_logical_writes**|**bigint**|此觸發程序在單次執行期間曾執行的邏輯寫入的最小數目。|  
|**max_logical_writes**|**bigint**|此觸發程序在單次執行期間曾執行的邏輯寫入的數目上限。|  
|**total_logical_reads**|**bigint**|編譯以來執行所執行的此觸發程序的邏輯讀取總數。|  
|**last_logical_reads**|**bigint**|邏輯讀取數執行最後一個觸發程序執行的時間。|  
|**min_logical_reads**|**bigint**|此觸發程序在單次執行期間曾執行的邏輯讀取次數的最小數目。|  
|**max_logical_reads**|**bigint**|此觸發程序在單次執行期間曾執行的邏輯讀取次數的數目上限。|  
|**total_elapsed_time**|**bigint**|已耗用時間總計，以百萬分之一秒為單位，此觸發程序完成執行。|  
|**last_elapsed_time**|**bigint**|這個觸發程序最近完成執行經歷的時間 (以微秒為單位)。|  
|**min_elapsed_time**|**bigint**|最小耗用時間 （毫秒），此觸發程序的任何已完成執行。|  
|**max_elapsed_time**|**bigint**|耗用時間上限，以百萬分之一秒為單位，任何在完成執行的此觸發程序。| 
|**total_spills**|**bigint**|編譯以來執行此觸發程序溢出的頁面總數。<br /><br /> **適用於**： 從[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**last_spills**|**bigint**|頁數溢出最後一個觸發程序執行的時間。<br /><br /> **適用於**： 從[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**min_spills**|**bigint**|此觸發程序曾經有在單次執行期間溢出的頁面最小數目。<br /><br /> **適用於**： 從[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
|**max_spills**|**bigint**|此觸發程序曾經有在單次執行期間溢出的頁面數目上限。<br /><br /> **適用於**： 從[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]CU3|  
  
## <a name="remarks"></a>備註  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，動態管理檢視不可以公開可能會影響資料庫內含項目的資訊或公開有關使用者可存取之其他資料庫的資訊。 為了避免公開此資訊，包含不屬於連接租用戶之資料的每個資料列都會被篩選出來。  

完成查詢時，會更新檢視中的統計資料。  
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
  
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
[執行相關動態管理檢視和函式&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
[sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
[sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
[sys.dm_exec_procedure_stats &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)   
[sys.dm_exec_cached_plans &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql.md)  
  
  
