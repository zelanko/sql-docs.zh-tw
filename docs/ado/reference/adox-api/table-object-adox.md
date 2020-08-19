---
description: Table 物件 (ADOX)
title: 資料表物件 (ADOX) |Microsoft Docs
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
ms.openlocfilehash: c9bbf6a33eeb76f406a6fd6dc87ef591a3d4f12a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439480"
---
# <a name="table-object-adox"></a>Table 物件 (ADOX)
表示資料庫資料表，包括資料行、索引和索引鍵。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新的 **資料表**：  
  
```  
Dim obj As New Table  
```  
  
 使用 **資料表** 物件的屬性和集合，您可以：  
  
-   找出 [名稱屬性 (ADOX) ](../../../ado/reference/adox-api/name-property-adox.md) 屬性的資料表。  
  
-   判斷具有 [Type 屬性 (table)  (ADOX) ](../../../ado/reference/adox-api/type-property-table-adox.md) 屬性的資料表類型。  
  
-   使用資料 [行集合 (ADOX) ](../../../ado/reference/adox-api/columns-collection-adox.md) 集合來存取資料表的資料庫資料行。  
  
-   使用 [ (ADOX) 的索引集合 ](../../../ado/reference/adox-api/indexes-collection-adox.md)來存取資料表的索引。  
  
-   使用 [ (ADOX) 的索引鍵集合 ](../../../ado/reference/adox-api/keys-collection-adox.md)來存取資料表的索引鍵。  
  
-   使用 ParentCatalog 屬性指定擁有資料表的目錄， [ (ADOX) ](../../../ado/reference/adox-api/parentcatalog-property-adox.md) 屬性。  
  
-   傳回具有 DateCreated 屬性的日期資訊 [ (adox) ](../../../ado/reference/adox-api/datecreated-property-adox.md) 和 [DATEMODIFIED 屬性 (ADOX) ](../../../ado/reference/adox-api/datemodified-property-adox.md) 屬性。  
  
-   使用 [ (ADO) 集合的屬性集合 ](../../../ado/reference/ado-api/properties-collection-ado.md) 來存取提供者特定的資料表屬性。  
  
> [!NOTE]
>  您的資料提供者可能不支援 **資料表** 物件的所有屬性。 如果您已針對提供者不支援的屬性設定值，就會發生錯誤。 若為新的 **資料表** 物件，當物件附加至集合時，就會發生此錯誤。 針對現有的物件，設定屬性時將會發生錯誤。  
>   
>  建立 **資料表** 物件時，選擇性屬性的適當預設值是否存在，並不保證您的提供者支援此屬性。 如需提供者所支援之屬性的詳細資訊，請參閱您的提供者檔。  
  
 本節包含下列主題。  
  
-   [Table 物件屬性、方法和事件](../../../ado/reference/adox-api/table-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄 ActiveConnection 屬性範例 (VB) ](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Columns 和 Tables Append 方法、Name 屬性範例 (VB) ](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例 (VB) ](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [資料行集合 (ADOX) ](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [ (ADOX) 的索引集合 ](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [ (ADOX) 的索引鍵集合 ](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [ (ADO) 的屬性集合 ](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)
