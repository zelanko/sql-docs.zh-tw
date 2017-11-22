---
title: "Move 方法 (ADO) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords: Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9d1db74ef70a98467e320dc09ff4e19c5935ac04
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2017
---
# <a name="move-method-ado"></a>Move 方法 (ADO)
移動中的目前記錄的位置[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="syntax"></a>語法  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>參數  
 *NumRecords*  
 帶正負號**長**運算式，指定目前的記錄位置移動的記錄數目。  
  
 *啟動*  
 選擇性。 A**字串**值或**Variant** ，評估為書籤。 您也可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
## <a name="remarks"></a>備註  
 **移動**方法適用於所有**資料錄集**物件。  
  
 如果*NumRecords*引數為大於零，目前的記錄位置前移 (的尾端**資料錄集**)。 如果*NumRecords*小於零，會向後移動目前的記錄位置 (開頭**資料錄集**)。  
  
 如果**移動**呼叫會將目前的記錄位置移至第一筆記錄之前，ADO 資料錄集中第一筆記錄之前的位置設定為目前的記錄 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**，則為 True**). 嘗試移動回溯時**BOF**內容已出現**True**會產生錯誤。  
  
 如果**移動**呼叫會移至某個點目前的記錄位置最後一筆記錄之後，ADO 資料錄集中的最後一筆記錄之後將目前的記錄設定至位置 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**，則為 True**). 嘗試移動時，正向**EOF**內容已出現**True**會產生錯誤。  
  
 呼叫**移動**方法從空**資料錄集**物件會產生錯誤。  
  
 如果您要傳入*啟動*相對於與此書籤，記錄的引數，移動的假設**資料錄集**物件支援書籤。 如果未指定，移動的過程相對於目前的記錄。  
  
 如果您使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)屬性，以在本機快取提供者，從記錄傳遞*NumRecords*移動目前的記錄位置快取記錄的目前群組外的引數強制 ADO 来擷取的記錄，從目的記錄開始新的群組。 **CacheSize**屬性會決定新擷取群組的大小和目的記錄是第一個擷取的記錄。  
  
 如果**資料錄集**物件是順向、 使用者仍然可以傳遞*NumRecords*引數小於零，提供目的地是目前的快取的資料錄集內。 如果**移動**呼叫會將目前的記錄位置之前記錄第一個快取，會發生錯誤。 因此，您可以使用支援透過支援僅向前捲動的提供者的完整捲動記錄快取。 因為快取的記錄會載入到記憶體中，您應該避免快取更多超出所需的記錄。 即使順向**資料錄集**物件支援向後移動，如此一來，呼叫[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法上任何順向**資料錄集**物件仍然會產生錯誤。  
  
> [!NOTE]
>  支援在順向後移動**資料錄集**不是可預測，您的提供者而定。 如果目前的記錄具有已位於最後一筆記錄之後**資料錄集**，**移動**回溯可能不會造成在正確的目前位置。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>請參閱＜  
 [Move 方法範例 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 方法範例 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 方法的範例 （VC + +）](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
