---
title: SQLXML 4.0 程式設計概念
description: 查看 SQLXML 4.0 中所使用之程式設計概念的相關資訊。
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, about SQLXML
- SQLXML
ms.assetid: 5a11cda2-b8a3-4453-848f-641afdaa7024
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 21e32d4e0091738c95ed995318e4a1904c81d127
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809293"
---
# <a name="sqlxml-40-programming-concepts"></a>SQLXML 4.0 程式設計概念
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  SQLXML 3.0 會以 Web 發行的形式提供了額外的用戶端 XML 功能以及現有功能的增強功能，例如註解 XSD 結構描述、XML 大量載入、Web 服務 (SOAP) 支援和 Updategram。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 導入了 SQLXML 4.0，繼續提供與 SQLXML 3.0 相同的功能，以及配合 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 所導入之新功能的其他更新。  
  
 本節會提供 SQLXML 4.0 的相關資訊。  
  
 [SQLXML 不會安裝在 SQL Server 中](../../relational-databases/sqlxml/sqlxml-is-not-installed-in-sql-server.md)  
 說明如何安裝 SQLXML 4.0。  
  
 [SQLXML 4.0 SP1 的新功能](../../relational-databases/sqlxml/what-s-new-in-sqlxml-4-0-sp1.md)  
 說明 SQLXML 4.0 中的更新和增強功能，並提供此文件中的相關主題連結。  
  
 [使用 ADO 執行 SQLXML 4.0 查詢](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md)  
 描述如何使用 ADO 進行 SQLXML 查詢。 ADO 在 SQLXML 4.0 中的功能遠比在舊版中強大。  
  
 [xml 資料類型在 SQLXML 4.0 中的支援](../../relational-databases/sqlxml/xml-data-type-support-in-sqlxml-4-0.md)  
 描述已針對 SQLXML 4.0 新增的 xml 資料類型支援。  
  
 [執行 SQLXML 範例的需求](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md)  
 描述從所提供的 SQLXML 範例建立工作範例的需求。  
  
 [用戶端和伺服器端格式設定 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml/formatting/client-side-and-server-side-formatting-sqlxml-4-0.md)  
 提供用戶端和伺服器端之格式設定的相關資訊和比較，包括用來建構 XML 文件的 FOR XML 命令。  
  
 [SQLXML 4.0 中的註解式 XSD 結構描述](../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xsd-schemas-in-sqlxml-4-0.md)  
 提供在 SQLXML 4.0 中使用註解 XSD 結構描述的相關資訊。 也提供用於舊版應用程式的註解 XDR 結構描述的相關資訊。  
  
 [在 SQLXML 4.0 中使用 XPath 查詢](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/using-xpath-queries-in-sqlxml-4-0.md)  
 描述如何使用 XPath 語言的子集來查詢由註解 XSD 結構描述所建立的 XML 檢視，並且提供範例。  
  
 [使用 Updategram 來修改 SQLXML 4.0 中的資料](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/using-updategrams-to-modify-data-in-sqlxml-4-0.md)  
 提供有關 Updategram 的相關資訊，Updategram 會針對 XSD (或 XDR) 註解結構描述所提供的 XML 檢視進行作業，以修改資料庫中的資料。  
  
 [執行 XML 資料的大量載入 &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
 描述如何在 SQLXML 4.0 中大量載入 XML。  
  
 [SQLXML 4.0 Data Access Components](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/data-access-components-provider/sqlxml-4-0-data-access-components-sqlxmloledb-provider.md)  
 提供 SQLXMLOLEDB 提供者的說明以及其他 SQLXML 4.0 資料存取元件的連結。  
  
 [SQLXML 4.0 .NET Framework 支援](../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)  
 描述 .NET Framework 的 SQLXML 4.0 支援。  
  
 [&#40;SQLXML 4.0 快取範本、XSL 和架構&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/caching-templates-xsl-and-schemas-sqlxml-4-0.md)  
 描述 SQLXML 為增強效能而提供的快取功能。  
  
 [SQLXML 4.0 安全性考量](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/sqlxml-4-0-security-considerations.md)  
 討論與 SQLXML 4.0 相關的安全性問題。  
  
 [SQLXML 4.0 的指導方針和限制](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/guidelines-and-limitations-of-sqlxml-4-0.md)  
 列出在使用 SQLXML 4.0 時要注意的問題。  
  
## <a name="see-also"></a>另請參閱  
 [XML 資料 &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
