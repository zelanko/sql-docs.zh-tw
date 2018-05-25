---
title: sys.dm_xe_session_events (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_events
- sys.dm_xe_session_events_TSQL
- dm_xe_session_events
- dm_xe_session_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_events dynamic management view
- extended events [SQL Server], views
ms.assetid: 4f027b31-4e03-43a6-849d-1ba9d8d34ae8
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f26973eb275e818690c1e61b7e27c3681f7b64c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmxesessionevents-transact-sql"></a>sys.dm_xe_session_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回有關工作階段事件的資訊。 事件是不連續的執行點。 述詞可以套用至事件，以便在事件不包含必要資訊時阻止事件引發。  
   
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件工作階段的記憶體位址。 不可為 Null。|  
|event_name|**nvarchar(60)**|動作繫結之事件的名稱。 不可為 Null。|  
|event_package_guid|**uniqueidentifier**|包含此事件之封裝的 GUID。 不可為 Null。|  
|event_predicate|**nvarchar(2048)**|套用至事件之述詞樹狀結構的 XML 表示。 可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
### <a name="relationship-cardinalities"></a>關聯性基數  
  
|來源|若要|關聯性|  
|----------|--------|------------------|  
|sys.dm_xe_session_events.event_session_address|sys.dm_xe_sessions.address|多對一|  
|sys.dm_xe_session_events.event_package_guid, sys.dm_xe_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [動態管理檢視與函數 &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

