---
title: MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 905fc532057a827f30735efe067464f488f51dc0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63242909"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)
移至 [first、 last、 下一步]，或上一個記錄中指定[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，會記錄目前的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>備註  
 使用**MoveFirst**方法，將目前的記錄位置移至中的第一個記錄**資料錄集**。  
  
 使用**MoveLast**方法來移動目前的記錄位置的最後一個記錄中**資料錄集**。 **資料錄集**物件必須支援書籤或回溯資料指標移動; 否則方法呼叫會產生錯誤。  
  
 呼叫**MoveFirst**或是**MoveLast**時**資料錄集**是空的 (兩者**BOF**並**EOF**為 True） 就會產生錯誤。  
  
 使用**MoveNext**方法來移動目前的記錄位置的一筆記錄正向 (底端**資料錄集**)。 如果最後一筆記錄是目前的記錄，而且您呼叫**MoveNext**方法，ADO 會設定目前的記錄位置中的最後一個記錄之後**Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，則為 true**)。 嘗試移動時，向前**EOF**屬性已 **，則為 True**會產生錯誤。  
  
 在 ADO 中 2.5 及更新版本，當**資料錄集**已經過篩選或排序，並變更目前的資料錄的資料時，呼叫**MoveNext**方法會移動資料指標兩個記錄轉送從目前的記錄. 這是因為目前的資料錄變更時下, 一筆記錄就會成為新的目前記錄。 呼叫**MoveNext**變更從新的目前記錄移動資料指標一筆記錄開始之後。 這是在 ADO 2.1 中行為不同及更早版本。 在這些較早的版本中，變更目前的記錄中的已排序或篩選的資料**Recordset**不會變更目前的記錄，位置和**MoveNext**游標移至下一筆記錄後面的目前的記錄。  
  
 使用**MovePrevious**方法來移動目前的記錄位置一筆記錄為了與舊版 (頂端**資料錄集**)。 **資料錄集**物件必須支援書籤或回溯資料指標移動; 否則方法呼叫會產生錯誤。 如果第一筆記錄是目前的記錄，而且您呼叫**MovePrevious**方法，ADO 會設定目前的記錄中的第一個記錄之前的位置**Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，則為 True**)。 嘗試移動時，為了與舊版**BOF**屬性已 **，則為 True**會產生錯誤。 如果**Recordset**物件不支援書籤或回溯資料指標移動**MovePrevious**方法會產生錯誤。  
  
 如果**Recordset**是順向，而且您想要支援向前及向後捲動，您可以使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性，以建立記錄快取將支援向後的資料指標移動透過[移動](../../../ado/reference/ado-api/move-method-ado.md)方法。 因為快取的記錄會載入到記憶體中，您應該避免快取更多超出所需的記錄。 您可以呼叫**MoveFirst**方法，在順向**資料錄集**物件，如此一來，可能會導致要重新執行的命令，產生的提供者**資料錄集**物件.  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法範例 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法範例 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法範例 （VC + +）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
