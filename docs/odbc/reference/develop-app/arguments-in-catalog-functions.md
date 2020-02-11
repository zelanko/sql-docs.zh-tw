---
title: 目錄函數中的引數 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106287"
---
# <a name="arguments-in-catalog-functions"></a>目錄函式中的引數
所有目錄函式都接受引數，應用程式可以在其中限制所傳回的資料範圍。 例如，下列程式碼中**SQLTables**的第一個和第二個呼叫會傳回包含所有資料表之相關資訊的結果集，而第三個呼叫會傳回 Orders 資料表的相關資訊：  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 目錄函數位符串引數分為四種不同類型：一般引數（OA）、模式值引數（PV）、識別碼引數（ID）和值清單引數（VL）。 大部分的字串引數可以是兩種不同類型的其中一種，視 SQL_ATTR_METADATA_ID 語句屬性的值而定。 下表列出每個目錄函數的引數，並描述 SQL_TRUE 的引數類型或 SQL_ATTR_METADATA_ID 的 SQL_FALSE 值。  
  
|函式|引數|SQL_ 時輸入<br /><br /> ATTR_METADATA_<br /><br /> 識別碼 = SQL_FALSE|SQL_ 時輸入<br /><br /> ATTR_METADATA_<br /><br /> 識別碼 = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|識別碼識別碼識別碼|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|識別碼識別碼識別碼|  
|**SQLForeignKeys**|*Sqlforeignkeys* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|識別碼識別碼識別碼識別碼識別碼|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼識別碼|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|識別碼識別碼識別碼|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|識別碼識別碼|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼識別碼|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|識別碼識別碼|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|識別碼識別碼|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|識別碼識別碼識別碼 VL|  
  
 此章節包含下列主題。  
  
-   [一般引數](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [識別碼引數](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [值清單引數](../../../odbc/reference/develop-app/value-list-arguments.md)
