---
description: sys.resource_stats (Azure SQL Database)
title: sys.resource_stats (Azure SQL Database) Microsoft Docs
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
ms.openlocfilehash: eea603b089c93b86b92ac39a22d0c6e9c64b49d9
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91807014"
---
# <a name="sysresource_stats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  傳回 Azure SQL Database 的 CPU 使用量和儲存體資料。 於五分鐘間隔內收集及彙總資料。 針對每個使用者資料庫，每隔五分鐘的報告視窗都會有一個資料列，其中資源耗用量有變更。 傳回的資料包含 CPU 使用量、儲存體大小變更和資料庫 SKU 修改。 沒有變更的閒置資料庫在每隔五分鐘的間隔內可能不會有資料列。 歷程記錄資料大約會保留 14 天。  
  
 **Sys.resource_stats** view 具有不同的定義，這取決於與資料庫相關聯的 Azure SQL Database 伺服器版本。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。  
  
 下表描述 v12 伺服器中可用的資料行：  
  
|資料行|資料類型|描述|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC 時間，表示5分鐘報告間隔的開始時間。|  
|end_time|**datetime**|指出五分鐘報告間隔結束的 UTC 時間。|  
|database_name|**nvarchar(128)**|使用者資料庫的名稱。|  
|sku|**nvarchar(128)**|資料庫服務層。 以下是可能的值：<br /><br /> 基本<br /><br /> 標準<br /><br /> Premium<br /><br />一般用途<br /><br />業務關鍵|  
|storage_in_megabytes|**float**|時間週期的最大儲存體大小（以 mb 為單位），包括資料庫資料、索引、預存程式和中繼資料。|  
|avg_cpu_percent|**decimal (5，2) **|平均運算使用率，以服務層限制的百分比計算。|  
|avg_data_io_percent|**decimal (5，2) **|根據服務層限制，計算平均 I/O 使用率的百分比。 針對超大規模資料庫，請參閱 [資源使用量統計資料中的資料 IO](/azure/sql-database/sql-database-hyperscale-performance-diagnostics#data-io-in-resource-utilization-statistics)。|  
|avg_log_write_percent|**decimal (5，2) **|平均寫入資源使用率，以服務層限制的百分比計算。|  
|max_worker_percent|**decimal (5，2) **|並行工作者 (要求的最大值會根據資料庫服務層級的限制，) 以百分比表示。<br /><br /> 根據並行背景工作計數的15秒樣本，最大值目前是以五分鐘的間隔計算。|  
|max_session_percent|**decimal (5，2) **|並行會話的數目上限，以百分比為單位，以資料庫的服務層級為基礎。<br /><br /> 根據並行會話計數的15秒樣本，最大值目前是根據五分鐘的間隔進行計算。|  
|dtu_limit|**int**|此間隔期間，此資料庫目前的最大資料庫 DTU 設定。 |
|xtp_storage_percent|**decimal (5，2) **|記憶體內部 OLTP 的儲存體使用量，以服務層的限制百分比為單位， (在報告間隔結束時) 。 這包括用於儲存下列記憶體內部 OLTP 物件的記憶體：記憶體優化資料表、索引和資料表變數。 它也包含用來處理 ALTER TABLE 作業的記憶體。<br /><br /> 如果資料庫中未使用記憶體內部 OLTP，則傳回0。|
|avg_login_rate_percent|**decimal (5，2) **|僅供參考之用。 不支援。 我們無法保證未來的相容性。|
|avg_instance_cpu_percent|**decimal (5，2) **|平均資料庫 CPU 使用量，以 SQL Database 進程的百分比表示。|
|avg_instance_memory_percent|**decimal (5，2) **|平均資料庫記憶體使用量（以 SQL Database 進程的百分比表示）。|
|cpu_limit|**decimal (5，2) **|此資料庫在此間隔期間的虛擬核心數目。 針對使用以 DTU 為基礎之模型的資料庫，這個資料行是 Null。|
|allocated_storage_in_megabytes|**float**|格式化的檔案空間量（以 MB 為單位），可用於儲存資料庫資料。 格式化的檔案空間也稱為已配置的資料空間。  如需詳細資訊，請參閱： [SQL Database 中的檔案空間管理](/azure/sql-database/sql-database-file-space-management)|
  
> [!TIP]  
>  如需這些限制和服務層級的詳細內容，請參閱 [服務層級](/azure/azure-sql/database/purchasing-models)。  
    
## <a name="permissions"></a>權限  
 此視圖適用于具有連接至虛擬 **master** 資料庫之許可權的所有使用者角色。  
  
## <a name="remarks"></a>備註  
 **Sys.resource_stats**所傳回的資料會以您正在執行的服務層級/效能層級的最大允許限制百分比表示。  
  
 當資料庫是彈性集區的成員時，以百分比值呈現的資源統計資料會以彈性集區設定中設定之資料庫的最大限制百分比表示。  
  
 若要更細微地查看這項資料，請在使用者資料庫中使用 **sys.dm_db_resource_stats** 動態管理檢視。 此檢視表每隔 15 秒就會擷取一次資料，並會維持 1 小時內的歷程記錄資料。  如需詳細資訊，請參閱 [sys.dm_db_resource_stats &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)。  

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
 [服務層級](/azure/azure-sql/database/purchasing-models)   
 [服務層的功能和限制](/azure/azure-sql/database/performance-guidance)  
  
