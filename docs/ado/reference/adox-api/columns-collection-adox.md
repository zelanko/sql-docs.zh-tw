---
description: Columns 集合 (ADOX)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c0e37715077af500e0c5cc023021765a9e4978d
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770977"
---
# <a name="columns-collection-adox"></a>Columns 集合 (ADOX)
包含資料表、索引或索引鍵的所有資料 [行](./column-object-adox.md) 物件。  
  
## <a name="remarks"></a>備註  
 資料**行**集合的[APPEND](./append-method-adox-columns.md)方法對於 ADOX 而言是唯一的。 您可以：  
  
-   使用 **Append** 方法將新的資料行新增至集合。  
  
 其餘的屬性和方法是 ADO 集合的標準。 您可以：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 屬性存取集合中的資料行。  
  
-   傳回集合中包含 [Count](../ado-api/count-property-ado.md) 屬性的資料行數目。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法，從集合中移除資料行。  
  
-   使用 [Refresh](../ado-api/refresh-method-ado.md) 方法更新集合中的物件，以反映目前資料庫的架構。  
  
> [!NOTE]
>  如果資料行不存在於已附加至[資料表](./tables-collection-adox.md)集合的[資料表](./table-object-adox.md)中，將資料**行**附加至[索引](./index-object-adox.md)的資料**行**集合**時，將**會發生錯誤。  
  
 本節包含下列主題。  
  
-   [Columns 集合屬性、方法和事件](./columns-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例 (VB) ](./connection-close-method-table-type-property-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](./parentcatalog-property-example-vb.md)   
 [ (VB) 的 SortOrder 屬性範例 ](./sortorder-property-example-vb.md)   
 [Column 物件 (ADOX)](./column-object-adox.md)