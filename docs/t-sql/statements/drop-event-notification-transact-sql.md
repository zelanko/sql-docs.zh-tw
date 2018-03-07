---
title: "卸除事件通知 (TRANSACT-SQL) |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP EVENT NOTIFICATION
- DROP_EVENT_NOTIFICATION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- event notifications [SQL Server], removing
- deleting event notifications
- dropping event notifications
- DROP EVENT NOTIFICATION statement
- removing event notifications
ms.assetid: 0ffd8f47-4ea3-4238-9e73-c318df710cf7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b2ecaff48f54ce76fe0d193eda5406df1bc574e7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/02/2018
---
# <a name="drop-event-notification-transact-sql"></a>DROP EVENT NOTIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  從目前資料庫移除事件通知觸發程序。  
  
 ![主題連結圖示](../../database-engine/configure-windows/media/topic-link.gif "主題連結圖示") [Transact-SQL 語法慣例](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>語法  
  
```  
  
DROP EVENT NOTIFICATION notification_name [ ,...n ]  
ON { SERVER | DATABASE | QUEUE queue_name }  
[ ; ]  
```  
  
## <a name="arguments"></a>引數  
 *notification_name*  
 這是要移除之事件通知的名稱。 您可以指定多個事件通知。 若要查看目前建立的事件通知清單，請使用[sys.event_notifications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md).  
  
 SERVER  
 指出將事件通知範圍套用在目前伺服器上。 如果建立事件通知時指定了 SERVER，就必須指定 SERVER。  
  
 DATABASE  
 指出將事件通知範圍套用在目前資料庫上。 如果建立事件通知時指定了 DATABASE，就必須指定 DATABASE。  
  
 佇列*queue_name*  
 表示事件通知範圍套用到所指定的佇列*queue_name*。 如果建立事件通知時指定了 QUEUE，就必須指定 QUEUE。 *queue_name*是佇列的名稱，而且也必須指定。  
  
## <a name="remarks"></a>備註  
 如果在交易內引發事件通知，且在相同交易內卸除它，就會傳送事件通知執行個體，之後，再卸除事件通知。  
  
## <a name="permissions"></a>Permissions  
 若要卸除資料庫層級範圍的事件通知，使用者至少必須是事件通知的擁有者，或有目前資料庫的 ALTER ANY DATABASE EVENT NOTIFICATION 權限。  
  
 若要卸除伺服器層級範圍的事件通知，使用者至少必須是事件通知的擁有者，或有伺服器中的 ALTER ANY EVENT NOTIFICATION 權限。  
  
 若要卸除特定佇列中的事件通知，使用者至少必須是事件通知的擁有者，或有父佇列的 ALTER 權限。  
  
## <a name="examples"></a>範例  
 下列範例建立資料庫範圍的事件通知，然後卸除它：  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE  
FOR ALTER_TABLE  
TO SERVICE 'NotifyService',  
    '8140a771-3c4b-4479-8ac0-81008ab17984';  
GO  
DROP EVENT NOTIFICATION NotifyALTER_T1  
ON DATABASE;  
```  
  
## <a name="see-also"></a>請參閱  
 [建立事件通知 &#40;TRANSACT-SQL &#41;](../../t-sql/statements/create-event-notification-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.event_notifications &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)   
 [sys.events &#40;TRANSACT-SQL &#41;](../../relational-databases/system-catalog-views/sys-events-transact-sql.md)  
  
  
