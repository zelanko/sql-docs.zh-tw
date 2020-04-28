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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "73843865"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 SQL Database 伺服器中的所有彈性集區的資源使用量統計資料。 每個彈性集區，每 15 秒報告時間範圍會傳回一列 (每分鐘四列)。 包括集區中所有資料庫的 CPU、IO、記錄、儲存體使用情況和並行的要求/工作階段使用量。 此資料會保留14天。 
  
||  
|-|  
|**適用**于： [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|表示15秒報告間隔開始的 UTC 時間。|  
|**end_time**|**datetime2**|指出15秒報告間隔結束的 UTC 時間。|  
|**elastic_pool_name**|**nvarchar(128)**|彈性資料庫集區的名稱。|  
|**avg_cpu_percent**|**decimal （5，2）**|集區限制的平均計算使用量百分比。|  
|**avg_data_io_percent**|**decimal （5，2）**|集區限制的平均 I/O 使用量百分比。|  
|**avg_log_write_percent**|**decimal （5，2）**|集區限制的平均寫入資源使用量百分比。|  
|**avg_storage_percent**|**decimal （5，2）**|集區儲存體限制的平均儲存體使用量百分比。|  
|**max_worker_percent**|**decimal （5，2）**|集區限制的並行背景工作角色 (要求) 百分比。|  
|**max_session_percent**|**decimal （5，2）**|集區限制的並行工作階段百分比。|  
|**elastic_pool_dtu_limit**|**int**|間隔期間此彈性集區目前最大的彈性集區 DTU 設定。|  
|**elastic_pool_storage_limit_mb**|**bigint**|間隔期間此彈性集區目前最大的彈性集區儲存體限制設定 (MB)。|
|**avg_allocated_storage_percent**|**decimal （5，2）**|彈性集區中所有資料庫所配置的資料空間百分比。  這是配置給彈性集區之資料大小上限的資料空間比例。  如需詳細資訊，請參閱： [SQL DB 中的檔案空間管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>備註

 此視圖存在於 SQL Database 伺服器的 master 資料庫中。 您必須連接到 master 資料庫，才能查詢**sys.databases elastic_pool_resource_stats**。  
  
## <a name="permissions"></a>權限

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

 [透過彈性資料庫進行爆炸性成長](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [建立和管理 SQL Database 彈性資料庫集區（預覽）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
