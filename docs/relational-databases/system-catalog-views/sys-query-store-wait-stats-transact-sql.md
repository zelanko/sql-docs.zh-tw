---
title: sys.databases query_store_wait_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.query_store_wait_stats
- query_store_wait_stats
dev_langs:
- TSQL
helpviewer_keywords:
- query_store_wait_stats catalog view
- sys.query_store_wait_stats catalog view
ms.assetid: ccf7a57c-314b-450c-bd34-70749a02784a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6bff80fbe2b5022e12eca58de42192a3a1bb18d1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74190365"
---
# <a name="sysquery_store_wait_stats-transact-sql"></a>sys.databases query_store_wait_stats （Transact-sql）

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  包含查詢之等候資訊的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|資料列的識別碼，代表 plan_id、runtime_stats_interval_id、execution_type 和 wait_category 的等候統計資料。 只有過去的執行時間統計資料間隔才是唯一的。 對於目前使用中的間隔，可能會有多個資料列代表 plan_id 所參考之計畫的等候統計資料，並以 execution_type 所表示的執行類型，以及 wait_category 所表示的等候類別目錄。 通常，一個資料列代表排清到磁片的等候統計資料，而其他則表示記憶體中的狀態。 因此，若要取得每個間隔的實際狀態，您需要匯總計量、依 plan_id、runtime_stats_interval_id、execution_type 和 wait_category 進行分組。 |  
|**plan_id**|**bigint**|外鍵。 [Query_store_plan &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)的聯結。|  
|**runtime_stats_interval_id**|**bigint**|外鍵。 [Query_store_runtime_stats_interval &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)的聯結。|  
|**wait_category**|**tinyint**|使用下表來分類等候類型，然後在這些等候類別中匯總等候時間。 不同的等候類別需要不同的後續追蹤分析來解決問題，但來自相同類別的等候類型會導致類似的疑難排解體驗，並提供受影響的查詢，除了等待時間外，這是完成大部分這類調查的遺漏部分。|
|**wait_category_desc**|**nvarchar(128)**|如需 [等候類別目錄] 欄位的文字描述，請參閱下表。|
|**execution_type**|**tinyint**|決定查詢執行的類型：<br /><br /> 0-正常執行（成功完成）<br /><br /> 3-用戶端起始的中止執行<br /><br /> 4-例外狀況已中止執行|  
|**execution_type_desc**|**nvarchar(128)**|執行類型欄位的文字描述：<br /><br /> 0-一般<br /><br /> 3-已中止<br /><br /> 4-例外狀況|  
|**total_query_wait_time_ms**|**bigint**|匯總`CPU wait`間隔和等候類別中查詢計劃的總時間（以毫秒為單位來報告）。|
|**avg_query_wait_time_ms**|**float**|在匯總間隔和等候類別中，每次執行查詢計劃的平均等候持續時間（以毫秒為單位來報告）。|
|**last_query_wait_time_ms**|**bigint**|匯總間隔和等候類別中查詢計劃的最後等候持續時間（以毫秒為單位來報告）。|
|**min_query_wait_time_ms**|**bigint**|匯總`CPU wait`間隔和等候類別中查詢計劃的最小時間（以毫秒為單位來報告）。|
|**max_query_wait_time_ms**|**bigint**|匯總`CPU wait`間隔和等候類別中查詢計劃的最長時間（以毫秒為單位來報告）。|
|**stdev_query_wait_time_ms**|**float**|`Query wait`匯總間隔和等候類別中查詢計劃的持續時間標準差（以毫秒為單位來報告）。|

## <a name="wait-categories-mapping-table"></a>等候類別對應表

"%" 當做萬用字元使用
  
