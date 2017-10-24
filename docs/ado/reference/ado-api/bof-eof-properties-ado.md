---
title: "BOF，EOF 屬性 (ADO) |Microsoft 文件"
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
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93689aa347014fd3976645682a396230a38476e6
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="bof-eof-properties-ado"></a>BOF，EOF 屬性 (ADO)
-   **BOF**表示目前的記錄位置是在第一筆記錄之前[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
-   **EOF**表示目前的記錄位置是在最後一筆記錄之後**資料錄集**物件。  
  
## <a name="return-value"></a>傳回值  
 **BOF**和**EOF**屬性傳回**布林**值。  
  
## <a name="remarks"></a>備註  
 使用**BOF**和**EOF**屬性，以決定是否**資料錄集**物件包含的記錄，或是否您已經超出限制的**資料錄集**物件時移動記錄記錄。  
  
 **BOF**屬性會傳回**True** (-1) 如果目前的記錄位置是在第一個資料錄之前和**False** (0)，表示目前的記錄位置或之後的第一個資料錄。  
  
 **EOF**屬性會傳回**True**如果目前的記錄位置是在最後一筆記錄之後和**False**如果目前的記錄位置是在或之前最後一筆記錄。  
  
 如果有任一個**BOF**或**EOF**屬性是**True**，沒有目前的記錄。  
  
 如果您開啟**資料錄集**物件，其中包含任何記錄， **BOF**和**EOF**屬性會設為**True** (請參閱[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)屬性，如需有關此狀態的**資料錄集**)。 當您開啟**資料錄集**包含至少一筆記錄，第一筆記錄的物件是目前的記錄和**BOF**和**EOF**屬性**False**.  
  
 如果您刪除中的最後一個剩餘記錄**資料錄集**物件**BOF**和**EOF**屬性可能會維持**False**直到您嘗試重新調整位置目前的記錄。  
  
 下表顯示哪些**移動**方法允許不同的組合用於**BOF**和**EOF**屬性。  
  
||MoveFirst，<br /><br /> MoveLast|MovePrevious，<br /><br /> 移動 < 0|移動 0|MoveNext，<br /><br /> 移動 > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**， **EOF**=**False**|Allowed|錯誤|錯誤|Allowed|  
|**BOF**=**False**， **EOF**=**，則為 True**|Allowed|Allowed|錯誤|錯誤|  
|同時**，則為 True**|錯誤|錯誤|錯誤|錯誤|  
|同時**False**|Allowed|Allowed|Allowed|Allowed|  
  
 允許**移動**方法不保證方法將會成功找到某筆記錄; 它僅表示呼叫指定**移動**方法不會產生錯誤。  
  
 下表顯示發生什麼事**BOF**和**EOF**屬性設定，當您呼叫各種**移動**方法但這是成功找不到記錄。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**， **MoveLast**|設定為**，則為 True**|設定為**，則為 True**|  
|**移動**0|沒有變更|沒有變更|  
|**MovePrevious**，**移動**< 0|設定為**，則為 True**|沒有變更|  
|**MoveNext**，**移動**> 0|沒有變更|設定為**，則為 True**|  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、 EOF 和書籤屬性範例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和書籤屬性範例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   

