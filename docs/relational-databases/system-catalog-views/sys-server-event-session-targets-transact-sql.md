---
title: sys.server_event_session_targets (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b38bfd00a699cb997f6cc73776daf6bed5f4cb8
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023997"
---
# <a name="sysservereventsessiontargets-transact-sql"></a>sys.server_event_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  傳回事件工作階段中每一個事件目標的資料列。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|event_session_id|**int**|事件工作階段的識別碼。 不可為 Null。|  
|target_id|**int**|目標的識別碼。 這個識別碼在事件工作階段物件中是唯一的。 不可為 Null。|  
|NAME|**sysname**|事件目標的名稱。 不可為 Null。|  
|封裝|**sysname**|包含此事件目標之事件封裝的名稱。 不可為 Null。|  
|module|**sysname**|包含此事件目標之模組的名稱。 不可為 Null。|  
  
## <a name="permissions"></a>Permissions  
 需要伺服器的 VIEW SERVER STATE 權限。  
  
## <a name="remarks"></a>備註  
 此檢視有下列關聯性基數。  
  
||||  
|-|-|-|  
|來源|若要|關聯性|  
|sys.server_event_session_targets.event_session_id|sys.server_event_sessions.event_session_id|多對一|  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [擴充的事件目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [擴充事件](../../relational-databases/extended-events/extended-events.md)  
  
  
