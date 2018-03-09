---
title: "在資料流程元件中記錄和定義記錄項目 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
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
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7d00316246ed4e12a70cd9f488c578dc29e21fe
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/25/2018
---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>在資料流程元件中記錄和定義記錄項目
  自訂資料流程元件可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法，將訊息公佈到現有的記錄項目中。 它們也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> 介面的 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 方法或是類似方法，將資訊呈現給使用者。 但是，這個方法會產生引發及處理其他事件的額外負擔，並強制使用者詳查詳細的參考用訊息，以找出他們可能感興趣的訊息。 您可以使用自訂記錄項目，如底下所述，將清楚標示的自訂記錄資訊提供給元件的使用者。  
  
## <a name="registering-and-using-a-custom-log-entry"></a>註冊及使用自訂記錄項目  
  
### <a name="registering-a-custom-log-entry"></a>註冊自訂記錄項目  
 若要註冊自訂記錄項目以供元件使用，請覆寫 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> 基底類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent> 方法。 下列範例會註冊自訂記錄項目，並提供名稱和描述。  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> 列舉會將有關此事件將要記錄之頻率的提示提供給執行階段：  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>：有時記錄事件，而不是每次執行時都記錄。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>：每次執行時，事件都會記錄固定次數。  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>：事件記錄的次數與完成的工作量成比例。  
  
 以上範例使用 <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>，因為此元件預期每次執行都會記錄項目一次。  
  
 在註冊自訂記錄項目以及將自訂元件的執行個體新增至資料流程設計工具介面之後，設計工具中的 [記錄] 對話方塊會顯示新的記錄項目，其中 "My Custom Component Log Entry" 名稱會出現在可用的記錄項目清單中。  
  
### <a name="logging-to-a-custom-log-entry"></a>記錄到自訂記錄項目  
 在註冊自訂記錄項目以後，此元件現在可以記錄自訂訊息。 底下範例會在 <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> 方法期間撰寫自訂記錄項目，其中包含此元件所使用之 SQL 陳述式的文字。  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 現在如果使用者在執行套件時，選取了 [記錄] 對話方塊中的 "My Custom Component Log Entry"，此記錄將會包含一個清楚標示為 "User::My Custom Component Log Entry" 的項目。 這個新的記錄項目包含了 SQL 陳述式的文字、時間戳記以及開發人員記錄的任何其他資料。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 記錄](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
