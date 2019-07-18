---
title: 撰寫 ODBC 3.x 驅動程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078899"
---
# <a name="writing-odbc-3x-drivers"></a>撰寫 ODBC 3.x 驅動程式
下表會顯示在 ODBC 3 函數支援。*x*驅動程式和 ODBC 應用程式和函式呼叫針對 ODBC 3 時執行的驅動程式管理員中的對應。*x*驅動程式。  
  
|函數|支援<br /><br /> 藉由<br /><br /> ODBC 3。*x*<br /><br /> 驅動程式？|支援<br /><br /> 藉由<br /><br /> ODBC 3。*x*<br /><br /> 應用程式嗎？|對應/支援<br /><br /> ODBC 3 中。*x*<br /><br /> 驅動程式管理員<br /><br /> ODBC 3。*x*驅動程式？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|否|No[1]|是|  
|**SQLAllocEnv**|否|No[1]|是|  
|**SQLAllocHandle**|是|是|否|  
|**SQLAllocStmt**|否|No[1]|是|  
|**SQLBindCol**|是|是|否|  
|**SQLBindParam**|否|[是] [2]|是|  
|**SQLBindParameter**|是|是|否|  
|**SQLBrowseConnect**|是|是|否|  
|**SQLBulkOperations**|是|是|否|  
|**SQLCancel**|是|是|否|  
|**SQLCloseCursor**|是|是|否|  
|**SQLColAttribute**|是|是|否|  
|**SQLColAttributes**|No[3]|否|是|  
|**SQLColumnPrivileges**|是|是|否|  
|**SQLColumns**|是|是|否|  
|**SQLConnect**|是|是|否|  
|**SQLCopyDesc**|是|是|[是] [4]|  
|**SQLDataSources**|否|是|是|  
|**SQLDescribeCol**|是|是|否|  
|**SQLDescribeParam**|是|是|否|  
|**SQLDisconnect**|是|是|否|  
|**SQLDriverConnect**|是|是|否|  
|**SQLDrivers**|否|是|是|  
|**SQLEndTran**|是|是|否|  
|**SQLError**|否|No[1]|是|  
|**SQLExecDirect**|是|是|否|  
|**SQLExecute**|是|是|否|  
|**SQLExtendedFetch**|是|否|否|  
|**SQLFetch**|是|是|否|  
|**SQLFetchScroll**|是|是|否|  
|**SQLForeignKeys**|是|是|否|  
|**SQLFreeConnect**|否|[是] [1]|是|  
|**SQLFreeEnv**|否|[是] [1]|是|  
|**SQLFreeHandle**|是|是|否|  
|**SQLFreeStmt**|是|是|否|  
|**SQLGetConnectAttr**|是|是|否|  
|**SQLGetConnectOption**|No[5]|No[1]|是|  
|**SQLGetCursorName**|是|是|否|  
|**SQLGetData**|是|是|否|  
|**SQLGetDescField**|是|是|否|  
|**SQLGetDescRec**|是|是|否|  
|**SQLGetDiagField**|是|是|否|  
|**SQLGetDiagRec**|是|是|否|  
|**SQLGetEnvAttr**|是|是|否|  
|**SQLGetFunctions**|No[6]|是|是|  
|**SQLGetInfo**|是|是|否|  
|**SQLGetStmtAttr**|是|是|否|  
|**SQLGetStmtOption**|No[5]|No[1]|是|  
|**SQLGetTypeInfo**|是|是|否|  
|**SQLMoreResults**|是|是|否|  
|**SQLNativeSql**|是|是|否|  
|**SQLNumParams**|是|是|否|  
|**SQLNumResultCols**|是|是|否|  
|**SQLParamData**|是|是|否|  
|**SQLParamOptions**|否|否|是|  
|**SQLPrepare**|是|是|否|  
|**SQLPrimaryKeys**|是|是|否|  
|**SQLProcedureColumns**|是|是|否|  
|**SQLProcedures**|是|是|否|  
|**SQLPutData**|是|是|否|  
|**SQLRowCount**|是|是|否|  
|**SQLSetConnectAttr**|是|是|否|  
|**SQLSetConnectOption**|No[5]|No[1]|是|  
|**SQLSetCursorName**|是|是|否|  
|**SQLSetDescField**|是|是|否|  
|**SQLSetDescRec**|是|是|否|  
|**SQLSetEnvAttr**|是|是|否|  
|**SQLSetPos**|是|是|否|  
|**SQLSetParam**|否|否|是|  
|**SQLSetScrollOption**|是|是|否|  
|**SQLSetStmtAttr**|是|是|否|  
|**SQLSetStmtOption**|No[5]|No[1]|是|  
|**SQLSpecialColumns**|是|是|否|  
|**SQLStatistics**|是|是|否|  
|**SQLTablePrivileges**|是|是|否|  
|**SQLTables**|是|是|否|  
|**SQLTransact**|否|No[1]|是|  
  
 [1] 此函式已被取代，在 ODBC 3。*x*。 ODBC 3。*x*應用程式不應使用此函式。 不過，開啟 群組或 ISO CLI 相容的應用程式可以呼叫此函式。  
  
 [2] ODBC 3。*x*應用程式應該改用**SQLBindParameter**而非**SQLBindParam**。 不過，開啟 群組或 ISO CLI 相容的應用程式可以呼叫此函式。  
  
 [3] 的驅動程式撰寫人員應該注意到 ODBC 2。*x*資料行屬性使用，則必須支援 SQL_COLUMN_PRECISION、 SQL_COLUMN_SCALE 和 SQL_COLUMN_LENGTH **SQLColAttribute**。  
  
 [4] **SQLCopyDesc**跨屬於不同的驅動程式的連接複製描述項時，則部分實作由驅動程式管理員。 支援所需的驅動程式**SQLCopyDesc**跨兩個自己的連線。 這類函式**SQLDrivers**這會實作完全由驅動程式管理員，不會出現在這份清單。  
  
 [5] 在某些情況下，驅動程式可能需要支援此函式。 如需詳細資訊，請參閱此函式的參考頁面。  
  
 [6] 的驅動程式可以選擇支援**SQLGetFunctions**如果驅動程式所支援的函式集改變連接連接。
