---
title: "sys.dm_continuous_copy_status (Azure SQL Database) |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.dm_continuous_copy_status_TSQL
- dm_continuous_copy_status_TSQL
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
dev_langs:
- TSQL
helpviewer_keywords:
- dm_continuous_copy_status
- sys.dm_continuous_copy_status
ms.assetid: 411b2e71-4421-4ef5-900d-5af068750899
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34d840580edb8bb15f4af379575bc0f24b44edcc
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmcontinuouscopystatus-azure-sql-database"></a>sys.dm_continuous_copy_status (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回資料列的每個使用者資料庫 (V11) 目前參與異地備援連續複製關聯性。 如果給定的主要資料庫起始一個以上的連續複製關聯性，這個資料表會針對每個使用中的次要資料庫各包含一個資料列。  
  
如果您使用 SQL Database V12 您應該使用[sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md) (因為*sys.dm_continuous_copy_status*只適用於 V11)。

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**copy_guid**|**uniqueidentifier**|複本資料庫的唯一識別碼。|  
|**partner_server**|**sysname**|連結的 SQL Database 伺服器的名稱。|  
|**partner_database**|**sysname**|連結的 SQL Database 伺服器上所連結資料庫的名稱。|  
|**last_replication**|**datetimeoffset**|最後套用之複寫交易的時間戳記。|  
|**replication_lag_sec**|**int**|目前時間與作用中的次要資料庫尚未認可之主要資料庫上最後一個成功認可交易的時間戳記之間的時差。|  
|**replication_state**|**tinyint**|此資料庫的連續複製複寫狀態。 以下是可能的值和它們的描述。<br /><br /> 1： 植入。 將要植入複寫目標，且該目標處於交易不一致的狀態。 在植入完成之前，您無法連接到作用中的次要資料庫。 <br />2： 趕上進度。 作用中的次要資料庫目前正在趕上主要資料庫，並且處於交易一致的狀態。<br />3： 重新植入。 因為發生無法復原的複寫失敗，所以作用中的次要資料庫正要自動重新植入。<br />4： 暫止。 這表示沒有作用中的連續複製關聯性。 這個狀態通常表示互連可用的頻寬對於主要資料庫上的交易活動層級而言不足。 不過，連續複製關聯性仍保持不變。|  
|**replication_state_desc**|**nvarchar(256)**|replication_state 的描述有下列幾種：<br /><br /> SEEDING<br /><br /> CATCH_UP<br /><br /> RE_SEEDING<br /><br /> SUSPENDED|  
|**is_rpo_limit_reached**|**bit**|這個值一定會設定為 0。|  
|**is_target_role**|**bit**|0 = 複製關聯性的來源<br /><br /> 1 = 複製關聯性的目標|  
|**is_interlink_connected**|**bit**|1 = 互連已連接。<br /><br /> 0 = 互連中斷連接。|  
  
## <a name="permissions"></a>Permissions  
 要擷取資料，需要的成員資格**db_owner**資料庫角色。 Dbo 使用者、 成員的**dbmanager**資料庫角色和 sa 登入全都可以查詢此檢視也。  
  
## <a name="remarks"></a>備註  
 **Sys.dm_continuous_copy_status**中建立檢視**資源**資料庫中，會顯示在所有資料庫，包括邏輯 master 中。 不過，在邏輯 master 中查詢這個檢視表會傳回空集。  
  
 如果在資料庫上，該資料庫中的資料列的連續複製關聯性終止**sys.dm_continuous_copy_status**檢視就會消失。  
  
 像**sys.dm_database_copies**  檢視中， **sys.dm_continuous_copy_status**會反映連續複製關聯性中資料庫的主要或作用中次要資料庫的狀態. 不同於**sys.dm_database_copies**， **sys.dm_continuous_copy_status**包含數個資料行提供有關作業與效能的詳細資料。 這些資料行包含**last_replication**，和**replication_lag_sec**...  
  
## <a name="see-also"></a>另請參閱  
 [sys.dm_database_copies &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-copies-azure-sql-database.md)   
 [作用中地理複寫預存程序 &#40;TRANSACT-SQL &#41;](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)  
  
  
