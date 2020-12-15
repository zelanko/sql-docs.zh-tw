---
title: " (SQLXML) 的批註解讀"
description: 瞭解 SQLXML 4.0 中的 XML 大量載入如何解讀 XSD 和 XDR 架構中的注釋。
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9763f36a2a2d4678ec76f77cec65bc68d5cbef85
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462919"
---
# <a name="annotation-interpretation-sqlxml-40"></a>註解的解譯 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  本章節的主題描述 XML 大量載入要如何解譯 XSD 結構描述中的註解。 這裡所述的行為也適用於 XDR 結構描述中的註解。  
  
> [!NOTE]  
>  這些主題的資訊只會描述 XML 大量載入在處理時所使用的註解。 如需 SQLXML 4.0 所支援之 XSD 架構注釋的完整清單，請參閱 [在 Xsd 架構中使用注釋 &#40;sqlxml 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md)。 如需 XDR 架構支援的注釋清單，請參閱 [SQLXML 4.0&#41;中 &#40;取代的批註式 XDR 架構 ](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md)。  
  
## <a name="in-this-section"></a>本節內容  
 [sql： relationship 和索引鍵順序規則 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 描述如何在 XML 大量載入中解讀 **sql： relationship** 注釋。  
  
 [sql：對應 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 描述如何在 XML 大量載入中解讀 **sql：對應** 的注釋。  
  
 [sql： limit-field 和 sql： limit-value &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 描述如何在 XML 大量載入中解讀 **sql： limit 欄位** 和 **sql： limit 值** 注釋。  
  
 [sql：溢位-field &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 描述如何在 XML 大量載入中解讀 **sql：溢** 位注釋。  
  
 [&#40;SQLXML 4.0&#41;的其他批註 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 描述如何在 XML 大量載入中解讀下列注釋： **sql： id-前置** 詞、 **sql： use-cdata**、 **sql： url 編碼**、 **sql：為-對應-架構**、 **sql：索引鍵欄位**。  
  
  
