---
title: 索引物件 (ADOX) |Microsoft 文件
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a8e5398c07a4abc449974dd890820ab7195830c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="index-object-adox"></a>索引物件 (ADOX)
代表資料庫資料表中的索引。  
  
## <a name="remarks"></a>備註  
 下列程式碼建立新**索引**:  
  
```  
Dim obj As New Index  
```  
  
 與屬性和集合**索引**物件，您可以：  
  
-   識別具有索引[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   存取資料庫的資料行與索引[資料行](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   指定索引鍵是否必須是唯一的[Unique](../../../ado/reference/adox-api/unique-property-adox.md)屬性。  
  
-   指定索引是否是與資料表的主索引鍵[PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md)屬性。  
  
-   指定其索引欄位中具有 null 值的記錄是否有索引的項目[IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md)屬性。  
  
-   指定索引是否叢集與[Clustered](../../../ado/reference/adox-api/clustered-property-adox.md)屬性。  
  
-   存取提供者特有的索引屬性與[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  當附加時，會發生錯誤[資料行](../../../ado/reference/adox-api/column-object-adox.md)至**資料行**集合**索引**如果**資料行**不存在於[資料表](../../../ado/reference/adox-api/table-object-adox.md)物件已經附加至[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
> [!NOTE]
>  您的資料提供者可能不支援的所有屬性**索引**物件。 如果您已設定提供者不支援屬性的值，就會發生錯誤。 對於新**索引**物件，該物件附加至集合時，會發生錯誤。 對於現有的物件，設定的屬性時，會發生錯誤。  
  
> [!NOTE]
>  建立時**索引**物件的適當預設值是選擇性的屬性是否存在並不保證您的提供者支援屬性。 如需哪一個屬性提供者所支援的詳細資訊，請參閱您的提供者文件。  
  
 本章節包含下列主題。  
  
-   [Index 物件屬性、方法和事件](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [索引附加方法範例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 屬性範例 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 和獨有的內容範例 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 屬性範例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
