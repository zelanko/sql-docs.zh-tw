---
description: SQLTables 函數
title: SQLTables 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1eb095849362914074e2c1e7f02166db2712894
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421042"
---
# <a name="sqltables-function"></a>SQLTables 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：開啟群組  
  
 **總結**  
 **SQLTables** 會傳回儲存在特定資料來源中的資料表、目錄或架構名稱，以及資料表類型的清單。 驅動程式會以結果集的形式傳回信息。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 輸出抓取之結果的語句控制碼。  
  
 *CatalogName*  
 輸出目錄名稱。 如果 SQL_OV_ODBC3 SQL_ODBC_VERSION 環境屬性， *CatalogName* 引數會接受搜尋模式;如果設定 SQL_OV_ODBC2，則不接受搜尋模式。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 指出這些資料表沒有目錄。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *CatalogName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *CatalogName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。 如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 輸出**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 輸出架構名稱的字串搜尋模式。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 指出這些資料表沒有架構。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *SchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *SchemaName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength2*  
 輸出**SchemaName*的長度（以字元為單位）。  
  
 *名*  
 輸出資料表名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *TableName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *TableName* 是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength3*  
 輸出**TableName*的長度（以字元為單位）。  
  
 *TableType*  
 輸出要符合的資料表類型清單。  
  
 請注意，SQL_ATTR_METADATA_ID 語句屬性在 *TableType* 引數上沒有作用。 無論 SQL_ATTR_METADATA_ID 的設定為何， *TableType*都是值清單引數。  
  
 *NameLength4*  
 輸出**TableType*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLTables**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLTables** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在 *StatementHandle*上開啟了資料指標，且已呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 如果 **SQLFetch** 或 **SQLFetchScroll** 尚未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果 **SQLFetch** 或 **SQLFetchScroll** 已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 在 *StatementHandle*上開啟了資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。|  
|40001|序列化失敗|交易已復原，因為另一個交易發生資源鎖死。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在 *StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效|SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE、 *CatalogName* 引數為 null 指標，且 SQL_CATALOG_NAME *InfoType* 會傳回支援的目錄名稱。<br /><br />  (DM) SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，且 *SchemaName* 或 *TableName* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 SQLTables 時，這個非同步函數仍在執行中。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 其中一個長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個名稱長度引數的值超過對應名稱的最大長度值。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|已指定目錄，且驅動程式或資料來源不支援目錄。<br /><br /> 指定了架構，而驅動程式或資料來源不支援架構。<br /><br /> 針對目錄名稱、資料表架構或資料表名稱指定了字串搜尋模式，且資料來源不支援一或多個這些引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而且 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回要求的結果集之前過期。 Timeout 期限是透過 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 **SQLTables** 會列出要求範圍中的所有資料表。 使用者不一定具有任何這些資料表的 SELECT 許可權。 若要檢查協助工具，應用程式可以：  
  
-   呼叫 **SQLGetInfo** 並檢查 SQL_ACCESSIBLE_TABLES 資訊類型。  
  
-   呼叫 **SQLTablePrivileges** 來檢查每個資料表的許可權。  
  
 否則，應用程式必須能夠處理使用者選取未授與 **SELECT** 許可權之資料表的情況。  
  
 *SchemaName*和*TableName*引數接受搜尋模式。 如果 SQL_OV_ODBC3 SQL_ODBC_VERSION 環境屬性， *CatalogName* 引數會接受搜尋模式;如果設定 SQL_OV_ODBC2，則不接受搜尋模式。 如果設定了 SQL_OV_ODBC3，ODBC*3.x 驅動程式* 就會要求將 *CatalogName* 引數中的萬用字元，以真正的方式處理。 如需有效搜尋模式的詳細資訊，請參閱 [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱 [目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 為了支援類別目錄、架構和資料表類型的列舉，會針對**SQLTables**的*CatalogName*、 *SchemaName*、 *TableName*和*TableType*引數定義下列特殊的語法：  
  
-   如果 *CatalogName* 是 SQL_ALL_CATALOGS，且 *SchemaName* 和 *TableName* 是空字串，則結果集會包含資料來源的有效目錄清單。  (TABLE_CAT 資料行以外的所有資料行都包含 Null。 )   
  
-   如果 *SchemaName* 是 SQL_ALL_SCHEMAS，且 *CatalogName* 和 *TableName* 是空字串，則結果集會包含資料來源的有效架構清單。  (TABLE_SCHEM 資料行以外的所有資料行都包含 Null。 )   
  
-   如果 *TableType* 是 SQL_ALL_TABLE_TYPES 且 *CatalogName*、 *SchemaName*和 *TableName* 是空字串，則結果集會包含資料來源的有效資料表類型清單。  (TABLE_TYPE 資料行以外的所有資料行都包含 Null。 )   
  
 如果 *TableType* 不是空字串，它必須包含感興趣之類型的逗號分隔值清單;每個值都可以用單引號括住 ( ' ) 或未加引號，例如 ' TABLE '、' VIEW ' 或 TABLE、VIEW。 應用程式應該一律以大寫指定資料表類型;驅動程式應該將資料表類型轉換成資料來源需要的任何大小寫。 如果資料來源不支援指定的資料表類型， **SQLTables** 就不會傳回該型別的任何結果。  
  
 **SQLTables** 會以 TABLE_TYPE、TABLE_CAT、TABLE_SCHEM 和 TABLE_NAME 排序的標準結果集傳回結果。 如需有關如何使用這項資訊的詳細資訊，請參閱 [目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要判斷 TABLE_CAT、TABLE_SCHEM 和 TABLE_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_TABLE_NAME_LEN 資訊類型來呼叫 **SQLGetInfo** 。  
  
 已重新命名 ODBC 3.x 的下列資料行 *。* 資料行名稱的變更不會影響回溯相容性，因為應用程式會依資料行編號進行系結。  
  
|ODBC 2.0 資料行|ODBC 3.x*資料行*|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出結果集中的資料行。 第5欄以外的其他資料行 (備註) 可以由驅動程式定義。 應用程式應該從結果集的結尾算下，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱 [目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0) |1|Varchar|目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄，例如當驅動程式從不同 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串 ( "" ) 。|  
|TABLE_SCHEM (ODBC 1.0) |2|Varchar|架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則會針對沒有架構的資料表傳回空字串 ( "" ) 。|  
|TABLE_NAME (ODBC 1.0) |3|Varchar|資料表名稱。|  
|TABLE_TYPE (ODBC 1.0) |4|Varchar|資料表類型名稱;下列其中一項：「資料表」、「視圖」、「系統資料表」、「全域暫存」、「本機暫存」、「別名」、「同義字」或資料來源特定的類型名稱。<br /><br /> 「別名」和「同義字」的意義是驅動程式特定的。|  
| (ODBC 1.0) 的備註|5|Varchar|資料表的描述。|  
  
## <a name="example"></a>範例  
 下列範例程式碼不會釋放控制碼和連接。 請參閱程式碼範例的 [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) 函式和 [SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md) 函式，以釋放控制碼和語句。  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料行或資料行的許可權|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料表統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回資料表或資料表的許可權|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
