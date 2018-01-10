---
title: "以程式設計方式新增資料流程工作 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- adding Data Flow task
- SSIS data flow
- data flow task [Integration Services], adding
- MainPipe object
ms.assetid: 0ca03712-a82e-4aa7-949b-f869a8936ddf
caps.latest.revision: "48"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb4f50bd43c697c843141849905ce72047fa4b48
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/08/2018
---
# <a name="adding-the-data-flow-task-programmatically"></a>以程式設計方式加入資料流程工作
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 包括稱為「資料流程」工作的一項工作，該工作是由物件模型中的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper> 命名空間所表示。 「資料流程」工作是一項特殊且高效能的工作，專門用來在封裝執行期間轉換及移動資料。 就像其他工作一樣，「資料流程」工作是由 <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost> 物件所包裝，而且從執行階段引擎的觀點來看，這項工作只是封裝內的另一項工作。 但是，此資料流程包含了其他稱為資料流程元件的物件。 這些元件是讓資料從來源移到目的地的元件，有時是透過轉換。 這些元件會定義移動的方向及轉換資料的方式。 設定「資料流程」工作牽涉到在此工作中加入元件，然後連接這些元件來建立資料流程，並達成所要的轉換。  
  
 「資料流程」工作內有三種類型的元件：[資料流程來源]、[資料流程轉換] 和 [資料流程目的地]，這些元件會依照這個順序顯示在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 設計師工具箱內。 這些類型也可以更簡單地稱為來源、轉換或目的地。 如同名稱所指示，資料會從來源流向轉換，然後再流向目的地。 這是過於簡單的資料流程描述，目的是要說明此概念，但是「資料流程」工作更具彈性而且功能非常強大，足以處理多個來源，並將傳送輸出給多個目的地的許多轉換連接在一起。  
  
 「資料流程」工作會加入到封裝中，其方式就像是加入其他工作一樣。 當加入此工作之後，會進行設定，其方式是將元件加入到資料流程工作中，然後在此工作中設定及連接元件。  
  
## <a name="sample"></a>範例  
 下列程式碼範例示範如何將「資料流程」工作加入到封裝。 此範例需要參考 Microsoft.SqlServer.PipelineHost、Microsoft.SqlServer.DTSPipelineWrap 和 Microsoft.SqlServer.ManagedDTS 組件。  
  
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
      Package p = new Package();  
      Executable e = p.Executables.Add("STOCK:PipelineTask");  
      TaskHost thMainPipe = e as TaskHost;  
      MainPipe dataFlowTask = thMainPipe.InnerObject as MainPipe;   
    }  
  }  
}  
```  
  
```vb  
Imports System.IO  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
    Dim e As Executable = p.Executables.Add("STOCK:PipelineTask")  
    Dim thMainPipe As TaskHost = CType(e, TaskHost)  
    Dim dataFlowTask As MainPipe = CType(thMainPipe.InnerObject, MainPipe)  
  
  End Sub  
  
End Module  
```  
  
## <a name="external-resources"></a>外部資源  
 blogs.msdn.com 上的部落格文章：[EzAPI – Updated for SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=243223) (EzAPI - 針對 SQL Server 2012 更新)。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式探索資料流程元件](../../integration-services/building-packages-programmatically/discovering-data-flow-components-programmatically.md)  
  
  
