---
title: SQLGetFunctions 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ac3d24b1213096be20658fb48dbfe9a6d39df8f
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206967"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLGetFunctions**傳回驅動程式是否支援特定的 ODBC 函式的相關資訊。 此函式被實作在驅動程式管理員;它也可以實作驅動程式中。 如果驅動程式會實作**SQLGetFunctions**，驅動程式管理員驅動程式中呼叫函式。 否則，它會執行函式本身。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *FunctionId*  
 [輸入]A **#define**識別感興趣; 的 ODBC 函數的值**SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**。 **SQL_API_ODBC3_ALL_FUNCTIONS**由 ODBC 3 *.x*應用程式，以判斷支援的 ODBC 3 *.x*和先前的函式。 **SQL_API_ALL_FUNCTIONS**由 ODBC 2 *.x*應用程式，以判斷支援的 ODBC 2 *.x*和先前的函式。  
  
 取得一份 **#define**識別 ODBC 函數的值，請參閱 「 註解。"中的資料表  
  
 *SupportedPtr*  
 [輸出] 如果*FunctionId*可識別單一的 ODBC 函式*SupportedPtr*指向單一 SQLUSMALLINT 值，這是 SQL_TRUE 的驅動程式，和 SQL_FALSE 是否支援指定的函式，如果不是支援。  
  
 如果*FunctionId*是 SQL_API_ODBC3_ALL_FUNCTIONS， *SupportedPtr*指向項目數等於 SQL_API_ODBC3_ALL_FUNCTIONS_SIZE SQLSMALLINT 陣列。 這個陣列會被視為可用來判斷是否 ODBC 3 4000 位元點陣圖的驅動程式管理員所 *.x*或 earlier 函數支援。 若要判斷函式支援稱為 SQL_FUNC_EXISTS 巨集。 （請參閱 「 註解。"）ODBC 3 *.x*應用程式可以呼叫**SQLGetFunctions**具有對其中一個 ODBC 3 SQL_API_ODBC3_ALL_FUNCTIONS *.x* ] 或 [ODBC 2 *.x*驅動程式。  
  
 如果*FunctionId*是 SQL_API_ALL_FUNCTIONS， *SupportedPtr*指向 SQLUSMALLINT 陣列的 100 個元素。 陣列以編製索引 **#define**所使用的值*FunctionId*來識別每個 ODBC 函式中，陣列的某些項目是未使用和保留供日後使用。 項目是 SQL_TRUE，如果它會識別 ODBC 2 *.x*或驅動程式支援的舊版函式。 如果它找出驅動程式不支援的 ODBC 函式，或不會識別 ODBC 函數，它就會是 SQL_FALSE。  
  
 陣列中傳回 **SupportedPtr*使用以零為起始的索引。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetFunctions**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_DBC 並*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetFunctions** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------|-----|-----------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) **SQLGetFunctions**之前已呼叫**SQLConnect**， **SQLBrowseConnect**，或**SQLDriverConnect**。<br /><br /> (DM) **SQLBrowseConnect**針對呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*ConnectionHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY095|函數類型超出範圍|(DM) 無效*FunctionId*指定的值。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
  
