---
title: 以程式設計方式加入工作 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- tasks [Integration Services], packages
- adding package tasks
ms.assetid: 5d4652d5-228c-4238-905c-346dd8503fdf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: da9a2e5bf8338b8188f00f3c340d50ef32f1204f
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388626"
---
# <a name="adding-tasks-programmatically"></a>以程式設計方式加入工作
  在執行階段引擎中可以將工作加入下列類型的物件：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Package>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Sequence>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler>  
  
 這些類別都視為容器，而且它們全部都繼承 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSSequence.Executables%2A> 屬性。 容器可以包含工作集合，這些工作是容器執行期間執行階段所處理的可執行物件。 在集合中的物件執行順序是由容器中每個工作上所設定的任何 <xref:Microsoft.SqlServer.Dts.Runtime.PrecedenceConstraint> 來決定。 優先順序條件約束允許根據集合中的 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 之成功、失敗或是完成來執行分支。  
  
 每個容器都有 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 集合，它包含個別的 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 物件。 每個可執行的工作都會繼承和實作 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Execute%2A> 方法和 <xref:Microsoft.SqlServer.Dts.Runtime.Executable.Validate%2A> 方法。 這兩種方法都是由執行階段引擎來呼叫以處理每個 <xref:Microsoft.SqlServer.Dts.Runtime.Executable>。  
  
 若要將工作加入封裝，您需要具有 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 現有集合的容器。 大部分的情況下，您將加入集合的工作是封裝。 若要將新工作可執行檔加入容器的集合，可呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 方法。 該方法有單一參數和一個字串，包含 CLSID、PROGID、STOCK Moniker 或是您正在加入的工作之 <xref:Microsoft.SqlServer.Dts.Runtime.TaskInfo.CreationName%2A>。  
  
## <a name="task-names"></a>工作名稱  
 雖然您可以依名稱或是識別碼指定工作，`STOCK` Moniker 是在 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 方法中最常使用的參數。 若要將工作加入 `STOCK` Moniker 識別的可執行檔，請使用下列語法：  
  
```csharp  
Executable exec = package.Executables.Add("STOCK:BulkInsertTask");  
  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add("STOCK:BulkInsertTask")  
  
```  
  
 下列清單顯示在 `STOCK` Moniker 後面所使用的每個工作名稱。  
  
-   ActiveXScriptTask  
  
-   BulkInsertTask  
  
-   ExecuteProcessTask  
  
-   ExecutePackageTask  
  
-   Exec80PackageTask  
  
-   FileSystemTask  
  
-   FTPTask  
  
-   MSMQTask  
  
-   PipelineTask  
  
-   ScriptTask  
  
-   SendMailTask  
  
-   SQLTask  
  
-   TransferStoredProceduresTask  
  
-   TransferLoginsTask  
  
-   TransferErrorMessagesTask  
  
-   TransferJobsTask  
  
-   TransferObjectsTask  
  
-   TransferDatabaseTask  
  
-   WebServiceTask  
  
-   WmiDataReaderTask  
  
-   WmiEventWatcherTask  
  
-   XMLTask  
  
 如果您喜歡較明確的語法，或是如果您想要加入的工作沒有 STOCK Moniker，可以使用其完整名稱將工作加入可執行檔。 這個語法需要您也指定工作的版本號碼。  
  
```csharp  
Executable exec = package.Executables.Add(  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " +  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " +  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91");  
```  
  
```vb  
Dim exec As Executable = package.Executables.Add( _  
  "Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask, " & _  
  "Microsoft.SqlServer.ScriptTask, Version=10.0.000.0, " & _  
  "Culture=neutral, PublicKeyToken=89845dcd8080cc91")  
```  
  
 您可以用程式設計的方式取得工作的完整名稱，而不需指定工作版本，方法是使用類別的 **AssemblyQualifiedName** 屬性，如下列範例所示。 這個範例需要 Microsoft.SqlServer.SQLTask 組件的參考。  
  
