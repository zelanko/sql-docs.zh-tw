---
title: 類型的事件 |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: b324857816df774486716978425d1332a695952a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708466"
---
# <a name="types-of-events"></a>事件的類型
有兩種基本的事件。 「 將事件 」 作業啟動之前呼叫它，通常是名稱中包含 「 將 」 — 比方說， **WillChangeRecordset**或**WillConnect**。 通常已完成事件後，會呼叫的事件其名稱中包含 「 完成 」 — 例如， **RecordChangeComplete**或是**ConnectComplete**。 例外狀況，例如**InfoMessage** — 但相關聯的作業完成後，會發生這些情況。  
  
## <a name="will-events"></a>將事件  
 作業開始提供您機會檢查或修改作業的參數，然後取消作業，或讓其完成之前，就會呼叫事件處理常式。 這些事件處理常式通常會有名稱格式 **將*事件 * * *。  
  
## <a name="complete-events"></a>完成事件  
 作業完成之後呼叫的事件處理常式可以通知您作業已完成的應用程式。 將事件處理常式取消暫止的作業時，這類事件處理常式也會收到通知。 這些事件處理常式通常會有名稱格式 ***事件 * 完成**。  
  
 將完整的事件通常會使用和成對。  
  
## <a name="other-events"></a>其他事件  
 其他事件處理常式 — 也就是事件名稱不是表單**將 * 事件*** 或 ***事件 * 完成**— 只有在作業完成之後，才會呼叫。 這些事件**中斷連線**， **EndOfRecordset**，並**InfoMessage**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件處理常式如何協同運作](../../../ado/guide/data/how-event-handlers-work-together.md)
