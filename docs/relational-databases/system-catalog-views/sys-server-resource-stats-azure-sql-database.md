---
title: sys.server_resource_stats (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: carlrab, edmaca
ms.technology: ''
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
manager: craigg
ms.openlocfilehash: 82cd70d9f1baa7741f4ecc449167d5c56e7fe954
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2018
ms.locfileid: "52392631"
---
# <a name="sysserverresourcestats-azure-sql-database"></a>sys.server_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

傳回 Azure SQL 受控執行個體的 CPU 使用量、 IO 和儲存體資料。 於五分鐘間隔內收集及彙總資料。 報告每 15 秒有一個資料列。 傳回的資料包括 CPU 使用量、 儲存體大小、 最高 IO 使用率，與受管理的執行個體 SKU。 歷程記錄資料大約會保留 14 天。

**Sys.server_resource_stats**檢視具有不同的定義，根據資料庫相關聯的 Azure SQL 受控執行個體的版本。 請考慮這些差異，以及升級到新伺服器版本時應用程式所需的任何修改。
 
  
 下表描述 v12 伺服器中可用的資料行：  
  
|[資料行]|資料類型|描述|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|指出報告 15 秒的時間間隔開始的 UTC 時間|  
|end_time|**datetime**|表示 15 秒報告時間間隔結束的 UTC 時間|
|resource_type|& lt;languagekeyword>nvarchar(128)</languagekeyword&gt|計量會提供的目標資源類型|
|resource_name|& lt;languagekeyword>nvarchar(128)</languagekeyword&gt|資源的名稱。|
|sku|& lt;languagekeyword>nvarchar(128)</languagekeyword&gt|受管理的執行個體的執行個體服務層。 以下是可能的值： <br><ul><li>一般用途</li></ul><ul><li>業務關鍵</li></ul>|
|hardware_generation|& lt;languagekeyword>nvarchar(128)</languagekeyword&gt|硬體產生識別碼： 例如，第 4 代或第 5 代|
|virtual_core_count|ssNoversion|代表每個執行個體 （8、 16 或 24 現供公開預覽） 的虛擬核心數目|
|avg_cpu_percent|decimal(5,2)|平均計算使用量過低的執行個體所管理的執行個體服務層限制的百分比。 它是計算的執行個體中的所有資料庫的所有資源集區的 CPU 時間的總和，除以該服務層可用的 CPU 時間，以指定的間隔。|
|reserved_storage_mb|BIGINT|保留每個執行個體的儲存體 （儲存體數量空格該客戶購買的受管理的執行個體）|
|storage_space_used_mb|decimal(18,2)|所有受管理的執行個體資料庫的檔案 （包括使用者和系統資料庫） 所使用的儲存體|
|io_request|BIGINT|I/o 的間隔內實體的作業總數|
|io_bytes_read|BIGINT|實體讀取的位元組數目的間隔內|
|io_bytes_written|BIGINT|實體寫入的位元組數目的間隔內|

 
> [!TIP]  
>  如需這些限制和服務層的詳細內容，請參閱主題[受控執行個體的服務層](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)。  
    
## <a name="permissions"></a>Permissions  
 這個檢視可供所有使用者角色權限來連接到**主要**資料庫。  
  
## <a name="remarks"></a>備註  
 所傳回的資料**sys.server_resource_stats**以外 avg_cpu，會以服務的限制所允許的最大的百分比來表示總位元組或 mb （資料行名稱中所述） 中使用您正在執行的層/效能層級。  
 
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
 [受控執行個體的服務層](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)
