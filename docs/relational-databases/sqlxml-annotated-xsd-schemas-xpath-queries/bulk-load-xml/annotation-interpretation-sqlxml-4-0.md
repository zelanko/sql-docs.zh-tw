---
title: "註解的解譯 (SQLXML 4.0) |Microsoft 文件"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7f2d066414f6835f0803d6530e0ea1fa187c04ff
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2018
---
# <a name="annotation-interpretation-sqlxml-40"></a>註解的解譯 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
本章節的主題描述 XML 大量載入要如何解譯 XSD 結構描述中的註解。 這裡所述的行為也適用於 XDR 結構描述中的註解。  
  
> [!NOTE]  
>  這些主題的資訊只會描述 XML 大量載入在處理時所使用的註解。 如需註解的 XSD 結構描述支援的 SQLXML 4.0 的完整清單，請參閱[使用 XSD 結構描述 &#40; 中的註釋SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md). 如需支援的註解的 XDR 結構描述的清單，請參閱[Annotated XDR Schemas &#40; SQLXML 4.0 &#41; 中的已過時](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [sql: relationship 和關鍵識別碼順序規則 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 描述如何**sql: relationship**註釋會在 XML 大量載入內解譯。  
  
 [sql:mapped &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 描述如何**sql： 對應**註釋會在 XML 大量載入內解譯。  
  
 [sql: limit-value-欄位和 sql: limit-value-值 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 描述如何**sql: limit-value-欄位**和**sql: limit-value-值**在 XML 大量載入內解譯註解。  
  
 [sql: overflow-field-欄位 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 描述如何**sql: overflow-field**註釋會在 XML 大量載入內解譯。  
  
 [其他註解 &#40;SQLXML 4.0 &#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 描述如何在 XML 大量載入內解譯下列註解： **sql: id-prefix-前置詞**， **sql: use-cdata-cdata**， **sql: url-encode-編碼**， **sql:為對應結構描述**， **sql: key-fields-欄位**。  
  
  
