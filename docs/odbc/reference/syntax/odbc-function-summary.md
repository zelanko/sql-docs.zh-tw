---
title: ODBC 函式摘要 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6829f4f5197fca28944e5bc9d2f636f6624c9d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686516"
---
# <a name="odbc-function-summary"></a>ODBC 函式摘要
下表列出 ODBC 函數，依類型的工作，並包含指定的一致性及每個函式用途的簡短描述。 如需合規性表示法的詳細資訊，請參閱[ODBC 和標準 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)。 如需語法和語意，每個函式的詳細資訊，請參閱[ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 應用程式可以呼叫**SQLGetInfo**函式來取得驅動程式的合規性資訊。 若要取得支援的驅動程式中的特定函式的相關資訊，應用程式可以呼叫**SQLGetFunctions**。  
  
|工作|函數名稱|合規性|目的|  
|----------|-------------------|-----------------|-------------|  
|連接到資料來源|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|取得環境、 連接、 陳述式或描述元控制代碼。|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|連接到特定的驅動程式的資料來源名稱、 使用者識別碼和密碼。|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|連接字串或要求的驅動程式管理員和驅動程式顯示使用者的 [連線] 對話方塊，連接到特定的驅動程式。|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|傳回連接屬性及有效的屬性值的連續層級。 每個連接屬性中具有指定的值，當連接到資料來源。|  
|取得驅動程式和資料來源的相關資訊|[SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|傳回可用的資料來源的清單。<br /><br /> 傳回已安裝的驅動程式和其屬性的清單。|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|傳回特定的驅動程式和資料來源的相關資訊。|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|傳回支援的驅動程式函式。|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|傳回支援的資料類型的相關資訊。|  
|設定和擷取驅動程式屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|設定連接屬性。<br /><br /> 傳回連接屬性的值。|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|設定環境屬性。|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|傳回環境屬性的值。|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|設定陳述式屬性。|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|傳回陳述式屬性的值。|  
|設定和擷取描述項欄位|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|傳回單一的描述項欄位的值。<br /><br /> 傳回多個描述項欄位的值。|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|設定單一的描述項欄位。|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|設定多個描述項欄位。|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|複製一個描述項控制代碼的描述元資訊儲存到另一個。|  
|準備 SQL 要求|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|準備 SQL 陳述式，以便稍後執行。|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|指派儲存體中的 SQL 陳述式的參數。|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|傳回陳述式控制代碼相關聯的資料指標名稱。|  
||[SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|指定資料指標名稱。|  
||[SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|設定控制資料指標行為的選項。|  
|提交要求|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|執行已備妥的陳述式。<br /><br /> 執行陳述式。|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|傳回 SQL 陳述式的文字，因為驅動程式所轉譯。|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|陳述式中傳回的特定參數的描述。|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|陳述式中傳回參數的數目。|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|用於搭配**SQLPutData**提供在執行階段的參數資料。 （適用於 long 資料值。）|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|會傳送部分或所有參數的資料值。 （適用於 long 資料值。）|  
|擷取結果和結果的相關資訊|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|傳回受到 insert、 update 或 delete 要求的資料列數目。<br /><br /> 傳回結果集中的資料行數目。|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|描述結果集中的資料行。|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|描述結果集中的資料行的屬性。|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|指派結果資料行的儲存體，而指定的資料類型。|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|傳回多個結果資料列。|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|傳回可捲動的結果資料列。|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|傳回部分或全部的一個資料列結果的一個資料行的設定。 （適用於 long 資料值。）|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|將擷取的資料區塊中的資料指標，並允許應用程式來重新整理資料列集中的資料，或是更新或刪除在結果集中的資料。|  
||[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|會執行大量插入以及大量的書籤的作業，包括更新、 刪除和擷取書籤。|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|判斷是否有更多的結果會設定可用，並若是如此，初始化處理下一個結果集。|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|傳回的其他診斷資訊 （診斷的資料結構中的單一欄位）。|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|傳回的其他診斷資訊 （診斷的資料結構中的多個欄位）。|  
|取得資料來源的系統資料表 （目錄函數） 的相關資訊|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 開啟群組|傳回資料行和一個或多個資料表相關聯的權限的清單。<br /><br /> 傳回指定資料表中的資料行名稱清單。|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|傳回組成外部索引鍵的資料行名稱的清單，如果它們存在指定的資料表。|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|傳回資料表的主索引鍵所組成的資料行名稱的清單。|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|傳回輸入和輸出參數，以及構成結果集針對指定的程序的資料行的清單。|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|傳回儲存在特定資料來源中的程序名稱清單。|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|開啟群組|傳回一組最佳資料行可唯一識別指定的資料表中的資料列或交易更新資料列中的任何值時所自動更新的資料行的資訊。|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|傳回單一的資料表和索引與資料表相關聯的清單相關的統計資料。|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|傳回一份資料表，以及與每個資料表相關聯的權限。|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|開啟群組|傳回儲存在特定資料來源中的資料表名稱清單。|  
|終止陳述式|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|結束陳述式處理、 捨棄暫止的結果，並選擇性地釋放陳述式控制代碼相關聯的所有資源。|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|關閉已開啟的陳述式控制代碼的資料指標。|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|取消陳述式上的處理。|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|取消陳述式或連接上的處理。|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|認可或回復交易。|  
|終止連線|[SQLDisconnect](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|關閉連接。<br /><br /> 釋放環境、 連接、 陳述式或描述元控制代碼。|