```csharp  
using Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask;  
...  
      Executable exec = package.Executables.Add(  
        typeof(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName);  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask  
...  
    Dim exec As Executable = package.Executables.Add( _  
      GetType(Microsoft.SqlServer.Dts.Tasks.ExecuteSQLTask.ExecuteSQLTask).AssemblyQualifiedName)  
```  
  
 下列程式碼範例顯示如何從新封裝建立 <xref:Microsoft.SqlServer.Dts.Runtime.Executables> 集合，然後使用工作的 `STOCK` Moniker，將檔案系統工作和大量插入工作加入集合。 這個範例需要 Microsoft.SqlServer.FileSystemTask 與 Microsoft.SqlServer.BulkInsertTask 組件的參考。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thBulkInsertTask = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        Console.WriteLine("Type {0}", taskHost.InnerObject.ToString());  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thBulkInsertTask As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      Console.WriteLine("Type {0}", taskHost.InnerObject.ToString())  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **範例輸出：**  
  
 `Type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
## <a name="taskhost-container"></a>TaskHost 容器  
 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 類別是不會出現在圖形化使用者介面的容器，但是對於程式設計非常重要。 這個類別是每項工作的包裝函數。 透過使用 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 方法做為 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 物件加入封裝的工作，可以轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 物件。 當工作轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 時，可以在工作上使用其他屬性與方法。 另外，工作本身可以透過 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 屬性來存取。 視您的需求而定，可以決定將工作保留為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 物件，如此便可透過 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 集合使用工作的屬性。 使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 的優點是您可以撰寫更一般的程式碼。 如果您對於工作需要非常特定的程式碼，則應該將工作轉換為其適當的物件。  
  
 下列程式碼範例顯示如何將 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 和 thBulkInsertTask (包含 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask>) 轉換為 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> 物件。  
  
```csharp  
BulkInsertTask myTask = thBulkInsertTask.InnerObject as BulkInsertTask;  
```  
  
```vb  
Dim myTask As BulkInsertTask = CType(thBulkInsertTask.InnerObject, BulkInsertTask)  
```  
  
 下列程式碼範例顯示如何將可執行檔轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>，然後使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 屬性以決定主機包含哪些類型的可執行檔。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Tasks.FileSystemTask;  
using Microsoft.SqlServer.Dts.Tasks.BulkInsertTask;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
      // Add a File System task to the package.  
      Executable exec1 = p.Executables.Add("STOCK:FileSystemTask");  
      TaskHost thFileSystemTask1 = exec1 as TaskHost;  
      // Add a Bulk Insert task to the package.  
      Executable exec2 = p.Executables.Add("STOCK:BulkInsertTask");  
      TaskHost thFileSystemTask2 = exec2 as TaskHost;  
  
      // Iterate through the package Executables collection.  
      Executables pExecs = p.Executables;  
      foreach (Executable pExec in pExecs)  
      {  
        TaskHost taskHost = (TaskHost)pExec;  
        if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask)  
        {  
          // Do work with FileSystemTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        else if (taskHost.InnerObject is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask)  
        {  
          // Do work with BulkInsertTask here.  
          Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString());  
        }  
        // Add additional statements to check InnerObject, if desired.  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Tasks.FileSystemTask  
Imports Microsoft.SqlServer.Dts.Tasks.BulkInsertTask  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    ' Add a File System task to the package.  
    Dim exec1 As Executable = p.Executables.Add("STOCK:FileSystemTask")  
    Dim thFileSystemTask1 As TaskHost = CType(exec1, TaskHost)  
    ' Add a Bulk Insert task to the package.  
    Dim exec2 As Executable = p.Executables.Add("STOCK:BulkInsertTask")  
    Dim thFileSystemTask2 As TaskHost = CType(exec2, TaskHost)  
  
    ' Iterate through the package Executables collection.  
    Dim pExecs As Executables = p.Executables  
    Dim pExec As Executable  
    For Each pExec In pExecs  
      Dim taskHost As TaskHost = CType(pExec, TaskHost)  
      If TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask Then  
        ' Do work with FileSystemTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      ElseIf TypeOf taskHost.InnerObject Is Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask Then  
        ' Do work with BulkInsertTask here.  
        Console.WriteLine("Found task of type {0}", taskHost.InnerObject.ToString())  
      End If  
      ' Add additional statements to check InnerObject, if desired.  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
 **範例輸出：**  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.FileSystemTask.FileSystemTask`  
  
 `Found task of type Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask`  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Executables.Add%2A> 陳述式會傳回從新建立的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 物件轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 物件的可執行檔。  
  
 若要在新物件上設定屬性或是呼叫方法，您有兩個選項：  
  
