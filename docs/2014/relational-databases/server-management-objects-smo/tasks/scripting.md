---
title: 指令碼 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- dependencies [SMO]
- scripts [SMO]
ms.assetid: 13a35511-3987-426b-a3b7-3b2e83900dc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a54a067ed9da68e25f9394a463fa352ccc165f21
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "72781924"
---
# <a name="scripting"></a>指令碼
  在 SMO 中，指令碼是由 <xref:Microsoft.SqlServer.Management.Smo.Scripter> 物件及其子物件控制，或是由個別物件的 `Script` 方法控制。 <xref:Microsoft.SqlServer.Management.Smo.Scripter>物件會針對實例[!INCLUDE[msCoName](../../../includes/msconame-md.md)]上物件的相依性關聯性控制對應[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 使用 <xref:Microsoft.SqlServer.Management.Smo.Scripter> 物件及其子物件所進行的進階指令碼作業是三階段的程序：  
  
1.  探索  
  
2.  產生清單  
  
3.  產生指令碼  
  
 探索階段會使用 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> 物件。 如果已給定物件 URN 清單，則 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.DiscoverDependencies%2A> 物件的 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker> 方法會針對 URN 清單中的物件傳回 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> 物件。 布林值*fParents*參數是用來選取是否要探索指定物件的父系或子系。 在這個階段可以修改相依性樹狀目錄。  
  
 在產生清單階段會傳入樹狀目錄並傳回產生的清單。 這個物件清單會以指令碼作業順序排列，且可以操作。  
  
 產生清單階段會使用 <xref:Microsoft.SqlServer.Management.Smo.DependencyWalker.WalkDependencies%2A> 方法傳回 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>。 在這個階段可以修改 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree>。  
  
 在第三個也就是最後階段時，會產生具有指定清單和指令碼選項的指令碼。 結果會以 <xref:System.Collections.Specialized.StringCollection> 系統物件傳回。 接下來在這個階段中會從 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree> 物件的 Items 集合以及 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.NumberOfSiblings%2A> 和 <xref:Microsoft.SqlServer.Management.Smo.DependencyTree.FirstChild%2A> 之類的屬性擷取相依物件的名稱。  
  
## <a name="example"></a>範例  
 如果要使用所提供的任何程式碼範例，您必須選擇建立應用程式用的程式設計環境、程式設計範本，及程式設計語言。 如需詳細資訊，請參閱[在 Visual Studio .net 中建立 VISUAL BASIC SMO 專案](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md)或[在 Visual Studio .Net 中建立 VISUAL C&#35; SMO 專案](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
 這個程式碼範例需要針對 System.Collections.Specialized 命名空間使用 `Imports` 陳述式。 請在應用程式中，將這個陳述式與其他的 Imports 陳述式一同插入任何宣告之前。  
  
```vb
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Common  
Imports System.Collections.Specialized  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-basic"></a>針對 Visual Basic 中的資料庫撰寫相依性的指令碼  
 這個程式碼範例示範如何探索相依性，並反覆運算清單以顯示結果。  
  
```vb
' compile with:   
' /r:Microsoft.SqlServer.Smo.dll   
' /r:Microsoft.SqlServer.ConnectionInfo.dll   
' /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
Imports Microsoft.SqlServer.Management.Smo  
Imports Microsoft.SqlServer.Management.Sdk.Sfc  
  
Public Class A  
   Public Shared Sub Main()  
      ' database name  
      Dim dbName As [String] = "AdventureWorksLT2012"   ' database name  
  
      ' Connect to the local, default instance of SQL Server.   
      Dim srv As New Server()  
  
      ' Reference the database.    
      Dim db As Database = srv.Databases(dbName)  
  
      ' Define a Scripter object and set the required scripting options.   
      Dim scrp As New Scripter(srv)  
      scrp.Options.ScriptDrops = False  
      scrp.Options.WithDependencies = True  
      scrp.Options.Indexes = True   ' To include indexes  
      scrp.Options.DriAllConstraints = True   ' to include referential constraints in the script  
  
      ' Iterate through the tables in database and script each one. Display the script.  
      For Each tb As Table In db.Tables  
         ' check if the table is not a system table  
         If tb.IsSystemObject = False Then  
            Console.WriteLine("-- Scripting for table " + tb.Name)  
  
            ' Generating script for table tb  
            Dim sc As System.Collections.Specialized.StringCollection = scrp.Script(New Urn() {tb.Urn})  
            For Each st As String In sc  
               Console.WriteLine(st)  
            Next  
            Console.WriteLine("--")  
         End If  
      Next  
   End Sub  
End Class  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-visual-c"></a>針對 Visual C# 中的資料庫撰寫相依性的指令碼  
 這個程式碼範例示範如何探索相依性，並反覆運算清單以顯示結果。  
  
```csharp
// compile with:   
// /r:Microsoft.SqlServer.Smo.dll   
// /r:Microsoft.SqlServer.ConnectionInfo.dll   
// /r:Microsoft.SqlServer.Management.Sdk.Sfc.dll   
  
using System;  
using Microsoft.SqlServer.Management.Smo;  
using Microsoft.SqlServer.Management.Sdk.Sfc;  
  
public class A {  
   public static void Main() {   
      String dbName = "AdventureWorksLT2012"; // database name  
  
      // Connect to the local, default instance of SQL Server.   
      Server srv = new Server();  
  
      // Reference the database.    
      Database db = srv.Databases[dbName];  
  
      // Define a Scripter object and set the required scripting options.   
      Scripter scrp = new Scripter(srv);  
      scrp.Options.ScriptDrops = false;  
      scrp.Options.WithDependencies = true;  
      scrp.Options.Indexes = true;   // To include indexes  
      scrp.Options.DriAllConstraints = true;   // to include referential constraints in the script  
  
      // Iterate through the tables in database and script each one. Display the script.     
      foreach (Table tb in db.Tables) {   
         // check if the table is not a system table  
         if (tb.IsSystemObject == false) {  
            Console.WriteLine("-- Scripting for table " + tb.Name);  
  
            // Generating script for table tb  
            System.Collections.Specialized.StringCollection sc = scrp.Script(new Urn[]{tb.Urn});  
            foreach (string st in sc) {  
               Console.WriteLine(st);  
            }  
            Console.WriteLine("--");  
         }  
      }   
   }  
}  
```  
  
## <a name="scripting-out-the-dependencies-for-a-database-in-powershell"></a>在 PowerShell 中針對資料庫撰寫相依性的指令碼  
 這個程式碼範例示範如何探索相依性，並反覆運算清單以顯示結果。  
  
```powershell
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
# Create a Scripter object and set the required scripting options.  
$scrp = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Scripter -ArgumentList (Get-Item .)  
$scrp.Options.ScriptDrops = $false  
$scrp.Options.WithDependencies = $true  
$scrp.Options.IncludeIfNotExists = $true  
  
# Set the path context to the tables in AdventureWorks2012.  
CD Databases\AdventureWorks2012\Tables  
  
foreach ($Item in Get-ChildItem)  
 {    
 $scrp.Script($Item)  
 }  
```  
