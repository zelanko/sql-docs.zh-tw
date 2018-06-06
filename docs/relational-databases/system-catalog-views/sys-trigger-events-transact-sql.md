---
title: sys.trigger_events (TRANSACT-SQL) |Microsoft 文件
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trigger_events_TSQL
- trigger_events
- sys.trigger_events
- sys.trigger_events_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.trigger_events catalog view
ms.assetid: 92540447-131c-491c-b033-c064c7d950e1
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 73010cbaae5461a9274b1d6f0d90f6276ff7c976
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2018
---
# <a name="systriggerevents-transact-sql"></a>sys.trigger_events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對引發觸發程序的每個事件，各包含一個資料列。  
  
> [!NOTE]  
>  **sys.trigger_events**不適用於事件通知。  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**\<資料行繼承自 sys.events >**|不適用|繼承**object_id**，**類型**， **type_desc**中的資料行[sys.events](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)。|  
|**is_first**|**bit**|觸發程序被標示為這個事件要引發的第一個觸發程序。|  
|**is_last**|**bit**|觸發程序被標示為這個事件要引發的最後一個觸發程序。|  
|**type_desc**|**int**|觸發程序建立所在的事件群組，如果未在事件群組上建立則為 null。|  
|**event_group_type**|**nvarchar(60)**|觸發程序建立所在之事件群組的描述，如果未在事件群組上建立則為 null。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 如需相關資訊，請參閱 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另請參閱  
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [物件目錄檢視&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
