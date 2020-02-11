---
title: sys. dm_db_resource_stats （Azure SQL Database） |Microsoft Docs
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 1dd66834788896e6952a0352eb2a19fd1a828513
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "75245957"
---
# <a name="sysdm_db_resource_stats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 資料庫的 CPU、I/O 和記憶體耗用量。 每 15 秒會有一列，即使資料庫沒有任何活動，也會有一列。 歷程記錄資料大約會保留一小時。  
  
|資料行|資料類型|描述|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|UTC 時間會指出目前報告間隔的結束。|  
|avg_cpu_percent|**decimal （5，2）**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**decimal （5，2）**|平均資料 i/o 使用率，以服務層限制的百分比表示。 如需超大規模資料庫資料庫，請參閱[資源使用量統計資料中的資料 IO](https://docs.microsoft.com/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)。|  
|avg_log_write_percent|**decimal （5，2）**|平均交易記錄寫入（以 MBps 為單位），以服務層限制的百分比表示。|  
|avg_memory_usage_percent|**decimal （5，2）**|平均記憶體使用率，以服務層限制的百分比計算。<br /><br /> 這包括用於緩衝集區頁面的記憶體，以及記憶體內部 OLTP 物件的儲存空間。|  
|xtp_storage_percent|**decimal （5，2）**|記憶體內部 OLTP 的儲存使用量，以服務層限制的百分比表示（在報告間隔結束時）。 這包括用於儲存下列記憶體內部 OLTP 物件的記憶體：記憶體優化資料表、索引和資料表變數。 它也包含用來處理 ALTER TABLE 作業的記憶體。<br /><br /> 如果資料庫中未使用記憶體內部 OLTP，則傳回0。|  
|max_worker_percent|**decimal （5，2）**|最大並行背景工作角色（要求），以資料庫服務層級限制的百分比表示。|  
|max_session_percent|**decimal （5，2）**|並行會話的最大值，以資料庫服務層的限制百分比表示。|  
|dtu_limit|**int**|此時間間隔期間，此資料庫目前的最大資料庫 DTU 設定。 對於使用以 vCore 為基礎之模型的資料庫，這個資料行是 Null。|
|cpu_limit|**decimal （5，2）**|此間隔期間此資料庫的虛擬核心數目。 對於使用以 DTU 為基礎之模型的資料庫，這個資料行是 Null。|
|avg_instance_cpu_percent|**decimal （5，2）**|平均資料庫 CPU 使用量，以 SQL DB 進程的百分比表示。|
|avg_instance_memory_percent|**decimal （5，2）**|以 SQL DB 進程的百分比表示的平均資料庫記憶體使用量。|
|avg_login_rate_percent|**decimal （5，2）**|僅供參考之用。 不支援。 我們無法保證未來的相容性。|
|replica_role|**int**|代表目前複本的角色，其中0為主要，1做為次要，而2作為轉寄站（異地次要資料庫的主要）。 當您使用 ReadOnly 意圖連接到所有可讀取的次要複本時，您會看到 "1"。 如果連接到異地次要資料庫但未指定 ReadOnly 意圖，您應該會看到 "2" （連接到轉寄站）。|
|||
  
> [!TIP]  
>  如需有關這些限制和服務層級的詳細資訊，請參閱[服務層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[服務層功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)主題。  
  
## <a name="permissions"></a>權限  
 此檢視需要 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 **Dm_db_resource_stats sys.databases**傳回的資料會以您所執行的服務層/效能層級的最大允許限制百分比表示。
 
 如果資料庫在過去的 60 分鐘內已容錯移轉到另一部伺服器，檢視將只會傳回該資料庫在容錯移轉之後做為主要資料庫時的資料。  
  
 若要以較長的保留期限更精細地查看此資料，請使用**master**資料庫中的**sys.databases resource_stats**目錄查看。 此檢視會每隔 5 秒擷取一次資料，並會保留 14 天內的歷程記錄資料。  如需詳細資訊，請參閱[sys. resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)。  
  
 當資料庫是彈性集區的成員時，以百分比值呈現的資源統計資料會以彈性集區設定中所設之資料庫的最大限制百分比表示。  
  
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
 [resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [服務層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服務層的功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
