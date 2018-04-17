---
title: 目錄函數中的引數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f46b286a929d261b1cf1c608fefccd5f266b92b2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="arguments-in-catalog-functions"></a>目錄函數中的引數
所有類別目錄函式接受引數與應用程式可以限制傳回的資料範圍。 例如，第一個和第二個呼叫**SQLTables**在下列程式碼會傳回包含所有的資料表的相關資訊，而第三個呼叫會傳回 Orders 資料表的相關資訊的結果集：  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目錄函式的字串引數分為四種不同類型： 一般引數 (OA)、 模式數值引數 (PV)、 識別項引數 (ID) 和值清單引數 (VL)。 大部分的字串引數可以是下列其中一種不同，根據 SQL_ATTR_METADATA_ID 陳述式屬性的值。 下表列出每個類別目錄函式的引數，並描述 SQL_ATTR_METADATA_ID SQL_TRUE 或 SQL_FALSE 值的引數的型別。  
  
|函數|引數|輸入當 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|輸入當 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|識別碼 ID 識別碼 ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|識別碼 ID 識別碼 ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|識別碼 ID 識別碼 ID 識別碼 ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼 ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|識別碼 ID 識別碼 ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|識別碼 ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼 ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼 ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|識別碼 ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|識別碼 ID 識別碼 VL|  
  
 此章節包含下列主題。  
  
-   [一般引數](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [識別碼引數](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值清單引數](../../../odbc/reference/develop-app/value-list-arguments.md)
