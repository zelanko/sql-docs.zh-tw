---
title: "SQLTables 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLTables
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTables
helpviewer_keywords:
- SQLTables function [ODBC]
ms.assetid: 60d5068a-7d7c-447c-acc6-f3f2cf73440c
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd6e505ee08d7162ef820c7c7c75195b3616e585
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqltables-function"></a>SQLTables 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： Open Group  
  
 **摘要**  
 **SQLTables**傳回的資料表、 類別目錄或結構描述的名稱，以及儲存在特定資料來源中的資料表類型的清單。 驅動程式會傳回結果集的資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLTables(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      TableType,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼擷取結果。  
  
 *CatalogName*  
 [輸入]目錄名稱。 *CatalogName* SQL_ODBC_VERSION 環境屬性是否為 sql_ov_odbc3 時，引數會接受搜尋模式; 如果設定 SQL_OV_ODBC2 不接受搜尋模式。 如果驅動程式支援目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料的不同 Dbms，空字串 ("") 表示沒有目錄的資料表。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*會被視為識別項和其案例並不重要。 如果是 SQL_FALSE， *CatalogName*模式值引數; 將它視為常值，和其案例很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]中的字元長度 **CatalogName*。  
  
 *SchemaName*  
 [輸入]結構描述名稱的字串搜尋模式。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料的不同 Dbms，空字串 ("") 表示沒有結構描述的資料表。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *SchemaName*會被視為識別項和其案例並不重要。 如果是 SQL_FALSE， *SchemaName*模式值引數; 將它視為常值，和其案例很重要。  
  
 *NameLength2*  
 [輸入]中的字元長度 **SchemaName*。  
  
 *TableName*  
 [輸入]資料表名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *TableName*會被視為識別項和其案例並不重要。 如果是 SQL_FALSE， *TableName*模式值引數; 將它視為常值，和其案例很重要。  
  
 *NameLength3*  
 [輸入]中的字元長度 **TableName*。  
  
 *TableType*  
 [輸入]要比對的資料表類型的清單。  
  
 請注意 SQL_ATTR_METADATA_ID 陳述式屬性有任何影響*TableType*引數。 *TableType*是值清單引數，不論 SQL_ATTR_METADATA_ID 的設定為何。  
  
 *NameLength4*  
 [輸入]中的字元長度 **TableType*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLTables**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLTables** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在開啟游標的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**如同呼叫。 傳回這個錯誤是由驅動程式管理員如果**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，如果驅動程式傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 在開啟游標的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|相關聯的連接失敗，此函式，在執行期間，無法決定交易的狀態。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|無效的 null 指標使用|SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*引數為 null 指標和 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*SchemaName*或*TableName*引數為 null 指標。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 SQLTables 呼叫時這個非同步函式還在執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 的長度引數的其中一個值小於 0 卻不等於 SQL_NTS。<br /><br /> 其中一個名稱的長度引數的值超過最大長度的值對應的名稱。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定類別目錄，並且在驅動程式或資料來源不支援目錄。<br /><br /> 指定結構描述，並且在驅動程式或資料來源不支援結構描述。<br /><br /> 指定字串的搜尋模式的目錄名稱、 資料表結構描述或資料表名稱和資料來源不支援搜尋模式的其中一個或多個這些引數。<br /><br /> 驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，，並且 SQL_ATTR_CURSOR_TYPE 陳述式屬性設定為 驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 逾時期限透過設定**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLTables**列出要求的範圍中的所有資料表。 使用者可能會或可能沒有任何這些資料表的 SELECT 權限。 若要檢查協助工具，應用程式可以：  
  
-   呼叫**SQLGetInfo**並檢查 SQL_ACCESSIBLE_TABLES 資訊類型。  
  
