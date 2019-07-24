---
title: resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
author: julieMSFT
ms.author: jrasnick
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f151d62a03cebf931c58f37b1e126a7331cefae9
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/23/2019
ms.locfileid: "68418864"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 Azure SQL Database 的 CPU 使用量和儲存體資料。 於五分鐘間隔內收集及彙總資料。 針對每個使用者資料庫, 每五分鐘的報告時間範圍都會有一個資料列, 其中資源耗用量有變更。 傳回的資料包括 CPU 使用量、儲存體大小變更和資料庫 SKU 修改。 沒有變更的閒置資料庫, 每隔五分鐘不會有資料列。 歷程記錄資料大約會保留 14 天。  
  
 **Resource_stats** view 具有不同的定義, 視與資料庫相關聯的 Azure SQL Database 伺服器版本而定。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。  
  
 下表描述 v12 伺服器中可用的資料行：  
  
|[資料行]|資料類型|描述|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC 時間, 表示五分鐘報告間隔的開始。|  
|end_time|**datetime**|UTC 時間, 表示五分鐘報告間隔的結束。|  
|database_name|**nvarchar(128)**|使用者資料庫的名稱。|  
|sku|**nvarchar(128)**|資料庫服務層。 以下是可能的值：<br /><br /> [基本]<br /><br /> Standard<br /><br /> Premium<br /><br />一般用途<br /><br />業務關鍵|  
|storage_in_megabytes|**float**|時間週期內的最大儲存體大小 (以 mb 為單位), 包括資料庫資料、索引、預存程式和中繼資料。|  
|avg_cpu_percent|**decimal(5,2)**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**decimal(5,2)**|根據服務層限制，計算平均 I/O 使用率的百分比。|  
|avg_log_write_percent|**decimal(5,2)**|平均寫入資源使用率，以服務層限制的百分比計算。|  
|max_worker_percent|**decimal(5,2)**|最大並行背景工作 (要求) 百分比, 以資料庫服務層的限制為准。<br /><br /> 根據並行背景工作計數的15秒樣本, 目前已計算五分鐘間隔的最大值。|  
|max_session_percent|**decimal(5,2)**|以資料庫服務層的限制為依據的最大並行會話數百分比。<br /><br /> 根據並行會話計數的15秒樣本, 目前已針對五分鐘的間隔計算最大值。|  
|dtu_limit|**int**|此時間間隔期間, 此資料庫目前的最大資料庫 DTU 設定。 |   
|allocated_storage_in_megabytes|**float**|用來儲存資料庫資料的格式化檔案空間量 (以 MB 為單位)。 已格式化的檔案空間也稱為已配置的資料空間。  如需詳細資訊，請參閱：[SQL DB 中的檔案空間管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  如需有關這些限制和服務層級的詳細資訊, 請參閱[服務層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)主題。  
    
## <a name="permissions"></a>Permissions  
 此視圖適用于具有連接到虛擬**master**資料庫之許可權的所有使用者角色。  
  
## <a name="remarks"></a>備註  
 **Resource_stats**所傳回的資料會以您所執行的服務層/效能層級的最大允許限制百分比表示。  
  
 當資料庫是彈性集區的成員時, 以百分比值呈現的資源統計資料會以彈性集區設定中所設之資料庫的最大限制百分比表示。  
  
 如需這項資料的更細微觀點, 請在使用者資料庫中使用**sys.databases _db_resource_stats**動態管理檢視。 此檢視表每隔 15 秒就會擷取一次資料，並會維持 1 小時內的歷程記錄資料。  如需詳細資訊, 請參閱[_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)。  

## <a name="examples"></a>範例  
 下列範例會傳回上一週平均至少為 80% 運算使用率的所有資料庫。  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>另請參閱  
 [服務層級](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服務層級功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
