---
title: 處理 ADO 事件 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1738c7432dce6538fe15c4b23f15f5ab7fe6f219
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606502"
---
# <a name="handling-ado-events"></a>處理 ADO 事件
ADO 事件模型支援發出特定同步和非同步 ADO operations*事件*，或在作業啟動之前或之後完成的通知。 事件是實際的事件處理常式，您在您的應用程式中定義的呼叫。  
  
 如果您在作業啟動之前發生的事件群組，提供處理常式函式或程序，您可以檢查或修改已傳遞給作業的參數。 因為它擁有尚未執行，您可以取消作業，或讓其完成。  
  
 在作業完成之後，就會發生的事件就顯得特別重要，如果您以非同步方式使用 ADO 的。 例如，應用程式啟動的非同步[Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)作業會在執行完整事件作業結束時收到通知。  
  
 使用 ADO 事件模型將一些額外負荷新增至您的應用程式，但提供比其他方法的非同步作業，例如監視處理更多的彈性[狀態](../../../ado/reference/ado-api/state-property-ado.md)迴圈與物件的屬性。  
  
> [!NOTE]
>  若要處理事件，ADO 需要有訊息幫浦，或使用單一執行緒 apartment (STA) 模型中。 ADO 事件會在內部處理建立隱藏的視窗。 ADO 事件要引發時，將訊息張貼到這個視窗。 這為了確保事件會傳送至呼叫的執行緒**IConnectionPoint::Advise**連接點上。 此架構時應接收通知的執行緒不會不提取視窗訊息，可能會造成問題。 潛在的問題包括 ADO 事件無法傳遞至執行緒和通用的視窗廣播逾時和可能減緩整個系統，因為隱藏的 windows 不會處理訊息。 STA 執行緒通常會有訊息幫浦，因此這個問題不會不顯現在 STA 執行緒上執行。 MTA 執行緒，不過，通常沒有訊息幫浦因此問題會通常顯現 MTA 執行緒上。  
  
 此章節包含下列主題。  
  
-   [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [事件的類型](../../../ado/guide/data/types-of-events.md)  
  
-   [事件參數](../../../ado/guide/data/event-parameters.md)  
  
-   [事件處理常式如何協同運作](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO 事件具現化 (依語言)](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件的類型](../../../ado/guide/data/types-of-events.md)
