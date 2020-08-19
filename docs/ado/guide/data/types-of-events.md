---
description: 事件的類型
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3fa59b0faeb5b1c74ccd4dff3f9d3c274a8f12c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452680"
---
# <a name="types-of-events"></a>事件的類型
有兩種基本類型的事件。 「將會在作業開始之前呼叫的事件」，通常會在其名稱中包含 "in"，例如 **WillChangeRecordset** 或 **WillConnect**。 在事件完成後呼叫的事件通常會在其名稱中包含 "Complete"，例如 **RecordChangeComplete** 或 **ConnectComplete**。 例外狀況存在（例如 **InfoMessage** ），但在相關聯的作業完成之後就會發生例外狀況。  
  
## <a name="will-events"></a>將會發生事件  
 在作業開始之前呼叫的事件處理常式，可讓您有機會檢查或修改作業參數，然後取消作業或允許其完成。 這些事件處理常式常式通常會有格式為<strong>*事件*</strong>的名稱。  
  
## <a name="complete-events"></a>完成事件  
 作業完成後呼叫的事件處理常式可以通知您的應用程式已結束作業。 當事件處理常式取消暫止的作業時，也會通知這類事件處理常式。 這些事件處理常式常式通常會有形式 <strong>*事件*完成</strong>的名稱。  
  
 和完成事件通常會成對使用。  
  
## <a name="other-events"></a>其他事件  
 其他事件處理常式-也就是，其名稱不是形式的事件<strong>將*Event*會</strong>在<strong> *Event*作業完成時</strong>呼叫。 這些事件會 **中斷**連線、 **EndOfRecordset**和 **InfoMessage**。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化（依語言）](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件處理常式如何協同運作](../../../ado/guide/data/how-event-handlers-work-together.md)
