---
title: 執行 XML 資料 (SQLXML) 的批次載入
description: 瞭解如何在 SQLXML 4.0 中使用 XML 大容量載入將半結構化 XML 資料載入到 Microsoft SQL Server 表中。
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
ms.openlocfilehash: 3aeb221d19ef163d567cae2fc9298a09ae33a797
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387982"
---
# <a name="performing-bulk-load-of-xml-data-sqlxml-40"></a>執行 XML 資料的大量載入 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  XML 大量載入是獨立的 COM 物件，可讓您將半結構化的 XML 資料載入至 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料表。  
  
## <a name="in-this-section"></a>本節內容  
 [XML 大容量負載介紹 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/introduction-to-xml-bulk-load-sqlxml-4-0.md)  
 提供有關使用 XML 大量載入公用程式來大量載入 XML 資料的一般資訊。 主題包含 XML 資料流以及交易與非交易大量載入作業。  
  
 [記錄產生過程&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/record-generation-process-sqlxml-4-0.md)  
 描述藉以產生 XML 大量載入之記錄的程序和規則。  
  
 [註釋解釋&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sqlxml-4-0.md)  
 描述 XML 大量載入如何解譯 XSD 和 XDR 結構描述中的註解。  
  
 [SQL Server XML 大量載入物件模型&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/sql-server-xml-bulk-load-object-model-sqlxml-4-0.md)  
 描述 SQLXMLBulkLoad 物件及其方法和屬性。  
  
 [XML 大容量負載示例&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/xml-bulk-load-examples-sqlxml-4-0.md)  
 提供使用 XML 大量載入的範例程式碼。  
  
 [資料類型和 XML 大量載入行為&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/data-types-and-xml-bulk-load-behavior-sqlxml-4-0.md)  
 描述 XML 大量載入在處理 XSD 和 XDR 中的不同類型時的行為。  
  
 [XML 大容量負載的指南和限制&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/guidelines-and-limitations-of-xml-bulk-load-sqlxml-4-0.md)  
 列出一些在使用 XML 大量載入時要注意的問題。  
  
  
