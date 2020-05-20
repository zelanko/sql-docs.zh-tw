---
title: WillChangeField 和 FieldChangeComplete 事件（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldChangeComplete
- Recordset::WillChangeField
- Recordset::FieldChangeComplete
- WillChangeField
helpviewer_keywords:
- WillChangeField event [ADO]
- fieldchangecomplete event [ADO]
ms.assetid: 3e49fb89-c45b-4d39-823e-3cc887c59b37
author: rothja
ms.author: jroth
ms.openlocfilehash: e4a4fb74e95bf0e1ba9dc9d0001b3d653f9294c1
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764489"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 和 FieldChangeComplete 事件 (ADO)
在暫止的作業變更[記錄集中](../../../ado/reference/ado-api/recordset-object-ado.md)一個或多個[欄位](../../../ado/reference/ado-api/field-object.md)物件的值之前，會呼叫**WillChangeField**事件。 **FieldChangeComplete**事件會在一或多個**欄位**物件的值變更後呼叫。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *cFields*  
 **Long** ，表示*欄位*中的**欄位**物件數目。  
  
 *欄位*  
 針對**WillChangeField**， *Fields*參數是**variant**的陣列，其中包含具有原始值的**欄位**物件。 針對**FieldChangeComplete**， *Fields*參數是**variant**的陣列，其中包含具有已變更值的**欄位**物件。  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它會描述*adStatus*的值為**adStatusErrorsOccurred**時所發生的錯誤。否則不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當呼叫**WillChangeField**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** 。 如果此事件無法要求取消暫止的作業，則會設定為**adStatusCantDeny** 。  
  
 當呼叫**FieldChangeComplete**時，如果造成事件的作業成功，此參數會設定為**adStatusOK** ，如果作業失敗，則設為**adStatusErrorsOccurred** 。  
  
 在**WillChangeField**傳回之前，請將此參數設定為**adStatusCancel** ，以要求取消暫止的作業。  
  
 在**FieldChangeComplete**傳回之前，請將此參數設定為**adStatusUnwantedEvent** ，以防止後續的通知。  
  
 *pRecordset*  
 **記錄集**物件。 發生此事件的**記錄集**。  
  
## <a name="remarks"></a>備註  
 設定[Value](../../../ado/reference/ado-api/value-property-ado.md)屬性並使用欄位和值陣列參數呼叫[Update](../../../ado/reference/ado-api/update-method.md)方法時，可能會發生**WillChangeField**或**FieldChangeComplete**事件。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