-   呼叫**SQLTablePrivileges**檢查每個資料表的權限。  
  
 否則，應用程式必須能夠處理的情況下，使用者在選取資料表的**選取**不授與權限。  
  
 *SchemaName*和*TableName*引數接受搜尋模式。 *CatalogName* SQL_ODBC_VERSION 環境屬性是否為 sql_ov_odbc3 時，引數會接受搜尋模式; 如果設定 SQL_OV_ODBC2 不接受搜尋模式。 如果 sql_ov_odbc3 時設定，ODBC 3*.x*驅動程式會要求該萬用字元字串中字元*CatalogName*逸出常值視為引數。 如需有效的搜尋模式的詳細資訊，請參閱[模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 若要支援的目錄、 結構描述和資料表類型的列舉，為定義下列特殊的語意*CatalogName*， *SchemaName*， *TableName*，和*TableType*引數的**SQLTables**:  
  
-   如果*CatalogName*為 SQL_ALL_CATALOGS 和*SchemaName*和*TableName*則為空字串，結果集包含的資料來源的有效目錄清單。 （除了 TABLE_CAT 資料行以外的所有資料行包含 Null）。  
  
-   如果*SchemaName*是 SQL_ALL_SCHEMAS 和*CatalogName*和*TableName*則為空字串，結果集包含資料來源的有效結構描述的清單。 （除了再依據 table_schem 排列資料行以外的所有資料行包含 Null）。  
  
-   如果*TableType*是 SQL_ALL_TABLE_TYPES 和*CatalogName*， *SchemaName*，和*TableName*則為空字串，結果集包含有效的資料表類型的資料來源的清單。 （除了 TABLE_TYPE 資料行以外的所有資料行包含 Null）。  
  
 如果*TableType*不是空字串，它必須包含一份以逗號分隔值感興趣的類型，則每個值可括在單引號 （'） 或不加引號，例如 'TABLE'、 '檢視' 或資料表中，檢視。 應用程式應該一律指定資料表類型中大寫;驅動程式應將資料表類型轉換成任何案例所需的資料來源中。 如果資料來源不支援指定的資料表類型， **SQLTables**不會傳回該類型的任何結果。  
  
 **SQLTables**做為標準的結果集，依據 TABLE_TYPE、 TABLE_CAT、 再依據 table_schem 排列和 TABLE_NAME 排序傳回的結果。 如需這項資訊可能會如何使用資訊，請參閱[的目錄資料會使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要判斷 TABLE_CAT、 再依據 table_schem 排列和 TABLE_NAME 的資料行的實際長度，應用程式可以呼叫**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_TABLE_NAME_LEN 資訊型別。  
  
 下列資料行已重新命名為 ODBC 3*.x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3*.x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出結果集內的資料行。 欄 5 （< 備註 >） 以外的其他資料行可以定義由驅動程式。 應用程式應該存取驅動程式特有的資料行，來計算從結果集而不是指定明確的序數位置的結尾。 如需詳細資訊，請參閱[目錄函數所傳回資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目錄名稱。如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些資料表，但不適用於其他項目，例如當驅動程式會從不同的 Dbms 擷取資料，它會傳回空字串 ("") 沒有目錄這些資料表。|  
|再依據 TABLE_SCHEM 排列 (ODBC 1.0)|2|Varchar|結構描述名稱。如果不適用於資料來源，則為 NULL。 如果驅動程式支援的結構描述對於某些資料表，但不適用於其他項目，例如當驅動程式會從不同的 Dbms 擷取資料，它會傳回空字串 ("") 並沒有結構描述這些資料表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|資料表名稱。|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|資料表類型名稱。下列其中之一: 「 資料表 」、 「 檢視 」、 「 系統資料表 」、 「 全域暫存 」、 「 本機暫存"、 「 別名 」、 「 同義字 」 或資料來源專用的類型名稱。<br /><br /> 「 別名 」 和 「 同義字 」 的意義是驅動程式專屬的。|  
|註解 (ODBC 1.0)|5|Varchar|資料表的描述。|  
  
## <a name="example"></a>範例  
 下列範例程式碼不會釋放控制代碼和連線。 請參閱[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)和[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)釋放控制代碼和陳述式的程式碼範例。  
  
```  
// SQLTables.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
// simple helper functions  
int MySQLSuccess(SQLRETURN rc) {  
   return (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO);  
}  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printCatalog(const struct DataBinding* catalogResult) {  
   if (catalogResult[0].StrLen_or_Ind != SQL_NULL_DATA)   
      printf("Catalog Name = %s\n", (char *)catalogResult[0].TargetValuePtr);  
}  
  
// remember to disconnect and free memory, and free statements and handles  
int main() {  
   int bufferSize = 1024, i, numCols = 5;  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   wchar_t* dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   wchar_t* userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR*)"Driver={SQL Server}", SQL_NTS, (SQLCHAR*)connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferSize);  
  
   bufferSize = 1024;  
  
   // allocate memory for the binding  
   // free this memory when done  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // setup the binding (can be used even if the statement is closed by closeStatementHandle)  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   // all catalogs query  
   printf( "A list of names of all catalogs\n" );  
   retCode = SQLTables( hstmt, (SQLCHAR*)SQL_ALL_CATALOGS, SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS, (SQLCHAR*)"", SQL_NTS );  
   for ( retCode = SQLFetch(hstmt) ;  MySQLSuccess(retCode) ; retCode = SQLFetch(hstmt) )  
      printCatalog( catalogResult );  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回的資料行或資料行的權限|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|傳回的資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|擷取單一資料列或資料區塊的順向的方向|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料表的統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回針對資料表或資料表的權限|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
