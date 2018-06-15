---
title: 資料表物件 (ADOX) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17a34c8e53bba7cdb67024b83a8758900d8f6183
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/11/2018
ms.locfileid: "35286821"
---
# <a name="table-object-adox"></a>Table 物件 (ADOX)
代表資料庫資料表中的資料行、 索引和索引鍵。  
  
## <a name="remarks"></a>備註  
 下列程式碼建立新**資料表**:  
  
```  
Dim obj As New Table  
```  
  
 與屬性和集合**資料表**物件，您可以：  
  
-   識別具有資料表[名稱屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   決定資料表類型[Type 屬性 （資料表） (ADOX)](../../../ado/reference/adox-api/type-property-table-adox.md)屬性。  
  
-   存取資料庫資料行的資料表具有[資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   存取與資料表的索引[索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)。  
  
-   存取與資料表的索引鍵[索引鍵集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)。  
  
-   指定擁有與該資料表的類別目錄[ParentCatalog 屬性 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)屬性。  
  
-   傳回日期資訊與[DateCreated 屬性 (ADOX)](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DateModified 屬性 (ADOX)](../../../ado/reference/adox-api/datemodified-property-adox.md)屬性。  
  
-   存取與提供者特定資料表屬性[屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  您的資料提供者可能不支援的所有屬性**資料表**物件。 如果您已設定提供者不支援屬性的值，就會發生錯誤。 對於新**資料表**物件，該物件附加至集合時，會發生錯誤。 對於現有的物件，設定的屬性時，會發生錯誤。  
>   
>  建立時**資料表**物件的適當預設值是選擇性的屬性是否存在並不保證您的提供者支援屬性。 如需哪一個屬性提供者所支援的詳細資訊，請參閱您的提供者文件。  
  
 本章節包含下列主題。  
  
-   [Table 物件屬性、方法和事件](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄 ActiveConnection 屬性範例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [資料行和資料表附加名稱屬性範例 (VB) 方法](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [連接關閉方法，資料表類型屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [索引鍵集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
