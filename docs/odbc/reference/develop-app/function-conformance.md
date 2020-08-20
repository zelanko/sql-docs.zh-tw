---
description: 函式一致性
title: 函數一致性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ff61c62b18f531eaad7cc822f99c7065fcba129
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465790"
---
# <a name="function-conformance"></a>函式一致性
下表指出每個 ODBC 函數的一致性層級，這是妥善定義的。  
  
|函式|一致性層級|  
|--------------|-----------------------|  
|**SQLAllocHandle**|核心|  
|**SQLBindCol**|核心|  
|**SQLBindParameter**|核心 [1]|  
|**SQLBrowseConnect**|層級 1|  
|**SQLBulkOperations**|層級 1|  
|**SQLCancel**|核心 [1]|  
|**SQLCloseCursor**|核心|  
|**SQLColAttribute**|核心 [1]|  
|**SQLColumnPrivileges**|層級 2|  
|**SQLColumns**|核心|  
|**SQLConnect**|核心|  
|**SQLCopyDesc**|核心|  
|**SQLDataSources**|核心|  
|**SQLDescribeCol**|核心 [1]|  
|**SQLDescribeParam**|層級 2|  
|**SQLDisconnect**|核心|  
|**SQLDriverConnect**|核心|  
|**SQLDrivers**|核心|  
|**SQLEndTran**|核心 [1]|  
|**SQLExecDirect**|核心|  
|**SQLExecute**|核心|  
|**SQLFetch**|核心|  
|**SQLFetchScroll**|核心 [1]|  
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
|**SQLSetConnectAttr**|核心 [2]|  
|**SQLSetCursorName**|核心|  
|**SQLSetDescField**|核心 [1]|  
|**SQLSetDescRec**|核心|  
|**SQLSetEnvAttr**|核心 [2]|  
|**SQLSetPos**|層級 1 [1]|  
|**SQLSetStmtAttr**|核心 [2]|  
|**SQLSpecialColumns**|核心 [1]|  
|**SQLStatistics**|核心|  
|**SQLTablePrivileges**|層級 2|  
|**SQLTables**|核心|  
  
 [1] 此函式的重要功能僅適用于較高的一致性層級。  
  
 [2] 將某些屬性設定為非預設值取決於一致性層級。 如需詳細資訊，請參閱下一節的 [屬性一致性](../../../odbc/reference/develop-app/attribute-conformance.md)。
