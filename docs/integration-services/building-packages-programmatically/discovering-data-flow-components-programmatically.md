---
title: "以程式設計方式探索資料流程元件 |Microsoft 文件"
ms.custom: 
ms.date: 03/03/2017
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
- PipelineComponentInfos collection
- data flow task [Integration Services], components
- discovering data flow components
- components [Integration Services], data flow
- data flow [Integration Services], components
ms.assetid: ff92a96a-8af6-4532-82cc-c0bbff92401b
caps.latest.revision: 44
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 78090618d5025a6ab29c888d09db44ddfff278fa
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="discovering-data-flow-components-programmatically"></a>以程式設計方式探索資料流程元件
  在將資料流程工作加入封裝之後，下一步可能就是要判斷有哪些資料流程元件可供您使用。 您可以使用程式設計方式探索安裝在本機電腦上可供使用的資料流程來源、轉換和目的地。 將資料流程工作加入封裝的相關資訊，請參閱[資料資料流程工作以程式設計方式加入](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)。  
  
## <a name="discovering-components"></a>探索元件  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別提供 <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> 集合，其中包含每個正確安裝在本機電腦之元件的 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 物件。 每個 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 都包含元件的相關資訊，例如其名稱、描述和建立名稱。 當您將元件加入封裝時，可以使用在 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 屬性中傳回的值，以設定 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性。  
  
## <a name="next-step"></a>下一個步驟  
 可用的元件之後下, 一個步驟是加入和設定元件，在下一個主題中，討論[加入資料資料流程元件以程式設計方式](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)。  
  
## <a name="sample"></a>範例  
 下列程式碼範例會示範如何列舉 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfos> 物件的 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 集合，以程式設計方式探索在本機電腦上可用的資料流程元件。 這個範例需要 Microsoft.SqlServer.ManagedDTS 組件的參考。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Application application = new Application();  
      PipelineComponentInfos componentInfos = application.PipelineComponentInfos;  
  
      foreach (PipelineComponentInfo componentInfo in componentInfos)  
      {  
        Console.WriteLine("Name: " + componentInfo.Name + "\n" +  
          " CreationName: " + componentInfo.CreationName + "\n");  
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
  
    Dim application As Application = New Application()  
  
    Dim componentInfos As PipelineComponentInfos = application.PipelineComponentInfos  
  
    For Each componentInfo As PipelineComponentInfo In componentInfos  
      Console.WriteLine("Name: " & componentInfo.Name & vbCrLf & _  
        " CreationName: " & componentInfo.CreationName & vbCrLf)  
    Next  
  
    Console.Read()  
  
  End Sub  
  
End Module  
```
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式加入資料流程元件](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  

