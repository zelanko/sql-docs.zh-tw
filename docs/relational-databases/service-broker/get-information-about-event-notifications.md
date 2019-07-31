---
title: 取得事件通知詳細資訊 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: fefdced57d611d241dbb96b71a0b220139683243
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083836"
---
# <a name="get-information-about-event-notifications"></a>取得事件通知詳細資訊
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  下列目錄檢視可用以查詢事件通知的中繼資料。  
  
 **若要取得非伺服器層級的事件通知資訊**  
  
-   [sys.event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  若要檢視在資料庫層級所建立 **sys.event_notifications** 中任何事件通知的相關中繼資料，您必須至少具有下列權限：資料庫的 CONTROL、ALTER、TAKE OWNERSHIP 或 VIEW DEFINITION 權限、身為事件通知的擁有者，或是具有 ALTER ANY DATABASE EVENT NOTIFICATION 權限。 如果是在特定佇列上建立的事件通知，您必須至少具有下列權限：物件的 CONTROL、ALTER、TAKE OWNERSHIP 或 VIEW DEFINITION 權限、身為事件通知的擁有者，或是具有 ALTER ANY DATABASE EVENT NOTIFICATION 權限。  
  
 **若要取得伺服器層級的事件通知資訊**  
  
-   [sys.server_event_notifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)  
  
> [!NOTE]  
>  您必須至少具有下列權限：伺服器的 CONTROL 或 VIEW ANY DEFINITION 權限、身為事件通知的登入或擁有者，或是具有「改變任何資料庫事件通知」 權限，才能檢視 **sys.server_event_notifications** 中任何事件通知的相關中繼資料。  
  
 **若要取得所有可以引發事件通知的事件資訊**  
  
-   [sys.event_notification_event_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-event-notification-event-types-transact-sql.md)  
  
> [!NOTE]  
>  此目錄檢視不會傳回事件群組。  
  
## <a name="see-also"></a>另請參閱  
 [事件通知](../../relational-databases/service-broker/event-notifications.md)  
  
  
