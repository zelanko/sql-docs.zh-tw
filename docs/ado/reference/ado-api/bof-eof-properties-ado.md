---
title: BOF、 EOF 屬性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 72954cb199976f05eacd7c79ba0e89cab0a45bbc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62821439"
---
# <a name="bof-eof-properties-ado"></a>BOF、EOF 屬性 (ADO)
-   **BOF**指出目前的記錄位置位於第一筆記錄之前[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
-   **EOF**指出目前的記錄位置位於最後一筆記錄，在之後**資料錄集**物件。  
  
## <a name="return-value"></a>傳回值  
 **BOF**並**EOF**屬性傳回**布林**值。  
  
## <a name="remarks"></a>備註  
 使用**BOF**並**EOF**屬性，以決定是否**資料錄集**物件包含記錄，或是您已經看超過限制的**資料錄集**物件時移動記錄記錄。  
  
 **BOF**屬性會傳回 **，則為 True** (-1) 如果目前的記錄位置是在第一個資料錄之前並**False**如果目前的記錄位置是在或之後的第一個 (0)資料錄。  
  
 **EOF**屬性會傳回 **，則為 True**如果目前的記錄位置位於最後一筆記錄之後， **False**如果目前的記錄位置是在或之前最後一筆記錄。  
  
 如果有任一**BOF**或**EOF**屬性**True**，沒有目前的記錄。  
  
 如果您開啟**資料錄集**物件，不包含任何記錄， **BOF**並**EOF**屬性設定為**True** (請參閱[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)如需此狀態的詳細資訊的屬性**資料錄集**)。 當您開啟**資料錄集**物件，其中包含至少一筆記錄，第一筆記錄是目前的記錄和**BOF**並**EOF**屬性**False**.  
  
 如果您刪除中的最後一個剩餘記錄**資料錄集**物件， **BOF**並**EOF**屬性可能會維持**False**直到您嘗試重新調整位置目前的記錄。  
  
 下表顯示哪些**移動**允許方法具有不同的組合**BOF**並**EOF**屬性。  
  
||MoveFirst、<br /><br /> MoveLast|MovePrevious，<br /><br /> 移動 < 0|移動 0|MoveNext，<br /><br /> 移動 > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**，則為 True**， **EOF**=**False**|Allowed|錯誤|錯誤|Allowed|  
|**BOF**=**False**， **EOF**=**，則為 True**|Allowed|Allowed|錯誤|錯誤|  
|兩者 **，則為 True**|錯誤|錯誤|錯誤|錯誤|  
|兩者**False**|Allowed|Allowed|Allowed|Allowed|  
  
 允許**移動**方法並不保證方法已成功將尋找一筆記錄; 它只表示指定該呼叫**移動**方法不會產生錯誤。  
  
 下表顯示會發生什麼事**BOF**並**EOF**屬性設定，當您呼叫各種**移動**方法但很難順利找出一筆記錄。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**， **MoveLast**|若要設定 **，則為 True**|若要設定 **，則為 True**|  
|**Move** 0|沒有變更|沒有變更|  
|**MovePrevious**，**移動**< 0|若要設定 **，則為 True**|沒有變更|  
|**MoveNext**，**移動**> 0|沒有變更|若要設定 **，則為 True**|  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、 EOF 和 Bookmark 屬性範例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和 Bookmark 屬性範例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
