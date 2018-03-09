---
title: "在資料流程元件中引發和定義事件 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 29e81f38876b25e3a789ef1eebdbdf9d1abebe1a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>在資料流程元件中引發和定義事件
  元件開發人員可以引發 <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> 介面中定義的事件子集，其方式是呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A> 屬性上所公開的方法。 您也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> 集合來定義自訂事件，然後在執行期間使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 方法來引發這些事件。 本章節描述如何建立及引發事件，並提供有關您在設計階段的何時應該引發事件的指引。  
  
## <a name="raising-events"></a>引發事件  
 元件會使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 介面的 **Fire\<X>** 方法來引發事件。 您可以在元件的設計和執行期間引發事件。 一般在元件設計期間，<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> 和 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A> 方法會在驗證期間呼叫。 這些事件會在 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] 的 [錯誤清單] 窗格內顯示訊息，並在元件設定不正確時提供意見給元件的使用者。  
  
 元件也可以在執行期間的任何時間點引發事件。 事件可讓元件開發人員在執行元件時，提供意見給此元件的使用者。 在執行期間呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> 方法很可能會讓封裝失敗。  
  
## <a name="defining-and-raising-custom-events"></a>定義及引發自訂事件  
  
### <a name="defining-a-custom-event"></a>定義自訂事件  
 自訂事件的建立是藉由呼叫 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> 集合的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> 方法。 這個集合是由資料流程工作所設定，並透過 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 基底類別當做屬性提供給元件開發人員。 這個類別包含資料流程工作所定義的自訂事件，以及此元件在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 方法期間所定義的自訂事件。  
  
 元件的自訂事件不會保存在封裝 XML 中。 因此，設計和執行期間會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 方法，好讓此元件定義它所引發的事件。  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> 方法的 *allowEventHandlers* 參數會指定此元件是否允許針對此事件建立 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 物件。 請注意，<xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> 是同步的。 因此，要等到附加至自訂事件的 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 已經完成執行以後，此元件才會繼續執行。 如果 *allowEventHandlers* 參數為 **true**，此事件的每一個參數都會自動提供給任何 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> 物件使用，這是透過 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 執行階段所自動建立及擴展的變數。  
  
### <a name="raising-a-custom-event"></a>引發自訂事件  
 元件引發自訂事件的方式，是藉由呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 方法及提供此事件的名稱、文字和參數。 如果 *allowEventHandlers* 參數為 **true**，針對自訂事件所建立的任何 <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> 都會由 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 執行階段引擎所執行。  
  
### <a name="custom-event-sample"></a>自訂事件範例  
 下列程式碼範例示範一個元件，此元件會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> 方法期間定義自訂事件，然後在執行階段藉由呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> 方法來引發此事件。  
  
```csharp  
public override void RegisterEvents()  
{  
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};  
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};  
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};  
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref paramterTypes, ref parameterDescriptions);  
}  
public override void ProcessInput(int inputID, PipelineBuffer buffer)  
{  
    while (buffer.NextRow())  
    {  
       // Process buffer rows.  
    }  
  
    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];  
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };  
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);  
}  
```  
  
```vb  
Public  Overrides Sub RegisterEvents()   
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"}   
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)}   
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."}   
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, paramterTypes, parameterDescriptions)   
End Sub   
  
Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer)   
  While buffer.NextRow   
  End While   
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort")   
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now}   
  ComponentMetaData.FireCustomEvent("StartingSort", _  
    "Beginning sort operation.", arguments, _  
    ComponentMetaData.Name, FireSortEventAgain)   
End Sub  
```  

## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 事件處理常式](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [將事件處理常式新增至套件](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  
