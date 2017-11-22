---
title: "WillChangeField 和 FieldChangeComplete 事件 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d532aa3857e2a61bb5ec23fa9258f6d7aa1186f2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 和 FieldChangeComplete 事件 (ADO)
**WillChangeField**事件被呼叫之前暫止的作業變更的一或多個值[欄位](../../../ado/reference/ado-api/field-object.md)中的物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **FieldChangeComplete**事件之後的一或多個值，就會呼叫**欄位**物件已變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *cFields*  
 A**長**表示的數**欄位**中的物件*欄位*。  
  
 *欄位*  
 如**WillChangeField**、*欄位*參數為陣列**變異**包含**欄位**與原始值的物件。 如**FieldChangeComplete**、*欄位*參數為陣列**變異**包含**欄位**值已變更的物件.  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它描述如果發生之錯誤的值*adStatus*是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**WillChangeField**是呼叫，此參數設為**adStatusOK**如果造成事件的作業是否成功。 設定為**adStatusCantDeny**如果此事件不可以要求取消的暫止的作業。  
  
 當**FieldChangeComplete**是呼叫，此參數設為**adStatusOK**如果造成事件的作業成功，或**adStatusErrorsOccurred**如果作業失敗。  
  
 之前**WillChangeField**傳回時，會將此參數設定為**adStatusCancel**要求取消的暫止的作業。  
  
 之前**FieldChangeComplete**傳回時，會將此參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 A **WillChangeField**或**FieldChangeComplete**設定時，可能會發生事件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性，並呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法使用欄位和值的陣列參數。  
  
## <a name="see-also"></a>請參閱＜  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
