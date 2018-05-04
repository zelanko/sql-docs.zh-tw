---
title: XSD 註解 (SQLXML 4.0) |Microsoft 文件
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a7ef117b5abccb1e7e860d0bebafa8f4239e01da
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 註解 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  下表列出 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中推出的 XSD 註解，並與 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中推出的 XDR 註解相比較。  
  
|XSD 註解|Description|主題連結|XDR 註解|  
|--------------------|-----------------|----------------|--------------------|  
|**sql:encode**|當 XML 元素或屬性對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 資料行時，允許要求參考 URI。 此 URI 稍後可用於傳回 BLOB 資料。|[要求的 URL 參考 BLOB 資料使用 sql： 編碼&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|**url-encode**|  
|**sql:guid**|可讓您指定要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的 GUID 值，還是使用 Updategram 中針對該資料行提供的值。|[使用 sql:identity 和 sql:guid 註解](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|不支援|  
|**sql:hide**|在產生的 XML 文件中，隱藏結構描述中指定的元素或屬性。|[使用 sql:hide 來隱藏項目和屬性](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)|不支援|  
|**sql:identity**|可以在對應到 IDENTITY 類型之資料庫資料行的任何節點上指定。 針對此註解指定的值會定義如何更新資料庫中對應的 IDENTITY 類型資料行。|[使用 sql:identity 和 sql:guid 註解](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)|不支援|  
|**sql:inverse**|指引 updategram 邏輯反轉使用指定的父子式關聯性的解譯 **\<sql: relationship >**。|[Sql: relationship 指定 sql: inverse 屬性&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|不支援|  
|**sql:is-constant**|建立不對應到任何資料表的 XML 元素。 該元素會出現在查詢輸出中。|[建立常數元素使用 sql: is-constant< &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|相同|  
|**sql:key-fields**|可用來指定一或多個資料行，以用來唯一識別資料表中的資料列。|[識別索引鍵資料行使用 sql: key-fields-欄位&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|相同|  
|**sql:limit-field**<br /><br /> **sql:limit-value**|可用來限制根據限制值傳回的值。|[篩選值使用 sql: limit-value-欄位和 sql: limit-value-值&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)|相同|  
|**sql:mapped**|可用來將結構描述項目排除在結果之外。|[產生 XML 文件使用的 sql 中排除結構描述項目： 對應&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|**對應欄位**|  
|**sql:max-depth**|可讓您指定結構描述中指定之遞迴關聯性的深度。|[使用 sql:max-depth 來指定遞迴關聯性的深度](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|不支援|  
|**sql:overflow-field**|可識別包含溢位資料的資料庫資料行。|[擷取未耗用資料使用 sql: overflow-field-欄位&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)|相同|  
|**sql:prefix**|建立有效的 XML ID、IDREF 和 IDREFS。 在字串前面加上 ID、IDREF 和 IDREFS 的值。|[建立有效的 ID、 IDREF 和 IDREFS 類型屬性使用 sql: prefix &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|相同|  
|**sql:relationship**|指定 XML 元素之間的關聯性。 **父**，**子**，**父索引鍵**，和**子索引鍵**屬性用來建立關聯性。|[指定關聯性使用 sql: relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|屬性名稱不同：<br /><br /> **索引鍵關聯性**<br /><br /> **foreign-relation**<br /><br /> **索引鍵**<br /><br /> **foreign-key**|  
|**sql:use-cdata**|可用來針對 XML 文件中的特定元素指定要使用的 CDATA 區段。|[建立 CDATA 區段使用 sql: use-cdata-cdata &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|相同|  
  
> [!NOTE]  
>  XSD 原生**targetNamespace**屬性會取代**目標命名空間**中所導入的註解[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]XDR 對應結構描述。  
  
## <a name="see-also"></a>另請參閱  
 [指定目標命名空間使用 targetNamespace 屬性&#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
