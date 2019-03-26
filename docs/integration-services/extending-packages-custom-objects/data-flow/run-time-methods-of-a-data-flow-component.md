---
title: 資料流程元件的執行階段方法 | Microsoft Docs
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
- run-time [Integration Services]
- data flow components [Integration Services], run-time methods
ms.assetid: fd9e4317-18dd-43af-bbdc-79db32183ac4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 945b92c5f73ad139b79f66e4ca2aeccdb1aabdb7
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/20/2019
ms.locfileid: "58277147"
---
# <a name="run-time-methods-of-a-data-flow-component"></a>資料流程元件的執行階段方法
  在執行階段，資料流程工作會檢查元件的順序、準備執行計畫，以及管理執行工作計畫的工作者執行緒集區。 此工作會從來源載入資料列、透過轉換處理它們，然後將它們儲存到目的地。  
  
## <a name="sequence-of-method-execution"></a>方法執行的順序  
 在資料流程元件的執行期間，會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基底類別中的方法子集。 方法與呼叫方法的順序永遠都是相同的，但 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法例外。 會根據元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 物件之存在與否及組態來呼叫這兩個方法。  
  
 下列清單按照元件執行期間呼叫方法的順序來顯示它們。 請注意，在呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 時，永遠會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 的前面呼叫它。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrepareForExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.AcquireConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PostExecute%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReleaseConnections%2A>  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Cleanup%2A>  
  
### <a name="primeoutput-method"></a>PrimeOutput 方法  
 當元件至少有一個輸出透過 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> 物件附加至下游元件，而且輸出的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 屬性是零時，便會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 方法。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.PrimeOutput%2A> 方法是針對來源元件以及具有非同步輸出的轉換所呼叫。 與以下所述的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法不同的是，每個需要 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法的元件都只會呼叫它一次。  
  
### <a name="processinput-method"></a>ProcessInput 方法  
 如果元件至少有一個輸入是由 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> 物件附加至上游元件，則會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSPath100> 方法。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSRuntimeComponent100.ProcessInput%2A> 方法是針對目的地元件以及具有同步輸出的轉換所呼叫。 會重複呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>，直到不再從上游元件處理資料列為止。  
  
## <a name="working-with-inputs-and-outputs"></a>處理輸入和輸出  
 在執行階段，資料流程元件會執行下列工作：  
  
-   來源元件會加入資料列。  
  
-   具有同步輸出的轉換元件會接收來源元件所提供的資料列。  
  
-   具有非同步輸出的轉換元件會接收資料列並加入資料列。  
  
-   目的地元件會接收資料列，然後將它們載入目的地中。  
  
 在執行期間，資料流程工作會配置 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 物件，這些物件包含定義在元件序列之輸出資料行集合中的所有資料行。 例如，如果資料流程序列中四個元件的每一個都會將一個輸出資料行加入至其輸出資料行集合，則提供給每個元件的緩衝區都會包含四個資料行，其中每個元件的每個輸出資料行都有一個資料行。 因為這個行為的緣故，元件有時會接收包含未使用之資料行的緩衝區。  
  
 因為元件所接收的緩衝區可能包含此元件將不會使用的資料行，所以您必須在資料流程工作提供給此元件的緩衝區中，找到要在元件的輸入與輸出資料行集合中使用的資料行。 您可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 屬性的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 方法來完成這項動作。 基於效能的考量，這個工作通常會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法期間執行，而不是在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 中執行。  
  
 在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法之前，會先呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>，而且是在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 變成可供元件使用之後，元件第一次有機會執行這個工作。 在這個方法期間，元件應該在緩衝區中找到其資料行，並在內部儲存這項資訊，以便在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法中可以使用這些資料行。  
  
 下列程式碼範例示範在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期間，具有同步輸出的轉換元件如何在緩衝區中找到其輸入資料行。  
  
```csharp  
private int []bufferColumnIndex;  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    bufferColumnIndex = new int[input.InputColumnCollection.Count];  
  
    for( int x=0; x < input.InputColumnCollection.Count; x++)  
    {  
        IDTSInputColumn100 column = input.InputColumnCollection[x];  
        bufferColumnIndex[x] = BufferManager.FindColumnByLineageID( input.Buffer, column.LineageID);  
    }  
}  
```  
  
