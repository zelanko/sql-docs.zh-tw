---
title: WillChangeRecord 和 RecordChangeComplete 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: 6e632db34fbbacbee61cd943067052af27a8cfe8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938671"
---
# <a name="willchangerecord-and-recordchangecomplete-events-ado"></a>WillChangeRecord 和 RecordChangeComplete 事件 (ADO)
**WillChangeRecord**事件是在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)內的一或多筆記錄（資料列）變更之前呼叫。 **RecordChangeComplete**事件會在一或多筆記錄變更後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeRecord adReason, cRecords, adStatus, pRecordset  
RecordChangeCompleteadReason, cRecords, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定此事件的原因。 其值可以是**adRsnAddNew**、 **adRsnDelete**、 **adRsnUpdate**、 **adRsnUndoUpdate**、 **adRsnUndoAddNew**、 **adRsnUndoDelete**或**adRsnFirstChange**。  
  
 *cRecords*  
 **Long**值，指出變更的記錄數目（受影響）。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述*adStatus*的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫**WillChangeRecord**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** 。 如果此事件無法要求取消暫止的作業，則會設定為**adStatusCantDeny** 。  
  
 當呼叫**RecordChangeComplete**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** ，如果作業失敗，則設為**adStatusErrorsOccurred** 。  
  
 在**WillChangeRecord**傳回之前，請將此參數設定為**adStatusCancel** ，以要求取消造成此事件的作業，或將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 在**RecordChangeComplete**傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 **記錄集**物件。 發生此事件的**記錄集**。  
  
## <a name="remarks"></a>備註  
 由於下列**記錄集**作業，資料列中第一個已變更的欄位可能會發生**WillChangeRecord**或**RecordChangeComplete**事件： [Update](../../../ado/reference/ado-api/update-method.md)、 [Delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)、 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)、 [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md)、 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)和[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)。 **記錄集** [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)的值會決定造成事件發生的作業。  
  
 在**WillChangeRecord**事件期間，**記錄集**[篩選](../../../ado/reference/ado-api/filter-property.md)屬性會設定為**adFilterAffectedRecords**。 您無法在處理事件時變更此屬性。  
  
 您必須針對每個可能的**adReason**值，將**adStatus**參數設定為**adStatusUnwantedEvent** ，以完全停止包含**adReason**參數之任何事件的事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
