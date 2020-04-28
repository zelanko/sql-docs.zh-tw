---
title: sys.databases dm_user_db_resource_governance （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.resource_governance
- sys.resource_governance_TSQL
- resource_governance
- resource_governance_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_governance catalog view
ms.assetid: ''
author: joesackmsft
ms.author: josack
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: aa7c7e7a7c510f797377c3cbbceb7c2751418da3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "74165916"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.databases dm_user_db_resource_governance （Transact-sql）

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

傳回目前資料庫或彈性集區中資源管理機制所使用的實際設定和容量設定。
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|int|資料庫的識別碼，在 Azure SQL Database 伺服器內是唯一的。|
|**logical_database_guid**|UNIQUEIDENTIFIER|使用者資料庫的邏輯 GUID，會在使用者資料庫的存留期間持續。  重新命名資料庫或變更其服務等級目標不會變更此值。|
|**physical_database_guid**|UNIQUEIDENTIFIER|使用者資料庫的實體 GUID，它會持續在使用者資料庫的實體實例存留期間。 變更資料庫服務等級目標會導致此值變更。|
|**server_name**|NVARCHAR|邏輯伺服器名稱。|
|**database_name**|NVARCHAR|邏輯資料庫名稱。|
|**slo_name**|NVARCHAR|服務等級目標，包括硬體世代。|
|**dtu_limit**|int|資料庫的 DTU 限制（vCore 為 Null）。|
|**cpu_limit**|int|資料庫的 vCore 限制（DTU 資料庫為 Null）。|
|**min_cpu**|TINYINT|使用者工作負載資源集區的 MIN_CPU_PERCENT 值。 請參閱[資源集區概念](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)。|
|**max_cpu**|TINYINT|使用者工作負載資源集區的 MAX_CPU_PERCENT 值。 請參閱[資源集區概念](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)。|
|**cap_cpu**|TINYINT|使用者工作負載資源集區的 CAP_CPU_PERCENT 值。 請參閱[資源集區概念](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)。|
|**min_cores**|SMALLINT|僅供內部使用。|
|**max_dop**|SMALLINT|使用者工作負載群組的 MAX_DOP 值。 請參閱[建立工作負載群組](https://docs.microsoft.com/sql/t-sql/statements/create-workload-group-transact-sql)。|
|**min_memory**|int|使用者工作負載資源集區的 MIN_MEMORY_PERCENT 值。 請參閱[資源集區概念](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)。|
|**max_memory**|int|使用者工作負載資源集區的 MAX_MEMORY_PERCENT 值。 請參閱[資源集區概念](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor-resource-pool?#resource-pool-concepts)。|
|**max_sessions**|int|使用者工作負載群組中允許的會話數目上限。|
|**max_memory_grant**|int|使用者工作負載群組的 REQUEST_MAX_MEMORY_GRANT_PERCENT 值。 請參閱[建立工作負載群組](https://docs.microsoft.com/sql/t-sql/statements/create-workload-group-transact-sql)。|
|**max_db_memory**|int|僅供內部使用。|
|**govern_background_io**|bit|僅供內部使用。|
|**min_db_max_size_in_mb**|BIGINT|資料檔案的最小 max_size 值（以 MB 為單位）。 請參閱[sys.databases database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。|
|**max_db_max_size_in_mb**|BIGINT|資料檔案的最大 max_size 值（以 MB 為單位）。 請參閱[sys.databases database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。|
|**default_db_max_size_in_mb**|BIGINT|資料檔案的預設 max_size 值（以 MB 為單位）。 請參閱[sys.databases database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。|
|**db_file_growth_in_mb**|BIGINT|資料檔案的預設成長增量（以 MB 為單位）。 請參閱[sys.databases database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。|
|**initial_db_file_size_in_mb**|BIGINT|新資料檔案的預設大小（以 MB 為單位）。 請參閱[sys.databases database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。|
|**log_size_in_mb**|BIGINT|新記錄檔的預設大小（以 MB 為單位）。 請參閱[sys.databases database_files](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。|
|**instance_cap_cpu**|int|僅供內部使用。|
|**instance_max_log_rate**|BIGINT|SQL Server 實例的記錄產生速率限制（以每秒位元組數為單位）。 適用于實例所產生的所有記錄檔， `tempdb`包括和其他系統資料庫。 在彈性集區中，會套用至集區中所有資料庫所產生的記錄檔。|
|**instance_max_worker_threads**|int|SQL Server 實例的背景工作執行緒限制。|
|**replica_type**|int|複本類型，其中0是主要，1是次要。|
|**max_transaction_size**|BIGINT|任何交易所使用的記錄空間上限（以 KB 為單位）。|
|**checkpoint_rate_mbps**|int|僅供內部使用。|
|**checkpoint_rate_io**|int|僅供內部使用。|
|**last_updated_date_utc**|Datetime|上次變更或重新設定的日期和時間（UTC）。|
|**primary_group_id**|int|主要複本和次要複本上的使用者工作負載的工作負載群組識別碼。|
|**primary_group_max_workers**|int|使用者工作負載群組的背景工作執行緒限制。|
|**primary_min_log_rate**|BIGINT|使用者工作負載群組層級的最低記錄速率（以每秒位元組為單位）。 資源管理不會嘗試減少低於此值的記錄速率。|
|**primary_max_log_rate**|BIGINT|使用者工作負載群組層級的最大記錄速率（以每秒位元組為單位）。 資源管理不允許高於此值的記錄速率。|
|**primary_group_min_io**|int|使用者工作負載群組的最小 IOPS。 資源管理不會嘗試減少低於此值的 IOPS。|
|**primary_group_max_io**|int|使用者工作負載群組的最大 IOPS。 資源管理將不允許高於此值的 IOPS。|
|**primary_group_min_cpu**|FLOAT|使用者工作負載群組層級的最小 CPU 百分比。 資源管理不會嘗試減少低於此值的 CPU 使用率。|
|**primary_group_max_cpu**|FLOAT|使用者工作負載群組層級的最大 CPU 百分比。 資源管理不允許高於此值的 CPU 使用率。|
|**primary_log_commit_fee**|int|使用者工作負載群組的記錄速率治理認可費用（以位元組為單位）。 認可費用會根據固定值，將每個記錄 IO 的大小增加為僅限記錄檔速率帳戶處理的目的。 實際的記錄 IO 到儲存體不會增加。|
|**primary_pool_max_workers**|int|使用者工作負載資源集區的背景工作執行緒限制。|
|**pool_max_io**|int|使用者工作負載資源集區的最大 IOPS 限制。|
|**govern_db_memory_in_resource_pool**|bit|僅供內部使用。|
|**volume_local_iops**|int|僅供內部使用。|
|**volume_managed_xstore_iops**|int|僅供內部使用。|
|**volume_external_xstore_iops**|int|僅供內部使用。|
|**volume_type_local_iops**|int|僅供內部使用。|
|**volume_type_managed_xstore_iops**|int|僅供內部使用。|
|**volume_type_external_xstore_iops**|int|僅供內部使用。|
|**volume_pfs_iops**|int|僅供內部使用。|
|**volume_type_pfs_iops**|int|僅供內部使用。|
|||

## <a name="permissions"></a>權限

此檢視需要 VIEW DATABASE STATE 權限。

## <a name="remarks"></a>備註

如需 Azure SQL Database 中資源管理的說明，請參閱[SQL Database 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server)。

> [!IMPORTANT]
> 這個 DMV 所傳回的大部分資料都是供內部使用，而且隨時可能變更。

## <a name="examples"></a>範例

下列查詢（在使用者資料庫的內容中執行）會傳回使用者工作負載群組和資源集區層級的最大記錄速率和最大 IOPS。 若為單一資料庫，則會傳回一個資料列。 對於彈性集區中的資料庫，會針對集區中的每個資料庫傳回一個資料列。

```
SELECT database_name,
       primary_group_id,
       primary_max_log_rate,
       primary_group_max_io,
       pool_max_io
FROM sys.dm_user_db_resource_governance
ORDER BY database_name;  
```

## <a name="see-also"></a>另請參閱

- [資源管理員](https://docs.microsoft.com/sql/relational-databases/resource-governor/resource-governor)
- [sys.dm_resource_governor_resource_pools (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-transact-sql)
- [sys.dm_resource_governor_workload_groups (Transact-SQL)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql)
- [sys.databases dm_resource_governor_resource_pools_history_ex （Transact-sql）](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-resource-pools-history-ex-azure-sql-database)
- [sys.dm_resource_governor_workload_groups_history_ex (Azure SQL Database)](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-history-ex-azure-sql-database)
- [交易記錄速率治理](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [單一資料庫 DTU 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [單一資料庫 vCore 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
