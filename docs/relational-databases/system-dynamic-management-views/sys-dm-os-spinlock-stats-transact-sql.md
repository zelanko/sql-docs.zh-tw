---
title: sys.dm_os_spinlock_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/03/2019
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats_TSQL
- dm_os_spinlock_stats
- sys.dm_os_spinlock_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_spinlock_stats dynamic management view
ms.assetid: ''
caps.latest.revision: ''
author: bluefooted
ms.author: pamela
manager: amitban
ms.workload: Inactive
ms.openlocfilehash: d26369b657848bf1ff092bc69fba1a6aa5850102
ms.sourcegitcommit: ab867100949e932f29d25a3c41171f01156e923d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/27/2019
ms.locfileid: "67420850"
---
# <a name="sysdmosspinlockstats-transact-sql"></a>sys.dm_os_spinlock_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

傳回依類型組織的所有單一執行緒存取鎖等候的相關資訊。  
  

|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|NAME|**nvarchar(256)**|執行緒同步鎖定類型的名稱。|  
|衝突|**bigint**|執行緒嘗試取得單一執行緒存取鎖，且被封鎖，因為另一個在目前執行緒的次數會保留單一執行緒存取鎖。|  
|執行微調|**bigint**|執行緒的次數執行迴圈，嘗試取得單一執行緒存取鎖。|  
|spins_per_collision|**real**|每個衝突的拋的比率。|  
|sleep_time|**bigint**|以毫秒為單位，執行緒所花費的輪詢時進入睡眠狀態的時間量。|  
|輪詢之外|**int**|「 旋轉 」 執行緒取得單一執行緒存取鎖就會失敗並產生排程器次數。|  


