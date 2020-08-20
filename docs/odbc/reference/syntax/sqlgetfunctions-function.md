---
description: SQLGetFunctions 函數
title: SQLGetFunctions 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetFunctions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetFunctions
helpviewer_keywords:
- SQLGetFunctions function [ODBC]
ms.assetid: 0451d2f9-0f4f-46ba-b252-670956a52183
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 396c677c6052176240afaa86e02c5f52ba4739b8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460981"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetFunctions** 會傳回有關驅動程式是否支援特定 ODBC 函數的資訊。 此函數會在驅動程式管理員中執行;它也可以在驅動程式中執行。 如果驅動程式會執行 **SQLGetFunctions**，驅動程式管理員會在驅動程式中呼叫函式。 否則，它會執行函數本身。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入] 連線控制代碼。  
  
 *FunctionId*  
 輸出識別感興趣之 ODBC 函數的 **#define** 值; **SQL_API_ODBC3_ALL_FUNCTIONS orSQL_API_ALL_FUNCTIONS**。 ODBC*3.x 應用程式*會使用**SQL_API_ODBC3_ALL_FUNCTIONS**來判斷 odbc 3.x 和舊版函式的*支援。* ODBC*2.x 應用程式*會使用**SQL_API_ALL_FUNCTIONS**來判斷 odbc*2.x 和先前*函數的支援。  
  
 如需識別 ODBC 函數的 **#define** 值清單，請參閱「批註」中的資料表。  
  
 *SupportedPtr*  
 出 如果 *FunctionId* 識別單一 ODBC 函數， *SupportedPtr* 會指向單一 SQLUSMALLINT 值，如果驅動程式支援指定的函式，就會 SQL_TRUE 這個值，如果不支援，則會 SQL_FALSE。  
  
 如果 *FunctionId* 是 SQL_API_ODBC3_ALL_FUNCTIONS， *SUPPORTEDPTR* 會指向 SQLSMALLINT 陣列，其中有數個元素等於 SQL_API_ODBC3_ALL_FUNCTIONS_SIZE。 驅動程式管理員會將這個陣列視為4000位點陣圖，可用來判斷是否支援 ODBC*3.x 或更早的函* 式。 呼叫 SQL_FUNC_EXISTS 宏以判斷函數支援。  (請參閱「批註」。) ODBC*3.x 應用程式*可以針對 odbc*3.x 或 odbc* 2.x 驅動程式使用 SQL_API_ODBC3_ALL_FUNCTIONS 來呼叫**SQLGetFunctions** *。*  
  
 如果 *FunctionId* 是 SQL_API_ALL_FUNCTIONS， *SupportedPtr* 會指向100元素的 SQLUSMALLINT 陣列。 陣列是以*FunctionId*用來識別每個 ODBC 函數的 **#define**值來編制索引;陣列的一些元素未使用，並保留供日後使用。 如果專案識別出驅動程式所支援的 ODBC*2.x 或更* 早的函式，就會 SQL_TRUE 專案。 如果它識別出驅動程式不支援的 ODBC 函數，或未識別 ODBC 函數，則會 SQL_FALSE 它。  
  
 **SupportedPtr* 中傳回的陣列會使用以零為基礎的索引。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetFunctions**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DBC）和*ConnectionHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLGetFunctions** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------|-----|-----------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤|在**SQLConnect**、 **SQLBrowseConnect**或**SQLDriverConnect**之前呼叫 (DM) **SQLGetFunctions** 。<br /><br /> 針對*ConnectionHandle*呼叫 (DM) **SQLBrowseConnect** ，並傳回 SQL_NEED_DATA。 在 **SQLBrowseConnect** 傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS 之前，會呼叫此函數。<br /><br /> 針對*ConnectionHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY095|函數類型超出範圍| (DM) 指定了不正確 *FunctionId* 值。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
  
