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
ms.openlocfilehash: c0ffc6fb258799b0ab0bb03e7acbd922f6a67d1f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918987"
---
# <a name="editmode-property"></a>EditMode 屬性
指出目前記錄的編輯狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值。  
  
## <a name="remarks"></a>備註  
 ADO 會維護與目前記錄相關聯的編輯緩衝區。 這個屬性會指出是否已對此緩衝區進行變更，或是否已建立新的記錄。 使用**EditMode**屬性來判斷目前記錄的編輯狀態。 如果編輯進程已中斷，您可以測試暫止的變更，並判斷您是否需要使用[Update](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
 在*立即更新模式*中，呼叫**update**方法的成功呼叫之後， **EditMode**屬性會重設為**adEditNone** 。 當呼叫[delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)無法成功刪除資料來源中的記錄或記錄時（例如，因為參考完整性違規），[記錄集會](../../../ado/reference/ado-api/recordset-object-ado.md)維持在編輯模式中（**EditMode** = **adEditInProgress**）。 因此，您必須先呼叫**CancelUpdate** ，然後才能移出目前的記錄（例如，with [Move](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)或[Close](../../../ado/reference/ado-api/close-method-ado.md) ）。  
  
 在*批次更新模式*中（提供者會快取多個變更，並只在您呼叫[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法時將它們寫入基礎資料來源），當第一次作業執行時， **EditMode**屬性的值會變更，而且不會由**update**方法的呼叫重設。 即使執行不同的作業，後續作業也不會變更**EditMode**屬性的值。 例如，如果第一個作業是加入新的記錄，而第二個作業變更了現有的記錄，則**EditMode**的屬性仍會是**adEditAdd**。 在呼叫**UpdateBatch**之後，才會將**EditMode**屬性重設為**adEditNone** 。 若要判斷已執行的作業，請將[Filter](../../../ado/reference/ado-api/filter-property.md)屬性設定為[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) ，如此一來，就只會顯示具有暫止變更的記錄，並檢查每一筆記錄的[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)屬性，以判斷資料已做了哪些變更。  
  
> [!NOTE]
>  只有在目前的記錄時， **EditMode**才會傳回有效的值。 如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為 true，或目前的記錄已刪除，則**EditMode**會傳回錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、LockType 和 EditMode 屬性範例（VB）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 屬性範例（VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 方法（ADO）](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 方法（ADO Recordset）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
