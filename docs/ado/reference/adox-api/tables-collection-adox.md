---
title: 資料表集合 (ADOX) |Microsoft 文件
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Tables
- Tables
helpviewer_keywords:
- Tables collection [ADOX]
ms.assetid: 38d750e7-f3fb-426e-b4b4-55eea4f1a654
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87e78e81a7e3885c78d7d30bbfdff732b5de5920
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/18/2018
---
# <a name="tables-collection-adox"></a>資料表集合 (ADOX)
包含所有[資料表](../../../ado/reference/adox-api/table-object-adox.md)的目錄物件。  
  
## <a name="remarks"></a>備註  
 [附加](../../../ado/reference/adox-api/append-method-adox-tables.md)方法**資料表**集合都是唯一的 ADOX。 您可以：  
  
-   將新資料表加入至集合，**附加**方法。  
  
 是標準，以 ADO 集合其餘的屬性和方法。 您可以：  
  
-   存取集合中具有資料表[項目](../../../ado/reference/ado-api/item-property-ado.md)屬性。  
  
-   傳回集合中包含的資料表數目[計數](../../../ado/reference/ado-api/count-property-ado.md)屬性。  
  
-   從集合中移除資料表[刪除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法。  
  
-   更新以反映目前的資料庫結構描述與集合中的物件[重新整理](../../../ado/reference/ado-api/refresh-method-ado.md)方法。  
  
 某些提供者可能會傳回其他結構描述物件，例如檢視**資料表**集合。 因此，有些 ADOX 集合可能包含多個參考相同的物件。 您應該從一個集合中刪除物件，該變更將不會顯示在另一個集合，其參考已刪除的物件直到**重新整理**集合上呼叫方法。 例如，使用 OLE DB Provider for Microsoft Jet，檢視會傳回與**資料表**集合。 如果您卸除檢視時，您必須重新整理**資料表**集合會反映變更之前的集合。  
  
 本章節包含下列主題。  
  
-   [Tables 集合屬性、方法和事件](../../../ado/reference/adox-api/tables-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄 ActiveConnection 屬性範例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [資料行和資料表附加名稱屬性範例 (VB) 方法](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [連接關閉方法，資料表類型屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [Table 物件 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)
