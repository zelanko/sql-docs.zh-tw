---
title: 使用訊息 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- messages [SMO]
ms.assetid: 4037a866-4826-4c1f-890c-e7e3658adf13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e67d8818fb20d339c4166f606d15e0f7dbceced
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63015260"
---
# <a name="using-messages"></a>使用訊息
  在 SMO 中，系統訊息是由屬於 `Server` 物件的 <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> 物件表示。 因為系統訊息無法修改，所以 `SystemMessage` 物件屬性是唯讀的。  
  
 在 SMO 中，使用者定義的訊息是由 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> 物件以程式設計的方式表示。 現有的使用者定義的訊息可以藉由反覆運算集合而找到。 新的使用者定義訊息則可藉由具現化新的 `UserDefinedMessage` 物件和設定適當的屬性來建立。  
  
## <a name="examples"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱 < [Visual Studio.NET 中建立 Visual Basic SMO Project](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)並[建立 Visual C&#35; Visual Studio.NET 中的 SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>在 Visual Basic 中尋找特定的系統訊息  
 此程式碼範例示範如何依識別碼辨識系統訊息並加以顯示。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMessages1](SMO How to#SMO_VBMessages1)]  -->  
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>在 Visual C# 中尋找特定的系統訊息  
 此程式碼範例示範如何依識別碼辨識系統訊息並加以顯示。  
  
```  
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
            //Reference an existing system message using the   
            //ItemByIdAndLanguage method.   
            SystemMessage msg = default(SystemMessage);  
            msg = srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
        }  
```  
  
## <a name="finding-a-particular-system-message-in-powershell"></a>在 PowerShell 中尋找特定的系統訊息  
 此程式碼範例示範如何依識別碼辨識系統訊息並加以顯示。  
  
```  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = get-item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>在 Visual Basic 中加入新的使用者自訂訊息  
 此程式碼範例示範如何建立識別碼大於 50000 的使用者定義訊息。  
  
```  
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>在 Visual C# 中加入新的使用者自訂訊息  
 此程式碼範例示範如何建立識別碼大於 50000 的使用者定義訊息。  
  
```  
{  
  
            Server mysrv = new Server();  
  
            UserDefinedMessage udm = new UserDefinedMessage(mysrv, 50030, "us_english",16, "Test message");  
            udm.Create();  
             UserDefinedMessage  msg = mysrv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
            //Display the message ID and text.   
            Console.WriteLine(msg.ID.ToString() + " " + msg.Text);  
  
        }  
```  
  
## <a name="adding-a-new-user-defined-message-in-powershell"></a>在 PowerShell 中加入新的使用者自訂訊息  
 此程式碼範例示範如何建立識別碼大於 50000 的使用者定義訊息。  
  
```  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message  
  
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -argumentlist `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
  
  
