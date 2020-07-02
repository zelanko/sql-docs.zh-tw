---
title: sys. geo_replication_links （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
author: CarlRabeler
ms.author: carlrab
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c59f3379d2f210d96b97e497ecb8f332a6f93d2a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85647902"
---
# <a name="sysgeo_replication_links-azure-sql-database"></a>sys.geo_replication_links (Azure SQL Database)

[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  針對異地複寫合作關係中的主要和次要資料庫之間的每個複寫連結，各包含一個資料列。 此檢視表位於邏輯 master 資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Sys.databases 視圖中目前資料庫的識別碼。|  
|start_date|**datetimeoffset**|起始資料庫複寫時，地區 SQL Database 資料中心的 UTC 時間|  
|modify_date|**datetimeoffset**|當資料庫異地複寫完成時，地區 SQL Database datacenter 的 UTC 時間。 此時，新的資料庫會與主資料庫同步處理。 .|  
|link_guid|**uniqueidentifier**|異地複寫連結的唯一識別碼。|  
|partner_server|**sysname**|包含異地複寫資料庫之 SQL Database 伺服器的名稱。|  
|partner_database|**sysname**|已連結 SQL Database 伺服器上的異地複寫資料庫名稱。|  
|replication_state|**tinyint**|此資料庫的異地複寫狀態，下列其中一個：。<br /><br /> 0 = 暫止。 已排程建立作用中次要資料庫，但尚未完成必要的準備步驟。<br /><br /> 1 = 植入。 已植入異地複寫目標，但這兩個資料庫尚未同步處理。 在植入完成之前，您無法連接到次要資料庫。 從主要複本移除次要資料庫將會取消植入操作。<br /><br /> 2 = 趕上。 次要資料庫處於交易一致的狀態，而且經常與主資料庫同步處理。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|異地複寫角色，下列其中一個：<br /><br /> 0 = 主要。 Database_id 指的是「異地複寫」合作關係中的主資料庫。<br /><br /> 1 = 次要。  Database_id 指的是「異地複寫」合作關係中的主資料庫。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|次要類型，下列其中一個：<br /><br /> 0 = 否。 在容錯移轉之前，無法存取次要資料庫。<br /><br /> 1 = 唯讀。 次要資料庫只能供 ApplicationIntent = ReadOnly 的用戶端連接存取。<br /><br /> 2 = 全部。 次要資料庫可供任何用戶端連接存取。|  
|secondary_allow_connections _desc|**nvarchar(256)**|否<br /><br /> 全部<br /><br /> 唯讀|  
  
## <a name="permissions"></a>權限

此視圖僅適用于**master**資料庫中的伺服器層級主體登入。  
  
## <a name="example"></a>範例

顯示具有異地複寫連結的所有資料庫。  

```sql
SELECT
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc
FROM sys.geo_replication_links;  
```

## <a name="see-also"></a>另請參閱

 [ALTER DATABASE （Azure SQL Database）](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
