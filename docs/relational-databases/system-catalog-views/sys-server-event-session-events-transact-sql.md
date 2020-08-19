---
description: sys.server_event_session_events (Transact-SQL)
title: sys. server_event_session_events (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_events
- server_event_session_events_TSQL
- sys.server_event_session_events
- sys.server_event_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_events catalog view
- xe
ms.assetid: 75986e91-1fc7-4f14-98ac-4e90154a74db
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cc4b6f67d282ce838ab5a5b8a401ade3a5e2e4c2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88447770"
---
# <a name="sysserver_event_session_events-transact-sql"></a>sys.server_event_session_events (Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  針對事件工作階段中的每個事件傳回資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|event_id|**int**|事件的識別碼。 這個識別碼在事件工作階段物件中是唯一的。 不可為 Null。|  
|NAME|**sysname**|事件的名稱。 不可為 Null。|  
|套件|**sysname**|包含此事件之事件封裝的名稱。 不可為 Null。|  
|name|**sysname**|包含此事件之模組的名稱。 不可為 Null。|  
|predicate|**Nvarchar (3000) **|套用至事件的述詞運算式。 可為 Null。|  
|predicate_xml|**Nvarchar (3000) **|套用至事件的 XML 述詞運算式。 可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
| 寄件者 | 收件者 | 關聯性 |
| ---- | -- | ------------ |
|sys.server_event_session_events.event_session_id|sys. server_event_sessions. event_session_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [&#40;Transact-sql&#41;的擴充事件目錄檢視 ](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
