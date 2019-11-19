---
title: sys.databases dm_exec_query_profiles （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 10/25/2019
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
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cd30a6c07bccde04bb38189fab00f688dd763356
ms.sourcegitcommit: f018eb3caedabfcde553f9a5fc9c3e381c563f1a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2019
ms.locfileid: "74165500"
---
# <a name="sysdm_exec_query_profiles-transact-sql"></a>sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

監視查詢執行時的即時查詢進度。 例如，使用此 DMV 判斷查詢的哪個部份執行得很慢。 使用描述欄位中識別的資料行可將此 DMV 與其他系統 DMV 聯結。 或者，使用時間戳記資料行，將此 DMV 與其他效能計數器 (例如效能監視器 xperf) 聯結在一起。  
  
## <a name="table-returned"></a>傳回的資料表  
傳回的計數器是以每個執行緒的每個運算子為基礎。 結果是動態的，而且不符合現有選項的結果，例如只有在查詢完成時才會建立輸出的 `SET STATISTICS XML ON`。  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|識別此查詢執行所在的工作階段。 參考 dm_exec_sessions.session_id。|  
|request_id|**int**|識別目標要求。 參考 dm_exec_sessions.request_id。|  
|sql_handle|**varbinary(64)**|這是一個標記，可唯一識別查詢所屬的批次或預存程式。 參考 dm_exec_query_stats.sql_handle。|  
|plan_handle|**varbinary(64)**|這是一個標記，可唯一識別已執行之批次的查詢執行計畫，且其計畫位於計畫快取中，或目前正在執行。 參考 dm_exec_query_stats. plan_handle。|  
|physical_operator_name|**nvarchar(256)**|實體運算子名稱。|  
|node_id|**int**|識別查詢樹狀結構中的運算子節點。|  
|thread_id|**int**|區分屬於相同查詢運算子節點的執行緒 (針對平行查詢)。|  
|task_address|**Varbinary （8）**|識別此執行緒使用的 SQLOS 工作。 參考 dm_os_tasks.task_address。|  
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
|elapsed_time_ms|**bigint**|目前為止，目標節點的作業所用的總時間（以毫秒為單位）。|  
|cpu_time_ms|**bigint**|目前為止目標節點的作業所使用的總 CPU 時間（以毫秒為單位）。|  
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
|actual_read_row_count|**bigint**|套用剩餘述詞之前，由運算子讀取的資料列數目。| 
|estimated_read_row_count|**bigint**|**適用物件：** 從 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] SP1 開始。 <br/>在套用剩餘述詞之前，由運算子讀取的估計資料列數目。|  
  
## <a name="general-remarks"></a>一般備註  
 如果 [查詢計劃] 節點沒有任何 i/o，所有 i/o 相關的計數器都會設定為 Null。  
  
 這個 DMV 所報告的 i/o 相關計數器，比下列兩種方式的 `SET STATISTICS IO` 所報告的更細微：  
  
-   `SET STATISTICS IO` 將所有 i/o 的計數器一起分組到指定的資料表。 使用此 DMV 時，會針對查詢計劃中的每個節點，取得對資料表執行 i/o 的個別計數器。  
  
-   如果有平行掃描，此 DMV 會針對掃描上運作的每個平行執行緒報告計數器。
 
從 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 開始，*標準查詢執行統計資料分析基礎結構*會與*輕量查詢執行統計資料分析基礎結構*並存存在。 `SET STATISTICS XML ON` 和 `SET STATISTICS PROFILE ON` 一律使用*標準查詢執行統計資料分析基礎結構*。 若要填入 `sys.dm_exec_query_profiles`，必須啟用其中一個查詢分析基礎結構。 如需詳細資訊，請參閱[查詢分析基礎結構](../../relational-databases/performance/query-profiling-infrastructure.md)。    

>[!NOTE]
> 調查中的查詢必須在已啟用查詢分析基礎結構**之後**啟動，在查詢開始之後啟用它將不會產生 `sys.dm_exec_query_profiles`的結果。 如需如何啟用查詢分析基礎結構的詳細資訊，請參閱[查詢分析基礎結構](../../relational-databases/performance/query-profiling-infrastructure.md)。

## <a name="permissions"></a>Permissions  
在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 受控實例上，需要 `db_owner` 資料庫角色的 `VIEW DATABASE STATE` 許可權和成員資格。   
在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 高階層級上，需要資料庫中的 `VIEW DATABASE STATE` 許可權。 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 標準和基本層上，需要**伺服器管理員**或 Azure Active Directory 的系統**管理員**帳戶。   
   
## <a name="examples"></a>範例  
 步驟1：登入您打算執行查詢的會話，您將使用 `sys.dm_exec_query_profiles`進行分析。 若要設定查詢進行分析，請使用 `SET STATISTICS PROFILE ON`。 在此相同工作階段中執行查詢。  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 步驟2：登入與執行查詢的會話不同的第二個會話。  
  
 下列陳述式摘要目前正在工作階段 54 中執行的查詢進度。 為了達成目的，它會計算每個節點所有執行緒的輸出資料列總數，並且將它和該節點的輸出資料列預估數比較。  
  
```sql  
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
 
