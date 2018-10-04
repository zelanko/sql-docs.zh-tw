---
title: sys.dm_geo_replication_link_status (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 10/13/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 57212bc80087e3f2227f90ab6fa16678df37517e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47809076"
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含每個複寫連結中的異地複寫合作關係的主要和次要資料庫之間的資料列。 這包括主要和次要資料庫。 如果給定主要資料庫有一個以上的連續複寫連結，此資料表會包含一個資料列，每個關聯性。 在所有資料庫，包括邏輯主機中建立檢視。 不過，在邏輯 master 中查詢這個檢視表會傳回空集。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|複寫連結的唯一識別碼。|  
|partner_server|**sysname**|包含連結的資料庫的邏輯伺服器的名稱。|  
|partner_database|**sysname**|連結的邏輯伺服器上所連結資料庫的名稱。|  
|last_replication|**datetimeoffset**|由次要的主要資料庫時鐘為基礎的最後一個交易的認可時間戳記。 只有在主要資料庫上使用此值。|  
|replication_lag_sec|**int**|時間之間的時差 last_replication 值與該交易的認可，在主要伺服器上，根據主要資料庫的時鐘的時間戳記。  只有在主要資料庫上使用此值。|  
|replication_state|**tinyint**|此資料庫，其中的異地複寫的狀態:。<br /><br /> 1 = 植入。 異地複寫目標正在植入，但兩個資料庫都尚未同步處理。 植入完成之前，您無法連接到次要資料庫。 從主要中移除次要資料庫，將會取消植入作業。<br /><br /> 2 = 更新。 次要資料庫處於交易一致的狀態，並且與主要資料庫持續同步處理。<br /><br /> 4 = 已暫停。 這表示沒有作用中的連續複製關聯性。 這個狀態通常表示互連可用的頻寬對於主要資料庫上的交易活動層級而言不足。 不過，連續複製關聯性仍保持不變。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|異地複寫角色，其中一個：<br /><br /> 0 = 主要。 Database_id 指的是 「 異地複寫 」 合作關係中的主要資料庫。<br /><br /> 1 = 次要資料庫。  Database_id 指的是 「 異地複寫 」 合作關係中的主要資料庫。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|次要類型，其中一個：<br /><br /> 0 = 不直接允許連接次要資料庫，而且資料庫不是可讀取權限。<br /><br /> 2 = all 允許次要的 repl; 中的資料庫連接 ication 進行唯讀存取。|  
|secondary_allow_connections_desc|**nvarchar(256)**|否<br /><br /> All|  
|last_commit|**datetimeoffset**|認可至資料庫的最後一個交易的時間。 如果擷取主要資料庫上，它會指出主要資料庫的上次認可時間。 如果擷取次要資料庫上，它會指出在次要資料庫上的最後一個認可時間。 如果擷取次要資料庫上的複寫連結的主要已關閉時，它會指出直到哪個時間點的次要資料庫趕上之後。|
  
> [!NOTE]  
>  如果藉由移除次要資料庫 （一節 4.2），該資料庫中的資料列，就會終止複寫關聯性**sys.dm_geo_replication_link_status**檢視就會消失。  
  
## <a name="permissions"></a>Permissions  
 任何具有 view_database_state 權限的帳戶可以查詢**sys.dm_geo_replication_link_status**。  
  
## <a name="example"></a>範例  
 顯示複寫落後和我的次要資料庫的上次複寫時間。  
  
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
  
  
