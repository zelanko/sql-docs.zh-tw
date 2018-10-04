---
title: sys.geo_replication_links (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: system-objects
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6b37ca384c2d3402a3b9ec01a4b9d6ccbfb7d402
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610106"
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含每個複寫連結中的異地複寫合作關係的主要和次要資料庫之間的資料列。 此檢視表位於邏輯 master 資料庫。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|database_id|**int**|目前資料庫中的 sys.databases 檢視的識別碼。|  
|start_date|**datetimeoffset**|在區域 SQL Database 資料中心起始資料庫複製時的 UTC 時間|  
|modify_date|**datetimeoffset**|在完成資料庫異地複寫區域的 SQL Database 資料中心的 UTC 時間。 新的資料庫與主要資料庫於此時間同步。 .|  
|link_guid|**uniqueidentifier**|異地複寫連結的唯一識別碼。|  
|partner_server|**sysname**|包含異地複寫資料庫的邏輯伺服器的名稱。|  
|partner_database|**sysname**|異地複寫連結的邏輯伺服器上資料庫的名稱。|  
|replication_state|**tinyint**|此資料庫，其中的異地複寫的狀態:。<br /><br /> 0 = 暫止。 已排程建立作用中次要資料庫，但必要的準備步驟尚未完成。<br /><br /> 1 = 植入。 異地複寫目標正在植入，但兩個資料庫都尚未同步處理。 植入完成之前，您無法連接到次要資料庫。 從主要中移除次要資料庫，將會取消植入作業。<br /><br /> 2 = 更新。 次要資料庫處於交易一致的狀態，並且與主要資料庫持續同步處理。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|異地複寫角色，其中一個：<br /><br /> 0 = 主要。 Database_id 指的是 「 異地複寫 」 合作關係中的主要資料庫。<br /><br /> 1 = 次要資料庫。  Database_id 指的是 「 異地複寫 」 合作關係中的主要資料庫。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|次要類型，其中一個：<br /><br /> 0 = 否。 容錯移轉之前，不可以存取次要資料庫。<br /><br /> 1 = 唯讀。 次要資料庫是只能存取用戶端連線使用 ApplicationIntent = ReadOnly。<br /><br /> 2 = 全部。 存取所有用戶端連接至次要資料庫。|  
|secondary_allow_connections _desc|**nvarchar(256)**|否<br /><br /> All<br /><br /> 唯讀|  
  
## <a name="permissions"></a>Permissions  
 此檢視僅供以**主要**伺服器層級主體登入的資料庫。  
  
## <a name="example"></a>範例  
 顯示具有異地複寫連結的所有資料庫。  
  
```  
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
 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL Database&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
