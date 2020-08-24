---
description: Status 屬性 (ADO Field)
title: Status 屬性 (ADO Field) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 70b77c60d2a2ac77a2d36a4ce29d2e20187495f9
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777317"
---
# <a name="status-property-ado-field"></a>Status 屬性 (ADO Field)
表示 [欄位](./field-object.md) 物件的狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回 [FieldStatusEnum](./fieldstatusenum.md) 值。 預設值為 **adFieldOK**。  
  
## <a name="remarks"></a>備註  
  
## <a name="record-field-status"></a>記錄欄位狀態  
 在[記錄](./record-object-ado.md)物件的 Fields 集合中，**欄位**物件值的變更會被快取，直到呼叫物件的[Update](./update-method.md)方法為止。 屆時，如果欄位的值變更造成錯誤，OLE DB **DB_E_ERRORSOCCURRED** (2147749409) 時引發錯誤。 在**欄位**集合中造成錯誤的任何**欄位**物件的 Status 屬性，將會包含描述問題原因的[FieldStatusEnum](./fieldstatusenum.md)值。  
  
 為了增強效能，會快取**記錄**物件之[Fields](./fields-collection-ado.md)集合的新增和刪除，直到呼叫**Update**方法為止，然後在 batch 開放式更新中進行變更。 如果未呼叫 **Update** 方法，則不會補救伺服器。 如果有任何更新失敗，則會傳回 OLE DB 提供者錯誤 (DB_E_ERRORSOCCURRED) ，且 **Status** 屬性會指出作業的組合值和錯誤狀態碼。 例如， **ADFIELDPENDINGINSERT 或 adFieldPermissionDenied**。 您可以使用每個**欄位**的**Status**屬性來判斷為何未加入、修改或刪除**欄位**。  
  
 新增、修改或刪除 **欄位** 時遇到的許多類型問題都會透過 **Status** 屬性回報。 例如，如果使用者刪除 **欄位**，則會將它標示為從 **Fields** 集合中刪除。 如果後續 **更新** 因為使用者嘗試刪除沒有許可權的 **欄位** 而傳回錯誤，此 **欄位** 的 **狀態** 將會是 **adFieldPermissionDenied 或 adFieldPendingDelete**。 呼叫 [CancelUpdate](./cancelupdate-method-ado.md) 方法會還原原始值，並將 **狀態** 設定為 **adFieldOK**。  
  
 同樣地， **Update** 方法可能會傳回錯誤，因為新的 **欄位** 已加入並有不適當的值。 在這種情況下，新 **欄位** 會在 **Fields** 集合中，而且會有 **adFieldPendingInsert** 的狀態，而且可能會根據您的提供者) 來 (**adFieldCantCreate** 。 您可以為新 **欄位** 提供適當的值，然後再次呼叫 **Update** 。  
  
## <a name="recordset-field-status"></a>記錄集欄位狀態  
 在[記錄集](./recordset-object-ado.md)的 Fields 集合中，**欄位**物件值的變更會被快取，直到呼叫物件的[Update](./update-method.md)方法為止。 屆時，如果欄位的值變更造成錯誤，OLE DB **DB_E_ERRORSOCCURRED** (2147749409) 時引發錯誤。 在**欄位**集合中造成錯誤的任何**欄位**物件的 Status 屬性，將會包含描述問題原因的[FieldStatusEnum](./fieldstatusenum.md)值。  
  
## <a name="applies-to"></a>套用至  
 [Field 物件](./field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Status 屬性範例 (欄位)  (VB) ](./status-property-example-field-vb.md)   
 [Status 屬性範例 (VC++)](./status-property-example-vc.md)