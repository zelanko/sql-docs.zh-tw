---
title: "資料行物件 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Column
helpviewer_keywords:
- Column object [ADOX]
ms.assetid: 6e772783-1bc8-4ea7-94b2-7d7a52ea5c47
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a5a8a5047f4cd4655ebe1dd041e44949ca361c54
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="column-object-adox"></a>資料行物件 (ADOX)
從資料表、 索引或索引鍵代表的資料行。  
  
## <a name="remarks"></a>備註  
 下列程式碼建立新**資料行**:  
  
 `Dim obj As New Column`  
  
 與屬性和集合**資料行**物件，您可以：  
  
-   識別具有資料行[名稱屬性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)屬性。  
  
-   指定的資料行的資料型別[Type 屬性 (Key) (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)屬性。  
  
-   判斷是否是固定長度的資料行，或者它可以包含 null 值與[屬性屬性 (ADOX)](../../../ado/reference/adox-api/attributes-property-adox.md)屬性。  
  
-   指定的資料行的大小上限[DefinedSize 屬性 (ADOX)](../../../ado/reference/adox-api/definedsize-property-adox.md)屬性。  
  
-   對於數值資料值，指定縮放比例和[NumericScale 屬性 (ADOX)](../../../ado/reference/adox-api/numericscale-property-adox.md)屬性。  
  
-   數值資料值，指定與最大有效位數[有效位數屬性 (ADOX)](../../../ado/reference/adox-api/precision-property-adox.md)屬性。  
  
-   指定[目錄物件 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)擁有的資料行[ParentCatalog 屬性 (ADOX)](../../../ado/reference/adox-api/parentcatalog-property-adox.md)屬性。  
  
-   索引鍵資料行，指定相關的資料行的名稱與相關的資料表中[RelatedColumn 屬性 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)屬性。  
  
-   索引資料行，指定排序次序為遞增或遞減與[SortOrder 屬性 (ADOX)](../../../ado/reference/adox-api/sortorder-property-adox.md)屬性。  
  
-   存取提供者特有的屬性，與[屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)集合。  
  
> [!NOTE]
>  並非所有的屬性**資料行**物件可能支援的資料提供者。 如果您已設定提供者不支援屬性的值，就會發生錯誤。 對於新**資料行**物件，該物件附加至集合時，會發生錯誤。 對於現有的物件，設定的屬性時，會發生錯誤。  
>   
>  建立時**資料行**物件的適當預設值是選擇性的屬性是否存在並不保證您的提供者支援屬性。 如需哪一個屬性提供者所支援的詳細資訊，請參閱您的提供者文件。  
  
 本章節包含下列主題。  
  
-   [資料行物件屬性、 方法和事件](../../../ado/reference/adox-api/column-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [資料行和資料表附加名稱屬性範例 (VB) 方法](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [連接關閉方法，資料表類型屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ADOX 程式碼範例： NumericScale 和有效位數屬性範例 (VB)](../../../ado/reference/adox-api/adox-code-example-numericscale-and-precision-properties-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [SortOrder 屬性範例 (VB)](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [資料行集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [屬性集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)