|整數值|等候類別|等候類型包含在類別中|  
|-----------------|---------------|-----------------|  
|**0**|**Unknown**|Unknown |  
|**1**|**使用率**|SOS_SCHEDULER_YIELD|
|**2**|**背景工作執行緒**|THREADPOOL|
|**3**|**狀**|LCK_M_%|
|**4**|**插銷**|LATCH_%|
|**5**|**緩衝區閂鎖**|PAGELATCH_%|
|**6**|**緩衝區 IO**|PAGEIOLATCH_%|
|**7**|**編譯***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR%、SQLCLR%|
|**9**|**鏡像**|DBMIRROR%|
|**10**|**事務**|交易%、DTC%、TRAN_MARKLATCH_%、MSQL_XACT_%、TRANSACTION_MUTEX|
|**11**|**Idle**|SLEEP_%、LAZYWRITER_SLEEP、SQLTRACE_BUFFER_FLUSH、SQLTRACE_INCREMENTAL_FLUSH_SLEEP、SQLTRACE_WAIT_ENTRIES、FT_IFTS_SCHEDULER_IDLE_WAIT、XE_DISPATCHER_WAIT、REQUEST_FOR_DEADLOCK_SEARCH、LOGMGR_QUEUE、ONDEMAND_TASK_QUEUE、CHECKPOINT_QUEUE、XE_TIMER_EVENT|
|**12**|**防患於未然**|PREEMPTIVE_%|
|**十三**|**Service Broker**|BROKER_% **（但不是 BROKER_RECEIVE_WAITFOR）**|
|**14**|**事務記錄 IO**|LOGMGR、LOGBUFFER、LOGMGR_RESERVE_APPEND、LOGMGR_FLUSH、LOGMGR_PMM_LOG、CHKPT、WRITELOG|
|**15**|**網路 IO**|ASYNC_NETWORK_IO、NET_WAITFOR_PACKET、PROXY_NETWORK_IO、EXTERNAL_SCRIPT_NETWORK_IOF|
|**1600**|**平行處理原則**|CXPACKET，EXCHANGE，HT%，BMP%，BP%|
|**17**|**記憶體**|RESOURCE_SEMAPHORE、CMEMTHREAD、CMEMPARTITIONED、EE_PMOLOCK、MEMORY_ALLOCATION_EXT、RESERVED_MEMORY_ALLOCATION_EXT、MEMORY_GRANT_UPDATE|
|**18**|**使用者等候**|WAITFOR、WAIT_FOR_RESULTS、BROKER_RECEIVE_WAITFOR|
|**19**|**追蹤**|TRACEWRITE、SQLTRACE_LOCK、SQLTRACE_FILE_BUFFER、SQLTRACE_FILE_WRITE_IO_COMPLETION、SQLTRACE_FILE_READ_IO_COMPLETION、SQLTRACE_PENDING_BUFFER_WRITERS、SQLTRACE_SHUTDOWN、QUERY_TRACEOUT、TRACE_EVTNOTIFF|
|**20**|**全文檢索搜尋**|FT_RESTART_CRAWL、全文檢索收集程式、MSSEARCH、FT_METADATA_MUTEX、FT_IFTSHC_MUTEX、FT_IFTSISM_MUTEX、FT_IFTS_RWLOCK、FT_COMPROWSET_RWLOCK、FT_MASTER_MERGE、FT_PROPERTYLIST_CACHE、FT_MASTER_MERGE_COORDINATOR、PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC|
|**21**|**其他磁片 IO**|ASYNC_IO_COMPLETION、IO_COMPLETION、BACKUPIO、WRITE_COMPLETION、IO_QUEUE_LIMIT、IO_RETRY|
|**22**|**複寫**|SE_REPL_%、REPL_%、HADR_% **（但不 HADR_THROTTLE_LOG_RATE_GOVERNOR）**、PWAIT_HADR_%、REPLICA_WRITES、FCB_REPLICA_WRITE、FCB_REPLICA_READ、PWAIT_HADRSIM|
|**23**|**記錄檔速率管理員**|LOG_RATE_GOVERNOR、POOL_LOG_RATE_GOVERNOR、HADR_THROTTLE_LOG_RATE_GOVERNOR、INSTANCE_LOG_RATE_GOVERNOR|

目前不支援**編譯**等候類別目錄。

## <a name="permissions"></a>權限

 需要 `VIEW DATABASE STATE` 權限。  
  
## <a name="see-also"></a>另請參閱

- [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)
- [sys.query_context_settings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-context-settings-transact-sql.md)
- [sys.query_store_plan &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)
- [sys.query_store_query &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-transact-sql.md)
- [sys.query_store_query_text &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-query-text-transact-sql.md)
- [sys.query_store_runtime_stats_interval &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)
- [使用查詢存放區監視效能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)
- [查詢存放區預存程序 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
