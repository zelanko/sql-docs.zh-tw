---
title: 資料表集合 (ADOX) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965137"
---
# <a name="tables-collection-adox"></a>Tables 集合 (ADOX)
包含所有[資料表](../../../ado/reference/adox-api/table-object-adox.md)的目錄物件。  
  
## <a name="remarks"></a>備註  
 [Append](../../../ado/reference/adox-api/append-method-adox-tables.md)方法**資料表**集合都是唯一的 ADOX。 您可以：  
  
-   將新的資料表加入至集合**Append**方法。  
  
 其餘的屬性和方法是標準的 ADO 集合。 您可以：  
  
-   存取集合中具有資料表[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回與集合中包含的資料表數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合中移除資料表[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映與目前的資料庫結構描述集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 某些提供者可能會傳回其他的結構描述物件，例如檢視中，在**資料表**集合。 因此，有些 ADOX 集合可能包含多個參考相同的物件。 您應該從一個集合中刪除物件，變更將不會顯示在另一個集合的參考已刪除的物件，直到**重新整理**集合上呼叫方法。 例如，使用 OLE DB Provider for Microsoft Jet，檢視會傳回與**資料表**集合。 如果您卸除檢視時，您必須重新整理**資料表**集合將會反映變更之前的集合。  
  
 本章節包含下列主題。  
  
-   [Tables 集合屬性、方法和事件](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog ActiveConnection 屬性範例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns 和 Tables Append 方法、 Name 屬性範例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、 Table Type 屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 方法、 索引鍵的型別、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Catalog 物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
