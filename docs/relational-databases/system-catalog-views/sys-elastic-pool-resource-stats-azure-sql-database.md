---
title: sys.elastic_pool_resource_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0712785a5af3e8cc3c606a597ba02e0075c88dd9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843865"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys. elastic_pool_resource_stats （Azure SQL Database）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 SQL Database 伺服器中所有彈性集區的資源使用量統計資料。 針對每個彈性集區，每15秒報告時間範圍都會有一個資料列（每分鐘四個數據列）。 其中包括 CPU、IO、記錄、儲存體耗用量，以及集區中所有資料庫的並行要求/會話使用率。 此資料會保留14天。 
  
||  
|-|  
|**適用**于： [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。|  
  
|資料行名稱|[名稱]|描述|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|表示15秒報告間隔開始的 UTC 時間。|  
|**end_time**|**datetime2**|指出15秒報告間隔結束的 UTC 時間。|  
|**elastic_pool_name**|**nvarchar(128)**|彈性資料庫集區的名稱。|  
|**avg_cpu_percent**|**decimal （5，2）**|集區限制的平均計算使用率（以百分比表示）。|  
|**avg_data_io_percent**|**decimal （5，2）**|根據集區限制的平均 i/o 使用率（以百分比表示）。|  
|**avg_log_write_percent**|**decimal （5，2）**|平均寫入資源使用率（以集區限制的百分比表示）。|  
|**avg_storage_percent**|**decimal （5，2）**|集區儲存體限制的平均儲存體使用率（以百分比表示）。|  
|**max_worker_percent**|**decimal （5，2）**|以集區限制為依據的最大並行背景工作（要求）百分比。|  
|**max_session_percent**|**decimal （5，2）**|以集區限制為基礎的並行會話數目上限（以百分比表示）。|  
|**elastic_pool_dtu_limit**|**int**|此時間間隔期間，此彈性集區目前的最大彈性集區 DTU 設定。|  
|**elastic_pool_storage_limit_mb**|**bigint**|在此間隔期間，此彈性集區的目前最大彈性集區儲存體限制設定（以 mb 為單位）。|
|**avg_allocated_storage_percent**|**decimal （5，2）**|彈性集區中所有資料庫所配置的資料空間百分比。  這是配置給彈性集區之資料大小上限的資料空間比例。  如需詳細資訊，請參閱： [SQL DB 中的檔案空間管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Remarks

 此視圖存在於 SQL Database 伺服器的 master 資料庫中。 您必須連接到 master 資料庫，才能查詢**sys.databases elastic_pool_resource_stats**。  
  
## <a name="permissions"></a>Permissions

 需要**dbmanager**角色中的成員資格。  
  
## <a name="examples"></a>範例

 下列範例會針對目前 SQL Database 伺服器中的所有彈性資料庫集區，傳回最近一次所排序的資源使用量資料。  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 下列範例會計算給定集區的平均 DTU 百分比耗用量。  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>另請參閱

 [利用彈性資料庫來應對爆炸性成長](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [建立和管理 SQL Database 彈性資料庫集區（預覽）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [resource_stats &#40;Azure SQL Database&#41; ](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
