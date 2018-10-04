---
title: sys.elastic_pool_resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 210e051088539920ad9c26e8036c7d9a911a2e4c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653126"
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回邏輯伺服器中的所有彈性資料庫集區的資源使用量統計資料。 針對每個彈性資料庫集區中，有一個資料列的每 15 秒報告視窗 （每分鐘四個資料列）。 這包括 CPU、 IO、 記錄、 儲存體耗用量和並行的要求/工作階段使用量的集區中的所有資料庫。 這項資料會保留 14 天。 
  
||  
|-|  
|**適用於**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|表示 15 秒的報告間隔開始的 UTC 時間。|  
|**end_time**|**datetime2**|指出報告間隔 15 秒結束的 UTC 時間。|  
|**elastic_pool_name**|**nvarchar(128)**|彈性資料庫集區名稱。|  
|**avg_cpu_percent**|**decimal(5,2)**|平均計算使用量限制的集區的百分比。|  
|**avg_data_io_percent**|**decimal(5,2)**|平均 I/O 使用量百分比限制的集區。|  
|**avg_log_write_percent**|**decimal(5,2)**|平均寫入資源使用量的集區的限制百分比表示。|  
|**avg_storage_percent**|**decimal(5,2)**|平均儲存體使用量的集區的儲存體限制的百分比。|  
|**max_worker_percent**|**decimal(5,2)**|最大並行背景工作角色 （要求） 限制的集區的百分比。|  
|**max_session_percent**|**decimal(5,2)**|最大並行工作階段百分比限制的集區。|  
|**elastic_pool_dtu_limit**|**int**|目前最大的彈性集區 DTU 設定此彈性集區在此間隔期間。|  
|**elastic_pool_storage_limit_mb**|**bigint**|在此間隔期間此彈性集區，以 mb 為單位設定目前最大的彈性集區儲存體限制。|
|**avg_allocated_storage_percent**|**decimal(5,2)**|彈性集區中的所有資料庫所配置的資料空間的百分比。  這是配置給資料的彈性集區的最大大小的資料空間的比例。  如需詳細資訊，請參閱： [SQL DB 中的檔案空間管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>備註  
 此檢視位於邏輯伺服器的 master 資料庫。 您必須連接到 master 資料庫來查詢**sys.elastic_pool_resource_stats**。  
  
## <a name="permissions"></a>Permissions  
 需要的成員資格**dbmanager**角色。  
  
## <a name="examples"></a>範例  
 下列範例會傳回依據目前的邏輯伺服器中的所有彈性資料庫集區的最新時間排序的資源使用量資料。  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 下列範例會計算指定的集區的平均 DTU 百分比耗用量。  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>另請參閱  
 [使用彈性資料庫抑止爆炸性的成長](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [建立和管理 SQL Database 彈性資料庫集區 （預覽）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
