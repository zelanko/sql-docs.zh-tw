---
title: _user_db_resource_governance (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
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
ms.openlocfilehash: ea07ba28efc4ac50fdeef04bb1b3643c359ead28
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/30/2019
ms.locfileid: "70176252"
---
# <a name="sysdm_user_db_resource_governance-transact-sql"></a>sys.databases _user_db_resource_governance (Transact-sql)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

傳回 Azure SQL Database 資料庫的資源管理設定和容量設定。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**database_id**|ssNoversion|資料庫的識別碼, 在 Azure SQL Database 伺服器內是唯一的。|
|**logical_database_guid**|UNIQUEIDENTIFIER|使用者資料庫的邏輯 guid, 並持續在使用者資料庫的存留期間內。  將資料庫重新命名或設定為不同的 SLO 不會變更 GUID。 |
|**physical_database_guid**|UNIQUEIDENTIFIER|使用者資料庫的實體 guid, 它會持續在使用者資料庫的實體實例存留期間。 將設定為不同的 SLO 會使此資料行變更。|
|**server_name**|NVARCHAR|邏輯伺服器名稱。|
|**database_name**|NVARCHAR|邏輯資料庫名稱。|
|**slo_name**|NVARCHAR|服務等級目標和硬體世代。|
|**dtu_limit**|ssNoversion|資料庫的 DTU 限制 (vCore 為 Null)。|
|**cpu_limit**|ssNoversion|資料庫的 vCore 限制 (DTU 資料庫為 Null)。|
|**min_cpu**|TINYINT|使用者工作負載可使用的最小 CPU 百分比。|
|**max_cpu**|TINYINT|使用者工作負載可使用的最大 CPU 百分比。|
|**cap_cpu**|TINYINT|使用者工作負載群組的 CPU 百分比上限。|
|**min_cores**|SMALLINT|SQL 所使用的 Cpu 數目。|
|**max_dop**|SMALLINT|使用者工作負載所使用的平行處理原則最大程度。|
|**min_memory**|ssNoversion|使用者工作負載可使用的最小記憶體百分比。|
|**max_memory**|ssNoversion|使用者工作負載可使用的最大記憶體百分比。|
|**max_sessions**|ssNoversion|使用者群組的會話限制。|
|**max_memory_grant**|ssNoversion|使用者工作負載中每個查詢的最大記憶體授與 (以百分比為單位)。|
|**max_db_memory**|ssNoversion|使用者資料庫工作負載的最大緩衝集區記憶體上限|
|**govern_background_io**|bit|指出是否要對使用者群組收取背景寫入費用。|
|**min_db_max_size_in_mb**|Bigint|最小資料庫檔案大小 (以 MB 為單位)。|
|**max_db_max_size_in_mb**|Bigint|最大資料庫檔案數 (以 MB 為單位)。|
|**default_db_max_size_in_mb**|Bigint|預設的資料庫檔案大小上限 (以 MB 為單位)。|
|**db_file_growth_in_mb**|Bigint|Azure 資料庫檔案的預設成長 (以 MB 為單位)。|
|**initial_db_file_size_in_mb**|Bigint|預設的資料庫檔案大小 (以 MB 為單位)。|
|**log_size_in_mb**|Bigint|預設記錄檔大小 (以 MB 為單位)。|
|**instance_cap_cpu**|ssNoversion|實例層級的 CPU 限定。|
|**instance_max_log_rate**|Bigint|實例層級的記錄產生速率上限 (以每秒位元組數為單位)。|
|**instance_max_worker_threads**|ssNoversion|實例層級的背景工作執行緒限制。|
|**replica_type**|ssNoversion|複本類型, 其中0是主要, 1 是次要。|
|**max_transaction_size**|Bigint|任何交易所使用的記錄空間上限 (以 KB 為單位)。|
|**checkpoint_rate_mbps**|ssNoversion|檢查點頻寬 (以 Mbps 為單位)。|
|**checkpoint_rate_io**|ssNoversion|每秒 io 的檢查點 IO 速率。|
|**last_updated_date_utc**|datetime|上次變更或重新設定的日期和時間。|
|**primary_group_id**|ssNoversion|主要使用者工作負載群組識別碼。|
|**primary_group_max_workers**|ssNoversion|主要使用者工作負載群組層級的背景工作限制。|
|**primary_min_log_rate**|Bigint|主要使用者工作負載群組層級的最小記錄速率 (每秒位元組數)。|
|**primary_max_log_rate**|Bigint|主要使用者工作負載群組層級的最大記錄速率 (每秒位元組數)。|
|**primary_group_min_io**|ssNoversion|主要使用者工作負載群組層級的 IO 下限。|
|**primary_group_max_io**|ssNoversion|主要使用者工作負載群組層級的 IO 上限。|
|**primary_group_min_cpu**|float|主要使用者工作負載群組層級的最小 CPU 百分比限制。|
|**primary_group_max_cpu**|float|主要使用者工作負載群組層級的最大 CPU 百分比限制。|
|**primary_log_commit_fee**|ssNoversion|主要使用者工作負載群組層級的記錄速率治理認可費用。|
|**primary_pool_max_workers**|ssNoversion|主要使用者集區層級的背景工作限制。
|**pool_max_io**|ssNoversion|主要使用者集區層級的最大 IO 限制。|
|**govern_db_memory_in_resource_pool**|bit|指出緩衝集區的大小上限是否受資源集區層級控制。 通常會針對彈性集區中的資料庫設定。|
|**volume_local_iops**|ssNoversion|本機磁片區的每秒 Io 上限 (例如 C:、D:)。|
|**volume_managed_xstore_iops**|ssNoversion|遠端儲存體帳戶的每秒 Io 數上限。|
|**volume_external_xstore_iops**|ssNoversion|Azure SQL DB 備份和遙測所使用之遠端儲存體帳戶的每秒 Io 數上限。|
|**volume_type_local_iops**|ssNoversion|所有本機磁片區的每秒 Io 上限。|
|**volume_type_managed_xstore_iops**|ssNoversion|實例所使用之所有遠端儲存體帳戶的每秒 Io 數上限。|
|**volume_type_external_xstore_iops**|ssNoversion|Azure SQL DB 備份和實例的遙測所使用的所有遠端儲存體帳戶的每秒 Io 上限。|
|**volume_pfs_iops**|ssNoversion|Premium 檔案儲存體的 Io 每秒上限。|
|**volume_type_pfs_iops**|ssNoversion|實例所使用之所有 premium 檔案儲存體的每秒 Io 上限。|
|||

## <a name="permissions"></a>Permissions

此檢視需要 VIEW DATABASE STATE 權限。

## <a name="remarks"></a>備註

使用者可以存取此動態管理檢視, 以進行資源管理設定和 Azure SQL Database 資料庫的容量設定。 

> [!IMPORTANT]
> 此 DMV 所呈現的大部分資料都是供內部使用, 而且可能隨時變更。

## <a name="examples"></a>範例

下列範例會針對單一或集區資料庫, 傳回資料庫伺服器內資料庫名稱所排序的實例最大記錄速率資料。

```
SELECT database_name,
       primary_max_log_rate
FROM sys.dm_user_db_resource_governance
ORDER BY database_name DESC;  
```

## <a name="see-also"></a>另請參閱

- [交易記錄速率治理](https://docs.microsoft.com/azure/sql-database/sql-database-resource-limits-database-server#transaction-log-rate-governance)
- [單一資料庫 DTU 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-dtu-resource-limits-single-databases)
- [單一資料庫 vCore 資源限制](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-single-databases)
