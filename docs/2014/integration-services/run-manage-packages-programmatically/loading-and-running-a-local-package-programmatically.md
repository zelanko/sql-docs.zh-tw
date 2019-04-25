---
title: 以程式設計方式載入和執行本機套件 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Integration Services packages, running
- events [Integration Services], capturing
- packages [Integration Services], running
- loading packages programmatically
- Visual Basic [Integration Services]
- running packages [Integration Services]
- programmatically load and run packages [SSIS]
ms.assetid: 2f9fc1a8-a001-4c54-8c64-63b443725422
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 00d213bf8ca554b60edc8dc3de3f1290cd00f538
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62766890"
---
# <a name="loading-and-running-a-local-package-programmatically"></a>以程式設計的方式載入和執行本機封裝
  您可以使用[執行套件](../packages/run-integration-services-ssis-packages.md)中所述的方法，視需要或是依預定的次數執行 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 套件。 然而，只需要幾行的程式碼，您就可以從 Windows Form 應用程式、主控台應用程式、ASP.NET Web 表單或 Web 服務，或是 Windows 服務等自訂應用程式執行封裝。  
  
 此主題會討論：  
  
-   以程式設計方式載入封裝  
  
-   以程式設計方式執行封裝  
  
 本主題中用以載入和執行封裝的所有方法，都需要 `Microsoft.SqlServer.ManagedDTS` 組件的參考。 在新專案中加入參考之後，請使用 `using` 或 `Imports` 陳述式匯入 <xref:Microsoft.SqlServer.Dts.Runtime> 命名空間。  
  
## <a name="loading-a-package-programmatically"></a>以程式設計方式載入封裝  
 無論封裝儲存在本機或遠端，如果要在本機電腦上以程式設計方式載入封裝，請呼叫下列其中一種方法：  
  
|儲存位置|要呼叫的方法|  
|----------------------|--------------------|  
|檔案|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A>|  
|SSIS 封裝存放區|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|<xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A>|  
  
> [!IMPORTANT]  
>  搭配 SSIS 封裝存放區使用之 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別的方法，僅支援 "."、localhost 或本機伺服器的伺服器名稱。 您無法使用 "(local)"。  
  
## <a name="running-a-package-programmatically"></a>以程式設計方式執行封裝  
 在本機電腦上執行封裝的 Managed 程式碼中開發自訂應用程式需要下列方法。 接下來的範例主控台應用程式中將示範此處摘要的步驟。  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically"></a>以程式設計的方式在本機電腦上執行封裝  
  
1.  啟動 Visual Studio 開發環境，並以慣用的開發語言建立新應用程式。 此範例使用主控台應用程式，不過，您也可以從 Windows Form 應用程式、ASP.NET Web 表單或 Web 服務或是 Windows 服務執行封裝。  
  
2.  在 [專案] 功能表上，按一下 [新增參考]，然後新增 **Microsoft.SqlServer.ManagedDTS.dll** 的參考。 按一下 [確定] 。  
  
3.  使用 Visual Basic`Imports`陳述式或 C#`using`陳述式匯入**Microsoft.SqlServer.Dts.Runtime**命名空間。  
  
4.  在主常式中加入下列程式碼。 完成的主控台應用程式應類似下列範例。  
  
    > [!NOTE]  
    >  範例程式碼會透過使用 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadPackage%2A> 方法示範從檔案系統載入封裝。 不過，您也可以呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromSqlServer%2A> 方法從 MSDB 資料庫載入封裝，或是呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Application.LoadFromDtsServer%2A> 方法從 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 封裝存放區載入封裝。  
  
5.  執行專案。 範例程式碼會執行隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 範例安裝的 CalculatedColumns 範例封裝。 封裝執行的結果會顯示在主控台視窗中。  
  
### <a name="sample-code"></a>範例程式碼  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, Nothing)  
    pkgResults = pkg.Execute()  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppCS  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, null);  
      pkgResults = pkg.Execute();  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
