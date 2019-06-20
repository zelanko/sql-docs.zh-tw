---
title: 取得事件通知詳細資訊 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9786faaf44724b1a2452bd5304b63deb2c9ea54e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63015310"
---
# <a name="get-information-about-event-notifications"></a>取得事件通知詳細資訊
  下列目錄檢視可用以查詢事件通知的中繼資料。  
  
 **若要取得非伺服器層級的事件通知資訊**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-event-notifications-transact-sql)  
  
> [!NOTE]  
>  若要檢視中的任何事件通知的中繼資料**sys.event_notifications**建立在資料庫層級，至少您必須擁有下列：控制、 ALTER、 TAKE OWNERSHIP 或 VIEW DEFINITION 權限的資料庫、 是事件通知的擁有者或具有 ALTER ANY DATABASE EVENT NOTIFICATION 權限。 針對特定的佇列上建立的事件通知，至少您必須具備下列：控制、 ALTER、 TAKE OWNERSHIP 或 VIEW DEFINITION 權限的物件、 是事件通知的擁有者或具有 ALTER ANY DATABASE EVENT NOTIFICATION 權限。  
  
 **若要取得伺服器層級的事件通知資訊**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql)  
  
> [!NOTE]  
>  最小值，您必須具備下列項目：控制或檢視伺服器上的 ANY DEFINITION 權限、 的登入或事件通知的擁有者或具有 ALTER ANY EVENT NOTIFICATION 權限檢視中的任何事件通知的中繼資料**sys.server_event_notifications**.  
  
 **若要取得所有可以引發事件通知的事件資訊**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql)  
  
> [!NOTE]  
>  此目錄檢視不會傳回事件群組。  
  
## <a name="see-also"></a>另請參閱  
 [事件通知](event-notifications.md)  
  
  
