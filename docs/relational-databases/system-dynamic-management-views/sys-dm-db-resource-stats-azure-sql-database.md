---
title: sys.dm_db_resource_stats (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: a91988c36604ce38c7022e6bc111cc1941e43a03
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回的 CPU、 I/O 和記憶體耗用量[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]資料庫。 每 15 秒有一個資料列存在，即使資料庫中沒有任何活動亦然。 歷程記錄資料會保留一個小時。  
  
|資料行|資料類型|Description|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|UTC 時間會指出目前報告間隔的結束。|  
|avg_cpu_percent|**decimal (5,2)**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**decimal (5,2)**|平均資料 I/O 使用量佔服務層限制的百分比。|  
|avg_log_write_percent|**decimal (5,2)**|平均寫入資源使用率，以服務層限制的百分比計算。|  
|avg_memory_usage_percent|**decimal (5,2)**|平均記憶體使用率，以服務層限制的百分比計算。<br /><br /> 這包括用來儲存記憶體中 OLTP 物件的記憶體。|  
|xtp_storage_percent|**decimal (5,2)**|儲存體使用量記憶體內部 OLTP 的服務層限制的百分比表示 （結尾的報告的時間間隔）。 這包括用來儲存下列記憶體中 OLTP 物件的記憶體： 記憶體最佳化資料表、 索引和資料表變數。 它也包含用於處理的 ALTER TABLE 作業的記憶體。<br /><br /> 如果未使用記憶體內部 OLTP 資料庫中，則傳回 0。|  
|max_worker_percent|**decimal (5,2)**|最大並行工作者 （要求），以資料庫的服務層限制的百分比表示。|  
|max_session_percent|**decimal (5,2)**|最大並行工作階段的資料庫服務層限制的百分比。|  
|dtu_limit|**int**|目前最大資料庫 DTU 此資料庫設定此間隔。 |
|||
  
> [!TIP]  
>  詳細說明這些限制，以及服務層的內容，請參閱主題[服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[服務層的功能以及限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)。  
  
## <a name="permissions"></a>Permissions  
 此檢視需要 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 所傳回的資料**sys.dm_db_resource_stats**的最大允許您正在執行的服務層/效能層級的限制百分比表示。
 
 如果資料庫在過去的 60 分鐘內已容錯移轉到另一部伺服器，檢視將只會傳回該資料庫在容錯移轉之後做為主要資料庫時的資料。  
  
 這項資料較不精細的檢視，使用**sys.resource_stats**目錄檢視中的**主要**資料庫。 此檢視會每隔 5 秒擷取一次資料，並會保留 14 天內的歷程記錄資料。  如需詳細資訊，請參閱[sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)。  
  
 彈性集區的成員資料庫時，資源統計資料呈現為百分比的值會表示為資料庫在彈性集區設定中所設定的最大限制的百分比。  
  
## <a name="example"></a>範例  
  
下列範例會傳回資源使用率資料，並依據目前連接之資料庫的最新時間排序。  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 下列範例會識別平均 DTU 耗用量，其形式為過去一小時內使用者資料庫的效能層級所允許的最大 DTU 限制百分比。 如果這些百分比持續接近 100%，請考慮增加效能層級。  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 下列範例會傳回 CPU 百分比、資料和記錄檔 I/O 以及記憶體耗用量在過去一個小時內的平均值和最大值。  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服務層的功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
