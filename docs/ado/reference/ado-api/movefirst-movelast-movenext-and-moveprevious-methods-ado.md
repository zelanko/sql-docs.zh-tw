---
description: 'MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (ADO) '
title: " (ADO) 的 MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
author: rothja
ms.author: jroth
ms.openlocfilehash: dd050c775c706b3cafe2586eed05d93f9079fe27
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990549"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (ADO) 
移至指定 [記錄集](./recordset-object-ado.md) 物件中的第一個、最後一個、下一個或上一個記錄，並使其記錄目前的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>備註  
 您可以使用 **MoveFirst** 方法，將目前的記錄位置移至 **記錄集**內的第一筆記錄。  
  
 您可以使用 **MoveLast** 方法，將目前的記錄位置移至 **記錄集**內的最後一筆記錄。 **記錄集**物件必須支援書簽或後置資料指標移動;否則，方法呼叫將會產生錯誤。  
  
 當**記錄集**是空的時，呼叫**MoveFirst**或**MoveLast** (**BOF**和**EOF**都是 True) 會產生錯誤。  
  
 使用 **MoveNext** 方法可將目前的記錄位置向下一筆記錄移 (到 **記錄集**) 的底部。 如果最後一筆記錄是目前的記錄，而您呼叫 **MoveNext** 方法，則 ADO 會將目前的記錄設定為 **記錄集** 內最後一筆記錄之後的位置， ([EOF](./bof-eof-properties-ado.md) 是 **True**) 。 當 **EOF** 屬性已 **成立** 時，嘗試向前移動會產生錯誤。  
  
 在 ADO 2.5 和更新版本中，當 **記錄集** 已經過篩選或排序，且目前記錄的資料變更時，呼叫 **MoveNext** 方法會將資料指標從目前記錄向前移動兩筆記錄。 這是因為當目前的記錄變更時，下一筆記錄會成為新的目前記錄。 在變更之後呼叫 **MoveNext** ，會將資料指標從新的目前記錄向前移動一筆記錄。 這與 ADO 2.1 及更早版本中的行為不同。 在這些舊版中，在已排序或已篩選的 **記錄集中** 變更目前記錄的資料並不會變更目前記錄的位置，而 **MoveNext** 會在目前的記錄之後，立即將資料指標移到下一筆記錄。  
  
 您可以使用 **MovePrevious** 方法，將目前的記錄位置下移一筆記錄， (朝 **記錄集**) 的頂端。 **記錄集**物件必須支援書簽或後置資料指標移動;否則，方法呼叫將會產生錯誤。 如果第一個記錄是目前的記錄，而且您呼叫 **MovePrevious** 方法，則 ADO 會將目前的記錄設定為 **記錄集** 內第一筆記錄之前的位置 ([BOF](./bof-eof-properties-ado.md) 為 **True**) 。 當 **BOF** 屬性已 **為 True** 時，嘗試向後移動會產生錯誤。 如果 **記錄集** 物件不支援書簽或後置資料指標移動， **MovePrevious** 方法將會產生錯誤。  
  
 如果 **記錄集** 是順向的，而且您想要同時支援向前和向後滾動，則可以使用 [CacheSize](./cachesize-property-ado.md) 屬性來建立記錄快取，以支援透過 [Move](./move-method-ado.md) 方法進行的反向資料指標移動。 由於快取記錄會載入至記憶體中，因此，您應該避免快取比所需更多的記錄。 您可以在順向**記錄集**物件中呼叫**MoveFirst**方法;這樣做可能會導致提供者重新執行產生**記錄集**物件的命令。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法範例 (VB) ](./movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法範例 (VBScript) ](./movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法範例 (VC + +) ](./movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [ (ADO) 的 Move 方法 ](./move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS) ](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](./moverecord-method-ado.md)