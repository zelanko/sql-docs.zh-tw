---
title: MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 4acdf777429e879ed22b99ea5a0f07775bc3798c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764499"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法（ADO）
移至指定之[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中的第一個、最後一個、下一個或上一個記錄，並將該記錄設為目前的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>備註  
 使用**MoveFirst**方法，將目前的記錄位置移至**記錄集**內的第一筆記錄。  
  
 使用**MoveLast**方法，將目前的記錄位置移至**記錄集**內的最後一筆記錄。 **記錄集**物件必須支援書簽或回溯游標移動;否則，方法呼叫會產生錯誤。  
  
 當**記錄集**是空的（ **BOF**和**EOF**皆為 True）時，呼叫**MoveFirst**或**MoveLast**時，會產生錯誤。  
  
 使用**MoveNext**方法，將目前的記錄位置向前移動一筆記錄（朝**記錄集**的底部）。 如果最後一筆記錄是目前的記錄，而您呼叫**MoveNext**方法，ADO 會將目前的記錄設定為**記錄集**內最後一筆記錄之後的位置（[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為**True**）。 當**EOF**屬性已經是**True**時，嘗試繼續進行，會產生錯誤。  
  
 在 ADO 2.5 和更新版本中，當**記錄集**已篩選或排序，而且目前記錄的資料已變更時，呼叫**MoveNext**方法會將游標從目前記錄中向前移動兩筆記錄。 這是因為當目前的記錄變更時，下一筆記錄會變成新的目前記錄。 在變更之後呼叫**MoveNext** ，會將游標從新的目前記錄中向前移動一筆記錄。 這與 ADO 2.1 和更早版本中的行為不同。 在舊版中，變更已排序或已篩選之**記錄集中**目前記錄的資料，並不會變更目前記錄的位置，而**MoveNext**會將游標移至目前記錄之後的下一個記錄。  
  
 使用**MovePrevious**方法，將目前的記錄位置向後移動一筆記錄（朝向**記錄集**的頂端）。 **記錄集**物件必須支援書簽或回溯游標移動;否則，方法呼叫會產生錯誤。 如果第一筆記錄是目前的記錄，而且您呼叫**MovePrevious**方法，ADO 會將目前的記錄設定為**記錄集**內第一筆記錄之前的位置（[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為**True**）。 當**BOF**屬性已經**為 True**時，嘗試向後移動會產生錯誤。 如果**記錄集**物件不支援書簽或回溯資料指標移動， **MovePrevious**方法將會產生錯誤。  
  
 如果**記錄集**只有轉送，而您想要同時支援向前和向後滾動，您可以使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性來建立記錄快取，以支援透過[Move](../../../ado/reference/ado-api/move-method-ado.md)方法的回溯游標移動。 因為快取的記錄會載入記憶體中，所以您應該避免快取超過所需的記錄。 您可以在順向**記錄集**物件中呼叫**MoveFirst**方法;這麼做可能會導致提供者重新執行產生**記錄集**物件的命令。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法範例（VB）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法範例（VBScript）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法範例（VC + +）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 方法（ADO）](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法（RDS）](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
