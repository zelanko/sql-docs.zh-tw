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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0628c0af52473c3b7eb7200cb4a06bfc45123a10
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758874"
---
# <a name="handling-ado-events"></a>處理 ADO 事件
ADO 事件模型支援在作業開始之前或完成之後，發出*事件*或通知的特定同步和非同步 ADO 作業。 事件實際上是呼叫您在應用程式中定義的事件處理常式常式。  
  
 如果您針對作業開始之前發生的事件群組提供處理函式或程式，您可以檢查或修改傳遞至作業的參數。 因為尚未執行，所以您可以取消作業或允許它完成。  
  
 如果您以非同步方式使用 ADO，在作業完成之後所發生的事件就特別重要。 例如，啟動非同步[記錄集](../../../ado/reference/ado-api/open-method-ado-recordset.md)的應用程式。作業結束時，「執行完成」事件會通知「開啟」作業。  
  
 使用 ADO 事件模型會增加應用程式的額外負荷，但是提供的彈性比其他處理非同步作業的方法更多，例如監視具有迴圈之物件的[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性。  
  
> [!NOTE]
>  若要處理事件，ADO 必須有訊息抽取或用於單一執行緒的單元（STA）模型。 ADO 事件會藉由建立隱藏視窗來進行內部處理。 當事件需要引發時，ADO 會將訊息張貼到這個視窗。 這麼做是為了確保事件會傳送到連接點上呼叫**IConnectionPoint：： Advise**的執行緒。 當應該收到通知的執行緒不會提取視窗訊息時，此架構可能會造成問題。 可能的問題包括不會傳遞至執行緒的 ADO 事件，而全域視窗會廣播計時，而且可能會使整個系統變慢，因為隱藏的視窗不會處理訊息。 STA 執行緒通常會有執行中的訊息提取，因此這個問題不會在 STA 執行緒上單獨出現。 不過，MTA 執行緒通常不會有訊息提取，因此問題通常會在 MTA 執行緒上顯示。  
  
 此章節包含下列主題。  
  
-   [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [事件種類](../../../ado/guide/data/types-of-events.md)  
  
-   [事件參數](../../../ado/guide/data/event-parameters.md)  
  
-   [事件處理常式如何協同運作](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO 事件具現化 (依語言)](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [依語言的 ADO 事件具現化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件種類](../../../ado/guide/data/types-of-events.md)
