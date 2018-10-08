---
title: 取得事件通知詳細資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- event notifications [SQL Server], metadata
- status information [SQL Server], event notifications
- metadata [SQL Server], event notifications
ms.assetid: 8bc10867-66d6-4f57-ac32-a6c29f3327cd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f789212398759dc7daf23b1651b27c2051e961ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638076"
---
# <a name="get-information-about-event-notifications"></a>取得事件通知詳細資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下列目錄檢視可用以查詢事件通知的中繼資料。  
  
 **若要取得非伺服器層級的事件通知資訊**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  若要檢視在資料庫層級所建立之 **sys.event_notifications** 中任何事件通知的相關中繼資料，您必須至少具有資料庫的 CONTROL、ALTER、TAKE OWNERSHIP 或 VIEW DEFINITION 權限、身為事件通知的擁有者，或是具有 ALTER ANY DATABASE EVENT NOTIFICATION 權限。 如果是特定佇列上建立的事件通知，您至少必須要有以下權限：物件上的 CONTROL、ALTER、TAKE OWNERSHIP 或 VIEW DEFINITION 權限、身為事件通知的擁有者，或是具備 ALTER ANY DATABASE EVENT NOTIFICATION 權限。  
  
 **若要取得伺服器層級的事件通知資訊**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  您必須至少具有伺服器的 CONTROL 或 VIEW ANY DEFINITION 權限、身為事件通知的登入或擁有者，或是具有 ALTER ANY EVENT NOTIFICATION 權限，才能檢視 **sys.server_event_notifications**中任何事件通知的相關中繼資料。  
  
 **若要取得所有可以引發事件通知的事件資訊**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  此目錄檢視不會傳回事件群組。  
  
## <a name="see-also"></a>另請參閱  
 [事件通知](../../relational-databases/service-broker/event-notifications.md)  
  
  
