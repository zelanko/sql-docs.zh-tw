---
title: "在指令碼元件中引發事件 |Microsoft 文件"
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
helpviewer_keywords:
- Script component [Integration Services], raising events
ms.assetid: bb389073-e1d0-4794-8d29-c8b293b6a5e3
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 505855e82b683fc15ca00073f58e1f9cb348f830
ms.contentlocale: zh-tw
ms.lasthandoff: 08/03/2017

---
# <a name="raising-events-in-the-script-component"></a>在指令碼元件中引發事件
  事件會提供向包含封裝報告錯誤、警告和其他資訊 (例如工作進度或狀態) 的方法。 封裝提供管理事件通知的事件處理常式。 指令碼元件可以引發事件上呼叫方法<xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>屬性**ScriptMain**類別。 如需有關如何[!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]封裝處理事件，請參閱[Integration Services &#40;SSIS &#41;事件處理常式](../../../integration-services/integration-services-ssis-event-handlers.md)。  
  
 事件可以記錄到封裝中啟用的任何記錄提供者。 記錄提供者會在資料存放區中儲存事件的相關資訊。 指令碼元件也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法將資訊記錄到記錄提供者，而不會引發事件。 如需有關如何使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法的詳細資訊，請參閱下一節。  
  
 為了引發事件，指令碼工作會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性公開的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 介面之下列其中一個方法：  
  
|事件|Description|  
|-----------|-----------------|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>|引發封裝中使用者定義的自訂事件。|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A>|通知封裝有關錯誤狀況。|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A>|提供資訊給使用者。|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireProgress%2A>|通知封裝有關元件的進度。|  
|<xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A>|通知封裝元件是在需要使用者通知的狀態，但不是錯誤狀況。|  
  
 以下是引發 Error 事件的簡單範例：  
  
 `Dim myMetadata as IDTSComponentMetaData100`  
  
 `myMetaData = Me.ComponentMetaData`  
  
 `myMetaData.FireError(...)`  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS &#41;事件處理常式](../../../integration-services/integration-services-ssis-event-handlers.md)   
 [將事件處理常式加入封裝](http://msdn.microsoft.com/library/5e56885d-8658-480a-bed9-3f2f8003fd78)  
  
  

