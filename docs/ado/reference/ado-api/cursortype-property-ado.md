---
title: CursorType 屬性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 5bf0790307ec8f8f739d3975620967a8671c3fcb
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763499"
---
# <a name="cursortype-property-ado"></a>CursorType 屬性 (ADO)
表示[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中使用的資料指標類型。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值。 預設值為**adOpenForwardOnly**。  
  
## <a name="remarks"></a>備註  
 使用**CursorType**屬性來指定開啟**記錄集**物件時應使用的資料指標類型。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**，則只支援**adOpenStatic**的設定。 如果設定了不支援的值，則不會產生任何錯誤。將改用最接近的支援**CursorType** 。  
  
 如果提供者不支援要求的資料指標類型，它可能會傳回另一個資料指標類型。 當[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件開啟時， **CursorType**屬性將會變更，以符合實際使用的資料指標類型。 若要確認所傳回資料指標的特定功能，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法。 關閉**記錄集**之後， **CursorType**屬性會還原為其原始設定。  
  
 下圖顯示每個資料指標類型所需的提供者功能（由**支援**的方法常數所識別）。  
  
|適用于此 CursorType 的記錄集|支援方法的所有常數都必須傳回 True|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|無|  
|**adOpenKeyset**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
  
> [!NOTE]
>  雖然針對動態和順向資料指標的**支援**（**adUpdateBatch**）可能是 true，但對於批次更新，您應該使用索引鍵集或靜態資料指標。 將[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)屬性設為**adLockBatchOptimistic** ，並將**CursorLocation**屬性設定為**adUseClient** ，以針對批次更新所需的 OLE DB 啟用資料指標服務。  
  
 當**記錄集**關閉時， **CursorType**屬性是讀取/寫入，而當它開啟時則為唯讀。  
  
> [!NOTE]
>  **遠端資料服務使用量**在用戶端**記錄集**物件上使用時， **CursorType**屬性只能設定為**adOpenStatic**。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CursorType、LockType 和 EditMode 屬性範例（VB）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 屬性範例（VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
