---
title: Broker 事件類別目錄 | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Broker event category
- Broker event category [SQL Server]
- event classes [SQL Server], Broker event category
ms.assetid: 470dc93c-0dda-4d89-829b-937738d59b31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9918aca57caaef0dc460e810f5ed5ca2d1106ac3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62663807"
---
# <a name="broker-event-category"></a>Broker 事件類別目錄
  **Broker** 事件類別目錄包含一般的 Service Broker 事件。  
  
## <a name="in-this-section"></a>本節內容  
  
|主題|描述|  
|-----------|-----------------|  
|[Broker:Activation 事件類別](broker-activation-event-class.md)|當佇列監視器啟動一個啟用預存程序時產生的事件。|  
|[Broker:Connection 事件類別](broker-connection-event-class.md)|為報告 Service Broker 所管理之傳輸連接的狀態而產生的事件。|  
|[Broker:Conversation 事件類別](broker-conversation-event-class.md)|為報告交談進度而產生的事件。|  
|[Broker:Conversation Group 事件類別](broker-conversation-group-event-class.md)|資料庫建立或卸除交談群組時產生的事件。|  
|[Broker:Corrupted Message 事件類別](broker-corrupted-message-event-class.md)|產生的事件，用以報告資料庫已接收到損毀的訊息。|  
|[Broker:Forwarded Message Dropped 事件類別](broker-forwarded-message-dropped-event-class.md)|當 SQL Server 卸除已轉送的 Service Broker 訊息時產生的事件。|  
|[Broker:Forwarded Message Sent 事件類別](broker-forwarded-message-sent-event-class.md)|當 SQL Server 轉送 Service Broker 訊息時產生的事件。|  
|[Broker:Message Classify 事件類別](broker-message-classify-event-class.md)|當 Service Broker 決定訊息的路由時產生的事件。|  
|[Broker:Message Drop 事件類別](broker-message-drop-event-class.md)|當 Service Broker 無法保留已收到且應該已傳遞給此執行個體中服務的訊息時產生的事件。|  
|[Broker:Remote Message Ack 事件類別](broker-remote-message-ack-event-class.md)|當 Service Broker 傳送或接收訊息收條時產生的事件。|  
  
 還為 Service Broker 提供了兩個安全性稽核事件。 如需這些事件的詳細資訊，請參閱 [Audit Broker 登入事件類別](audit-broker-login-event-class.md) 和 [Audit Broker 交談事件類別](audit-broker-conversation-event-class.md)。  
  
## <a name="see-also"></a>另請參閱  
 [安全性稽核事件類別目錄](https://docs.microsoft.com/bi-reference/trace-events/security-audit-event-category)  
  
  
