---
title: ODBC API 參考 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d56d6068b842256bd450844c7b163727e5d35f3d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653395"
---
# <a name="odbc-api-reference"></a>ODBC API 參考
在本節中的主題描述依字母順序的每個 ODBC 函式。 每個函式定義為 C 程式設計語言函式。 描述包含下列各項：  
  
-   用途  
  
-   ODBC 版本  
  
-   標準的 CLI 一致性層級  
  
-   語法  
  
-   引數  
  
-   傳回值  
  
-   診斷  
  
-   使用方式實作的相關註解  
  
-   程式碼範例  
  
-   相關的函式的參考  
  
 標準的 CLI 一致性層級可以是下列其中一項：ISO 92 開啟 [ODBC] 群組，或已被取代。 標記為 ISO 92 符合標準也會出現在 Open Group 第 1 版中，因為 Open Group 是純粹的 ISO 92 函式。 標記為 開啟群組符合規範的函式也會出現在 ODBC 3。*x*，因為 ODBC 3。*x*純 Open Group 第 1 版的超集。 標記為符合 ODBC 規範的函式會出現在沒有標準。 標記為已被取代的函式已被取代，在 ODBC 3。*x*。  
  
 處理診斷資訊所述[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函式描述。 SQLSTATE 值相關聯的文字就會包含提供條件的描述，但不是要指定特定的文字。  
  
> [!NOTE]  
>  如需 ODBC 函數的驅動程式專屬資訊，請參閱驅動程式區段。  
  
 本章節包含下列函式的主題：  
  
-   [SQLAllocConnect 函式](../../../odbc/reference/syntax/sqlallocconnect-function.md)  
  
-   [SQLAllocEnv 函式](../../../odbc/reference/syntax/sqlallocenv-function.md)  
  
-   [SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
-   [SQLAllocStmt 函式](../../../odbc/reference/syntax/sqlallocstmt-function.md)  
  
-   [SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)  
  
-   [SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)  
  
-   [SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)  
  
-   [SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)  
  
-   [SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)  
  
-   [SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)  
  
-   [SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)  
  
-   [SQLColAttribute 函式](../../../odbc/reference/syntax/sqlcolattribute-function.md)  
  
-   [SQLColAttributes 函式](../../../odbc/reference/syntax/sqlcolattributes-function.md)  
  
-   [SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)  
  
-   [SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)  
  
-   [SQLCompleteAsync 函式](../../../odbc/reference/syntax/sqlcompleteasync-function.md)  
  
-   [SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)  
  
-   [SQLCopyDesc 函式](../../../odbc/reference/syntax/sqlcopydesc-function.md)  
  
-   [SQLDataSources 函式](../../../odbc/reference/syntax/sqldatasources-function.md)  
  
-   [SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)  
  
-   [SQLDescribeParam 函式](../../../odbc/reference/syntax/sqldescribeparam-function.md)  
  
-   [SQLDisconnect 函式](../../../odbc/reference/syntax/sqldisconnect-function.md)  
  
-   [SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)  
  
-   [SQLDrivers 函式](../../../odbc/reference/syntax/sqldrivers-function.md)  
  
-   [SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)  
  
-   [SQLError 函式](../../../odbc/reference/syntax/sqlerror-function.md)  
  
-   [SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)  
  
-   [SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)  
  
-   [SQLExtendedFetch 函式](../../../odbc/reference/syntax/sqlextendedfetch-function.md)  
  
-   [SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)  
  
-   [SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)  
  
-   [SQLForeignKeys 函式](../../../odbc/reference/syntax/sqlforeignkeys-function.md)  
  
-   [SQLFreeConnect 函式](../../../odbc/reference/syntax/sqlfreeconnect-function.md)  
  
-   [SQLFreeEnv 函式](../../../odbc/reference/syntax/sqlfreeenv-function.md)  
  
-   [SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
-   [SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)  
  
-   [SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
-   [SQLGetConnectOption 函式](../../../odbc/reference/syntax/sqlgetconnectoption-function.md)  
  
-   [SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)  
  
-   [SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
-   [SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)  
  
-   [SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)  
  
-   [SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
-   [SQLGetDiagRec 函式](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
-   [SQLGetEnvAttr 函式](../../../odbc/reference/syntax/sqlgetenvattr-function.md)  
  
-   [SQLGetFunctions 函式](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
-   [SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
-   [SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
-   [SQLGetStmtOption 函式](../../../odbc/reference/syntax/sqlgetstmtoption-function.md)  
  
-   [SQLGetTypeInfo 函式](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
-   [SQLMoreResults 函式](../../../odbc/reference/syntax/sqlmoreresults-function.md)  
  
-   [SQLNativeSql 函式](../../../odbc/reference/syntax/sqlnativesql-function.md)  
  
-   [SQLNumParams 函式](../../../odbc/reference/syntax/sqlnumparams-function.md)  
  
-   [SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)  
  
-   [SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)  
  
-   [SQLParamOptions 函式](../../../odbc/reference/syntax/sqlparamoptions-function.md)  
  
-   [SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)  
  
-   [SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)  
  
-   [SQLProcedureColumns 函式](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)  
  
-   [SQLProcedures 函式](../../../odbc/reference/syntax/sqlprocedures-function.md)  
  
-   [SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)  
  
-   [SQLRowCount 函式](../../../odbc/reference/syntax/sqlrowcount-function.md)  
  
-   [SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)  
  
-   [SQLSetConnectOption 函式](../../../odbc/reference/syntax/sqlsetconnectoption-function.md)  
  
-   [SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)  
  
-   [SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)  
  
-   [SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
-   [SQLSetEnvAttr 函式](../../../odbc/reference/syntax/sqlsetenvattr-function.md)  
  
-   [SQLSetParam 函式](../../../odbc/reference/syntax/sqlsetparam-function.md)  
  
-   [SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
-   [SQLSetScrollOptions 函式](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)  
  
-   [SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)  
  
-   [SQLSetStmtOption 函式](../../../odbc/reference/syntax/sqlsetstmtoption-function.md)  
  
-   [SQLSpecialColumns 函式](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)  
  
-   [SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)  
  
-   [SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)  
  
-   [SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)  
  
-   [SQLTransact 函式](../../../odbc/reference/syntax/sqltransact-function.md)
