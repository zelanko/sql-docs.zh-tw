---
title: 索引集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e84f49d5ad2d88ebb88417ae01046c0bcfd8006
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966043"
---
# <a name="indexes-collection-adox"></a>Indexes 集合 (ADOX)
包含資料表的所有[索引](../../../ado/reference/adox-api/index-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 對於 ADOX 而言，**索引**集合的[Append](../../../ado/reference/adox-api/append-method-adox-indexes.md)方法是唯一的。 您可以：  
  
-   使用**Append**方法，將新的索引新增至集合。  
  
 其餘的屬性和方法都是 ADO 集合的標準。 您可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)屬性存取集合中的索引。  
  
-   傳回包含在集合中具有[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性的索引數目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法，從集合中移除索引。  
  
-   更新集合中的物件，以使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法來反映目前的資料庫架構。  
  
 本章節包含下列主題。  
  
-   [Indexes 集合屬性、方法和事件](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [索引附加方法範例（VB）](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [Index 物件 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)
