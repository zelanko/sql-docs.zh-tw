---
description: 事件處理常式如何協同運作
title: 事件處理常式如何一起運作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a571c36a67a4d2c1c3b98c64c826af949b0e773
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453250"
---
# <a name="how-event-handlers-work-together"></a>事件處理常式如何協同運作
除非您是在 Visual Basic 中進行程式設計，否則無論您是否真的處理所有事件，都必須實作為 **連接** 和 **記錄集** 事件的所有事件處理常式。 您必須執行的實作為工作量取決於您的程式設計語言。 如需詳細資訊，請參閱 [ADO 事件具現化（依語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)）。  
  
## <a name="paired-event-handlers"></a>成對的事件處理常式  
 每個事件處理常式都會有相關聯的 **完整** 事件處理常式。 例如，當您的應用程式變更欄位的值時，就會呼叫 **WillChangeField** 事件處理常式。 如果可接受變更，您的應用程式會讓 **adStatus** 參數保持不變，並執行此作業。 當作業完成時， **FieldChangeComplete** 事件會通知您的應用程式作業已完成。 如果成功完成， **adStatus** 會包含 **adStatusOK**;否則， **adStatus** 會包含 **adStatusErrorsOccurred** ，您必須檢查 **error** 物件以判斷錯誤的原因。  
  
 當呼叫 **WillChangeField** 時，您可能會決定不應該進行變更。 在此情況下，請將 **adStatus** 設定為 **adStatusCancel。** 作業已取消， **FieldChangeComplete**事件會接收**adStatusErrorsOccurred**的**adStatus**值。 **錯誤**物件包含**adErrOperationCancelled** ，讓您的**FieldChangeComplete**處理常式知道作業已取消。 不過，您必須先檢查**adStatus**參數的值，然後再進行變更，因為如果將參數設定為 [ **adStatusCantDeny** ]，則將**adStatus**設定為 [ **adStatusCancel** ] 不會有任何作用。  
  
 有時作業可能引發一個以上的事件。 例如， **記錄集** 物件已將 **欄位** 變更和 **記錄** 變更的事件配對。 當您的應用程式變更 **欄位**的值時，就會呼叫 **WillChangeField** 事件處理常式。 如果判斷作業可以繼續，也會引發 **WillChangeRecord** 事件處理常式。 如果此處理程式也允許事件繼續進行，則會進行變更並呼叫 **FieldChangeComplete** 和 **RecordChangeComplete** 事件處理常式。 系統不會定義特定作業之事件處理常式的呼叫順序，所以您應該避免撰寫相依于特定序列中呼叫處理常式的程式碼。  
  
 在實例中，當引發多個事件時，其中一個事件可能會取消暫止的作業。 例如，當您的應用程式變更 **欄位**的值時，通常會呼叫 **WillChangeField** 和 **WillChangeRecord** 事件處理常式。 但是，如果在第一個事件處理常式中取消作業，則會立即使用**adStatusOperationCancelled**來呼叫其相關聯的**完整**處理常式。 絕不會呼叫第二個處理常式。 但是，如果第一個事件處理常式允許事件繼續進行，則會呼叫另一個事件處理常式。 如果它接著取消作業，則會如先前的範例所示呼叫這兩個 **完整** 事件。  
  
## <a name="unpaired-event-handlers"></a>不成對的事件處理常式  
 只要不**adStatusCantDeny**傳遞至事件的狀態，您就可以在*status*參數中傳回**adStatusUnwantedEvent** ，以關閉任何事件的事件通知。 例如，當您第一次呼叫 **完整** 事件處理常式時，您可以傳回 **adStatusUnwantedEvent**。 您稍後將**只會收到事件。** 不過，某些事件可能會因為一個以上的原因而觸發。 在此情況下，事件將會有 *Reason* 參數。 當您傳回 **adStatusUnwantedEvent**時，您只會在發生特定原因時，停止接收該事件的通知。 換句話說，您可能會收到事件可能觸發的每個可能原因的通知。  
  
 當您想要檢查將在作業中使用的參數時 **，事件處理常式會很** 有用。 您可以修改這些作業參數或取消作業。  
  
 或者，讓 **完成** 的事件通知保持啟用狀態。 當您的第一個會呼叫事件處理常式時，會傳回 **adStatusUnwantedEvent**。 您接下來將只會收到 **完整** 的事件。  
  
 單一 **完整** 事件處理常式有助於管理非同步作業。 每個非同步作業都有適當的 **完整** 事件。  
  
 例如，填入大型 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md) 物件可能需要很長的時間。 如果您的應用程式已正確撰寫，您可以啟動作業 `Recordset.Open(...,adAsyncExecute)` ，並繼續進行其他處理。 當 **記錄集** 是由 **ExecuteComplete** 事件填入時，最終會收到通知。  
  
## <a name="single-event-handlers-and-multiple-objects"></a>單一事件處理常式和多個物件  
 程式設計語言的彈性（例如 Microsoft Visual C++®）可讓您有一個事件處理常式處理來自多個物件的事件。 例如，您可能有一個 **中斷** 連接事件處理常式處理來自數個 **連接** 物件的事件。 如果其中一個連接結束，則會呼叫 **中斷連接** 事件處理常式。 您可以判斷哪個連接造成事件，因為事件處理常式物件參數會設定為對應的 **連接** 物件。  
  
> [!NOTE]
>  這項技術無法在 Visual Basic 中使用，因為該語言只能將一個物件關聯至事件處理常式。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化（依語言）](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件種類](../../../ado/guide/data/types-of-events.md)
