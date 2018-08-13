---
title: 伺服器端 XML 格式化 (SQLXML 4.0) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: c7c32468545c500383601a5b19f8693d73f6905e
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2018
ms.locfileid: "39534458"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>伺服器端 XML 格式 (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  本主題提供在伺服器端上，從針對 Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 資料庫執行之查詢產生的資料列集格式化 XML 文件的相關資訊。  
  
 在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中，您可以將 XML 文件儲存到資料庫資料表中，以及從資料庫資料表中擷取 XML 文件。 若要擷取 XML 文件，請在 SELECT 查詢中使用 FOR XML 查詢延伸模組。  
  
 例如，假設用戶端應用程式針對執行命令[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，包含下列[!INCLUDE[tsql](../../../includes/tsql-md.md)]查詢：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 伺服器會以兩個步驟執行查詢。 首先，伺服器會執行這個 SELECT 陳述式：  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 接著，伺服器會將 FOR XML 轉換套用到產生的資料列集。 產生的 XML 就會傳送到用戶端，做為單一資料行資料列集。 在此文件集中，此程序也就是所謂的伺服器端 XML 格式化。  
  
 在伺服器端，您可以利用 FOR XML 子句指定下列模式：  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 如需有關 FOR XML 子句的詳細資訊，請參閱 <<c0> [ 使用 FOR XML 建構 XML](../../../relational-databases/xml/for-xml-sql-server.md)。  
  
## <a name="see-also"></a>另請參閱  
 [用戶端和伺服器端 XML 格式化架構&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [用戶端 XML 格式化&#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
