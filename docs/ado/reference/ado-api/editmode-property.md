---
title: "EditMode 屬性 |Microsoft 文件"
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
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be4670f359212f1079044341285ec2b0aff6c559
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="editmode-property"></a>EditMode 屬性
指出目前記錄的編輯狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值。  
  
## <a name="remarks"></a>備註  
 ADO 會維護目前記錄相關聯的編輯緩衝區。 此屬性會指出是否已變更到這個緩衝區中，或是否會建立新的記錄。 使用**EditMode**屬性來判斷目前記錄的編輯狀態。 您可以測試暫止的變更如果編輯程序已中斷，並判斷是否需要使用[更新](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
 在*立即更新模式* **EditMode**屬性重設為**adEditNone**之後在成功呼叫**更新**方法呼叫. 當呼叫[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)不會成功地刪除的資料來源中的記錄 （例如，因為參考完整性違規）[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)仍會留在編輯模式 (**EditMode** = **adEditInProgress**)。 因此， **CancelUpdate**移動目前的資料錄之前必須先呼叫 (例如[移動](../../../ado/reference/ado-api/move-method-ado.md)， [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[關閉](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 在*批次更新模式*(其中提供者會快取多個變更，並將它們寫入基礎資料來源，只有當您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，值**EditMode**屬性變更時第一項作業會執行，且它不會由呼叫重設**更新**方法。 後續的作業不會變更的值**EditMode**屬性，即使不同作業。 比方說，如果第一項作業是加入新的記錄，而第二個可進行變更的現有記錄、 屬性**EditMode**仍會**adEditAdd**。 **EditMode**屬性不會重設為**adEditNone**呼叫之後，才**UpdateBatch**。 若要判斷哪些作業已執行，請設定[篩選](../../../ado/reference/ado-api/filter-property.md)屬性[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md)以便僅記錄與暫止的變更將會顯示，並檢查[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性來判斷哪些變更已對資料的每一筆記錄。  
  
> [!NOTE]
>  **EditMode**可以傳回有效的值，只有當目前的記錄。 **EditMode**會傳回錯誤，如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為 true，或如果目前的記錄已被刪除。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、 LockType 和 EditMode 屬性範例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType 和 EditMode 屬性範例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 方法 （ADO 資料錄集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)

