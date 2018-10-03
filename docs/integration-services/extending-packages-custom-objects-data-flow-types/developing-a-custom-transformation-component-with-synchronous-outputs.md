---
title: 開發具有同步輸出的自訂轉換元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
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
- ProcessInput method
- buffer allocations [Integration Services]
- synchronous outputs [Integration Services]
- transformation components [Integration Services]
- output columns [Integration Services]
- data flow components [Integration Services], transformation components
ms.assetid: b694d21f-9919-402d-9192-666c6449b0b7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e5aac894abea70c3612b2ec053556718348313f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47694456"
---
# <a name="developing-a-custom-transformation-component-with-synchronous-outputs"></a>開發具有同步輸出的自訂轉換元件
  具有同步輸出的轉換元件會從上游元件接收資料列，並在傳遞資料列給下游元件時，讀取或是修改這些資料列之資料行中的值。 它們也必須定義從上游元件提供的資料行所衍生之其他輸出資料行，但是它們不需要將資料列加入資料流程。 如需同步與非同步元件之間差異的詳細資訊，請參閱[了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)。  
  
 這種元件適用於將資料提供給元件時以內嵌方式修改資料的工作，以及元件不必看到所有的資料列就能處理它們的工作。 它是最容易開發的元件，因為具有同步輸出的轉換通常不會連接至外部資料來源、管理外部中繼資料行，或是將資料列加入輸出緩衝區。  
  
 建立具有同步輸出的轉換元件需要加入含有為元件選取的上游資料行之 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSInput100>，以及可能包含由元件建立的衍生資料行之 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100> 物件。 建立的過程也包括實作設計階段方法，並提供執行期間在內送緩衝區資料列中讀取或修改資料行的程式碼。  
  
 本節提供實作自訂轉換元件所需的資訊，並提供程式碼範例以協助您更加了解概念。  
  
## <a name="design-time"></a>設計階段  
 這個元件的設計階段程式碼需要建立輸入和輸出，加入元件產生的任何其他輸出資料行，並驗證元件的組態。  
  
### <a name="creating-the-component"></a>建立元件  
 元件的輸入、輸出和自訂屬性通常會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法期間建立。 有兩種方法可以加入具有同步輸出的轉換元件之輸入和輸出。 您可以使用該方法的基底類別實作，然後修改它建立的預設輸入和輸出，或者可以自己明確地加入輸入與輸出。  
  
 下列程式碼範例顯示 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 的實作，以明確地加入輸入和輸出物件。 註解中包含的對基底類別的呼叫也可以完成同一件事情。  
  
```csharp  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.Samples.SqlServer.Dts  
{  
    [DtsPipelineComponent(DisplayName = "SynchronousComponent", ComponentType = ComponentType.Transform)]  
    public class SyncComponent : PipelineComponent  
    {  
  
        public override void ProvideComponentProperties()  
        {  
            // Add the input.  
            IDTSInput100 input = ComponentMetaData.InputCollection.New();  
            input.Name = "Input";  
  
            // Add the output.  
            IDTSOutput100 output = ComponentMetaData.OutputCollection.New();  
            output.Name = "Output";  
            output.SynchronousInputID = input.ID;  
  
            // Alternatively, you can let the base class add the input and output  
            // and set the SynchronousInputID of the output to the ID of the input.  
            // base.ProvideComponentProperties();  
        }  
    }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
Imports Microsoft.SqlServer.Dts.Runtime  
  
<DtsPipelineComponent(DisplayName:="SynchronousComponent", ComponentType:=ComponentType.Transform)> _  
Public Class SyncComponent  
    Inherits PipelineComponent  
  
    Public Overrides Sub ProvideComponentProperties()  
  
        ' Add the input.  
        Dim input As IDTSInput100 = ComponentMetaData.InputCollection.New()  
        input.Name = "Input"  
  
        ' Add the output.  
        Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection.New()  
        output.Name = "Output"  
        output.SynchronousInputID = Input.ID  
  
        ' Alternatively, you can let the base class add the input and output  
        ' and set the SynchronousInputID of the output to the ID of the input.  
        ' base.ProvideComponentProperties();  
  
    End Sub  
  
End Class  
```  
  
### <a name="creating-and-configuring-output-columns"></a>建立和設定輸出資料行  
 雖然具有同步輸出的轉換元件不會將資料列加入緩衝區，但是它們可能會將額外的輸出資料行加入其輸出。 一般而言，當元件加入輸出資料行時，會在執行階段從上游元件提供給該元件之一或多個資料行所含的資料中，衍生新輸出資料行的值。  
  
 在建立輸出資料行之後，必須設定其資料類型屬性。 設定輸出資料行的資料類型屬性需要特殊的處理，而且是透過呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.SetDataTypeProperties%2A> 方法來執行。 這個方法是必要的，因為 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Length%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.Precision%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.CodePage%2A> 屬性每個都是唯讀的，而且每個屬性都與另一個屬性的設定相依。 這個方法保證以一致的方式設定屬性值，而且資料流程工作會驗證它們是否已正確設定。  
  
 資料行的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> 會決定為其他屬性設定的值。 下表顯示每個 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.DataType%2A> 的相依屬性之需求。 未列出的資料類型會將其相依屬性設定為零。  
  
