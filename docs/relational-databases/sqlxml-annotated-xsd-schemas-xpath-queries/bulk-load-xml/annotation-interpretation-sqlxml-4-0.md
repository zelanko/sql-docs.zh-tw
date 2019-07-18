---
title: 註解解譯 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 80db781d32c8d48f9df48c27baa1807eef5a9f7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68054395"
---
# <a name="annotation-interpretation-sqlxml-40"></a>註解的解譯 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本章節的主題描述 XML 大量載入要如何解譯 XSD 結構描述中的註解。 這裡所述的行為也適用於 XDR 結構描述中的註解。  
  
> [!NOTE]  
>  這些主題的資訊只會描述 XML 大量載入在處理時所使用的註解。 SQLXML 4.0 支援之 XSD 結構描述註解的完整清單，請參閱 <<c0> [ 使用的註解 XSD 結構描述中&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。</c0> 如需支援的註解 XDR 結構描述的清單，請參閱 < [Annotated XDR Schemas&#40;在 SQLXML 4.0 中已被取代&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [sql: relationship 和關鍵識別碼順序規則&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 描述如何**sql: relationship**註釋會在 XML 大量載入內解譯。  
  
 [sql： 對應&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 描述如何**sql： 對應**註釋會在 XML 大量載入內解譯。  
  
 [sql: limit-value-欄位和 sql: limit-value-值&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 描述如何**sql: limit-value-欄位**並**sql: limit-value-值**註釋會在 XML 大量載入內解譯。  
  
 [sql: overflow-field-欄位&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 描述如何**sql: overflow-field**註釋會在 XML 大量載入內解譯。  
  
 [其他註解&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 描述如何在 XML 大量載入內解譯下列註解： **sql: id-prefix-前置詞**， **sql: use-cdata-cdata**， **sql: url-encode-編碼**， **sql:為對應結構描述**， **sql: key-fields 來-欄位**。  
  
  
