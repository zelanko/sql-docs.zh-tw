---
title: "升級資料流程元件的版本 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- PerformUpgrade method
- custom data flow components [Integration Services], upgrading version
- data flow components [Integration Services], upgrading version
- upgrading data flow components [Integration Services]
ms.assetid: c2a298c6-01b3-4ad1-884d-6108165eb56e
caps.latest.revision: 25
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 65e38600b0974d75f5509a4231f6ebb0a15ba19a
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="upgrading-the-version-of-a-data-flow-component"></a>升級資料流程元件的版本
  使用舊版元件建立的封裝，可能包含不再有效的中繼資料，例如在新版元件中使用方式已有所修改的自訂屬性。 您可以覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法，以更新之前儲存在舊封裝的中繼資料，從而反映元件的目前屬性。  
  
> [!NOTE]  
>  當您為新版本的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 重新編譯自訂元件時，如果未變更元件的屬性，就不必變更 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.CurrentVersion%2A> 屬性的值。  
  
## <a name="example"></a>範例  
 下列範例包含 2.0 版的虛構資料流程元件之程式碼。 新版本號碼是定義在 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.CurrentVersion%2A> 的 <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> 屬性中。 該元件具有一個屬性，它定義如何處理超過臨界值的數值。 在 1.0 版的虛構元件中，這個屬性名為 `RaiseErrorOnInvalidValue` 並接受 True 或 False 的布林值。 在 2.0 版的虛構元件中，該屬性重新命名為 `InvalidValueHandling` 並接受自訂列舉的四個可能值之一。  
  
 下列範例中覆寫的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A> 方法會執行下列動作：  
  
-   取得元件的目前版本。  
  
-   取得舊的自訂屬性值。  
  
-   移除自訂屬性集合中的舊屬性。  
  
-   若有可能的話，根據舊屬性值設定新自訂屬性值。  
  
-   將版本中繼資料設定成元件的目前版本。  
  
> [!NOTE]  
>  資料流程引擎會傳遞到自己的版本號碼<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PerformUpgrade%2A>方法中的*pipelineVersion*參數。 此參數在 1.0 版的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 中沒有用處，但是在後續版本中可能會變成有用。  
  
 範例程式碼只會使用兩個列舉值，以直接對應至自訂屬性之前的布林值。 使用者可以透過元件的自訂使用者介面、在 [進階編輯器] 中或是以程式設計方式，選取其他可用的列舉值。 在 [進階編輯器] 中顯示自訂屬性的列舉值的資訊，請參閱中的 < 建立自訂屬性"[資料流程元件的設計階段方法](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)。  
  
```vb  
Imports Microsoft.SqlServer.Dts.Pipeline  
Imports Microsoft.SqlServer.Dts.Pipeline.Wrapper  
  
<DtsPipelineComponent(ComponentType:=ComponentType.Transform, CurrentVersion:=2)> _  
Public Class PerformUpgrade  
  Inherits PipelineComponent  
  
  ' Define the set of possible values for the new custom property.  
  Private Enum InvalidValueHandling  
    Ignore  
    FireInformation  
    FireWarning  
    FireError  
  End Enum  
  
  Public Overloads Overrides Sub PerformUpgrade(ByVal pipelineVersion As Integer)  
  
    ' Obtain the current component version from the attribute.  
    Dim componentAttribute As DtsPipelineComponentAttribute = _  
      CType(Attribute.GetCustomAttribute(Me.GetType, _  
      GetType(DtsPipelineComponentAttribute), False), _  
      DtsPipelineComponentAttribute)  
    Dim currentVersion As Integer = componentAttribute.CurrentVersion  
  
    ' If the component version saved in the package is less than  
    '  the current version, Version 2, perform the upgrade.  
    If ComponentMetaData.Version < currentVersion Then  
  
      ' Get the current value of the old custom property, RaiseErrorOnInvalidValue,   
      ' and then remove the property from the custom property collection.  
      Dim oldValue As Boolean = False  
      Try  
        Dim oldProperty As IDTSCustomProperty100 = _  
          ComponentMetaData.CustomPropertyCollection("RaiseErrorOnInvalidValue")  
        oldValue = CType(oldProperty.Value, Boolean)  
        ComponentMetaData.CustomPropertyCollection.RemoveObjectByIndex("RaiseErrorOnInvalidValue")  
      Catch ex As Exception  
        ' If the old custom property is not available, ignore the error.  
      End Try  
  
      ' Set the value of the new custom property, InvalidValueHandling,  
      '  by using the appropriate enumeration value.  
      Dim newProperty As IDTSCustomProperty100 = _  
        ComponentMetaData.CustomPropertyCollection("InvalidValueHandling")  
      If oldValue = True Then  
        newProperty.Value = InvalidValueHandling.FireError  
      Else  
        newProperty.Value = InvalidValueHandling.Ignore  
      End If  
  
    End If  
  
    ' Update the saved component version metadata to the current version.  
    ComponentMetaData.Version = currentVersion  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Pipeline;  
using Microsoft.SqlServer.Dts.Pipeline.Wrapper;  
  
[DtsPipelineComponent(ComponentType = ComponentType.Transform, CurrentVersion = 2)]  
public class PerformUpgradeCS :  
  PipelineComponent  
  
  // Define the set of possible values for the new custom property.  
{  
  private enum InvalidValueHandling  
  {  
    Ignore,  
    FireInformation,  
    FireWarning,  
    FireError  
  };  
  
  public override void PerformUpgrade(int pipelineVersion)  
  {  
  
    // Obtain the current component version from the attribute.  
    DtsPipelineComponentAttribute componentAttribute =   
      (DtsPipelineComponentAttribute)Attribute.GetCustomAttribute(this.GetType(), typeof(DtsPipelineComponentAttribute), false);  
    int currentVersion = componentAttribute.CurrentVersion;  
  
    // If the component version saved in the package is less than  
    //  the current version, Version 2, perform the upgrade.  
    if (ComponentMetaData.Version < currentVersion)  
  
    // Get the current value of the old custom property, RaiseErrorOnInvalidValue,   
    // and then remove the property from the custom property collection.  
    {  
      bool oldValue = false;  
      try  
      {  
        IDTSCustomProperty100 oldProperty =   
          ComponentMetaData.CustomPropertyCollection["RaiseErrorOnInvalidValue"];  
        oldValue = (bool)oldProperty.Value;  
        ComponentMetaData.CustomPropertyCollection.RemoveObjectByIndex("RaiseErrorOnInvalidValue");  
      }  
      catch (Exception ex)  
      {  
        // If the old custom property is not available, ignore the error.  
      }  
  
      // Set the value of the new custom property, InvalidValueHandling,  
      //  by using the appropriate enumeration value.  
      IDTSCustomProperty100 newProperty =   
         ComponentMetaData.CustomPropertyCollection["InvalidValueHandling"];  
      if (oldValue == true)  
      {  
        newProperty.Value = InvalidValueHandling.FireError;  
      }  
      else  
      {  
        newProperty.Value = InvalidValueHandling.Ignore;  
      }  
  
    }  
  
    // Update the saved component version metadata to the current version.  
    ComponentMetaData.Version = currentVersion;  
  
  }  
  
}  
```

