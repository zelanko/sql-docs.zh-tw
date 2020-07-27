---
title: MSMQ 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.msmqconnectionmanager.f1
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a99770eded434ef15966535f082bbd25e07aece7
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923108"
---
# <a name="msmq-connection-manager"></a>MSMQ 連接管理員

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  MSMQ 連接管理員可讓封裝連接到使用 Message Queuing (又稱為 MSMQ) 的訊息佇列。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的「訊息佇列」工作會使用 MSMQ 連線管理員。  
  
 當您將 MSMQ 連線管理員加入封裝時， [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 會建立在執行階段解析為 MSMQ 連接的連線管理員、設定連線管理員屬性，並將連線管理員加入封裝上的 **Connections** 集合。 連線管理員的 **ConnectionManagerType** 屬性會設為 **MSMQ**。  
  
 您可以利用下列方式設定 MSMQ 連接管理員：  
  
-   提供連接字串。  
  
-   提供要連接之訊息佇列的路徑。  
  
 路徑的格式取決於佇列類型，如下表所示。  
  
|佇列類型|範例路徑|  
|----------------|-----------------|  
|公開|\<computer name>\\<佇列名稱\>|  
|Private|\<computer name>\Private$\\<佇列名稱\>|  
  
 您可以使用句號 (.) 代表本機電腦。  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 連接管理員的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請參閱 [MSMQ 連線管理員編輯器](../../integration-services/connection-manager/msmq-connection-manager-editor.md)。  
  
 如需以程式設計方式設定連線管理員的資訊，請參閱 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 和 [以程式設計方式加入連接](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="msmq-connection-manager-editor"></a>MSMQ 連線管理員編輯器
  使用 [MSMQ 連線管理員]  對話方塊，來指定 Message Queuing (又稱為 MSMQ) 訊息佇列的路徑。  
  
 若要深入了解 MSMQ 連線管理員，請參閱＜ [MSMQ Connection Manager](../../integration-services/connection-manager/msmq-connection-manager.md)＞。  
  
> [!NOTE]  
>  MSMQ 連線管理員支援本機的共用和私用佇列，以及遠端的公用佇列。 但不支援遠端私用佇列。 如需使用指令碼工作的解決方案，請參閱＜ [以指令碼工作傳送至遠端私用訊息佇列](../../integration-services/extending-packages-scripting-task-examples/sending-to-a-remote-private-message-queue-with-the-script-task.md)＞。  
  
### <a name="options"></a>選項。  
 **名稱**  
 提供唯一的名稱給工作流程中的 MSMQ 連線管理員。 提供的名稱將顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師內。  
  
 **說明**  
 描述連接管理員。 最佳作法是以其用途描述連接管理員，使封裝可以自我記錄並易於維護。  
  
 **路徑**  
 輸入訊息佇列的完整路徑。 路徑的格式取決於佇列的類型。  
  
|佇列類型|範例路徑|  
|----------------|-----------------|  
|公開|\<computer name>\\<佇列名稱\>|  
|Private|\<computer name>\Private$\\<佇列名稱\>|  
  
 您可以使用 "." 代表本機電腦。  
  
 **Test**  
 在設定 MSMQ 連線管理員之後，請按一下 [測試]  來確認連接已可使用。  
  
## <a name="see-also"></a>另請參閱  
 [訊息佇列工作](../../integration-services/control-flow/message-queue-task.md)   
 [Integration Services &#40;SSIS&#41; 連接](../../integration-services/connection-manager/integration-services-ssis-connections.md)  
  
  
