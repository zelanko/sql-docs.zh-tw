---
title: sys.dm_user_db_resource_governance (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
manager: craigg
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: bb4c43fa4193d9254d7f06f24bd903f974739e87
ms.sourcegitcommit: a9a03f9a7ec4dad507d2dfd5ca33571580114826
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/28/2019
ms.locfileid: "58567634"
---
# <a name="sysdmuserdbresourcegovernance-transact-sql"></a>sys.dm_user_db_resource_governance (Transact-SQL)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

傳回資源控管 Azure SQL Database 資料庫的組態和容量設定。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|ssNoversion|資料庫中的 Azure SQL Database 伺服器的唯一識別碼。|
|**logical_database_guid**|UNIQUEIDENTIFIER|使用者資料庫和透過生命週期的使用者資料庫會保持邏輯的 guid。  重新命名或將資料庫設為不同的 SLO 不會變更的 GUID。 |
|**physical_database_guid**|UNIQUEIDENTIFIER|實體的使用者資料庫會持續透過使用者資料庫的實體執行個體的生命週期的 guid。 不同的 SLO 的設定會導致變更這個資料行。|
|**server_name**|NVARCHAR|邏輯伺服器名稱。|
|**database_name**|NVARCHAR|邏輯資料庫名稱。|
|**slo_name**|NVARCHAR|服務等級目標和硬體產生。|
|**dtu_limit**|ssNoversion|資料庫 (如虛擬核心為 NULL) 的 DTU 限制。|
|**cpu_limit**|ssNoversion|資料庫 (NULL DTU 資料庫) 的虛擬核心限制。|
|**min_cpu**|TINYINT|使用者的工作負載可以使用最小 CPU 百分比。|
|**max_cpu**|TINYINT|可供使用者的工作負載的最大 CPU 百分比。|
|**cap_cpu**|TINYINT|使用者工作負載群組的 CPU 百分比上限。|
|**min_cores**|SMALLINT|使用 SQL 的 Cpu 數目。|
|**max_dop**|SMALLINT|使用者的工作負載所使用的平行處理原則的最大程度。|
|**min_memory**|ssNoversion|可供使用者的工作負載的最小記憶體百分比。|
|**max_memory**|ssNoversion|可供使用者的工作負載的最大記憶體百分比。|
|**max_sessions**|ssNoversion|使用者群組的工作階段限制。|
|**max_memory_grant**|ssNoversion|最大記憶體授與每個查詢中使用者的工作負載中，以百分比表示。|
|**max_db_memory**|ssNoversion|使用者的 DB 工作負載的最大緩衝區集區記憶體上限|
|**govern_background_io**|bit|指出是否已將背景寫入而向經銷商計費使用者群組。|
|**min_db_max_size_in_mb**|BIGINT|最小值最大的資料庫檔案大小，以 mb 為單位。|
|**max_db_max_size_in_mb**|BIGINT|最大值最大資料庫檔案，以 mb 為單位。|
|**default_db_max_size_in_mb**|BIGINT|預設資料庫檔案大小上限，以 mb 為單位。|
|**db_file_growth_in_mb**|BIGINT|Azure 的資料庫檔案，以 mb 為單位的預設成長。|
|**initial_db_file_size_in_mb**|BIGINT|預設資料庫檔案大小，以 mb 為單位。|
|**log_size_in_mb**|BIGINT|預設記錄檔大小，以 mb 為單位。|
|**instance_cap_cpu**|ssNoversion|執行個體層級的 CPU 上限。|
|**instance_max_log_rate**|BIGINT|記錄產生執行個體層級，以位元組為單位，每秒的速率上限。|
|**instance_max_worker_threads**|ssNoversion|背景工作執行緒執行個體層級的限制。|
|**replica_type**|ssNoversion|次要複本的類型，其中 0 是主要和 1。|
|**max_transaction_size**|BIGINT|使用的任何交易，以 kb 為單位的最大記錄空間。|
|**checkpoint_rate_mbps**|ssNoversion|檢查點頻寬，以 mbps 為單位。|
|**checkpoint_rate_io**|ssNoversion|檢查點 IO 在 IOs 中每秒速率。|
|**last_updated_date_utc**|DATETIME|日期和時間的最後一個設定變更或重新設定。|
|**primary_group_id**|ssNoversion|主要使用者的工作負載群組識別碼。|
|**primary_group_max_workers**|ssNoversion|在主要使用者的工作負載群組層級的背景工作角色限制。|
|**primary_min_log_rate**|BIGINT|在主要使用者的工作負載群組層級最低記錄速率 （每秒位元組為單位）。|
|**primary_max_log_rate**|BIGINT|在主要使用者的工作負載群組層級記錄檔最大速率 （每秒位元組為單位）。|
|**primary_group_min_io**|ssNoversion|在主要使用者的工作負載群組層級的 IO 下限。|
|**primary_group_max_io**|ssNoversion|在主要使用者的工作負載群組層級的最大 IO。|
|**primary_group_min_cpu**|FLOAT|最小 CPU 百分比限制在主要使用者的工作負載群組層級。|
|**primary_group_max_cpu**|FLOAT|最大 CPU 百分比限制在主要使用者的工作負載群組層級。|
|**primary_log_commit_fee**|ssNoversion|記錄速率控管認可費用在主要使用者的工作負載群組層級。|
|**primary_pool_max_workers**|ssNoversion|在主要的使用者集區層級的背景工作角色限制。
|**pool_max_io**|ssNoversion|在主要的使用者集區層級的最大 IO 限制。|
|**govern_db_memory_in_resource_pool**|bit|指出是否緩衝集區的大小上限受到資源集區層級。 通常為彈性集區內的資料庫。|
|**volume_local_iops**|ssNoversion|每個本機磁碟區 （例如 c:、 d:） 的第二個端點的 IOs。|
|**volume_managed_xstore_iops**|ssNoversion|每個遠端儲存體帳戶的第二個端點的 IOs。|
|**volume_external_xstore_iops**|ssNoversion|每個 Azure SQL DB 備份和遙測所使用的遠端儲存體帳戶的第二個端點的 IOs。|
|**volume_type_local_iops**|ssNoversion|為所有的本機磁碟區的第二個端點每 IOs。|
|**volume_type_managed_xstore_iops**|ssNoversion|每個執行個體所使用的所有遠端儲存體帳戶的第二個端點的 IOs。|
|**volume_type_external_xstore_iops**|ssNoversion|使用 Azure SQL DB 備份和遙測執行個體的所有遠端儲存體帳戶的第二個端點每 IOs。|
|**volume_pfs_iops**|ssNoversion|每個進階檔案儲存體的第二個端點的 IOs。|
|**volume_type_pfs_iops**|ssNoversion|每個執行個體所使用的所有進階檔案儲存體的第二個端點的 IOs。|
|||

## <a name="permissions"></a>Permissions

此檢視需要 VIEW DATABASE STATE 權限。

## <a name="remarks"></a>備註

使用者可以存取的資源控管設定這個動態管理檢視和 Azure SQL Database 資料庫的容量設定。 

> [!IMPORTANT]
> 此 DMV 所呈現的資料大部分供內部使用，而且可能有所變更。

## <a name="examples"></a>範例

下列範例會傳回執行個體最大記錄檔資料速率依資料庫伺服器內的單一或集區資料庫的資料庫名稱。

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>另請參閱

- [交易記錄檔的速率控管](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [單一資料庫 DTU 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [單一資料庫 vCore 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
