---
title: 目錄函式中的引數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 649c00f1db486dab4a996138be4e26b0e270fbae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106287"
---
# <a name="arguments-in-catalog-functions"></a>目錄函式中的引數
所有目錄函式都接受引數與應用程式可以限制傳回的資料範圍。 比方說，第一個和第二個呼叫**SQLTables**在下列程式碼會傳回包含所有資料表的相關資訊，而第三個呼叫會傳回 Orders 資料表的相關資訊的結果集：  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目錄函式的字串引數可分為四種不同類型： 一般引數 (OA)、 模式值引數 (PV)、 識別碼引數 (ID) 和值清單引數 (VL)。 大部分的字串引數可以是其中一種兩種不同類型的詳細資訊，根據 SQL_ATTR_METADATA_ID 陳述式屬性的值。 下表列出每個目錄函式的引數，並描述 SQL_ATTR_METADATA_ID SQL_TRUE 或 SQL_FALSE 值的引數的型別。  
  
|函數|引數|輸入當 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|輸入當 SQL_<br /><br /> ATTR_METADATA_<br /><br /> 識別碼 = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|識別碼 ID 識別碼 ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|識別碼 ID 識別碼 ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|識別碼 ID 識別碼 ID 識別碼 ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼為識別碼 ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|識別碼 ID 識別碼 ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|識別碼為識別碼 ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼為識別碼 ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼為識別碼 ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|識別碼為識別碼 ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|識別碼 ID 識別碼 VL|  
  
 此章節包含下列主題。  
  
-   [一般引數](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [識別碼引數](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值清單引數](../../../odbc/reference/develop-app/value-list-arguments.md)
