---
title: 使用 Database Mail |Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- e-mail [SMO]
- Database Mail [SMO]
- mail [SMO]
ms.assetid: 7605390f-b485-48cc-8d97-e364a066067b
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: d5d6d7b6d314df4917b804c0b9c9c15bc90c9427
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36132151"
---
# <a name="using-database-mail"></a>使用 Database Mail
  在 SMO 中，Database Mail 子系統是由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 屬性所參考的 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 物件表示。 藉由使用 SMO <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 物件，您可以設定 Database Mail 子系統，並且管理設定檔和郵件帳戶。 SMO<xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail>所屬的物件，`Server`物件，代表郵件帳戶的範圍伺服器層級。  
  
## <a name="examples"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[Visual Studio.NET 中建立 Visual Basic SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[建立 Visual C&#35; SMO Project in Visual Studio](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
 程式使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Database Mail，您必須包含`Imports`陳述式來限定 Mail 命名空間。 將陳述式插入至其他 `Imports` 陳述式之後、在應用程式中的任何宣告之前，例如：  
  
 `Imports Microsoft.SqlServer.Management.Smo`  
  
 `Imports Microsoft.SqlServer.Management.Common`  
  
 `Imports Microsoft.SqlServer.Management.Smo.Mail`  
  
## <a name="creating-a-database-mail-account-by-using-visual-basic"></a>使用 Visual Basic 建立 Database Mail 帳戶  
 此程式碼範例示範如何在 SMO 中建立電子郵件帳戶。 Database Mail 是由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 物件表示，且由 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Server> 屬性參考。 SMO 可用於以程式設計的方式設定 Database Mail，但不能用於傳送或處理已收到的電子郵件。  
  
 VB.NET  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBMail1](SMO How to#SMO_VBMail1)]  -->  
  
## <a name="creating-a-database-mail-account-by-using-visual-c"></a>使用 Visual C# 建立 Database Mail 帳戶  
 此程式碼範例示範如何在 SMO 中建立電子郵件帳戶。 Database Mail 是由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 物件表示，且由 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Server> 屬性參考。 SMO 可用於以程式設計的方式設定 Database Mail，但不能用於傳送或處理已收到的電子郵件。  
  
```csharp  
{  
         //Connect to the local, default instance of SQL Server.  
         Server srv = default(Server);   
           srv = new Server();   
           //Define the Database Mail service with a SqlMail object variable   
           //and reference it using the Server Mail property.   
           SqlMail sm;   
           sm = srv.Mail;   
           //Define and create a mail account by supplying the Database Mail  
           //service, name, description, display name, and email address  
           //arguments in the constructor.   
           MailAccount a = default(MailAccount);   
           a = new MailAccount(sm, "AdventureWorks2012 Administrator", "AdventureWorks2012 Automated Mailer", "Mail account for administrative e-mail.", "dba@Adventure-Works.com");   
           a.Create();    
}  
```  
  
## <a name="creating-a-database-mail-account-by-using-powershell"></a>使用 PowerShell 建立 Database Mail 帳戶  
 此程式碼範例示範如何在 SMO 中建立電子郵件帳戶。 Database Mail 是由 <xref:Microsoft.SqlServer.Management.Smo.Mail.SqlMail> 物件表示，且由 <xref:Microsoft.SqlServer.Management.Smo.Server.Mail%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.Server> 屬性參考。 SMO 可用於以程式設計的方式設定 Database Mail，但不能用於傳送或處理已收到的電子郵件。  
  
 PowerShell  
  
```powershell  
#Connect to the local, default instance of SQL Server.  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Define the Database Mail; reference it using the Server Mail property.  
$sm = $srv.Mail  
  
#Define and create a mail account by supplying the Database Mail service,  
#name, description, display name, and email address arguments in the constructor.  
$a = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Mail.MailAccount -argumentlist $sm, `  
"Adventure Works Administrator", "Adventure Works Automated Mailer",`  
 "Mail account for administrative e-mail.", "dba@Adventure-Works.com"  
$a.Create()  
```  
  
  