---
title: 以指令碼工作傳送至遠端私用訊息佇列 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], remote private message queues
- Message Queue task [Integration Services]
- Script task [Integration Services], examples
ms.assetid: 636314fd-d099-45cd-8bb4-f730d0a06739
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8e595c437df054bfff996c864fe687818ea9d467
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/02/2018
ms.locfileid: "48156808"
---
# <a name="sending-to-a-remote-private-message-queue-with-the-script-task"></a>以指令碼工作傳送至遠端私用訊息佇列
  訊息佇列 (又稱為 MSMQ) 能夠讓開發人員容易藉由傳送和接收訊息來與應用程式快速且確實地通訊。 訊息佇列有可能位於本機電腦或是遠端電腦上，而且可能是公用或私用的。 在 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 中，MSMQ 連接管理員與訊息佇列工作不支援傳送到遠端電腦上的私用佇列。 不過，透過使用指令碼工作，就可以很輕鬆地將訊息傳送到遠端私用佇列。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>描述  
 下列範例使用現有的 MSMQ 連線管理員，加上來自 System.Messaging 命名空間的物件與方法，將包含在封裝變數中的文字傳送到遠端私用訊息佇列。 MSMQ 連接管理員的 m:microsoft.sqlserver.dts.managedconnections.msmqconn.acquireconnection （system.object） 方法的呼叫傳回**MessageQueue**物件，其`Send`方法可完成此作業工作。  
  
#### <a name="to-configure-this-script-task-example"></a>設定此指令碼工作範例  
  
1.  使用預設名稱建立 MSMQ 連接管理員。 以下列格式設定有效的遠端私用佇列路徑：  
  
    ```  
    FORMATNAME:DIRECT=OS:<computername>\private$\<queuename>  
    ```  
  
2.  建立[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]名**MessageText**型別的`String`來將訊息文字傳遞至指令碼。 輸入預設訊息做為變數值。  
  
3.  將指令碼工作加入設計介面並編輯它。 在 [指令碼工作編輯器] 的 [指令碼] 索引標籤上，將 `MessageText` 變數加入 **ReadOnlyVariables** 屬性，以便在指令碼中使用此變數。  
  
4.  按一下 [編輯指令碼] 以開啟 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA) 指令碼編輯器。  
  
5.  在指令碼專案中，加入 `System.Messaging` 命名空間的參考。  
  
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
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [訊息佇列工作](../control-flow/message-queue-task.md)  
  
  