## <a name="permissions"></a>Permissions  
在  [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`權限。   
在  [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] Premium 層需要`VIEW DATABASE STATE`資料庫的權限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]標準和基本層，則需要**伺服器系統管理員**該**Azure Active Directory 管理員**帳戶。    
  
## <a name="remarks"></a>備註  
 
 sys.dm_os_spinlock_stats 可用來識別執行緒同步鎖定競爭的來源。 在某些情況下，您可能可以解決或減少執行緒同步鎖定競爭。 不過有些時候您可能還是必須連絡 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 客戶支援服務部門。  
  
 您可以使用連線，重設的 sys.dm_os_spinlock_stats 內容`DBCC SQLPERF`，如下所示：  
  
```  
DBCC SQLPERF ('sys.dm_os_spinlock_stats', CLEAR);  
GO  
```  
  
 此舉會將所有的計數器重設為 0。  
  
> [!NOTE]  
>  如果重新啟動 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，將無法保存這些統計資料。 所有的資料都是從上次重設統計資料之後，或是從 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 啟動之後開始累加計算。  
  
## <a name="spinlocks"></a>單一執行緒存取鎖  
 執行緒同步鎖定是用來序列化資料結構，這通常會保留一段時間的存取權的輕量型同步處理物件。 此執行緒當執行緒嘗試存取受其正由另一個執行緒的執行緒同步鎖定的資源時，會執行迴圈，或 「 啟動 」 並再試一次，存取的資源，而不立即產生與閂鎖或其他資源的 排程器等候。 執行緒會繼續的微調資源，或迴圈完成，此時執行緒將會產生排程器，並回到 可執行佇列。 這種做法有助於減少內容切換過多的執行緒，但執行緒同步鎖定競爭高時，大量的 CPU 使用率可能會觀察到。
   
 下表包含一些最常見的執行緒同步鎖定類型的簡短描述。  
  
|執行緒同步鎖定類型|描述|  
|-----------------|-----------------|  
|ABR|僅供內部使用。|
|ADB_CACHE|僅供內部使用。|
|ALLOC_CACHES_HASH|僅供內部使用。|
|APPENDONLY_STORAGE|僅供內部使用。|
|APRC_BACK_OFF_STATS|僅供內部使用。|
|APRC_EVENT_LIST|僅供內部使用。|
|APRC_QUEUE_LIST|僅供內部使用。|
|APRC_VALIDATION_QUEUE_LIST|僅供內部使用。|
|ASYNC_OP_ADMIN_CLIENT_REGISTRATION_LIST|僅供內部使用。|
|ASYNC_OP_ADMIN_WORK_REGISTRATION_HASH_TABLE|僅供內部使用。|
|ASYNCSTATSLIST|僅供內部使用。|
|BACKUP|僅供內部使用。|
|BACKUP_COPY_CONTEXT|僅供內部使用。|
|BACKUP_CTX|僅供內部使用。|
|BASE_XACT_HASH|僅供內部使用。|
|BLOCKER_ENUM|僅供內部使用。|
|BPREPARTITION|僅供內部使用。|
|BPWORKFILE|僅供內部使用。|
|BUF_HASH|僅供內部使用。|
|BUF_LINK|僅供內部使用。|
|BUF_WRITE_LOG|僅供內部使用。|
|CACHEOBJ_DBG|僅供內部使用。|
|CHANNELFORCECLOSEMANAGER|僅供內部使用。|
|CHECK_AGGREGATE_STATE|僅供內部使用。|
|CLR_HOSTTASK|僅供內部使用。|
|CLR_SPIN_LOCK|僅供內部使用。|
|CMED_DATABASE|僅供內部使用。|
|CMED_HASH_SET|僅供內部使用。|
|COLUMNDATASETSESSIONLIST|僅供內部使用。|
|COLUMNSTORE_HASHTABLE|僅供內部使用。|
|COLUMNSTOREBUILDSTATE_LIST|僅供內部使用。|
|COM_INIT|僅供內部使用。|
|認可|僅供內部使用。|
|COMPPLAN_SKELETON|僅供內部使用。|
|CONNECTION_MANAGER|僅供內部使用。|
|連接|僅供內部使用。|
|CSIBUILDMEM|僅供內部使用。|
|CURSOR|僅供內部使用。|
|CURSQL|僅供內部使用。|
|DATAPORTCONSUMER|僅供內部使用。|
|DATAPORTSOURCEINFOCREDIT|僅供內部使用。|
|DATAPORTSOURCEINFOQUEUE|僅供內部使用。|
|DATASET_FREELIST|僅供內部使用。|
|DBCC_CHECK|僅供內部使用。|
|DBSEEDING_OPERATION|僅供內部使用。|
|DBT_HASH|僅供內部使用。|
|DBT_IO_LIST|僅供內部使用。|
|DBTABLE|控制存取的記憶體中的資料結構中包含的屬性，該資料庫的 SQL Server 每一個資料庫。 請參閱[這篇文章](https://techcommunity.microsoft.com/t5/SQL-Server/Improving-Concurrency-Scalability-of-SQL-Server-workload-by/ba-p/384789)如需詳細資訊。 |
|DEFERRED_WF_EXT_DROP|僅供內部使用。|
|DEK_INSTANCE|僅供內部使用。|
|DELAYED_PARTITIONED_STACK|僅供內部使用。|
|DELETEBITMAP|僅供內部使用。|
|DIAG_MANAGER|僅供內部使用。|
|DIAG_OBJECT|僅供內部使用。|
|DIGEST_CACHE|僅供內部使用。|
|DINPBUF|僅供內部使用。|
|DIRECTLOGCONSUMER|僅供內部使用。|
|DP_LIST|控制項的存取權的中途分頁清單已開啟的間接檢查點的資料庫。 請參閱[這篇文章](https://techcommunity.microsoft.com/t5/SQL-Server/Indirect-Checkpoint-and-tempdb-8211-the-good-the-bad-and-the-non/ba-p/385510)如需詳細資訊。|
|DROP|僅供內部使用。|
|DROP_TEMPO|僅供內部使用。|
|DROPPED_ALLOC_UNIT|僅供內部使用。|
|DTC_HASHTABLE|僅供內部使用。|
|DTT_LIST|僅供內部使用。|
|ENDD_LIST|僅供內部使用。|
|EXT_CACHE|僅供內部使用。|
|EXTENT_ACTIVATION|僅供內部使用。|
|FABRIC_DB_MGR_PTR|僅供內部使用。|
|FABRIC_LOG_MANAGEMENT_INPUT_VALUE|僅供內部使用。|
|FABRIC_REPLICA_TRANSPORT|僅供內部使用。|
|FABRIC_TVF_DATA_CONSUMER_LIST|僅供內部使用。|
|FABRIC_TVF_LOAD_LIB|僅供內部使用。|
|FCB_REPLICA_SYNC|僅供內部使用。|
|FGCB_PRP_FILL|僅供內部使用。|
|FILE_HANDLE_CACHE|僅供內部使用。|
|FILE_TABLE|僅供內部使用。|
|FILESTREAM_CHUNKER|僅供內部使用。|
|FREE_SPACE_CACHE_ENTRY|僅供內部使用。|
|FS_CONTAINER_LIST_WITH_DELETE|僅供內部使用。|
|FS_DELETED_FOLDER_CLEANUP|僅供內部使用。|
|FSAGENT|僅供內部使用。|
|FSGHOST_STATUS|僅供內部使用。|
|FT_INIT|僅供內部使用。|
|GHOST_FREE|僅供內部使用。|
|GHOST_HASH|僅供內部使用。|
|GLOBAL_SCHEDULER_LIST|僅供內部使用。|
|GLOBAL_TRACE_FLAGS|僅供內部使用。|
|GLOBALTRANS|僅供內部使用。|
|GROUP_COMMIT_FEEDBACK_LOOP|僅供內部使用。|
|GUARDIAN|僅供內部使用。|
|HADR_AGH_X_ACCESS|僅供內部使用。|
|HADR_AR_CONTROLLER_COLLECTION|僅供內部使用。|
|HADR_AR_DB_MGR|僅供內部使用。|
|HADR_AR_TRANSPORT|僅供內部使用。|
|HADR_COMPRESSION_MGR_POOL|僅供內部使用。|
|HADR_FABRIC_FACTORY|僅供內部使用。|
|HADR_PRIORITY_QUEUE|僅供內部使用。|
|HADR_TRANSPORT_CONTROL|僅供內部使用。|
|HADR_TRANSPORT_LIST|僅供內部使用。|
|HADRSEEDINGLIST|僅供內部使用。|
|HOBT_DROPPED|僅供內部使用。|
|HOBT_HASH|僅供內部使用。|
|HTTP|僅供內部使用。|
|HTTP_CONNCACHE|僅供內部使用。|
|HTTP_ENDPOINT|僅供內部使用。|
|IDENTITY|僅供內部使用。|
|INDEX_CREATE|僅供內部使用。|
|IO_DISPENSER_PAUSE|僅供內部使用。|
|IO_RG_VOLUME_HASHTABLE|僅供內部使用。|
|IOREQ|僅供內部使用。|
|ISSRESOURCE|僅供內部使用。|
|KTM_ENLISTMENT|僅供內部使用。|
|LANG_RES_LOAD|僅供內部使用。|
|LIVE_TARGET_TVF|僅供內部使用。|
|LOCK_FREE_LIST|僅供內部使用。|
|LOCK_HASH|保護存取權會持有鎖定的相關資訊儲存在資料庫中的鎖定管理員雜湊表。 請參閱[這篇文章](https://support.microsoft.comkb/2926217)如需詳細資訊。|
|LOCK_NOTIFICATION|僅供內部使用。|
|LOCK_RESOURCE_ID|僅供內部使用。|
|LOCK_RW_ABTX_HASH_SET|僅供內部使用。|
|LOCK_RW_AGDB_HEALTH_DIAG|僅供內部使用。|
|LOCK_RW_CMED_HASH_SET|僅供內部使用。|
|LOCK_RW_DPT_TABLE|僅供內部使用。|
|LOCK_RW_IN_ROW_TRACKER|僅供內部使用。|
|LOCK_RW_LOGIN_RATE_STATS|僅供內部使用。|
|LOCK_RW_PVS_PAGE_TRACKER|僅供內部使用。|
|LOCK_RW_RBIO_REQ|僅供內部使用。|
|LOCK_RW_SECURITY_CACHE|僅供內部使用。|
|LOCK_RW_TEST|僅供內部使用。|
|LOCK_RW_WPR_BUCKET|僅供內部使用。|
|LOCK_SORT_STREAM|僅供內部使用。|
|LOCK_SQLSATELLITE_MESSAGE|僅供內部使用。|
|LOG_CONSOLIDATION|僅供內部使用。|
|LOG_RG_GOVERNOR|僅供內部使用。|
|LOGCACHE_ACCESS|僅供內部使用。|
|LOGFLUSHQ|僅供內部使用。|
|LOGIOSEQ|僅供內部使用。|
|LOGIOSEQMAPPENDINGMESSAGEQUEUE|僅供內部使用。|
|LOGLC|僅供內部使用。|
|LOGLFM|僅供內部使用。|
|LOGON_TRIGGER_CACHE|僅供內部使用。|
|LOGPOOL_HASHBUCKET|僅供內部使用。|
|LOGPOOL_REFCOUNTEDOBJECT|僅供內部使用。|
|LOGPOOL_SHAREDCACHEBUFFER|僅供內部使用。|
|LOGPOOL_SIZEPERRESOURCEPOOL|僅供內部使用。|
|LPE_BATCH|僅供內部使用。|
|LPE_SESSION|僅供內部使用。|
|LPE_SXTP|僅供內部使用。|
|LSID|僅供內部使用。|
|LSLIST|僅供內部使用。|
|LSNREFLIST|僅供內部使用。|
|LSS_SYNC_DTC|僅供內部使用。|
|MD_CHANGE_NOTIFICATION|僅供內部使用。|
|MDB_REMOTE_BATCH_STATS_HASH_TABLE|僅供內部使用。|
|MDB_REMOTE_SESSION_HASH_TABLE|僅供內部使用。|
|MEM_MGR|僅供內部使用。|
|MGR_CACHE|僅供內部使用。|
|MIGRATION_BUF_LIST|僅供內部使用。|
|NETCONN_ADDRESS|僅供內部使用。|
|ONDEMAND_TASK|僅供內部使用。|
|ONE_PROC_SIM_NODE_CONTEXT|僅供內部使用。|
|ONE_PROC_SIM_NODE_CONTEXT_LIST|僅供內部使用。|
|ONE_PROC_SIM_REPLICA_CONTEXT|僅供內部使用。|
|ONE_PROC_SIM_SERVICE_PARTITION|僅供內部使用。|
|OPT_IDX_MISS_ID|僅供內部使用。|
|OPT_IDX_MISS_KEY|僅供內部使用。|
|OPT_IDX_STATS|僅供內部使用。|
|OPT_INFO_MGR|僅供內部使用。|
|PAGE_WORKITEMLIST|僅供內部使用。|
|PAGECOPIER|僅供內部使用。|
|PARALLELREDOCACHE|僅供內部使用。|
|PARTITIONED_HEAP_FREE_LIST|僅供內部使用。|
|PROGRESS_REPORT|僅供內部使用。|
|QE_SHUTDOWN|僅供內部使用。|
|QSCAN_CACHE|僅供內部使用。|
|QUERY_EXEC_STATS|僅供內部使用。|
|QUERY_STORE_ASYNC_PERSIST|僅供內部使用。|
|QUERY_STORE_ASYNC_QUEUE_TLIST|僅供內部使用。|
|QUERY_STORE_CAPTURE_POLICY_INTERVAL|僅供內部使用。|
|QUERY_STORE_CAPTURE_POLICY_STATS|僅供內部使用。|
|QUERY_STORE_CAPTURE_POLICY_THRESHOLD|僅供內部使用。|
|QUERY_STORE_CURRENT_INTERVAL|僅供內部使用。|
|QUERY_STORE_HT_CACHE|僅供內部使用。|
|QUERY_STORE_LIST|僅供內部使用。|
|QUERY_STORE_PLAN_COMP_AGG|僅供內部使用。|
|QUERY_STORE_PLAN_LIST|僅供內部使用。|
|QUERY_STORE_READ_ONLY_FLAGS|僅供內部使用。|
|QUERY_STORE_SELF_AGG|僅供內部使用。|
|QUERY_STORE_STMT_COMP_AGG|僅供內部使用。|
|QUERYEXEC|僅供內部使用。|
|QUERYSCAN|僅供內部使用。|
|RANGE_GENERATION|僅供內部使用。|
|READ_AHEAD|僅供內部使用。|
|REDOMGRSTATE|僅供內部使用。|
|REMOTE_SESSION_CACHE|僅供內部使用。|
|REMOTEBLOCKIO|僅供內部使用。|
|REMOTEOP|僅供內部使用。|
|REPL_LOGREADER_HISTORY_CACHE|僅供內部使用。|
|REPL_LOGREADER_PERDB_HISTORY_CACHE|僅供內部使用。|
|RESMANAGER|僅供內部使用。|
|資源|僅供內部使用。|
|RESQUEUE|僅供內部使用。|
|RFS_THREAD_QUEUE|僅供內部使用。|
|RG_TIMER|僅供內部使用。|
|ROWGROUP_VERSIONS|僅供內部使用。|
|RPCCHANNELPOOL|僅供內部使用。|
|RPCPACKAGE|僅供內部使用。|
|RPCREQUESTORCONTEXT|僅供內部使用。|
|RWLOCK_LAST|僅供內部使用。|
|SATELLITE_CONNECTION|僅供內部使用。|
|SBS_CLIENT_ENDPOINTS|僅供內部使用。|
|SBS_CLIENT_REQUESTS|僅供內部使用。|
|SBS_DISPATCH|僅供內部使用。|
|SBS_PENDING|僅供內部使用。|
|SBS_SERVER_XACT_TASK_PROXY|僅供內部使用。|
|SBS_TRANSPORT|僅供內部使用。|
|SBS_UCS_DISPATCH|僅供內部使用。|
|安全性|僅供內部使用。|
|SECURITY_CACHE|僅供內部使用。|
|SECURITY_FEDAUTH_AAD_BECWSCONNS|僅供內部使用。|
|SEMANTIC_TICACHE|僅供內部使用。|
|SEQUENCED_OBJECT|僅供內部使用。|
|SEQUEUE_SIZED_THREADSAFE|僅供內部使用。|
|SESSION_KILLER|僅供內部使用。|
|SESSION_MANAGER|僅供內部使用。|
|SESSION_SEC_CONTEXT|僅供內部使用。|
|SETRANGE_SYNC|僅供內部使用。|
|SHARABLE_SESSION_OBJECTS|僅供內部使用。|
|SLO_INFO_LIST|僅供內部使用。|
|SNI|僅供內部使用。|
|SNI_NODE_PENDING_IO_QUEUE|僅供內部使用。|
|SOAPSESSIONS|僅供內部使用。|
|SOS_ABORT_TASK|僅供內部使用。|
|SOS_ACTIVEDESCRIPTOR|僅供內部使用。|
|SOS_BLOCKALLOCPARTIALLIST|僅供內部使用。|
|SOS_BLOCKDESCRIPTORBUCKET|僅供內部使用。|
|SOS_CACHESTORE|同步處理至各種記憶體中快取在 SQL Server 計畫快取或暫存資料表快取等的存取。 嚴重的競爭問題，此執行緒同步鎖定類型可以表示特定快取的競爭中根據許多不同的項目。 請連絡[!INCLUDE[msCoName](../../includes/msconame-md.md)]幫助您疑難排解此執行緒同步鎖定類型的客戶支援服務。 |
|SOS_CACHESTORE_CLOCK|僅供內部使用。|
|SOS_CLOCKALG_INTERNODE_SYNC|僅供內部使用。|
|SOS_DEBUG_HOOK|僅供內部使用。|
|SOS_DESCDATABUFFERLIST|僅供內部使用。|
|SOS_LARGEPAGE_ALLOCATOR|僅供內部使用。|
|SOS_MINITHREAD|僅供內部使用。|
|SOS_NODE|僅供內部使用。|
|SOS_OBJECT_POOL|僅供內部使用。|
|SOS_OBJECT_STORE|僅供內部使用。|
|SOS_OOM_CHECK|僅供內部使用。|
|SOS_PHYS_PAGE_CACHE|僅供內部使用。|
|SOS_RESOURCE_CLERK_LIST|僅供內部使用。|
|SOS_RINGBUFFER_RECORD|僅供內部使用。|
|SOS_RW|僅供內部使用。|
|SOS_SATELLITE_USER_POOL|僅供內部使用。|
|SOS_SCHEDULER|僅供內部使用。|
|SOS_SELIST_SIZED_SLOCK|僅供內部使用。|
|SOS_SUSPEND_QUEUE|僅供內部使用。|
|SOS_SYSTHREAD|僅供內部使用。|
|SOS_SYSTHREAD_DISPATCHER|僅供內部使用。|
|SOS_TASK|僅供內部使用。|
|SOS_TLIST|僅供內部使用。|
|SOS_VM_LOW|僅供內部使用。|
|SOS_WAIT_STATS|僅供內部使用。|
|SOS_WAITABLE_ADDRESS_HASHBUCKET|僅供內部使用。|
|SPIN_EVENT_MUTEX|僅供內部使用。|
|SPL_DISPATCHER_LIST|僅供內部使用。|
|SPL_DISPATCHER_QUEUE|僅供內部使用。|
|SPL_NONYIELD_ANALYSIS|僅供內部使用。|
|SPL_QUERY_STORE_CTX_INITIALIZED|僅供內部使用。|
|SPL_QUERY_STORE_EXEC_STATS_AGG|僅供內部使用。|
|SPL_QUERY_STORE_EXEC_STATS_READ|僅供內部使用。|
|SPL_QUERY_STORE_STATS_COOKIE_CACHE|僅供內部使用。|
|SPL_SOS_DISPATCHER|僅供內部使用。|
|SPL_TDS_PKT_QUEUE|僅供內部使用。|
|SPL_XE_BUFFER_MGR|僅供內部使用。|
|SPL_XE_DISPATCHER_QUEUE|僅供內部使用。|
|SPL_XE_NOTIFICATION_CALLBACK_LIST|僅供內部使用。|
|SPL_XE_SESSION_EVENT_MGR|僅供內部使用。|
|SPL_XE_SESSION_MGR|僅供內部使用。|
|SPL_XE_SESSION_TARGET_MGR|僅供內部使用。|
|SPT_PROFILE|僅供內部使用。|
|SQL_MGR|僅供內部使用。|
|SQL_NORM|僅供內部使用。|
|SQLTRACE_FILE_BUFFER|僅供內部使用。|
|SRVPROC|僅供內部使用。|
|STACK_HASHER|僅供內部使用。|
|SUBLATCH|僅供內部使用。|
|SUBPDESC|僅供內部使用。|
|SUBPDESC_LIST|僅供內部使用。|
|SVC_BROKER_CTRL|僅供內部使用。|
|SVC_BROKER_DEBUG_LIST|僅供內部使用。|
|SVC_BROKER_LIST|僅供內部使用。|
|SVC_BROKER_OBJECT|僅供內部使用。|
|SYNCPOINT_RESOURCE|僅供內部使用。|
|TaskElapsedExecutionMonitor|僅供內部使用。|
|TDS_TVP|僅供內部使用。|
|TESTTEAM|僅供內部使用。|
|TESTTEAMEXPONENTIAL|僅供內部使用。|
|TESTTEAMEXPONENTIALTASTAS|僅供內部使用。|
|TESTTEAMTASTAS|僅供內部使用。|
|TMP_SESS_KEY|僅供內部使用。|
|TSQL_DEBUG|僅供內部使用。|
|TXFRM_REPL|僅供內部使用。|
|VDI_OPERATION|僅供內部使用。|
|WINFAB_REPORT_FAULT|僅供內部使用。|
|WRITE_PAGE_RECORDER|僅供內部使用。|
|X_PACKET_LIST|僅供內部使用。|
|X_PIPE|僅供內部使用。|
|X_PIPE_DEMAND|僅供內部使用。|
|X_PORT|僅供內部使用。|
|XACT_LOCK_INFO|僅供內部使用。|
|XACT_LOCKINFO_TASK|僅供內部使用。|
|XACT_WORKSPACE|僅供內部使用。|
|XCB|僅供內部使用。|
|XCB_FREE_LIST|僅供內部使用。|
|XCB_HASH|僅供內部使用。|
|XCHNG_TRACE|僅供內部使用。|
|XDES|僅供內部使用。|
|XDES_HASH|僅供內部使用。|
|XDESMGR|僅供內部使用。|
|XDESTABLELIST|僅供內部使用。|
|XE_RATE_LIMITER_STRETCHDB|僅供內部使用。|
|XE_SESSION_STORAGE|僅供內部使用。|
|XID_ARRAY|僅供內部使用。|
|XIO_BLOCKLIST|僅供內部使用。|
|XIO_REQSTR|僅供內部使用。|
|XIO_SEQNUMBUMP|僅供內部使用。|
|XIOSTATS|僅供內部使用。|
|XTP_RT_DATA_LIST|僅供內部使用。|
|XTS_MGR|僅供內部使用。|
|XVB_CSN|僅供內部使用。|
|XVB_LIST|僅供內部使用。|
 

  
## <a name="see-also"></a>另請參閱  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [SQL Server 作業系統相關的動態管理檢視&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  

 [何時是單一執行緒存取鎖重要驅動程式的 CPU 使用率在 SQL Server？](https://techcommunity.microsoft.com/t5/SQL-Server-Support/When-is-Spinlock-a-Significant-Driver-of-CPU-utilization-in-SQL/ba-p/530142)

 [診斷和解決 SQL Server 上的執行緒同步鎖定競爭](https://www.microsoft.com/download/details.aspx?id=26666)
  
  


