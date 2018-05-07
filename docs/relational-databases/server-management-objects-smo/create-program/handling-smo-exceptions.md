---
title: 處理 SMO 例外狀況 |Microsoft 文件
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 85d0705776117d09584ea27d1d0b6ef68ede1b9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="handling-smo-exceptions"></a>處理 SMO 例外狀況
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  在 Managed 程式碼中發生錯誤時會擲回例外狀況。 SMO 方法和屬性不會在傳回值中報告成功或失敗， 而是由例外處理常式攔截和處理例外狀況。  
  
 SMO 中有不同的例外狀況類別。 有關例外狀況的資訊可以擷取自例外狀況屬性，例如 **Message** 屬性，此屬性會提供有關例外狀況的文字訊息。  
  
 例外狀況處理陳述式會依程式語言而定。 例如，在[!INCLUDE[msCoName](../../../includes/msconame-md.md)]Visual Basic 中是**攔截**陳述式。  
  
## <a name="inner-exceptions"></a>內部例外狀況  
 例外狀況可以是一般或特定的。 一般例外狀況包含一組特定的例外狀況。 可以用數個 **Catch** 陳述式來處理預期的錯誤，而讓剩餘的錯誤通過以留待一般例外狀況處理程式碼處理。 例外狀況通常是以串聯式序列發生。 SMO 例外狀況經常是由 SQL 例外狀況所導致。 偵測此種狀況的方法是連續使用 **InnerException** 屬性來判斷導致最後之最上層例外狀況的原始例外狀況。  
  
> [!NOTE]  
>  **SQLException**例外狀況會在宣告**System.Data.SqlClient**命名空間。  
  
 ![此圖顯示的層級 excp](../../../relational-databases/server-management-objects-smo/create-program/media/exception-flow.gif "的圖表，顯示的層級 excp")  
  
 此圖顯示應用程式層級中的例外狀況流程。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[建立 Visual C&#35; SMO Project in Visual Studio](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。
  
## <a name="catching-an-exception-in-visual-basic"></a>在 Visual Basic 中攔截例外狀況  
 這個程式碼範例示範如何使用**再試一次...Catch...最後**[!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]陳述式來攔截 SMO 例外狀況。 所有的 SMO 例外狀況都具有 SmoException 類型，而且會列於 SMO 參考中。 內部例外狀況的順序會顯示，以指出錯誤的根源所在。 如需詳細資訊，請參閱 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET 文件集。  
  
```VBNET
'This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace is included.
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.
'Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.
Dim op As [Operator]
op = New [Operator](srv.JobServer, "Test_Operator")
op.Create()
'Start exception handling.
Try
    'Create the operator again to cause an SMO exception.
    Dim opx As OperatorCategory
    opx = New OperatorCategory(srv.JobServer, "Test_Operator")
    opx.Create()
    'Catch the SMO exception
Catch smoex As SmoException
    Console.WriteLine("This is an SMO Exception")
    'Display the SMO exception message.
    Console.WriteLine(smoex.Message)
    'Display the sequence of non-SMO exceptions that caused the SMO exception.
    Dim ex As Exception
    ex = smoex.InnerException
    Do While ex.InnerException IsNot (Nothing)
        Console.WriteLine(ex.InnerException.Message)
        ex = ex.InnerException
    Loop
    'Catch other non-SMO exceptions.
Catch ex As Exception
    Console.WriteLine("This is not an SMO exception.")
End Try
``` 
  
## <a name="catching-an-exception-in-visual-c"></a>在 Visual C# 中攔截例外狀況  
 此程式碼範例示範如何使用 **Try…Catch…Finally** Visual C# 陳述式來攔截 SMO 例外狀況。 所有的 SMO 例外狀況都具有 SmoException 類型，而且會列於 SMO 參考中。 內部例外狀況的順序會顯示，以指出錯誤的根源所在。 如需詳細資訊，請參閱 Visual C# 文件集。  
  
```csharp  
{   
//This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace to be included.   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.   
//Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.   
op = new Operator(srv.JobServer, "Test_Operator");   
op.Create();   
//Start exception handling.   
try {   
    //Create the operator again to cause an SMO exception.   
    OperatorCategory opx;   
    opx = new OperatorCategory(srv.JobServer, "Test_Operator");   
    opx.Create();   
}   
//Catch the SMO exception   
catch (SmoException smoex) {   
    Console.WriteLine("This is an SMO Exception");   
   //Display the SMO exception message.   
   Console.WriteLine(smoex.Message);   
   //Display the sequence of non-SMO exceptions that caused the SMO exception.   
   Exception ex;   
   ex = smoex.InnerException;   
   while (!object.ReferenceEquals(ex.InnerException, (null))) {   
      Console.WriteLine(ex.InnerException.Message);   
      ex = ex.InnerException;   
    }   
    }   
   //Catch other non-SMO exceptions.   
   catch (Exception ex) {   
      Console.WriteLine("This is not an SMO exception.");   
}   
}  
```  
  
  