```vb  
Dim bufferColumnIndex As Integer()  
  
    Public Overrides Sub PreExecute()  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
  
        ReDim bufferColumnIndex(input.InputColumnCollection.Count)  
  
        For x As Integer = 0 To input.InputColumnCollection.Count  
  
            Dim column As IDTSInputColumn100 = input.InputColumnCollection(x)  
            bufferColumnIndex(x) = BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID)  
  
        Next  
  
    End Sub  
```  
  
### <a name="adding-rows"></a>加入資料列  
 透過將資料列加入至 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 物件，元件會提供資料列給下游元件。 資料流程工作會提供輸出緩衝區的陣列，每個連接至下游元件的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 物件都有一個輸出緩衝區，以做為 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法的參數。 具有非同步輸出的來源元件與轉換元件會將資料列加入至緩衝區，並且會在完成加入資料列時呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> 方法。 資料流程工作會管理提供給元件的輸出緩衝區，而當緩衝區變成完整時，便會自動將緩衝區中的資料列移到下一個元件。 每個元件都會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法一次，不像 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法一樣重複呼叫。  
  
 下列程式碼範例示範在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法期間，元件會如何將資料列加入至其輸出緩衝區，然後呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.SetEndOfRowset%2A> 方法。  
  
```csharp  
public override void PrimeOutput( int outputs, int []outputIDs,PipelineBuffer []buffers)  
{  
    for( int x=0; x < outputs; x++ )  
    {  
        IDTSOutput100 output = ComponentMetaData.OutputCollection.GetObjectByID( outputIDs[x]);  
        PipelineBuffer buffer = buffers[x];  
  
        // TODO: Add rows to the output buffer.  
    }  
    foreach( PipelineBuffer buffer in buffers )  
    {  
        /// Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset();  
    }  
}  
```  
  
```vb  
public overrides sub PrimeOutput( outputs as Integer , outputIDs() as Integer ,buffers() as PipelineBuffer buffers)  
  
    For x As Integer = 0 To outputs.MaxValue  
  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.GetObjectByID(outputIDs(x))  
        Dim buffer As PipelineBuffer = buffers(x)  
  
        ' TODO: Add rows to the output buffer.  
  
    Next  
  
    For Each buffer As PipelineBuffer In buffers  
  
        ' Notify the data flow task that no more rows are coming.  
        buffer.SetEndOfRowset()  
  
    Next  
  
End Sub  
```  
  
 如需開發將資料列新增至輸出緩衝區之元件的詳細資訊，請參閱[開發自訂來源元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)和[開發具有非同步輸出的自訂轉換元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)。  
  
### <a name="receiving-rows"></a>接收資料列  
 元件會從 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 物件中的上游元件接收資料列。 資料流程工作會提供 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 物件，該物件包含上游元件以 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法的參數形式加入至資料流程的資料列。 這個輸入緩衝區可用以檢查和修改緩衝區中的資料列與資料行，但是無法用以加入或是移除資料列。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法會重複呼叫，直到沒有其他可用的緩衝區為止。 上次呼叫它時，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性是 **true**。 您可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> 方法，使緩衝區前進到下一個資料列，以逐一查看緩衝區中的資料列集合。 當緩衝區位於集合中的最後一個資料列時，此方法會傳回 **false**。 除非您在已處理最後一個資料列之後還必須執行其他動作，否則不必檢查 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性。  
  
 下列文字將示範使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.NextRow%2A> 方法和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性的正確模式：  
  
 `while (buffer.NextRow())`  
  
 `{`  
  
 `// Do something with each row.`  
  
 `}`  
  
 `if (buffer.EndOfRowset)`  
  
 `{`  
  
 `// Optionally, do something after all rows have been processed.`  
  
 `}`  
  
 下列程式碼範例示範元件如何在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法期間，處理輸入緩衝區中的資料列。  
  
```csharp  
public override void ProcessInput( int inputID, PipelineBuffer buffer )  
{  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
        while( buffer.NextRow())  
        {  
            // TODO: Examine the columns in the current row.  
        }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
        While buffer.NextRow() = True  
  
            ' TODO: Examine the columns in the current row.  
        End While  
  
End Sub  
```  
  
 如需開發接收輸入緩衝區中資料列之元件的詳細資訊，請參閱[開發自訂目的地元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-destination-component.md)和[開發具有同步輸出的自訂轉換元件](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程元件的設計階段方法](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
  
  