## <a name="comments"></a>註解  
 **SQLGetFunctions** 一律會傳回支援 **SQLGetFunctions**、 **SQLDataSources**和 **SQLDrivers** 。 因為這些函式會在驅動程式管理員中執行，所以會執行此工作。 如果 Unicode 函式存在，驅動程式管理員會將 ANSI 函式對應至對應的 Unicode 函式，而且如果 ANSI 函數存在，則會將 Unicode 函式對應至對應的 ANSI 函數。 如需應用程式如何使用 **SQLGetFunctions**的詳細資訊，請參閱 [介面一致性層級](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 以下是符合 ISO 92 標準合規性層級之函式的有效值清單 *FunctionId* ：  
  
|FunctionId 值|FunctionId 值|  
|----------|----------|  
|SQL_API_SQLALLOCHANDLE|SQL_API_SQLGETDESCFIELD|  
|SQL_API_SQLBINDCOL|SQL_API_SQLGETDESCREC|  
|SQL_API_SQLCANCEL|SQL_API_SQLGETDIAGFIELD|  
|SQL_API_SQLCLOSECURSOR|SQL_API_SQLGETDIAGREC|  
|SQL_API_SQLCOLATTRIBUTE|SQL_API_SQLGETEN加值稅TR|  
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
|SQL_API_SQLGETCONNECTATTR|SQL_API_SQLSETEN加值稅TR|  
|SQL_API_SQLGETCURSORNAME|SQL_API_SQLSETSTMTATTR|  
|SQL_API_SQLGETDATA| |  
  
 以下是符合開放式群組標準相容性層級之函式的有效值清單 *FunctionId* ：  
  
|FunctionId 值|FunctionId 值|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 以下是符合 ODBC 標準合規性層級之函式的有效值清單 *FunctionId* 。  
  
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
  
 [1] 使用 ODBC*2.x 驅動程式*時，只有在下列兩項都成立時，才會以支援的方式傳回**SQLBulkOperations** ： ODBC 2.X 驅動 *.x*程式支援**SQLSetPos**，而資訊類型 SQL_POS_OPERATIONS 傳回 SQL_POS_ADD 位的設定。  
  
 以下是 ODBC 3.8 或更新版本中所引進函數的有效值清單 *FunctionId* ：  
  
|FunctionId 值|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2]   **SQLCancelHandle** 只有在驅動程式同時支援 **SQLCancel** 和 **SQLCancelHandle**時，才會傳回支援。 如果支援 **SQLCancel** 但 **SQLCancelHandle** 不是，應用程式仍然可以在語句控制碼上呼叫 **SQLCancelHandle** ，因為它會對應至 **SQLCancel**。  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS 宏  
 SQL_FUNC_EXISTS (*SupportedPtr*、 *FunctionID*) 宏用來判斷在使用 SQL_API_ODBC3_ALL_FUNCTIONS *FunctionID*引數呼叫**SQLGetFunctions**之後，ODBC 3.x 或舊版函式的*支援。* 應用程式會呼叫 SQL_FUNC_EXISTS，並將*SupportedPtr*引數設定為傳入*SQLGetFunctions*的*SupportedPtr* ，並將*FunctionID*引數設定為函式的 **#define** 。 如果支援函數，SQL_FUNC_EXISTS 會傳回 SQL_TRUE，否則會傳回 SQL_FALSE。  
  
> [!NOTE]
>  使用 ODBC 2.x 驅動程式時，ODBC 3.x 驅動程式管理員會 *.x*傳回**SQLAllocHandle**和**SQLFreeHandle**的 SQL_TRUE，因為**SQLAllocHandle**對應到**SQLAllocEnv**、 **SQLAllocConnect**或**SQLAllocStmt**，而且**SQLFreeHandle**會對應到**SQLFreeEnv**、 **SQLFreeConnect**或**SQLFreeStmt**。* * 但是，即使針對函式*傳回了 SQL_TRUE* ， **SQLAllocHandle**或 SQL_HANDLE_DESC **SQLFreeHandle**也不受支援，因為在此情況下，不會對應到 ODBC*2.x 函數。*  
  
## <a name="code-example"></a>程式碼範例  
 下列三個範例示範應用程式如何使用 **SQLGetFunctions** 來判斷驅動程式是否支援 **SQLTables**、 **SQLColumns**和 **SQLStatistics**。 如果驅動程式不支援這些功能，應用程式就會從驅動程式中斷連線。 第一個範例會針對每個函式呼叫 **SQLGetFunctions** 一次。  
  
```cpp  
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
  
 在第二個範例中，ODBC 3.x 應用程式會呼叫 **SQLGetFunctions** ，並將陣列傳遞給它，而 **SQLGetFunctions** 會傳回所有 ODBC 3.x 和先前函數的相關資訊。  
  
```cpp  
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
  
 第三個範例是 ODBC 2.x 應用程式呼叫 **SQLGetFunctions** 並傳遞100元素陣列，其中 **SQLGetFunctions** 會傳回所有 ODBC 2.x 和先前函數的相關資訊。  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回驅動程式或資料來源的相關資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|傳回語句屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
