---
title: Move 方法（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d76f239094185af7a3e940201b3f99132c0194a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918189"
---
# <a name="move-method-ado"></a>Move 方法 (ADO)
移動[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中目前記錄的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>參數  
 *NumRecords*  
 此為帶正負號的**長**運算式，指定目前記錄位置移動的記錄數目。  
  
 *Start*  
 選擇性。 評估為書簽的**字串**值或**Variant** 。 您也可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
## <a name="remarks"></a>備註  
 所有**記錄集**物件都支援**Move**方法。  
  
 如果*NumRecords*引數大於零，則目前的記錄位置會向前移動（朝**記錄集**的結尾）。 如果*NumRecords*小於零，則目前的記錄位置會向後移動（朝**記錄集**的開頭）。  
  
 如果**移動**呼叫會將目前的記錄位置移至第一筆記錄之前的某個點，ADO 會將目前的記錄設定為記錄集內第一筆記錄之前的位置（[BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為**True**）。 當**BOF**屬性已經**為 True**時，嘗試向後移動會產生錯誤。  
  
 如果**移動**呼叫會將目前的記錄位置移至最後一筆記錄之後的某個點，ADO 會將目前的記錄設定為記錄集內最後一筆記錄之後的位置（[EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)為**True**）。 當**EOF**屬性已經是**True**時，嘗試繼續進行，會產生錯誤。  
  
 從空的**記錄集**物件呼叫**Move**方法會產生錯誤。  
  
 如果您傳遞*Start*引數，則移動會相對於含有此書簽的記錄，假設**記錄集**物件支援書簽。 如果未指定，則移動會相對於目前的記錄。  
  
 如果您使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性從提供者本機快取記錄，傳遞*NumRecords*引數，將目前的記錄位置移到目前的快取記錄群組之外，會強制 ADO 從目的地記錄開始，抓取新的記錄群組。 **CacheSize**屬性會決定新取出群組的大小，而目的地記錄則是第一個抓取的記錄。  
  
 如果**記錄集**物件只是轉寄，則使用者仍然可以傳遞小於零的*NumRecords*引數，前提是目的地是在目前的快取記錄集中。 如果**移動**呼叫會在第一次快取記錄之前將目前的記錄位置移至記錄，將會發生錯誤。 因此，您可以使用記錄快取，以支援在僅支援向前滾動的提供者上進行完整的滾動。 因為快取的記錄會載入記憶體中，所以您應該避免快取超過所需的記錄。 即使順向**記錄集**物件以這種方式支援回溯移動，在任何順向**記錄集**物件上呼叫[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法仍會產生錯誤。  
  
> [!NOTE]
>  視提供者而定，支援順向**記錄集中**的回溯是不可預測的。 如果目前的記錄已放在**記錄集**的最後一筆記錄之後，則向後**移動**可能不會產生正確的目前位置。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Move 方法範例（VB）](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 方法範例（VBScript）](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 方法範例（VC + +）](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法（ADO）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法（RDS）](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
