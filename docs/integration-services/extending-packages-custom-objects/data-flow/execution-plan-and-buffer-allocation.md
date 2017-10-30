---
title: "執行計劃和緩衝區配置 |Microsoft 文件"
ms.custom: 
ms.date: 03/04/2017
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
- custom data flow components [Integration Services], buffer allocations
- custom data flow components [Integration Services], execution plans
- buffer allocations [Integration Services]
- data flow components [Integration Services], buffer allocations
- data flow components [Integration Services], execution plans
- execution plans [Integration Services]
ms.assetid: 679d9ff0-641e-47c3-abb8-d1a7dcb279dd
caps.latest.revision: 40
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 931196de739980cb889f120b977b82bfb313ddd9
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="execution-plan-and-buffer-allocation"></a>執行計劃和緩衝區配置
  在執行之前，資料流程工作會檢查其元件並為元件的每個順序產生執行計劃。 本節提供有關執行計劃的詳細資料、如何檢視計劃以及輸入與輸出緩衝區如何根據執行計劃配置。  
  
## <a name="understanding-the-execution-plan"></a>了解執行計劃  
 任何執行計劃都包含來源執行緒與工作執行緒，而且每個執行緒都包含工作清單，以指定來源執行緒的輸出工作清單，或是工作執行緒的輸入與輸出工作清單。 執行計劃中的來源執行緒代表資料流程中之資料的來源元件和執行計畫中所識別*SourceThread**n*，其中 *n* 是以零為起始的來源執行緒數目。  
  
 每個來源執行緒會建立一個緩衝區、設定接聽程式，並且呼叫來源元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法。 這是執行開始和資料起源的地方，即來源元件開始將資料列加入資料流程工作所提供的輸出緩衝區。 在來源執行緒執行之後，會將工作平衡地散佈在工作執行緒之間。  
  
 工作執行緒可能包含兩個輸入和輸出工作清單，並在執行計劃，為識別*WorkThread**n*，其中 *n* 是以零為起始的工作執行緒數目。 當圖表包含具有非同步輸出的元件時，這些執行緒會包含輸出工作清單。  
  
 下列範例執行計劃代表一個資料流程，其中包含連接到轉換的來源元件，而該轉換則帶有連接到目的地元件的非同步輸出。 在此範例中，WorkThread0 包含輸出工作清單，因為轉換元件具有非同步輸出。  
  
```  
SourceThread0   
    Influences: 72 158   
    Output Work List   
        CreatePrimeBuffer of type 1 for output id 10   
        SetBufferListener: "WorkThread0" for input ID 73   
        CallPrimeOutput on component "OLE DB Source" (1)   
    End Output Work List   
    This thread drives 0 distributors   
End SourceThread0   
WorkThread0   
    Influences: 72 158   
    Input Work list, input ID 73   
        CallProcessInput on input ID 73 on component "Sort" (72) for view type 2   
    End Input Work list for input 73   
    Output Work List   
        CreatePrimeBuffer of type 3 for output id 74   
        SetBufferListener: "WorkThread1" for input ID 171with internal handoff   
        CallPrimeOutput on component "Sort" (72)   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread0   
WorkThread1   
    Influences: 158   
    Input Work list, input ID 171  
        CallProcessInput on input ID 171 on component "OLE DB Destination" (158) for view type 4  
    End Input Work list for input 171   
    Output Work List   
    End Output Work List   
    This thread drives 0 distributors   
End WorkThread1  
```  
  
> [!NOTE]  
>  執行計畫會產生每次封裝會執行，而且可以藉由新增到套件中，啟用記錄，並選取記錄提供者擷取**PipelineExecutionPlan**事件。  
  
## <a name="understanding-buffer-allocation"></a>了解緩衝區配置  
 根據執行計劃，資料流程工作會建立緩衝區，以包含資料流程元件的輸出中所定義的資料行。 當資料流經元件的順序時，會重複使用緩衝區，直到遇到非同步輸出的元件為止。 接著會建立新緩衝區，它包含非同步輸出的輸出資料行，以及下游元件的輸出資料行。  
  
 在執行期間，元件可以存取目前來源或是工作執行緒中的緩衝區。 緩衝區可能是由 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法所提供的輸入緩衝區，或是由 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法所提供的輸出緩衝區。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.Mode%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 屬性也可將每個緩衝區識別為輸入或是輸出緩衝區。  
  
 具有非同步輸出的轉換元件會從 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法接收現有輸入緩衝區，並從 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法接收新輸出緩衝區。 具有非同步輸出的轉換元件是唯一會接收輸入和輸出緩衝區的資料流程元件類型。  
  
 因為提供給元件的緩衝區可能包含的資料行多於元件具有在其輸入或輸出資料行集合中，元件開發人員可以呼叫<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A>方法，以在緩衝區中找出資料行，藉由指定其**LineageID**。  
  