## <a name="comments"></a>註解  
 **SQLGetFunctions**一律會傳回所**SQLGetFunctions**， **SQLDataSources**，和**SQLDrivers**支援。 這是因為會實作這些函式可以在驅動程式管理員。 驅動程式管理員會將 ANSI 函式對應至對應的 Unicode 函式，如果 Unicode 函式存在，而且如果 ANSI 函式存在，將對應 Unicode 函式的對應的 ANSI 函式。 如需有關如何使用應用程式資訊**SQLGetFunctions**，請參閱[介面一致性層級](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 下列是有效值的清單*FunctionId*符合 ISO 92 標準相容性層級的函式：  
  
|FunctionId 值|FunctionId 值|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETENVATTR|  
|SQL_API_SQLCONNECT|SQL_API_SQLGETFUNCTIONS|  
|SQL_API_SQLCOPYDESC|SQL_API_SQLGETINFO|  
|SQL_API_SQLDATASOURCES|SQL_API_SQLGETSTMTATTR|  
|SQL_API_SQLDESCRIBECOL|SQL_API_SQLGETTYPEINFO|  
|SQL_API_SQLDISCONNECT|SQL_API_SQLNUMRESULTCOLS|  
|SQL_API_SQLDRIVERS|SQL_API_SQLPARAMDATA|  
|SQL_API_SQLENDTRAN|SQL_API_SQLPREPARE|  
|SQL_API_SQLEXECDIRECT|SQL_API_SQLPUTDATA|  
|SQL_API_SQLEXECUTE|SQL_API_SQLROWCOUNT|  
|SQL_API_SQLFETCH|SQL_API_SQLSETCONNECTATTR|  
|SQL_API_SQLFETCHSCROLL|SQL_API_SQLSETCURSORNAME|  
|SQL_API_SQLFREEHANDLE|SQL_API_SQLSETDESCFIELD|  
|SQL_API_SQLFREESTMT|SQL_API_SQLSETDESCREC|  
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETENVATTR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 下列是有效值的清單*FunctionId*符合 Open Group 標準相容性層級的函式：  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 下列是有效值的清單*FunctionId*符合 ODBC 標準相容性層級的函式。  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS [1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] 時使用的 ODBC 2 *.x*驅動程式**SQLBulkOperations**會傳回只支援兩個動作是否為 true: ODBC 2 *.x*驅動程式支援**SQLSetPos**，和類型資訊，請 SQL_POS_OPERATIONS 傳回所設定的 SQL_POS_ADD 位元。  
  
 下列是有效值的清單*FunctionId*導入在 ODBC 3.8 或更新版本的函式：  
  
|FunctionId 值|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle**會傳回只支援此驅動程式支援同時**SQLCancel**並**SQLCancelHandle**。 如果**SQLCancel**支援，但**SQLCancelHandle**不是，應用程式仍然可以呼叫**SQLCancelHandle**陳述式控制代碼，因為它會對應到**SQLCancel**。  
  
## <a name="sqlfuncexists-macro"></a>SQL_FUNC_EXISTS 巨集  
 SQL_FUNC_EXISTS (*SupportedPtr*， *FunctionID*) 巨集用來判斷支援的 ODBC 3 *.x*或先前的函式之後**SQLGetFunctions**已使用呼叫*FunctionId* SQL_API_ODBC3_ALL_FUNCTIONS 引數。 應用程式會呼叫與 SQL_FUNC_EXISTS *SupportedPtr*引數設定為*SupportedPtr*傳入*SQLGetFunctions*，並使用*FunctionID*引數設定為 **#define**函式。 SQL_FUNC_EXISTS 否則傳回支援的函式，如果 SQL_TRUE 和 SQL_FALSE。  
  
> [!NOTE]
>  使用 ODBC 2 時 *.x*驅動程式，而 ODBC 3 *.x*驅動程式管理員會傳回 SQL_TRUE，如**SQLAllocHandle**並**SQLFreeHandle**因為**SQLAllocHandle**會對應到**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**，及因為**SQLFreeHandle**對應至**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**。 **SQLAllocHandle**或是**SQLFreeHandle**具有*HandleType* SQL_HANDLE_DESC 引數不支援，不過，即使函式中，會傳回 SQL_TRUE，因為沒有任何ODBC 2 *.x*將在此情況下對應至函式。  
  
## <a name="code-example"></a>程式碼範例  
 下列三個範例顯示如何使用應用程式**SQLGetFunctions**決定了驅動程式是否支援**SQLTables**， **SQLColumns**，和**SQLStatistics**。 如果驅動程式不支援這些函式，應用程式中斷連線的驅動程式。 第一個範例會呼叫**SQLGetFunctions**一次，每個函式。  
  
```  
SQLUSMALLINT TablesExists, ColumnsExists, StatisticsExists;  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
  
retcodeTables = SQLGetFunctions(hdbc, SQL_API_SQLTABLES, &TablesExists);  
retcodeColumns = SQLGetFunctions(hdbc, SQL_API_SQLCOLUMNS, &ColumnsExists);  
retcodeStatistics = SQLGetFunctions(hdbc, SQL_API_SQLSTATISTICS, &StatisticsExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (retcodeTables == SQL_SUCCESS && TablesExists == SQL_TRUE &&   
retcodeColumns == SQL_SUCCESS && ColumnsExists == SQL_TRUE &&   
retcodeStatistics == SQL_SUCCESS && StatisticsExists == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 在第二個範例中，ODBC 3.x 應用程式會呼叫**SQLGetFunctions**並將它在其中傳遞陣列**SQLGetFunctions**傳回所有的 ODBC 的相關資訊 3.x 和先前的函式。  
  
```  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[SQL_API_ODBC3_ALL_FUNCTIONS_SIZE];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ODBC3_ALL_FUNCTIONS, fExists);  
  
// SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver.  
if (reccode == SQL_SUCCESS &&   
SQL_FUNC_EXISTS(fExists, SQL_API_SQLTABLES) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLCOLUMNS) == SQL_TRUE &&  
   SQL_FUNC_EXISTS(fExists, SQL_API_SQLSTATISTICS) == SQL_TRUE)   
{  
  
   // Continue with application  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
 第三個範例是 ODBC 2.x 應用程式呼叫**SQLGetFunctions**並將它在其中傳遞的 100 個元素陣列**SQLGetFunctions**傳回資訊所有 ODBC 2.x 和先前的函式。  
  
```  
#define FUNCTIONS 100  
  
RETCODE retcodeTables, retcodeColumns, retcodeStatistics  
SQLUSMALLINT fExists[FUNCTIONS];  
  
retcode = SQLGetFunctions(hdbc, SQL_API_ALL_FUNCTIONS, fExists);  
  
/* SQLGetFunctions is completed successfully and SQLTables, SQLColumns, and SQLStatistics are supported by the driver. */  
if (retcode == SQL_SUCCESS &&   
fExists[SQL_API_SQLTABLES] == SQL_TRUE &&  
   fExists[SQL_API_SQLCOLUMNS] == SQL_TRUE &&  
   fExists[SQL_API_SQLSTATISTICS] == SQL_TRUE)   
{  
  
   /* Continue with application */  
  
}  
  
SQLDisconnect(hdbc);  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回的驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
