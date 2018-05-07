---
title: sys.dm_geo_replication_link_status (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 10/13/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5eb252c42cb8c455c4dff4f5c65e638edb140158
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含每個複寫連結進行異地複寫合作關係中的主要和次要資料庫之間的資料列。 這包括主要和次要資料庫。 如果在給定主要資料庫有一個以上的連續複寫連結，此資料表會包含一個資料列，每個關聯性。 在所有資料庫，包括邏輯 master 中建立檢視。 不過，在邏輯 master 中查詢這個檢視表會傳回空集。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|複寫連結的唯一識別碼。|  
|partner_server|**sysname**|包含連結的資料庫的邏輯伺服器的名稱。|  
|partner_database|**sysname**|連結的邏輯伺服器上所連結資料庫的名稱。|  
|last_replication|**datetimeoffset**|由次要的主要資料庫的最後一個交易的認可時間戳記。 只有在主要資料庫上使用此值。|  
|replication_lag_sec|**int**|以秒為單位的時間差異 last_replication 值之間的主要資料庫在主要伺服器上的該交易的認可時間戳記。  只有在主要資料庫上使用此值。|  
|replication_state|**tinyint**|此資料庫，其中的地理複寫的狀態:。<br /><br /> 1 = 植入。 地理複寫目標正在植入，但兩個資料庫都尚未同步處理。 植入完成之前，您無法連接到次要資料庫。 移除次要資料庫從主要會取消植入作業。<br /><br /> 2 = 更新。 次要資料庫處於交易一致的狀態，並正在經常同步處理與主要資料庫。<br /><br /> 4 = 已暫停。 這表示沒有作用中的連續複製關聯性。 這個狀態通常表示互連可用的頻寬對於主要資料庫上的交易活動層級而言不足。 不過，連續複製關聯性仍保持不變。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|地理複寫角色，其中一個：<br /><br /> 0 = 主要。 Database_id 指地理複寫合作關係中的主要資料庫。<br /><br /> 1 = 次要資料庫。  Database_id 指地理複寫合作關係中的主要資料庫。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|次要類型，其中一個：<br /><br /> 0 = 不直接允許連接次要資料庫與資料庫不是可讀取權限。<br /><br /> 2 = 所有次要 repl; 中的資料庫允許連接 ication 進行唯讀存取。|  
|secondary_allow_connections_desc|**nvarchar(256)**|否<br /><br /> 全部|  
|last_commit|**datetimeoffset**|對資料庫認可的最後一個交易的時間。 如果擷取主要資料庫上，它會指出在主要資料庫上的上次認可時間。 如果擷取次要資料庫上，它會指出在次要資料庫上的上次認可時間。 如果擷取次要資料庫上的主要複寫連結已關閉時，它會指出哪個時間點的次要資料庫趕上之後之前。|
  
> [!NOTE]  
>  如果終止複寫關聯性中移除次要資料庫 （區段 4.2）、 該資料庫中的資料列**sys.dm_geo_replication_link_status**檢視就會消失。  
  
## <a name="permissions"></a>Permissions  
 任何具有 view_database_state 權限的帳戶可以查詢**sys.dm_geo_replication_link_status**。  
  
## <a name="example"></a>範例  
 顯示複寫延遲和我的次要資料庫上一次複寫時間。  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>另請參閱  
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
