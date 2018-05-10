---
title: 以指令碼工作傳送至遠端私用訊息佇列 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: extending-packages-scripting-task-examples
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2ca6b64970565612f18b3dcb21258d8345bd2485
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>以指令碼工作傳送至遠端私用訊息佇列
  訊息佇列 (又稱為 MSMQ) 能夠讓開發人員容易藉由傳送和接收訊息來與應用程式快速且確實地通訊。 訊息佇列有可能位於本機電腦或是遠端電腦上，而且可能是公用或私用的。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，MSMQ 連接管理員與訊息佇列工作不支援傳送到遠端電腦上的私用佇列。 不過，透過使用指令碼工作，就可以很輕鬆地將訊息傳送到遠端私用佇列。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>描述  
 下列範例使用現有的 MSMQ 連線管理員，加上來自 System.Messaging 命名空間的物件與方法，將包含在封裝變數中的文字傳送到遠端私用訊息佇列。 呼叫 MSMQ 連線管理員的 M:Microsoft.SqlServer.Dts.ManagedConnections.MSMQConn.AcquireConnection(System.Object) 方法會傳回 **MessageQueue** 物件，其 **Send** 方法會完成此項工作。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
1.  使用預設名稱建立 MSMQ 連接管理員。 以下列格式設定有效的遠端私用佇列路徑：  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  建立類型為 **String** 且名為 **MessageText** 的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 變數，以將訊息文字傳遞至指令碼中。 輸入預設訊息做為變數值。  
  
3.  將指令碼工作加入設計介面並編輯它。 在 [指令碼工作編輯器] 的 [指令碼] 索引標籤上，將 `MessageText` 變數加入 **ReadOnlyVariables** 屬性，以便在指令碼中使用此變數。  
  
4.  按一下 [編輯指令碼] 以開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 指令碼編輯器。  
  
5.  在指令碼專案中，加入 **System.Messaging** 命名空間的參考。  
  
6.  以下列小節中的程式碼取代指令碼視窗中的內容。  
  
## <a name="code"></a>程式碼  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Messaging  
  
Public Class ScriptMain  
  
    Public Sub Main()  
  
        Dim remotePrivateQueue As MessageQueue  
        Dim messageText As String  
  
        remotePrivateQueue = _  
            DirectCast(Dts.Connections("Message Queue Connection Manager").AcquireConnection(Dts.Transaction), _  
            MessageQueue)  
        messageText = DirectCast(Dts.Variables("MessageText").Value, String)  
        remotePrivateQueue.Send(messageText)  
  
        Dts.TaskResult = ScriptResults.Success  
  
    End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Messaging;  
  
public class ScriptMain  
{  
  
    public void Main()  
        {  
  
            MessageQueue remotePrivateQueue = new MessageQueue();  
            string messageText;  
  
            remotePrivateQueue = (MessageQueue)(Dts.Connections["Message Queue Connection Manager"].AcquireConnection(Dts.Transaction) as MessageQueue);  
            messageText = (string)(Dts.Variables["MessageText"].Value);  
            remotePrivateQueue.Send(messageText);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [訊息佇列工作](../../integration-services/control-flow/message-queue-task.md)  
  
  
