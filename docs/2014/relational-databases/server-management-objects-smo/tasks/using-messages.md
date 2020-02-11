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
ms.openlocfilehash: 43ff94bf10dee2bda0a61b573b87621fa5d3256b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "72781803"
---
# <a name="using-messages"></a>使用訊息
  在 SMO 中，系統訊息是由屬於 <xref:Microsoft.SqlServer.Management.Smo.SystemMessageCollection> 物件的 `Server` 物件表示。 因為系統訊息無法修改，所以 `SystemMessage` 物件屬性是唯讀的。  
  
 在 SMO 中，使用者定義的訊息是由 <xref:Microsoft.SqlServer.Management.Smo.UserDefinedMessageCollection> 物件以程式設計的方式表示。 現有的使用者定義的訊息可以藉由反覆運算集合而找到。 新的使用者定義訊息則可藉由具現化新的 `UserDefinedMessage` 物件和設定適當的屬性來建立。  
  
## <a name="examples"></a>範例  
 在下列的程式碼範例中，您必須選取用於建立應用程式的程式設計環境、程式設計範本和程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)和[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="finding-a-particular-system-message-in-visual-basic"></a>在 Visual Basic 中尋找特定的系統訊息  
 此程式碼範例示範如何依識別碼辨識系統訊息並加以顯示。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMessages1](SMO How to#SMO_VBMessages1)]  -->  
  
## <a name="finding-a-particular-system-message-in-visual-c"></a>在 Visual C# 中尋找特定的系統訊息  
 此程式碼範例示範如何依識別碼辨識系統訊息並加以顯示。  
  
```csharp
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
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\  
$srv = Get-Item default  
  
#Get the message 14126 in US English and display it  
$msg = $srv.SystemMessages.ItemByIdAndLanguage(14126, "us_english")  
$msg.ID.ToString() + " "+ $msg.Text  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-basic"></a>在 Visual Basic 中加入新的使用者自訂訊息  
 此程式碼範例示範如何建立識別碼大於 50000 的使用者定義訊息。  
  
```vb
Dim mysrv As Server  
mysrv = New Server  
Dim udm As UserDefinedMessage  
udm = New UserDefinedMessage(mysrv, 50003, "us_english", 16, "Test message")  
udm.Create()  
```  
  
## <a name="adding-a-new-user-defined-message-in-visual-c"></a>在 Visual C# 中加入新的使用者自訂訊息  
 此程式碼範例示範如何建立識別碼大於 50000 的使用者定義訊息。  
  
```csharp
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
  
```powershell
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a new message
$udm = New-Object -TypeName Microsoft.SqlServer.Management.SMO.UserDefinedMessage -ArgumentList `  
$srv, 50030, "us_english", 16, "Test message"  
$udm.Create()  
$msg = $srv.UserDefinedMessages.ItemByIdAndLanguage(50030, "us_english");  
$msg  
```  
