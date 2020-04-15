---
title: SQLGet 函數功能 |微軟文件
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
ms.openlocfilehash: 15537b28ff2bae8a4fcd3e7be82426eb53aa83a8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285328"
---
# <a name="sqlgetfunctions-function"></a>SQLGetFunctions 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGet功能**傳回有關驅動程式是否支援特定 ODBC 函數的資訊。 此功能在驅動程式管理器中實現;也可以在驅動程序中實現。 如果驅動程式實現**SQLGet 函數**,驅動程式管理器將在驅動程式中調用該函數。 否則,它將執行函數本身。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetFunctions(  
     SQLHDBC           ConnectionHandle,  
     SQLUSMALLINT      FunctionId,  
     SQLUSMALLINT *    SupportedPtr);  
```  
  
## <a name="arguments"></a>引數  
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *功能 Id*  
 [輸入]標識感興趣的 ODBC 函數**的#define**值;**SQL_API_ODBC3_ALL_FUNCTIONSorSQL_API_ALL_FUNCTIONS。** **SQL_API_ODBC3_ALL_FUNCTIONS**由 ODBC 3 *.x*應用程式用於確定對 ODBC 3 *.x*和早期功能的支援。 **SQL_API_ALL_FUNCTIONS**由 ODBC 2 *.x*應用程式用於確定對 ODBC 2 *.x*和早期功能的支援。  
  
 有關標識 ODBC 函數 **#define**值的清單,請參閱"註釋"中的表。  
  
 *支援的 Ptr*  
 【輸出] 如果*函數 Id*識別單個 ODBC 函數,*則受支援的 Ptr*指向 SQLUSMALLINT 值,該值在驅動程式支援指定函數時SQL_TRUE,如果未支援該函數,則SQL_FALSE。  
  
 如果*函數 Id* SQL_API_ODBC3_ALL_FUNCTIONS,*則受支援的 Ptr*指向具有許多元素等於SQL_API_ODBC3_ALL_FUNCTIONS_SIZE的 SQLSMALLINT 陣列。 驅動程式管理員將此陣列視為 4,000 位圖,可用於確定是否支援 ODBC 3 *.x*或更早的功能。 調用SQL_FUNC_EXISTS宏以確定函數支援。 (請參閱"註釋」。。ODBC 3 *.x*應用程式可以針對 ODBC 3 *.x*或 ODBC 2 *.x*驅動程式使用SQL_API_ODBC3_ALL_FUNCTIONS呼叫**SQLGet 功能**。  
  
 如果*函數 Id* SQL_API_ALL_FUNCTIONS,*則受支援的 Ptr*指向包含 100 個元素的 SQLUSMALLINT 陣列。 陣列由*函數 Id***#define**用於標識每個 ODBC 函數的值#define索引;陣列的某些元素未使用並保留以供將來使用。 如果元素識別驅動程式支援的 ODBC 2 *.x*或較早的函數,則SQL_TRUE該元素。 如果驅動程式未識別 ODBC 函數或未識別 ODBC 函數,則SQL_FALSE。  
  
 在 [ 支援*Ptr*中傳回的陣列使用零基索引。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGet 函數**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該*句柄類型*為SQL_HANDLE_DBC和*連接句柄*。 *Handle* 下表列出了**SQLGet 函數**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------|-----|-----------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) **SQLGet函數**是在**SQLConnect、SQLBrowseConnect**或**SQLBrowseConnect****SQLDriverConnect**之前調用的。<br /><br /> (DM) **SQLBrowseConnect**被調用用於*連接句柄*並返回SQL_NEED_DATA。 在**SQLBrowseConnect**返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS之前調用此功能。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用用於**SQLExecDirect***連接處理*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY095|函式類型範圍外|(DM) 指定了無效*的函數 Id*值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
  
## <a name="comments"></a>註解  
 **SQLGet 函數**始終返回**SQLGet 函數** **、SQLDataSources**和**SQLDrivers**受支援。 這樣做是因為這些函數在驅動程式管理器中實現。 如果存在 Unicode 函數,驅動程式管理員將 ANSI 函數映射到相應的 Unicode 函數,並且如果存在 ANSI 函數,則將 Unicode 函數映射到相應的 ANSI 函數。 有關應用程式如何使用**SQLGet 函數**的資訊,請參閱[介面一致性級別](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 以下是符合 ISO 92 標準合規性等級的*函數的函數 Id*的有效值清單:  
  
|函數 Id 值|函數 Id 值|  
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
  
 以下是符合開放組標準合規性等級的*函數的函數 Id*的有效值清單:  
  
|函數 Id 值|函數 Id 值|  
|-|-|  
|SQL_API_SQLCOLUMNS|SQL_API_SQLSTATISTICS|  
|SQL_API_SQLSPECIALCOLUMNS|SQL_API_SQLTABLES|  
  
 以下是符合 ODBC 標準合規性級別的*函數的函數 Id*的有效值清單。  
  
|函數 Id 值|函數 Id 值|  
|-|-|  
|SQL_API_SQLBINDPARAMETER|SQL_API_SQLNATIVESQL|  
|SQL_API_SQLBROWSECONNECT|SQL_API_SQLNUMPARAMS|  
|SQL_API_SQLBULKOPERATIONS[1]|SQL_API_SQLPRIMARYKEYS|  
|SQL_API_SQLCOLUMNPRIVILEGES|SQL_API_SQLPROCEDURECOLUMNS|  
|SQL_API_SQLDESCRIBEPARAM|SQL_API_SQLPROCEDURES|  
|SQL_API_SQLDRIVERCONNECT|SQL_API_SQLSETPOS|  
|SQL_API_SQLFOREIGNKEYS|SQL_API_SQLTABLEPRIVILEGES|  
|SQL_API_SQLMORERESULTS| |  
  
 [1] 使用 ODBC 2 *.x*驅動程式時 **,SQLBulk操作**將返回為支援,僅當以下兩個都為 true 時:ODBC 2 *.x*驅動程式支援**SQLSetPos,** 並且資訊類型SQL_POS_OPERATIONS按設置返回SQL_POS_ADD位。  
  
 以下是 ODBC 3.8 或更高版本中引入的函數*的函數 Id*的有效值清單:  
  
|函數 Id 值|  
|-|  
|SQL_API_SQLCANCELHANDLE [2]|  
  
 [2] **SQLCancelHandle**將僅作為支援返回,因為驅動程式同時支援**SQLCancel**和**SQLCancelHandle**。 如果**SQLCancel**受支援,但**SQLCancelHandle**不支援,則應用程式仍然可以在語句句柄上調用**SQLCancelHandle,** 因為它將映射到**SQLCancel**。  
  
## <a name="sql_func_exists-macro"></a>SQL_FUNC_EXISTS宏  
 SQL_FUNC_EXISTS(*支援 Ptr,**函數 ID)* 巨集用於確定在**SQLGet 函數**使用函數*id*參數SQL_API_ODBC3_ALL_FUNCTIONS調用後對 ODBC 3 *.x*或早期函數的支援。 應用程式呼叫SQL_FUNC_EXISTS與*支援Ptr*參數設定為在*SQLGet 函數*中傳遞*的受支援的 Ptr,* 並且*函數 ID*參數設定為函數的 **#define。** 如果支援該函數,SQL_FUNC_EXISTS返回SQL_TRUE,否則SQL_FALSE。  
  
> [!NOTE]
>  使用 ODBC 2 *.x*驅動程式時,ODBC 3 *.x*驅動程式管理器將返回**SQLAllocHandle**和**SQLFreeHandle** SQL_TRUE,因為**SQLAllocHandle**映射到**SQLAllocEnv、SQLAllocConnect**或**SQLAllocStmt,** 並且因為**SQLFreeHandle**映射到**SQLFreeEnv、SQLFreeConnect**或**SQLFreestmt**。 **SQLAllocConnect** **SQLFreeConnect** 但是,即使為函數返回了SQL_TRUE,但不支援具有SQL_HANDLE_DESC*句柄類型*參數的**SQLAllocHandle**或**SQLFreeHandle,** 因為在這種情況下沒有要映射到的 ODBC 2 *.x*函數。  
  
## <a name="code-example"></a>程式碼範例  
 以下三個範例顯示了應用程式如何使用**SQLGet 函數**來確定驅動程式是否支援**SQLTables、SQLColumns**和**SQLStatistics**。 **SQLColumns** 如果驅動程式不支援這些功能,則應用程式將斷開與驅動程式的連接。 第一個範例為每個函數調用**SQLGet 函數**一次。  
  
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
  
 在第二個範例中,ODBC 3.x 應用程式呼叫**SQLGet功能**並傳遞一個陣列,其中**SQLGet函數**傳回有關所有ODBC 3.x和早期函數的資訊。  
  
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
  
 第三個範例是 ODBC 2.x 應用程式呼叫**SQLGet 功能**,並傳遞一個包含 100 個元素的陣列,其中**SQLGet 函數**傳回有關所有 ODBC 2.x 和早期函數的資訊。  
  
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
|傳回連線屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回關於驅動程式或資料來源的資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|傳回敘述屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
