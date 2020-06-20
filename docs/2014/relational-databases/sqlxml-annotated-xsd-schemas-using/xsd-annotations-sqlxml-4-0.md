---
title: XSD 注釋（SQLXML 4.0） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, annotations listed
- XSD schemas [SQLXML], annotations
ms.assetid: c62a6785-8d66-40a2-9c5d-80c73d600a3b
author: rothja
ms.author: jroth
ms.openlocfilehash: d693217a264388f39fa18859c47b9e7aabdd45aa
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003222"
---
# <a name="xsd-annotations-sqlxml-40"></a>XSD 註解 (SQLXML 4.0)
  下表列出 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中推出的 XSD 註解，並與 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 中推出的 XDR 註解相比較。  
  
|XSD 註解|描述|主題連結|XDR 註解|  
|--------------------|-----------------|----------------|--------------------|  
|`sql:encode`|當 XML 元素或屬性對應到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] BLOB 資料行時，允許要求參考 URI。 此 URI 稍後可用於傳回 BLOB 資料。|[使用 sql： &#40;SQLXML 4.0&#41;要求對 BLOB 資料的 URL 參考](requesting-url-references-to-blob-data-using-sql-encode-sqlxml-4-0.md)|`url-encode`|  
|`sql:guid`|可讓您指定要使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 產生的 GUID 值，還是使用 Updategram 中針對該資料行提供的值。|[使用 sql:identity 和 sql:guid 註解](using-the-sql-identity-and-sql-guid-annotations.md)|不支援|  
|`sql:hide`|在產生的 XML 文件中，隱藏結構描述中指定的元素或屬性。|[使用 sql:hide 來隱藏項目和屬性](hiding-elements-and-attributes-by-using-sql-hide.md)|不支援|  
|`sql:identity`|可以在對應到 IDENTITY 類型之資料庫資料行的任何節點上指定。 針對此註解指定的值會定義如何更新資料庫中對應的 IDENTITY 類型資料行。|[使用 sql:identity 和 sql:guid 註解](using-the-sql-identity-and-sql-guid-annotations.md)|不支援|  
|`sql:inverse`|指示 updategram 邏輯反轉其對使用所指定之父子式關聯性的轉譯 **\<sql:relationship>** 。|[在 sql： relationship 上指定 sql：反向屬性 &#40;SQLXML 4.0&#41;](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md)|不支援|  
|`sql:is-constant`|建立不對應到任何資料表的 XML 元素。 該元素會出現在查詢輸出中。|[使用 sql： is-常數建立常數元素 &#40;SQLXML 4.0&#41;](creating-constant-elements-using-sql-is-constant-sqlxml-4-0.md)|相同|  
|`sql:key-fields`|可用來指定一或多個資料行，以用來唯一識別資料表中的資料列。|[使用 sql：索引鍵-欄位來識別索引鍵資料行 &#40;SQLXML 4.0&#41;](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md)|相同|  
|`sql:limit-field`<br /><br /> `sql:limit-value`|可用來限制根據限制值傳回的值。|[使用 sql： limit-field 和 sql： limit-value &#40;SQLXML 4.0&#41;篩選值](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)|相同|  
|`sql:mapped`|可用來將結構描述項目排除在結果之外。|[使用 sql：對應 &#40;SQLXML 4.0&#41;，從產生的 XML 檔排除架構元素](excluding-schema-elements-from-the-xml-document-using-sql-mapped.md)|`map-field`|  
|`sql:max-depth`|可讓您指定結構描述中指定之遞迴關聯性的深度。|[使用 sql:max-depth 來指定遞迴關聯性的深度](specifying-depth-in-recursive-relationships-by-using-sql-max-depth.md)|不支援|  
|`sql:overflow-field`|可識別包含溢位資料的資料庫資料行。|[使用 sql：溢位欄位來抓取未使用的資料 &#40;SQLXML 4.0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)|相同|  
|`sql:prefix`|建立有效的 XML ID、IDREF 和 IDREFS。 在字串前面加上 ID、IDREF 和 IDREFS 的值。|[使用 sql： prefix 建立有效的 ID、IDREF 和 IDREFS 類型屬性 &#40;SQLXML 4.0&#41;](creating-valid-id-idref-and-idrefs-type-attributes-using-sql-prefix-sqlxml-4-0.md)|相同|  
|`sql:relationship`|指定 XML 元素之間的關聯性。 `parent`、`child`、`parent-key` 和 `child-key` 屬性可用來建立關聯性。|[使用 sql： relationship 指定關聯性 &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)|屬性名稱不同：<br /><br /> `key-relation`<br /><br /> `foreign-relation`<br /><br /> `key`<br /><br /> `foreign-key`|  
|`sql:use-cdata`|可用來針對 XML 文件中的特定元素指定要使用的 CDATA 區段。|[使用 sql： use-CDATA 建立 CDATA 區段 &#40;SQLXML 4.0&#41;](creating-cdata-sections-using-sql-use-cdata-sqlxml-4-0.md)|相同|  
  
> [!NOTE]  
>  XSD 原生 `targetNamespace` 屬性會取代 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] XDR 對應結構描述中推出的 `target-namespace` 註解。  
  
## <a name="see-also"></a>另請參閱  
 [使用 targetNamespace 屬性來指定目標命名空間 &#40;SQLXML 4.0&#41;](specifying-a-target-namespace-using-the-targetnamespace-attribute-sqlxml-4-0.md)  
  
  
