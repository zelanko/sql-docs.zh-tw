---
title: 使用 CLR 整合的消費者入門 |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: quickstart
dev_langs:
- TSQL
- VB
- CSharp
helpviewer_keywords:
- database objects [CLR integration]
- namespaces [CLR integration]
- database objects [CLR integration], about CLR integration
- stored procedures [CLR integration]
- common language runtime [SQL Server], about CLR integration
- building database objects [CLR integration], about CLR integration
- common language runtime [SQL Server], stored procedures
- common language runtime [SQL Server], namespaces
- Hello World example [CLR integration]
- library [CLR integration]
ms.assetid: c73e628a-f54a-411a-bfe3-6dae519316cc
author: rothja
ms.author: jroth
ms.openlocfilehash: c71af732f9d4097904c38b6fff019dc86f02a6f0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "76761925"
---
# <a name="getting-started-with-clr-integration"></a>CLR 整合使用者入門

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本主題提供使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]與 .NET Framework common language runtime （CLR）整合來編譯資料庫物件所需之命名空間和程式庫的總覽。 此外，本主題還會為您示範如何撰寫、編譯及執行以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# 所撰寫的簡單 CLR 預存程序。  
  
## <a name="required-namespaces"></a>必要命名空間  

開發基本 CLR 資料庫物件所需的元件會隨一起[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]安裝。 CLR 整合功能會在稱為 system.data.dll (.NET Framework 的一部分) 的組件中公開。 此組件可以在全域組件快取 (GAC) 及 .NET Framework 目錄中找到。 命令列工具及 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio 通常會自動加入此組件的參考，因此不需要手動加入。  
  
system.data.dll 組件包含下列編譯 CLR 資料庫物件所需的命名空間：  
  
- `System.Data`  
- `System.Data.Sql`  
- `Microsoft.SqlServer.Server`  
- `System.Data.SqlTypes`  

> [!TIP]
> 支援在 Linux 上載入 CLR 資料庫物件，但必須以 .NET Framework 建立（SQL Server CLR 整合不支援 .NET Core）。 此外，Linux 上不支援具有 EXTERNAL_ACCESS 或 UNSAFE 許可權集合的 CLR 元件。

## <a name="writing-a-simple-hello-world-stored-procedure"></a>撰寫簡單的 "Hello World" 預存程序  

將下列 Visual C# 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic 程式碼複製並貼至文字編輯器中，然後將其儲存在名為 "helloworld.cs" 或 "helloworld.vb" 的檔案中。  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.SqlServer.Server;  
using System.Data.SqlTypes;  
  
public class HelloWorldProc  
{  
    [Microsoft.SqlServer.Server.SqlProcedure]  
    public static void HelloWorld(out string text)  
    {  
        SqlContext.Pipe.Send("Hello world!" + Environment.NewLine);  
        text = "Hello world!";  
    }  
}  
```  
  
```vb  
Imports System  
Imports System.Data  
Imports Microsoft.SqlServer.Server  
Imports System.Data.SqlTypes  
Imports System.Runtime.InteropServices  
  
Public Class HelloWorldProc  
    \<Microsoft.SqlServer.Server.SqlProcedure> _   
    Public Shared  Sub HelloWorld(\<Out()> ByRef text as String)  
        SqlContext.Pipe.Send("Hello world!" & Environment.NewLine)  
        text = "Hello world!"  
    End Sub  
End Class  
  
