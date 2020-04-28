---
title: Status 屬性（ADO Field） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d90eff53ef998a009aecd4d82fc3b502a487c01d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67930839"
---
# <a name="status-property-ado-field"></a>Status 屬性 (ADO Field)
指出[欄位](../../../ado/reference/ado-api/field-object.md)物件的狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)值。 預設值為**adFieldOK**。  
  
## <a name="remarks"></a>備註  
  
## <a name="record-field-status"></a>記錄欄位狀態  
 在[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件的 Fields 集合中，**欄位**物件值的變更會被快取，直到呼叫物件的[Update](../../../ado/reference/ado-api/update-method.md)方法為止。 此時，如果對欄位的值所做的變更造成錯誤，OLE DB 會引發錯誤**DB_E_ERRORSOCCURRED** （2147749409）。 造成錯誤之**Fields**集合中任何**欄位**物件的 Status 屬性會包含[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)的值，描述問題的原因。  
  
 為了增強效能，會快取**記錄**物件之[Fields](../../../ado/reference/ado-api/fields-collection-ado.md)集合的新增和刪除，直到呼叫**Update**方法為止，然後在批次開放式更新中進行變更。 如果未呼叫**Update**方法，伺服器就不會更新。 如果有任何更新失敗，則會傳回 OLE DB 提供者錯誤（DB_E_ERRORSOCCURRED），而**Status**屬性會指出作業和錯誤狀態碼的結合值。 例如， **ADFIELDPENDINGINSERT 或 adFieldPermissionDenied**。 每個**欄位**的**Status**屬性可以用來判斷**欄位**未新增、修改或刪除的原因。  
  
 新增、修改或刪除**欄位**時所遇到的許多類型問題，都是透過**Status**屬性來回報。 例如，如果使用者刪除**欄位**，則會將它標示為從**Fields**集合中刪除。 如果後續的**更新**傳回錯誤，因為使用者嘗試刪除其沒有許可權的**欄位**，則此**欄位**的**狀態**會是**adFieldPermissionDenied 或 adFieldPendingDelete**。 呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法會還原原始值，並將**狀態**設定為**adFieldOK**。  
  
 同樣地， **Update**方法可能會傳回錯誤，因為已加入新的**欄位**，並提供了不適當的值。 在此情況下，新**欄位**會在**Fields**集合中，且狀態為**adFieldPendingInsert** ，可能是**adFieldCantCreate** （視您的提供者而定）。 您可以為新**欄位**提供適當的值，然後再次呼叫**Update** 。  
  
## <a name="recordset-field-status"></a>記錄集欄位狀態  
 對[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)之 Fields 集合中的**欄位**物件值所做的變更，會在呼叫物件的[Update](../../../ado/reference/ado-api/update-method.md)方法之前進行快取。 此時，如果對欄位的值所做的變更造成錯誤，OLE DB 會引發錯誤**DB_E_ERRORSOCCURRED** （2147749409）。 造成錯誤之**Fields**集合中任何**欄位**物件的 Status 屬性會包含[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)的值，描述問題的原因。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Status 屬性範例（Field）（VB）](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status 屬性範例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
