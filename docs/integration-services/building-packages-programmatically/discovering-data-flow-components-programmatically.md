---
title: "以程式設計方式探索資料流程元件 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: building-packages-programmatically
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
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
caps.latest.revision: "44"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ad91fc10f1799978de74207f8b3bfae79c4d22b1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="discovering-data-flow-components-programmatically"></a>以程式設計方式探索資料流程元件
  在將資料流程工作加入封裝之後，下一步可能就是要判斷有哪些資料流程元件可供您使用。 您可以使用程式設計方式探索安裝在本機電腦上可供使用的資料流程來源、轉換和目的地。 如需將資料流程工作新增套件的資訊，請參閱[以程式設計方式新增資料流程工作](../../integration-services/building-packages-programmatically/adding-the-data-flow-task-programmatically.md)。  
  
## <a name="discovering-components"></a>探索元件  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別提供 <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> 集合，其中包含每個正確安裝在本機電腦之元件的 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 物件。 每個 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 都包含元件的相關資訊，例如其名稱、描述和建立名稱。 當您將元件加入封裝時，可以使用在 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 屬性中傳回的值，以設定 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性。  
  
## <a name="next-step"></a>下一個步驟  
 在探索可用的元件之後，下一個步驟是新增和設定元件，這將在下一主題中討論：[以程式設計方式新增資料流程元件](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)。  
  
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
 [以程式設計方式新增資料流程元件](../../integration-services/building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  
