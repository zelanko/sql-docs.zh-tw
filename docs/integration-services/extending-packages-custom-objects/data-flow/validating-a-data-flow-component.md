---
title: 驗證資料流程元件 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ReinitializeMetaData method
- Validate method
- component validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- data flow components [Integration Services], validating
- validation [Integration Services]
ms.assetid: 1a7d5925-b387-4e31-af7f-c7f3c5151040
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03c0d26ae97be2ca22b341c40b01cf0e5c558399
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65724636"
---
# <a name="validating-a-data-flow-component"></a>驗證資料流程元件

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  提供 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法，可以避免執行設定不正確的元件。 使用這個方法可確認元件具有預期的輸入和輸出物件數、此元件的自訂屬性具有可接受的值，以及指定了任何需要的連接。 使用這個方法也可確認輸入和輸出集合內的資料行具有正確的資料類型，以及每一個資料行的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSUsageType> 都針對此元件適當地設定。 基底類別實作會協助驗證程序，其方式是檢查此元件的輸入資料行集合，並確保此集合中的每一個資料行都會參考上游元件之 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputCollection100> 中的資料行。  
  
## <a name="validate-method"></a>Validate 方法  
 在 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師中編輯元件時，便會重複呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 方法。 您可以透過 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> 列舉傳回值及藉由公佈警告和錯誤，提供意見給此元件的設計人員和使用者。 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus> 列舉包含可指示失敗的各個階段的三個值，以及第四個值 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISVALID>，該值會指出此元件是否已正確設定並準備好要執行。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> 值指出 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 中有錯誤存在，而且此元件可修復錯誤。 如果元件遇到了可以修復的中繼資料錯誤，它不應該修正 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 方法中的錯誤，而且驗證期間不應該修改 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>。 而是 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 方法應該只能傳回 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA>，而且此元件應該在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法的呼叫中修復此錯誤，如同本章節稍後所述。  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISBROKEN> 值指出，此元件的錯誤可以在設計師中編輯此元件來加以修正。 此錯誤通常是因為自訂屬性或是未指定或設定錯誤的必要連接所造成。  
  
 最後的錯誤值是 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_ISCORRUPT>，該值指出此元件發現的錯誤只有在直接修改了 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 屬性時才應該發生 (不論是編輯封裝 XML 或使用物件模型)。 例如，當元件只加入了單一輸入，但是驗證作業發現 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 中有一個以上的輸入存在時，就會發生這種錯誤。 若要修復產生這個傳回值的錯誤，只能重設此元件或是使用 [進階編輯器]  對話方塊中的 [重設]  按鈕。  
  
 除了傳回錯誤值以外，元件還會藉由公佈驗證期間的警告或錯誤來提供意見。 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireWarning%2A> 和 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents.FireError%2A> 方法會提供這項機制。 當呼叫這些方法時，這些事件會在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 的 [錯誤清單]  視窗內公佈。 然後元件開發人員可以提供有關所發生之錯誤的直接意見給使用者，並在適當的情況下提供修正錯誤的方式。  
  
 下列程式碼範例會示範已覆寫的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 實作。  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    bool pbCancel = false;  
  
    // Validate that there is one input.  
    if (ComponentMetaData.InputCollection.Count != 1)  
    {  
    ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, out pbCancel);  
    return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Validate that the UserName custom property is set.  
    if (ComponentMetaData.CustomPropertyCollection["UserName"].Value == null || ((string)ComponentMetaData.CustomPropertyCollection["UserName"].Value).Length == 0)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISBROKEN;  
    }  
  
    // Validate that there is one output.  
    if (ComponentMetaData.OutputCollection.Count != 1)  
    {  
        ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, out pbCancel);  
        return DTSValidationStatus.VS_ISCORRUPT;  
    }  
  
    // Let the base class verify that the input column reflects the output   
    // of the upstream component.  
    return base.Validate();  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
  
 Dim pbCancel As Boolean = False  
  
 ' Validate that there is one input.  
 If Not (ComponentMetaData.InputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of inputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Validate that the UserName custom property is set.  
 If ComponentMetaData.CustomPropertyCollection("UserName").Value Is Nothing OrElse CType(ComponentMetaData.CustomPropertyCollection("UserName").Value, String).Length = 0 Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "The UserName property must be set.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISBROKEN   
 End If   
  
 ' Validate that there is one output.  
 If Not (ComponentMetaData.OutputCollection.Count = 1) Then   
   ComponentMetaData.FireError(0, ComponentMetaData.Name, "Incorrect number of outputs.", "", 0, pbCancel)   
   Return DTSValidationStatus.VS_ISCORRUPT   
 End If   
  
 ' Let the base class verify that the input column reflects the output   
 ' of the upstream component.  
  
 Return MyBase.Validate   
  
End Function  
```  
  
## <a name="reinitializemetadata-method"></a>ReinitializeMetaData 方法  
 當您編輯的元件從其 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法傳回 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSValidationStatus.VS_NEEDSNEWMETADATA> 時，[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計工具便會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 方法。 元件包含的程式碼，應能偵測及修正此元件在驗證期間所指出的各項問題。  
  
 下列範例所示的元件，會在驗證期間偵測問題，並使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法修正這些錯誤。  
  
```csharp  
private bool areInputColumnsValid = true;  
public override DTSValidationStatus Validate()  
{  
    IDTSInput100 input = ComponentMetaData.InputCollection[0];  
    IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
    bool Cancel = false;  
    foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
    {  
        try  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
        }  
        catch  
        {  
            ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, out Cancel);  
            areInputColumnsValid = false;  
            return DTSValidationStatus.VS_NEEDSNEWMETADATA;  
        }  
    }  
  
    return DTSValidationStatus.VS_ISVALID;  
}  
public override void ReinitializeMetaData()  
{  
    if (!areInputColumnsValid)  
    {  
        IDTSInput100 input = ComponentMetaData.InputCollection[0];  
        IDTSVirtualInput100 vInput = input.GetVirtualInput();  
  
        foreach (IDTSInputColumn100 column in input.InputColumnCollection)  
        {  
            IDTSVirtualInputColumn100 vColumn = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID);  
  
            if (vColumn == null)  
                input.InputColumnCollection.RemoveObjectByID(column.ID);  
        }  
        areInputColumnsValid = true;  
    }  
}  
```  
  
```vb  
Private areInputColumnsValid As Boolean = True   
  
