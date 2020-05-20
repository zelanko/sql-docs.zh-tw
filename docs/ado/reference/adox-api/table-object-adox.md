---
title: Table 物件（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table
helpviewer_keywords:
- Table object [ADOX]
ms.assetid: a6d74000-0828-49ba-850a-63da865f8802
author: rothja
ms.author: jroth
ms.openlocfilehash: bcebe14b7b989e584539dd3f92fd8ea676ebd48a
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763299"
---
# <a name="table-object-adox"></a>Table 物件 (ADOX)
表示資料庫資料表，包括資料行、索引和索引鍵。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新的**資料表**：  
  
```  
Dim obj As New Table  
```  
  
 使用**Table**物件的屬性和集合，您可以：  
  
-   識別具有[Name 屬性（ADOX）](../../../ado/reference/adox-api/name-property-adox.md)屬性的資料表。  
  
-   使用[Type 屬性（table）（ADOX）](../../../ado/reference/adox-api/type-property-table-adox.md)屬性判斷資料表的類型。  
  
-   使用[Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)集合來存取資料表的資料庫資料行。  
  
-   使用[索引集合（ADOX）](../../../ado/reference/adox-api/indexes-collection-adox.md)存取資料表的索引。  
  
-   使用[Keys 集合（ADOX）](../../../ado/reference/adox-api/keys-collection-adox.md)存取資料表的索引鍵。  
  
-   指定擁有具有[ParentCatalog 屬性（ADOX）](../../../ado/reference/adox-api/parentcatalog-property-adox.md)屬性之資料表的目錄。  
  
-   傳回具有[DateCreated 屬性（adox）](../../../ado/reference/adox-api/datecreated-property-adox.md)和[DATEMODIFIED 屬性（adox）](../../../ado/reference/adox-api/datemodified-property-adox.md)屬性的日期資訊。  
  
-   使用[屬性集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)集合存取提供者特定的資料表屬性。  
  
> [!NOTE]
>  您的資料提供者可能不支援**資料表**物件的所有屬性。 如果您已設定提供者不支援之屬性的值，就會發生錯誤。 針對新的**Table**物件，當物件附加至集合時，就會發生錯誤。 針對現有的物件，設定屬性時將會發生此錯誤。  
>   
>  建立**資料表**物件時，選擇性屬性的適當預設值是否存在，並不保證您的提供者支援屬性。 如需提供者所支援之屬性的詳細資訊，請參閱您的提供者檔。  
  
 本章節包含下列主題。  
  
-   [Table 物件屬性、方法和事件](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog ActiveConnection 屬性範例（VB）](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns 和 Tables Append 方法、Name 屬性範例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 屬性範例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [索引集合（ADOX）](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Keys 集合（ADOX）](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Properties 集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
