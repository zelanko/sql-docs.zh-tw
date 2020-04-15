---
title: 編寫 ODBC 3.x 驅動程式 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300358"
---
# <a name="writing-odbc-3x-drivers"></a>撰寫 ODBC 3.x 驅動程式
下表顯示了 ODBC 3 中的功能支援。*x*驅動程式和 ODBC 應用程式,以及驅動程式管理員在針對 ODBC 3 調用函數時執行的映射。*x*驅動程式。  
  
|函式|支援<br /><br /> 由<br /><br /> ODBC 3.*x*<br /><br /> 司機?|支援<br /><br /> 由<br /><br /> ODBC 3.*x*<br /><br /> 應用?|映射/支援<br /><br /> 由 ODBC 3。*x*<br /><br /> 驅動程式管理員到<br /><br /> ODBC 3.*x*驅動程式?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAlloc 連線**|否|否[1]|是|  
|**SQLAllocEnv**|否|否[1]|是|  
|**SQLAllocHandle**|是|是|否|  
|**SQLAllocStmt**|否|否[1]|是|  
|**SQLBindCol**|是|是|否|  
|**SQLBindParam**|否|是[2]|是|  
|**SQLBindParameter**|是|是|否|  
|**SQLBrowseConnect**|是|是|否|  
|**SQLBulk 操作**|是|是|否|  
|**SQLCancel**|是|是|否|  
|**SQLCloseCursor**|是|是|否|  
|**SQLColAttribute**|是|是|否|  
|**SQLColattributes**|否[3]|否|是|  
|**SQLColumnPrivileges**|是|是|否|  
|**SQLColumns**|是|是|否|  
|**SQLConnect**|是|是|否|  
|**SQLCopyDesc**|是|是|是[4]|  
|**SQLData來源**|否|是|是|  
|**SQLDescribeCol**|是|是|否|  
|**SQLDescribeParam**|是|是|否|  
|**SQL 斷線**|是|是|否|  
|**SQLDriverConnect**|是|是|否|  
|**SQLDrivers**|否|是|是|  
|**SQLEndTran**|是|是|否|  
|**SQLError**|否|否[1]|是|  
|**SQLExecDirect**|是|是|否|  
|**SQLExecute**|是|是|否|  
|**SQL 延伸**|是|否|否|  
|**SQLFetch**|是|是|否|  
|**SQLFetchScroll**|是|是|否|  
|**SQLForeignKeys**|是|是|否|  
|**SQLFreeConnect**|否|是[1]|是|  
|**SQLFreeEnv**|否|是[1]|是|  
|**SQLFreeHandle**|是|是|否|  
|**SQLFreeStmt**|是|是|否|  
|**SQLGetConnectAttr**|是|是|否|  
|**SQLGetConnectOption**|否[5]|否[1]|是|  
|**SQLGetCursorName**|是|是|否|  
|**SQLGetData**|是|是|否|  
|**SQLGetDescField**|是|是|否|  
|**SQLGetDescRec**|是|是|否|  
|**SQLGetDiagField**|是|是|否|  
|**SQLGetDiagRec**|是|是|否|  
|**SQLGetEnvAttr**|是|是|否|  
|**SQLGetFunctions**|否[6]|是|是|  
|**SQLGetInfo**|是|是|否|  
|**SQLGetStmtAttr**|是|是|否|  
|**SQLGetStmtOption**|否[5]|否[1]|是|  
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
|**SQLSet 連線選項**|否[5]|否[1]|是|  
|**SQLSetCursor 名稱**|是|是|否|  
|**SQLSetDescField**|是|是|否|  
|**SQLSetDescRec**|是|是|否|  
|**SQLSetEnvAttr**|是|是|否|  
|**SQLSetPos**|是|是|否|  
|**SQLSetParam**|否|否|是|  
|**SQLSetScrollOption**|是|是|否|  
|**SQLSetStmtAttr**|是|是|否|  
|**SQLSetStmtOption**|否[5]|否[1]|是|  
|**SQLSpecialColumns**|是|是|否|  
|**SQLStatistics**|是|是|否|  
|**SQLTablePrivileges**|是|是|否|  
|**SQLTables**|是|是|否|  
|**SQLTransact**|否|否[1]|是|  
  
 [1] 此函數在 ODBC 3 中被棄用。*x*. . ODBC 3.*x*應用程式不應使用此函數。 但是,開放組或符合 ISO CLI 的應用程式可以調用此功能。  
  
 [2] ODBC 3。*x*應用程式應使用**SQLBind 參數**而不是**SQLBindParam**。 但是,開放組或符合 ISO CLI 的應用程式可以調用此功能。  
  
 [3] 驅動程式編寫器應注意 ODBC 2。*x* **sqlColattribute**必須支援 SQL_COLUMN_PRECISION、SQL_COLUMN_SCALE 和SQL_COLUMN_LENGTH的 x 列屬性。  
  
 [4] **SQLCopyDesc**部分由驅動程式管理器實現,當跨屬於不同驅動程式的連接複製描述符時。 驅動程式需要跨兩個連接支援**SQLCopyDesc。** 僅由驅動程式管理器實現的**SQLDriver**等函數不會顯示在此清單中。  
  
 [5] 在某些情況下,驅動程式可能需要支援此功能。 有關詳細資訊,請參閱此函數的參考頁。  
  
 [6] 如果驅動程式支援的函數集因連線而異,驅動程式可以選擇支援**SQLGet 功能**。