Public  Overrides Function Validate() As DTSValidationStatus   
 Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
 Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
 Dim Cancel As Boolean = False   
 For Each column As IDTSInputColumn100 In input.InputColumnCollection   
   Try   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
   Catch   
     ComponentMetaData.FireError(0, ComponentMetaData.Name, "The input column " + column.IdentificationString + " does not match a column in the upstream component.", "", 0, Cancel)   
     areInputColumnsValid = False   
     Return DTSValidationStatus.VS_NEEDSNEWMETADATA   
   End Try   
 Next   
 Return DTSValidationStatus.VS_ISVALID   
End Function   
  
Public  Overrides Sub ReinitializeMetaData()   
 If Not areInputColumnsValid Then   
   Dim input As IDTSInput100 = ComponentMetaData.InputCollection(0)   
   Dim vInput As IDTSVirtualInput100 = input.GetVirtualInput   
   For Each column As IDTSInputColumn100 In input.InputColumnCollection   
     Dim vColumn As IDTSVirtualInputColumn100 = vInput.VirtualInputColumnCollection.GetVirtualInputColumnByLineageID(column.LineageID)   
     If vColumn Is Nothing Then   
       input.InputColumnCollection.RemoveObjectByID(column.ID)   
     End If   
   Next   
   areInputColumnsValid = True   
 End If   
End Sub  
```  
  
