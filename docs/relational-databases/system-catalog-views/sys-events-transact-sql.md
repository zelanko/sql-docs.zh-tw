---
title: "sys.events (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs: TSQL
helpviewer_keywords: sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
caps.latest.revision: "38"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b975acfb9ee4134eb768055bd9a012678681dc4b
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/21/2017
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對引發觸發程序或事件通知的每個事件，各包含一個資料列。 這些事件代表觸發程序或事件通知以建立時所指定的事件類型[CREATE TRIGGER](../../t-sql/statements/create-trigger-transact-sql.md)或[CREATE EVENT NOTIFICATION](../../t-sql/statements/create-event-notification-transact-sql.md)。  
  
||  
|-|  
|**適用於**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 至 [目前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658))、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。|  
  
|資料行名稱|資料類型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|觸發程序或事件通知的識別碼。 此值搭配**類型**，以唯一識別資料列。|  
|**型別**|**int**|造成觸發程序引發的事件。|  
|**type_desc**|**nvarchar （60)**|造成觸發程序引發之事件的描述。|  
|**is_trigger_event**|**bit**|1 = 觸發程序事件。<br /><br /> 0 = 通知事件。|  
|**type_desc**|**int**|觸發程序或事件通知建立所在的事件群組，如果未在事件群組上建立則為 null。|  
|**event_group_type**|**nvarchar （60)**|觸發程序或事件通知建立所在之事件群組的描述，如果未在事件群組上建立則為 null。|  
  
## <a name="see-also"></a>請參閱＜  
 [物件目錄檢視 &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