|DataType|長度|小數位數|有效位數|CodePage|  
|--------------|------------|-----------|---------------|--------------|  
|DT_DECIMAL|0|大於 0，且小於或等於 28。|0|0|  
|DT_CY|0|0|0|0|  
|DT_NUMERIC|0|大於 0、小於或等於 28，且小於有效位數 (Precision)。|大於或等於 1，且小於或等於 38。|0|  
|DT_BYTES|大於 0。|0|0|0|  
|DT_STR|大於 0 且小於 8000。|0|0|非 0，並為有效的字碼頁。|  
|DT_WSTR|大於 0，且小於 4000。|0|0|0|  
  
 由於資料類型屬性的限制會以輸出資料行的資料類型為準，因此在使用 Managed 類型時，必須選擇正確的 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 資料類型。 基底類別提供三種 Helper 方法：<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ConvertBufferDataTypeToFitManaged%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferTypeToDataRecordType%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.DataRecordTypeToBufferType%2A>，可協助 Managed 元件開發人員在有提供 Managed 類型時，選取 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型。 這些方法會將 Managed 資料類型轉換為 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 資料類型，反之亦然。  
  
## <a name="run-time"></a>執行階段  
 一般而言，元件之執行階段部分的實作可分成兩項工作：在緩衝區中尋找元件的輸入與輸出資料行，以及在內送緩衝區資料列中讀取或寫入這些資料行的值。  
  
### <a name="locating-columns-in-the-buffer"></a>找出緩衝區中的資料行  
 在執行期間提供給元件的緩衝區中之資料行數目，有可能超過元件之輸入或輸出集合中的資料行數目。 這是因為每個緩衝區都包含資料流程的元件中定義的所有輸出資料行。 為了確保緩衝區資料行正確地符合輸入或輸出的資料行，元件開發人員必須使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSBufferManager100.FindColumnByLineageID%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 方法。 這個方法會使用資料行的歷程識別碼來尋找指定緩衝區中的資料行。 一般而言，會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期間找到資料行，因為這是 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.BufferManager%2A> 屬性變成可用的第一個執行階段方法。  
  
 下列程式碼範例示範在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期間，於其輸入與輸出資料行集合中找到資料行索引的元件。 資料行索引是儲存在整數陣列中，而且在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 期間可以讓元件存取。  
  
```csharp  
int []inputColumns;  
int []outputColumns;  
  
public override void PreExecute()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSOutput100 output = ComponentMetaData.OutputCollection[0];  
  
    inputColumns = new int[input.InputColumnCollection.Count];  
    outputColumns = new int[output.OutputColumnCollection.Count];  
  
    for(int col=0; col < input.InputColumnCollection.Count; col++)  
    {  
        IDTSInputColumn100 inputColumn = input.InputColumnCollection[col];  
        inputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID);  
    }  
  
    for(int col=0; col < output.OutputColumnCollection.Count; col++)  
    {  
        IDTSOutputColumn100 outputColumn = output.OutputColumnCollection[col];  
        outputColumns[col] = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID);  
    }  
  
}  
```  
  
```vb  
Public Overrides Sub PreExecute()  
  
    Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)  
    Dim output As IDTSOutput100 = ComponentMetaData.OutputCollection(0)  
  
    ReDim inputColumns(input.InputColumnCollection.Count)  
    ReDim outputColumns(output.OutputColumnCollection.Count)  
  
    For col As Integer = 0 To input.InputColumnCollection.Count  
  
        Dim inputColumn As IDTSInputColumn100 = input.InputColumnCollection(col)  
        inputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, inputColumn.LineageID)  
    Next  
  
    For col As Integer = 0 To output.OutputColumnCollection.Count  
  
        Dim outputColumn As IDTSOutputColumn100 = output.OutputColumnCollection(col)  
        outputColumns(col) = BufferManager.FindColumnByLineageID(input.Buffer, outputColumn.LineageID)  
    Next  
  
End Sub  
```  
  
### <a name="processing-rows"></a>處理資料列  
 元件會接收 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer> 方法中包含資料列與資料行的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 物件。 在這個方法期間會反覆運算緩衝區中的資料列，而且會在讀取和修改 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 期間識別資料行。 資料流程工作會重複呼叫該方法，直到不再從上游元件提供其他資料列為止。  
  
 透過使用陣列索引子存取方法，或是透過使用其中一個 **Get** 或 **Set** 方法，會讀取或寫入緩衝區中的個別資料行。 在已知緩衝區內資料行的資料類型時，應該使用較有效率的 **Get** 和 **Set** 方法。  
  
 下列程式碼範例顯示處理內送資料列的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法之實作。  
  
