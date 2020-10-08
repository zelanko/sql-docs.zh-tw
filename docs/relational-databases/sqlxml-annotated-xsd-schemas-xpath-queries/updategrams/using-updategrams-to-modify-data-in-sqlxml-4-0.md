---
title: 使用 Updategram 來修改 SQLXML 4.0 中的資料
description: 查看有關 updategram 的資訊和範例，以及如何使用它們來修改 SQLXML 4.0 中的資料。
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- data insertions [SQLXML]
- data deletions [SQLXML]
- updating data [SQLXML]
- modifying data [SQLXML]
- OPENXML function
- updategrams [SQLXML]
- database modifications [SQLXML]
- data updates [SQLXML]
- modifying databases
- data modifications [SQLXML]
- deleting data
- inserting data
ms.assetid: b8b3b892-cb73-41d0-b945-bce148d81d9b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fa45ac2a57ff4f59dc3f3367dc2c66f638f2516b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/07/2020
ms.locfileid: "91811062"
---
# <a name="using-updategrams-to-modify-data-in-sqlxml-40"></a>使用 Updategram 來修改 SQLXML 4.0 中的資料
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  您可以 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 使用 UPDATEGRAM 或 OPENXML 函數，從現有的 XML 檔修改 (插入、更新或刪除) 資料庫 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 。  
  
 本節提供有關 Updategram 及其使用範例的資訊。  
  
## <a name="in-this-section"></a>本節內容  
 [Updategram &#40;SQLXML 4.0&#41;簡介 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/introduction-to-updategrams-sqlxml-4-0.md)  
 提供 Updategram 的基本資訊和範例。  
  
 [在 Updategram 中指定批註式對應架構 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)  
 說明與提供 Updategram 中的註解式對應結構描述範例。  
  
 [&#40;SQLXML 4.0&#41;的 Null 處理 ](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/null-handling-sqlxml-4-0.md)  
 描述如何針對元素和屬性值指定 NULL。  
  
 [使用 XML Updategram 插入資料 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
 描述與提供使用 Updategram 插入資料的範例。  
  
 [使用 XML Updategram 刪除資料 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/deleting-data-using-xml-updategrams-sqlxml-4-0.md)  
 描述與提供使用 Updategram 刪除資料的範例。  
  
 [使用 XML Updategram 更新資料 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)  
 描述與提供使用 Updategram 修改現有資料的範例。  
  
 [將參數傳遞至 Updategram &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)  
 描述與提供將參數傳遞到 Updategram 的範例。  
  
 [在 Updategram 中處理資料庫並行問題 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/handling-database-concurrency-issues-in-updategrams-sqlxml-4-0.md)  
 描述在 Updategram 中處理並行問題的各種可能保護等級，並提供範例。  
  
 [Updategram &#40;SQLXML 4.0&#41;的範例應用程式 ]()  
 提供使用 Updategram 的範例應用程式。  
  
 [XML Updategram 的指導方針和限制 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/guidelines-and-limitations-of-xml-updategrams-sqlxml-4-0.md)  
 列出使用 Updategram 時要注意的事項。  
  
