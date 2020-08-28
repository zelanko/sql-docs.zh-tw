---
description: WillMove 和 MoveComplete 事件 (ADO)
title: WillMove 和 MoveComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 27d86dc84960399be6b5738f72c69430c6834c7e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987759"
---
# <a name="willmove-and-movecomplete-events-ado"></a>WillMove 和 MoveComplete 事件 (ADO)
在暫止的作業變更[記錄集](./recordset-object-ado.md)的目前位置之前，會呼叫**WillMove**事件。 **MoveComplete**事件是在**記錄集**的目前位置變更之後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillMove adReason, adStatus, pRecordset  
MoveComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](./eventreasonenum.md)值，指定這個事件的原因。 其值可以是 **adRsnMoveFirst**、 **adRsnMoveLast**、 **adRsnMoveNext**、 **adRsnMovePrevious**、 **adRsnMove**或 **adRsnRequery**。  
  
 *pError*  
 [Error](./error-object.md)物件。 描述 *adStatus* 的值為 **adStatusErrorsOccurred**時所發生的錯誤;否則，就不會設定參數。  
  
 *adStatus*  
 [EventStatusEnum](./eventstatusenum.md)狀態值。  
  
 當呼叫 **WillMove** 時，如果造成事件的作業成功，這個參數會設定為 **adStatusOK** 。 如果此事件無法要求取消暫止的作業，則會設定為 **adStatusCantDeny** 。  
  
 當呼叫 **MoveComplete** 時，如果造成事件的作業成功，這個參數會設定為 **adStatusOK** ，如果作業失敗，則會 **adStatusErrorsOccurred** 。  
  
 在 **WillMove** 傳回之前，請將此參數設定為 **adStatusCancel** 以要求取消暫止的作業，或將此參數設定為 **adStatusUnwantedEvent** 以防止後續的通知。  
  
 在 **MoveComplete** 傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 [記錄集](./recordset-object-ado.md)物件。 發生此事件的 **記錄集** 。  
  
## <a name="remarks"></a>備註  
 **WillMove**或**MoveComplete**事件可能是因為下列**記錄集**作業所造成：[開啟](./open-method-ado-recordset.md)、[移動](./move-method-ado.md)、 [MoveFirst](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveLast](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MoveNext](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)、 [AddNew](./addnew-method-ado.md)和重新[查詢](./requery-method.md)。 這些事件可能會因為下列屬性而發生： [Filter](./filter-property.md)、 [Index](./index-property.md)、 [Bookmark](./bookmark-property-ado.md)、 [AbsolutePage](./absolutepage-property-ado.md)和 [AbsolutePosition](./absoluteposition-property-ado.md)。 如果子 **記錄** 集已連接了 **記錄集** 事件，而且已移動父 **記錄集** ，也會發生這些事件。  
  
 您必須針對每個可能的*adReason*值，將*adStatus*參數設定為**adStatusUnwantedEvent** ，才能完全停止任何包含*adReason*參數之事件的事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](./ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../guide/data/ado-event-handler-summary.md)   
 [Recordset 物件 (ADO)](./recordset-object-ado.md)