```csharp  
public override void ProcessInput( int InputID, PipelineBuffer buffer)  
{  
       while( buffer.NextRow())  
       {  
            for(int x=0; x < inputColumns.Length;x++)  
            {  
                if(!buffer.IsNull(inputColumns[x]))  
                {  
                    object columnData = buffer[inputColumns[x]];  
                    // TODO: Modify the column data.  
                    buffer[inputColumns[x]] = columnData;  
                }  
            }  
  
      }  
}  
```  
  
```vb  
Public Overrides Sub ProcessInput(ByVal InputID As Integer, ByVal buffer As PipelineBuffer)  
  
        While (buffer.NextRow())  
  
            For x As Integer = 0 To inputColumns.Length  
  
                if buffer.IsNull(inputColumns(x)) = false then  
  
                    Dim columnData As Object = buffer(inputColumns(x))  
                    ' TODO: Modify the column data.  
                    buffer(inputColumns(x)) = columnData  
  
                End If  
            Next  
  
        End While  
End Sub  
```  
  
## <a name="sample"></a>範例  
 下列範例顯示具有同步輸出的簡單轉換元件，可將所有字串資料行值轉換為大寫字元。 這個範例並未示範本主題中討論的所有方法與功能。 它示範每個具有同步輸出的自訂轉換元件必須覆寫的重要方法，但是並不包含設計階段驗證的程式碼。  
  
```csharp  
using System;  
using System.Collections;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
using Microsoft.SqlServer.Dts.Runtime.Wrapper;  
  
namespace Uppercase  
{  
  [DtsPipelineComponent(DisplayName = "Uppercase")]  
  public class Uppercase : PipelineComponent  
  {  
    ArrayList m_ColumnIndexList = new ArrayList();  
  
    public override void ProvideComponentProperties()  
    {  
      base.ProvideComponentProperties();  
      ComponentMetaData.InputCollection[0].Name = "Uppercase Input";  
      ComponentMetaData.OutputCollection[0].Name = "Uppercase Output";  
    }  
  
    public override void PreExecute()  
    {  
      IDTSInput100 input = ComponentMetaData.InputCollection[0];  
      IDTSInputColumnCollection100 inputColumns = input.InputColumnCollection;  
  
      foreach (IDTSInputColumn100 column in inputColumns)  
      {  
        if (column.DataType == DataType.DT_STR || column.DataType == DataType.DT_WSTR)  
        {  
          m_ColumnIndexList.Add((int)BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID));  
        }  
      }  
    }  
  
    public override void ProcessInput(int inputID, PipelineBuffer buffer)  
    {  
      while (buffer.NextRow())  
      {  
        foreach (int columnIndex in m_ColumnIndexList)  
        {  
          string str = buffer.GetString(columnIndex);  
          buffer.SetString(columnIndex, str.ToUpper());  
        }  
      }  
    }  
  }  
}  
```  
  
```vb  
Imports System   
Imports System.Collections   
Imports Microsoft.SqlServer.Dts.Pipeline   
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper   
Imports Microsoft.SqlServer.Dts.Runtime.Wrapper   
Namespace Uppercase   
  
 <DtsPipelineComponent(DisplayName="Uppercase")> _   
 Public Class Uppercase   
 Inherits PipelineComponent   
   Private m_ColumnIndexList As ArrayList = New ArrayList   
  
   Public  Overrides Sub ProvideComponentProperties()   
     MyBase.ProvideComponentProperties   
     ComponentMetaData.InputCollection(0).Name = "Uppercase Input"   
     ComponentMetaData.OutputCollection(0).Name = "Uppercase Output"   
   End Sub   
  
   Public  Overrides Sub PreExecute()   
     Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
     Dim inputColumns As IDTSInputColumnCollection100 = input.InputColumnCollection   
     For Each column As IDTSInputColumn100 In inputColumns   
       If column.DataType = DataType.DT_STR OrElse column.DataType = DataType.DT_WSTR Then   
         m_ColumnIndexList.Add(CType(BufferManager.FindColumnByLineageID(input.Buffer, column.LineageID), Integer))   
       End If   
     Next   
   End Sub   
  
   Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
     While buffer.NextRow   
       For Each columnIndex As Integer In m_ColumnIndexList   
         Dim str As String = buffer.GetString(columnIndex)   
         buffer.SetString(columnIndex, str.ToUpper)   
       Next   
     End While   
   End Sub   
 End Class   
End Namespace  
```  
  
## <a name="see-also"></a>另請參閱  
 [開發具有非同步輸出的自訂轉換元件](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)   
 [了解同步和非同步轉換](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [使用指令碼元件建立同步轉換](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)  
  
  
