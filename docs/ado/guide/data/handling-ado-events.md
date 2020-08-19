---
description: 處理 ADO 事件
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
ms.openlocfilehash: 76af7a55c0f3a6e4de2caea7eb3da67e9c27c5cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453310"
---
# <a name="handling-ado-events"></a>處理 ADO 事件
ADO 事件模型支援在作業開始之前或完成之後發出 *事件*或通知的特定同步和非同步 ADO 作業。 事件實際上是呼叫您在應用程式中定義的事件處理常式常式。  
  
 如果您針對作業開始之前發生的事件群組提供處理常式函式或程式，您可以檢查或修改傳遞給作業的參數。 由於尚未執行此作業，您可以取消作業或允許它完成。  
  
 如果您以非同步方式使用 ADO，在作業完成後發生的事件特別重要。 例如，啟動非同步 [記錄集](../../../ado/reference/ado-api/open-method-ado-recordset.md) 的應用程式。當作業結束時，執行完成事件就會通知開啟作業。  
  
 使用 ADO 事件模型會增加應用程式的額外負荷，但提供的彈性比處理非同步作業的其他方法更多，例如使用迴圈監視物件的 [State](../../../ado/reference/ado-api/state-property-ado.md) 屬性。  
  
> [!NOTE]
>  若要處理事件，ADO 必須有訊息提取或用於單一執行緒的單元 (STA) 模型。 ADO 事件是藉由建立隱藏視窗來進行內部處理。 當需要引發事件時，ADO 會將訊息張貼到此視窗。 這樣做的目的是為了確保將事件傳送到連接點上呼叫 **IConnectionPoint：： Advise** 的執行緒。 當接收通知的執行緒不會提取視窗訊息時，此架構可能會造成問題。 可能的問題包括未傳遞至執行緒的 ADO 事件，而全域視窗則會廣播計時，而且可能會使整個系統變慢，因為隱藏的視窗不會處理訊息。 STA 執行緒通常會有一個執行中的訊息，因此這個問題不會在 STA 執行緒上出現。 但是，MTA 執行緒通常不會有訊息提取，因此問題通常會在 MTA 執行緒上出現。  
  
 此章節包含下列主題。  
  
-   [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)  
  
-   [事件種類](../../../ado/guide/data/types-of-events.md)  
  
-   [事件參數](../../../ado/guide/data/event-parameters.md)  
  
-   [事件處理常式如何協同運作](../../../ado/guide/data/how-event-handlers-work-together.md)  
  
-   [ADO 事件具現化 (依語言)](../../../ado/guide/data/ado-event-instantiation-by-language.md)  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化（依語言）](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [ADO 事件](../../../ado/reference/ado-api/ado-events.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件種類](../../../ado/guide/data/types-of-events.md)
