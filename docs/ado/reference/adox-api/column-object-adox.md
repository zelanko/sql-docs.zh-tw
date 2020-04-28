---
title: Column 物件（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db2c2dbe6af2a50fc2507a9ade92d83e0502f2ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966917"
---
# <a name="column-object-adox"></a>Column 物件 (ADOX)
表示資料表、索引或索引鍵中的資料行。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新的資料**行**：  
  
 `Dim obj As New Column`  
  
 使用資料**行**物件的屬性和集合，您可以：  
  
-   識別具有[Name 屬性（ADOX）](../../../ado/reference/adox-api/name-property-adox.md)屬性的資料行。  
  
-   使用[Type 屬性（Key）（ADOX）](../../../ado/reference/adox-api/type-property-key-adox.md)屬性指定資料行的資料類型。  
  
-   判斷資料行是否為固定長度，或是否可以包含具有[Attributes 屬性（ADOX）](../../../ado/reference/adox-api/attributes-property-adox.md)屬性的 null 值。  
  
-   使用[DefinedSize 屬性（ADOX）](../../../ado/reference/adox-api/definedsize-property-adox.md)屬性指定資料行的大小上限。  
  
-   若為數值資料值，請使用[NumericScale 屬性（ADOX）](../../../ado/reference/adox-api/numericscale-property-adox.md)屬性指定小數位數值。  
  
-   針對數值資料值，使用[Precision 屬性（ADOX）](../../../ado/reference/adox-api/precision-property-adox.md)屬性指定最大有效位數。  
  
-   指定擁有具有[ParentCatalog 屬性（adox）](../../../ado/reference/adox-api/parentcatalog-property-adox.md)屬性之資料行的[目錄物件（adox）](../../../ado/reference/adox-api/catalog-object-adox.md) 。  
  
-   針對 [索引鍵資料行]，使用[RelatedColumn 屬性（ADOX）](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)屬性指定相關資料表中相關資料行的名稱。  
  
-   針對 [索引資料行]，使用 [ [SortOrder 屬性（ADOX）](../../../ado/reference/adox-api/sortorder-property-adox.md) ] 屬性指定排序次序為 [遞增] 或 [遞減]。  
  
-   使用[屬性集合（ADO）](../../../ado/reference/ado-api/properties-collection-ado.md)集合存取提供者特定的屬性。  
  
> [!NOTE]
>  並非資料**行**物件的所有屬性都可由您的資料提供者支援。 如果您已設定提供者不支援之屬性的值，就會發生錯誤。 針對新的資料**行**物件，當物件附加至集合時，就會發生此錯誤。 針對現有的物件，設定屬性時將會發生此錯誤。  
>   
>  建立資料**行**物件時，選擇性屬性的適當預設值是否存在，並不保證您的提供者支援屬性。 如需提供者所支援之屬性的詳細資訊，請參閱您的提供者檔。  
  
 本章節包含下列主題。  
  
-   [Column 物件屬性、方法和事件](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例（VB）](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 程式碼範例： NumericScale 和 Precision 屬性範例（VB）](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog 屬性範例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 屬性範例（VB）](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [Columns 集合（ADOX）](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
