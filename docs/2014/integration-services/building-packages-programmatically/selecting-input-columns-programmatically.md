---
title: 以程式設計方式選取輸入資料行 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- input column mapping
- data flow task [Integration Services], components
- data flow task [Integration Services], column mapping
- mapping input columns [Integration Services]
- column mapping [Integration Services]
- data flow [Integration Services], column mapping
- data flow [Integration Services], components
ms.assetid: b53b110a-dcf4-4464-ae98-81e892ab74c3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d7c1592058776246ad3df657c3340303a60df296
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58390907"
---
# <a name="selecting-input-columns-programmatically"></a>以程式設計方式選取輸入資料行
  在您以程式設計方式連接元件之後，請從您要轉換或是傳遞到下游元件的上游元件中選取資料行。 如果您不為元件選取輸入資料行，元件不會從資料流程工作收到任何資料列。  
  
## <a name="selecting-columns"></a>選取資料行  
 呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100.GetVirtualInput%2A> 方法從上游元件擷取可用資料行的清單，然後呼叫設計階段元件執行個體的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetUsageType%2A> 方法，以便從虛擬輸入資料行集合選取資料行。 當您呼叫此方法時，元件會在其輸入資料行集合中，建立新輸入資料行，該輸入資料行集合與上游元件之輸出集合中的對應資料行，具有相同的歷程識別碼。  
  
 請勿直接呼叫虛擬輸入物件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSVirtualInput100.SetUsageType%2A> 方法來選取資料行，因為這會略過元件根據不適當的資料類型或是其他屬性來拒絕資料行的能力。  
  
## <a name="sample"></a>範例  
 下列程式碼範例示範如何使用元件的設計階段執行個體，為元件選取資料行。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      // Create a package and add a Data Flow task.  
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLE DB connection manager to the package.  
      ConnectionManager conMgr = package.Connections.Add("OLEDB");  
      conMgr.ConnectionString = "Provider=SQLOLEDB.1;" +  
        "Data Source=<servername>;Initial Catalog=AdventureWorks;" +  
        "Integrated Security=SSPI;";  
      conMgr.Name = "SSIS Connection Manager for OLE DB";  
      conMgr.Description = "OLE DB connection to the AdventureWorks database.";  
  
      // Create and configure an OLE DB source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      // Create the design-time instance of the source.  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      // The ProvideComponentProperties method creates a default output.  
      srcDesignTime.ProvideComponentProperties();  
      // Assign the connection manager.  
      source.RuntimeConnectionCollection[0].ConnectionManager =  
        DtsConvert.GetExtendedInterface(conMgr);  
      // Set the custom properties of the source.  
      srcDesignTime.SetComponentProperty("AccessMode", 2);  
      srcDesignTime.SetComponentProperty("SqlCommand",  
        "Select * from Production.Product");  
  
      // Connect to the data source,  
      //  and then update the metadata for the source.  
      srcDesignTime.AcquireConnections(null);  
      srcDesignTime.ReinitializeMetaData();  
      srcDesignTime.ReleaseConnections();  
  
      // Create and configure an OLE DB destination.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      // Create the design-time instance of the destination.  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      // The ProvideComponentProperties method creates a default input.  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path from source to destination.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
  
      // Get the destination's default input and virtual input.  
      IDTSInput100 input = destination.InputCollection[0];  
      IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
      // Iterate through the virtual input column collection.  
      foreach (IDTSVirtualInputColumn100 vColumn in vInput.VirtualInputColumnCollection)  
      {  
        // Call the SetUsageType method of the destination  
        //  to add each available virtual input column as an input column.  
        destDesignTime.SetUsageType(  
           input.ID, vInput, vColumn.LineageID, DTSUsageType.UT_READONLY);  
      }  
  
      // Verify that the columns have been added to the input.  
      foreach (IDTSInputColumn100 inputColumn in destination.InputCollection[0].InputColumnCollection)  
        Console.WriteLine(inputColumn.Name);  
      Console.Read();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    ' Create a package and add a Data Flow task.  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Add an OLE DB connection manager to the package.  
    Dim conMgr As ConnectionManager = package.Connections.Add("OLEDB")  
    conMgr.ConnectionString = "Provider=SQLOLEDB.1;" & _  
      "Data Source=<servername>;Initial Catalog=AdventureWorks;" & _  
      "Integrated Security=SSPI;"  
    conMgr.Name = "SSIS Connection Manager for OLE DB"  
    conMgr.Description = "OLE DB connection to the AdventureWorks database."  
  
    ' Create and configure an OLE DB source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    ' Create the design-time instance of the source.  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate  
    ' The ProvideComponentProperties method creates a default output.  
    srcDesignTime.ProvideComponentProperties()  
    ' Assign the connection manager.  
    source.RuntimeConnectionCollection(0).ConnectionManager = _  
      DtsConvert.GetExtendedInterface(conMgr)  
    ' Set the custom properties of the source.  
    srcDesignTime.SetComponentProperty("AccessMode", 2)  
    srcDesignTime.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Connect to the data source,  
    '  and then update the metadata for the source.  
    srcDesignTime.AcquireConnections(Nothing)  
    srcDesignTime.ReinitializeMetaData()  
    srcDesignTime.ReleaseConnections()  
  
    ' Create and configure an OLE DB destination.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    ' Create the design-time instance of the destination.  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate  
    ' The ProvideComponentProperties method creates a default input.  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path from source to destination.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
    ' Get the destination's default input and virtual input.  
    Dim input As IDTSInput100 = destination.InputCollection(0)  
    Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput  
  
    ' Iterate through the virtual input column collection.  
    For Each vColumn As IDTSVirtualInputColumn100 In vInput.VirtualInputColumnCollection  
      ' Call the SetUsageType method of the destination  
      '  to add each available virtual input column as an input column.  
      destDesignTime.SetUsageType(input.ID, vInput, vColumn.LineageID, DTSUsageType.UT_READONLY)  
    Next  
  
    ' Verify that the columns have been added to the input.  
    For Each inputColumn As IDTSInputColumn100 In destination.InputCollection(0).InputColumnCollection  
      Console.WriteLine(inputColumn.Name)  
    Next  
    Console.Read()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式儲存套件](../building-packages-programmatically/saving-a-package-programmatically.md)  
  
  
