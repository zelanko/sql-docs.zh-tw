---
title: 資料流程元件的設計階段方法 | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom data flow components [Integration Services], method execution sequence
- ProcessInput method
- method execution sequence [Integration Services]
- PrimeOutput method
- data flow components [Integration Services], method execution sequence
ms.assetid: b5a121a1-b87c-441b-a42c-2cec628dc81c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 24debd25c95242ae78142e1de597b2b5b632c197
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354774"
---
# <a name="design-time-methods-of-a-data-flow-component"></a>資料流程元件的設計階段方法
  據說在執行之前，資料流程工作會設計狀態階段進行累加變更。 變更可包括元件的加入或移除、連接元件的路徑物件之加入或移除，以及對於元件中繼資料的變更。 當中繼資料變更發生時，元件可以監視變更並對其做出反應。 例如，元件可以不允許某些變更，或是做其他變更以回應變更。 在設計階段，設計工具會透過設計階段 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 介面與元件互動。  
  
## <a name="design-time-implementation"></a>設計階段實作  
 元件的設計階段介面是由 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 介面所描述。 雖然您未明確地實作這個介面，不過熟悉定義在這個介面中的方法，將可協助您了解 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基底類別的哪些方法與元件的設計階段執行個體對應。  
  
 在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 中載入元件時，會具現化元件的設計階段執行個體，並在編輯元件時，呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSDesigntimeComponent100> 介面的方法。 基底類別的實作可讓您只覆寫元件所需的方法。 在許多情況下，您可以覆寫這些方法以防止對元件的不當編輯。 例如，若要防止使用者將輸出加入元件，請覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.InsertOutput%2A> 方法。 否則，呼叫由基底類別實作的此方法時，它會將輸出加入元件。  
  
 不論元件的目的或功能為何，您都應該覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A>、<xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 與 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 方法。 如需 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.Validate%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> 的詳細資訊，請參閱[驗證資料流程元件](validating-a-data-flow-component.md)。  
  
## <a name="providecomponentproperties-method"></a>提供 ComponentProperties 方法  
 元件的初始化會發生在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法中。 當元件加入資料流程工作時，[!INCLUDE[ssIS](../../../includes/ssis-md.md)] 設計師會呼叫這個方法，此方法類似類別建構函式。 元件開發人員應該在此方法呼叫期間，建立並初始化輸入、輸出和自訂屬性。 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法與建構函式不同，因為它並不會在每次具現化元件的設計階段執行個體或是執行階段執行個體時呼叫。  
  
 該方法的基底類別實作會將輸入和輸出加入元件，並將輸入的識別碼指派到 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutput100.SynchronousInputID%2A> 屬性。 不過，在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，並未命名基底類別加入的輸入和輸出物件。 如果封裝包含的元件所帶有的輸入或輸出物件未設定 Name 屬性，封裝將無法成功載入。 因此，當您使用基底實作時，必須將值明確地指派到預設輸入與輸出的 Name 屬性。  
  
```csharp  
public override void ProvideComponentProperties()  
{  
    /// TODO: Reset the component.  
    /// TODO: Add custom properties.  
    /// TODO: Add input objects.  
    /// TODO: Add output objects.  
}  
```  
  
```vb  
Public Overrides Sub ProvideComponentProperties()  
    ' TODO: Reset the component.  
    ' TODO: Add custom properties.  
    ' TODO: Add input objects.  
    ' TODO: Add output objects.  
End Sub  
```  
  
### <a name="creating-custom-properties"></a>建立自訂屬性  
 在呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProvideComponentProperties%2A> 方法時，元件開發人員應該將自訂屬性 (<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100>) 加入元件。 自訂屬性沒有資料類型屬性。 自訂屬性的資料類型是由您指派至其 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.Value%2A> 屬性的值資料類型所設定。 不過，在您將初始值指派到自訂屬性之後，您無法以不同的資料類型指派值。  
  
> [!NOTE]  
>  <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100> 介面對於 `Object` 類型的屬性值之支援有限。 您可以儲存為自訂屬性值的唯一物件是簡單類型的陣列，例如字串或是整數。  
  
 您可以將自訂屬性的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.ExpressionType%2A> 屬性值設定成 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.DTSCustomPropertyExpressionType> 列舉的 `CPET_NOTIFY`，藉此指出自訂屬性支援屬性運算式，如下列範例所示。 您不必加入任何程式碼以處理或是驗證使用者所輸入的屬性運算式。 您可以為屬性設定預設值、驗證其值，以及正常地讀取和使用其值。  
  
```csharp  
IDTSCustomProperty100 myCustomProperty;  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY;  
```  
  
```vb  
Dim myCustomProperty As IDTSCustomProperty100  
...  
myCustomProperty.ExpressionType = DTSCustomPropertyExpressionType.CPET_NOTIFY  
```  
  
 您可以使用從列舉選取自訂屬性值來限制使用者<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.TypeConverter%2A>屬性，如下列的範例中，假設您已定義名為的公用列舉中所示`MyValidValues`。  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the type with the custom property.  
customProperty.TypeConverter = typeof(MyValidValues).AssemblyQualifiedName;  
// Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne;    
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the type with the custom property.  
customProperty.TypeConverter = GetType(MyValidValues).AssemblyQualifiedName   
' Now you can use the enumeration values directly.  
customProperty.Value = MyValidValues.ValueOne  
```  
  
 如需詳細資訊，請參閱 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022) 中的＜通用類型轉換＞與＜實作類型轉換子＞。  
  
 您可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 屬性，為自訂屬性值指定自訂編輯器對話方塊，如下列範例所示。 首先，如果您無法找到符合需求的現有 UI 類型編輯器，必須建立一個繼承自 `System.Drawing.Design.UITypeEditor`的自訂類型編輯器。  
  
```csharp  
public class MyCustomTypeEditor : UITypeEditor  
{  
...  
}  
```  
  
```vb  
Public Class MyCustomTypeEditor  
  Inherits UITypeEditor   
  ...  
End Class  
```  
  
 接著將此類別指定為自訂屬性的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSCustomProperty100.UITypeEditor%2A> 屬性值。  
  
```csharp  
IDTSCustomProperty100 customProperty = outputColumn.CustomPropertyCollection.New();  
customProperty.Name = "My Custom Property";  
// This line associates the editor with the custom property.  
customProperty.UITypeEditor = typeof(MyCustomTypeEditor).AssemblyQualifiedName;  
```  
  
```vb  
Dim customProperty As IDTSCustomProperty100 = outputColumn.CustomPropertyCollection.New   
customProperty.Name = "My Custom Property"   
' This line associates the editor with the custom property.  
customProperty.UITypeEditor = GetType(MyCustomTypeEditor).AssemblyQualifiedName  
```  
  
 如需詳細資訊，請參閱 [MSDN Library](https://go.microsoft.com/fwlink/?LinkId=7022) 中的＜實作 UI 類型編輯器＞。  
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期**<br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [資料流程元件的執行階段方法](run-time-methods-of-a-data-flow-component.md)  
  
  
