---
title: sys.resource_stats （SQL Azure 資料庫） |Microsoft 文件
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c2f8a0e0cebcf64bedac33861184e806f322d7d1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回 Azure SQL Database 的 CPU 使用量和儲存體資料。 於五分鐘間隔內收集及彙總資料。 每個使用者資料庫各有一個資料列代表每隔五分鐘報告資源耗用變化的視窗。 傳回的資料包括 CPU 使用量、 儲存體大小變更或資料庫 SKU 修改。 每隔五分鐘的間隔，未變更的閒置資料庫可能沒有資料列。 歷程記錄資料大約會保留 14 天。  
  
 **Sys.resource_stats**檢視具有不同的定義，根據資料庫相關聯的 Azure SQL Database 伺服器的版本。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。  
  
 下表描述 v12 伺服器中可用的資料行：  
  
|資料行|資料類型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC 時間表示的五分鐘報告間隔的開始。|  
|end_time|**datetime**|指出五分鐘報告間隔結束的 UTC 時間。|  
|database_name|**varchar**|使用者資料庫的名稱。|  
|sku|**varchar**|資料庫服務層。 以下是可能的值：<br /><br /> Basic<br /><br /> Standard<br /><br /> Premium<br /><br />一般用途<br /><br />業務關鍵|  
|storage_in_megabytes|**float**|儲存體大小上限以 mb 為單位的時間週期，包括資料庫資料、 索引、 預存程序和中繼資料。|  
|avg_cpu_percent|**numeric**|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**numeric**|根據服務層限制，計算平均 I/O 使用率的百分比。|  
|avg_log_write_percent|**numeric**|平均寫入資源使用率，以服務層限制的百分比計算。|  
|max_worker_percent|**decimal(5,2)**|最大並行工作者 （要求），以根據資料庫的服務層限制的百分比表示。<br /><br /> 最大值目前計算五分鐘的間隔 15 秒樣本的並行工作者計數為基礎。|  
|max_session_percent|**decimal(5,2)**|以百分比表示，根據資料庫的服務層限制的最大並行工作階段。<br /><br /> 最大值目前計算五分鐘的間隔 15 秒樣本的並行工作階段計數為基礎。|  
|dtu_limit|**int**|目前最大資料庫 DTU 此資料庫設定此間隔。 |  
  
> [!TIP]  
>  詳細說明這些限制，以及服務層的內容，請參閱主題[服務層](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)。  
    
## <a name="permissions"></a>Permissions  
 這個檢視可用於所有的使用者角色有權連接到虛擬**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 所傳回的資料**sys.resource_stats**的最大允許您正在執行的服務層/效能層級的限制百分比表示。  
  
 彈性集區的成員資料庫時，資源統計資料呈現為百分比的值會表示為資料庫在彈性集區設定中所設定的最大限制的百分比。  
  
 這項資料的更細微的檢視，使用**sys.dm_db_resource_stats**使用者資料庫中的動態管理檢視。 此檢視擷取資料每隔 15 秒，並維持 1 小時內的歷程記錄資料。  如需詳細資訊，請參閱[sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)。  

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
 [服務層的功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
