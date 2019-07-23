---
title: 以程式設計的方式連線資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], components
- paths [Integration Services], components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: 404ecab7-7698-447b-93d6-dd256beb11ff
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a85214d54b533918a2328aab74c16fc18fcb3cd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68052181"
---
# <a name="connecting-data-flow-components-programmatically"></a>以程式設計的方式連接資料流程元件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  在將元件加入資料流程工作後，就可以連接元件以建立執行樹狀目錄，以代表從來源經過轉換到目的地的資料流程。 您使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 物件以連接資料流程中的元件。  
  
## <a name="creating-a-path"></a>建立路徑  
 呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipe> 介面中 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.MainPipeClass.PathCollection%2A> 屬性的 New 方法，以建立新路徑並將它新增資料流程工作中的路徑集合。 此方法會傳回中斷連接的新 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 物件，您可用以連接兩個元件。  
  
 呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100.AttachPathAndPropagateNotifications%2A> 方法以連接路徑並通知元件參與已連接它們的路徑。 這個方法會以參數的方式接受上游元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100>以及下游元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>。 依預設，呼叫元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法會為具有輸入的元件建立單一輸入，並為具有輸出的元件建立單一輸出。 下列範例使用目的地之來源與輸入的這個預設輸出。  
  
## <a name="next-step"></a>下一個步驟  
 在您建立兩個元件之間的路徑之後，下一個步驟就是要對應下游元件中的輸入資料行，這將在下一主題中討論：[以程式設計方式選取輸入資料行](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)。  
  
## <a name="sample"></a>範例  
 下列程式碼範例示範如何在兩個元件之間建立路徑。  
  
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
      Package package = new Package();  
      Executable e = package.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;  
  
      // Create the source component.    
      IDTSComponentMetaData100 source =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      source.ComponentClassID = "DTSAdapter.OleDbSource";  
      CManagedComponentWrapper srcDesignTime = source.Instantiate();  
      srcDesignTime.ProvideComponentProperties();  
  
      // Create the destination component.  
      IDTSComponentMetaData100 destination =  
        dataFlowTask.ComponentMetaDataCollection.New();  
      destination.ComponentClassID = "DTSAdapter.OleDbDestination";  
      CManagedComponentWrapper destDesignTime = destination.Instantiate();  
      destDesignTime.ProvideComponentProperties();  
  
      // Create the path.  
      IDTSPath100 path = dataFlowTask.PathCollection.New();  
      path.AttachPathAndPropagateNotifications(source.OutputCollection[0],  
        destination.InputCollection[0]);  
    }  
  }  
```  
  
 }  
  
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
  
    ' Create the source component.    
    Dim source As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    source.ComponentClassID = "DTSAdapter.OleDbSource"  
    Dim srcDesignTime As CManagedComponentWrapper = source.Instantiate()  
    srcDesignTime.ProvideComponentProperties()  
  
    ' Create the destination component.  
    Dim destination As IDTSComponentMetaData100 = _  
      dataFlowTask.ComponentMetaDataCollection.New()  
    destination.ComponentClassID = "DTSAdapter.OleDbDestination"  
    Dim destDesignTime As CManagedComponentWrapper = destination.Instantiate()  
    destDesignTime.ProvideComponentProperties()  
  
    ' Create the path.  
    Dim path As IDTSPath100 = dataFlowTask.PathCollection.New()  
    path.AttachPathAndPropagateNotifications(source.OutputCollection(0), _  
      destination.InputCollection(0))  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式選取輸入資料行](../../integration-services/building-packages-programmatically/selecting-input-columns-programmatically.md)  
  
  
