---
description: CursorType 屬性 (ADO)
title: " (ADO) 的 CursorType 屬性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: rothja
ms.author: jroth
ms.openlocfilehash: a85bb0f624c5f5a3100bfba5d33d63a574fa9d0e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775497"
---
# <a name="cursortype-property-ado"></a>CursorType 屬性 (ADO)
指出 [記錄集](./recordset-object-ado.md) 物件中使用的資料指標類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 [CursorTypeEnum](./cursortypeenum.md) 值。 預設值為 **adOpenForwardOnly**。  
  
## <a name="remarks"></a>備註  
 您可以使用 **CursorType** 屬性來指定在開啟 **記錄集** 物件時，應該使用的資料指標類型。  
  
 如果[CursorLocation](./cursorlocation-property-ado.md)屬性設定為**adUseClient**，則只支援**adOpenStatic**的設定。 如果設定了不支援的值，則不會產生任何錯誤;將改用最接近的支援 **CursorType** 。  
  
 如果提供者不支援所要求的資料指標類型，則可能會傳回另一個資料指標類型。 當[記錄集](./recordset-object-ado.md)物件開啟時， **CursorType**屬性將會變更，以符合實際使用的資料指標類型。 若要確認所傳回之資料指標的特定功能，請使用 [支援](./supports-method.md) 方法。 當您關閉 **記錄集**之後， **CursorType** 屬性會還原為其原始設定。  
  
 下圖顯示 (所識別的提供者功能，可 **支援** 每個資料指標類型) 所需的方法常數。  
  
|針對此 CursorType 的記錄集|支援方法的所有常數都必須傳回 True|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|無|  
|**adOpenKeyset**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
  
> [!NOTE]
>  雖然 **支援** (**adUpdateBatch**) 適用于動態和順向資料指標，但是針對批次更新，您應該使用索引鍵集或靜態資料指標。 將 [LockType](./locktype-property-ado.md) 屬性設定為 **adLockBatchOptimistic** ，並將 **CursorLocation** 屬性設定為 **adUseClient** ，以針對批次更新所需的 OLE DB 啟用資料指標服務。  
  
 當**記錄集**已關閉時， **CursorType**屬性是讀取/寫入，而當記錄開啟時，則為唯讀屬性。  
  
> [!NOTE]
>  **遠端資料服務使用量** 在用戶端 **記錄集** 物件上使用時， **CursorType** 屬性只能設定為 **adOpenStatic**。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、LockType 和 EditMode 屬性範例 (VB) ](./cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 屬性範例 (VC + +) ](./cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 方法](./supports-method.md)