---
title: Keys 集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a7bebc1c05ab195d3b23c5c0894d4fcce967625
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82746545"
---
# <a name="keys-collection-adox"></a>Keys 集合 (ADOX)
包含[資料表](../../../ado/reference/adox-api/table-object-adox.md)的所有索引[鍵](../../../ado/reference/adox-api/key-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 索引[鍵集合](../../../ado/reference/adox-api/keys-collection-adox.md)的[APPEND](../../../ado/reference/adox-api/append-method-adox-keys.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用[Append](../../../ado/reference/adox-api/append-method-adox-keys.md)方法，將新的索引鍵新增至集合。  
  
 其餘的屬性和方法都是 ADO 集合的標準。 您可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)屬性來存取集合中的索引鍵。  
  
-   傳回包含在集合中具有[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性的索引鍵數目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法從集合中移除索引鍵。  
  
-   更新集合中的物件，以使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法來反映目前資料庫的架構。  
  
 本章節包含下列主題。  
  
-   [Indexes 集合屬性、方法和事件](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Keys 集合屬性、方法和事件](../../../ado/reference/adox-api/keys-collection-properties-methods-and-events.md)   
 [Key 物件 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
