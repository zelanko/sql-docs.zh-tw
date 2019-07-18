---
title: sys.dm_resource_governor_resource_pools_history_ex (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governor
- sys.resource_governor_TSQL
- resource_governor
- resource_governor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governor catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: 7b40d9afe54137fb31088aa8aa8b5664c90b715d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053301"
---
# <a name="sysdmresourcegovernorresourcepoolshistoryex-transact-sql"></a>sys.dm_resource_governor_resource_pools_history_ex & Amp;#40;transact-SQL&AMP;#41;

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

傳回快照集，以 15 秒間隔過去 30 分鐘的資源集區統計資料，Azure SQL database。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|ssNoversion|資源集區的識別碼。 不可為 Null。
|**name**|sysname|資源集區的名稱。 不可為 Null。|
|**snapshot_time**|datetime2|所建立的資源集區統計資料快照的日期時間|
|**duration_ms**|ssNoversion|目前和先前的快照集之間的持續時間|
|**statistics_start_time**|datetime2|重設此集區統計資料時的時間。 不可為 Null。|
|**active_session_count**|ssNoversion|將作用中的工作階段總數中目前的快照集|
|**active_worker_count**|ssNoversion|在目前的快照集的背景工作角色總數|
|**delta_cpu_usage_ms**|ssNoversion|在上一個快照集以來的毫秒數的 CPU 使用量。 不可為 Null。|
|**delta_cpu_usage_preemptive_ms**|ssNoversion|Preemptive 的 win32 呼叫未管理由 SQL CPU RG，自上一個快照集|
|**used_data_space_kb**|BIGINT|使用者集區相關聯的使用者資料庫中所使用的總空間|
|**allocated_disk_space_kb**|BIGINT|總資料檔案中相關聯的使用者資料庫的大小與使用者集區|
|**target_memory_kb**|BIGINT|資源集區嘗試佔用的目標記憶體數量 (以 KB 為單位)。 這是以目前的設定與伺服器狀態為基礎。 不可為 Null。|
|**used_memory_kb**|BIGINT|資源集區所使用的記憶體數量 (以 KB 為單位)。 不可為 Null。|
|**cache_memory_kb**|BIGINT|目前的快取記憶體總使用量 (以 KB 為單位)。 不可為 Null。|
|**compile_memory_kb**|BIGINT|目前奪取的記憶體總使用量 (以 KB 為單位)。 這個使用量大部分用於編譯和最佳化，但是也可以包含其他記憶體使用者。 不可為 Null。|
|**active_memgrant_count**|BIGINT|記憶體授與的目前計數。 不可為 Null。|
|**active_memgrant_kb**|BIGINT|目前記憶體授與的總和 (以 KB 為單位)。 不可為 Null。|
|**used_memgrant_kb**|BIGINT|記憶體授與的目前已使用 (奪取) 記憶體總量。 不可為 Null。|
|**delta_memgrant_timeout_count**|ssNoversion|計數的記憶體授與此資源集區中的逾時，在這段期間。 不可為 Null。|
|**delta_memgrant_waiter_count**|ssNoversion|目前在記憶體授與暫止的查詢計數。 不可為 Null。|
|**delta_out_of_memory_count**|ssNoversion|最後一個快照集之後，集區中失敗的記憶體配置數目。 不可為 Null。|
|**delta_read_io_queued**|ssNoversion|讀取自上一個快照集總數的 IOs 加入佇列。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_read_io_issued**|ssNoversion|讀取自最後一個快照以來所發出的 Io 總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_read_io_completed**|ssNoversion|讀取自最後一個快照以來已完成的 Io 總數。 不可為 Null。|
|**delta_read_io_throttled**|ssNoversion|讀取已節流處理，因為快照集的 Io 總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_read_bytes**|BIGINT|上一個快照集之後，讀取的位元組總數。 不可為 Null。|
|**delta_read_io_stall_ms**|ssNoversion|總時間 （以毫秒為單位） 讀取的 IO 從抵達到最後一個快照相比的完成。 不可為 Null。|
|**delta_read_io_stall_queued_ms**|ssNoversion|總時間 （以毫秒為單位） 讀取 IO 從抵達到最後一個快照相比的問題。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。 非零 delta_read_io_stall_queued_ms 表示 IO 會受到 RG。|
|**delta_write_io_queued**|ssNoversion|自最後一個快照以來加入佇列的 IOs 寫入總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_write_io_issued**|ssNoversion|最後一個快照集之後所發出的 Io 寫入總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_write_io_completed**|ssNoversion|自最後一個快照以來已完成的 Io 寫入總數。 不可為 Null|
|**delta_write_io_throttled**|ssNoversion|總寫入 Io 節流自上一個快照集。 不可為 Null|
|**delta_write_bytes**|BIGINT|上一個快照集之後寫入的位元組總數。 不可為 Null。|
|**delta_write_io_stall_ms**|ssNoversion|總時間 （以毫秒為單位） 寫入 IO 從抵達到完成，因為上一個快照集。 不可為 Null。|
|**delta_write_io_stall_queued_ms**|ssNoversion|總時間 （以毫秒為單位） 寫入 IO 從抵達到最後一個快照相比的問題。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_io_issue_delay_ms**|ssNoversion|總時間 （以毫秒為單位） 已排程的問題，並提供實際發出 IO 自上一個快照集。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**max_iops_per_volume**|ssNoversion|最大每秒 IO (IOPS 每個磁碟區設定，此集區)。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**max_memory_kb**|BIGINT|資源集區可以擁有的最大記憶體數量 (以 KB 為單位)。 這是以目前的設定與伺服器狀態為基礎。 不可為 Null。
|**max_log_rate_kb**|BIGINT|在資源集區層級記錄檔最大速率 （kb-每秒的位元組）。|
|**max_data_space_kb**|BIGINT|設定此彈性集區，以 kb 為單位的最大的彈性集區儲存體限制。|
|**max_session**|ssNoversion|集區的工作階段限制|
|**max_worker**|ssNoversion|集區的背景工作限制|
|**min_cpu_percent**|ssNoversion|當發生 CPU 競爭時，資源集區中所有要求之保證平均 CPU 頻寬的目前組態。 不可為 Null。|
|**max_cpu_percent**|ssNoversion|當 CPU 出現競爭時，資源集區中所有要求允許之最大平均 CPU 頻寬的目前組態。 不可為 Null。|
|**cap_cpu_percent**|ssNoversion|資源集區中所有要求都將接收的 CPU 頻寬硬體上限。 將最大 CPU 頻寬層級限制為指定的層級。 允許的值範圍從 1 至 100。 不可為 Null。|
|**min_vcores**|decimal(5,2)|當發生 CPU 競爭時，資源集區中所有要求之保證平均 CPU 頻寬的目前組態。  以 Vcore 為單位|
|**max_vcores**|decimal(5,2)|當 CPU 出現競爭時，資源集區中所有要求允許之最大平均 CPU 頻寬的目前組態。  單位中的虛擬核心|
|**cap_vcores**|decimal(5,2)|資源集區中所有要求都將接收的 CPU 頻寬硬體上限。  在上個 Vcore 的單位|
|**instance_cpu_count**|ssNoversion|設定執行個體的 CPU 數目|
|**instance_cpu_percent|decimal(5,2)|設定執行個體的 CPU 百分比|
|**instance_vcores**|decimal(5,2)|為執行個體設定的虛擬核心數目|
|**delta_log_bytes_used**|decimal(5,2)|記錄總計 （以位元組為單位） 層級產生集區自上一個快照集|
|**avg_login_rate_percent**|decimal(5,2)|登入限制進行比較的最後一個快照相比的登入次數|
|**delta_vcores_used**|decimal(5,2)|計算自上一個快照集的使用量中的虛擬核心計數。|
|**cap_vcores_used_percent**|decimal(5,2)|平均計算使用量限制的集區的百分比。|
|**instance_vcores_used_percent**|decimal(5,2)|平均計算使用量限制的 SQL 執行個體的百分比。|
|**avg_data_io_percent**|decimal(5,2)|平均 I/O 使用量百分比限制的集區。|
|**avg_log_write_percent**|decimal(5,2)|平均寫入資源使用量的集區的限制百分比表示。|
|**avg_storage_percent**|decimal(5,2)|平均儲存體使用量的集區的儲存體限制的百分比。|
|**avg_allocated_storage_percent**|decimal(5,2)|彈性集區中的所有資料庫所配置的資料空間的百分比。 這是配置給資料的彈性集區的最大大小的資料空間的比例。 如需詳細資訊，請參閱：SQL DB 中的檔案空間管理|
|**max_worker_percent**|decimal(5,2)|最大並行背景工作角色 （要求） 限制的集區的百分比。|
|**max_session_percent**|decimal(5,2)|最大並行工作階段百分比限制的集區。|
|||

## <a name="permissions"></a>Permissions

此檢視需要 VIEW SERVER STATE 權限。

## <a name="remarks"></a>備註

使用者可以存取這個動態管理檢視，以監視近乎即時的使用者工作負載集區，以及 Azure SQL Database 執行個體的系統內部集區的資源耗用量。

> [!IMPORTANT]
> 此 DMV 所呈現的資料大部分供內部使用，而且可能有所變更。

## <a name="examples"></a>範例

下列範例會傳回最大記錄檔資料速率和耗用量在每個快照集的使用者集區  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

下列範例傳回 sys.elastic_pool_resource_stats 為類似的資訊，而不需要連線到邏輯 Master

```sql
select snapshot_time, name, cap_vcores_used_percent,
  avg_data_io_percent,  
  avg_log_write_percent,
  avg_storage_percent,
  avg_allocated_storage_percent,
  max_data_space_kb,
  max_worker_percent,
  max_session_percent
    from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

## <a name="see-also"></a>另請參閱

- [翻譯記錄速率控管](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [彈性集區 DTU 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [彈性集區虛擬核心資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
