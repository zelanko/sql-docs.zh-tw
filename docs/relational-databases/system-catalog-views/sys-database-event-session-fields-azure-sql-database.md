---
title: sys. database_event_session_fields （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
ms.assetid: 9b5c94d6-612c-4e0f-976d-ac6ba55da3ac
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 910c4a6a8ebf40de23069ecbf3c96d8d67533efa
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823540"
---
# <a name="sysdatabase_event_session_fields-azure-sql-database"></a>sys.database_event_session_fields (Azure SQL Database)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  針對事件和目標上明確設定的每一個可自訂資料行傳回資料列。  
  
||  
|-|  
|**適用**于： [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 和任何更新版本。|  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|object_id|**int**|這個欄位相關聯之物件的識別碼。 不可為 Null。|  
|name|**sysname**|欄位的名稱。 不可為 Null。|  
|value|**sql_variant**|此欄位的值。 不可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW DATABASE STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
||||  
|-|-|-|  
|從|至|關聯性|  
|database_event_session_actions. event_session_id|database_event_sessions. event_session_id|多對一|  
|database_event_session_actions. event_id<br /><br /> database_event_session_actions. object_id<br /><br /> database_event_session_actions. event_session_id|database_event_session_events. event_session_id<br /><br /> database_event_session_events. event_id|多對一|  
|database_event_session_actions. event_session_id<br /><br /> database_event_session_actions. object_id|database_event_session_targets. event_session_id<br /><br /> database_event_session_targets. target_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
