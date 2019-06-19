---
title: WillChangeRecord 和 RecordChangeComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- RecordChangeComplete
- Recordset::WillChangeRecord
- WillChangeRecord
- Recordset::RecordChangeComplete
helpviewer_keywords:
- WillChangeRecord event [ADO]
- recordchangecomplete event [ADO]
ms.assetid: cbc369fd-63af-4a7d-96ae-efa91b78ca69
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: ef2e02ec156aeed69089a585d743e16e592eb95f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710152"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 和 RecordChangeComplete 事件 (ADO)
**WillChangeRecord**之前一或多個資料錄 （資料列），會呼叫事件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)變更。 **RecordChangeComplete**事件被呼叫一次之後，或更多記錄變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定此事件的原因。 其值可以是**adRsnAddNew**， **adRsnDelete**， **adRsnUpdate**， **adRsnUndoUpdate**， **adRsnUndoAddNew**， **adRsnUndoDelete**，或**adRsnFirstChange**。  
  
 *cRecords*  
 A**長**值，指出變更的記錄數目 （受影響）。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它說明如果發生錯誤的值*adStatus*是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**WillChangeRecord**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成。 它會設定為**adStatusCantDeny**如果此事件不能要求取消暫止的作業。  
  
 當**RecordChangeComplete**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成，或**adStatusErrorsOccurred**如果作業失敗。  
  
 再**WillChangeRecord**傳回，這個參數設定為**adStatusCancel**來要求取消作業，導致此事件，或將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 再**RecordChangeComplete**傳回，這個參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 A **WillChangeRecord**或是**RecordChangeComplete**可能會發生事件之變更的第一個欄位，因為下列資料列中**資料錄集**作業：[更新](../../../ado/reference/ado-api/update-method.md)，[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)， [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)， [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，以及[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md). 值**Recordset** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)決定哪個作業導致發生的事件。  
  
 期間**WillChangeRecord**事件， **Recordset** [篩選](../../../ado/reference/ado-api/filter-property.md)屬性設定為**adFilterAffectedRecords**。 處理事件時，您無法變更此屬性。  
  
 您必須設定**adStatus**參數來**adStatusUnwantedEvent**每個可能**adReason**完全停止，其中包含的任何事件的事件通知的值**adReason**參數。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
