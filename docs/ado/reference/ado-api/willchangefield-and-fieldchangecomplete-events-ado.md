---
title: WillChangeField 和 FieldChangeComplete 事件 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f046a3a33e05228ab5e49116bc46eb9451f43129
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673656"
---
# <a name="willchangefield-and-fieldchangecomplete-events-ado"></a>WillChangeField 和 FieldChangeComplete 事件 (ADO)
**WillChangeField**暫止的作業變更一個或多個值之前，會呼叫事件[欄位](../../../ado/reference/ado-api/field-object.md)中的物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)。 **FieldChangeComplete**事件會被呼叫一或多個值後面**欄位**物件已變更。  
  
## <a name="syntax"></a>語法  
  
```  
  
WillChangeField cFields, Fields, adStatus, pRecordset  
FieldChangeComplete cFields, Fields, pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>參數  
 *cFields*  
 A**長**表示數目**欄位**中的物件*欄位*。  
  
 *欄位*  
 針對**WillChangeField**，則*欄位*參數是陣列**變體**，其中包含**欄位**與原始值的物件。 針對**FieldChangeComplete**，則*欄位*參數是陣列**變體**包含**欄位**值已變更的物件.  
  
 *pError*  
 [錯誤](../../../ado/reference/ado-api/error-object.md)物件。 它說明如果發生錯誤的值*adStatus*是**adStatusErrorsOccurred**; 否則它不會設定。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)狀態值。  
  
 當**WillChangeField**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成。 它會設定為**adStatusCantDeny**如果此事件不能要求取消暫止的作業。  
  
 當**FieldChangeComplete**是呼叫，此參數設為**adStatusOK**如果造成事件的作業已順利完成，或**adStatusErrorsOccurred**如果作業失敗。  
  
 再**WillChangeField**傳回，這個參數設定為**adStatusCancel**要求取消的暫止的作業。  
  
 再**FieldChangeComplete**傳回，這個參數設定為**adStatusUnwantedEvent**以避免後續的通知。  
  
 *pRecordset*  
 A**資料錄集**物件。 **資料錄集**如發生此事件。  
  
## <a name="remarks"></a>備註  
 A **WillChangeField**或是**FieldChangeComplete**設定時，可能會發生事件[值](../../../ado/reference/ado-api/value-property-ado.md)屬性，並呼叫[更新](../../../ado/reference/ado-api/update-method.md)方法欄位和值的陣列參數。  
  
## <a name="see-also"></a>另請參閱  
 [ADO 事件模型範例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件處理常式摘要](../../../ado/guide/data/ado-event-handler-summary.md)
