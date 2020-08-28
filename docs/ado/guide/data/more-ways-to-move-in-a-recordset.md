---
description: 更多可以在資料錄集中移動的方法
title: 更多在記錄集中移動的方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: e8c668bc24b388d0367429086416cd67b5355550
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980289"
---
# <a name="more-ways-to-move-in-a-recordset"></a>更多可以在資料錄集中移動的方法
下列四種方法可用來在 **記錄集**內四處移動或滾動： [MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)。  (在順向資料指標上無法使用這些方法的部分。 )   
  
 **MoveFirst** 會將目前的記錄位置變更為 **記錄集**內的第一筆記錄。 **MoveLast** 會將目前的記錄位置變更為 **記錄集**內的最後一筆記錄。 若要使用 **MoveFirst** 或 **MoveLast**， **記錄集** 物件必須支援書簽或後置資料指標移動;否則，方法呼叫將會產生錯誤。  
  
 **MoveNext** 將目前的記錄位置往前移動一個位置。 如果您在呼叫 **MoveNext**時是在最後一筆記錄上， **EOF** 將會設定為 **True**。 **MovePrevious** 會將目前的記錄位置向後移動一個位置。 當您呼叫 **MovePrevious**時，如果您是第一筆記錄，則 **BOF** 將設定為 **True**。 使用這些方法時，最好檢查 **EOF** 和 **BOF** 屬性，如果您移出 **記錄集**的任一端，則將游標移回有效的目前記錄位置，如下所示：  
  
```  
. . .  
oRs.MoveNext  
If oRs.EOF Then oRs.MoveLast  
. . .   
```  
  
 或者，在 **MovePrevious** 方法的案例中：  
  
```  
. . .   
oRs.MovePrevious  
If oRs.BOF Then oRs.MoveFirst  
. . .  
```  
  
 如果已篩選或排序 **記錄集** ，且目前記錄的資料已變更，則位置也可能會變更。 在這種情況下， **MoveNext** 方法會正常運作，但請注意，位置會從新位置向前移動一筆記錄，而不是舊的位置。 例如，變更目前記錄中的資料，讓記錄移至已排序**記錄集**的結尾，表示呼叫**MoveNext**會導致 ADO 將目前的記錄設定為**記錄集**內最後一筆記錄之後的位置， (**EOF**  =  **True**) 。  
  
 **記錄集**物件之各種移動方法的行為，取決於**記錄集**內資料的某些程度。 新記錄加入至 **記錄集** 時，一開始會以特定的順序加入，此順序是由資料來源所定義，而且可能會隱含或明確地在新記錄中的資料上相依。 例如，如果在填入 **記錄集**的查詢內執行排序或聯結，則會將新的記錄插入 **記錄集**內的適當位置。 如果在建立 **記錄集**時未明確指定順序，資料來源執行的變更可能會使傳回的資料列順序不小心變更。 此外， **記錄集** 的排序、篩選和編輯函數可能會影響順序，而且可能會顯示記錄集中的資料列。  
  
 因此， **MoveNext**、 **MovePrevious**、 **MoveFirst**、 **MoveLast**和 **Move** 全都是對相同 **記錄集**上執行的其他作業敏感。 ADO 一律會嘗試維持您目前的位置，直到您明確移動為止，但有時候，中間的變更會讓您難以瞭解後續移動的影響。 例如，如果您呼叫 **MoveFirst** 來定位已排序之 **記錄集** 的第一個資料列，並將排序從遞增順序變更為遞減順序，您仍會在同一個資料列上，但現在它是 **記錄集**的最後一個資料列。 **MoveFirst** 會將您帶到不同的資料列， (新的第一個資料列) 。  
  
 另一個範例是，如果您將定位於 **記錄集** 中間的特定資料列，而且您呼叫 **Delete** ，然後呼叫 **MoveNext**，則現在會在已刪除之記錄之後的記錄上。 但是呼叫 **MovePrevious** 會讓記錄在您刪除目前記錄的前面，因為已刪除的記錄不會在 **記錄集**的作用中成員資格內計算。  
  
 在對目前記錄中變更資料的臉部 **MovePrevious**、 **MoveNext**和 **移動** 的所有提供者之間，定義一致的移動語法，特別困難。 例如，如果您使用已排序、已篩選的 **記錄集**，而您變更目前記錄中的資料，使其在所有其他記錄之前，但變更過的資料也不再符合篩選，則在執行 **MoveNext** 作業時並不清楚。 最安全的結論是， **記錄集** 內的相對移動風險于絕對移動 (例如使用 **MoveFirst** 或 **MoveLast**) 當資料在編輯、新增或刪除記錄時變更。 排序和篩選應以主鍵或識別碼為基礎，因為這種類型的值不應變更。