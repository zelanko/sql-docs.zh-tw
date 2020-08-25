---
description: Index 屬性
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 084c27d5101c5aa08d25e7d073158a859d275d3b
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774803"
---
# <a name="index-property"></a>Index 屬性
表示 [記錄集](./recordset-object-ado.md) 物件目前作用中的索引名稱。  
  
## <a name="settings-and-return-values"></a>設定和傳回值  
 設定或傳回 **字串** 值，這是索引的名稱。  
  
## <a name="remarks"></a>備註  
 **索引**屬性所命名的索引之前，必須先在**記錄集**物件的基礎資料表上宣告。 也就是說，您必須以程式設計的方式將索引宣告為 ADOX [索引](../adox-api/index-object-adox.md) 物件，或在建立基表時以程式設計的方式宣告。  
  
 如果無法設定索引，就會發生執行階段錯誤。 在下列情況下，無法設定 **Index** 屬性：  
  
-   在 [WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md) 或 **RecordsetChangeComplete** 事件處理常式中。  
  
-   如果 **記錄集** 仍在執行作業 (可由 [狀態](./state-property-ado.md) 屬性) 來決定。  
  
-   如果已在具有[篩選](./filter-property.md)屬性的**記錄集**上設定篩選準則，則為。  
  
 如果**記錄集**已關閉，**索引**屬性一律可以成功設定，但是如果基礎提供者不支援索引，則不會成功開啟**記錄集**，或者索引將無法使用。  
  
 如果可以設定索引，則目前的資料列位置可能會變更。 這會導致 [AbsolutePosition](./absoluteposition-property-ado.md) 屬性的更新，並且會引發 **WillChangeRecordset**、 **RecordsetChangeComplete**、 [WillMove](./willmove-and-movecomplete-events-ado.md)和 [MoveComplete](./willmove-and-movecomplete-events-ado.md) 事件。  
  
 如果可以設定索引，且 [LockType](./locktype-property-ado.md) 屬性為 **adLockPessimistic** 或 **adLockOptimistic**，則會執行隱含的 [UpdateBatch](./updatebatch-method.md) 作業。 這會釋放目前和受影響的群組。 任何現有的篩選都會釋出，而且目前的資料列位置會變更為重新排序 **記錄集**的第一個資料列。  
  
 **Index**屬性與[Seek](./seek-method.md)方法搭配使用。 如果基礎提供者不支援 **Index** 屬性，因此是 **Seek** 方法，請考慮改為使用 [Find](./find-method-ado.md) 方法。 判斷 **記錄集** 物件是否支援 [支援](./supports-method.md)** (adIndex) ** 方法的索引。  
  
 內建 **索引** 屬性與動態 [優化](./optimize-property-dynamic-ado.md) 屬性無關，雖然它們都能處理索引。  
  
## <a name="applies-to"></a>套用至  
 [Recordset 物件 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另請參閱  
 [Seek 方法和 Index 屬性範例 (VB) ](./seek-method-and-index-property-example-vb.md)   
 [ (ADOX) 的索引物件 ](../adox-api/index-object-adox.md)   
 [Seek 方法](./seek-method.md)