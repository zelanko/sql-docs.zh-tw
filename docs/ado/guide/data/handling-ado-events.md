---
title: "處理 ADO 事件 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- events [ADO]
- ADO, events
- event handlers [ADO]
ms.assetid: e9003457-0762-48b3-942f-0820266b158f
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a451023d3e3501ac60cd2724349337f30c46b689
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="handling-ado-events"></a>處理 ADO 事件
ADO 事件模型支援發出特定同步和非同步 ADO 作業*事件*，或在作業開始之前或之後完成的通知。 事件是實際的事件處理常式常式，在您的應用程式中定義的呼叫。  
  
 如果您在作業開始前發生的事件群組，提供處理函式或程序，您可以檢查或修改已傳遞至作業的參數。 因為它具有尚未執行，您可以取消作業，或讓它完成。  
  
 在作業完成之後發生的事件是以非同步方式使用 ADO 時尤其重要。 例如，應用程式開始執行非同步[Recordset.Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)作業就會在作業結束時執行完整事件通知。  
  
 使用 ADO 事件模型加入您的應用程式的一些額外負荷，但是提供更多的彈性比其他方法處理非同步作業，例如監視的[狀態](../../../ado/reference/ado-api/state-property-ado.md)迴圈與物件的屬性。  
  
> [!NOTE]
>  若要處理事件，ADO 必須有訊息幫浦，或使用單一執行緒 apartment (STA) 模型中。 ADO 事件是在內部處理藉由建立隱藏的視窗。 ADO 會將訊息公佈到這個視窗中，如果事件要引發觸發程序。 這樣做可確保事件會傳送至呼叫的執行緒**Iconnectionpoint**連接點上。 此架構時應接收通知的執行緒不會不提取視窗訊息，可能會造成問題。 潛在的問題包括 ADO 不傳遞到執行緒和全域視窗廣播逾時並因為隱藏的視窗不會處理訊息，可能降低整個系統的事件。 STA 執行緒通常會有訊息幫浦，因此這個問題不會不會出現在 STA 執行緒上執行。 MTA 執行緒，不過，通常不會有訊息幫浦內所以問題將通常會出現在 MTA 執行緒上。  
  
 此章節包含下列主題。  
  
-   [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [事件類型](../../../ado/guide/data/types-of-events.md)  
  
-   [事件參數](../../../ado/guide/data/event-parameters.md)  
  
-   [事件處理常式一起運作的方式](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件類型](../../../ado/guide/data/types-of-events.md)

