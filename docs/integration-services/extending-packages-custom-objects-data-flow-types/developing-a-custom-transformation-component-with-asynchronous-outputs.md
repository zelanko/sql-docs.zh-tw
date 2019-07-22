---
title: 開發具有非同步輸出的自訂轉換元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], transformation components
- asynchronous outputs [Integration Services]
- ProcessInput method
- cache [Integration Services]
- buffer allocations [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], transformation components
ms.assetid: 1c3e92c7-a4fa-4fdd-b9ca-ac3069536274
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bb2f04e556d2ebdeb0776e112beb75aad9c637b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68026015"
---
# <a name="developing-a-custom-transformation-component-with-asynchronous-outputs"></a>開發具有非同步輸出的自訂轉換元件

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  當轉換在元件收到它的所有輸入資料列以前無法輸出資料料時，或是當轉換無法針對每一個收到的輸入資料列剛好產生一個輸出資料列時，您會使用非同步輸出。 例如，彙總轉換要等到讀取所有資料列以後，才能計算資料列的總和。 相反地，每當您在資料通過時修改每一個資料列時，都可以搭配同步輸出來使用元件。 您可以就地修改每一個資料列的資料，或是建立一或多個其他新的資料行，每一個資料行對於每一個輸入資料列都有一個值。 如需同步與非同步元件之間差異的詳細資訊，請參閱[了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 具有非同步輸出的轉換元件是唯一的，因為它們會同時當做目的地和來源元件。 這種元件會從上游元件收到資料列，並加入下游元件所耗用的資料列。 沒有其他資料流程元件會執行這兩種作業。  
  
 可供具有同步輸出之元件使用之上游元件中的資料行會自動提供給此元件的下游元件使用。 因此，具有同步輸出的元件不必定義任何輸出資料行，也可提供資料行和資料列給下一個元件。 就另一方面而言，具有非同步輸出的元件必須定義輸出資料行，並提供資料列給下游元件。 因此，具有非同步輸出的元件在設計和執行階段會有更多的工作要執行，而且元件開發人員會有更多的程式碼要實作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 包含數個具有非同步輸出的轉換。 例如，排序轉換會先要求它的所有資料列，然後才能加以排序，並使用非同步輸出達成這個結果。 當它收到所有資料列以後，它會加以排序並將其加入到輸出中。  
  
 本章節將詳細說明如何開發具有非同步輸出的轉換。 如需來源元件開發的詳細資訊，請參閱[開發自訂來源元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-source-component.md)。  
  
## <a name="design-time"></a>設計階段  
  
### <a name="creating-the-component"></a>建立元件  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 物件上的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 屬性會識別輸出為同步或非同步。 若要建立非同步輸出，請將輸出加入到元件中，並將 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 設定為零。 設定這個屬性也會決定資料流程工作是否會同時針對元件的輸入和輸出來配置 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 物件，或者是否會配置單一緩衝區並在兩個物件之間共用。  
  
 下列範例程式碼顯示一個元件，此元件會在它的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 實作中建立非同步輸出。  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "AsyncComponent",ComponentType = ComponentType.Transform)]  
    public class AsyncComponent : PipelineComponent  
    {  
        public override void ProvideComponentProperties()  
        {  
            // Call the base class, which adds a synchronous input  
            // and output.  
            base.ProvideComponentProperties();  
  
            // Make the output asynchronous.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
            output.SynchronousInputID = 0;  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="AsyncComponent", ComponentType:=ComponentType.Transform)> _  
Public Class AsyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Call the base class, which adds a synchronous input  
        ' and output.  
        Me.ProvideComponentProperties()  
  
        ' Make the output asynchronous.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
        output.SynchronousInputID = 0  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>建立和設定輸出資料行  
 如同之前所述，非同步元件會將資料行加入它的輸出資料行集合中，以提供資料行給下游元件。 根據元件的需求而定，有幾種設計階段方法可供選擇。 例如，如果您想要將上游元件中的所有資料行傳遞給下游元件，您會覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.OnInputPathAttached%2A> 方法來加入資料行，因為這是可供此元件使用之輸入資料行中的第一個方法。  
  
 如果此元件根據為其輸入選取的資料行來建立輸出資料行，請覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.SetUsageType%2A> 方法來選取輸出資料行，並指示將要如何使用這些資料行。  
  
 如果具有非同步輸出的元件根據上游元件中的資料行建立輸出資料行，而且可用的上游資料行變更了，則此元件應該更新它的輸出資料行集合。 此元件應該會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 期間偵測到這些變更，並在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 期間加以修正。  
  
> [!NOTE]  
>  當從輸出資料行集合中移除輸出資料行時，資料流程中參考此資料行的下游元件會受到負面的影響。 必須修復輸出資料行，而不能移除及重新建立此資料行，以免破壞下游元件。 例如，如果此資料行的資料類型已經變更，您必須更新資料類型。  
  
 下列程式碼範例示範一個元件，此元件會針對上游元件中可用的每一個資料行將輸出資料行加入它的輸出資料行集合中。  
  
```csharp  
public override void OnInputPathAttached(int inputID)  
{  
   IDTSInput100 input = ComponentMetaData.InputCollection.GetObjectByID(inputID);  
   IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
   IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
   foreach (IDTSVirtualInputColumn100 vCol in vInput.VirtualInputColumnCollection)  
   {  
      IDTSOutputColumn100 outCol = output.OutputColumnCollection.New();  
      outCol.Name = vCol.Name;  
      outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage);  
   }  
}  
```  
  
```vb  
Public Overrides Sub OnInputPathAttached(ByVal inputID As Integer)  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection.GetObjectByID(inputID)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
    Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput()  
  
    For Each vCol As IDTSVirtualInputColumn100 In vInput.VirtualInputColumnCollection  
  
        Dim outCol As IDTSOutputColumn100 = output.OutputColumnCollection.New()  
        outCol.Name = vCol.Name  
        outCol.SetDataTypeProperties(vCol.DataType, vCol.Length, vCol.Precision, vCol.Scale, vCol.CodePage)  
  
    Next  
End Sub  
```  
  
## <a name="run-time"></a>執行階段  
 具有非同步輸出的元件也會在執行階段執行一連串與其他元件類型不同的方法。 首先，它們是同時收到 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法呼叫的僅有元件。 具有非同步輸出的元件也會先要求所有內送資料列的存取權，然後才可以開始處理；因此，在已經讀取所有資料列以前，它們必須在內部快取輸入資料列。 最後，具有非同步輸出的元件會同時收到輸入緩衝區和輸出緩衝區，與其他元件不同。  
  
### <a name="understanding-the-buffers"></a>了解緩衝區  
 此元件會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 期間收到輸入緩衝區。 此緩衝區包含了由上游元件加入到緩衝區的資料列。 此緩衝區也包含元件輸入的資料行，同時還有之前在上游元件的輸出內所提供，但是未加入到非同步元件輸入集合中的資料行。  
  
 提供給 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 內之元件的輸出緩衝區一開始不包含資料列。 此元件會將資料列加入到這個緩衝區內，並在緩衝區已滿時將它提供給下游元件。 輸出緩衝區包含此元件的輸出資料行集合內所定義的資料行，同時還有其他下游元件已加入到其輸出內的任何資料行。  
  
 這個行為與具有同步輸出的元件不同，該元件會收到單一共用緩衝區。 具有同步輸出之元件的共用緩衝區包含了此元件的輸入和輸出資料行，同時還有加入到上游和下游元件之輸出中的資料行。  
  
### <a name="processing-rows"></a>處理資料列  
  
#### <a name="caching-input-rows"></a>快取輸入資料列  
 當您撰寫具有非同步輸出的元件時，您有三個選項可將資料列加入到輸出緩衝區。 您可以將它們當做收到的輸入資料列來加入，也可以快取它們，直到此元件收到上游元件中的所有資料列為止，或者可以在適合此元件的時機加入它們。 您所選擇的方法取決於此元件的需求。 例如，排序元件需要收到所有的上游資料列，然後才可加以排序。 因此，將資料列加入到輸出緩衝區以前，它會等候所有的資料列都已讀取。  
  
 此元件必須在內部快取輸入緩衝區內收到的資料列，直到準備處理這些資料列為止。 內送緩衝區資料列可以在資料表、多維度陣列或其他任何內部結構中快取。  
  
#### <a name="adding-output-rows"></a>加入輸出資料列  
 不論您在收到資料列時還是在收到所有資料列以後，將資料列加入到輸出緩衝區，您都可以在輸出緩衝區上呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.AddRow%2A> 方法來這樣做。 當您加入此資料列以後，您會在新的資料列中設定每一個資料行的值。  
  
 因為輸出緩衝區中的資料行有時會多於此元件之輸出資料行集合中的資料行，所以您必須先找出緩衝區內適當資料行的索引，然後才可以設定它的值。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 屬性的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 方法會傳回緩衝區資料列中具有指定之歷程識別碼的資料行索引，然後會用它來將此值指派給緩衝區資料行。  
  
 在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PrimeOutput%2A> 方法以前所呼叫的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法是 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 屬性可用時的第一個方法，以及在輸入和輸出緩衝區內尋找資料行之索引的第一個機會。  
  
## <a name="sample"></a>範例  
 下列範例顯示具有非同步輸出的簡單轉換元件，該元件會將收到的資料列加入到輸出緩衝區。 這個範例並未示範本主題中討論的所有方法與功能。 而是示範每個具有非同步輸出的自訂轉換元件必須覆寫的重要方法，但是並不包含設計階段驗證的程式碼。 此外，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 中的程式碼會假設輸出資料行集合針對輸入資料行集合中的每一個資料行都有一個資料行。  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
   [DtsPipelineComponent(DisplayName = "AsynchronousOutput")]  
   public class AsynchronousOutput : PipelineComponent  
   {  
      PipelineBuffer outputBuffer;  
      int[] inputColumnBufferIndexes;  
      int[] outputColumnBufferIndexes;  
  
      public override void ProvideComponentProperties()  
      {  
         // Let the base class add the input and output objects.  
         base.ProvideComponentProperties();  
  
         // Name the input and output, and make the  
         // output asynchronous.  
         ComponentMetaData.InputCollection[0].Name = "Input";  
         ComponentMetaData.OutputCollection[0].Name = "AsyncOutput";  
         ComponentMetaData.OutputCollection[0].SynchronousInputID = 0;  
      }  
      public override void PreExecute()  
      {  
         IDTSInput100 input = ComponentMetaData.InputCollection[0];  
         IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
         inputColumnBufferIndexes = new int[input.InputColumnCollection.Count];  
         outputColumnBufferIndexes = new int[output.OutputColumnCollection.Count];  
  
         for (int col = 0; col < input.InputColumnCollection.Count; col++)  
            inputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection[col].LineageID);  
  
         for (int col = 0; col < output.OutputColumnCollection.Count; col++)  
            outputColumnBufferIndexes[col] = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection[col].LineageID);  
  
      }  
  
      public override void PrimeOutput(int outputs, int[] outputIDs, PipelineBuffer[] buffers)  
      {  
         if (buffers.Length != 0)  
            outputBuffer = buffers[0];  
      }  
      public override void ProcessInput(int inputID, PipelineBuffer buffer)  
      {  
            // Advance the buffer to the next row.  
            while (buffer.NextRow())  
            {  
               // Add a row to the output buffer.  
               outputBuffer.AddRow();  
               for (int x = 0; x < inputColumnBufferIndexes.Length; x++)  
               {  
                  // Copy the data from the input buffer column to the output buffer column.  
                  outputBuffer[outputColumnBufferIndexes[x]] = buffer[inputColumnBufferIndexes[x]];  
               }  
            }  
         if (buffer.EndOfRowset)  
         {  
            // EndOfRowset on the input buffer is true.  
            // Set EndOfRowset on the output buffer.  
            outputBuffer.SetEndOfRowset();  
         }  
      }  
   }  
}  
```  
  
```vb  
Imports System  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper  
  
