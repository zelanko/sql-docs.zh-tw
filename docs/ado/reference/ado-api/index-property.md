---
title: "Index 屬性 |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9091e9a65b178806c8695faffa50f11946c6b2ca
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="index-property"></a>Index 屬性
表示索引的目前作用中的名稱[資料錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，這是索引的名稱。  
  
## <a name="remarks"></a>備註  
 索引命名**索引**屬性必須先前已宣告於基底資料表的基礎**資料錄集**物件。 也就是索引之前一定已經宣告以程式設計方式為 ADOX[索引](../../../ado/reference/adox-api/index-object-adox.md)物件，或建立基底資料表時。  
  
 如果索引不能設定，會發生執行階段錯誤。 **索引**屬性無法設定下列條件：  
  
-   內[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)或**RecordsetChangeComplete**事件處理常式。  
  
-   如果**資料錄集**仍在執行作業 (這可以由[狀態](../../../ado/reference/ado-api/state-property-ado.md)屬性)。  
  
-   如果已設定篩選器上**資料錄集**與[篩選](../../../ado/reference/ado-api/filter-property.md)屬性。  
  
 **索引**屬性可以永遠成功設定如果**資料錄集**已關閉，但**資料錄集**將不成功，會開啟，或索引將無法使用，如果基礎提供者不支援索引。  
  
 如果可以設定的索引，可能會變更目前的資料列位置。 這會導致更新[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性，而且會引發**WillChangeRecordset**， **RecordsetChangeComplete**， [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)，和[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)事件。  
  
 如果可以設定索引和[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)屬性是**Locktype**或**Adlockreadonly**，然後隱含[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)會執行作業。 這會釋放目前和受影響的群組。 已釋放任何現有的篩選，和目前資料列位置變更為第一個資料列 reordered**資料錄集**。  
  
 **索引**屬性用於搭配[搜尋](../../../ado/reference/ado-api/seek-method.md)方法。 如果基礎提供者不支援**索引**屬性，因此**搜尋**方法，請考慮使用[尋找](../../../ado/reference/ado-api/find-method-ado.md)方法改為。 判斷是否**資料錄集**物件支援的索引將以[支援](../../../ado/reference/ado-api/supports-method.md)**(adIndex)**方法。  
  
 內建**索引**與不相關的動態屬性[最佳化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)屬性，雖然它們都處理索引。  
  
## <a name="applies-to"></a>適用於  
 [資料錄集物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [搜尋方法和索引屬性範例 (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [索引物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [搜尋方法](../../../ado/reference/ado-api/seek-method.md)
