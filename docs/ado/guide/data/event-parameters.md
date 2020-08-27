---
description: 事件參數
title: 事件參數 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
author: rothja
ms.author: jroth
ms.openlocfilehash: cc36f0ab059bb7b605b02316008a969411663a8d
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991299"
---
# <a name="event-parameters"></a>事件參數
每個事件處理常式都有一個狀態參數，可控制事件處理常式。 若為完整事件，此參數也會用來指出產生事件的作業成功或失敗。 大部分的完整事件也都有 error 參數，以提供可能發生之任何錯誤的相關資訊，以及一個或多個物件參數參考用來執行作業的 ADO 物件。 例如， [ExecuteComplete](../../reference/ado-api/executecomplete-event-ado.md) 事件包含 **命令**的物件參數、 **記錄集**，以及與事件相關聯的 **連接** 物件。 在下列 Microsoft® Visual Basic®範例中，您可以看到 pCommand、pRecordset 和 pConnection 物件，這些物件代表**Execute**方法所使用的**命令**、**記錄集**和**連接**物件。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 除了 **Error** 物件以外，也會將相同的參數傳遞至將會是事件。 這可讓您檢查將在暫止作業中使用的每個物件，並判斷是否應該允許該作業完成。  
  
 某些事件處理常式有 *Reason* 參數，可提供事件發生原因的其他相關資訊。 例如， **WillMove** 和 **MoveComplete** 事件可能是因為任何一種流覽方法 (**MoveNext**、 **MovePrevious**等等) 被呼叫，或做為重新查詢的結果。  
  
## <a name="status-parameter"></a>Status 參數  
 當呼叫事件處理常式常式時， *Status* 參數會設定為下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**adStatusOK**|傳遞至兩者都會完成事件。 這個值表示導致事件的作業已順利完成。|  
|**adStatusErrorsOccurred**|只傳遞給完成的事件。 這個值表示導致事件的作業不成功，或是事件會取消作業。 如需詳細資料，請查看 *錯誤* 參數。|  
|**adStatusCantDeny**|傳遞給的只會是事件。 這個值表示「將」事件無法取消作業。 必須執行此作業。|  
  
 如果您在「您的」中判斷出作業應該繼續的事件，請將 *Status* 參數保持不變。 不過，只要傳入的 status 參數未設定為 **adStatusCantDeny**，您就可以將 *狀態* 變更為 **adStatusCancel**，以取消暫止的作業。 當您這樣做時，與作業相關聯的完整事件會將其 *Status* 參數設定為 **adStatusErrorsOccurred**。 傳遞至完整事件的 **Error** 物件將包含 **adErrOperationCancelled**值。  
  
 如果您不想再處理事件，您可以將 *狀態* 設定為 **adStatusUnwantedEvent** ，而您的應用程式將不會再收到該事件的通知。 不過，請記住，某些事件可能會因為一個以上的原因而引發。 在這種情況下，您必須針對每個可能的原因指定 **adStatusUnwantedEvent** 。 例如，若要停止接收暫止**RecordChange**事件的通知，您必須將**adRsnAddNew**、 **adRsnDelete**、 **adRsnUpdate**、 **adRsnUndoUpdate**、 **adRsnUndoAddNew**、 **adRsnUndoDelete**和**adRsnFirstChange**的*Status*參數設定為**adStatusUnwantedEvent** 。  
  
|值|描述|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|要求此事件處理常式不會收到任何其他通知。|  
|**adStatusCancel**|要求取消即將進行的作業。|  
  
## <a name="error-parameter"></a>Error 參數  
 *Error*參數是 ADO [Error](../../reference/ado-api/error-object.md)物件的參考。 當 *Status* 參數設定為 **AdStatusErrorsOccurred**時， **Error** 物件會包含作業失敗原因的詳細資料。 如果與完整事件相關聯的事件已藉由將 *Status* 參數設定為 **adStatusCancel**來取消作業，則錯誤物件一律設定為 **adErrOperationCancelled**。  
  
## <a name="object-parameter"></a>物件參數  
 每個事件都會接收一個或多個物件，代表與作業相關的物件。 例如， **ExecuteComplete** 事件會接收 **命令** 物件、 **記錄集** 物件和 **連接** 物件。  
  
## <a name="reason-parameter"></a>Reason 參數  
 *Reason*參數*adReason*會提供事件發生原因的其他相關資訊。 具有 *adReason* 參數的事件可能會被呼叫數次，即使是針對相同的作業，每次都有不同的原因。 例如，針對即將進行或復原記錄的插入、刪除或修改的作業，呼叫 **WillChangeRecord** 事件處理常式。 如果您只想要在發生特定原因時處理事件，您可以使用 *adReason* 參數來篩選出您不感興趣的專案。 例如，如果您只想要在記錄變更事件因為加入記錄而發生時處理它們，您可以使用如下所示的內容。  
  
```  
' BeginEventExampleVB01  
Private Sub rsTest_WillChangeRecord(ByVal adReason As ADODB.EventReasonEnum, ByVal cRecords As Long, adStatus As ADODB.EventStatusEnum, ByVal pRecordset As ADODB.Recordset)  
   If adReason = adRsnAddNew Then  
       ' Process event  
       '...  
   Else  
       ' Cancel event notification for all  
       ' other possible adReason values.  
       adStatus = adStatusUnwantedEvent  
   End If  
End Sub  
' EndEventExampleVB01  
```  
  
 在此情況下，通知可能會因其他原因而發生。 不過，它只會針對每個原因發生一次。 一旦每個原因發生一次通知，您就只會收到新增記錄的通知。  
  
 相反地，您必須將 *adStatus* 設定為僅 **adStatusUnwantedEvent** 一次，以要求沒有 **adReason** 參數的事件處理常式停止接收事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](./ado-event-handler-summary.md)   
 [ADO 事件具現化（依語言）](./ado-event-instantiation-by-language.md)   
 [事件處理常式如何一起運作](./how-event-handlers-work-together.md)   
 [事件的類型](./types-of-events.md)