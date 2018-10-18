---
title: 更多資料錄集中移動的方式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- Recordset object [ADO], moving
- MovePrevious method [ADO]
ms.assetid: 9f8cf1b2-3def-453f-a0ff-4646c5f15262
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: acc9da7f07836d0aad8e9cc60a79ff117371dd46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822616"
---
# <a name="more-ways-to-move-in-a-recordset"></a>更多可以在資料錄集中移動的方法
下列四種方法來移動，或在捲動**Recordset**: [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)。 （其中某些方法是在順向資料指標上無法使用）。  
  
 **MoveFirst**中的第一個記錄中變更目前的記錄位置**資料錄集**。 **MoveLast**中的目前記錄的最後一個位置的變更記錄**資料錄集**。 若要使用**MoveFirst**或是**MoveLast**，則**資料錄集**物件必須支援書籤或回溯資料指標移動; 否則方法呼叫會產生錯誤。  
  
 **MoveNext**移動目前的記錄向前置於同一個地方。 如果您在最後一個記錄當您呼叫**MoveNext**， **EOF**將會設定為**True**。 **MovePrevious**移動目前的記錄位置回溯的同一個地方。 當您呼叫如果會在第一筆資料錄**MovePrevious**， **BOF**將會設定為**True**。 最好是檢查**EOF**並**BOF**時使用這些方法的屬性並將游標移回是有效的目前記錄位置如果您移動的任一端關閉**資料錄集**，如下所示：  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 或者，若是**MovePrevious**方法：  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 萬一其中**資料錄集**已篩選或排序和目前的記錄資料變更時，可能也會變更位置。 在此情況下**MoveNext**方法可正常運作，但請留意這個位置是移動的一個轉寄記錄從新的位置，而不是舊的位置。 比方說，變更目前的記錄中的資料，使記錄會移至結尾的已排序**資料錄集**，表示該呼叫**MoveNext**結果在 ADO 中設為目前的記錄在最後一筆記錄之後的位置**Recordset** (**EOF** = **True**)。  
  
 各種移動方法的行為**Recordset**某種程度來說中的資料物件相依**資料錄集**。 加入新資料錄**資料錄集**一開始加入在特定的順序排列，這由資料來源所定義，且可能隱含相依或明確地在新的記錄中的資料。 比方說，如果排序或完成聯結於其中填入在查詢內**Recordset**，在中的適當位置插入新資料錄**資料錄集**。 如果順序未明確指定在建立時**資料錄集**，在資料來源實作的變更可能使不小心變更傳回的資料列的排序。 此外，排序、 篩選與編輯函式**資料錄集** 蝭 順序和資料錄集中的哪些資料列可能會顯示。  
  
 因此， **MoveNext**， **MovePrevious**， **MoveFirst**， **MoveLast**，以及**移動**全部在同一個執行的其他作業來區分**資料錄集**。 ADO 將永遠嘗試維持您目前的位置，直到您明確地移動，但有時候，中間變更讓您難以了解後續移動的影響。 比方說，如果您呼叫**MoveFirst**上的已排序的第一個資料列的位置**資料錄集**，並且將遞增順序與遞減順序排序，您就仍在相同的資料列，但現在它是最後一個資料列在 **資料錄集**。 **MoveFirst**會帶您前往不同的資料列 （新的第一個資料列）。  
  
 另舉一例，如果您位於特定的資料列中的中間**資料錄集**，而且您呼叫**刪除**，然後呼叫**MoveNext**，現在您已記錄已刪除的資料錄的正後方。 但呼叫**MovePrevious**可讓記錄之前刪除目前的記錄，因為已刪除的資料錄，就不會再計算的使用中的成員資格**資料錄集**。  
  
 特別難以定義一致的移動語意的方法，會移動相對於目前資料錄的所有提供者之間 — **MovePrevious**， **MoveNext**，和**移動** — 面對變更目前的記錄中的資料。 比方說，如果您正在使用已排序、 篩選**資料錄集**，並且您變更目前的記錄中的資料，因此它會在所有其他的記錄，但您已變更的資料也不再符合篩選條件，並不清楚的位置**MoveNext**作業花費時間。 最安全的結論是，相對的移動內**Recordset**較高的風險比絕對的移動 (例如使用**MoveFirst**或**MoveLast**) 資料時變更時記錄正在進行編輯，新增或刪除。 排序和篩選應該根據主索引鍵或識別碼，因為這種類型的值不應該變更。
