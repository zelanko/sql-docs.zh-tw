---
title: 索引物件 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Index
helpviewer_keywords:
- Index object [ADOX]
ms.assetid: 6b9578c0-bc94-46b9-b801-c18e14b04b31
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b6fd63de0b6147b86aa0d6b548669c56aefdcf20
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "66706713"
---
# <a name="index-object-adox"></a>Index 物件 (ADOX)
表示從資料庫資料表的索引。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新**Index**:  
  
```  
Dim obj As New Index  
```  
  
 使用屬性和集合**Index**物件時，您可以：  
  
-   找出與索引[名稱](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   存取資料庫的資料行與索引[資料行](../../../ado/reference/adox-api/columns-collection-adox.md)集合。  
  
-   指定是否必須使用唯一索引鍵[Unique](../../../ado/reference/adox-api/unique-property-adox.md)屬性。  
  
-   指定索引是否具有資料表的主索引鍵[PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md)屬性。  
  
-   指定其索引欄位中具有 null 值的記錄是否擁有與索引項目[IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md)屬性。  
  
-   指定索引是否為叢集使用[Clustered](../../../ado/reference/adox-api/clustered-property-adox.md)屬性。  
  
-   存取使用的提供者特有的索引屬性[屬性](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  將附加時，會發生錯誤[資料行](../../../ado/reference/adox-api/column-object-adox.md)要**資料行**集合**索引**如果**資料行**不存在於[表格](../../../ado/reference/adox-api/table-object-adox.md)已經附加至物件[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合。  
  
> [!NOTE]
>  您的資料提供者可能不支援的所有屬性**Index**物件。 如果您已設定提供者不支援屬性的值，就會發生錯誤。 對新**Index**物件，該物件會附加至集合時，會發生錯誤。 對於現有的物件，設定的屬性時，會發生錯誤。  
  
> [!NOTE]
>  建立時**Index**物件時，適當的預設值的選擇性屬性是否存在並不保證您的提供者支援的屬性。 如需哪一個屬性提供者所支援的詳細資訊，請參閱您的提供者文件。  
  
 本章節包含下列主題。  
  
-   [Index 物件屬性、方法和事件](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Indexes Append 方法範例 (VB)](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [IndexNulls 屬性範例 (VB)](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 和 Unique 屬性範例 (VB)](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [SortOrder 屬性範例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Indexes 集合 (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
