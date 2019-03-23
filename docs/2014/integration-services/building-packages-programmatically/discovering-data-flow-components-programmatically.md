---
title: 以程式設計方式探索資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92cd83935ef4cb76c40aae0964100c7b88d847e4
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378256"
---
# <a name="discovering-data-flow-components-programmatically"></a>以程式設計方式探索資料流程元件
  在將資料流程工作加入封裝之後，下一步可能就是要判斷有哪些資料流程元件可供您使用。 您可以使用程式設計方式探索安裝在本機電腦上可供使用的資料流程來源、轉換和目的地。 如需將資料流程工作新增套件的資訊，請參閱[以程式設計方式新增資料流程工作](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md)。  
  
## <a name="discovering-components"></a>探索元件  
 <xref:Microsoft.SqlServer.Dts.Runtime.Application> 類別提供 <xref:Microsoft.SqlServer.Dts.Runtime.Application.PipelineComponentInfos%2A> 集合，其中包含每個正確安裝在本機電腦之元件的 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 物件。 每個 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo> 都包含元件的相關資訊，例如其名稱、描述和建立名稱。 當您將元件加入封裝時，可以使用在 <xref:Microsoft.SqlServer.Dts.Runtime.PipelineComponentInfo.CreationName%2A> 屬性中傳回的值，以設定 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ComponentClassID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性。  
  
## <a name="next-step"></a>下一個步驟  
 在探索可用的元件之後，下一個步驟是新增和設定元件，這將在下一主題中討論：[以程式設計方式新增資料流程元件](../building-packages-programmatically/adding-data-flow-components-programmatically.md)。  
  
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
  
![Integration Services 圖示 （小）](../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [以程式設計方式新增資料流程元件](../building-packages-programmatically/adding-data-flow-components-programmatically.md)  
  
  
