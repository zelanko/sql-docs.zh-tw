---
title: sys.dm_exec_requests (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_requests_TSQL
- sys.dm_exec_requests
- dm_exec_requests_TSQL
- dm_exec_requests
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_requests dynamic management view
ms.assetid: 4161dc57-f3e7-4492-8972-8cfb77b29643
caps.latest.revision: 67
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 85c9decc6e59e3a35290081cbc0af59410c5db9d
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39548024"
---
# <a name="sysdmexecrequests-transact-sql"></a>sys.dm_exec_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  傳回在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行之每項要求的相關資訊。  
  
> [!NOTE]  
>  若要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部的程式碼 (例如，擴充預存程序和分散式查詢)，執行緒必須在非先佔式排程器的控制之外執行。 若要這麼做，工作者必須切換到先佔式模式。 這個動態管理檢視傳回的時間值不包括先佔式模式所花費的時間。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|這個要求相關的工作階段識別碼。 不可為 Null。|  
|request_id|**int**|要求的識別碼。 在工作階段的內容中是唯一的。 不可為 Null。|  
|start_time|**datetime**|要求到達時的時間戳記。 不可為 Null。|  
|status|**nvarchar(30)**|要求的狀態。 這可以是下列項目之一：<br /><br /> 背景<br />執行中<br />可執行的<br />休眠中<br />已暫停<br /><br /> 不可為 Null。|  
|command|**nvarchar(32)**|識別目前所處理命令的類型。 常見命令類型包括下列項目：<br /><br /> SELECT<br />Insert<br />UPDATE<br />Delete<br />BACKUP LOG<br />BACKUP DATABASE<br />DBCC<br />FOR<br /><br /> 要求的文字可使用 sys.dm_exec_sql_text 加上要求的對應 sql_handle 來擷取。 內部系統處理序會根據其所執行工作的類型來設定命令。 工作包括下列項目：<br /><br /> LOCK MONITOR<br />CHECKPOINTLAZY<br />WRITER<br /><br /> 不可為 Null。|  
|sql_handle|**varbinary(64)**|要求之 SQL 文字的雜湊對應。 可為 Null。|  
|statement_start_offset|**int**|目前執行的批次或預存程序中的字元數，目前執行的陳述式即從該處開始。 可與 sql_handle、statement_end_offset 和 sys.dm_exec_sql_text 動態管理函數一起使用，來擷取該要求目前執行的陳述式。 可為 Null。|  
|statement_end_offset|**int**|目前執行的批次或預存程序中的字元數，目前執行的陳述式即在該處結束。 可與 sql_handle、statement_end_offset 和 sys.dm_exec_sql_text 動態管理函數一起使用，來擷取該要求目前執行的陳述式。 可為 Null。|  
|plan_handle|**varbinary(64)**|SQL 執行計畫的雜湊對應。 可為 Null。|  
|database_id|**smallint**|要求執行目標的資料庫識別碼。 不可為 Null。|  
|user_id|**int**|提交要求之使用者的識別碼。 不可為 Null。|  
|connection_id|**uniqueidentifier**|要求到達所用連接的識別碼。 可為 Null。|  
|blocking_session_id|**smallint**|封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。<br /><br /> -2 = 封鎖資源是由被遺棄的分散式交易所擁有。<br /><br /> -3 = 封鎖資源是由延遲的復原交易所擁有。<br /><br /> -4 = 由於內部閂鎖狀態轉換，目前無法判斷封鎖閂鎖擁有者的工作階段識別碼。|  
|wait_type|**nvarchar(60)**|若要求目前被封鎖，這個資料行會傳回等候的類型。 可為 Null。<br /><br /> 如需等候的類型資訊，請參閱[sys.dm_os_wait_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|  
|wait_time|**int**|若要求目前被封鎖，這個資料行會傳回目前等候的持續時間 (以毫秒為單位)。 不可為 Null。|  
|last_wait_type|**nvarchar(60)**|如果這個要求先前被封鎖，這個資料行會傳回上次等候的類型。 不可為 Null。|  
|wait_resource|**nvarchar(256)**|若要求目前被封鎖，這個資料行會傳回要求目前等候的資源。 不可為 Null。|  
|open_transaction_count|**int**|為這項要求開啟的交易數目。 不可為 Null。|  
|open_resultset_count|**int**|為這項要求開啟的結果集數目。 不可為 Null。|  
|transaction_id|**bigint**|這項要求執行所在交易的識別碼。 不可為 Null。|  
|context_info|**varbinary(128)**|工作階段的 CONTEXT_INFO 值。 可為 Null。|  
|percent_complete|**real**|下列命令已完成工作的百分比：<br /><br /> ALTER INDEX REORGANIZE<br />含有 ALTER DATABASE 的 AUTO_SHRINK 選項<br />BACKUP DATABASE<br />DBCC CHECKDB<br />DBCC CHECKFILEGROUP<br />DBCC CHECKTABLE<br />DBCC INDEXDEFRAG<br />DBCC SHRINKDATABASE<br />DBCC SHRINKFILE<br />RECOVERY<br />RESTORE DATABASE<br />ROLLBACK<br />TDE ENCRYPTION<br /><br /> 不可為 Null。|  
|estimated_completion_time|**bigint**|僅供內部使用。 不可為 Null。|  
|cpu_time|**int**|要求所用的 CPU 時間 (以毫秒為單位)。 不可為 Null。|  
|total_elapsed_time|**int**|要求到達後所經過的總時間 (以毫秒為單位)。 不可為 Null。|  
|scheduler_id|**int**|排程這項要求之排程器的識別碼。 不可為 Null。|  
|task_address|**varbinary(8)**|配置給這項要求之關聯工作的記憶體位址。 可為 Null。|  
|reads|**bigint**|這項要求所執行的讀取數。 不可為 Null。|  
|writes|**bigint**|這項要求所執行的寫入數。 不可為 Null。|  
|logical_reads|**bigint**|這項要求所執行的邏輯讀取數。 不可為 Null。|  
|text_size|**int**|這項要求的 TEXTSIZE 設定。 不可為 Null。|  
|language|**nvarchar(128)**|這項要求的語言設定。 可為 Null。|  
|date_format|**nvarchar(3)**|這項要求的 DATEFORMAT 設定。 可為 Null。|  
|date_first|**smallint**|這項要求的 DATEFIRST 設定。 不可為 Null。|  
|quoted_identifier|**bit**|1 = 這項要求的 QUOTED_IDENTIFIER 是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|arithabort|**bit**|1 = 這項要求的 ARITHABORT 設定是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|ansi_null_dflt_on|**bit**|1 = 這項要求的 ANSI_NULL_DFLT_ON 設定是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|ansi_defaults|**bit**|1 = 這項要求的 ANSI_DEFAULTS 設定是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|ansi_warnings|**bit**|1 = 這項要求的 ANSI_WARNINGS 設定是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|ansi_padding|**bit**|1 = 這項要求的 ANSI_PADDING 設定是 ON。<br /><br /> 否則，它會是 0。<br /><br /> 不可為 Null。|  
|ansi_nulls|**bit**|1 = 這項要求的 ANSI_NULLS 設定是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|concat_null_yields_null|**bit**|1 = 這項要求的 CONCAT_NULL_YIELDS_NULL 設定是 ON。 否則，它會是 0。<br /><br /> 不可為 Null。|  
|transaction_isolation_level|**smallint**|建立這項要求之交易所用的隔離等級。 不可為 Null。<br /><br /> 0 = Unspecified<br /><br /> 1 = ReadUncomitted<br /><br /> 2 = ReadCommitted<br /><br /> 3 = Repeatable<br /><br /> 4 = Serializable<br /><br /> 5 = Snapshot|  
|lock_timeout|**int**|這項要求的鎖定逾時期限 (以毫秒為單位)。 不可為 Null。|  
|deadlock_priority|**int**|這項要求的 DEADLOCK_PRIORITY 設定。 不可為 Null。|  
|row_count|**bigint**|這項要求傳回用戶端的資料列數。 不可為 Null。|  
|prev_error|**int**|這項要求執行期間最後一次發生的錯誤。 不可為 Null。|  
|nest_level|**int**|這項要求所執行程式碼的目前巢狀層級。 不可為 Null。|  
|granted_query_memory|**int**|配置給這項要求之查詢執行的頁數。 不可為 Null。|  
|executing_managed_code|**bit**|指出特定要求目前是否正在執行 Common Language Runtime 物件 (如常式、類型和觸發程序)。 這是為 Common Language Runtime 物件在堆疊上的完全時間所設定，即使是從 Common Language Runtime 內部執行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 也是如此。 不可為 Null。|  
|group_id|**int**|這個查詢所屬工作負載群組的識別碼。 不可為 Null。|  
|query_hash|**binary(8)**|針對查詢所計算的二進位雜湊值，可用來識別含有類似邏輯的查詢。 您可以使用查詢雜湊判別只有常值不同之查詢的彙總資源使用狀況。|  
|query_plan_hash|**binary(8)**|從查詢執行計畫計算所得的二進位雜湊值將用於識別類似的查詢執行計畫。 您可以使用查詢計劃雜湊尋找具有類似執行計畫之查詢的累計成本。|  
|statement_sql_handle|**varbinary(64)**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 個別查詢的 SQL 控制代碼。 |  
|statement_context_id|**bigint**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> Sys.query_context_settings 選擇性外部索引鍵。 |  
|dop |**int** |**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 查詢的平行處理原則程度。 |  
|parallel_worker_count |**int** |**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 如果這是平行查詢的保留平行工作者數目。  |  
|external_script_request_id |**uniqueidentifier** |**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 與目前要求相關聯的外部指令碼要求識別碼。 |  
|is_resumable |**bit** |**適用於**： [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指出要求是否可繼續索引作業。 |  
  
## <a name="permissions"></a>Permissions  
 如果使用者擁有`VIEW SERVER STATE`伺服器的權限，使用者會看到所有執行的工作階段的執行個體上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 否則使用者會看到只有目前的工作階段。 `VIEW SERVER STATE` 無法授與在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]因此`sys.dm_exec_requests`會受限於目前的連接。 
  
## <a name="examples"></a>範例  
  
### <a name="a-finding-the-query-text-for-a-running-batch"></a>A. 尋找執行中批次的查詢文字  
 下列範例會查詢 `sys.dm_exec_requests` 來尋找重要查詢並且從輸出複製其 `sql_handle`。  
  
```  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 然後，若要取得陳述式文字，請使用複製的 `sql_handle` 搭配系統函數 `sys.dm_exec_sql_text(sql_handle)`。  
  
```  
SELECT * FROM sys.dm_exec_sql_text(< copied sql_handle >);  
GO  
```  
  
### <a name="b-finding-all-locks-that-a-running-batch-is-holding"></a>B. 尋找執行中批次持有的所有鎖定  
 下列範例會查詢**sys.dm_exec_requests**來尋找有趣的批次和複製其`transaction_id`從輸出中。  
  
```  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 然後，若要尋找鎖定資訊，請使用 複製`transaction_id`搭配系統函數**sys.dm_tran_locks**。  
  
```  
SELECT * FROM sys.dm_tran_locks   
WHERE request_owner_type = N'TRANSACTION'   
    AND request_owner_id = < copied transaction_id >;  
GO  
```  
  
### <a name="c-finding-all-currently-blocked-requests"></a>C. 尋找所有目前封鎖的要求  
 下列範例會查詢**sys.dm_exec_requests**來尋找有關封鎖要求的資訊。  
  
```  
SELECT session_id ,status ,blocking_session_id  
    ,wait_type ,wait_time ,wait_resource   
    ,transaction_id   
FROM sys.dm_exec_requests   
WHERE status = N'suspended';  
GO  
```  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [執行相關動態管理檢視和函式&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_os_memory_clerks &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)   
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_exec_query_memory_grants &#40;-SQL&AMP;#41;&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
