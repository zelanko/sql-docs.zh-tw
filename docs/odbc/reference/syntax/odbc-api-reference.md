---
title: "ODBC API 參考 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apitype: dllExport
ms.assetid: b7a49774-f458-44ce-9a04-a0457501405b
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 348b9a8bead318f99f0ab85f0f961e64a56770f5
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="odbc-api-reference"></a>ODBC 應用程式開發介面參考
本節中的主題會描述每個 ODBC 函數，依字母順序。 每個函式定義為 C 程式設計語言的函式。 描述包含下列各項：  
  
-   目的  
  
-   ODBC 版本  
  
-   標準的 CLI 一致性層級  
  
-   語法  
  
-   引數  
  
-   傳回值  
  
-   診斷  
  
-   使用方式和實作的相關註解  
  
-   程式碼範例  
  
-   相關函數的參考  
  
 標準的 CLI 一致性層級可以是下列其中之一： ISO 92、 Open Group、 ODBC 或已過時。 標記為 ISO 92 標準也會出現在第 1 版的 Open Group Open Group 的 ISO 92 純超集，因為函式。 標記為符合開啟群組的函式也會出現在 ODBC 3。*x*，因為 ODBC 3。*x*是純粹的 Open Group 第 1 版。 標記為 ODBC 相容的函式會出現在任何標準。 標記為已被取代的函式已被取代，在 ODBC 3。*x*。  
  
 處理診斷資訊述[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)函式描述。 SQLSTATE 值相關聯的文字就會包含提供條件的描述，但不是能指定特定的文字。  
  
> [!NOTE]  
>  如需 ODBC 函數的驅動程式特定資訊，請參閱驅動程式 」 一節。  
  
 本節包含主題的下列功能：  
  
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
