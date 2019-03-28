---
title: 檢視儲存的 XML 結構描述集合 | Microsoft 文件
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8cde5898fc4c9ae8b71452bfb22ff58e0c3c9725
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536160"
---
# <a name="view-a-stored-xml-schema-collection"></a>檢視儲存的 XML 結構描述集合
  使用 [CREATE XML SCHEMA COLLECTION](/sql/t-sql/statements/create-xml-schema-collection-transact-sql)匯入 XML 結構描述集合之後，即會將結構描述元件儲存在中繼資料中。 您可以使用 [xml_schema_namespace](/sql/t-sql/xml/xml-schema-namespace)內建函數以重建 XML 結構描述集合。 這個函數會傳回 `xml` 資料類型執行個體。  
  
 例如，下列查詢會從`ProductDescriptionSchemaCollection`資料庫的生產關聯式結構描述擷取 XML 結構描述集合 ( [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] )。  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection')  
GO  
```  
  
 如果您只想查看 XML 結構描述集合的一個結構描述，您可以針對 `xml_schema_namespace` 傳回的 `xml` 類型結果指定 XQuery。  
  
```  
SELECT xml_schema_namespace(N'RelationalSchemaName',N'XmlSchemaCollectionName').query('  
/xs:schema[@targetNamespace="TargetNameSpace"]  
')  
GO  
```  
  
 例如，下列查詢可從 `ProductDescriptionSchemaCollection` XML 結構描述集合擷取產品保證和維護 XML 結構描述資訊。  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection').query('  
/xs:schema[@targetNamespace="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"]  
')  
GO  
```  
  
 您也可以將選擇性的目標命名空間當做第三個參數傳遞至 `xml_schema_namespace` 函數，以擷取集合中的特定結構描述，如下列查詢所示：  
  
```  
SELECT xml_schema_namespace(N'Production',N'ProductDescriptionSchemaCollection', N'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain')  
GO  
```  
  
 當使用資料庫中的 CREATE XML SCHEMA COLLECTION 來建立 XML 結構描述集合時，陳述式會在中繼資料內儲存結構描述元件。 請注意只會儲存 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可辨識的結構描述元件。 不會儲存任何註解或非 XSD 屬性。 因此， **xml_schema_namespace** 重新建構的結構描述在功能上等於原始結構描述，但是它看起來不一定相同。 例如，您將看不到與原始結構描述中相同的前置詞。 **xml_schema_namespace** 傳回的結構描述使用 **t** 作為目標命名空間以及其他命名空間 **ns1**、 **ns2**等的前置詞。  
  
 如果您想要保留一份完全相同的 XML 結構描述，您應該將 XML 結構描述儲存在檔案或資料庫資料表的 `xml` 類型資料行中。  
  
 [sys.xml_schema_collections](/sql/relational-databases/system-catalog-views/sys-xml-schema-collections-transact-sql) 目錄檢視也會傳回 XML 結構描述集合的資訊。 此資訊包含集合的名稱、建立日期以及集合的擁有者。  
  
## <a name="see-also"></a>另請參閱  
 [XML 結構描述集合 &#40;SQL Server&#41;](xml-schema-collections-sql-server.md)  
  
  
