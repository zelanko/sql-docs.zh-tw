---
title: WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::RecordsetChangeComplete
- RecordsetChangeComplete
- Recordset::WillChangeRecordset
- WillChangeRecordset
helpviewer_keywords:
- RecordsetChangeComplete event [ADO]
- WillChangeRecordset event [ADO]
ms.assetid: d5d44659-e0d9-46d9-a297-99c43555082f
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5ca84c5759523bf17c4e047b22cafbd48dce547
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66710071"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)
**WillChangeRecordset**事件會被呼叫之前暫止的作業會變更[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **RecordsetChangeComplete**事件之後，呼叫**資料錄集**已變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定此事件的原因。 其值可以是**adRsnRequery**， **adRsnResynch**， **adRsnClose**， **adRsnOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**WillChangeRecordset**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成。 它會設定為**adStatusCantDeny**如果此事件不能要求取消暫止的作業。  
  
 當**RecordsetChangeComplete**是呼叫，此參數設為**adStatusOK**造成事件的作業成功，則**adStatusErrorsOccurred**如果作業失敗，或是**adStatusCancel**如果與先前接受的作業相關聯**WillChangeRecordset**事件已被取消。  
  
 再**WillChangeRecordset**傳回，這個參數設定為**adStatusCancel**要求取消暫止的作業，或將此參數設定來防止 adStatusUnwantedEvent 後續通知。  
  
 之前**WillChangeRecordset**或是**RecordsetChangeComplete**傳回時，會將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它說明如果發生錯誤的值*adStatus*是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *pRecordset*  
 A**資料錄集**物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 A **WillChangeRecordset**或是**RecordsetChangeComplete**事件可能會發生因為**資料錄集** [Requery](../../../ado/reference/ado-api/requery-method.md)或[開啟](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法。  
  
 如果提供者不支援書籤**RecordsetChange**事件通知，就會發生每個提供者會擷取新的資料列的時間。 這個事件的頻率取決於**RecordsetCacheSize**屬性。  
  
 您必須設定**adStatus**參數來**adStatusUnwantedEvent**每個可能**adReason**完全停止，其中包含的任何事件的事件通知的值**adReason**參數。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
