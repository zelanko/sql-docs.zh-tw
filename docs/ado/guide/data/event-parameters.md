---
title: 事件參數 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26caf2b54b4f0affbbe7cdc58fa2bf742f0d4101
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925360"
---
# <a name="event-parameters"></a>事件參數
每個事件處理常式都有一個控制事件處理常式的 status 參數。 針對完整事件，這個參數也會用來指出產生事件之作業的成功或失敗。 大部分的完整事件也會有錯誤參數，以提供可能發生之任何錯誤的相關資訊，以及參考用來執行作業之 ADO 物件的一或多個物件參數。 例如， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)事件包含與事件相關聯之**命令**、**記錄集**和**連接**物件的物件參數。 在下列 Microsoft® Visual Basic®範例中，您可以看到 pCommand、pRecordset 和 pConnection 物件，其中代表**Execute**方法所使用的**命令**、**記錄集**和**連接**物件。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 除了**錯誤**物件之外，也會將相同的參數傳遞至將會事件。 這可讓您檢查將在暫止作業中使用的每個物件，並判斷是否應該允許作業完成。  
  
 某些事件處理常式具有*Reason*參數，可提供事件發生原因的其他資訊。 例如， **WillMove**和**MoveComplete**事件可能是因為呼叫任何一種流覽方法（**MoveNext**、 **MovePrevious**等等），或因重新查詢的結果而發生。  
  
## <a name="status-parameter"></a>Status 參數  
 呼叫事件處理常式常式時， *Status*參數會設定為下列其中一個值。  
  
|值|描述|  
|-----------|-----------------|  
|**adStatusOK**|同時傳遞給會和 Complete 事件。 此值表示導致事件成功完成的作業。|  
|**adStatusErrorsOccurred**|僅傳遞至完整的事件。 此值表示導致事件的作業不成功，或將事件取消作業。 請檢查*錯誤*參數以取得詳細資料。|  
|**adStatusCantDeny**|傳遞至只會有事件。 這個值表示，「事件」無法取消作業。 必須執行此作業。|  
  
 如果您在 [您的事件] 中判斷作業應該繼續執行，請將 [*狀態*] 參數保持不變。 不過，只要 [內送狀態] 參數未設定為 [ **adStatusCantDeny**]，您就可以將*狀態*變更為 [ **adStatusCancel**] 來取消暫止的作業。 當您這麼做時，與作業相關聯的完整事件會將其*Status*參數設定為**adStatusErrorsOccurred**。 傳遞至 Complete 事件的**Error**物件將包含值**adErrOperationCancelled**。  
  
 如果您不想再處理事件，您可以將*狀態*設定為**adStatusUnwantedEvent** ，您的應用程式就不會再收到該事件的通知。 不過，請記住，某些事件可能會因為一個以上的原因而引發。 在這種情況下，您必須針對每個可能的原因指定**adStatusUnwantedEvent** 。 例如，若要停止接收暫止**RecordChange**事件的通知，您必須在**adRsnAddNew**、 **adRsnDelete**、 **adRsnUpdate**、adRsnUndoUpdate、 **AdRsnUndoAddNew**、 **AdRsnUndoDelete**和**adRsnFirstChange**發生**時，將** *Status*參數設定為**adStatusUnwantedEvent** 。  
  
|值|描述|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|要求此事件處理常式不會再收到任何通知。|  
|**adStatusCancel**|要求取消即將發生的作業。|  
  
## <a name="error-parameter"></a>錯誤參數  
 *錯誤*參數是 ADO[錯誤](../../../ado/reference/ado-api/error-object.md)物件的參考。 當*Status*參數設定為**AdStatusErrorsOccurred**時，**錯誤**物件會包含作業失敗原因的詳細資料。 如果與完成事件相關聯的事件已藉由將*Status*參數設定為**adStatusCancel**來取消作業，則錯誤物件一律會設定為**adErrOperationCancelled**。  
  
## <a name="object-parameter"></a>物件參數  
 每個事件都會接收一或多個物件，代表包含在作業中的物件。 例如， **ExecuteComplete**事件會接收**Command**物件、 **Recordset**物件和**Connection**物件。  
  
## <a name="reason-parameter"></a>原因參數  
 *Reason*參數*adReason*會提供事件發生原因的其他資訊。 具有*adReason*參數的事件可能會被呼叫數次，即使是相同的作業，每次都會有不同的原因。 例如， **WillChangeRecord**事件處理常式會針對即將執行或復原記錄的插入、刪除或修改的作業呼叫。 如果您只想要在發生特定原因時處理事件，您可以使用*adReason*參數來篩選出您不感興趣的出現次數。 例如，如果您只想要在因為已加入記錄而發生記錄變更事件時進行處理，您可以使用如下所示的內容。  
  
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
  
 在此情況下，可能會因其他原因而發生通知。 不過，每個原因只會發生一次。 在每個原因都發生通知之後，您只會收到加入新記錄的通知。  
  
 相反地，您必須將*adStatus*設定為只**adStatusUnwantedEvent**一次，要求沒有**adReason**參數的事件處理常式停止接收事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [依語言的 ADO 事件具現化](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件處理常式如何搭配使用](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件的類型](../../../ado/guide/data/types-of-events.md)
