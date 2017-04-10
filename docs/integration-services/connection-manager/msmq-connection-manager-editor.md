---
title: "MSMQ 連線管理員編輯器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.msmqconnectionmanager.f1"
helpviewer_keywords: 
  - "MSMQ 連線管理員編輯器"
ms.assetid: ef842cb4-82da-4550-85fe-9bedbc1e77c7
caps.latest.revision: 29
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 29
---
# MSMQ 連線管理員編輯器
  使用 [MSMQ 連線管理員] 對話方塊，來指定 Message Queuing (又稱為 MSMQ) 訊息佇列的路徑。  
  
 若要深入了解 MSMQ 連線管理員，請參閱＜ [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md)＞。  
  
> [!NOTE]  
>  MSMQ 連線管理員支援本機的共用和私用佇列，以及遠端的公用佇列。 但不支援遠端私用佇列。 如需使用指令碼工作的解決方案，請參閱＜ [Sending to a Remote Private Message Queue with the Script Task](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)＞。  
  
## 選項。  
 **名稱**  
 提供唯一的名稱給工作流程中的 MSMQ 連線管理員。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連線管理員。 最佳作法是以其用途描述連線管理員，使封裝可以自我記錄並易於維護。  
  
 **路徑**  
 輸入訊息佇列的完整路徑。 路徑的格式取決於佇列的類型。  
  
|佇列類型|範例路徑|  
|----------------|-----------------|  
|公用|\<電腦名稱>\\<佇列名稱>\>|  
|Private|\<電腦名稱>\Private$\\<佇列名稱>\>|  
  
 您可以使用 "." 代表本機電腦。  
  
 **測試**  
 在設定 MSMQ 連線管理員之後，請按一下 [測試] 來確認連接已可使用。  
  
## 請參閱＜  
 [Integration Services 錯誤和訊息參考](../../integration-services/integration-services-error-and-message-reference.md)  
  
  