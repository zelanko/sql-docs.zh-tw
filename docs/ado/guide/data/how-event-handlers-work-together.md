---
title: 事件處理常式一起運作的方式 |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- unpaired event handlers [ADO]
- paired event handlers [ADO]
- single event handlers [ADO]
- event handlers [ADO]
- multiple object event handlers [ADO]
ms.assetid: a86c8a02-dd69-420d-8a47-0188b339858d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ef9af3c4ba076048e0d04d31601b20e9d9ca321
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="how-event-handlers-work-together"></a>事件處理常式一起運作的方式
除非您在 Visual Basic 中，所有的事件處理常式中進行程式設計**連接**和**資料錄集**事件必須實作，不論是否是您實際處理的所有事件。 您只需要實作工作數量取決於您的程式語言。 如需詳細資訊，請參閱[ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)。  
  
## <a name="paired-event-handlers"></a>配對的事件處理常式  
 每個將事件處理常式都具有相關聯**完成**事件處理常式。 例如，當您的應用程式變更欄位的值， **WillChangeField**會呼叫事件處理常式。 如果這是可接受的變更，您的應用程式會使**adStatus**參數不變，而且執行作業。 當作業完成時， **FieldChangeComplete**事件會通知您作業已完成的應用程式。 如果成功， **adStatus**包含**adStatusOK**，否則**adStatus**包含**adStatusErrorsOccurred**和您必須檢查**錯誤**物件，以判斷錯誤的原因。  
  
 當**WillChangeField**是呼叫，您可能決定不進行變更。 在此情況下，設定**adStatus**至**adStatusCancel。** 在作業取消並**FieldChangeComplete**事件都會接收**adStatus**值**adStatusErrorsOccurred**。 **錯誤**物件包含**adErrOperationCancelled** ，讓您**FieldChangeComplete**處理常式可讓您知道作業已取消。 不過，您需要檢查的值**adStatus**參數，然後再變更它，因為設定**adStatus**至**adStatusCancel**沒有任何作用，如果設定了參數若要**adStatusCantDeny**程序項目。  
  
 有時作業可能會引發多個事件。 例如，**資料錄集**物件有配對的事件**欄位**變更和**記錄**變更。 當您的應用程式變更的值**欄位**、 **WillChangeField**會呼叫事件處理常式。 如果它決定可以繼續操作， **WillChangeRecord**也會引發事件處理常式。 如果這個處理常式也可讓繼續事件，進行變更和**FieldChangeComplete**和**RecordChangeComplete**會呼叫事件處理常式。 未定義稱為將事件處理常式的特定作業的順序，因此您應該避免撰寫依賴特定順序呼叫處理常式的程式碼。  
  
 執行個體在多個將會引發事件，當其中一個事件可能會取消暫止的作業。 例如，當您的應用程式的值變更**欄位**，這兩個**WillChangeField**和**WillChangeRecord**通常會呼叫事件處理常式。 不過，如果在作業取消第一個事件處理常式，其相關聯**完成**與立即呼叫處理常式**adStatusOperationCancelled**。 絕不會呼叫第二個處理常式。 如果，不過，第一個事件處理常式可讓繼續事件，則會呼叫此事件處理常式。 如果它再取消作業，同時**完成**事件將會被呼叫，如先前範例所示。  
  
## <a name="unpaired-event-handlers"></a>未配對的事件處理常式  
 只要狀態傳遞至事件就不會**adStatusCantDeny**，您可以藉由傳回關閉的任何事件的事件通知**adStatusUnwantedEvent**中*狀態*參數。 例如，當您**完成**第一次時，會呼叫事件處理常式，您可以傳回**adStatusUnwantedEvent**。 您接著會只收到**將**事件。 不過，某些事件可以觸發多個原因。 在此情況下，會有事件*原因*參數。 當您傳回**adStatusUnwantedEvent**，您將會停止接收通知事件只針對該特定原因發生的時候。 換句話說，您可能會收到通知的每個可能的原因，可能會觸發此事件。  
  
 單一**將**事件處理常式可以是很有用，當您想要檢查將會在作業中使用的參數。 您可以修改這些作業的參數，或取消作業。  
  
 或者，將**完成**啟用事件通知。 當您第一次將事件處理常式呼叫時，傳回**adStatusUnwantedEvent**。 您接著會只收到**完成**事件。  
  
 單一**完成**事件處理常式可用於管理非同步作業。 每個非同步作業已適當**完成**事件。  
  
 例如，可能需要很長的時間來擴展大型[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 如果您的應用程式適當地寫入，您可以啟動`Recordset.Open(...,adAsyncExecute)`作業並繼續進行其他處理。 最後將會收到通知時**資料錄集**會填入**ExecuteComplete**事件。  
  
## <a name="single-event-handlers-and-multiple-objects"></a>單一事件處理常式和多個物件  
 Microsoft 等程式設計語言的彈性可讓您有一個來自多個物件的事件處理常式處理事件。 例如，您可以有一個**中斷連線**事件處理常式處理事件從幾個**連接**物件。 如果其中一個連線結束時，**中斷連線**會呼叫事件處理常式。 您無法分辨哪一個連接是引發事件，因為事件處理常式物件參數會設定為對應**連接**物件。  
  
> [!NOTE]
>  無法在 Visual Basic 中使用這項技術，因為該語言可以相互關聯之事件處理常式只有一個物件。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件參數](../../../ado/guide/data/event-parameters.md)   
 [事件的類型](../../../ado/guide/data/types-of-events.md)
