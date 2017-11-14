---
title: "事件參數 |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Error parameter [ADO]
- Object parameter [ADO]
- Status parameter [ADO]
- events [ADO], parameters
- Reason parameter [ADO]
- event parameters [ADO]
ms.assetid: bd5c5afa-d301-4899-acda-40f98a6afa4d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9ae7ee638c8489795df8894be23ef80e63b26f07
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="event-parameters"></a>事件參數
每個事件處理常式具有控制事件處理常式的狀態參數。 完成事件，這個參數也用來表示成功或失敗的作業產生事件。 最完整的事件也具有錯誤參數，以提供可能會發生任何錯誤和參考用來執行作業的 ADO 物件的一或多個物件參數的資訊。 例如， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)事件包含物件的參數**命令**，**資料錄集**，和**連接**物件與事件相關聯。 在下列的 Microsoft® Visual Basic® 範例中，您可以看到 pCommand、 pRecordset 和 pConnection 物件代表**命令**，**資料錄集**，和**連接**物件所使用的**Execute**方法。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 除了**錯誤**物件、 將事件傳遞相同的參數。 此讓您檢查每個將用於暫止的作業，並判斷是否應該允許此作業完成的物件。  
  
 某些事件處理常式有*原因*參數，提供關於事件的發生原因的其他資訊。 例如， **WillMove**和**MoveComplete**事件可能會發生任何一種瀏覽方法 (**MoveNext**， **MovePrevious**，依此類推) 正在執行呼叫，或重新查詢的結果。  
  
## <a name="status-parameter"></a>狀態參數  
 當呼叫事件處理常式時，*狀態*參數設定為下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**adStatusOK**|傳遞至將會與完成事件。 這個值表示造成事件已順利完成的作業。|  
|**adStatusErrorsOccurred**|傳遞至僅適用於使用完整的事件。 這個值表示造成事件的作業不成功，或將事件取消該作業。 請檢查*錯誤*參數，如需詳細資訊。|  
|**adStatusCantDeny**|傳遞至僅適用於將事件。 這個值表示將事件無法取消此操作。 必須執行。|  
  
 如果您判斷您會在事件中，作業應該繼續，請將保留*狀態*參數保持不變。 只要連入的狀態參數未設定為**adStatusCantDeny**，不過，您可以取消暫止的作業，藉由變更*狀態*至**adStatusCancel**。 當您這樣做時，完成與作業相關聯的事件都有其*狀態*參數設定為**adStatusErrorsOccurred**。 **錯誤**物件傳遞至完成的事件將包含值**adErrOperationCancelled**。  
  
 如果您不再想要處理事件，您可以設定*狀態*至**adStatusUnwantedEvent**和您的應用程式不會再接收該事件的通知。 不過請記住，某些事件可能會引發多個原因。 在此情況下，您必須指定**adStatusUnwantedEvent**的每個可能的原因。 例如，若要停止接收通知的暫止**RecordChange**事件，您必須設定*狀態*參數**adStatusUnwantedEvent**如**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**，**adRsnUndoDelete**，和**adRsnFirstChange**發生。  
  
|值|Description|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|要求此事件處理常式會接收任何進一步的通知。|  
|**adStatusCancel**|要求取消作業，會發生。|  
  
## <a name="error-parameter"></a>錯誤的參數  
 *錯誤*參數是 ADO 參考[錯誤](../../../ado/reference/ado-api/error-object.md)物件。 當*狀態*參數設定為**adStatusErrorsOccurred**、**錯誤**物件包含有關作業失敗的原因詳細資料。 如果完成的事件與關聯的將事件已取消該作業，藉由設定*狀態*參數**adStatusCancel**，錯誤物件一定會設定為**adErrOperationCancelled**。  
  
## <a name="object-parameter"></a>物件參數  
 每個事件都會接收代表作業中所涉及的物件的一或多個物件。 例如， **ExecuteComplete**事件會接收**命令**物件**資料錄集**物件，和**連接**物件。  
  
## <a name="reason-parameter"></a>原因參數  
 *原因*參數， *adReason*，提供事件的發生原因的其他資訊。 事件的*adReason*參數可能被呼叫多次，甚至相同的作業，每次其他原因。 例如， **WillChangeRecord**即將執行或復原的插入、 刪除或修改一筆記錄的作業會呼叫事件處理常式。 如果您想要處理事件，只有時特別的理由，您可以使用*adReason*參數來篩選掉您不感興趣的項目。 例如，如果您想要處理記錄變更只有在發生事件時因為已新增一筆記錄，您可以使用像下面這樣。  
  
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
  
 在此情況下，通知可能可以針對每個其他原因發生。 不過，它會發生一次只能每個原因。 通知已發生一次每個原因之後，您會收到通知只供新增新的記錄。  
  
 相反地，您需要設定*adStatus*至**adStatusUnwantedEvent**一次要求的事件處理常式，而不**adReason**參數停止接收事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件處理常式一起運作的方式](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件類型](../../../ado/guide/data/types-of-events.md)

