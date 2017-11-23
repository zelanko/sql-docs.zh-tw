---
title: "sys.server_events (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- server_events_TSQL
- sys.server_events_TSQL
- server_events
- sys.server_events
dev_langs: TSQL
helpviewer_keywords: sys.server_events catalog view
ms.assetid: 996f6c9b-6426-4847-95d9-6b77541422be
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bbacdd3b1f3943906be711c64f2368c4a5e7a779
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysserverevents-transact-sql"></a>sys.server_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  針對伺服器層級事件通知或伺服器層級 DDL 觸發程序所引發的每個事件，各包含一個資料列。 資料行**object_id**和**類型**唯一識別伺服器事件。  

  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|引發之伺服器層級事件通知或伺服器層級 DDL 觸發程序的識別碼。|  
|**型別**|**int**|導致事件通知或 DDL 觸發程序引發的事件類型。|  
|**type_desc**|**nvarchar （60)**|導致 DDL 觸發程序或事件通知引發的事件描述。|  
|**type_desc**|**int**|觸發程序或事件通知建立所在的事件群組，如果未在事件群組上建立則為 null。|  
|**event_group_type**|**nvarchar （60)**|觸發程序或事件通知建立所在之事件群組的描述，如果未在事件群組上建立則為 null。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>請參閱＜  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
