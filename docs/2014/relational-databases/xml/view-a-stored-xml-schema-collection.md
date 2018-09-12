---
title: 檢視儲存的 XML 結構描述集合 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- schema collections [SQL Server], viewing
- XML schemas [SQL Server], viewing
- CREATE XML SCHEMA COLLECTION statement
- xml_schema_namespace function
- XML schema collections [SQL Server], viewing
- displaying XML schema collections
- viewing XML schema collections
ms.assetid: e38031af-22df-4cd9-a14e-e316b822f91b
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bbca5b4d378861731b77472c5f88442a3f6e793f
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889854"
---
# <a name="view-a-stored-xml-schema-collection"></a>檢視儲存的 XML 結構描述集合
  使用 [CREATE XML SCHEMA COLLECTION](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)匯入 XML 結構描述集合之後，即會將結構描述元件儲存在中繼資料中。 您可以使用 [xml_schema_namespace](/sql/t-sql/xml/xml-schema-namespace)內建函數以重建 XML 結構描述集合。 此函數會傳回`xml`資料類型執行個體。  
  
 例如，下列查詢會從`ProductDescriptionSchemaCollection`資料庫的生產關聯式結構描述擷取 XML 結構描述集合 ( [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] )。  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 如果您想要查看 XML 結構描述集合只能有一個結構描述，您可以指定針對 XQuery`xml`類型所傳回的結果`xml_schema_namespace`。  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 例如，下列查詢可從 `ProductDescriptionSchemaCollection` XML 結構描述集合擷取產品保證和維護 XML 結構描述資訊。  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 您也可以將選擇性的目標命名空間當做第三個參數傳遞至 `xml_schema_namespace` 函數，以擷取集合中的特定結構描述，如下列查詢所示：  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 當使用資料庫中的 CREATE XML SCHEMA COLLECTION 來建立 XML 結構描述集合時，陳述式會在中繼資料內儲存結構描述元件。 請注意只會儲存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可辨識的結構描述元件。 不會儲存任何註解或非 XSD 屬性。 因此， **xml_schema_namespace** 重新建構的結構描述在功能上等於原始結構描述，但是它看起來不一定相同。 例如，您將看不到與原始結構描述中相同的前置詞。 **xml_schema_namespace** 傳回的結構描述使用 **t** 作為目標命名空間以及其他命名空間 **ns1**、 **ns2**等的前置詞。  
  
 如果您想要保留一份完全相同的 XML 結構描述，您應該將 XML 結構描述儲存在檔案或資料庫資料表的 `xml` 類型資料行中。  
  
 [sys.xml_schema_collections](/sql/relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql) 目錄檢視也會傳回 XML 結構描述集合的資訊。 此資訊包含集合的名稱、建立日期以及集合的擁有者。  
  
## <a name="see-also"></a>另請參閱  
 [XML 結構描述集合 &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)  
  
  
