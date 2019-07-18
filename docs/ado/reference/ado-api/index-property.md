---
title: Index 屬性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba871d6d0e84b8068cb36a3ed2516a2665db28d4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932430"
---
# <a name="index-property"></a>Index 屬性
指出正在使用中的目前的索引名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，也就是索引的名稱。  
  
## <a name="remarks"></a>備註  
 所命名的索引**Index**屬性必須先前已宣告於基底資料表的基礎**資料錄集**物件。 也就是索引之前一定已經宣告以程式設計方式為 ADOX [Index](../../../ado/reference/adox-api/index-object-adox.md)物件，或建立基底資料表時。  
  
 如果索引不能設定，會發生執行階段錯誤。 **Index**無法設定屬性，在下列情況下：  
  
-   內[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)或是**RecordsetChangeComplete**事件處理常式。  
  
-   如果**Recordset**仍在執行作業 (這可判斷[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性)。  
  
-   如果已設定篩選**Recordset**使用[篩選](../../../ado/reference/ado-api/filter-property.md)屬性。  
  
 **的索引**可以一律可設定屬性成功**資料錄集**已關閉，但**資料錄集**將不成功，會開啟，或索引將無法使用，如果基礎提供者不支援索引。  
  
 如果可以設定索引，可能會變更目前的資料列位置。 這會更新[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性，並會引發**WillChangeRecordset**， **RecordsetChangeComplete**， [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)，並[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)事件。  
  
 如果可以設定索引和[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)屬性是**Locktype**或是**adLockOptimistic**，然後隱含[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)執行作業。 這會釋放目前和受影響的群組。 已釋放任何現有的篩選條件，和目前的資料列位置變更為已排序的第一列**資料錄集**。  
  
 **Index**屬性可搭配[搜尋](../../../ado/reference/ado-api/seek-method.md)方法。 如果基礎提供者不支援**索引**屬性，因此**Seek**方法，請考慮使用[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法改為。 判斷是否**Recordset**物件支援的索引[支援](../../../ado/reference/ado-api/supports-method.md) **(adIndex)** 方法。  
  
 內建**Index**屬性不相關的動態[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)屬性，雖然它們都處理索引。  
  
## <a name="applies-to"></a>適用於  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Seek 方法和 Index 屬性範例 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
