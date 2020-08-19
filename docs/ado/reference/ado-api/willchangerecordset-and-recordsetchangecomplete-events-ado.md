---
description: WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: fa7ec524d950a45dd11e1bc62a983810ab2550ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441510"
---
# <a name="willchangerecordset-and-recordsetchangecomplete-events-ado"></a>WillChangeRecordset 和 RecordsetChangeComplete 事件 (ADO)
在暫止的作業變更[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之前，會呼叫**WillChangeRecordset**事件。 **RecordsetChangeComplete**事件會在**記錄集**變更之後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeRecordset adReason, adStatus, pRecordset  
RecordsetChangeComplete adReason, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *adReason*  
 [EventReasonEnum](../../../ado/reference/ado-api/eventreasonenum.md)值，指定這個事件的原因。 其值可以是 **adRsnRequery**、 **adRsnResynch**、 **adRsnClose**、 **adRsnOpen**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫 **WillChangeRecordset** 時，如果造成事件的作業成功，這個參數會設定為 **adStatusOK** 。 如果此事件無法要求取消暫止的作業，則會設定為 **adStatusCantDeny** 。  
  
 當呼叫**RecordsetChangeComplete**時，如果造成事件的作業成功，則會將此參數設定為**adStatusOK** ; 如果作業失敗，則會**adStatusErrorsOccurred** ，如果與先前接受的**WillChangeRecordset**事件相關聯的作業已取消，則為**adStatusCancel** 。  
  
 在 **WillChangeRecordset** 傳回之前，請將此參數設定為 **adStatusCancel** ，以要求取消暫止的作業，或將此參數設定為 adStatusUnwantedEvent 以防止後續的通知。  
  
 在 **WillChangeRecordset** 或 **RecordsetChangeComplete** 傳回之前，請將此參數設定為 **adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pError*  
 [Error](../../../ado/reference/ado-api/error-object.md)物件。 描述 *adStatus* 的值為 **adStatusErrorsOccurred**時所發生的錯誤;否則未設定。  
  
 *pRecordset*  
 **記錄集**物件。 發生此事件的 **記錄集** 。  
  
## <a name="remarks"></a>備註  
 **WillChangeRecordset**或**RecordsetChangeComplete**事件可能是因為**記錄集**的[Requery](../../../ado/reference/ado-api/requery-method.md)或[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法所造成。  
  
 如果提供者不支援書簽，每次從提供者取出新資料列時，就會發生 **RecordsetChange** 事件通知。 此事件的頻率取決於 **RecordsetCacheSize** 屬性。  
  
 您必須針對每個可能的**adReason**值，將**adStatus**參數設定為**adStatusUnwantedEvent** ，以完全停止任何包含**adReason**參數之事件的事件通知。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 (VC + +) ](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
