---
title: "目錄物件 (ADOX) |Microsoft 文件"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26033bff0a1a88da25ed2eae566ffef49538c35f
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-object-adox"></a>目錄物件 (ADOX)
包含集合 ([資料表](../../../ado/reference/adox-api/tables-collection-adox.md)，[檢視](../../../ado/reference/adox-api/views-collection-adox.md)，[使用者](../../../ado/reference/adox-api/users-collection-adox.md)，[群組](../../../ado/reference/adox-api/groups-collection-adox.md)，和[程序](../../../ado/reference/adox-api/procedures-collection-adox.md))，說明資料來源的結構描述目錄。  
  
## <a name="remarks"></a>備註  
 您可以修改**目錄**物件藉由新增或移除物件或修改現有的物件。 某些提供者可能不支援的所有**目錄**物件，或者可能會支援僅限檢視結構描述資訊。  
  
 屬性和方法**目錄**物件，您可以：  
  
-   藉由設定開啟目錄[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)屬性 ADO[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件或有效的連接字串。  
  
-   建立新的目錄與[建立](../../../ado/reference/adox-api/create-method-adox.md)方法。  
  
-   判斷物件的擁有者**目錄**與[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)和[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法。  
  
 本章節包含下列主題。  
  
-   [目錄物件屬性、 方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [目錄 ActiveConnection 屬性範例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [命令和 CommandText 屬性範例 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [連接關閉方法，資料表類型屬性範例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create 方法範例 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [索引鍵附加方法、 金鑰類型、 RelatedColumn、 RelatedTable 和 UpdateRule 屬性範例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [參數集合中，命令屬性範例 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 屬性範例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [程序附加方法範例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [程序刪除方法的範例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [程序重新整理方法範例 (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [檢視和欄位集合範例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [檢視附加方法範例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [檢視集合，CommandText 屬性範例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [檢視刪除方法的範例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [檢視重新整理方法範例 (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [群組集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [程序集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [資料表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [使用者集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [檢視集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
