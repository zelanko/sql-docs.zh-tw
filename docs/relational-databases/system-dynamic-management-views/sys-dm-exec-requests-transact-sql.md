---
title: _exec_requests （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: pmasl
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fbd23a685507b62529477d6ef92dbbbd1980c5c1
ms.sourcegitcommit: 4c7151f9f3f341f8eae70cb2945f3732ddba54af
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/27/2019
ms.locfileid: "71326161"
---
# <a name="sysdm_exec_requests-transact-sql"></a>sys.dm_exec_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中執行之每項要求的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|這個要求相關的工作階段識別碼。 不可為 Null。|  
|request_id|**int**|要求的識別碼。 在工作階段的內容中是唯一的。 不可為 Null。|  
|start_time|**datetime**|要求到達時的時間戳記。 不可為 Null。|  
|status|**nvarchar(30)**|要求的狀態。 這可以是下列項目之一：<br /><br /> 背景<br />執行中<br />可執行的<br />休眠中<br />已暫停<br /><br /> 不可為 Null。|  
|command|**nvarchar(32)**|識別目前所處理命令的類型。 常見命令類型包括下列項目：<br /><br /> SELECT<br />Insert<br />UPDATE<br />DELETE<br />BACKUP LOG<br />BACKUP DATABASE<br />DBCC<br />FOR<br /><br /> 要求的文字可使用 sys.dm_exec_sql_text 加上要求的對應 sql_handle 來擷取。 內部系統處理序會根據其所執行工作的類型來設定命令。 工作包括下列項目：<br /><br /> LOCK MONITOR<br />CHECKPOINTLAZY<br />WRITER<br /><br /> 不可為 Null。|  
|sql_handle|**varbinary(64)**|這是一個標記，可唯一識別查詢所屬的批次或預存程式。 可為 Null。|  
|statement_start_offset|**int**|目前執行的批次或預存程序中的字元數，目前執行的陳述式即從該處開始。 可與 sql_handle、statement_end_offset 和 sys.dm_exec_sql_text 動態管理函數一起使用，來擷取該要求目前執行的陳述式。 可為 Null。|  
|statement_end_offset|**int**|目前執行的批次或預存程序中的字元數，目前執行的陳述式即在該處結束。 可與 sql_handle、statement_end_offset 和 sys.dm_exec_sql_text 動態管理函數一起使用，來擷取該要求目前執行的陳述式。 可為 Null。|  
|plan_handle|**varbinary(64)**|這是一個標記，可唯一識別目前執行之批次的查詢執行計畫。 可為 Null。|  
|database_id|**smallint**|要求執行目標的資料庫識別碼。 不可為 Null。|  
|user_id|**int**|提交要求之使用者的識別碼。 不可為 Null。|  
|connection_id|**uniqueidentifier**|要求到達所用連接的識別碼。 可為 Null。|  
|blocking_session_id|**smallint**|封鎖要求之工作階段的識別碼。 如果這個資料行是 NULL，表示要求沒有被封鎖，或者封鎖工作階段的工作階段資訊無法使用 (或無法識別)。<br /><br /> -2 = 封鎖資源是由被遺棄的分散式交易所擁有。<br /><br /> -3 = 封鎖資源是由延遲的復原交易所擁有。<br /><br /> -4 = 由於內部閂鎖狀態轉換，目前無法判斷封鎖閂鎖擁有者的工作階段識別碼。|  
|wait_type|**nvarchar(60)**|若要求目前被封鎖，這個資料行會傳回等候的類型。 可為 Null。<br /><br /> 如需等候類型的詳細資訊，請參閱[sys.databases _os_wait_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)。|  
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
|quoted_identifier|**bit**|1 = 這項要求的 QUOTED_IDENTIFIER 是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
|arithabort|**bit**|1 = 這項要求的 ARITHABORT 設定是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
|ansi_null_dflt_on|**bit**|1 = 這項要求的 ANSI_NULL_DFLT_ON 設定是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
|ansi_defaults|**bit**|1 = 這項要求的 ANSI_DEFAULTS 設定是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
|ansi_warnings|**bit**|1 = 這項要求的 ANSI_WARNINGS 設定是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
|ansi_padding|**bit**|1 = 這項要求的 ANSI_PADDING 設定是 ON。<br /><br /> 否則，它是0。<br /><br /> 不可為 Null。|  
|ansi_nulls|**bit**|1 = 這項要求的 ANSI_NULLS 設定是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
|concat_null_yields_null|**bit**|1 = 這項要求的 CONCAT_NULL_YIELDS_NULL 設定是 ON。 否則，它是0。<br /><br /> 不可為 Null。|  
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
|statement_sql_handle|**varbinary(64)**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 個別查詢的 SQL 控制碼。<br /><br />如果資料庫未啟用查詢存放區，則此資料行為 Null。 |  
|statement_context_id|**bigint**|**適用於**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> Query_coNtext_settings 的選擇性外鍵。<br /><br />如果資料庫未啟用查詢存放區，則此資料行為 Null。 |  
|dop |**int** |**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 查詢的平行處理原則程度。 |  
|parallel_worker_count |**int** |**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 如果這是平行查詢，則為保留的平行背景工作數目。  |  
|external_script_request_id |**uniqueidentifier** |**適用於**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 與目前要求相關聯的外部腳本要求識別碼。 |  
|is_resumable |**bit** |**適用於**： [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 至 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 指出要求是否為可繼續的索引作業。 |  
|page_resource |**binary(8)** |**適用於**：[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)]<br /><br /> 如果`wait_resource`資料行包含頁面，則為頁面資源的8位元組十六進位標記法。 如需詳細資訊，請參閱[fn_PageResCracker](../../relational-databases/system-functions/sys-fn-pagerescracker-transact-sql.md)。 |  
|page_server_reads|**bigint**|**適用於**：Azure SQL Database 超大規模資料庫<br /><br /> 此要求所執行的頁面伺服器讀取數目。 不可為 Null。|  

