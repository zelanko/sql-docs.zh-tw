---
title: 在記錄集中移動的更多方式 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3d68fb018e3b72e193127f8f49160813c06a1332
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764809"
---
# <a name="more-ways-to-move-in-a-recordset"></a>更多可以在資料錄集中移動的方法
下列四種方法可用來在**記錄集**內四處移動或滾動： [MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)。 （其中有些方法在順向資料指標上無法使用）。  
  
 **MoveFirst**會將目前的記錄位置變更為**記錄集**內的第一筆記錄。 **MoveLast**會將目前的記錄位置變更為**記錄集**內的最後一筆記錄。 若要使用**MoveFirst**或**MoveLast**，**記錄集**物件必須支援書簽或回溯游標移動;否則，方法呼叫會產生錯誤。  
  
 **MoveNext**會將目前的記錄位置向前移動一次。 當您呼叫**MoveNext**時，如果您在最後一筆記錄中， **EOF**將會設定為**True**。 **MovePrevious**將目前的記錄位置向後移動一處。 當您呼叫**MovePrevious**時，如果您在第一筆記錄，則會將**BOF**設定為**True**。 當您使用這些方法時，最好檢查**EOF**和**BOF**屬性，並在您移出**記錄集**的任一端時，將游標移回有效的目前記錄位置，如下所示：  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 或者，在**MovePrevious**方法的情況下：  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 如果**記錄集**已經過篩選或排序，而且目前記錄的資料已變更，則位置也可能會變更。 在這種情況下， **MoveNext**方法會正常運作，但請注意，位置會從新位置向前移動一筆記錄，而非舊位置。 例如，變更目前記錄中的資料，使記錄移至已排序**記錄集**的結尾，這表示呼叫**MoveNext**會在 ADO 中將目前的記錄設定為**記錄集**內最後一筆記錄之後的位置（**EOF**  =  **True**）。  
  
 **記錄集**物件之各種 Move 方法的行為，在**記錄集**內的資料上會有某種程度的相依。 加入至**記錄集**的新記錄一開始會以特定順序加入，這是由資料來源所定義，而且可能會隱含或明確地相依于新記錄中的資料。 例如，如果在填入**記錄集**的查詢中進行排序或聯結，則會將新的記錄插入**記錄集**內的適當位置。 如果在建立**記錄集**時未明確指定排序，則資料來源執行中的變更可能會導致傳回的資料列順序不小心變更。 此外，**記錄集**的排序、篩選和編輯功能可能會影響順序，而且記錄集內的資料列可能會顯示。  
  
 因此， **MoveNext**、 **MovePrevious**、 **MoveFirst**、 **MoveLast**和**Move**對相同**記錄集**上執行的其他作業都很敏感。 ADO 一律會嘗試維護您目前的位置，直到您明確地移動它，但有時中間的變更會使其難以瞭解後續移動的效果。 例如，如果您呼叫**MoveFirst**來定位已排序**記錄集**的第一個資料列，而您將排序從遞增順序變更為遞減順序，則您仍在相同的資料列上，但現在它是**記錄集**的最後一個資料列。 **MoveFirst**會將您帶到不同的資料列（新的第一個資料列）。  
  
 另一個範例是，如果您放在**記錄集**中間的特定資料列上，並呼叫**Delete** ，然後呼叫**MoveNext**，則您現在會緊接在已刪除記錄後面的記錄。 但是呼叫**MovePrevious**會使記錄在您刪除目前記錄的前面，因為已刪除的記錄不會再計入**記錄集**的使用中成員資格。  
  
 特別難以針對移動到目前記錄之方法的所有提供者，定義一致的移動語義，例如，變更目前記錄中資料的**MovePrevious**、 **MoveNext**和**移動**。 例如，如果您使用已排序、已篩選的**記錄集**，而且您變更了目前記錄中的資料，使其在所有其他記錄之前，但變更的資料也不再符合篩選準則，則不會清楚**MoveNext**作業應帶您的位置。 最安全的結論是在資料變更時，**記錄集**內的相對移動是風險，而在編輯、加入或刪除記錄時，則是以絕對移動（例如使用**MoveFirst**或**MoveLast**）來進行。 排序和篩選應該以主鍵或識別碼為基礎，因為此類型的值不應該變更。
