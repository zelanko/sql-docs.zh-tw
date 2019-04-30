---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11a39cf6f30e7a4892d6f2df5c8c373ab6847632
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63240329"
---
# <a name="status-property-ado-field"></a>Status 屬性 (ADO Field)
表示的狀態[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)值。 預設值是**adFieldOK**。  
  
## <a name="remarks"></a>備註  
  
## <a name="record-field-status"></a>記錄欄位狀態  
 變更的值**欄位**的欄位集合中的物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件會快取的物件直到[Update](../../../ado/reference/ado-api/update-method.md)呼叫方法。 此時，如果該欄位的值變更而造成錯誤，OLE DB 就會引發錯誤**DB_E_ERRORSOCCURRED** (2147749409)。 Status 屬性，其中任一**欄位**中的物件**欄位**造成錯誤的集合將包含的值從[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因此問題。  
  
 增強效能、 新增以及刪除[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)的集合**記錄**物件會快取直到**更新**呼叫方法時，然後所做的變更在批次的開放式更新中進行。 如果**更新**不會呼叫方法，不會更新伺服器。 如果任何更新失敗，則會傳回 OLE DB 提供者錯誤 (DB_E_ERRORSOCCURRED) 和**狀態**屬性會指出作業和錯誤狀態碼的結合的值。 例如， **adFieldPendingInsert OR adFieldPermissionDenied**。 **狀態**屬性分別**欄位**可用來判斷原因**欄位**已不新增、 修改或刪除。  
  
 許多類型的修改或刪除新增時，所遇到的問題**欄位**會報告透過**狀態**屬性。 例如，如果使用者刪除**欄位**，它已標示為要刪除**欄位**集合。 如果後續**更新**會傳回錯誤，因為使用者嘗試刪除**欄位**沒有權限，**欄位**會有**狀態**的**adFieldPermissionDenied OR adFieldPendingDelete**。 呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法還原原始值和集合**狀態**來**adFieldOK**。  
  
 同樣地，**更新**方法可能會傳回錯誤，因為新**欄位**已加入，並賦予不適當的值。 中的情況下的新**欄位**將處於**欄位**集合和狀態**adFieldPendingInsert**也可能**adFieldCantCreate**（視您的提供者）。 您可以提供適當的值的新**欄位**，並呼叫**更新**一次。  
  
## <a name="recordset-field-status"></a>資料錄集的欄位狀態  
 變更的值**欄位**的欄位集合中的物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)會快取的物件直到[Update](../../../ado/reference/ado-api/update-method.md)呼叫方法。 此時，如果該欄位的值變更而造成錯誤，OLE DB 就會引發錯誤**DB_E_ERRORSOCCURRED** (2147749409)。 Status 屬性，其中任一**欄位**中的物件**欄位**造成錯誤的集合將包含的值從[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因此問題。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [Status 屬性範例 (Field) (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [Status 屬性範例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
