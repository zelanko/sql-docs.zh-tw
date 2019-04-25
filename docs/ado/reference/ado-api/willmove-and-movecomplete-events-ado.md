---
title: WillMove 和 MoveComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::MoveComplete
- WillMove
- MoveComplete
- Recordset::WillMove
helpviewer_keywords:
- MoveComplete event [ADO]
- WillMove event [ADO]
ms.assetid: 1a3d1042-4f30-4526-a0c7-853c242496db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47040adf2ce7be17d0540755f7fa972d7a76266f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642470"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 和 MoveComplete 事件 (ADO)
**WillMove**暫止的作業變更的目前位置之前，會呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **MoveComplete**事件中的目前位置之後，呼叫**資料錄集**變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定此事件的原因。 其值可以是**adRsnMoveFirst**， **adRsnMoveLast**， **adRsnMoveNext**， **adRsnMovePrevious**， **adRsnMove**，或**adRsnRequery**。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 說明如果發生錯誤的值*adStatus*是**adStatusErrorsOccurred**; 否則為未設定參數。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**WillMove**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成。 它會設定為**adStatusCantDeny**如果此事件不能要求取消暫止的作業。  
  
 當**MoveComplete**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成，或**adStatusErrorsOccurred**如果作業失敗。  
  
 再**WillMove**傳回，這個參數設定為**adStatusCancel**要求取消暫止的作業，或將此參數設定為**adStatusUnwantedEvent**若要避免後續的通知。  
  
 再**MoveComplete**傳回，這個參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 A **WillMove**或是**MoveComplete**因為下列原因可能會發生事件**資料錄集**作業：[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)，[移動](../../../ado/reference/ado-api/move-method-ado.md)， [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)， [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)，[AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)，並[Requery](../../../ado/reference/ado-api/requery-method.md)。 這些事件可能會發生因為下列屬性：[篩選條件](../../../ado/reference/ado-api/filter-property.md)， [Index](../../../ado/reference/ado-api/index-property.md)，[書籤](../../../ado/reference/ado-api/bookmark-property-ado.md)， [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)，並[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)。 如果子系，也會發生這些事件**資料錄集**已**資料錄集**連線的事件和父代**資料錄集**移動。  
  
 您必須設定*adStatus*參數來**adStatusUnwantedEvent**每個可能*adReason*才能完全停止的任何事件的事件通知的值，包含*adReason*參數。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
