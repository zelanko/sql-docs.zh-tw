---
title: BOF、EOF 屬性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 9496a4e2115cb686764981e8a5fae3ecfe59401e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748738"
---
# <a name="bof-eof-properties-ado"></a>BOF、EOF 屬性 (ADO)
-   **BOF**指出目前的記錄位置是在[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的第一筆記錄之前。  
  
-   **EOF**指出目前的記錄位置是在記錄**集**物件中的最後一筆記錄之後。  
  
## <a name="return-value"></a>傳回值  
 **BOF**和**EOF**屬性會傳回**布林**值。  
  
## <a name="remarks"></a>備註  
 使用**BOF**和**EOF**屬性來判斷**記錄集**物件是否包含記錄，或當您從記錄移至記錄時，是否超出記錄**集**物件的限制。  
  
 如果目前的記錄位置位於第一筆記錄之前，則**BOF**屬性會傳回**True** （-1），如果目前的記錄位置是在第一筆記錄的前面或之後，則傳回**False** （0）。  
  
 如果目前的記錄位置在最後一筆記錄之後，則**EOF**屬性會傳回**True** ，如果目前的記錄位置在最後一筆記錄之前或之前，則傳回**False** 。  
  
 如果**BOF**或**EOF**屬性為**True**，則沒有目前的記錄。  
  
 如果您開啟不包含任何記錄的**記錄集**物件，則**BOF**和**EOF**屬性會設定為**True** （如需有關此**記錄集**狀態的詳細資訊，請參閱[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)屬性）。 當您開啟包含至少一筆記錄的記錄**集**物件時，第一筆記錄是目前的記錄，而**BOF**和**EOF**屬性則為**False**。  
  
 如果您刪除**記錄集**物件中的最後一筆記錄，則在您嘗試重新置放目前的記錄之前， **BOF**和**EOF**屬性可能會保持**為 False** 。  
  
 下表顯示可以使用不同的**BOF**和**EOF**屬性組合的**移動**方法。  
  
||MoveFirst<br /><br /> MoveLast|MovePrevious<br /><br /> 移動 < 0|移動0|MoveNext<br /><br /> 移動 > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF** =**True**、 **EOF** = **False**|允許|錯誤|錯誤|允許|  
|**BOF** =**False**、 **EOF** = **True**|允許|允許|錯誤|錯誤|  
|同時**為 True**|錯誤|錯誤|錯誤|錯誤|  
|兩者皆**為 False**|允許|允許|允許|允許|  
  
 允許**Move**方法並不保證方法會成功地找出記錄;這只表示呼叫指定的**Move**方法不會產生錯誤。  
  
 下表顯示當您呼叫各種**移動**方法但無法成功找出記錄時， **BOF**和**EOF**屬性設定會發生什麼情況。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**、 **MoveLast**|設定為**True**|設定為**True**|  
|**移動**0|沒有變更|沒有變更|  
|**MovePrevious**，**移動**< 0|設定為**True**|沒有變更|  
|**MoveNext**，**移動**> 0|沒有變更|設定為**True**|  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [BOF、EOF 和 Bookmark 屬性範例（VB）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、EOF 和 Bookmark 屬性範例（VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
