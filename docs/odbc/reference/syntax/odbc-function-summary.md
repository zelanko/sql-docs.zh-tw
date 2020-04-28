---
title: ODBC 函數摘要 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], listed by task
ms.assetid: 7aa635da-e6b7-439f-8e9b-c3860e24de5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c10cc7880cf941a1490f963e21e8b44bc91db215
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298919"
---
# <a name="odbc-function-summary"></a>ODBC 函式摘要
下表列出 ODBC 函式，依工作類型分組，並包含一致性指定和每個函式的用途簡短描述。 如需一致性指派的詳細資訊，請參閱[ODBC 和標準 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)。 如需有關每個函式之語法和語義的詳細資訊，請參閱[ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 應用程式可以呼叫**SQLGetInfo**函數來取得驅動程式的一致性資訊。 若要取得驅動程式中特定函式支援的相關資訊，應用程式可以呼叫**SQLGetFunctions**。  
  
|工作|函式名稱|標準|目的|  
|----------|-------------------|-----------------|-------------|  
|連接到資料來源|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|取得環境、連接、語句或描述項控制碼。|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|依資料來源名稱、使用者識別碼和密碼連接到特定驅動程式。|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|依連接字串連接到特定驅動程式，或要求 [驅動程式管理員] 和 [驅動程式] 顯示使用者的連接對話方塊。|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|傳回連續層級的連接屬性和有效的屬性值。 針對每個連接屬性指定值時，會連接到資料來源。|  
|取得驅動程式和資料來源的相關資訊|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|傳回可用資料來源的清單。<br /><br /> 傳回已安裝驅動程式及其屬性的清單。|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|傳回特定驅動程式和資料來源的相關資訊。|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|傳回支援的驅動程式函式。|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|傳回支援的資料類型的相關資訊。|  
|設定和抓取驅動程式屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|設定連接屬性。<br /><br /> 傳回連接屬性的值。|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|設定環境屬性。|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|傳回環境屬性的值。|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|設定語句屬性。|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|傳回語句屬性的值。|  
|設定和抓取描述項欄位|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|傳回單一描述項欄位的值。<br /><br /> 傳回多個描述項欄位的值。|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|設定單一描述項欄位。|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|設定多個描述項欄位。|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|將描述元資訊從一個描述項控制碼複製到另一個。|  
|準備 SQL 要求|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|準備 SQL 語句以供稍後執行。|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|在 SQL 語句中指派參數的儲存體。|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|傳回與語句控制碼相關聯的資料指標名稱。|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|指定資料指標名稱。|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|設定控制資料指標行為的選項。|  
|提交要求|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|執行已備妥的陳述式。<br /><br /> 執行陳述式。|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|傳回驅動程式所轉譯之 SQL 語句的文字。|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|傳回語句中特定參數的描述。|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|傳回語句中的參數數目。|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|與**SQLPutData**搭配使用，以在執行時間提供參數資料。 （適用于 long 資料值）。|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|傳送參數的部分或所有資料值。 （適用于 long 資料值）。|  
|正在抓取結果和結果的相關資訊|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|傳回受 insert、update 或 delete 要求影響的資料列數目。<br /><br /> 傳回結果集中的資料行數目。|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|描述結果集中的資料行。|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|描述結果集中資料行的屬性。|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|指派結果資料行的儲存體，並指定資料類型。|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|傳回多個結果資料列。|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|傳回可滾動的結果資料列。|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|傳回結果集中一個資料列的部分或所有資料行。 （適用于 long 資料值）。|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|將資料指標置於提取的資料區塊內，並允許應用程式重新整理資料列集中的資料，或更新或刪除結果集中的資料。|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|執行大量插入和大量書簽作業，包括依書簽的更新、刪除和提取。|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|判斷是否有更多結果集可供使用，如果是的話，則會初始化下一個結果集的處理。|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|傳回其他診斷資訊（診斷資料結構的單一欄位）。|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|傳回其他診斷資訊（診斷資料結構的多個欄位）。|  
|取得資料來源系統資料表的相關資訊（目錄函數）|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 開啟群組|傳回一或多個資料表的資料行清單和相關聯的許可權。<br /><br /> 傳回指定資料表中的資料行名稱清單。|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|傳回組成外鍵之資料行名稱的清單（如果有指定的資料表存在）。|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|傳回構成資料表主鍵的資料行名稱清單。|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|傳回輸入和輸出參數的清單，以及組成指定程式之結果集的資料行。|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|傳回儲存在特定資料來源中的程式名稱清單。|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|開啟群組|傳回可唯一識別指定資料表中之資料列的最佳資料行集合的相關資訊，或當交易更新資料列中的任何值時，自動更新的資料行。|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|傳回單一資料表的統計資料，以及與資料表相關聯的索引清單。|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|傳回資料表的清單，以及與每個資料表相關聯的許可權。|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|開啟群組|傳回儲存在特定資料來源中的資料表名稱清單。|  
|終止語句|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|結束語句處理、捨棄暫止的結果，並選擇性地釋放與語句控制碼相關聯的所有資源。|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|關閉已經在語句控制碼上開啟的資料指標。|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|取消語句的處理。|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|取消語句或連接上的處理。|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|認可或回復交易。|  
|終止連接|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|關閉連接。<br /><br /> 釋放環境、連接、語句或描述項控制碼。|
