---
title: dm_resource_governor_resource_pools_history_ex (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
ms.openlocfilehash: 30c024fb1d1298e0ba2f2e4e49b2acf04d9b7619
ms.sourcegitcommit: 777704aefa7e574f4b7d62ad2a4c1b10ca1731ff
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2020
ms.locfileid: "87823893"
---
# <a name="sysdm_resource_governor_resource_pools_history_ex-transact-sql"></a>dm_resource_governor_resource_pools_history_ex (Transact-sql) 

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

針對 Azure SQL Database 的資源集區統計資料總計) ，傳回過去32分鐘的20秒間隔的快照集 (128 recs。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**pool_id**|int|資源集區的識別碼。 不可為 Null。
|**name**|sysname|資源集區的名稱。 不可為 Null。|
|**snapshot_time**|datetime2|所取得資源集區統計資料快照的日期時間|
|**duration_ms**|int|目前與上一個快照之間的持續時間|
|**statistics_start_time**|datetime2|重設此集區統計資料時的時間。 不可為 Null。|
|**active_session_count**|int|目前快照中的作用中會話總數|
|**active_worker_count**|int|目前快照中的背景工作總計|
|**delta_cpu_usage_ms**|int|自上一個快照以來的 CPU 使用率（以毫秒為單位）。 不可為 Null。|
|**delta_cpu_usage_preemptive_ms**|int|自上一個快照集以來，未受 SQL CPU RG 管理的搶先 win32 呼叫|
|**used_data_space_kb**|BIGINT|與使用者集區相關聯的使用者資料庫中使用的總空間|
|**allocated_disk_space_kb**|BIGINT|與使用者集區相關聯之使用者資料庫的資料檔案大小總計|
|**target_memory_kb**|BIGINT|資源集區嘗試佔用的目標記憶體數量 (以 KB 為單位)。 這是以目前的設定與伺服器狀態為基礎。 不可為 Null。|
|**used_memory_kb**|BIGINT|資源集區所使用的記憶體數量 (以 KB 為單位)。 不可為 Null。|
|**cache_memory_kb**|BIGINT|目前的快取記憶體總使用量 (以 KB 為單位)。 不可為 Null。|
|**compile_memory_kb**|BIGINT|目前奪取的記憶體總使用量 (以 KB 為單位)。 這個使用量大部分用於編譯和最佳化，但是也可以包含其他記憶體使用者。 不可為 Null。|
|**active_memgrant_count**|BIGINT|記憶體授與的目前計數。 不可為 Null。|
|**active_memgrant_kb**|BIGINT|目前記憶體授與的總和 (以 KB 為單位)。 不可為 Null。|
|**used_memgrant_kb**|BIGINT|記憶體授與的目前已使用 (奪取) 記憶體總量。 不可為 Null。|
|**delta_memgrant_timeout_count**|int|這段期間內，此資源集區中的記憶體授與超時計數。 不可為 Null。|
|**delta_memgrant_waiter_count**|int|目前在記憶體授與暫止的查詢計數。 不可為 Null。|
|**delta_out_of_memory_count**|int|集區自上一個快照以來失敗的記憶體配置數目。 不可為 Null。|
|**delta_read_io_queued**|int|自上一個快照集以來，已排入佇列的讀取 Io 總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_read_io_issued**|int|自上一個快照集以來發出的讀取 Io 總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_read_io_completed**|int|自上一個快照集以來完成的讀取 Io 總數。 不可為 Null。|
|**delta_read_io_throttled**|int|快照集後已節流的讀取 Io 總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_read_bytes**|BIGINT|自上一個快照集以來讀取的總位元組數。 不可為 Null。|
|**delta_read_io_stall_ms**|int|讀取 IO 抵達和完成後的總時間 (（以毫秒為單位）) 自上一個快照集。 不可為 Null。|
|**delta_read_io_stall_queued_ms**|int|讀取 IO 抵達和上次快照以來的問題的總時間 (（以毫秒) 為單位）。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。 非零的 delta_read_io_stall_queued_ms 表示 IO 受到 RG 的影響。|
|**delta_write_io_queued**|int|自上一個快照集以來，排入佇列的總 Io。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_write_io_issued**|int|自上一個快照集以來發行的寫入 Io 總數。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_write_io_completed**|int|自上一個快照集以來完成的總寫入 Io。 不可為 Null|
|**delta_write_io_throttled**|int|自上一個快照集以來，已節流的總 Io。 不可為 Null|
|**delta_write_bytes**|BIGINT|自上一個快照集以來寫入的總位元組數。 不可為 Null。|
|**delta_write_io_stall_ms**|int|寫入 IO 抵達和完成後的總時間 (（以毫秒為單位）) 上一個快照集。 不可為 Null。|
|**delta_write_io_stall_queued_ms**|int|寫入 IO 抵達和自上一個快照以來的問題的總時間 (（以毫秒) 為單位）。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**delta_io_issue_delay_ms**|int|排定的問題與自上一個快照集的實際發生 IO 問題之間的總時間 (（以毫秒為單位）) 。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**max_iops_per_volume**|int|此集區的每個磁片區設定的每秒 IO 數上限 (IOPS) 。 可為 Null。 如果資源集區不受 IO 管制，則為 NULL。|
|**max_memory_kb**|BIGINT|資源集區可以擁有的最大記憶體數量 (以 KB 為單位)。 這是以目前的設定與伺服器狀態為基礎。 不可為 Null。
|**max_log_rate_kb**|BIGINT|資源集區層級的最大記錄速率 (每秒 kb 數) 。|
|**max_data_space_kb**|BIGINT|此彈性集區的最大彈性集區儲存體限制設定（以 kb 為單位）。|
|**max_session**|int|集區的會話限制|
|**max_worker**|int|集區的背景工作限制|
|**min_cpu_percent**|int|當發生 CPU 競爭時，資源集區中所有要求之保證平均 CPU 頻寬的目前組態。 不可為 Null。|
|**max_cpu_percent**|int|當 CPU 出現競爭時，資源集區中所有要求允許之最大平均 CPU 頻寬的目前組態。 不可為 Null。|
|**cap_cpu_percent**|int|資源集區中所有要求都將接收的 CPU 頻寬硬體上限。 將最大 CPU 頻寬層級限制為指定的層級。 允許的值範圍從 1 至 100。 不可為 Null。|
|**min_vcores**|decimal (5，2) |當發生 CPU 競爭時，資源集區中所有要求之保證平均 CPU 頻寬的目前組態。  以虛擬核心單位|
|**max_vcores**|decimal (5，2) |當 CPU 出現競爭時，資源集區中所有要求允許之最大平均 CPU 頻寬的目前組態。  在虛擬核心單位中|
|**cap_vcores**|decimal (5，2) |資源集區中所有要求都將接收的 CPU 頻寬硬體上限。  在虛擬核心的單位中|
|**instance_cpu_count**|int|為實例設定的 CPU 數目|
|**instance_cpu_percent**|decimal (5，2) |為實例設定的 CPU 百分比|
|**instance_vcores**|decimal (5，2) |為實例設定的虛擬核心數目|
|**delta_log_bytes_used**|decimal (5，2) |集區層級自上一個快照以來的總記錄產生 (（以位元組為單位）) |
|**avg_login_rate_percent**|decimal (5，2) |自上一個快照集起的登入數目，相較于登入限制|
|**delta_vcores_used**|decimal (5，2) |自上一個快照集以來，計算使用量的虛擬核心計數。|
|**cap_vcores_used_percent**|decimal (5，2) |集區限制的平均計算使用量百分比。|
|**instance_vcores_used_percent**|decimal (5，2) |SQL 實例限制的平均計算使用率（以百分比表示）。|
|**avg_data_io_percent**|decimal (5，2) |集區限制的平均 I/O 使用量百分比。|
|**avg_log_write_percent**|decimal (5，2) |集區限制的平均寫入資源使用量百分比。|
|**avg_storage_percent**|decimal (5，2) |集區儲存體限制的平均儲存體使用量百分比。|
|**avg_allocated_storage_percent**|decimal (5，2) |彈性集區中所有資料庫所配置的資料空間百分比。 這是配置給彈性集區之資料大小上限的資料空間比例。 如需詳細資訊，請參閱： SQL Database 中的檔案空間管理|
|**max_worker_percent**|decimal (5，2) |集區限制的並行背景工作角色 (要求) 百分比。|
|**max_session_percent**|decimal (5，2) |集區限制的並行工作階段百分比。|
|||

## <a name="permissions"></a>權限

此視圖需要 VIEW SERVER STATE 許可權。

## <a name="remarks"></a>備註

使用者可以存取此動態管理檢視，以監視使用者工作負載集區的近乎即時資源耗用量，以及 Azure SQL Database 實例的系統內部集區。

> [!IMPORTANT]
> 此 DMV 所呈現的大部分資料都是供內部使用，而且可能隨時變更。

## <a name="examples"></a>範例

下列範例會依使用者集區傳回每個快照的最大記錄速率資料和耗用量  

```sql
select snapshot_time, name, max_log_rate_kb, delta_log_bytes_used from sys.dm_resource_governor_resource_pools_history_ex where name like 'UserPool%' order by snapshot_time desc
```

下列範例會傳回與 sys 相同的資訊，而不需要連接到邏輯 Master，elastic_pool_resource_stats

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

- [翻譯記錄速率治理](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [彈性集區 DTU 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-elastic-pools)
- [彈性集區 vCore 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools)
