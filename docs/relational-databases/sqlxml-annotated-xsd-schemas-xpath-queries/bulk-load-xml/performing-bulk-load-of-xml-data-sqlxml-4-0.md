---
title: 執行 XML 資料的大量載入（SQLXML）
description: 瞭解如何使用 SQLXML 4.0 中的 XML 大量載入，將半結構化的 XML 資料載入 Microsoft SQL Server 資料表。
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- XML Bulk Load [SQLXML]
- bulk load [SQLXML]
- data insertions [SQLXML]
- SQLXML, bulk loading
- XSD schemas [SQLXML], XML Bulk Load
- XDR schemas [SQLXML], XML Bulk Load
- inserting data
ms.assetid: 3708b493-322e-4f3c-9b27-441d0c0ee346
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c696f39c3e41afa42f5f4f0fac5c7dfd1a4dd080
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773073"
---
# <a name="performing-bulk-load-of-xml-data-sqlxml-40"></a>執行 XML 資料的大量載入 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  XML 大量載入是獨立的 COM 物件，可讓您將半結構化的 XML 資料載入至 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
## <a name="in-this-section"></a>本節內容  
 [XML 大量載入簡介 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/introduction-to-xml-bulk-load-sqlxml-4-0.md)  
 提供有關使用 XML 大量載入公用程式來大量載入 XML 資料的一般資訊。 主題包含 XML 資料流以及交易與非交易大量載入作業。  
  
 [記錄產生進程 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/record-generation-process-sqlxml-4-0.md)  
 描述藉以產生 XML 大量載入之記錄的程序和規則。  
  
 [&#40;SQLXML 4.0&#41;的注釋轉譯](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
 描述 XML 大量載入如何解譯 XSD 和 XDR 結構描述中的註解。  
  
 [SQL Server XML 大量載入物件模型 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md)  
 描述 Sqlxmlbulkload.sqlxmlbulkload.4.0 物件及其方法和屬性。  
  
 [XML 大量載入範例 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
 提供使用 XML 大量載入的範例程式碼。  
  
 [資料類型與 XML 大量載入行為 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/data-types-and-xml-bulk-load-behavior-sqlxml-4-0.md)  
 描述 XML 大量載入在處理 XSD 和 XDR 中的不同類型時的行為。  
  
 [XML 大量載入的指導方針和限制 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/guidelines-and-limitations-of-xml-bulk-load-sqlxml-4-0.md)  
 列出一些在使用 XML 大量載入時要注意的問題。  
  
  
