---
description: Column 物件 (ADOX)
title: 資料行物件 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: f620dd4c8c8c5b3e00c8875b18686259d71429d7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771117"
---
# <a name="column-object-adox"></a>Column 物件 (ADOX)
表示來自資料表、索引或索引鍵的資料行。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新的資料 **行**：  
  
 `Dim obj As New Column`  
  
 使用資料 **行** 物件的屬性和集合，您可以：  
  
-   使用 [Name 屬性 (ADOX) ](./name-property-adox.md) 屬性來識別資料行。  
  
-   使用 [Type 屬性 (索引鍵)  (ADOX) ](./type-property-key-adox.md) 屬性來指定資料行的資料類型。  
  
-   判斷資料行是否為固定長度，或是否可包含 [屬性屬性 (ADOX) ](./attributes-property-adox.md) 屬性的 null 值。  
  
-   使用 [DefinedSize 屬性 (ADOX) ](./definedsize-property-adox.md) 屬性來指定資料行的大小上限。  
  
-   若為數值資料值，請使用 NumericScale 屬性指定小數位數 [ (ADOX) ](./numericscale-property-adox.md) 屬性。  
  
-   若為數值資料值，請使用 [Precision 屬性 (ADOX) ](./precision-property-adox.md) 屬性來指定最大有效位數。  
  
-   指定 [ (adox) 的目錄物件 ](./catalog-object-adox.md) ，其擁有具有 [PARENTCATALOG 屬性 (ADOX) ](./parentcatalog-property-adox.md) 屬性的資料行。  
  
-   針對索引鍵資料行，請使用 RelatedColumn 屬性，在相關資料表中指定相關資料行的名稱 [ (ADOX) ](./relatedcolumn-property-adox.md) 屬性。  
  
-   針對 [索引資料行]，指定排序次序是以 [SortOrder] 屬性為 [遞增] 或 [遞減] [ (ADOX) ](./sortorder-property-adox.md) 屬性。  
  
-   使用 [ (ADO) 集合的屬性集合 ](../ado-api/properties-collection-ado.md) 來存取提供者特有的屬性。  
  
> [!NOTE]
>  您的資料提供者可能不支援資料 **行** 物件的所有屬性。 如果您已針對提供者不支援的屬性設定值，就會發生錯誤。 若為新的資料 **行** 物件，當物件附加至集合時，就會發生此錯誤。 針對現有的物件，設定屬性時將會發生錯誤。  
>   
>  建立資料 **行** 物件時，選擇性屬性的適當預設值是否存在，並不保證您的提供者支援此屬性。 如需提供者所支援之屬性的詳細資訊，請參閱您的提供者檔。  
  
 本節包含下列主題。  
  
-   [Column 物件屬性、方法和事件](./column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](./columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例 (VB) ](./connection-close-method-table-type-property-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 程式碼範例： NumericScale 和 Precision 屬性範例 (VB) ](./adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](./parentcatalog-property-example-vb.md)   
 [ (VB) 的 SortOrder 屬性範例 ](./sortorder-property-example-vb.md)   
 [資料行集合 (ADOX) ](./columns-collection-adox.md)   
 [Properties 集合 (ADO)](../ado-api/properties-collection-ado.md)