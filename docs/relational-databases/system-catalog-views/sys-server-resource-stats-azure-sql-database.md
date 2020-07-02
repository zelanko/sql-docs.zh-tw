---
title: sys. server_resource_stats （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
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
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: e85a74b203d270223d215ace08a58a0eea980fa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772984"
---
# <a name="sysserver_resource_stats-azure-sql-database"></a>sys. server_resource_stats （Azure SQL Database）
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

傳回 Azure SQL 受控執行個體的 CPU 使用量、IO 和儲存體資料。 於五分鐘間隔內收集及彙總資料。 每隔15秒報告就會有一個資料列。 傳回的資料包括 CPU 使用量、儲存體大小、IO 使用率和受控實例 SKU。 歷程記錄資料大約會保留 14 天。

根據與資料庫相關聯的 Azure SQL 受控實例版本而定，[ **server_resource_stats** ] 視圖會有不同的定義。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。
 
  
 下表描述 v12 伺服器中可用的資料行：  
  
|資料行|資料類型|描述|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|表示十五秒報告間隔開始的 UTC 時間|  
|end_time|**datetime**|表示十五秒報告間隔結束的 UTC 時間|
|resource_type|Nvarchar(128)|提供計量的資源類型|
|resource_name|nvarchar(128)|資源名稱。|
|sku|nvarchar(128)|受控執行個體實例的服務層級。 以下是可能的值： <br><ul><li>一般用途</li></ul><ul><li>業務關鍵</li></ul>|
|hardware_generation|nvarchar(128)|硬體世代識別碼：例如 Gen 4 或 Gen 5|
|virtual_core_count|int|代表每個實例的虛擬核心數目（公開預覽中為8、16或24）|
|avg_cpu_percent|decimal （5，2）|實例所使用之受控執行個體服務層級限制的平均計算使用率百分比。 其計算方式為實例中所有資料庫之所有資源集區的 CPU 時間總和，並依給定間隔中該階層的可用 CPU 時間分割。|
|reserved_storage_mb|BIGINT|每個實例的保留儲存體（客戶為受控實例購買的儲存空間數量）|
|storage_space_used_mb|十進位（18，2）|所有受控實例資料庫檔案所使用的儲存空間（包括使用者和系統資料庫）|
|io_request|BIGINT|間隔內的 i/o 實體作業總數|
|io_bytes_read|BIGINT|在間隔內讀取的實體位元組數|
|io_bytes_written|BIGINT|在間隔內寫入的實體位元組數|

 
> [!TIP]  
>  如需有關這些限制和服務層級的詳細資訊，請參閱[受控執行個體服務層級](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)的主題。  
    
## <a name="permissions"></a>權限  
 這個視圖適用于具有連接到**master**資料庫之許可權的所有使用者角色。  
  
## <a name="remarks"></a>備註  
 **Server_resource_stats sys.databases**所傳回的資料會以 [avg_cpu] 以外的 [位元組] 或 [mb] （在 [資料行名稱] 中所述）來表示，這會以您所執行的服務層級/效能等級上限的百分比表示。  
 
## <a name="examples"></a>範例  
 下列範例會傳回上一週平均至少為 80% 運算使用率的所有資料庫。  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>另請參閱  
 [受控執行個體服務層級](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)
