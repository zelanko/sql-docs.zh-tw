---
title: sys.dm_xe_database_session_targets (Azure SQL Database) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7284d59668742f2ad8821ebfb435de469ed31c4e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxedatabasesessiontargets-azure-sql-database"></a>sys.dm_xe_database_session_targets (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  傳回有關工作階段目標的資訊。  
  
||  
|-|  
|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和所有未來的版本。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件工作階段的記憶體位址。 具有多對一關係 sys.dm_xe_database_sessions.address。 不可為 Null。|  
|target_name|**nvarchar(60)**|工作階段內的目標名稱。 不可為 Null。|  
|target_package_guid|**uniqueidentifier**|包含目標之封裝的 GUID。 不可為 Null。|  
|execution_count|**bigint**|此目標已針對工作階段執行的次數。 不可為 Null。|  
|execution_duration_ms|**bigint**|此目標已經執行的總時間 (以毫秒為單位)。 不可為 Null。|  
|target_data|**nvarchar(max)**|此目標所維護的資料，例如事件彙總資訊。 可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要 VIEW DATABASE STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_targets.event_session_address|sys.dm_xe_database_sessions.address|多對一|  
  
  
