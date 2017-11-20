---
title: "傳送 HTML 郵件 with the Script Task |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-scripting-task-examples
ms.reviewer: 
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: b5f50a79ca83243ea130c77a0d95ab402ba2d31a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>使用指令碼工作傳送 HTML 郵件訊息
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SendMail 工作只支援純文字格式的郵件訊息。 不過您可以使用指令碼工作與 .NET Framework 的郵件功能，輕鬆地傳送 HTML 郵件訊息。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>Description  
 下列範例會使用**System.Net.Mail**來設定和傳送 HTML 郵件訊息的命名空間。 指令碼、 取得從主旨以及從封裝變數的電子郵件的本文、 使用它們來建立新**MailMessag**e 和設定其**IsBodyHtml**屬性**True**。 然後它會從另一個封裝變數初始化的執行個體中取得 SMTP 伺服器名稱**System.Net.Mail.SmtpClient**，並呼叫其**傳送**傳送 HTML 郵件的方法。 這個範例會封裝在副程式中傳送功能的訊息，副程式本身可在其他指令碼中重複使用。  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>若要不使用 SMTP 連接管理員來設定這個指令碼工作範例  
  
1.  建立名為 `HtmlEmailTo`、`HtmlEmailFrom` 和 `HtmlEmailSubject` 的字串變數，並為有效的測試訊息指派適當的值給它們。  
  
2.  建立名為 `HtmlEmailBody` 的字串變數，並將 HTML 標記的字串指派給它。 例如：  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  建立名為 `HtmlEmailServer` 的字串變數，並指派可用的 SMTP 伺服器名稱，以接受匿名的外寄訊息。  
  
4.  指派至這些變數的全部五個**[readonlyvariables]**新的指令碼工作的屬性。  
  
5.  匯入**System.Net**和**System.Net.Mail**插入程式碼中的命名空間。  
  
 本主題中的範例程式碼會從封裝變數取得 SMTP 伺服器名稱。 不過，您也可以利用 SMTP 連接管理員封裝連接資訊，並從程式碼中的連接管理員擷取伺服器名稱。 SMTP 連接管理員的 <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> 方法會以下列格式傳回字串：  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 您可以使用**String.Split**號 （=），然後擷取第二個引數 （標註 1） 做為伺服器名稱陣列中的方法分為個別在每個分號 （;） 的字串陣列中的這個引數清單，或等於。  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>若要使用 SMTP 連接管理員來設定這個指令碼工作範例  
  
1.  修改指令碼工作，藉由移除先前設定`HtmlEmailServer`變數的清單從**[readonlyvariables]**。  
  
2.  取代用以取得伺服器名稱的程式碼行：  
  
    ```  
    Dim smtpServer As String = _  
      Dts.Variables("HtmlEmailServer").Value.ToString  
    ```  
  
     使用下列這些行：  
  
    ```  
    Dim smtpConnectionString As String = _  
      DirectCast(Dts.Connections("SMTP Connection Manager").AcquireConnection(Dts.Transaction), String)  
    Dim smtpServer As String = _  
      smtpConnectionString.Split(New Char() {"="c, ";"c})(1)  
    ```  
  
## <a name="code"></a>程式碼  
  
```vb  
Public Sub Main()  
  
  Dim htmlMessageTo As String = _  
    Dts.Variables("HtmlEmailTo").Value.ToString  
  Dim htmlMessageFrom As String = _  
    Dts.Variables("HtmlEmailFrom").Value.ToString  
  Dim htmlMessageSubject As String = _  
    Dts.Variables("HtmlEmailSubject").Value.ToString  
  Dim htmlMessageBody As String = _  
    Dts.Variables("HtmlEmailBody").Value.ToString  
  Dim smtpServer As String = _  
    Dts.Variables("HtmlEmailServer").Value.ToString  
  
  SendMailMessage( _  
      htmlMessageTo, htmlMessageFrom, _  
      htmlMessageSubject, htmlMessageBody, _  
      True, smtpServer)  
  
  Dts.TaskResult = ScriptResults.Success  
  
End Sub  
  
Private Sub SendMailMessage( _  
    ByVal SendTo As String, ByVal From As String, _  
    ByVal Subject As String, ByVal Body As String, _  
    ByVal IsBodyHtml As Boolean, ByVal Server As String)  
  
  Dim htmlMessage As MailMessage  
  Dim mySmtpClient As SmtpClient  
  
  htmlMessage = New MailMessage( _  
    SendTo, From, Subject, Body)  
  htmlMessage.IsBodyHtml = IsBodyHtml  
  
  mySmtpClient = New SmtpClient(Server)  
  mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials  
  mySmtpClient.Send(htmlMessage)  
  
End Sub  
```  
  
```csharp  
public void Main()  
        {  
  
            string htmlMessageTo = Dts.Variables["HtmlEmailTo"].Value.ToString();  
            string htmlMessageFrom = Dts.Variables["HtmlEmailFrom"].Value.ToString();  
            string htmlMessageSubject = Dts.Variables["HtmlEmailSubject"].Value.ToString();  
            string htmlMessageBody = Dts.Variables["HtmlEmailBody"].Value.ToString();  
            string smtpServer = Dts.Variables["HtmlEmailServer"].Value.ToString();  
  
            SendMailMessage(htmlMessageTo, htmlMessageFrom, htmlMessageSubject, htmlMessageBody, true, smtpServer);  
  
            Dts.TaskResult = (int)ScriptResults.Success;  
  
        }  
  
        private void SendMailMessage(string SendTo, string From, string Subject, string Body, bool IsBodyHtml, string Server)  
        {  
  
            MailMessage htmlMessage;  
            SmtpClient mySmtpClient;  
  
            htmlMessage = new MailMessage(SendTo, From, Subject, Body);  
            htmlMessage.IsBodyHtml = IsBodyHtml;  
  
            mySmtpClient = new SmtpClient(Server);  
            mySmtpClient.Credentials = CredentialCache.DefaultNetworkCredentials;  
            mySmtpClient.Send(htmlMessage);  
  
        }  
```  
  
## <a name="see-also"></a>另請參閱  
 [傳送郵件工作](../../integration-services/control-flow/send-mail-task.md)  
  
  

