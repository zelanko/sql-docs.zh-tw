---
title: WillChangeRecordset 和 RecordsetChangeComplete 事件（ADO） |Microsoft Docs
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
ms.openlocfilehash: dd4e2f1485c18ce1fecc76d4eb23aa4132d85329
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67938681"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)
在暫止的作業變更[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之前，會呼叫**WillChangeRecordset**事件。 **RecordsetChangeComplete**事件是在**記錄集**變更後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定此事件的原因。 其值可以是**adRsnRequery**、 **adRsnResynch**、 **adRsnClose**、 **adRsnOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫**WillChangeRecordset**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** 。 如果此事件無法要求取消暫止的作業，則會設定為**adStatusCantDeny** 。  
  
 當呼叫**RecordsetChangeComplete**時，如果造成事件的作業成功，則會將此參數設定為**adStatusOK** ，如果作業失敗則為**adStatusErrorsOccurred** ; 如果已取消與先前接受之**WillChangeRecordset**事件關聯的作業，則會**adStatusCancel** 。  
  
 在**WillChangeRecordset**傳回之前，請將此參數設定為**adStatusCancel** ，以要求取消暫止的作業，或將此參數設定為 adStatusUnwantedEvent，以防止後續的通知。  
  
 在**WillChangeRecordset**或**RecordsetChangeComplete**傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述*adStatus*的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *pRecordset*  
 **記錄集**物件。 發生此事件的**記錄集**。  
  
## <a name="remarks"></a>備註  
 **WillChangeRecordset**或**RecordsetChangeComplete**事件可能是因為**記錄集**重新[查詢](../../../ado/reference/ado-api/requery-method.md)或[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法所造成。  
  
 如果提供者不支援書簽，每次從提供者抓取新的資料列時，就會發生**RecordsetChange**事件通知。 這個事件的頻率取決於**RecordsetCacheSize**屬性。  
  
 您必須針對每個可能的**adReason**值，將**adStatus**參數設定為**adStatusUnwantedEvent** ，以完全停止包含**adReason**參數之任何事件的事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
