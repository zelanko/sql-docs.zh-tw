---
title: '在 XSD 架構中使用注釋 (SQLXML) '
description: 瞭解如何使用 SQLXML 4.0 中的 XSD 架構語言所支援的注釋，在 XSD 架構中指定 XML 對關聯式的對應。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, about annotated XSD schemas
- annotations [SQLXML]
- relationships [SQLXML]
- relationships [SQLXML], hierarchical relationships
- hierarchical relationships [SQLXML]
- mapping schema [SQLXML], scenarios for using
ms.assetid: 78f318a4-7a36-473b-9852-a4bae6940ce5
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec539fce08e832f2d92032bd48fce76f12ff73e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479329"
---
# <a name="using-annotations-in-xsd-schemas-sqlxml-40"></a>在 XSD 結構描述中使用註釋 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQLXML 4.0 中，XSD 結構描述語言以類似 XML-Data Reduced (XDR) 結構描述語言所推出之註解的方式支援註解。 在 XSD 中有 XDR 不支援的其他註解。  
  
 這些註解可以在 XSD 結構描述內，用於指定 XML 到關聯式的對應。 這包括 XSD 結構描述中的元素和屬性到資料庫中的資料表 (檢視) 和資料行之間的對應。  
  
 如果您沒有指定註解，就會使用預設對應。 根據預設，包含複雜類型的 XSD 元素會對應到指定之資料庫中的資料表 (檢視) 名稱，而包含簡單類型的元素或屬性會對應到具有相同名稱的資料行，做為元素或屬性。  
  
 這些批註也可以用於指定 XML 中的階層式關聯性，以代表資料庫中的關聯性，因為 XSD 架構只是關聯式資料的 XML 觀點。  
  
 本節提供您可搭配 XSD 結構描述一起使用之註解的描述以及其使用方式的範例。  
  
> [!NOTE]  
>  本節中的所有範例都會根據每個範例中所描述的註解式 XSD 結構描述，指定簡單的 XPath 查詢。 同時會假設您熟悉 XPath 語言。  
  
## <a name="in-this-section"></a>本節內容  
 [&#40;SQLXML 4.0&#41;的 XSD 批註 ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/xsd-annotations-sqlxml-4-0.md)  
 列出您可以搭配 XSD 結構描述使用的註解、其描述，以及適用於 XDR 的相等註解。  
  
 [XSD 元素和屬性與資料表和資料行的預設對應 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/default-mapping-of-xsd-elements-and-attributes-to-tables-and-columns-sqlxml-4-0.md)  
 說明預設對應，並提供與預設對應相關之工作的範例。  
  
 [XSD 元素和屬性與資料表和資料行的明確對應 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/explicit-mapping-xsd-elements-and-attributes-to-tables-and-columns.md)  
 說明與 **sql： relation** 和 **sql： field** 批註的明確對應，並提供範例。  
  
 [使用 sql： relationship 指定關聯性 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
 描述和提供 **sql： relationship** 注釋的範例。  
  
 [在 sql： relationship &#40;SQLXML 4.0&#41;上指定 sql：反向屬性 ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)  
 描述 **sql：反向** 注釋。  
  
 [使用 sql：建立常數元素是常數 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)  
 描述和提供 **sql：為-常數** 注釋的範例。  
  
 [使用 sql：對應的 XML 檔從產生的 XML 檔排除架構元素 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)  
 描述和提供 **sql：對應** 注釋的範例。  
  
 [使用 sql： limit-field 和 sql： limit-value &#40;SQLXML 4.0&#41;篩選值 ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/filtering-values-using-sql-limit-field-and-sql-limit-value-sqlxml-4-0.md)  
 描述並提供 **sql： limit 欄位** 和 **sql： limit-value** 注釋的範例。  
  
 [使用 sql：索引鍵欄位來識別索引鍵資料行 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)  
 描述及提供 **sql：索引鍵-欄位** 批註的範例。  
  
 [使用 targetNamespace 屬性指定目標命名空間 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
 描述和提供 **targetNamespace** 屬性的範例。  
  
 [使用 sql： prefix 建立有效的 ID、IDREF 和 IDREFS 類型屬性 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)  
 描述並提供 **sql： prefix** 批註的範例。  
  
 [資料類型轉換和 sql： datatype 注釋 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md)  
 描述和提供 **sql： datatype** 注釋的範例。  
  
 [將 XSD 資料類型對應到 XPath 資料類型 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/mapping-xsd-data-types-to-xpath-data-types-sqlxml-4-0.md)  
 提供比較 XSD、XDR 與 XPath 資料類型的資料表，並列出相關的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 轉換。  
  
 [使用 sql： use-cdata 建立 CDATA 區段 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)  
 描述和提供 **sql： use-data** 注釋的範例。  
  
 [使用 sql：編碼 &#40;SQLXML 4.0&#41;來要求 BLOB 資料的 URL 參考 ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)  
 描述和提供 **sql：編碼** 注釋的範例。  
  
 [使用 sql：溢位欄位來抓取未耗用的資料 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/retrieving-unconsumed-data-using-the-sql-overflow-field-sqlxml-4-0.md)  
 描述並提供 **sql：溢位欄位** 批註的範例。  
  
 [使用 sql:hide 來隱藏項目和屬性](../../relational-databases/sqlxml-annotated-xsd-schemas-using/hiding-elements-and-attributes-by-using-sql-hide.md)  
 描述和提供 **sql： hide** 批註的範例。  
  
 [使用 sql:identity 和 sql:guid 註解](../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-the-sql-identity-and-sql-guid-annotations.md)  
 描述及提供 **sql： identity** 和 **sql： guid** 批註的範例。  
  
 [使用 sql:max-depth 來指定遞迴關聯性的深度](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)  
 描述及提供 **sql：最大深度** 注釋的範例。  
  
## <a name="see-also"></a>另請參閱  
 [&#40;SQLXML 4.0&#41;的批註式架構安全性考慮 ](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/annotated-schema-security-considerations-sqlxml-4-0.md)  
  
  