1.  使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 集合。 例如，若要從物件取得屬性，請使用 `th.Properties["propertyname"].GetValue(th))`。 若要設定屬性，請使用 `th.Properties["propertyname"].SetValue(th, <value>);`。  
  
2.  將 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.InnerObject%2A> 的 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 轉換為工作類別。 例如，若要在將大量插入工作加入封裝以做為 <xref:Microsoft.SqlServer.Dts.Tasks.BulkInsertTask.BulkInsertTask> 以及接著轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.Executable> 之後，將該工作轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>，請使用 `BulkInsertTask myTask = th.InnerObject as BulkInsertTask;`。  
  
 在程式碼中使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 類別，而不是轉換為工作特定的類別具有下列優點：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost><xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 提供者並不需要程式碼中組件的參考。  
  
-   您可以撰寫可用於任何工作的一般常式，因為在編譯時期並不需要知道工作的名稱。 這樣的一般常式包括您傳遞工作名稱給該方法的一些方法，而且該方法的程式碼適用於所有工作。 這是撰寫測試程式碼的好方法。  
  
 從 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 轉換為工作特定的類別，具有下列優點：  
  
-   Visual Studio 專案提供您陳述式完成 (IntelliSense)。  
  
-   程式碼的執行速度可能更快。  
  
-   工作特定物件允許早期繫結與結果最佳化。 如需有關早期和晚期繫結的詳細資訊，請參閱＜Visual Basic 語言概念＞中的＜早期和晚期繫結＞主題。  
  
 下列程式碼範例擴充了重複使用工作程式碼的概念。 程式碼範例並不是將工作轉換為其特定的類別對等項目，而是將可執行檔轉換為 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>，然後使用 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost.Properties%2A> 以針對所有的工作撰寫一般程式碼。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package package = new Package();  
  
      string[] tasks = { "STOCK:SQLTask", "STOCK:ScriptTask",   
        "STOCK:ExecuteProcessTask", "STOCK:PipelineTask",   
        "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask" };  
  
      foreach (string s in tasks)  
      {  
        TaskHost taskhost = package.Executables.Add(s) as TaskHost;  
        DtsProperties props = taskhost.Properties;  
        Console.WriteLine("Enumerating properties on " + taskhost.Name);  
        Console.WriteLine(" TaskHost.InnerObject is " + taskhost.InnerObject.ToString());  
        Console.WriteLine();  
  
        foreach (DtsProperty prop in props)  
        {  
          Console.WriteLine("Properties for " + prop.Name);  
          Console.WriteLine("Name : " + prop.Name);  
          Console.WriteLine("Type : " + prop.Type.ToString());  
          Console.WriteLine("Readable : " + prop.Get.ToString());  
          Console.WriteLine("Writable : " + prop.Set.ToString());  
          Console.WriteLine();  
        }  
      }  
      Console.Read();  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Package = New Package()  
  
    Dim tasks() As String = New String() {"STOCK:SQLTask", "STOCK:ScriptTask", _  
              "STOCK:ExecuteProcessTask", "STOCK:PipelineTask", _  
              "STOCK:FTPTask", "STOCK:SendMailTask", "STOCK:MSMQTask"}  
  
    For Each s As String In tasks  
  
      Dim taskhost As TaskHost = CType(package.Executables.Add(s), TaskHost)  
      Dim props As DtsProperties = taskhost.Properties  
      Console.WriteLine("Enumerating properties on " & taskhost.Name)  
      Console.WriteLine(" TaskHost.InnerObject is " & taskhost.InnerObject.ToString())  
      Console.WriteLine()  
  
      For Each prop As DtsProperty In props  
        Console.WriteLine("Properties for " + prop.Name)  
        Console.WriteLine(" Name : " + prop.Name)  
        Console.WriteLine(" Type : " + prop.Type.ToString())  
        Console.WriteLine(" Readable : " + prop.Get.ToString())  
        Console.WriteLine(" Writable : " + prop.Set.ToString())  
        Console.WriteLine()  
      Next  
  
    Next  
    Console.Read()  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章：[EzAPI - Updated for SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=243223) (EzAPI - 針對 SQL Server 2012 更新)。  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式連線工作](../building-packages-programmatically/connecting-tasks-programmatically.md)  
  
  
