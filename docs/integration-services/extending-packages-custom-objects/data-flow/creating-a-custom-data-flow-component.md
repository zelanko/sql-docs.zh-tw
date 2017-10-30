---
title: "建立自訂資料流程元件 |Microsoft 文件"
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
- design-time component interface [Integration Services]
- custom data flow components [Integration Services], about data flow components
- custom data flow components [Integration Services]
- data flow components [Integration Services]
- data flow components [Integration Services], developing
ms.assetid: 9d96bcf5-eba8-44bd-b113-ed51ad0d0521
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 565a2b8e48537cea20a8e509cf5b6d7b59cc12f0
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="creating-a-custom-data-flow-component"></a>建立自訂資料流程元件
  在[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]，資料流程工作會公開物件模型，可讓開發人員建立自訂資料流程元件： 來源、 轉換和目的地 — 使用[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]和 managed 程式碼。  
  
 資料流程工作是由兩個元件所組成：<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面以及定義元件之間資料移動的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 物件之集合。  
  
> [!NOTE]  
>  建立自訂提供者時，您需要使用中繼資料資料行值更新 ProviderDescriptors.xml 檔。  
  
## <a name="design-time-and-run-time"></a>設計階段與執行階段  
 據說在執行之前，資料流程工作會設計狀態階段進行累加變更。 變更可包括元件的加入或移除、連接元件的路徑物件之加入或移除，以及對於元件中繼資料的變更。 當中繼資料變更發生時，元件可以監視變更並對其做出反應。 例如，元件可以不允許某些變更，或是做其他變更以回應變更。 在設計階段，設計工具會透過設計階段 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 介面與元件互動。  
  
 在執行時，資料流程工作會檢查元件的順序、準備執行計劃以及管理執行工作計劃的工作者執行緒集區。 雖然每個工作者執行緒都會執行資料流程工作內部的某些工作，但是工作者執行緒的主要工作是透過執行階段 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> 介面來呼叫元件的方法。  
  
## <a name="creating-a-component"></a>建立元件  
 若要建立資料流程元件，您可以從 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基底類別衍生類別、套用 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 類別，然後覆寫基底類別的適當方法。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 會實作 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100> 介面，並為您公開其方法以便在元件中覆寫。  
  
 視您的元件使用的物件而定，專案將需要參考下列組件的某些或是全部：  
  
|功能|要參考的組件|要匯入的命名空間|  
|-------------|---------------------------|-------------------------|  
|資料流程|Microsoft.SqlServer.PipelineHost|<xref:Microsoft.SqlServer.Dts.Pipeline>|  
|資料流程包裝函數|Microsoft.SqlServer.DTSPipelineWrap|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>|  
|執行階段|Microsoft.SQLServer.ManagedDTS|<xref:Microsoft.SqlServer.Dts.Runtime>|  
|執行階段包裝函數|Microsoft.SqlServer.DTSRuntimeWrap|<xref:Microsoft.SqlServer.Dts.Runtime.Wrapper>|  
  
 下列程式碼範例顯示從基底類別衍生的簡單元件，並套用 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>。 您需要加入 Microsoft.SqlServer.DTSPipelineWrap 組件的參考。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SampleComponent", ComponentType = ComponentType.Transform )]  
    public class BasicComponent: PipelineComponent  
    {  
        // TODO: Override the base class methods.  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(DisplayName:="SampleComponent", ComponentType:=ComponentType.Transform)> _  
Public Class BasicComponent  
  
    Inherits PipelineComponent  
  
    ' TODO: Override the base class methods.  
  
End Class  
```  
  
## <a name="see-also"></a>另請參閱  
 [開發資料流程元件的使用者介面](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
  
  