## <a name="capturing-events-from-a-running-package"></a>從執行封裝擷取事件  
 當您以程式設計方式執行封裝 (如前面的範例所示)，可能也會想要擷取當封裝執行時所發生的錯誤及其他事件。 您可以藉由加入從 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 類別繼承的類別，以及藉由在載入封裝時將參考傳遞給該類別，來完成這項作業。 雖然下列範例只會擷取 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents.OnError%2A> 事件，不過 <xref:Microsoft.SqlServer.Dts.Runtime.DefaultEvents> 類別可讓您擷取更多其他事件。  
  
#### <a name="to-run-a-package-on-the-local-computer-programmatically-and-capture-package-events"></a>以程式設計的方式在本機電腦上執行封裝並擷取封裝事件  
  
1.  遵循上述範例中的步驟，為此範例建立專案。  
  
2.  在主常式中加入下列程式碼。 完成的主控台應用程式應類似下列範例。  
  
3.  執行專案。 範例程式碼會執行隨 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 範例安裝的 CalculatedColumns 範例封裝。 封裝執行的結果以及任何發生的錯誤都會顯示在主控台視窗中。  
  
### <a name="sample-code"></a>範例程式碼  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim pkgLocation As String  
    Dim pkg As New Package  
    Dim app As New Application  
    Dim pkgResults As DTSExecResult  
  
    Dim eventListener As New EventListener()  
  
    pkgLocation = _  
      "C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" & _  
      "\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx"  
    pkg = app.LoadPackage(pkgLocation, eventListener)  
    pkgResults = pkg.Execute(Nothing, Nothing, eventListener, Nothing, Nothing)  
  
    Console.WriteLine(pkgResults.ToString())  
    Console.ReadKey()  
  
  End Sub  
  
End Module  
  
Class EventListener  
  Inherits DefaultEvents  
  
  Public Overrides Function OnError(ByVal source As Microsoft.SqlServer.Dts.Runtime.DtsObject, _  
    ByVal errorCode As Integer, ByVal subComponent As String, ByVal description As String, _  
    ByVal helpFile As String, ByVal helpContext As Integer, _  
    ByVal idofInterfaceWithError As String) As Boolean  
  
    ' Add application-specific diagnostics here.  
    Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description)  
    Return False  
  
  End Function  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace RunFromClientAppWithEventsCS  
{  
  class MyEventListener : DefaultEvents  
  {  
    public override bool OnError(DtsObject source, int errorCode, string subComponent,   
      string description, string helpFile, int helpContext, string idofInterfaceWithError)  
    {  
      // Add application-specific diagnostics here.  
      Console.WriteLine("Error in {0}/{1} : {2}", source, subComponent, description);  
      return false;  
    }  
  }  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      string pkgLocation;  
      Package pkg;  
      Application app;  
      DTSExecResult pkgResults;  
  
      MyEventListener eventListener = new MyEventListener();  
  
      pkgLocation =  
        @"C:\Program Files\Microsoft SQL Server\100\Samples\Integration Services" +  
        @"\Package Samples\CalculatedColumns Sample\CalculatedColumns\CalculatedColumns.dtsx";  
      app = new Application();  
      pkg = app.LoadPackage(pkgLocation, eventListener);  
      pkgResults = pkg.Execute(null, null, eventListener, null, null);  
  
      Console.WriteLine(pkgResults.ToString());  
      Console.ReadKey();  
    }  
  }  
}  
```  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [了解本機與遠端執行之間的差異](../run-manage-packages-programmatically/understanding-the-differences-between-local-and-remote-execution.md)   
 [以程式設計方式載入和執行遠端封裝](../run-manage-packages-programmatically/loading-and-running-a-remote-package-programmatically.md)   
 [載入本機套件的輸出](../run-manage-packages-programmatically/loading-the-output-of-a-local-package.md)  
  
  
