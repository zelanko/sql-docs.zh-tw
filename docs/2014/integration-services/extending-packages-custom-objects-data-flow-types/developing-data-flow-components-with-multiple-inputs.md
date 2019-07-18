---
title: 開發具有多個輸入的資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 74bcf1549cdd97752c805f1c6a9cc774ef1a9e52
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62896028"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>開發具有多個輸入的資料流程元件
  如果具有多個輸入的資料流程元件其多個輸入會以不平均的速率產生資料，可能會耗用過多的記憶體。 當您開發支援兩個或多個輸入的自訂資料流程元件時，可以使用 Microsoft.SqlServer.Dts.Pipeline 命名空間中的下列成員來管理記憶體壓力：  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性。 如果您想要實作為了讓自訂資料流程元件管理速率不平均之資料所需的程式碼，請將這個屬性的值設定為 `true`。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 如果您將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 屬性設定為 `true`，就必須提供這個方法的實作。 如果您沒有提供實作，資料流程引擎會在執行階段引發例外狀況。  
  
-   <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 如果您將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 屬性設定為 `true`，而且自訂元件支援超過兩個的輸入，您也必須提供這個方法的實作。 如果您沒有提供實作，而且使用者附加超過兩個輸入，資料流程引擎會在執行階段引發例外狀況。  
  
 結合這些成員，即可讓您開發與 Microsoft 所開發之「合併」和「合併聯結」轉換方案類似的記憶體壓力方案。  
  
## <a name="setting-the-supportsbackpressure-property"></a>設定 SupportsBackPressure 屬性  
 針對自訂支援多個輸入之資料流程元件實作更好的記憶體管理中的第一個步驟，就是在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 中將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性的值設定為 `true`。 當 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 的值為 `true` 時，資料流程引擎會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法，具有超過兩個輸入時，也會在執行階段呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。  
  
### <a name="example"></a>範例  
 在下列範例中，<xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 的實作會將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 的值設定為 `true`。  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>實作 IsInputReady 方法  
 當您在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> 物件中將 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性的值設定為 `true` 時，就必須提供 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 類別之 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法的實作。  
  
> [!NOTE]  
>  您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法實作不應該呼叫基底類別中實作。 在基底類別中，這個方法的預設實作只會引發 `NotImplementedException`。  
  
 實作這個方法時，您會針對每個元件的輸入設定布林值 *canProcess* 陣列中的元素狀態 (輸入是由它們在 *inputIDs* 陣列中的識別碼值所識別)。當您設定的值中的項目*canProcess*陣列`true`針對某個輸入，資料流程引擎會呼叫元件的<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A>方法，並為指定的輸入提供更多資料。  
  
 更多的上游資料可供使用，而值*canProcess*都必須至少一個輸入的陣列元素`true`，或處理就會停止。  
  
 資料流程引擎會在傳送資料的每個緩衝區之前，呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法，以判斷哪一個輸入正在等候接收更多資料。 當傳回值表示輸入遭到封鎖時，資料流程引擎就會為該輸入暫時快取資料的其他緩衝區，而不會將它們傳送到元件。  
  
> [!NOTE]  
>  您不用在自己的程式碼中呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 資料流程引擎執行您的元件時，資料流程引擎會呼叫這些方法以及您所覆寫之 `PipelineComponent` 類別的其他方法。  
  
### <a name="example"></a>範例  
 在下列的範例中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法的實作指出當下列條件成立時，輸入會等候接收更多資料：  
  
-   有更多的上游資料可供輸入使用 (`!inputEOR`)。  
  
-   元件目前沒有可用來處理元件已接收之緩衝區中的資料 (`inputBuffers[inputIndex].CurrentRow() == null`)。  
  
 如果輸入正在等候接收更多資料，資料流程元件就會將這表示設定為`true`的值中的項目*canProcess*與該輸入對應的陣列。  
  
 相反地，當元件仍有可用於處理輸入的資料時，這個範例會暫停處理輸入。 這個範例會設定為`false`的值中的項目*canProcess*與該輸入對應的陣列。  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 前面的範例會使用布林 (Boolean) `inputEOR` 陣列來指出是否有更多的上游資料可供每個輸入使用。 陣列名稱中的 `EOR` 代表「資料列集結束」，也會參考資料流程緩衝區的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性。 在這裡未包含的範例部分中，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> 方法會檢查它所接收資料的每個緩衝區之 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> 屬性值。 當 `true` 的值表示沒有其他上游資料可供輸入使用時，範例會將該輸入的 `inputEOR` 陣列元素設定為 `true`。 此範例中的<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>方法會設定對應的項目中的值*canProcess*陣列`false`針對某個輸入時的值`inputEOR`陣列項目指出已沒有其他上游可用的輸入資料。  
  
## <a name="implementing-the-getdependentinputs-method"></a>實作 GetDependentInputs 方法  
 當您的自訂資料元件支援超過兩個輸入時，您也必須針對 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法提供實作。  
  
> [!NOTE]  
>  您的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法實作不應該呼叫基底類別中實作。 在基底類別中，這個方法的預設實作只會引發 `NotImplementedException`。  
  
 資料流程引擎只會在使用者將超過兩個輸入附加至元件時呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 當元件只有兩個輸入時，而<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A>方法指出其中一個輸入遭到封鎖 (*canProcess* = `false`)，資料流程引擎知道其他輸入正在等候接收更多資料。 但是，具有超過兩個輸入，而且 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 方法指出其中一個輸入遭到封鎖時，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 中額外的程式碼就會識別哪一個輸入正在等候接收更多資料。  
  
> [!NOTE]  
>  您不用在自己的程式碼中呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> 或 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法。 資料流程引擎執行您的元件時，資料流程引擎會呼叫這些方法以及您所覆寫之 `PipelineComponent` 類別的其他方法。  
  
### <a name="example"></a>範例  
 針對遭到封鎖的特定輸入，下列 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法的實作會傳回正在等候接收更多資料之輸入的集合，進而封鎖指定的輸入。 元件會檢查除了已封鎖輸入之外，目前在元件已接收緩衝區中，哪些輸入沒有可供處理的資料，以識別正在封鎖的輸入 (`inputBuffers[i].CurrentRow() == null`)。 然後，<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> 方法會以輸入識別碼集合的方式傳回正在封鎖的輸入集合。  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
