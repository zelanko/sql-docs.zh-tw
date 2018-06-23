---
title: 以程式設計方式建立套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: e44bcc70-32d3-43e8-a84b-29aef819d5d3
caps.latest.revision: 49
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c5955cc67583b5560e3998898822c7905d2d8e41
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/19/2018
ms.locfileid: "36031677"
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
  
 若要編譯和執行範例，請在 Visual Studio 中按 F5。 若要使用 C# 編譯器 **csc.exe** 建置程式碼，請在要編譯的命令提示字元之下，使用下列命令與檔案參考，以 .cs 或 .vb 檔案的名稱取代 \<filename>，並提供您所選擇的*\<outputfilename>*。  
  
 **csc /target:library /out: \<outputfilename>.dll \<filename>.cs /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 若要使用 Visual Basic .NET 編譯器 **vbc.exe** 建置程式碼，請在要編譯的命令提示字元之下，使用下列命令與檔案參考。  
  
 **vbc /target:library /out: \<outputfilename>.dll \<filename>.vb /r:Microsoft.SqlServer.Managed DTS.dll" /r:System.dll**  
  
 您也可以載入儲存在磁碟上、在檔案系統或是儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的現有封裝以建立封裝。 其差異在於會先建立 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 物件，然後其中一個應用程式的多載方法會填入封裝物件：`LoadPackage` 用於一般檔案、`LoadFromSQLServer` 用於儲存到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的封裝，或是 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> 用於儲存到檔案系統的封裝。 下列範例會從磁碟載入現有封裝，然後檢視封裝上的數個屬性。  
  
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
  
-   blogs.msdn.com 上的部落格文章：[API Sample - OleDB source and OleDB destination](http://go.microsoft.com/fwlink/?LinkId=220824) (API 範例 - OleDB 來源與 OleDB 目的地)。  
  
-   blogs.msdn.com 上的部落格文章：[EzAPI – Updated for SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223) (EzAPI - 針對 SQL Server 2012 更新)。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多 with Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式新增工作](../building-packages-programmatically/adding-tasks-programmatically.md)  
  
  