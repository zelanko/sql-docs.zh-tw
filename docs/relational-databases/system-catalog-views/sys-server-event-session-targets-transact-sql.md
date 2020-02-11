---
title: sys.databases server_event_session_targets （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_event_session_targets_TSQL
- sys.server_event_session_targets_TSQL
- sys.server_event_session_targets
- server_event_session_targets
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_event_session_targets catalog view
- xe
ms.assetid: dda4879d-57ae-4267-b410-1ef5c37404c7
author: stevestein
ms.author: sstein
ms.openlocfilehash: d9d3000b38f8cc59ef1349a1e0cd9219a3eb385f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68133185"
---
# <a name="sysserver_event_session_targets-transact-sql"></a>sys.server_event_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回事件工作階段中每一個事件目標的資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|target_id|**int**|目標的識別碼。 這個識別碼在事件工作階段物件中是唯一的。 不可為 Null。|  
|NAME|**sysname**|事件目標的名稱。 不可為 Null。|  
|套件|**sysname**|包含此事件目標之事件封裝的名稱。 不可為 Null。|  
|module|**sysname**|包含此事件目標之模組的名稱。 不可為 Null。|  
  
## <a name="permissions"></a>權限  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
||||  
|-|-|-|  
|從|至|關聯性|  
|sys.server_event_session_targets.event_session_id|server_event_sessions. event_session_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [擴充的事件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
