---
title: Catalog 物件 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5547090443e2f22a135234853b76480fb8295e14
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634416"
---
# <a name="catalog-object-adox"></a>Catalog 物件 (ADOX)
包含集合 ([資料表](../../../ado/reference/adox-api/tables-collection-adox.md)，[檢視](../../../ado/reference/adox-api/views-collection-adox.md)，[使用者](../../../ado/reference/adox-api/users-collection-adox.md)，[群組](../../../ado/reference/adox-api/groups-collection-adox.md)，以及[程序](../../../ado/reference/adox-api/procedures-collection-adox.md))，說明資料來源的結構描述目錄。  
  
## <a name="remarks"></a>備註  
 您可以修改**目錄**物件藉由新增或移除物件，或藉由修改現有的物件。 某些提供者可能不支援的所有**目錄**物件，或只檢視結構描述資訊可能會支援。  
  
 使用屬性和方法**目錄**物件時，您可以：  
  
-   藉由設定開啟類別目錄[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)屬性，以 ADO[連線](../../../ado/reference/ado-api/connection-object-ado.md)物件或有效的連接字串。  
  
-   建立與新的目錄[建立](../../../ado/reference/adox-api/create-method-adox.md)方法。  
  
-   判斷在物件的擁有者**類別目錄**具有[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)並[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法。  
  
 本章節包含下列主題。  
  
-   [Catalog 物件屬性、方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog ActiveConnection 屬性範例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Command 和 CommandText 屬性範例 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Connection Close 方法、 Table Type 屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create 方法範例 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Keys Append 方法、 索引鍵的型別、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters 集合、 Command 屬性範例 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [Procedures Append 方法範例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [Procedures Delete 方法範例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [Procedures Refresh 方法範例 (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [檢視和 Fields 集合範例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 方法範例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合、 CommandText 屬性範例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views Refresh 方法範例 (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [Procedures 集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Tables 集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Users 集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
