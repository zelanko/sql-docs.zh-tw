---
title: EditMode 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 2988d031e523c5199bed6c4a557078c803e7bd6b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/05/2019
ms.locfileid: "66698313"
---
# <a name="editmode-property"></a>EditMode 屬性
指出目前記錄的編輯狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值。  
  
## <a name="remarks"></a>備註  
 ADO 會維護一個編輯與目前記錄相關聯的緩衝區。 這個屬性會指出是否已變更此緩衝區中，或是否會建立新的記錄。 使用**EditMode**屬性來判斷目前的資料錄的編輯狀態。 您可以測試暫止的變更如果編輯程序已中斷，並判斷是否需要使用[更新](../../../ado/reference/ado-api/update-method.md)或是[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
 在 *立即更新模式* **EditMode**屬性重設為**adEditNone**之後成功呼叫**更新**方法稱為. 當呼叫[刪除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)不會成功地刪除的資料來源中的記錄 （例如，因為參考完整性違規），[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)仍會保留在編輯模式 (**EditMode** = **adEditInProgress**)。 因此， **CancelUpdate**必須先呼叫才能移出目前的記錄 (例如[移動](../../../ado/reference/ado-api/move-method-ado.md)， [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[關閉](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 在 *批次更新模式*(提供者會快取的多項變更並將其寫入至基礎資料來源，只有當您呼叫時，才[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，值**EditMode**屬性變更時第一項作業會執行，且它不會藉由呼叫重設**更新**方法。 後續的作業不會變更的值**EditMode**屬性，即使不同作業。 例如，如果第一項作業是加入新的記錄，而第二個會進行變更的現有記錄，屬性**EditMode**仍會**adEditAdd**。 **EditMode**屬性不會重設為**adEditNone**直到呼叫**UpdateBatch**。 若要判斷已執行哪些作業，請設定[篩選條件](../../../ado/reference/ado-api/filter-property.md)屬性設[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md)以便只記錄暫止的變更將會顯示，並檢查[狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性來判斷哪些變更已對資料的每一筆記錄。  
  
> [!NOTE]
>  **EditMode**可以傳回有效的值，只有當目前的記錄。 **EditMode**會傳回錯誤，如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為 true，或如果已刪除目前的記錄。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、 LockType、 和 EditMode 屬性範例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType、 和 EditMode 屬性範例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 方法 (ADO Recordset)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
