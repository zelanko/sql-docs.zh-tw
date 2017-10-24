---
title: "Status 屬性 （ADO 欄位） |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Field::Status
- Field::get_Status
- Field::GetStatus
helpviewer_keywords:
- Status property [ADO Field]
ms.assetid: 8cd1f7f4-0a3a-4f07-b8ba-6582e70140ad
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65acf492f0364b26fa6a12240fbbd49c7d1dfed3
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="status-property-ado-field"></a>Status 屬性 （ADO 欄位）
表示狀態[欄位](../../../ado/reference/ado-api/field-object.md)物件。  
  
## <a name="return-value"></a>傳回值  
 傳回[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)值。 預設值是**adFieldOK**。  
  
## <a name="remarks"></a>備註  
  
## <a name="record-field-status"></a>記錄欄位狀態  
 變更的值為**欄位**的欄位集合中物件[記錄](../../../ado/reference/ado-api/record-object-ado.md)物件會快取的物件直到[更新](../../../ado/reference/ado-api/update-method.md)方法呼叫。 此時，如果欄位值的變更會造成錯誤，OLE DB 會引發錯誤**DB_E_ERRORSOCCURRED** (2147749409)。 任何的 Status 屬性**欄位**中的物件**欄位**造成錯誤的集合會包含值，以從[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因此問題。  
  
 若要增強效能、 新增和刪除[欄位](../../../ado/reference/ado-api/fields-collection-ado.md)的集合**記錄**直到快取物件**更新**呼叫方法時，，然後變更在批次開放式更新中進行。 如果**更新**不會呼叫方法，不會更新伺服器。 如果任何更新失敗，則會傳回 OLE DB 提供者錯誤 (DB_E_ERRORSOCCURRED) 和**狀態**屬性指示的作業和錯誤狀態碼的結合的值。 例如， **adFieldPendingInsert OR adFieldPermissionDenied**。 **狀態**每個屬性**欄位**可用來判斷原因**欄位**已不新增、 修改或刪除。  
  
 許多類型的修改或刪除加入時，所遇到的問題**欄位**會報告透過**狀態**屬性。 例如，如果使用者刪除**欄位**，它已標示為刪除**欄位**集合。 如果後續**更新**傳回錯誤，因為使用者嘗試刪除**欄位**沒有權限，**欄位**必須**狀態**的**adFieldPermissionDenied OR adFieldPendingDelete**。 呼叫[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法還原原始值和集合**狀態**至**adFieldOK**。  
  
 同樣地，**更新**方法可能會傳回錯誤，因為新**欄位**已加入，且提供不適當的值。 在的情況下，新**欄位**將處於**欄位**集合並且狀態為**adFieldPendingInsert**也可能**adFieldCantCreate**（視您的提供者）。 您可以提供適當的值，新的**欄位**呼叫**更新**一次。  
  
## <a name="recordset-field-status"></a>資料錄集欄位狀態  
 變更的值為**欄位**任一個的欄位集合中物件[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)會快取的物件直到[更新](../../../ado/reference/ado-api/update-method.md)方法呼叫。 此時，如果欄位值的變更會造成錯誤，OLE DB 會引發錯誤**DB_E_ERRORSOCCURRED** (2147749409)。 任何的 Status 屬性**欄位**中的物件**欄位**造成錯誤的集合會包含值，以從[FieldStatusEnum](../../../ado/reference/ado-api/fieldstatusenum.md)描述的原因此問題。  
  
## <a name="applies-to"></a>適用於  
 [Field 物件](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>另請參閱  
 [狀態屬性範例 （欄位） (VB)](../../../ado/reference/ado-api/status-property-example-field-vb.md)   
 [狀態屬性範例 （VC + +）](../../../ado/reference/ado-api/status-property-example-vc.md)   

