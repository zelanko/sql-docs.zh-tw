---
title: ODBC 功能摘要 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298919"
---
# <a name="odbc-function-summary"></a>ODBC 函式摘要
下表列出了 ODBC 函數,按任務類型分組,並包括符合性指定和每個函數用途的簡要說明。 有關符合性名稱的詳細資訊,請參閱[ODBC 和標準 CLI](../../../odbc/reference/odbc-and-the-standard-cli.md)。 有關每個函數的語法和語義的詳細資訊,請參閱[ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)。  
  
 應用程式可以調用**SQLGetInfo**函數來獲取有關驅動程式的一致性資訊。 要取得有關驅動程式中特定函數的資訊,應用程式可以呼叫**SQLGet 函數**。  
  
|Task|函式名稱|一致性|目的|  
|----------|-------------------|-----------------|-------------|  
|連接到資料來源|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|ISO 92|獲取環境、連接、語句或描述符句柄。|  
||[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|ISO 92|按數據來源名稱、使用者 ID 和密碼連接到特定驅動程式。|  
||[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|ODBC|通過連接字串連接到特定驅動程式,或請求驅動程式管理器和驅動程式顯示使用者的連接對話方塊。|  
||[SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|ODBC|返回連接屬性和有效屬性值的連續級別。 為每個連接屬性指定值後,連接到數據源。|  
|取得有關驅動程式和資料來源的資訊|[SQLData來源](../../../odbc/reference/syntax/sqldatasources-function.md)<br /><br /> [SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|ISO 92<br /><br /> ODBC|傳回可用資料來源的清單。<br /><br /> 返回已安裝驅動程式的清單及其屬性。|  
||[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)|ISO 92|返回有關特定驅動程序和數據源的資訊。|  
||[SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md)|ISO 92|返回支援的驅動程式函數。|  
||[SQLGetTypeInfo](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)|ISO 92|返回有關受支持數據類型的資訊。|  
|設定與檢索驅動程式屬性|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)<br /><br /> [SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|ISO 92<br /><br /> ISO 92|設置連接屬性。<br /><br /> 返回連接屬性的值。|  
||[SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|ISO 92|設置環境屬性。|  
||[SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|ISO 92|返回環境屬性的值。|  
||[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|ISO 92|設置語句屬性。|  
||[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|ISO 92|返回語句屬性的值。|  
|設定與檢索描述符位|[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)<br /><br /> [SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|ISO 92<br /><br /> ISO 92|返回單個描述符欄位的值。<br /><br /> 返回多個描述符位的值。|  
||[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|ISO 92|設定單個描述符位。|  
||[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|ISO 92|設置多個描述符位。|  
||[SQLCopyDesc](../../../odbc/reference/syntax/sqlcopydesc-function.md)|ISO 92|將描述符資訊從一個描述符句柄複製到另一個描述符句柄。|  
|準備 SQL 請求|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|ISO 92|準備 SQL 語句供以後執行。|  
||[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|ODBC|在 SQL 語句中為參數分配存儲。|  
||[SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|ISO 92|返回與語句句柄關聯的游標名稱。|  
||[SQLSetCursor 名稱](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|ISO 92|指定游標名稱。|  
||[SQLSetScroll 選項](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|ODBC|設置控制游標行為的選項。|  
|提交要求|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)<br /><br /> [SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|ISO 92<br /><br /> ISO 92|執行已備妥的陳述式。<br /><br /> 執行陳述式。|  
||[SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md)|ODBC|返回驅動程式翻譯的 SQL 語句的文本。|  
||[SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|ODBC|返回語句中特定參數的說明。|  
||[SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|ISO 92|返回語句中的參數數。|  
||[SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|ISO 92|與**SQLPutData**結合使用,在執行時提供參數數據。 (對於長數據值很有用。|  
||[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|ISO 92|發送參數的全部或部分資料值。 (對於長數據值很有用。|  
|檢索結果和結果資訊|[SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md)<br /><br /> [SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|ISO 92<br /><br /> ISO 92|返回受插入、更新或刪除請求影響的行數。<br /><br /> 傳回結果集中的資料行數目。|  
||[SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|ISO 92|描述結果集中的列。|  
||[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|ISO 92|描述結果集中列的屬性。|  
||[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|ISO 92|為結果列分配存儲並指定數據類型。|  
||[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|ISO 92|返回多個結果行。|  
||[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|ISO 92|返回可滾動的結果行。|  
||[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)|ISO 92|返回結果集一行的一列的一部分或全部。 (對於長數據值很有用。|  
||[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|ODBC|將游標定位在提取的數據塊中,並允許應用程式刷新行集中的數據或更新或刪除結果集中的數據。|  
||[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|ODBC|執行批量插入和批量書籤操作,包括按書籤更新、刪除和提取。|  
||[SQLMoreResults](../../../odbc/reference/syntax/sqlmoreresults-function.md)|ODBC|確定是否有更多可用的結果集,如果是,則初始化下一個結果集的處理。|  
||[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|ISO 92|返回其他診斷資訊(診斷數據結構的單個字段)。|  
||[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|ISO 92|返回其他診斷資訊(診斷數據結構的多個字段)。|  
|取得關於資料來源的系統表(目錄函數)的資訊|[SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)<br /><br /> [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|ODBC<br /><br /> 開啟群組|返回一個或多個表的列和關聯許可權的清單。<br /><br /> 傳回指定表中的列名稱清單。|  
||[SQLForeignKeys](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|ODBC|返回構成外鍵的列名稱的清單(如果它們存在於指定的表)。|  
||[SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|ODBC|返回構成表主鍵的列名稱的清單。|  
||[SQLProcedureColumns](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|ODBC|傳回輸入和輸出參數的清單,以及構成指定過程的結果集的列。|  
||[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)|ODBC|返回存儲在特定數據源中的過程名稱清單。|  
||[SQLSpecialColumns](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|開啟群組|返回有關唯一標識指定表中的行的最佳列集的資訊,或者當事務更新行中的任何值時自動更新的列的資訊。|  
||[SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|ISO 92|返回有關單個表的統計資訊以及與表關聯的索引清單。|  
||[SQLTablePrivileges](../../../odbc/reference/syntax/sqltableprivileges-function.md)|ODBC|返回表清單以及與每個表關聯的許可權。|  
||[SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|開啟群組|返回存儲在特定數據源中的表名稱的清單。|  
|終止敘述|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|ISO 92|結束語句處理,丟棄掛起的結果,並且(可選)釋放與語句句柄關聯的所有資源。|  
||[SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md)|ISO 92|關閉已在語句句柄上打開的游標。|  
||[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|ISO 92|取消對語句的處理。|  
||[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|ODBC|取消對語句或連接的處理。|  
||[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)|ISO 92|提交或回滾事務。|  
|終止連線|[SQL 斷線](../../../odbc/reference/syntax/sqldisconnect-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)|ISO 92<br /><br /> ISO 92|關閉連接。<br /><br /> 釋放環境、連接、語句或描述符句柄。|