Namespace Microsoft.Samples.SqlServer.Dts  
  
    <DtsPipelineComponent(DisplayName:="AsynchronousOutput")> _  
    Public Class AsynchronousOutput  
  
        Inherits PipelineComponent  
  
        Private outputBuffer As PipelineBuffer  
        Private inputColumnBufferIndexes As Integer()  
        Private outputColumnBufferIndexes As Integer()  
  
        Public Overrides Sub ProvideComponentProperties()  
  
            ' Let the base class add the input and output objects.  
            Me.ProvideComponentProperties()  
  
            ' Name the input and output, and make the  
            ' output asynchronous.  
            ComponentMetaData.InputCollection(0).Name = "Input"  
            ComponentMetaData.OutputCollection(0).Name = "AsyncOutput"  
            ComponentMetaData.OutputCollection(0).SynchronousInputID = 0  
        End Sub  
  
        Public Overrides Sub PreExecute()  
  
            Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
            Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
            ReDim inputColumnBufferIndexes(input.InputColumnCollection.Count)  
            ReDim outputColumnBufferIndexes(output.OutputColumnCollection.Count)  
  
            For col As Integer = 0 To input.InputColumnCollection.Count  
                inputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(input.Buffer, input.InputColumnCollection(col).LineageID)  
            Next  
  
            For col As Integer = 0 To output.OutputColumnCollection.Count  
                outputColumnBufferIndexes(col) = BufferManager.FindColumnByLineageID(output.Buffer, output.OutputColumnCollection(col).LineageID)  
            Next  
  
        End Sub  
        Public Overrides Sub PrimeOutput(ByVal outputs As Integer, ByVal outputIDs As Integer(), ByVal buffers As PipelineBuffer())  
  
            If buffers.Length <> 0 Then  
                outputBuffer = buffers(0)  
            End If  
  
        End Sub  
  
        Public Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)  
  
                ' Advance the buffer to the next row.  
                While (buffer.NextRow())  
  
                    ' Add a row to the output buffer.  
                    outputBuffer.AddRow()  
                    For x As Integer = 0 To inputColumnBufferIndexes.Length  
  
                        ' Copy the data from the input buffer column to the output buffer column.  
                        outputBuffer(outputColumnBufferIndexes(x)) = buffer(inputColumnBufferIndexes(x))  
  
                    Next  
                End While  
  
            If buffer.EndOfRowset = True Then  
                ' EndOfRowset on the input buffer is true.  
                ' Set the end of row set on the output buffer.  
                outputBuffer.SetEndOfRowset()  
            End If  
        End Sub  
    End Class  
End Namespace  
```  
  
## <a name="see-also"></a>另請參閱  
 [開發具有同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md)   
 [了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [使用指令碼元件建立非同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-an-asynchronous-transformation-with-the-script-component.md)  
  
  
