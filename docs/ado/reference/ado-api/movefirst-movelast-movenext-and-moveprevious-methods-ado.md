---
title: "MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6cbef486ed01dd49e13ba1ca88d197576dc98570
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)
移至 [first、 last、 在指定的下一步]，或上一個記錄[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件，會記錄目前的記錄。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>備註  
 使用**MoveFirst**方法來移動目前的記錄位置中的第一個記錄**資料錄集**。  
  
 使用**MoveLast**方法，將目前的記錄位置移到最後一個記錄中**資料錄集**。 **資料錄集**物件必須支援書籤或回溯資料指標移動; 否則方法呼叫會產生錯誤。  
  
 呼叫**MoveFirst**或**MoveLast**時**資料錄集**是空的 (兩者**BOF**和**EOF**為 True） 會產生錯誤。  
  
 使用**MoveNext**向前方法來移動目前的記錄位置的一筆記錄 (底部**資料錄集**)。 如果最後一筆記錄是目前的記錄，而且您呼叫**MoveNext**方法，ADO 集的目前記錄的位置中的最後一筆記錄之後**資料錄集**([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**True**)。 嘗試移動時，正向**EOF**內容已出現**True**會產生錯誤。  
  
 在 ADO 中 2.5 和更新版本時**資料錄集**已經過篩選或排序和變更的目前記錄資料時，呼叫**MoveNext**方法會移動資料指標兩個記錄將從目前的記錄. 這是因為目前的記錄變更時下, 一筆記錄就會成為新的目前記錄。 呼叫**MoveNext**變更移與新的目前記錄資料指標一筆記錄向前復原。 這是在 ADO 2.1 中行為不同及更早版本。 在這些舊版本中，變更目前的記錄中的已排序或篩選的資料**資料錄集**不會變更目前的記錄的位置和**MoveNext**將游標移至下一筆記錄後面的目前記錄。  
  
 使用**MovePrevious**方法來移動目前的記錄位置回溯一筆記錄 (上方**資料錄集**)。 **資料錄集**物件必須支援書籤或回溯資料指標移動; 否則方法呼叫會產生錯誤。 如果第一筆記錄是目前的記錄，而且您呼叫**MovePrevious**方法，ADO 會設定為目前的記錄中的第一個記錄之前的位置**資料錄集**([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**True**)。 嘗試移動回溯時**BOF**內容已出現**True**會產生錯誤。 如果**資料錄集**物件不支援書籤或回溯資料指標移動**MovePrevious**方法會產生錯誤。  
  
 如果**資料錄集**是順向的而且您想要支援向前及向後捲動，您可以使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性，建立將支援向後資料指標移動記錄快取透過[移動](../../../ado/reference/ado-api/move-method-ado.md)方法。 因為快取的記錄會載入到記憶體中，您應該避免快取比所需的多個記錄。 您可以呼叫**MoveFirst**中順向方法**資料錄集**物件; 如此一來，可能會導致重新執行所產生的命令，提供者**資料錄集**物件.  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱  
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法範例 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法範例 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法範例 （VC + +）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
