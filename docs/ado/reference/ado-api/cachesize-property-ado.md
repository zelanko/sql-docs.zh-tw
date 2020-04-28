---
title: CacheSize 屬性（ADO） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c6b33ef7eb4bae796fa2b2da59a7b1dc805d739e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920337"
---
# <a name="cachesize-property-ado"></a>CacheSize 屬性 (ADO)
指示記錄[集](../../../ado/reference/ado-api/recordset-object-ado.md)物件中，從本機快取到記憶體中的記錄數目。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回必須大於0的**長**數值。 預設值為 1。  
  
## <a name="remarks"></a>備註  
 您可以使用**CacheSize**屬性來控制要一次從提供者取得本機記憶體中的多少筆記錄。 例如，如果**CacheSize**是10，則在第一次開啟**記錄集**物件之後，提供者會將前10筆記錄抓取到本機記憶體。 當您在**記錄集**物件上移動時，提供者會傳回本機記憶體緩衝區中的資料。 當您移至快取中的最後一筆記錄之後，此提供者就會從資料來源將接下來10筆記錄抓取至快取中。  
  
> [!NOTE]
>  **CacheSize**是以**最大開啟資料列**提供者特定的屬性（在**記錄集**物件的**Properties**集合中）為基礎。 您無法將**CacheSize**設定為大於**最大開啟資料列**的值。 若要修改提供者可以開啟的資料列數目，請設定 [**開啟的最大資料列**數]。  
  
 **CacheSize**的值可以在**記錄集**物件的生命週期內進行調整，但變更此值只會影響從資料來源後續的檢索之後快取中的記錄數目。 單獨變更屬性值不會變更目前的快取內容。  
  
 如果要抓取的記錄少於**CacheSize**指定，則提供者會傳回其餘的記錄，而且不會發生錯誤。  
  
 不允許**CacheSize**設定為零，且會傳回錯誤。  
  
 從快取中取出的記錄，不會反映其他使用者對來源資料所做的並行變更。 若要強制更新所有快取的資料，請使用[Resync](../../../ado/reference/ado-api/resync-method.md)方法。  
  
 如果**CacheSize**設定為大於1的值，流覽方法（[Move](../../../ado/reference/ado-api/move-method-ado.md)、 [MoveFirst、MoveLast、MoveNext 和 MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)）可能會導致導覽至已刪除的記錄（如果在抓取記錄之後發生刪除）。 初始提取之後，除非您嘗試從已刪除的資料列存取資料值，否則後續的刪除將不會反映在資料快取中。 不過，將**CacheSize**設定為一個可以排除此問題，因為無法提取已刪除的資料列。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [CacheSize 屬性範例（VB）](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [CacheSize 屬性範例（VC + +）](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [CacheSize 屬性範例 (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
