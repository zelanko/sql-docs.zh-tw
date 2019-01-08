---
title: sys.resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 72945aca048d322ee03c8a1d88b76650ddd1db16
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392691"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 Azure SQL Database 的 CPU 使用量和儲存體資料。 於五分鐘間隔內收集及彙總資料。 每個使用者資料庫中，有一個資料列，這在沒有資源耗用變化的每隔五分鐘報告視窗。 傳回的資料包括 CPU 使用量、 儲存體大小的變更和資料庫 SKU 修改。 每隔五分鐘的間隔，而不需變更閒置的資料庫可能沒有資料列。 歷程記錄資料大約會保留 14 天。  
  
 **Sys.resource_stats**檢視具有不同的定義，根據資料庫相關聯的 Azure SQL Database 伺服器的版本。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。  
  
 下表描述 v12 伺服器中可用的資料行：  
  
|[資料行]|資料類型|描述|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|指出五分鐘報告間隔開始的 UTC 時間。|  
|end_time|**datetime**|UTC 時間表示 5 分鐘報告間隔的結尾。|  
|database_name|**varchar**|使用者資料庫的名稱。|  
|sku|**varchar**|資料庫服務層。 以下是可能的值：<br /><br /> [基本]<br /><br /> Standard<br /><br /> Premium<br /><br />一般用途<br /><br />業務關鍵|  
|storage_in_megabytes|**float**|儲存體大小上限以 mb 為單位的時間週期，包括資料庫資料、 索引、 預存程序和中繼資料。|  
|avg_cpu_percent|**numeric**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**numeric**|根據服務層限制，計算平均 I/O 使用率的百分比。|  
|avg_log_write_percent|**numeric**|平均寫入資源使用率，以服務層限制的百分比計算。|  
|max_worker_percent|**decimal(5,2)**|最大並行背景工作角色 （要求） 的資料庫服務層限制的百分比。<br /><br /> 最大值是目前計算五分鐘的間隔 15 秒樣本的並行背景工作計數為基礎。|  
|max_session_percent|**decimal(5,2)**|以百分比表示，根據資料庫的服務層限制的最大並行工作階段。<br /><br /> 最大值是目前計算五分鐘的間隔 15 秒樣本的並行工作階段計數為基礎。|  
|dtu_limit|**int**|目前最大資料庫 DTU 此資料庫設定在此間隔期間。 |  
|allocated_storage_in_megabytes|**float**|數量的格式化檔案空間 (MB) 可用於儲存資料庫的資料。 格式的檔案空間也稱為 「 配置的資料空間。  如需詳細資訊，請參閱：[SQL DB 中的檔案空間管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  如需這些限制和服務層的詳細內容，請參閱主題[服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)。  
    
## <a name="permissions"></a>Permissions  
 這個檢視可供所有使用者角色權限來連接到虛擬**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 所傳回的資料**sys.resource_stats**會以您所執行的服務層/效能層級的限制所允許的最大的百分比表示。  
  
 當資料庫的彈性集區成員時，資源統計資料顯示為百分比值，會以資料庫在彈性集區設定中所設定的最大限制的百分比表示。  
  
 這項資料的更細微的檢視，使用**sys.dm_db_resource_stats**使用者資料庫中的動態管理檢視。 此檢視表每隔 15 秒就會擷取一次資料，並會維持 1 小時內的歷程記錄資料。  如需詳細資訊，請參閱 < [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)。  

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
 [服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服務層功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
