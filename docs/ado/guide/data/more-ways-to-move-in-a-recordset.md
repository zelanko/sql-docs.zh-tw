---
title: "更多方法來移動資料錄集中 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c3e3f666fd96a1b00d78ba364a8df062fa3f6397
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="more-ways-to-move-in-a-recordset"></a>更多方法來移動資料錄集中
下列四種方法可用來移動，或在捲動**資料錄集**: [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)。 （其中某些方法是在順向資料指標上無法使用）。  
  
 **MoveFirst**第一個記錄中變更目前的記錄位置**資料錄集**。 **MoveLast**目前記錄的最後一個位置的變更記錄中**資料錄集**。 若要使用**MoveFirst**或**MoveLast**、**資料錄集**物件必須支援書籤或回溯資料指標移動; 否則方法呼叫會產生錯誤。  
  
 **MoveNext**移動目前的記錄向前置於同一個地方。 如果您在最後一個記錄當您呼叫**MoveNext**， **EOF**會設定為**True**。 **MovePrevious**移動目前的記錄位置回溯的同一個地方。 當您呼叫時如果是在第一筆資料錄**MovePrevious**， **BOF**會設定為**True**。 最好檢查**EOF**和**BOF**屬性時使用這些方法，並將游標移回是有效的目前記錄位置如果您移出結尾**資料錄集**，如下所示：  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 或者，如果是**MovePrevious**方法：  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 萬一其中**資料錄集**已篩選或排序和目前的記錄資料變更，也可能會變更位置。 在此情況下**MoveNext**方法可正常運作，但請注意，位置是一個移動記錄向前復原新的位置，而不是舊的位置。 比方說，變更目前的記錄中的資料，使記錄會移至結尾的已排序**資料錄集**，就表示在呼叫**MoveNext**導致 ADO 設為目前的記錄最後一筆記錄後的位置**資料錄集**(**EOF** = **True**)。  
  
 各種移動方法的行為**資料錄集**相依物件，在某種程度上內的資料**資料錄集**。 新記錄新增至**資料錄集**一開始會加入以特定順序，如此由資料來源所定義且可能會相依隱含或明確地在新的記錄中的資料。 例如，如果排序或聯結中進行查詢填入**資料錄集**，新的記錄將會插入中的適當位置中**資料錄集**。 如果順序不明確建立時指定**資料錄集**，在資料來源實作的變更可能使不小心變更傳回的資料列的順序。 此外，排序、 篩選與編輯函式的**資料錄集**可能會影響順序，可能是資料錄集中的哪些資料列就可以看到。  
  
 因此， **MoveNext**， **MovePrevious**， **MoveFirst**， **MoveLast**，和**移動**全部在同一個執行其他作業的區分**資料錄集**。 ADO 將永遠嘗試維持您目前的位置，直到您明確地移動檔案，但有時候，中間變更難以了解後續移動的效果。 比方說，如果您呼叫**MoveFirst**位置上的已排序的第一個資料列**資料錄集**並且將遞增的順序與遞減順序排序，您就仍然可以在相同的資料列上，但現在它是最後一個資料列在**資料錄集**。 **MoveFirst**會帶您前往不同的資料列 （新的第一個資料列）。  
  
 另舉一例，如果您所在位置中的特定資料列**資料錄集**而且您呼叫**刪除**，然後呼叫**MoveNext**，現在您已經準備記錄之後立即刪除的記錄。 但呼叫**MovePrevious**讓記錄之前刪除目前的記錄，因為已刪除的記錄，就不會再計算的作用中的成員資格**資料錄集**。  
  
 特別難以定義一致的移動語意，跨所有方法，會移動相對於目前的記錄提供者 — **MovePrevious**， **MoveNext**，和**移動** — 遇到時變更目前的記錄中的資料。 例如，如果您正在使用已排序，篩選**資料錄集**，並且您變更目前的記錄中的資料，使它會在所有其他的記錄之前，但您已變更的資料也不再符合篩選條件，並不清楚的位置**MoveNext**作業花費時間。 最安全的結論是該相對內移動**資料錄集**較高的風險比絕對移動 (例如使用**MoveFirst**或**MoveLast**) 資料時變更記錄會進行編輯，加入或刪除。 排序和篩選應能以於主索引鍵或識別碼，因為這種類型的值不應該變更。

