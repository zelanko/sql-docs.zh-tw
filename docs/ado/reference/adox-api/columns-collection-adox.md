---
title: Columns 集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index::Columns
- Table::Columns
- Key::Columns
- Columns
helpviewer_keywords:
- Columns collection [ADOX]
ms.assetid: 23b9fea8-4f76-4a51-95ce-1a6ce4560b34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bc3686ac69d7afeeebec14939a42e073f796b1ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67966849"
---
# <a name="columns-collection-adox"></a>Columns 集合 (ADOX)
包含資料表、索引或索引鍵的所有資料[行](../../../ado/reference/adox-api/column-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 資料**行**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-columns.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用**Append**方法，將新的資料行加入至集合。  
  
 其餘的屬性和方法都是 ADO 集合的標準。 您可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)屬性存取集合中的資料行。  
  
-   傳回具有[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性之集合中包含的資料行數目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法，從集合中移除資料行。  
  
-   更新集合中的物件，以使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法來反映目前資料庫的架構。  
  
> [!NOTE]
>  如果**資料行不**存在於已附加至[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合的[資料表](../../../ado/reference/adox-api/table-object-adox.md)中，將**資料行附加至**[索引](../../../ado/reference/adox-api/index-object-adox.md)的資料**行**集合時，將會發生錯誤。  
  
 本章節包含下列主題。  
  
-   [Columns 集合屬性、方法和事件](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 屬性範例（VB）](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
