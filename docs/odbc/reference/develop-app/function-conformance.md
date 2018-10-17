---
title: 函式一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], function
- function conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: bb5d68cf-d238-481e-babc-2e9401b4700e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b6cb2f56113487922866573caf3b5f8b67fff7c4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740076"
---
# <a name="function-conformance"></a>函式一致性
下表指出這是妥善定義的每個 ODBC 函式，一致性層級。  
  
|函數|一致性層級|  
|--------------|-----------------------|  
|**SQLAllocHandle**|核心|  
|**SQLBindCol**|核心|  
|**SQLBindParameter**|Core [1]|  
|**SQLBrowseConnect**|層級 1|  
|**SQLBulkOperations**|層級 1|  
|**SQLCancel**|Core [1]|  
|**SQLCloseCursor**|核心|  
|**SQLColAttribute**|Core [1]|  
|**SQLColumnPrivileges**|層級 2|  
|**SQLColumns**|核心|  
|**SQLConnect**|核心|  
|**SQLCopyDesc**|核心|  
|**SQLDataSources**|核心|  
|**SQLDescribeCol**|Core [1]|  
|**SQLDescribeParam**|層級 2|  
|**SQLDisconnect**|核心|  
|**SQLDriverConnect**|核心|  
|**SQLDrivers**|核心|  
|**SQLEndTran**|Core [1]|  
|**SQLExecDirect**|核心|  
|**SQLExecute**|核心|  
|**SQLFetch**|核心|  
|**SQLFetchScroll**|Core [1]|  
|**SQLForeignKeys**|層級 2|  
|**SQLFreeHandle**|核心|  
|**SQLFreeStmt**|核心|  
|**SQLGetConnectAttr**|核心|  
|**SQLGetCursorName**|核心|  
|**SQLGetData**|核心|  
|**SQLGetDescField**|核心|  
|**SQLGetDescRec**|核心|  
|**SQLGetDiagField**|核心|  
|**SQLGetDiagRec**|核心|  
|**SQLGetEnvAttr**|核心|  
|**SQLGetFunctions**|核心|  
|**SQLGetInfo**|核心|  
|**SQLGetStmtAttr**|核心|  
|**SQLGetTypeInfo**|核心|  
|**SQLMoreResults**|層級 1|  
|**SQLNativeSql**|核心|  
|**SQLNumParams**|核心|  
|**SQLNumResultCols**|核心|  
|**SQLParamData**|核心|  
|**SQLPrepare**|核心|  
|**SQLPrimaryKeys**|層級 1|  
|**SQLProcedureColumns**|層級 1|  
|**SQLProcedures**|層級 1|  
|**SQLPutData**|核心|  
|**SQLRowCount**|核心|  
|**SQLSetConnectAttr**|Core [2]|  
|**SQLSetCursorName**|核心|  
|**SQLSetDescField**|Core [1]|  
|**SQLSetDescRec**|核心|  
|**SQLSetEnvAttr**|Core [2]|  
|**SQLSetPos**|層級 1] [1]|  
|**SQLSetStmtAttr**|Core [2]|  
|**SQLSpecialColumns**|Core [1]|  
|**SQLStatistics**|核心|  
|**SQLTablePrivileges**|層級 2|  
|**SQLTables**|核心|  
  
 [1] 重要的功能，此函式可只能在較高的一致性層級。  
  
 [2] 將某些屬性設定為非預設值是根據一致性層級而定。 如需詳細資訊，請參閱下一步 區段中，[屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)。
