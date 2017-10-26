---
title: "以程式設計方式加入資料流程元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
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
- data flow task [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: c06065cf-43e5-4b6b-9824-7309d7f5e35e
caps.latest.revision: 61
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 8bd642d31e0a6a813b239935f3fb091003b682fc
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="adding-data-flow-components-programmatically"></a>以程式設計方式加入資料流程元件
  當您建立資料流程時，可以從加入元件開始。 接著您會設定這些元件，然後將它們連接在一起以便在執行階段建立資料流程。 本章節描述將元件加入資料流程工作，建立元件的設計階段執行個體，然後設定元件。 如需如何連接元件的資訊，請參閱[連接資料資料流程元件以程式設計方式](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)。  
  
## <a name="adding-a-component"></a>加入元件  
 呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaDataCollection100.New%2A> 集合的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.ComponentMetaDataCollection%2A> 方法，以建立新元件並將它加入資料流程工作中。 這個方法會傳回元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面。 不過，此時，<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 並不包含任何一個元件的特定資訊。 設定 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 屬性以識別元件的類型。 資料流程工作使用此屬性值在執行階段建立元件的執行個體。  
  
 在 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 屬性中指定的值，可以是 CLSID、PROGID 或是元件的 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 屬性。 CLSID 通常會顯示在 [屬性] 視窗中，做為元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 屬性值。 取得這個屬性以及可用元件的其他屬性的相關資訊，請參閱[探索資料資料流程元件以程式設計方式](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)。  
  
## <a name="adding-a-managed-component"></a>加入 Managed 元件  
 您無法使用 CLSID 或 PROGID 將 Managed 資料流程元件加入資料流程，因為這些值會指向包裝函數，而不是元件本身。 您可以改為使用**CreationName**屬性或**AssemblyQualifiedName**屬性，如下列範例所示。  
  
 如果您想要使用**AssemblyQualifiedName**屬性，則必須加入參考您[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]包含 managed 的元件的組件的專案。 這些組件不會列在 .NET 索引標籤的**加入參考** 對話方塊。 通常您必須瀏覽，以找出組件中的**C:\Program Files\Microsoft SQL Server\100\DTS\PipelineComponents**資料夾。  
  
 內建的 Managed 資料流程元件包括：  
  
-   [!INCLUDE[vstecado](../../includes/vstecado-md.md)] 來源  
  
-   XML 來源  
  
-   DataReader 目的地  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Compact 目的地  
  
-   指令碼元件  
  
 下列程式碼範例顯示兩種將 Managed 元件加入資料流程的方法：  
  
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
      Microsoft.SqlServer.Dts.Runtime.Package package = new Microsoft.SqlServer.Dts.Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Microsoft.SqlServer.Dts.Runtime.TaskHost thMainPipe = (Microsoft.SqlServer.Dts.Runtime.TaskHost)e;  
      MainPipe dataFlowTask = (MainPipe)thMainPipe.InnerObject;  
  
      // The Application object will be used to obtain the CreationName  
      //  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
      Application app = new Application();  
  
      // Add a first ADO NET source to the data flow.  
      //  The CreationName property requires an Application instance.  
      IDTSComponentMetaData100 component1 = dataFlowTask.ComponentMetaDataCollection.New();  
      component1.Name = "DataReader Source";  
      component1.ComponentClassID = app.PipelineComponentInfos["DataReader Source"].CreationName;  
  
      // Add a second ADO NET source to the data flow.  
      //  The AssemblyQualifiedName property requires a reference to the assembly.  
      IDTSComponentMetaData100 component2 = dataFlowTask.ComponentMetaDataCollection.New();  
      component2.Name = "DataReader Source";  
      component2.ComponentClassID = typeof(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName;  
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
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' The Application object will be used to obtain the CreationName  
    '  of a PipelineComponentInfo from its PipelineComponentInfos collection.  
    Dim app As New Application()  
  
    ' Add a first ADO NET source to the data flow.  
    '  The CreationName property requires an Application instance.  
    Dim component1 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component1.Name = "DataReader Source"  
    component1.ComponentClassID = app.PipelineComponentInfos("DataReader Source").CreationName  
  
    ' Add a second ADO NET source to the data flow.  
    '  The AssemblyQualifiedName property requires a reference to the assembly.  
    Dim component2 As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component2.Name = "DataReader Source"  
    component2.ComponentClassID = _  
      GetType(Microsoft.SqlServer.Dts.Pipeline.DataReaderSourceAdapter).AssemblyQualifiedName  
  
  End Sub  
  
End Module  
```  
  
## <a name="creating-the-design-time-instance-of-the-component"></a>建立元件的設計階段執行個體  
 呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.Instantiate%2A> 方法以建立 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 屬性所識別的元件之設計階段執行個體。 此方法會傳回 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapper> 物件，它是 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 介面的 Managed 包裝函數。  
  
 請盡可能使用設計階段執行個體的方法來修改元件，而不要採用直接修改元件中繼資料的方式。 雖然在中繼資料中有一些項目是必須直接設定的 (例如連接)，不過，通常不建議直接修改中繼資料，因為您會略過元件監視並驗證變更的能力。  
  
## <a name="assigning-connections"></a>指派連接  
 有些元件 (例如 OLE DB 來源元件) 需要外部資料的連接，並為了此用途使用封裝中現有的 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnectionCollection100.Count%2A> 集合的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 屬性會指出元件所需的執行階段 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> 物件數目。 如果計數大於零，則元件需要連接。 藉由指定 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.ConnectionManager%2A> 內第一個連接的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeConnection100.Name%2A> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.RuntimeConnectionCollection%2A> 屬性，將連接管理員從封裝指派至元件。 請注意，在執行階段連接集合中的連接管理員名稱必須符合連接 managerreferenced 從封裝的名稱。  
  
## <a name="setting-the-values-of-custom-properties"></a>設定自訂屬性值  
 在建立元件的設計階段執行個體之後，呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> 方法。 此方法類似於建構函式，因為它會建立其自訂屬性及其輸入和輸出物件，以初始化新建立的元件。 請勿在一個元件上呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> 超過一次，因為元件可能會重設本身，並且遺失之前對其中繼資料所做的任何修改。  
  
 元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.CustomPropertyCollection%2A> 包含該元件特有的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 物件之集合。 與其他程式設計模型不同的是，物件的屬性在物件上永遠是可見的，而元件只會在您呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ProvideComponentProperties%2A> 方法時，擴展其自訂屬性集合。 在您呼叫方法之後，請使用元件設計階段執行個體的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.SetComponentProperty%2A> 方法，將值指派到其自訂屬性。 此方法會接受識別自訂屬性的名稱/值組，並提供它的新值。  
  
## <a name="initializing-output-columns"></a>初始化輸出資料行  
 在您將元件加入工作並設定它之後，會初始化物件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 中之資料行集合。 這個步驟對於來源元件特別重要，但是可能無法初始化轉換與目的地元件的資料行，因為它們通常與從上游元件收到的資料行相依。  
  
 呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> 方法以初始化來源元件輸出中的資料行。 因為元件不會自動連接到外部資料來源，所以請在呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.AcquireConnections%2A> 之前先呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReinitializeMetaData%2A> 方法，以提供其外部資料來源的元件存取權，以及擴展其資料行中繼資料的能力。 最後，呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.CManagedComponentWrapperClass.ReleaseConnections%2A> 方法以釋放連接。  
  
## <a name="next-step"></a>下一個步驟  
 加入和設定元件之後, 下一個步驟是 > 主題中所討論的元件之間建立路徑[建立路徑之間兩個元件](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)。  
  
## <a name="sample"></a>範例  
 下列程式碼範例會將 OLE DB 來源元件加入資料流程工作，建立元件的設計階段執行個體，然後設定元件的屬性。 這個範例需要 Microsoft.SqlServer.DTSRuntimeWrap 組件的額外參考。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Runtime.Package package = new Runtime.Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      Runtime.TaskHost thMainPipe = e as Runtime.TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Add an OLEDB connection manager to the package.  
      ConnectionManager cm = package.Connections.Add("OLEDB");  
      cm.Name = "OLEDB ConnectionManager";  
      cm.ConnectionString = "Data Source=(local);" +   
        "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" +   
        "Integrated Security=SSPI;"  
  
      // Add an OLE DB source to the data flow.  
      IDTSComponentMetaData100 component =   
        dataFlowTask.ComponentMetaDataCollection.New();  
      component.Name = "OLEDBSource";  
      component.ComponentClassID = "DTSAdapter.OleDbSource.1";  
      // You can also use the CLSID of the component instead of the PROGID.  
      //component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
      // Get the design time instance of the component.  
      CManagedComponentWrapper instance = component.Instantiate();  
  
      // Initialize the component  
      instance.ProvideComponentProperties();  
  
      // Specify the connection manager.  
      if (component.RuntimeConnectionCollection.Count > 0)  
      {  
        component.RuntimeConnectionCollection[0].ConnectionManager =   
          DtsConvert.GetExtendedInterface(package.Connections[0]);  
        component.RuntimeConnectionCollection[0].ConnectionManagerID =   
          package.Connections[0].ID;      }  
  
      // Set the custom properties.  
      instance.SetComponentProperty("AccessMode", 2);  
      instance.SetComponentProperty("SqlCommand",   
        "Select * from Production.Product");  
  
      // Reinitialize the metadata.  
      instance.AcquireConnections(null);  
      instance.ReinitializeMetaData();  
      instance.ReleaseConnections();  
  
      // Add other components to the data flow and connect them.  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim package As Microsoft.SqlServer.Dts.Runtime.Package = _  
      New Microsoft.SqlServer.Dts.Runtime.Package()  
    Dim e As Executable = package.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As Microsoft.SqlServer.Dts.Runtime.TaskHost = _  
      CType(e, Microsoft.SqlServer.Dts.Runtime.TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
    ' Add an OLEDB connection manager to the package.  
    Dim cm As ConnectionManager = package.Connections.Add("OLEDB")  
    cm.Name = "OLEDB ConnectionManager"  
    cm.ConnectionString = "Data Source=(local);" & _  
      "Initial Catalog=AdventureWorks;Provider=SQLOLEDB.1;" & _  
      "Integrated Security=SSPI;"  
  
    ' Add an OLE DB source to the data flow.  
    Dim component As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    component.Name = "OLEDBSource"  
    component.ComponentClassID = "DTSAdapter.OleDbSource.1"  
    ' You can also use the CLSID of the component instead of the PROGID.  
    'component.ComponentClassID = "{2C0A8BE5-1EDC-4353-A0EF-B778599C65A0}";  
  
    ' Get the design time instance of the component.  
    Dim instance As CManagedComponentWrapper = component.Instantiate()  
  
    ' Initialize the component.  
    instance.ProvideComponentProperties()  
  
    ' Specify the connection manager.  
    If component.RuntimeConnectionCollection.Count > 0 Then  
      component.RuntimeConnectionCollection(0).ConnectionManager = _  
        DtsConvert.GetExtendedInterface(package.Connections(0))  
      component.RuntimeConnectionCollection(0).ConnectionManagerID = _  
        package.Connections(0).ID  
    End If  
  
    ' Set the custom properties.  
    instance.SetComponentProperty("AccessMode", 2)  
    instance.SetComponentProperty("SqlCommand", _  
      "Select * from Production.Product")  
  
    ' Reinitialize the metadata.  
    instance.AcquireConnections(vbNull)  
    instance.ReinitializeMetaData()  
    instance.ReleaseConnections()  
  
    ' Add other components to the data flow and connect them.  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部資源  
 部落格文章： [EzAPI-已更新 SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223)，blogs.msdn.com 上。  

## <a name="see-also"></a>另請參閱  
 [以程式設計方式連接資料流程元件](../../integration-services/building-packages-programmatically/connecting-data-flow-components-programmatically.md)  
  
  

