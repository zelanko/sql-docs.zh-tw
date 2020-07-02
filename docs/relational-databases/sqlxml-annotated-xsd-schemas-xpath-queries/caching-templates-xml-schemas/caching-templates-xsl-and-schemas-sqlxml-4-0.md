---
title: 快取範本、XSL 和架構（SQLXML）
description: 在 SQLXML 4.0 中，查看快取範本、XSL 和架構的相關資訊。
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a1481a45c65f2c6876c6acbc35d42d1706776b49
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/01/2020
ms.locfileid: "85650498"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>快取範本、XSL 和結構描述 (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  為增進效能，[!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 支援快取範本、XSL 和結構描述。  
  
 系統會快取所有架構、範本和 XSL 檔案（HTTPs://或 ftp://位置中的檔案除外）。 當程序正在執行時，快取的檔案仍然在記憶體中。 當程序結束時，所有快取都會消失。 因此，如果每個查詢執行一個程序，快取的效益可能就不明顯。  
  
 本節中的主題提供有關快取的詳細資訊。  
  
## <a name="in-this-section"></a>本節內容  
 [&#40;SQLXML 4.0&#41;的範本快取](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 描述並提供範本快取的登錄機碼。  
  
 [XSL Caching &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 描述並提供 XSL 快取的登錄機碼。  
  
 [架構快取 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 討論與結構描述快取相關的 SQLXML 並行安裝問題，並提供結構描述快取的登錄機碼。  
  
  
