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
manager: jroth
ms.openlocfilehash: 2912328aa61437b663a290952deaaea7b5c06bca
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700755"
---
# <a name="event-parameters"></a>事件參數
每個事件處理常式具有控制事件處理常式的狀態參數。 完整的事件，這個參數也用來表示成功或失敗的作業產生事件。 最完整的事件也會有一個錯誤的參數提供任何可能已發生的錯誤和參考用來執行作業的 ADO 物件的一或多個物件參數的相關資訊。 例如， [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)事件包含物件的參數**命令**，**資料錄集**，並**連接**物件與事件相關聯。 在下列的 Microsoft® Visual Basic® 範例中，您可以看到 pCommand、 pRecordset 和 pConnection 物件代表**命令**， **Recordset**，和**連接**所使用的物件**Execute**方法。  
  
```  
Private Sub connEvent_ExecuteComplete(ByVal RecordsAffected As Long, _  
     ByVal pError As ADODB.Error, _  
     adStatus As ADODB.EventStatusEnum, _  
     ByVal pCommand As ADODB.Command, _  
     ByVal pRecordset As ADODB.Recordset, _  
     ByVal pConnection As ADODB.Connection)  
```  
  
 除了**錯誤**物件，將事件傳遞相同的參數。 這樣，您可以檢查每個物件，將會用於暫止的作業，並判斷是否應該允許此作業完成。  
  
 有一些事件處理常式*原因*參數，提供事件的發生原因的其他資訊。 例如， **WillMove**並**MoveComplete**事件可能會發生任何一種瀏覽方法 (**MoveNext**， **MovePrevious**等等) 的呼叫，或重新查詢的結果。  
  
## <a name="status-parameter"></a>狀態參數  
 當呼叫的事件處理常式時，*狀態*參數設定為下列值之一。  
  
|值|描述|  
|-----------|-----------------|  
|**adStatusOK**|傳遞至會與完成事件。 這個值表示造成事件已順利完成的作業。|  
|**adStatusErrorsOccurred**|傳遞至完成的事件。 這個值表示造成事件的作業不成功，或將事件已取消作業。 請檢查*錯誤*參數，如需詳細資訊。|  
|**adStatusCantDeny**|傳遞至僅適用於將事件。 這個值表示將事件無法取消此操作。 必須執行。|  
  
 如果您判斷在您將情況下，作業應該繼續，請將保留*狀態*未變更的參數。 只要連入的狀態參數未設定為**adStatusCantDeny**，不過，您可以取消暫止的作業，藉由變更*狀態*來**adStatusCancel**。 當您這樣做時，完成與作業相關聯的事件具有其*狀態*參數設為**adStatusErrorsOccurred**。 **錯誤**物件傳遞至完成的事件會包含值**adErrOperationCancelled**。  
  
 如果您不再想要處理事件，您可以設定*狀態*要**adStatusUnwantedEvent**和您的應用程式將不會再收到該事件的通知。 不過請記住，多個原因會引發某些事件。 在此情況下，您必須指定**adStatusUnwantedEvent**的每個可能的原因。 例如，若要停止接收通知的暫止**RecordChange**事件，您必須設定*狀態*參數**adStatusUnwantedEvent**如**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**，**adRsnUndoDelete**，並**adRsnFirstChange**發生。  
  
|值|描述|  
|-----------|-----------------|  
|**adStatusUnwantedEvent**|要求此事件處理常式會收到任何進一步的通知。|  
|**adStatusCancel**|要求取消作業，會發生。|  
  
## <a name="error-parameter"></a>錯誤參數  
 *錯誤*參數是參考 ADO[錯誤](../../../ado/reference/ado-api/error-object.md)物件。 當*狀態*參數設為**adStatusErrorsOccurred**，則**錯誤**物件包含有關作業失敗的原因的詳細資訊。 如果將相關聯的事件與完整的事件已取消作業，藉由設定*狀態*參數來**adStatusCancel**，錯誤物件永遠設**adErrOperationCancelled**。  
  
## <a name="object-parameter"></a>物件參數  
 每個事件會接收一或多個物件，並代表與作業有關的物件。 比方說， **ExecuteComplete**事件會接收**命令**物件**資料錄集**物件，以及**連接**物件。  
  
## <a name="reason-parameter"></a>原因參數  
 *原因*參數*adReason*，提供事件的發生原因的其他資訊。 事件*adReason*參數可能被呼叫多次，甚至是相同的作業，因其他原因每次。 例如， **WillChangeRecord**事件處理常式會呼叫針對即將執行或復原的插入、 刪除或修改一筆記錄的作業。 如果您想要處理的事件，只有當它發生的特定原因，您可以使用*adReason*參數來篩選出您不感興趣的出現次數。 例如，如果您想要處理記錄變更事件，僅在發生因為已加入一筆記錄時，您可以使用類似下列的內容。  
  
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
  
 在此情況下，通知可能可以針對每個其他原因而發生。 不過，它會發生一次每個原因。 通知已發生一次每個原因之後，您會收到通知，只會針對加入的新記錄。  
  
 相反地，您需要設定*adStatus*要**adStatusUnwantedEvent**要求一次事件處理常式，而不需要**adReason**參數停止接收事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [ADO 事件具現化語言](../../../ado/guide/data/ado-event-instantiation-by-language.md)   
 [事件處理常式如何一起運作](../../../ado/guide/data/how-event-handlers-work-together.md)   
 [事件的類型](../../../ado/guide/data/types-of-events.md)
