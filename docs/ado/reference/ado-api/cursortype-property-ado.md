---
title: "CursorType 屬性 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::CursorType
helpviewer_keywords: CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f1f16755e5030cec19d7b513f725f3fd5defb3f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="cursortype-property-ado"></a>CursorType 屬性 (ADO)
表示使用中的資料指標類型[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值。 預設值是**adOpenForwardOnly**。  
  
## <a name="remarks"></a>備註  
 使用**CursorType**屬性來指定資料指標開啟時，應使用的型別**資料錄集**物件。  
  
 只有設定為**adOpenStatic**如果，則支援[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)屬性設定為**adUseClient**。 如果設定不支援的值，則不會產生錯誤。支援的最接近**CursorType**將改為使用。  
  
 如果提供者不支援要求的資料指標類型，它可能會傳回另一個資料指標類型。 **CursorType**屬性會變更以符合實際的資料指標類型的使用時機[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件是否開啟。 若要確認傳回的資料指標的特定功能，請使用[支援](../../../ado/reference/ado-api/supports-method.md)方法。 在您關閉之後**資料錄集**、 **CursorType**屬性會還原為其原始設定。  
  
 下圖顯示提供者功能 (由**支援**方法常數) 所需的每個資料指標類型。  
  
|資料錄集的這個 CursorType|支援方法必須為 true，則傳回所有這些常數|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|無|  
|**adOpenKeyset**|**adBookmark**， **adHoldRecords**， **adMovePrevious**， **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**， **adHoldRecords**， **adMovePrevious**， **adResync**|  
  
> [!NOTE]
>  雖然**支援**(**adUpdateBatch**) 可能是動態且順向資料指標，則為 true 批次更新，您應該使用索引鍵集或靜態資料指標。 設定[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)屬性**Adlockpessimistic**和**CursorLocation**屬性**adUseClient**以啟用資料指標OLE DB 中，所需的批次更新服務。  
  
 **CursorType**屬性是讀取/寫入時**資料錄集**開啟時，已關閉，且為唯讀。  
  
> [!NOTE]
>  **遠端資料服務使用量**使用用戶端時**資料錄集**物件**CursorType**屬性可以設為**adOpenStatic**。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱＜  
 [CursorType、 LockType 和 EditMode 屬性範例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType 和 EditMode 屬性範例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
