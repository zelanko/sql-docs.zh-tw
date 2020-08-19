---
description: EditMode 屬性
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e330e1bbe559940324962cfde772258d3345594b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444060"
---
# <a name="editmode-property"></a>EditMode 屬性
指出目前記錄的編輯狀態。  
  
## <a name="return-value"></a>傳回值  
 傳回 [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) 值。  
  
## <a name="remarks"></a>備註  
 ADO 會維護與目前記錄相關聯的編輯緩衝區。 這個屬性會指出是否已對此緩衝區進行變更，或是否已建立新的記錄。 您可以使用 **EditMode** 屬性來決定目前記錄的編輯狀態。 如果編輯程式已中斷，並判斷您是否需要使用 [Update](../../../ado/reference/ado-api/update-method.md) 或 [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 方法，您可以測試暫止的變更。  
  
 在*立即更新模式*中，呼叫**update**方法的成功呼叫之後， **EditMode**屬性會重設為**adEditNone** 。 當呼叫[delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)無法成功刪除資料來源中的記錄或記錄時 (例如，因為) 發生參考完整性違規，所以[記錄集會](../../../ado/reference/ado-api/recordset-object-ado.md)維持在編輯模式中 (**EditMode**  =  **adEditInProgress**) 。 因此，在將目前的記錄移出 (之前，必須先呼叫 **CancelUpdate** ，例如 [移動](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)或 [關閉](../../../ado/reference/ado-api/close-method-ado.md) ) 。  
  
 在 *批次更新模式* (中，提供者會快取多個變更，並將它們寫入基礎資料來源，只有當您呼叫 [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) 方法) 時， **EditMode** 屬性的值會在第一次作業執行時變更，而且不會透過呼叫 **update** 方法進行重設。 後續的作業不會變更 **EditMode** 屬性的值，即使執行不同的作業也是一樣。 例如，如果第一項作業是要加入新的記錄，而第二項作業會變更現有的記錄，則 **EditMode** 的屬性仍會 **adEditAdd**。 **EditMode**屬性在呼叫**UpdateBatch**之前，不會重設為**adEditNone** 。 若要判斷已執行哪些作業，請將 [ [篩選](../../../ado/reference/ado-api/filter-property.md) ] 屬性設定為 [ [adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) ]，如此就只會顯示具有暫止變更的記錄，並檢查每個記錄的 [ [狀態](../../../ado/reference/ado-api/status-property-ado-recordset.md) ] 屬性，以判斷已經對資料進行了哪些變更。  
  
> [!NOTE]
>  只有在目前有記錄時， **EditMode**才能傳回有效的值。 如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為 true，或目前的記錄已刪除，則**EditMode**會傳回錯誤。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、LockType 和 EditMode 屬性範例 (VB) ](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 屬性範例 (VC + +) ](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [ (ADO) 的 AddNew 方法 ](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [ (ADO 記錄集的 Delete 方法) ](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [ (ADO) 的 CancelUpdate 方法 ](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
