---
title: 資料行集合 (ADOX) |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67966849"
---
# <a name="columns-collection-adox"></a>Columns 集合 (ADOX)
包含所有[資料行](../../../ado/reference/adox-api/column-object-adox.md)資料表、 索引或索引鍵的物件。  
  
## <a name="remarks"></a>備註  
 [Append](../../../ado/reference/adox-api/append-method-adox-columns.md)方法**資料行**集合都是唯一的 ADOX。 您可以：  
  
-   將新的資料行加入至集合**Append**方法。  
  
 其餘的屬性和方法是標準的 ADO 集合。 您可以：  
  
-   存取集合中具有資料行[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回集合中具有包含資料行數[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合移除資料行[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映目前的資料庫結構描述集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
> [!NOTE]
>  將附加時，會發生錯誤**資料行**要**資料行**集合[索引](../../../ado/reference/adox-api/index-object-adox.md)如果**資料行**不存在於[表格](../../../ado/reference/adox-api/table-object-adox.md)已經附加至[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
 本章節包含下列主題。  
  
-   [Columns 集合屬性、方法和事件](../../../ado/reference/adox-api/columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、 Name 屬性範例 (VB)](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、 Table Type 屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 方法、 索引鍵的型別、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 屬性範例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Column 物件 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)
