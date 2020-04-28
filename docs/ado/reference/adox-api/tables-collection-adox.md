---
title: Tables 集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0bf28af10084a30a5c81c76fe7e44781178979ad
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965137"
---
# <a name="tables-collection-adox"></a>Tables 集合 (ADOX)
包含目錄的所有[資料表](../../../ado/reference/adox-api/table-object-adox.md)物件。  
  
## <a name="remarks"></a>備註  
 **資料表**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-tables.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用**Append**方法，將新的資料表加入至集合。  
  
 其餘的屬性和方法都是 ADO 集合的標準。 您可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)屬性存取集合中的資料表。  
  
-   使用[Count](../../../ado/reference/ado-api/count-property-ado.md)屬性傳回包含在集合中的資料表數目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法，從集合中移除資料表。  
  
-   更新集合中的物件，以使用[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法來反映目前的資料庫架構。  
  
 某些提供者可能會在**Tables**集合中傳回其他架構物件（例如 view）。 因此，某些 ADOX 集合可能包含相同物件的多個參考。 如果您要從一個集合中刪除物件，變更將不會顯示在另一個參考已刪除物件的集合中，直到在集合上呼叫**Refresh**方法為止。 例如，使用 Microsoft Jet 的 OLE DB 提供者時，會使用**Tables**集合傳回 views。 如果您卸載某個視圖，您必須重新整理**Tables**集合，集合才會反映該變更。  
  
 本章節包含下列主題。  
  
-   [Tables 集合屬性、方法和事件](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog ActiveConnection 屬性範例（VB）](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns 和 Tables Append 方法、Name 屬性範例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Catalog 物件（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
