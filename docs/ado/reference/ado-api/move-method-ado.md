---
description: Move 方法 (ADO)
title: " (ADO) 移動方法 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 57a5b882148c899136ff92315ff109b68868aa66
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774407"
---
# <a name="move-method-ado"></a>Move 方法 (ADO)
移動 [記錄集](./recordset-object-ado.md) 物件中目前記錄的位置。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>參數  
 *NumRecords*  
 帶正負號的 **長整數** 運算式，指定目前記錄位置移動的記錄數目。  
  
 *啟動*  
 選擇性。 評估為書簽的 **字串** 值或 **變異** 數。 您也可以使用 [BookmarkEnum](./bookmarkenum.md) 值。  
  
## <a name="remarks"></a>備註  
 所有**記錄集**物件都支援**Move**方法。  
  
 如果 *NumRecords* 引數大於零，則目前的記錄位置會向 (向前移動到 **記錄集**) 的結尾。 如果 *NumRecords* 小於零，則目前的記錄位置會向後 (朝 **記錄集** 的開頭) 。  
  
 如果 **移動** 呼叫會將目前的記錄位置移至第一筆記錄之前的某個點，則 ADO 會將目前的記錄設定為記錄集內的第一筆記錄之前的位置， ([BOF](./bof-eof-properties-ado.md) 為 **True**) 。 當 **BOF** 屬性已 **為 True** 時，嘗試向後移動會產生錯誤。  
  
 如果 **移動** 呼叫會將目前的記錄位置移至最後一筆記錄之後的某個點，則 ADO 會將目前的記錄設定為記錄集內最後一筆記錄之後的位置， ([EOF](./bof-eof-properties-ado.md) 是 **True**) 。 當 **EOF** 屬性已 **成立** 時，嘗試向前移動會產生錯誤。  
  
 從空的**記錄集**物件呼叫**Move**方法會產生錯誤。  
  
 如果您傳遞 *Start* 引數，則會在記錄 **集** 物件支援書簽時，使用此書簽來移動該記錄。 如果未指定，則移動會相對於目前的記錄。  
  
 如果您使用 [CacheSize](./cachesize-property-ado.md) 屬性從提供者本機快取記錄，則傳遞可將目前記錄位置移至目前快取記錄群組之外的 *NumRecords* 引數，會強制 ADO 從目的地記錄開始取得新的記錄群組。 **CacheSize**屬性會決定新抓取群組的大小，而目的地記錄是第一個抓取的記錄。  
  
 如果 **記錄集** 物件是順向的，使用者仍然可以傳遞小於零的 *NumRecords* 引數，但前提是目的地是在目前的快取記錄集內。 如果 **移動** 呼叫會在第一個快取記錄之前將目前的記錄位置移至記錄，將會發生錯誤。 因此，您可以使用記錄快取，支援在僅支援向前滾動的提供者上進行完整滾動。 由於快取記錄會載入至記憶體中，因此，您應該避免快取比所需更多的記錄。 即使順向**記錄集**物件以這種方式支援反向移動，在任何順向**記錄集**物件上呼叫[MovePrevious](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法仍會產生錯誤。  
  
> [!NOTE]
>  視您的提供者而定，支援在順向 **記錄集中** 向前移動是不可預測的。 如果目前的記錄已定位於 **記錄集**內的最後一筆記錄之後，則向後 **移動** 可能不會產生正確的目前位置。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB) 移動方法範例 ](./move-method-example-vb.md)   
 [將方法範例 (VBScript) ](./move-method-example-vbscript.md)   
 [將方法範例 (VC + +) ](./move-method-example-vc.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (ADO) ](./movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、MoveLast、MoveNext 和 MovePrevious 方法 (RDS) ](../rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](./moverecord-method-ado.md)