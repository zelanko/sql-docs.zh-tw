---
title: sys.database_event_session_fields (Azure SQL Database) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 0a7c7ee610ae5eb3a56a46c5b8c7ba1645b64532
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2018
ms.locfileid: "37981850"
---
# <a name="sysdatabaseeventsessionfields-azure-sql-database"></a>sys.database_event_session_fields (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  針對事件和目標上明確設定的每一個可自訂資料行傳回資料列。  
  
||  
|-|  
|**適用於**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 及更新的版本。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|object_id|**int**|這個欄位相關聯之物件的識別碼。 不可為 Null。|  
|NAME|**sysname**|欄位的名稱。 不可為 Null。|  
|value|**sql_variant**|此欄位的值。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
||||  
|-|-|-|  
|來源|若要|關聯性|  
|sys.database_event_session_actions.event_session_id|sys.database_event_sessions.event_session_id|多對一|  
|sys.database_event_session_actions.event_id<br /><br /> sys.database_event_session_actions.object_id<br /><br /> sys.database_event_session_actions.event_session_id|sys.database_event_session_events.event_session_id<br /><br /> sys.database_event_session_events.event_id|多對一|  
|sys.database_event_session_actions.event_session_id<br /><br /> sys.database_event_session_actions.object_id|sys.database_event_session_targets.event_session_id<br /><br /> sys.database_event_session_targets.target_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
