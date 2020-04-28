---
title: WillMove 和 MoveComplete 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: c91f3166b493ac1e2fada3e759cb107e34c7ca81
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67945917"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 和 MoveComplete 事件 (ADO)
在暫止的作業變更[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)內的目前位置之前，會呼叫**WillMove**事件。 **MoveComplete**事件是在**記錄集**的目前位置變更後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定此事件的原因。 其值可以是**adRsnMoveFirst**、 **adRsnMoveLast**、 **adRsnMoveNext**、 **adRsnMovePrevious**、 **adRsnMove**或**adRsnRequery**。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述*adStatus*的值為**adStatusErrorsOccurred**時所發生的錯誤。否則，就不會設定參數。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫**WillMove**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** 。 如果此事件無法要求取消暫止的作業，則會設定為**adStatusCantDeny** 。  
  
 當呼叫**MoveComplete**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** ，如果作業失敗，則設為**adStatusErrorsOccurred** 。  
  
 在**WillMove**傳回之前，請將此參數設定為**adStatusCancel**以要求取消暫止的作業，或將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 在**MoveComplete**傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 [記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。 發生此事件的**記錄集**。  
  
## <a name="remarks"></a>備註  
 **WillMove**或**MoveComplete**事件可能會因為下列**記錄集**作業而發生： [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveLast](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)和[Requery](../../../ado/reference/ado-api/requery-method.md)。 這些事件可能是因為下列屬性所造成： [Filter](../../../ado/reference/ado-api/filter-property.md)、 [Index](../../../ado/reference/ado-api/index-property.md)、 [Bookmark](../../../ado/reference/ado-api/bookmark-property-ado.md)、 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md)和[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)。 如果子**記錄集**已連接**記錄集**事件並移動父**記錄集**，也會發生這些事件。  
  
 您必須針對每個可能的*adReason*值，將*adStatus*參數設定為**adStatusUnwantedEvent** ，才能完全停止包含*adReason*參數之任何事件的事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)   
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
