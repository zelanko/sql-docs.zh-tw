---
title: Move 方法 (ADO) |Microsoft Docs
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
manager: jroth
ms.openlocfilehash: c7b99a0848101ca0fad4844c51e44f1ccc628cd6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707607"
---
# <a name="move-method-ado"></a>Move 方法 (ADO)
移動中的目前記錄的位置[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>參數  
 *NumRecords*  
 帶正負號**長**運算式，指定目前的記錄位置會移動的記錄數目。  
  
 *啟動*  
 選擇性。 A**字串**值，或**Variant**評估為書籤。 您也可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
## <a name="remarks"></a>備註  
 **移動**方法都支援所有**資料錄集**物件。  
  
 如果*NumRecords*引數是小於或等於零，目前的記錄位置會向前移動 (接近結尾**資料錄集**)。 如果*NumRecords*小於零，目前的記錄位置會向後移動 (開頭**資料錄集**)。  
  
 如果**移動**呼叫會將目前的記錄位置移至第一筆記錄之前的時間點、 ADO 資料錄集中第一筆記錄之前的位置設定目前的記錄 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，則為 True**). 嘗試移動時，為了與舊版**BOF**屬性已 **，則為 True**會產生錯誤。  
  
 如果**移動**呼叫會移至點目前的記錄位置在最後一筆記錄之後，ADO 資料錄集的最後一筆記錄之後位置設定目前的記錄 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，則為 True**). 嘗試移動時，向前**EOF**屬性已 **，則為 True**會產生錯誤。  
  
 呼叫**移動**方法的空**資料錄集**物件會產生錯誤。  
  
 如果您傳遞*開始*引數，是相對於與此書籤，記錄的移動假設**資料錄集**物件支援書籤。 如果未指定，移動是相對於目前的記錄。  
  
 如果您使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性，以在本機快取記錄提供者，並傳遞*NumRecords*移動目前的記錄位置的快取記錄的目前群組外的引數強制 ADO 來擷取一組新的記錄，從 目的記錄。 **CacheSize**屬性會決定新擷取群組的大小和目的地記錄會擷取第一筆記錄。  
  
 如果**Recordset**物件為順向、 使用者依然可以傳遞*NumRecords*引數小於零，就必須提供目的地是目前的快取的記錄集內。 如果**移動**呼叫會移動目前的記錄位置之前的第一個快取的記錄，記錄會發生錯誤。 因此，您可以使用支援透過支援只會順向捲動的提供者的完整捲動記錄快取。 因為快取的記錄會載入到記憶體中，您應該避免快取更多超出所需的記錄。 即使順向**Recordset**物件支援向後移動，如此一來，呼叫[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)任何方法順向**資料錄集**物件仍然會產生錯誤。  
  
> [!NOTE]
>  支援在順向後移動**資料錄集**是無法預測的取決於您的提供者而定。 如果已位置之後的最後一個記錄中的目前資料錄**Recordset**，**移動**回溯可能不會導致正確的目前位置。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Move 方法範例 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 方法範例 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 方法範例 （VC + +）](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
