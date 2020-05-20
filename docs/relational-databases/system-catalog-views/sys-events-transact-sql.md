---
title: sys.databases （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.events_TSQL
- sys.events
- events_TSQL
- events
dev_langs:
- TSQL
helpviewer_keywords:
- sys.events catalog view
ms.assetid: f245a97a-80fc-43fb-a6e4-139420c9a47a
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 17c8ab2013a1ad36d298039c5706bd518765dd3b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831945"
---
# <a name="sysevents-transact-sql"></a>sys.events (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  針對引發觸發程序或事件通知的每個事件，各包含一個資料列。 這些事件代表當使用[CREATE trigger](../../t-sql/statements/create-trigger-transact-sql.md)或[create event notification](../../t-sql/statements/create-event-notification-transact-sql.md)建立觸發程式或事件通知時，所指定的事件種類。  
  
|資料行名稱|資料類型|描述|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|觸發程序或事件通知的識別碼。 這個值連同**類型**，可唯一識別資料列。|  
|**type**|**int**|造成觸發程序引發的事件。|  
|**type_desc**|**nvarchar(60)**|造成觸發程序引發之事件的描述。|  
|**is_trigger_event**|**bit**|1 = 觸發程序事件。<br /><br /> 0 = 通知事件。|  
|**event_group_type**|**int**|觸發程序或事件通知建立所在的事件群組，如果未在事件群組上建立則為 null。|  
|**event_group_type_desc**|**nvarchar(60)**|觸發程序或事件通知建立所在之事件群組的描述，如果未在事件群組上建立則為 null。|  
  
## <a name="see-also"></a>另請參閱  
 [&#40;Transact-sql&#41;的物件目錄檢視](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目錄檢視 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
