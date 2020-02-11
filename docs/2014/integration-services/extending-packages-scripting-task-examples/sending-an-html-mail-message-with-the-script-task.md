---
title: 以指令碼工作傳送 HTML 郵件訊息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Send Mail task [Integration Services]
- Script task [Integration Services], examples
- Script task [Integration Services], HTML mail message
ms.assetid: dd2b1eef-b04f-4946-87ab-7bc56bb525ce
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 254f1fcb701fd11b22e35def915b09b537c4b33a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "62894987"
---
# <a name="sending-an-html-mail-message-with-the-script-task"></a>使用指令碼工作傳送 HTML 郵件訊息
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] SendMail 工作只支援純文字格式的郵件訊息。 不過您可以使用指令碼工作與 .NET Framework 的郵件功能，輕鬆地傳送 HTML 郵件訊息。  
  
> [!NOTE]  
>  如果您想要建立可更輕鬆地在多個封裝之間重複使用的工作，請考慮使用此指令碼工作範例中的程式碼做為自訂工作的起點。 如需詳細資訊，請參閱 [開發自訂工作](../extending-packages-custom-objects/task/developing-a-custom-task.md)。  
  
## <a name="description"></a>描述  
 下列範例使用 `System.Net.Mail` 命名空間來設定和傳送 HTML 郵件訊息。 指令碼會從封裝變數取得電子郵件的收件者、寄件者、主旨以及本文、使用它們來建立新的 `MailMessag`e 並將其 `IsBodyHtml` 屬性設定為 `True`。 然後它會從其他封裝變數取得 SMTP 伺服器名稱、初始化 `System.Net.Mail.SmtpClient` 的執行個體，然後呼叫其 `Send` 方法以傳送 HTML 訊息。 這個範例會封裝在副程式中傳送功能的訊息，副程式本身可在其他指令碼中重複使用。  
  
#### <a name="to-configure-this-script-task-example-without-an-smtp-connection-manager"></a>若要不使用 SMTP 連接管理員來設定這個指令碼工作範例  
  
1.  建立名為 `HtmlEmailTo`、`HtmlEmailFrom` 和 `HtmlEmailSubject` 的字串變數，並為有效的測試訊息指派適當的值給它們。  
  
2.  建立名為 `HtmlEmailBody` 的字串變數，並將 HTML 標記的字串指派給它。 例如：  
  
    ```  
    <html><body><h1>Testing</h1><p>This is a <b>test</b> message.</p></body></html>  
    ```  
  
3.  建立名為 `HtmlEmailServer` 的字串變數，並指派可用的 SMTP 伺服器名稱，以接受匿名的外寄訊息。  
  
4.  將這五個變數全部都指派到新指令碼工作的 **ReadOnlyVariables** 屬性。  
  
5.  將 `System.Net` 與 `System.Net.Mail` 命名空間匯入您的程式碼。  
  
 本主題中的範例程式碼會從封裝變數取得 SMTP 伺服器名稱。 不過，您也可以利用 SMTP 連接管理員封裝連接資訊，並從程式碼中的連接管理員擷取伺服器名稱。 SMTP 連接管理員的 <xref:Microsoft.SqlServer.Dts.ManagedConnections.SMTPConn.AcquireConnection%2A> 方法會以下列格式傳回字串：  
  
 `SmtpServer=smtphost;UseWindowsAuthentication=False;EnableSsl=False;`  
  
 您可以使用 `String.Split` 方法，在每個分號 (;) 或是等號 (=) 將此引數清單分隔成個別字串的陣列，然後從陣列中擷取第二個引數 (標註 1) 做為伺服器名稱。  
  
#### <a name="to-configure-this-script-task-example-with-an-smtp-connection-manager"></a>若要使用 SMTP 連接管理員來設定這個指令碼工作範例  
  
1.  透過從 `HtmlEmailServer`ReadOnlyVariables**清單中移除** 變數，以修改之前設定的指令碼工作。  
  
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
  
![Integration Services 圖示（小型）](../media/dts-16.gif "Integration Services 圖示 (小)")**與 Integration Services 保持最**新狀態  <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [傳送電子郵件工作](../control-flow/send-mail-task.md)  
  
  
