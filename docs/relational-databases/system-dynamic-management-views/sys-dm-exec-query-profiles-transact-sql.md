---
title: sys.dm_exec_query_profiles (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_query_profiles_TSQL
- sys.dm_exec_query_profiles_TSQL
- dm_exec_query_profiles
- sys.dm_exec_query_profiles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_query_profiles dynamic management view
ms.assetid: 54efc6cb-eea8-4f6d-a4d0-aa05eeb54081
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0b2f1bf4cf990c7888088388a8d9c65a45865a9f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727116"
---
# <a name="sysdmexecqueryprofiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  監視查詢執行時的即時查詢進度。 例如，使用此 DMV 判斷查詢的哪個部份執行得很慢。 使用描述欄位中識別的資料行可將此 DMV 與其他系統 DMV 聯結。 或者，使用時間戳記資料行，將此 DMV 與其他效能計數器 (例如效能監視器 xperf) 聯結在一起。  
  
## <a name="table-returned"></a>傳回的資料表  
 傳回的計數器是以每個執行緒的每個運算子為基礎。 這些結果是動態的，而且不符合現有選項的結果，例如只在查詢完成時建立輸出的 SET STATISTICS XML ON。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|識別此查詢執行所在的工作階段。 參考 dm_exec_sessions.session_id。|  
|request_id|**int**|識別目標要求。 參考 dm_exec_sessions.request_id。|  
|sql_handle|**varbinary(64)**|識別目標查詢。 參考 dm_exec_query_stats.sql_handle。|  
|plan_handle|**varbinary(64)**|識別目標查詢 (參考 dm_exec_query_stats.plan_handle)。|  
|physical_operator_name|**nvarchar(256)**|實體運算子名稱。|  
|node_id|**int**|識別查詢樹狀結構中的運算子節點。|  
|thread_id|**int**|區分屬於相同查詢運算子節點的執行緒 (針對平行查詢)。|  
|task_address|**varbinary(8)**|識別此執行緒使用的 SQLOS 工作。 參考 dm_os_tasks.task_address。|  
|row_count|**bigint**|目前為止運算子傳回的資料列數目。|  
|rewind_count|**bigint**|目前為止的倒轉數目。|  
|rebind_count|**bigint**|目前為止的重新繫結數目。|  
|end_of_scan_count|**bigint**|目前為止結束的掃描數目。|  
|estimate_row_count|**bigint**|估計的資料列數目。 將 estimated_row_count 與實際的 row_count 比較可能會很實用。|  
|first_active_time|**bigint**|初次呼叫運算子的時間 (以毫秒為單位)。|  
|last_active_time|**bigint**|最後呼叫運算子的時間 (以毫秒為單位)。|  
|open_time|**bigint**|開啟的時間戳記 (以毫秒為單位)。|  
|first_row_time|**bigint**|開啟第一個資料列的時間戳記 (以毫秒為單位)。|  
|last_row_time|**bigint**|開啟最後一個資料列的時間戳記 (以毫秒為單位)。|  
|close_time|**bigint**|關閉的時間戳記 (以毫秒為單位)。|  
|elapsed_time_ms|**bigint**|目標節點作業到目前為止所耗費的總時間 (以毫秒為單位)。|  
|cpu_time_ms|**bigint**|目標節點作業到目前為止所耗費的總 CPU 時間 (以毫秒為單位)。|  
|database_id|**smallint**|包含在上面執行讀取和寫入之物件的資料庫識別碼。|  
|object_id|**int**|正在上面執行讀取和寫入之物件的識別碼。 參考 sys.objects.object_id。|  
|index_id|**int**|資料列集開啟所依據的索引 (如果有的話)。|  
|scan_count|**bigint**|目前為止的資料表/索引掃描數目。|  
|logical_read_count|**bigint**|目前為止的邏輯讀取數目。|  
|physical_read_count|**bigint**|目前為止的實體讀取數目。|  
|read_ahead_count|**bigint**|目前為止的預先讀取數目。|  
|write_page_count|**bigint**|目前為止因為溢出的頁面寫入數目。|  
|lob_logical_read_count|**bigint**|目前為止的 LOB 邏輯讀取數目。|  
|lob_physical_read_count|**bigint**|目前為止的 LOB 實體讀取數目。|  
|lob_read_ahead_count|**bigint**|目前為止的 LOB 預先讀取數目。|  
|segment_read_count|**int**|目前為止的區段預先讀取數目。|  
|segment_skip_count|**int**|目前為止略過的區段數目。| 
|actual_read_row_count|**bigint**|殘餘述詞套用之前的運算子所讀取的資料列數目。| 
|estimated_read_row_count|**bigint**|**適用於：** 開頭[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]SP1。 <br/>估計的殘餘述詞套用之前，運算子來讀取的資料列數目。|  
  
## <a name="general-remarks"></a>一般備註  
 如果查詢計畫節點沒有任何 IO，所有與 IO 相關的計數器都會設定為 NULL。  
  
 此 DMV 報告之 IO 相關的計數器比起 SET STATISTICS I 報告的計數器，以下列兩種方式來得更為精細：  
  
-   SET STATISTICS IO 將所有 IO 的計數器群組為一個指定的資料表。 有了此 DMV，您就可以將執行 IO 之查詢計畫中每個節點分開的計數器送至資料表。  
  
-   如果有平行掃描，此 DMV 會針對掃描上運作的每個平行執行緒報告計數器。
 
 從開始[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]了 sp1 之後，分析基礎結構的標準查詢執行統計資料會有分析基礎結構的輕量型查詢執行統計資料中的並排顯示。 新的查詢執行程式碼剖析的統計資料基礎結構會大幅減少效能額外負荷，收集每個運算子的資料列的實際數目，查詢執行統計資料。 可以啟用這項功能，請使用 全域啟始[追蹤旗標 7412](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)，或使用 query_thread_profile 擴充的事件，會自動開啟。

>[!NOTE]
> CPU 和已耗用時間，不支援輕量型查詢執行統計資料分析基礎結構下以減少效能的影響。

 設定 XML ON 和 SET STATISTICS PROFILE ON 一律使用舊版查詢執行統計資料基礎結構程式碼剖析的統計資料。
  
## <a name="permissions"></a>Permissions  

在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`資料庫的權限。   
   
## <a name="examples"></a>範例  
 您打算使用 sys.dm_exec_query_profiles 執行分析的查詢的工作階段的步驟 1： 登入。 若要設定程式碼剖析的查詢會使用 SET STATISTICS PROFILE 上。 在此相同工作階段中執行查詢。  
  
```  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 不同於您的查詢執行所在工作階段的第二個工作階段的步驟 2： 登入。  
  
 下列陳述式摘要目前正在工作階段 54 中執行的查詢進度。 為了達成目的，它會計算每個節點所有執行緒的輸出資料列總數，並且將它和該節點的輸出資料列預估數比較。  
  
```  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關的動態管理檢視和函式 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

