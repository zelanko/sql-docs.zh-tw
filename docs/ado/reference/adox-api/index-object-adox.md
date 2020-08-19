---
description: Index 物件 (ADOX)
title: " (ADOX) 的索引物件 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 81f0bf8d07bbb89105a0ceab421d8433d52f1672
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439940"
---
# <a name="index-object-adox"></a>Index 物件 (ADOX)
表示資料庫資料表中的索引。  
  
## <a name="remarks"></a>備註  
 下列程式碼會建立新的 **索引**：  
  
```  
Dim obj As New Index  
```  
  
 利用 **Index** 物件的屬性和集合，您可以：  
  
-   使用 [Name](../../../ado/reference/adox-api/name-property-adox.md) 屬性來識別索引。  
  
-   使用資料 [行](../../../ado/reference/adox-api/columns-collection-adox.md) 集合存取索引的資料庫資料行。  
  
-   指定索引鍵是否必須[是唯一的唯一屬性。](../../../ado/reference/adox-api/unique-property-adox.md)  
  
-   指定索引是否為具有 [PrimaryKey](../../../ado/reference/adox-api/primarykey-property-adox.md) 屬性之資料表的主鍵。  
  
-   指定索引欄位中具有 null 值的記錄是否具有具有 [IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md) 屬性的索引項目。  
  
-   指定索引是否使用 [叢集屬性進行](../../../ado/reference/adox-api/clustered-property-adox.md) 叢集處理。  
  
-   使用 [屬性](../../../ado/reference/ado-api/properties-collection-ado.md) 集合存取提供者特定的索引屬性。  
  
> [!NOTE]
>  如果**資料行不**存在於已附加至[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)集合的[資料表](../../../ado/reference/adox-api/table-object-adox.md)物件中，則將資料[行](../../../ado/reference/adox-api/column-object-adox.md)附加至**索引**的資料**行**集合時，將會發生錯誤。  
  
> [!NOTE]
>  您的資料提供者可能不支援 **索引** 物件的所有屬性。 如果您已設定提供者不支援的屬性值，就會發生錯誤。 若為新的 **索引** 物件，當物件附加至集合時，就會發生此錯誤。 針對現有的物件，設定屬性時將會發生錯誤。  
  
> [!NOTE]
>  建立 **索引** 物件時，選擇性屬性的適當預設值是否存在，不保證您的提供者支援此屬性。 如需提供者所支援之屬性的詳細資訊，請參閱您的提供者檔。  
  
 本節包含下列主題。  
  
-   [Index 物件屬性、方法和事件](../../../ado/reference/adox-api/index-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [ (VB 的索引附加方法範例) ](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [ (VB) 的 IndexNulls 屬性範例 ](../../../ado/reference/adox-api/indexnulls-property-example-vb.md)   
 [PrimaryKey 和 Unique 屬性範例 (VB) ](../../../ado/reference/adox-api/primarykey-and-unique-properties-example-vb.md)   
 [ (VB) 的 SortOrder 屬性範例 ](../../../ado/reference/adox-api/sortorder-property-example-vb.md)   
 [資料行集合 (ADOX) ](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [ (ADOX) 的索引集合 ](../../../ado/reference/adox-api/indexes-collection-adox.md)   
 [Properties 集合 (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
