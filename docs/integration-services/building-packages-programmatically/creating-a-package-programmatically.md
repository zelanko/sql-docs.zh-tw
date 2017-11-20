---
title: "以程式設計方式建立封裝 |Microsoft 文件"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
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
- CSharp
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
caps.latest.revision: 51
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 58a8201d68cb6d942bd98ca3c53b6cf98336284e
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-package-programmatically"></a>以程式設計方式建立封裝
  <xref:Microsoft.SqlServer.Dts.Runtime.Package> 物件是 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 專案方案中所有其他物件的最上層容器。 做為最上層容器，封裝是第一個建立的物件，而且後續的物件會加入其中，然後在封裝的內容中執行。 封裝本身不會移動或是轉換資料。 封裝依賴它所含的工作 (Task) 以執行工作 (Work)。 工作 (Task) 會執行封裝所執行的大部分工作 (Work)，並定義封裝的功能。 只需要三行程式碼就可以建立和執行封裝，但是還需要將各種工作與 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件加入，以便為您的封裝提供其他功能。 本節討論如何以程式設計方式建立封裝。 有關如何建立工作或 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 的詳細資訊並非在此提供， 這些內容將於後續章節說明。  
  
## <a name="example"></a>範例  
 若要使用 Visual Studio IDE 撰寫程式碼，會需要 Microsoft.SqlServer.ManagedDTS.DLL 的參考，才能建立 Microsoft.SqlServer.Dts.Runtime 的 `using` 陳述式 (在 Visual Basic .NET 中則是 `Imports`)。 下列程式碼範例示範建立空的封裝。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package;  
      package = new Package();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package  
    package = New Package  
  
  End Sub  
  
End Module  
```  
  
 若要編譯和執行範例，請在 Visual Studio 中按 F5。 若要建置使用 C# 編譯器的程式碼**csc.exe**，請在命令提示字元進行編譯，請使用下列命令與檔案參考，取代*\<檔名 >* .cs 或.vb 檔案，並提供的名稱取代 *\<outputfilename >*您選擇。  
  
 **csc /target: library /out: \<outputfilename >.dll\<檔名 >.cs /r:Microsoft.SqlServer.Managed DTS.dll"/r**  
  
 若要建置程式碼使用 Visual Basic.NET 編譯器**vbc.exe**，請在命令提示字元進行編譯，請使用下列命令與檔案參考。  
  
 **vbc /target: library /out: \<outputfilename >.dll\<檔名 >.vb /r:Microsoft.SqlServer.Managed DTS.dll"/r**  
  
 您也可以載入儲存在磁碟上、在檔案系統或是儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的現有封裝以建立封裝。 其差異在於，<xref:Microsoft.SqlServer.Dts.Runtime.Application>第一次建立物件，和封裝物件然後填滿其中一種應用程式的多載方法： **LoadPackage**用於一般檔案、 **LoadFromSQLServer**封裝儲存到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，或<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>封裝儲存至檔案系統。 下列範例會從磁碟載入現有封裝，然後檢視封裝上的數個屬性。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class ApplicationTests  
  {  
    static void Main(string[] args)  
    {  
      // The variable pkg points to the location of the  
      // ExecuteProcess package sample that was installed with  
      // the SSIS samples.  
      string pkg = @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx";  
  
      Application app = new Application();  
      Package p = app.LoadPackage(pkg, null);  
  
      // Now that the package is loaded, we can query on  
      // its properties.  
      int n = p.Configurations.Count;  
      DtsProperty p2 = p.Properties["VersionGUID"];  
      DTSProtectionLevel pl = p.ProtectionLevel;  
  
      Console.WriteLine("Number of configurations = " + n.ToString());  
      Console.WriteLine("VersionGUID = " + (string)p2.GetValue(p));  
      Console.WriteLine("ProtectionLevel = " + pl.ToString());  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module ApplicationTests  
  
  Sub Main()  
  
    ' The variable pkg points to the location of the  
    ' ExecuteProcess package sample that was installed with  
    ' the SSIS samples.  
    Dim pkg As String = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\ExecuteProcess Sample\ExecuteProcess\UsingExecuteProcess.dtsx"  
  
    Dim app As Application = New Application()  
    Dim p As Package = app.LoadPackage(pkg, Nothing)  
  
    ' Now that the package is loaded, we can query on  
    ' its properties.  
    Dim n As Integer = p.Configurations.Count  
    Dim p2 As DtsProperty = p.Properties("VersionGUID")  
    Dim pl As DTSProtectionLevel = p.ProtectionLevel  
  
    Console.WriteLine("Number of configurations = " & n.ToString())  
    Console.WriteLine("VersionGUID = " & CType(p2.GetValue(p), String))  
    Console.WriteLine("ProtectionLevel = " & pl.ToString())  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **範例輸出：**  
  
 `Number of configurations = 2`  
  
 `VersionGUID = {09016682-89B8-4406-AAC9-AF1E527FF50F}`  
  
 `ProtectionLevel = DontSaveSensitive`  
  
## <a name="external-resources"></a>外部資源  
  
-   部落格文章： [API 範例-OleDB 來源與 OleDB 目的地](http://go.microsoft.com/fwlink/?LinkId=220824)，blogs.msdn.com 上。  
  
-   部落格文章： [EzAPI-已更新 SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223)，blogs.msdn.com 上。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式加入工作](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)  
  
  

