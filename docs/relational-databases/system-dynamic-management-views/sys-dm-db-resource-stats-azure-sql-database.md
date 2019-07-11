---
title: sys.dm_db_resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 05/21/2019
ms.service: sql-database
ms.reviewer: ''
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
author: julieMSFT
ms.author: jrasnick
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 22d771f57e5ac0d9035b8c283eb6da69027eadb3
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716683"
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 資料庫的 CPU、I/O 和記憶體耗用量。 每 15 秒有一個資料列存在，即使資料庫中沒有任何活動亦然。 歷程記錄資料會保留一個小時。  
  
|[資料行]|資料類型|描述|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|UTC 時間會指出目前報告間隔的結束。|  
|avg_cpu_percent|**decimal (5,2)**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**decimal (5,2)**|平均資料 I/O 使用率的服務層限制的百分比表示。|  
|avg_log_write_percent|**decimal (5,2)**|平均寫入 I/O 輸送量使用率的服務層限制的百分比。|  
|avg_memory_usage_percent|**decimal (5,2)**|平均記憶體使用率，以服務層限制的百分比計算。<br /><br /> 這包括用於緩衝集區分頁和儲存體的記憶體內部 OLTP 物件的記憶體。|  
|xtp_storage_percent|**decimal (5,2)**|儲存體使用量記憶體內部 OLTP 的服務層限制的百分比表示 （在報告的時間間隔結束）。 這包括用來儲存下列記憶體內部 OLTP 物件的記憶體： 記憶體最佳化資料表、 索引和資料表變數。 它也包含用於處理的 ALTER TABLE 作業的記憶體。<br /><br /> 如果未使用記憶體內部 OLTP 資料庫中，會傳回 0。|  
|max_worker_percent|**decimal (5,2)**|最大並行背景工作角色 （要求） 的資料庫的服務層限制的百分比表示。|  
|max_session_percent|**decimal (5,2)**|最大並行工作階段的資料庫服務層限制百分比表示。|  
|dtu_limit|**int**|目前最大資料庫 DTU 此資料庫設定在此間隔期間。 使用以 vCore 為基礎的模型資料庫，此資料行是 NULL。|
|cpu_limit|**decimal (5,2)**|在此間隔期間此資料庫的 Vcore 的數目。 使用以 DTU 為基礎的模型資料庫，此資料行是 NULL。|
|avg_instance_cpu_percent|**decimal (5,2)**|平均資料庫 CPU 使用量百分比。|
|avg_instance_memory_percent|**decimal (5,2)**|資料庫平均記憶體使用量百分比。|
|avg_login_rate_percent|**decimal (5,2)**|僅供參考之用。 不支援。 我們無法保證未來的相容性。|
|replica_role|**int**|表示目前的複本角色為主要的 0、 1 與次要資料庫，以及 2 為轉寄站 （異地次要資料庫的主要）。 您會看到 「 1 」 時連接到所有的可讀取次要複本的唯讀意圖。 如果未指定唯讀意圖，以連接到異地次要資料庫，您應該會看到"2"（連線到轉寄站）。|
|||
  
> [!TIP]  
>  如需這些限制和服務層的詳細內容，請參閱主題[服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)並[服務層功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)。  
  
## <a name="permissions"></a>Permissions  
 此檢視需要 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 所傳回的資料**sys.dm_db_resource_stats**會以您所執行的服務層/效能層級的限制所允許的最大的百分比表示。
 
 如果資料庫在過去的 60 分鐘內已容錯移轉到另一部伺服器，檢視將只會傳回該資料庫在容錯移轉之後做為主要資料庫時的資料。  
  
 這項資料較不精細的檢視，使用**sys.resource_stats**目錄檢視中的**主要**資料庫。 此檢視會每隔 5 秒擷取一次資料，並會保留 14 天內的歷程記錄資料。  如需詳細資訊，請參閱 < [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)。  
  
 當資料庫的彈性集區成員時，資源統計資料顯示為百分比值，會以資料庫在彈性集區設定中所設定的最大限制的百分比表示。  
  
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
    AVG(avg_log_write_percent) AS 'Average Log Write I/O Throughput Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write I/O Throughput Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>另請參閱  
 [sys.resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服務層功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
