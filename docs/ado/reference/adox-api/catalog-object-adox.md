---
description: Catalog 物件 (ADOX)
title: " (ADOX) 的目錄物件 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: rothja
ms.author: jroth
ms.openlocfilehash: 8329c4a94a6c9e01f0730b3244eabc6c74511cfa
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985309"
---
# <a name="catalog-object-adox"></a>Catalog 物件 (ADOX)
包含 ([資料表](./tables-collection-adox.md)、 [視圖](./views-collection-adox.md)、 [使用者](./users-collection-adox.md)、 [群組](./groups-collection-adox.md)和 [程式](./procedures-collection-adox.md) 的集合，) 描述資料來源的架構目錄。  
  
## <a name="remarks"></a>備註  
 您可以藉由新增或移除物件，或修改現有的物件來修改 **目錄** 物件。 某些提供者可能不支援所有的 **目錄** 物件，或可能只支援查看架構資訊。  
  
 使用 **目錄** 物件的屬性和方法，您可以：  
  
-   將 [ActiveConnection](./activeconnection-property-adox.md) 屬性設定為 ADO [連接](../ado-api/connection-object-ado.md) 物件或有效的連接字串，以開啟目錄。  
  
-   使用 [create](./create-method-adox.md) 方法建立新的目錄。  
  
-   使用[GetObjectOwner](./getobjectowner-method-adox.md)和[SetObjectOwner](./setobjectowner-method.md)方法，判斷**目錄**中物件的擁有者。  
  
 本節包含下列主題。  
  
-   [Catalog 物件屬性、方法和事件](./catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄 ActiveConnection 屬性範例 (VB) ](./catalog-activeconnection-property-example-vb.md)   
 [命令和 CommandText 屬性範例 (VB) ](./command-and-commandtext-properties-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例 (VB) ](./connection-close-method-table-type-property-example-vb.md)   
 [ (VB) 建立方法範例 ](./create-method-example-vb.md)   
 [Keys 附加方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例 (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters 集合、Command 屬性範例 (VB) ](./parameters-collection-command-property-example-vb.md)   
 [ (VB) 的 ParentCatalog 屬性範例 ](./parentcatalog-property-example-vb.md)   
 [程式附加方法範例 (VB) ](./procedures-append-method-example-vb.md)   
 [程式 Delete 方法範例 (VB) ](./procedures-delete-method-example-vb.md)   
 [程式 Refresh 方法範例 (VB) ](./procedures-refresh-method-example-vb.md)   
 [Views 和 Fields 集合範例 (VB) ](./views-and-fields-collections-example-vb.md)   
 [Views 附加方法範例 (VB) ](./views-append-method-example-vb.md)   
 [Views 集合、CommandText 屬性範例 (VB) ](./views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例 (VB) ](./views-delete-method-example-vb.md)   
 [Views Refresh 方法範例 (VB) ](./views-refresh-method-example-vb.md)   
 [群組集合 (ADOX) ](./groups-collection-adox.md)   
 [程式集合 (ADOX) ](./procedures-collection-adox.md)   
 [資料表集合 (ADOX) ](./tables-collection-adox.md)   
 [使用者集合 (ADOX) ](./users-collection-adox.md)   
 [Views 集合 (ADOX)](./views-collection-adox.md)