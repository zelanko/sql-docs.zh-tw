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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300358"
---
# <a name="writing-odbc-3x-drivers"></a>撰寫 ODBC 3.x 驅動程式
下表顯示 ODBC 3 中的函數支援。*x*驅動程式和 odbc 應用程式，以及在針對 ODBC 3 呼叫函數時，驅動程式管理員所執行的對應。*x*驅動程式。  
  
|函式|支援<br /><br /> 依據<br /><br /> ODBC 3。*x*<br /><br /> driver?|支援<br /><br /> 依據<br /><br /> ODBC 3。*x*<br /><br /> 應用程式?|對應/支援<br /><br /> 由 ODBC 3 所進行。*x*<br /><br /> 驅動程式管理員到<br /><br /> ODBC 3。*x*驅動程式？|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|否|否 [1]|是|  
|**SQLAllocEnv**|否|否 [1]|是|  
|**SQLAllocHandle**|是|是|否|  
|**SQLAllocStmt**|否|否 [1]|是|  
|**SQLBindCol**|是|是|否|  
|**SQLBindParam**|否|是 [2]|是|  
|**SQLBindParameter**|是|是|否|  
|**SQLBrowseConnect**|是|是|否|  
|**SQLBulkOperations**|是|是|否|  
|**SQLCancel**|是|是|否|  
|**SQLCloseCursor**|是|是|否|  
|**SQLColAttribute**|是|是|否|  
|**SQLColAttributes**|否 [3]|否|是|  
|**SQLColumnPrivileges**|是|是|否|  
|**SQLColumns**|是|是|否|  
|**SQLConnect**|是|是|否|  
|**SQLCopyDesc**|是|是|是 [4]|  
|**SQLDataSources**|否|是|是|  
|**SQLDescribeCol**|是|是|否|  
|**SQLDescribeParam**|是|是|否|  
|**SQLDisconnect**|是|是|否|  
|**SQLDriverConnect**|是|是|否|  
|**SQLDrivers**|否|是|是|  
|**SQLEndTran**|是|是|否|  
|**SQLError**|否|否 [1]|是|  
|**SQLExecDirect**|是|是|否|  
|**SQLExecute**|是|是|否|  
|**SQLExtendedFetch**|是|否|否|  
|**SQLFetch**|是|是|否|  
|**SQLFetchScroll**|是|是|否|  
|**SQLForeignKeys**|是|是|否|  
|**SQLFreeConnect**|否|是 [1]|是|  
|**SQLFreeEnv**|否|是 [1]|是|  
|**SQLFreeHandle**|是|是|否|  
|**SQLFreeStmt**|是|是|否|  
|**SQLGetConnectAttr**|是|是|否|  
|**SQLGetConnectOption**|否 [5]|否 [1]|是|  
|**SQLGetCursorName**|是|是|否|  
|**SQLGetData**|是|是|否|  
|**SQLGetDescField**|是|是|否|  
|**SQLGetDescRec**|是|是|否|  
|**SQLGetDiagField**|是|是|否|  
|**SQLGetDiagRec**|是|是|否|  
|**SQLGetEnvAttr**|是|是|否|  
|**SQLGetFunctions**|否 [6]|是|是|  
|**SQLGetInfo**|是|是|否|  
|**SQLGetStmtAttr**|是|是|否|  
|**SQLGetStmtOption**|否 [5]|否 [1]|是|  
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
|**SQLSetConnectOption**|否 [5]|否 [1]|是|  
|**SQLSetCursorName**|是|是|否|  
|**SQLSetDescField**|是|是|否|  
|**SQLSetDescRec**|是|是|否|  
|**SQLSetEnvAttr**|是|是|否|  
|**SQLSetPos**|是|是|否|  
|**SQLSetParam**|否|否|是|  
|**SQLSetScrollOption**|是|是|否|  
|**SQLSetStmtAttr**|是|是|否|  
|**SQLSetStmtOption**|否 [5]|否 [1]|是|  
|**SQLSpecialColumns**|是|是|否|  
|**SQLStatistics**|是|是|否|  
|**SQLTablePrivileges**|是|是|否|  
|**SQLTables**|是|是|否|  
|**SQLTransact**|否|否 [1]|是|  
  
 [1] 這個函數在 ODBC 3 中已被取代。*x*。 ODBC 3。*x*應用程式不應該使用這個函數。 不過，開放式群組或 ISO CLI 相容的應用程式可以呼叫此函式。  
  
 [2] ODBC 3。*x*應用程式應使用**SQLBindParameter** ，而不是**SQLBindParam**。 不過，開放式群組或 ISO CLI 相容的應用程式可以呼叫此函式。  
  
 [3] 驅動程式寫入器應該注意 ODBC 2。*x* SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE 和 SQL_COLUMN_LENGTH 的資料行屬性必須與**SQLColAttribute**支援。  
  
 [4] **SQLCopyDesc**由驅動程式管理員在每個屬於不同驅動程式的連接之間進行複製時，部分執行。 需要驅動程式，以支援兩個其本身連接的**SQLCopyDesc** 。 **SQLDrivers**這類函式（由驅動程式管理員單獨執行）不會顯示在這份清單上。  
  
 [5] 在某些情況下，驅動程式可能需要支援此功能。 如需詳細資訊，請參閱此函式的參考頁面。  
  
 [6] 如果驅動程式支援的一組函式因連接連線而有所不同，驅動程式可以選擇支援**SQLGetFunctions** 。
