---
title: sys.query_store_wait_stats & Amp;#40;transact-SQL&AMP;#41; |Microsoft Docs
ms.custom: ''
ms.date: 04/21/2017
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
ms.openlocfilehash: 68ceb35ee3ef2cb3db3233c7050380584163c317
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067918"
---
# <a name="sysquerystorewaitstats-transact-sql"></a>sys.query_store_wait_stats & Amp;#40;transact-SQL&AMP;#41;

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  包含查詢的等候資訊的相關資訊。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**wait_stats_id**|**bigint**|代表 plan_id、 runtime_stats_interval_id、 execution_type 和 wait_category 的等待統計資料的資料列的識別項。 它是唯一的僅針對過去的執行階段統計資料間隔。 目前使用的間隔，可能表示 execution_type wait_category 所代表的等候類別所表示的執行類型與參考 plan_id，計劃的等候統計資料的多個資料列。 一般而言，一個資料列代表等候的統計資料會排清至磁碟，而其他 (s) 代表記憶體中狀態。 因此，若要取得每個間隔中的實際狀態您需要彙總的度量，依 plan_id、 runtime_stats_interval_id、 execution_type 和 wait_category 群組。 |  
|**plan_id**|**bigint**|外部索引鍵。 加入[sys.query_store_plan &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)。|  
|**runtime_stats_interval_id**|**bigint**|外部索引鍵。 加入[sys.query_store_runtime_stats_interval &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-query-store-runtime-stats-interval-transact-sql.md)。|  
|**wait_category**|**tinyint**|等候類型會使用下表來分類，然後等候時間會加以彙總這些等候類別。 不同的等候類別需要不同的後續追蹤分析，以解決此問題，但是請等一下從相同的類別潛在客戶的型別，以類似的疑難排解體驗，並另外提供受影響的查詢，以等候是缺少的片段完成這類調查的大多數成功。|
|**wait_category_desc**|**nvarchar(128)**|等候類別目錄欄位的文字描述，請檢閱下表。|
|**execution_type**|**tinyint**|判斷執行查詢的類型：<br /><br /> 0-定期執行 （成功完成）<br /><br /> 3-用戶端起始已中止執行<br /><br /> 4-例外狀況已中止執行|  
|**execution_type_desc**|**nvarchar(128)**|文字執行的 [類型] 欄位的描述：<br /><br /> 0-一般<br /><br /> 3-已中止<br /><br /> 4-例外狀況|  
|**total_query_wait_time_ms**|**bigint**|總`CPU wait`查詢計劃的彙總間隔內的時間，並等候類別 （以毫秒為單位報告）。|
|**avg_query_wait_time_ms**|**float**|平均等候查詢計劃，每次執行 （以毫秒為單位報告） 的彙總間隔時間] 和 [等候分類內的持續時間。|
|**last_query_wait_time_ms**|**bigint**|上一次的等候持續時間的彙總間隔內的查詢計劃，並等候類別 （以毫秒為單位報告）。|
|**min_query_wait_time_ms**|**bigint**|最小值`CPU wait`查詢計劃的彙總間隔內的時間，並等候類別 （以毫秒為單位報告）。|
|**max_query_wait_time_ms**|**bigint**|最大`CPU wait`查詢計劃的彙總間隔內的時間，並等候類別 （以毫秒為單位報告）。|
|**stdev_query_wait_time_ms**|**float**|`Query wait` 持續時間的標準差的查詢計劃的彙總間隔內，並等候類別 （以毫秒為單位報告）。|

## <a name="wait-categories-mapping-table"></a>等候類別對應表

"%"做為萬用字元
  
|整數值|等候類別|包含在類別中等候類型|  
|-----------------|---------------|-----------------|  
|**0**|**Unknown**|Unknown |  
|**1**|**CPU**|SOS_SCHEDULER_YIELD|
|**2**|**背景工作執行緒**|THREADPOOL|
|**3**|**Lock**|LCK_M_%|
|**4**|**閂鎖**|LATCH_%|
|**5**|**緩衝區閂鎖**|PAGELATCH_%|
|**6**|**緩衝區 IO**|PAGEIOLATCH_%|
|**7**|**編譯***|RESOURCE_SEMAPHORE_QUERY_COMPILE|
|**8**|**SQL CLR**|CLR %、 SQLCLR %|
|**9**|**鏡像**|DBMIRROR %|
|**10**|**Transaction**|XACT %、 DTC %、 TRAN_MARKLATCH_ %、 第 %MSQL_XACT_ TRANSACTION_MUTEX|
|**11**|**閒置**|第 %SLEEP_ LAZYWRITER_SLEEP、 SQLTRACE_BUFFER_FLUSH、 SQLTRACE_INCREMENTAL_FLUSH_SLEEP、 SQLTRACE_WAIT_ENTRIES、 FT_IFTS_SCHEDULER_IDLE_WAIT、 XE_DISPATCHER_WAIT、 REQUEST_FOR_DEADLOCK_SEARCH、 LOGMGR_QUEUE、 ONDEMAND_TASK_QUEUE、 CHECKPOINT_佇列 XE_TIMER_EVENT|
|**12**|**Preemptive**|PREEMPTIVE_ %|
|**13**|**Service Broker**|BROKER_ % **（但不是 BROKER_RECEIVE_WAITFOR）**|
|**14**|**交易記錄 IO**|LOGMGR、 LOGBUFFER、 LOGMGR_RESERVE_APPEND、 LOGMGR_FLUSH、 LOGMGR_PMM_LOG、 CHKPT、 WRITELOG|
|**15**|**網路 IO**|ASYNC_NETWORK_IO, NET_WAITFOR_PACKET, PROXY_NETWORK_IO, EXTERNAL_SCRIPT_NETWORK_IOF|
|**16**|**平行處理原則**|CXPACKET EXCHANGE|
|**17**|**記憶體**|RESOURCE_SEMAPHORE、 CMEMTHREAD、 CMEMPARTITIONED、 EE_PMOLOCK、 MEMORY_ALLOCATION_EXT、 RESERVED_MEMORY_ALLOCATION_EXT、 MEMORY_GRANT_UPDATE|
|**18**|**使用者等待**|WAITFOR，WAIT_FOR_RESULTS，BROKER_RECEIVE_WAITFOR|
|**19**|**追蹤**|TRACEWRITE、 SQLTRACE_LOCK、 SQLTRACE_FILE_BUFFER、 SQLTRACE_FILE_WRITE_IO_COMPLETION、 SQLTRACE_FILE_READ_IO_COMPLETION、 SQLTRACE_PENDING_BUFFER_WRITERS、 SQLTRACE_SHUTDOWN、 QUERY_TRACEOUT、 TRACE_EVTNOTIFF|
|**20**|**全文檢索搜尋**|FT_RESTART_CRAWL、 全文檢索收集程式、 MSSEARCH、 FT_METADATA_MUTEX、 FT_IFTSHC_MUTEX、 FT_IFTSISM_MUTEX、 FT_IFTS_RWLOCK、 FT_COMPROWSET_RWLOCK、 FT_MASTER_MERGE、 FT_PROPERTYLIST_CACHE、 FT_MASTER_MERGE_COORDINATOR、 PWAIT_RESOURCE_SEMAPHORE_FT_PARALLEL_QUERY_SYNC|
|**21**|**其他磁碟 IO**|ASYNC_IO_COMPLETION、 IO_COMPLETION、 BACKUPIO、 WRITE_COMPLETION、 IO_QUEUE_LIMIT、 IO_RETRY|
|**22**|**複寫**|SE_REPL_ %、 REPL_ %、 %hadr_ **（但不是 HADR_THROTTLE_LOG_RATE_GOVERNOR）** ，PWAIT_HADR_ %replica_writes、 FCB_REPLICA_WRITE、 FCB_REPLICA_READ、 PWAIT_HADRSIM|
|**23**|**記錄檔的速率管理員**|LOG_RATE_GOVERNOR，POOL_LOG_RATE_GOVERNOR，HADR_THROTTLE_LOG_RATE_GOVERNOR INSTANCE_LOG_RATE_GOVERNOR|

**編譯**等候類別目前不支援。

## <a name="permissions"></a>Permissions

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
- [查詢存放區預存程序&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)  