## <a name="remarks"></a>備註 
若要執行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外部的程式碼 (例如，擴充預存程序和分散式查詢)，執行緒必須在非先佔式排程器的控制之外執行。 若要這麼做，工作者必須切換到先佔式模式。 這個動態管理檢視傳回的時間值不包括先佔式模式所花費的時間。

在資料[列模式](../../relational-databases/query-processing-architecture-guide.md#row-mode-execution)中執行平行要求[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]時，會指派背景工作執行緒來協調負責完成指派給它們之工作的工作者執行緒。 在此 DMV 中，只會顯示要求的協調器執行緒。 系統**不**會針對協調器執行緒更新資料行 [**讀取**]、[**寫入**]、[ **logical_reads**] 和 [ **row_count** ]。 只有協調器執行緒**才會更新** **wait_type**、 **wait_time**、 **last_wait_type**、 **wait_resource**和**granted_query_memory**資料行。 如需詳細資訊，請參閱[執行緒和工作架構指南](../../relational-databases/thread-and-task-architecture-guide.md)。

## <a name="permissions"></a>Permissions
如果使用者具有`VIEW SERVER STATE`伺服器的許可權，則使用者會看到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]實例上所有執行中的會話; 否則，使用者只會看到目前的會話。 `VIEW SERVER STATE`無法在中[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]授與`sys.dm_exec_requests` ，因此一律限制為目前的連接。
  
## <a name="examples"></a>範例  
  
### <a name="a-finding-the-query-text-for-a-running-batch"></a>A. 尋找執行中批次的查詢文字

 下列範例會查詢 `sys.dm_exec_requests` 來尋找重要查詢並且從輸出複製其 `sql_handle`。  

```sql
SELECT * FROM sys.dm_exec_requests;  
GO  
```  

然後，若要取得陳述式文字，請使用複製的 `sql_handle` 搭配系統函數 `sys.dm_exec_sql_text(sql_handle)`。  

```sql
SELECT * FROM sys.dm_exec_sql_text(< copied sql_handle >);  
GO  
```

### <a name="b-finding-all-locks-that-a-running-batch-is-holding"></a>B. 尋找執行中批次持有的所有鎖定

下列範例會查詢 **_exec_requests**以尋找感興趣的批次，並從輸出`transaction_id`複製其。

```sql
SELECT * FROM sys.dm_exec_requests;  
GO
```

然後，若要尋找鎖定資訊，請使用`transaction_id`以系統函數 **_tran_locks**所複製的。  

```sql
SELECT * FROM sys.dm_tran_locks
WHERE request_owner_type = N'TRANSACTION'
    AND request_owner_id = < copied transaction_id >;
GO  
```

### <a name="c-finding-all-currently-blocked-requests"></a>C. 尋找所有目前封鎖的要求

下列範例會查詢 **_exec_requests**以尋找已封鎖要求的相關資訊。  

```sql
SELECT session_id ,status ,blocking_session_id  
    ,wait_type ,wait_time ,wait_resource
    ,transaction_id
FROM sys.dm_exec_requests
WHERE status = N'suspended';  
GO  
```  

### <a name="d-ordering-existing-requests-by-cpu"></a>D. 依 CPU 排序現有要求

```sql
SELECT 
   req.session_id
   , req.start_time
   , cpu_time 'cpu_time_ms'
   , object_name(st.objectid,st.dbid) 'ObjectName' 
   , substring
      (REPLACE
        (REPLACE
          (SUBSTRING
            (ST.text
            , (req.statement_start_offset/2) + 1
            , (
               (CASE statement_end_offset
                  WHEN -1
                  THEN DATALENGTH(ST.text)  
                  ELSE req.statement_end_offset
                  END
                    - req.statement_start_offset)/2) + 1)
       , CHAR(10), ' '), CHAR(13), ' '), 1, 512)  AS statement_text  
FROM sys.dm_exec_requests AS req  
   CROSS APPLY sys.dm_exec_sql_text(req.sql_handle) as ST
   ORDER BY cpu_time desc;
GO
```

## <a name="see-also"></a>另請參閱

- [動態管理檢視和函數](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [執行相關的動態管理檢視和函數](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
- [sys.dm_os_memory_clerks](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-clerks-transact-sql.md)
- [sys.dm_os_sys_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)
- [sys.dm_exec_query_memory_grants](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-memory-grants-transact-sql.md)
- [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)
- [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)  
