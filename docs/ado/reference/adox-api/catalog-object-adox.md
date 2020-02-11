---
title: Catalog 物件（ADOX） |Microsoft Docs
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
ms.openlocfilehash: f9843ad9ac0a456f7e38e741e08ce9b66f862fd9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967050"
---
# <a name="catalog-object-adox"></a>Catalog 物件 (ADOX)
包含描述資料來源之架構目錄的集合（[資料表](../../../ado/reference/adox-api/tables-collection-adox.md)、[視圖](../../../ado/reference/adox-api/views-collection-adox.md)、[使用者](../../../ado/reference/adox-api/users-collection-adox.md)、[群組](../../../ado/reference/adox-api/groups-collection-adox.md)和[程式](../../../ado/reference/adox-api/procedures-collection-adox.md)）。  
  
## <a name="remarks"></a>備註  
 您可以藉由新增或移除物件，或藉由修改現有的物件來修改**類別目錄**物件。 某些提供者可能不支援所有的**目錄**物件，或只支援流覽架構資訊。  
  
 使用**目錄**物件的屬性和方法，您可以：  
  
-   將[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)屬性設定為 ADO[連接](../../../ado/reference/ado-api/connection-object-ado.md)物件或有效的連接字串，以開啟目錄。  
  
-   使用[create](../../../ado/reference/adox-api/create-method-adox.md)方法建立新的目錄。  
  
-   使用[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)和[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法，判斷**目錄**中物件的擁有者。  
  
 本章節包含下列主題。  
  
-   [Catalog 物件屬性、方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另請參閱  
 [Catalog ActiveConnection 屬性範例（VB）](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Command 和 CommandText 屬性範例（VB）](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [Connection Close 方法、Table Type 屬性範例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create 方法範例（VB）](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [Keys Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 屬性範例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters 集合、Command 屬性範例（VB）](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 屬性範例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [程式 Append 方法範例（VB）](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [程式 Delete 方法範例（VB）](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [程式 Refresh 方法範例（VB）](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [Views 和 Fields 集合範例（VB）](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 方法範例（VB）](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合、CommandText 屬性範例（VB）](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法範例（VB）](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views Refresh 方法範例（VB）](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [Groups 集合（ADOX）](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [程式集合（ADOX）](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Tables 集合（ADOX）](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [Users 集合（ADOX）](../../../ado/reference/adox-api/users-collection-adox.md)   
 [Views 集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
