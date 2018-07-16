---
title: MSMQ 連線管理員 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], message queues
- connection managers [Integration Services], MSMQ
- MSMQ connection manager
- message queue connections [Integration Services]
ms.assetid: a86900e2-450e-479f-b207-e1b02361d395
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f9be09df9ab705d45dfdeee7caebfeb556a7a669
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306118"
---
# <a name="msmq-connection-manager"></a>MSMQ 連接管理員
  MSMQ 連接管理員可讓封裝連接到使用 Message Queuing (又稱為 MSMQ) 的訊息佇列。  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含的「訊息佇列」工作使用 MSMQ 連線管理員。  
  
 當您將 MSMQ 連接管理員加入封裝時，[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]建立連接管理員會解析為 MSMQ 連接，在執行階段、 設定連接管理員屬性，並將連接管理員加入`Connections`集合封裝。 `ConnectionManagerType`連接管理員屬性設定為`MSMQ`。  
  
 您可以利用下列方式設定 MSMQ 連接管理員：  
  
-   提供連接字串。  
  
-   提供要連接之訊息佇列的路徑。  
  
 路徑的格式取決於佇列類型，如下表所示。  
  
|佇列類型|範例路徑|  
|----------------|-----------------|  
|公用|\<電腦名稱>\\<佇列名稱\>|  
|Private|\<電腦名稱>\Private$\\<佇列名稱\>|  
  
 您可以使用句號 (.) 代表本機電腦。  
  
## <a name="configuration-of-the-msmq-connection-manager"></a>MSMQ 連接管理員的組態  
 您可以透過 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師或以程式設計方式設定屬性。  
  
 如需可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師中設定之屬性的詳細資訊，請參閱 [MSMQ 連線管理員編輯器](../msmq-connection-manager-editor.md)。  
  
 以程式設計方式設定連接管理員的相關資訊，請參閱<xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>並[連線以程式設計方式加入](../building-packages-programmatically/adding-connections-programmatically.md)。  
  
## <a name="see-also"></a>另請參閱  
 [訊息佇列工作](../control-flow/message-queue-task.md)   
 [Integration Services &#40;SSIS&#41;連線](integration-services-ssis-connections.md)  
  
  
