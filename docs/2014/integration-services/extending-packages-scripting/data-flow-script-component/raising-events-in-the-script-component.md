---
title: 在指令碼元件中引發事件 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], raising events
ms.assetid: bb389073-e1d0-4794-8d29-c8b293b6a5e3
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2c0ff0ee604c2b7317aa27d7d4d1412cd9ecab47
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/02/2018
ms.locfileid: "37241018"
---
# <a name="raising-events-in-the-script-component"></a>在指令碼元件中引發事件
  事件會提供向包含封裝報告錯誤、警告和其他資訊 (例如工作進度或狀態) 的方法。 封裝提供管理事件通知的事件處理常式。 指令碼元件可以呼叫 `ScriptMain` 類別的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 屬性上之方法以引發事件。 如需 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 套件如何處理事件的詳細資訊，請參閱 [Integration Services &#40;SSIS&#41; 事件處理常式](../../integration-services-ssis-event-handlers.md)。  
  
 事件可以記錄到封裝中啟用的任何記錄提供者。 記錄提供者會在資料存放區中儲存事件的相關資訊。 指令碼元件也可以使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法將資訊記錄到記錄提供者，而不會引發事件。 如需有關如何使用 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> 方法的詳細資訊，請參閱下一節。  
  
 為了引發事件，指令碼工作會呼叫 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> 屬性公開的 <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A> 介面之下列其中一個方法：  
  
|事件|描述|  
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
  
![Integration Services 圖示 （小）](../../media/dts-16.gif "Integration Services 圖示 （小）")**保持最多包含 Integration Services 的日期** <br /> 若要取得 Microsoft 的最新下載、文件、範例和影片以及社群中的精選解決方案，請瀏覽 MSDN 上的 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 頁面：<br /><br /> [瀏覽 MSDN 上的 Integration Services 頁面](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 若要得到這些更新的自動通知，請訂閱該頁面上所提供的 RSS 摘要。  
  
## <a name="see-also"></a>另請參閱  
 [Integration Services &#40;SSIS&#41; 事件處理常式](../../integration-services-ssis-event-handlers.md)   
 [將事件處理常式新增至套件](../../add-an-event-handler-to-a-package.md)  
  
  
