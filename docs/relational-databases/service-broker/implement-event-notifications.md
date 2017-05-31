---
title: "實作事件通知 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- event notifications [SQL Server], target service
- target service [SQL Server]
- event notifications [SQL Server], creating
ms.assetid: 29ac8f68-a28a-4a77-b67b-a8663001308c
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: eac9804c15bfcafbb5581875258d4499df130db9
ms.contentlocale: zh-tw
ms.lasthandoff: 04/11/2017

---
# <a name="implement-event-notifications"></a>實作事件通知
  若要實作事件通知，您必須先建立目標服務來接收事件通知，然後建立事件通知。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 對話安全性。 對話安全性必須根據完整安全性模型，以手動方式加以設定。  
  
## <a name="creating-the-target-service"></a>建立目標服務  
 您不必建立 [!INCLUDE[ssSB](../../includes/sssb-md.md)]起始服務，因為 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 包括下列特定訊息類型和事件通知的合約：  
  
```  
http://schemas.microsoft.com/SQL/Notifications/PostEventNotification  
```  
  
 接收事件通知的目標服務必須遵照這項預先存在的合約。  
  
 **若要建立目標服務**：  
  
1.  建立要接收訊息的佇列。  
  
    > [!NOTE]  
    >  佇列會接收下列訊息類型： `http://schemas.microsoft.com/SQL/Notifications/QueryNotification`。  
  
2.  在參考事件通知合約的佇列上建立服務。  
  
3.  在服務上建立路由，以定義要 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 將該服務的訊息傳送到哪一個位址。 如果事件通知是以相同資料庫中的服務為目標，請指定 `ADDRESS = 'LOCAL'`。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 路由會判斷要接收通知訊息的服務。 如果事件通知是以遠端伺服器的服務為目標，則來源伺服器和目標伺服器上都必須要定義路由，以確保可以進行雙向通訊。  
  
 下列範例會建立佇列、佇列上的服務及服務上的路由，以處理來自事件通知合約的訊息：  
  
```  
CREATE QUEUE NotifyQueue ;  
GO  
CREATE SERVICE NotifyService  
ON QUEUE NotifyQueue  
(  
[http://schemas.microsoft.com/SQL/Notifications/PostEventNotification]  
);  
GO  
CREATE ROUTE NotifyRoute  
WITH SERVICE_NAME = 'NotifyService',  
ADDRESS = 'LOCAL';  
GO  
```  
  
## <a name="creating-the-event-notification"></a>建立事件通知  
 事件通知是使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE EVENT NOTIFICATION 陳述式建立，並使用 DROP EVENT NOTIFICATION STATEMENT 卸除。 若要修改事件通知，您必須先卸除再重新建立事件通知。  
  
 下列範例會建立事件通知 `CreateDatabaseNotification`。 當伺服器上發生任何 `CREATE_DATABASE` 事件時，這個通知會傳送此訊息給先前建立的 `NotifyService` 服務。  
  
```  
CREATE EVENT NOTIFICATION CreateDatabaseNotification  
ON SERVER  
FOR CREATE_DATABASE  
TO SERVICE 'NotifyService', '8140a771-3c4b-4479-8ac0-81008ab17984' ;  
```  
  
> [!CAUTION]  
>  事件通知以不同事件來辨識 CREATE_SCHEMA 事件和 CREATE SCHEMA 陳述式的 <schema_element> 定義。 例如，對 CREATE_SCHEMA 和 CREATE_TABLE 事件建立事件通知，且您執行下列批次。  
>   
>  `CREATE SCHEMA s`  
>   
>  `CREATE TABLE t1 (col1 int)`  
>   
>  在此案例中，事件通知引發了兩次：一次是在 CREATE_SCHEMA 事件發生時，一次只在 CREATE_TABLE 事件發生時。 我們建議您避免在 CREATE_SCHEMA 事件和任何對應 CREATE SCHEMA  定義的 <schema_element> 文字上建立事件通知，或在應用程式中建立邏輯，以避免擷取不想要的事件資料。  
  
 **若要建立事件通知**  
  
-   [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
 **若要卸除事件通知**  
  
-   [DROP EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-notification-transact-sql.md)  
  
## <a name="see-also"></a>另請參閱  
 [取得事件通知詳細資訊](../../relational-databases/service-broker/get-information-about-event-notifications.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