```  
  
此簡單的程式包含公用類別上的單一靜態方法。 這個方法會使用兩個新的類別**[SqlCoNtext](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlcontext.aspx)** 和**[SqlPipe](https://msdn.microsoft.com/library/microsoft.sqlserver.server.sqlpipe.aspx)**，來建立 managed 資料庫物件以輸出簡單的文字訊息。 此方法也會將字串 "Hello world!" 指派 為 out 參數的值。 此方法可以宣告為 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的預存程序，然後以與 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 預存程序相同的方法執行。  
  
將此程式編譯為程式庫，並將[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]其載入，並以預存程式的形式執行。  
  
## <a name="compile-the-hello-world-stored-procedure"></a>編譯 "Hello World" 預存程式  

依預設，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 會安裝 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework 轉散佈檔案。 這些檔案包括 csc.exe、vbc.exe 及 Visual C# 與 Visual Basic 程式的命令列編譯器。 若要編譯此範例，您必須修改路徑變數，使其指向包含 csc.exe 或 vbc.exe 的目錄。 以下為 .NET Framework 的預設安裝路徑。  
  
`C:\Windows\Microsoft.NET\Framework\(version)`  
  
Version 包含已安裝之 .NET Framework 可轉散發套件的版本號碼。 例如：  
  
`C:\Windows\Microsoft.NET\Framework\v4.6.1`

將 .NET Framework 目錄加入路徑後，您就可以使用下列命令將範例預存程序編譯為組件。 **/Target**選項可讓您將它編譯成元件。  
  
若為 Visual C# 來源檔案：  
  
`csc /target:library helloworld.cs`  
  
 若為 Visual Basic 來源檔案：  
  
`vbc /target:library helloworld.vb`  
  
這些命令會啟動 Visual C# 或 Visual Basic 編譯器，並使用 /target 選項來指定要建立程式庫 DLL。  
  
## <a name="loading-and-running-the-hello-world-stored-procedure-in-sql-server"></a>在 SQL Server 中載入並執行 "Hello World" 預存程序  

成功編譯範例程序後，您就可以在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中對其進行測試。 若要這樣做，請連接至適合的測試資料庫 (例如 AdventureWorks 範例資料庫)，然後開啟 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 並建立新查詢。  
  
在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，執行 Common Language Runtime (CLR) 程式碼的功能預設為 OFF。 您可以使用**sp_configure**系統預存程式來啟用 CLR 程式碼。 如需詳細資訊，請參閱 [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md)。  
  
我們必須先建立組件後，才可以存取預存程序。 針對此範例，假設已在 C:\ 目錄中建立 helloworld.dll 組件。 將下列 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 陳述式加入至查詢。  
  
`CREATE ASSEMBLY helloworld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE`  
  
組件建立完成後，您就可以使用 create procedure 陳述式存取 HelloWorld 方法。 我們會將該預存程序稱為 hello：  
  
```sql
CREATE PROCEDURE hello  
@i nchar(25) OUTPUT  
AS  
EXTERNAL NAME helloworld.HelloWorldProc.HelloWorld  
-- if the HelloWorldProc class is inside a namespace (called MyNS),  
-- the last line in the create procedure statement would be  
-- EXTERNAL NAME helloworld.[MyNS.HelloWorldProc].HelloWorld  
```  
  
程序建立完成後，就可以使用與執行 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中撰寫的一般預存程序一樣的方法來執行它。 執行以下命令：  
  
```sql
DECLARE @J nchar(25)  
EXEC hello @J out  
PRINT @J  
```  
  
這將在 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 訊息視窗中產生下列輸出。  
  
```
Hello world!  
Hello world!  
```  
  
## <a name="removing-the-hello-world-stored-procedure-sample"></a>移除 "Hello World" 預存程序範例  

完成執行該範例預存程序時，您就可以從測試資料庫中移除該程序及組件。  
  
首先，使用 drop procedure 命令移除該程序。  
  
```sql
IF EXISTS (SELECT name FROM sysobjects WHERE name = 'hello')  
   drop procedure hello  
```  
  
程序一旦刪除後，您就可以移除包含範例程式碼的組件。  
  
```sql
IF EXISTS (SELECT name FROM sys.assemblies WHERE name = 'helloworld')  
   drop assembly helloworld  
```  
  
## <a name="next-steps"></a>後續步驟

如需 SQL Server 中 CLR 整合的詳細資訊，請參閱下列文章：

- [CLR 預存程序](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)
- [ADO.NET 的 SQL Server 同處理序特定擴充](../../../relational-databases/clr-integration-data-access-in-process-ado-net/sql-server-in-process-specific-extensions-to-ado-net.md)
- [偵錯 CLR 資料庫物件](../../../relational-databases/clr-integration/debugging-clr-database-objects.md)
- [CLR 整合安全性](../../../relational-databases/clr-integration/security/clr-integration-security.md)
