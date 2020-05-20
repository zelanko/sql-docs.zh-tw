---
title: 索引屬性 |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 2a77aa3c2e144859eaead332e71c5c4c8776608c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758694"
---
# <a name="index-property"></a>Index 屬性
指出目前對[記錄集](../../../ado/reference/ado-api/recordset-object-ado.md)物件有效的索引名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回**字串**值，這是索引的名稱。  
  
## <a name="remarks"></a>備註  
 **索引**屬性所命名的索引之前，必須先在**記錄集**物件的基礎資料表上宣告。 也就是說，索引必須以程式設計方式宣告為 ADOX[索引](../../../ado/reference/adox-api/index-object-adox.md)物件，或建立基表時。  
  
 如果無法設定索引，將會發生執行階段錯誤。 在下列情況下，無法設定**Index**屬性：  
  
-   在[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)或**RecordsetChangeComplete**事件處理常式內。  
  
-   如果**記錄集**仍在執行作業（可以由[State](../../../ado/reference/ado-api/state-property-ado.md)屬性決定）。  
  
-   如果已在**記錄集**上使用[filter](../../../ado/reference/ado-api/filter-property.md)屬性來設定篩選準則。  
  
 如果**記錄集**已關閉，**索引**屬性一律可以成功設定，但是**記錄集**將無法成功開啟，或者如果基礎提供者不支援索引，則索引將無法使用。  
  
 如果可以設定索引，則目前的資料列位置可能會變更。 這會造成[AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md)屬性的更新，並且會引發**WillChangeRecordset**、 **RecordsetChangeComplete**、 [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)和[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)事件。  
  
 如果可以設定索引，而且[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)屬性是**adLockPessimistic**或**adLockOptimistic**，則會執行隱含的[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)作業。 這會釋放目前和受影響的群組。 已釋放任何現有的篩選，而且目前的資料列位置會變更為重新排序**記錄集**的第一個資料列。  
  
 **Index**屬性會與[Seek](../../../ado/reference/ado-api/seek-method.md)方法搭配使用。 如果基礎提供者不支援**Index**屬性，並因此是**Seek**方法，請考慮改用[Find](../../../ado/reference/ado-api/find-method-ado.md)方法。 使用[支援](../../../ado/reference/ado-api/supports-method.md)**（adIndex）** 方法來判斷**記錄集**物件是否支援索引。  
  
 內建**索引**屬性與動態[優化](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md)屬性不相關，雖然它們都處理索引。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Seek 方法和 Index 屬性範例（VB）](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Index 物件（ADOX）](../../../ado/reference/adox-api/index-object-adox.md)   
 [Seek 方法](../../../ado/reference/ado-api/seek-method.md)
