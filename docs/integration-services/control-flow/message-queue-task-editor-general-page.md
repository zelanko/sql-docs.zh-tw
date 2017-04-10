---
title: "訊息佇列工作編輯器 (一般頁面) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msgqueuetask.general.f1"
helpviewer_keywords: 
  - "訊息佇列工作編輯器"
ms.assetid: 09368b18-37a5-4321-a173-7cfe5d42d2a2
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# 訊息佇列工作編輯器 (一般頁面)
  使用 **[訊息佇列工作編輯器]** 對話方塊的 **[一般頁面]** ，即可命名和描述訊息佇列工作、指定訊息格式以及指出工作是否傳送或接收訊息。  
  
 若要了解這個工作，請參閱＜ [Message Queue Task](../../integration-services/control-flow/message-queue-task.md)＞。  
  
## 選項。  
 **名稱**  
 為訊息佇列工作提供唯一的名稱。 這個名稱是作為工作圖示中的標籤使用。  
  
> [!NOTE]  
>  工作名稱在封裝內必須是唯一的。  
  
 **說明**  
 輸入訊息佇列工作的描述。  
  
 **Use2000Format**  
 指示是否使用 Message Queuing (又稱為 MSMQ) 的 2000 格式。 預設值為 **False**。  
  
 **MSMQConnection**  
 選取現有的 MSMQ 連線管理員，或按一下 [\<新增連線...>] 建立新的連線管理員。  
  
 **相關主題**：[MSMQ 連線管理員](../../integration-services/connection-manager/msmq-connection-manager.md)、[MSMQ 連線管理員編輯器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)  
  
 **訊息**  
 指定訊息佇列工作是否傳送或接收訊息。 如果選取 **[傳送訊息]**，對話方塊的左窗格會列出 [傳送] 頁面，如果選取 **[接收訊息]**，則會列出 [接收] 頁面。 依預設，此值設定為 **[傳送訊息]**。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)   
 [訊息佇列工作編輯器 &#40;接收頁面&#41;](../../integration-services/control-flow/message-queue-task-editor-receive-page.md)   
 [訊息佇列工作編輯器 &#40;傳送頁面&#41;](../../integration-services/control-flow/message-queue-task-editor-send-page.md)   
 [運算式頁面](../../integration-services/expressions/expressions-page.md)  
  
  