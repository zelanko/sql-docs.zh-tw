---
title: sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_workload_groups_history_ex_TSQL
- sys.dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex
- dm_resource_governor_workload_groups_history_ex_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_resource_governor_workload_groups_history_ex dynamic management view
author: joesackmsft
ms.author: josack
ms.openlocfilehash: ac776813cb817d1357948091bfc48c981fa8e730
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053266"
---
# <a name="sysdmresourcegovernorworkloadgroupshistoryex-azure-sql-database"></a>sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回快照集，以 15 秒間隔過去 30 分鐘的資源集區統計資料，Azure SQL database。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**| ssNoversion |資源集區的識別碼。 不可為 Null。|
|**group_id**| ssNoversion |工作負載群組的識別碼。 不可為 Null。|
|**name**| nvarchar(256) |工作負載群組的名稱。 不可為 Null。|
|**snapshot_time**| datetime |所建立的資源群組統計資料快照的日期時間。|
|**duration_ms**| ssNoversion |目前和先前的快照集之間的持續時間。|
|**active_worker_count**| ssNoversion |將背景工作角色總數，在目前的快照集。|
|**active_request_count**| ssNoversion |目前的要求計數。 不可為 Null。|
|**active_session_count**| ssNoversion |總作用中工作階段中目前的快照集。|
|**total_request_count**| BIGINT |已在工作負載群組中完成之要求的累計計數。 不可為 Null。|
|**delta_request_count**| ssNoversion |自上一個快照集的工作負載群組中的已完成要求的計數。 不可為 Null。|
|**total_cpu_usage_ms**| BIGINT |此工作負載群組的累計 CPU 使用量 (以毫秒為單位)。 不可為 Null。|
|**delta_cpu_usage_ms**| ssNoversion |在上一個快照集以來的毫秒數的 CPU 使用量。 不可為 Null。|
|**delta_cpu_usage_preemptive_ms**| ssNoversion |先佔式 win32 呼叫不會控管由 SQL CPU RG，自上一個快照集。|
|**delta_reads_reduced_memgrant_count**| ssNoversion |最後一個快照集之後達到最大查詢大小限制的記憶體授權數目。 不可為 Null。|
|**reads_throttled**| ssNoversion |節流的讀取總數。|
|**delta_reads_queued**| ssNoversion |讀取自上一個快照集總數的 IOs 加入佇列。 可為 Null。 如果資源群組不受 IO 管制，則為 null。|
|**delta_reads_issued**| ssNoversion |讀取自最後一個快照以來所發出的 Io 總數。 可為 Null。 如果資源群組不受 IO 管制，則為 null。|
|**delta_reads_completed**| ssNoversion |讀取自最後一個快照以來已完成的 Io 總數。 不可為 Null。|
|**delta_read_bytes**| BIGINT |上一個快照集之後，讀取的位元組總數。 不可為 Null。|
|**delta_read_stall_ms**| ssNoversion |總時間 （以毫秒為單位） 讀取的 IO 從抵達到最後一個快照相比的完成。 不可為 Null。|
|**delta_read_stall_queued_ms**| ssNoversion |總時間 （以毫秒為單位） 讀取 IO 從抵達到最後一個快照相比的問題。 可為 Null。 如果資源群組不受 IO 管制，則為 null。 非零 delta_read_stall_queued_ms 表示 IO 會受到 RG。|
|**delta_writes_queued**| ssNoversion |自最後一個快照以來加入佇列的 IOs 寫入總數。 可為 Null。 如果資源群組不受 IO 管制，則為 null。|
|**delta_writes_issued**| ssNoversion |最後一個快照集之後所發出的 Io 寫入總數。 可為 Null。 如果資源群組不受 IO 管制，則為 null。|
|**delta_writes_completed**| ssNoversion |自最後一個快照以來已完成的 Io 寫入總數。 不可為 Null。|
|**delta_writes_bytes**| BIGINT |上一個快照集之後寫入的位元組總數。 不可為 Null。|
|**delta_write_stall_ms**| ssNoversion |總時間 （以毫秒為單位） 寫入 IO 從抵達到完成，因為上一個快照集。 不可為 Null。|
|**delta_background_writes**| ssNoversion |最後一個快照相比的背景工作執行總寫入。|
|**delta_background_write_bytes**| BIGINT |總寫入大小的背景工作執行，因為上一個快照集，以位元組為單位。|
|**delta_log_bytes_used**| BIGINT |使用自上一個快照集，以位元組為單位的記錄。|
|**delta_log_temp_db_bytes_used**| BIGINT |Tempdb 記錄檔，以位元組為單位的上一個快照集之後使用。|
|**delta_query_optimizations**| BIGINT |此工作負載群組中的查詢最佳化，因為上一個快照集數目。 不可為 Null。|
|**delta_suboptimal_plan_generations**| BIGINT |自從上一個快照集後發生在這個工作負載群組，因為記憶體壓力而的次佳計畫層代數目。 不可為 Null。
|**max_memory_grant_kb**| BIGINT |最大記憶體授與的群組，以 kb 為單位。|
|**max_request_cpu_msec**| BIGINT |單一要求的最大 CPU 使用量 (以毫秒為單位)。 不可為 Null。|
|**max_concurrent_request**| ssNoversion |並行要求之最大數目的目前設定。 不可為 Null。|
|**max_io**| ssNoversion |群組的最大 IO 限制。|
|**max_global_io**| ssNoversion |僅供參考之用。 不支援。 我們無法保證未來的相容性。
|**max_queued_io**| ssNoversion |僅供參考之用。 不支援。 我們無法保證未來的相容性。|
|**max_log_rate_kb**| BIGINT |資源群組層級記錄檔最大速率 （kb-每秒的位元組）。|
|**max_session**| ssNoversion |群組的工作階段限制。|
|**max_worker**| ssNoversion |群組的背景工作角色限制。|
|||

## <a name="permissions"></a>Permissions

此檢視需要 VIEW SERVER STATE 權限。

## <a name="remarks"></a>備註

使用者可以存取這個動態管理檢視，以監視近乎即時的使用者工作負載集區，以及 Azure SQL Database 執行個體的系統內部集區的資源耗用量。

> [!IMPORTANT]
> 此 DMV 所呈現的資料大部分供內部使用，而且可能有所變更。

## <a name="examples"></a>範例

下列範例會傳回使用者集區的最大記錄檔資料速率和在每個快照集的耗用量：

```sql
SELECT snapshot_time,
       name,
       max_log_rate_kb,
       delta_log_bytes_used
FROM sys.dm_resource_governor_workload_groups_history_ex
WHERE name LIKE 'User%'
ORDER BY snapshot_time DESC;
```

## <a name="see-also"></a>另請參閱

- [翻譯記錄速率控管](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [彈性集區 DTU 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [彈性集區虛擬核心資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
