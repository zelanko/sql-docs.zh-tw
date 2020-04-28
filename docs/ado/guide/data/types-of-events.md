---
title: 事件種類 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EventComplete event [ADO]
- events [ADO], types
- Will events [ADO]
- complete events [ADO]
- WillEvent event [ADO]
ms.assetid: f3327ea0-635a-43d4-bd78-c1674f62f1a2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c02d8d115a4336470c0e0d32aebabea63c05ab0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923819"
---
# <a name="types-of-events"></a>事件的類型
有兩種基本類型的事件。 「將會在作業開始之前呼叫的事件」，通常會在其名稱中包含 ""，例如**WillChangeRecordset**或**WillConnect**。 在事件完成後呼叫的事件通常會在其名稱中包含「完成」，例如**RecordChangeComplete**或**ConnectComplete**。 例外狀況存在（例如**InfoMessage** ），但在相關聯的作業完成後發生。  
  
## <a name="will-events"></a>將會發生事件  
 在作業開始之前呼叫的事件處理常式，可讓您有機會檢查或修改作業參數，然後取消作業或允許它完成。 這些事件處理常式常式通常會有表單的名稱，<strong>也就是*事件*</strong>。  
  
## <a name="complete-events"></a>完成事件  
 在作業完成後呼叫的事件處理常式，可以通知您的應用程式作業已結束。 當事件處理常式取消暫止的作業時，也會通知這類事件處理常式。 這些事件處理常式常式通常會有已完成的表單<strong>*事件*</strong>名稱。  
  
 和完整的事件通常會成對使用。  
  
## <a name="other-events"></a>其他事件  
 其他事件處理常式（也就是，其名稱不是其形式的事件）<strong>將會*Event* </strong> <strong> *Event*完成</strong>，只有在作業完成之後才會呼叫。 這些事件為**Disconnect**、 **EndOfRecordset**和**InfoMessage**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [依語言的 ADO 事件具現化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件處理常式如何協同運作](../../../ado/guide/data/how-event-handlers-work-together.md)
