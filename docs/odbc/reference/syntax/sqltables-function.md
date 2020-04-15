---
title: SQLTables 函數 |微軟文件
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
ms.openlocfilehash: ae52e6431679ed0f260e6885090ac38363b4ef3d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287128"
---
# <a name="sqltables-function"></a>SQLTables 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 開放組  
  
 **摘要**  
 **SQLTables**傳回儲存在特定資料來源中的表、目錄或架構名稱以及表類型的清單。 驅動程式將返回結果集。  
  
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
 *語句句柄*  
 [輸入]已檢索結果的語句句柄。  
  
 *目錄名稱*  
 [輸入]目錄名稱。 如果SQL_ODBC_VERSION環境屬性SQL_OV_ODBC3,則*目錄名稱*參數接受搜索模式;如果環境屬性SQL_OV_ODBC3,則目錄名稱參數接受搜索模式。如果設置了SQL_OV_ODBC2,則不接受搜索模式。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄,例如當驅動程式從不同的 DBMS 檢索資料時,空字串(")表示那些沒有目錄的表。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則*目錄名稱*將被視為標識符,其大小寫不重要。 如果它SQL_FALSE,目錄名稱是模式值參數;如果為 SQL_FALSE,則 *「目錄名稱」* 是模式值參數。它被從字面上處理,它的情況很重要。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度在 **目錄名稱*的字元中。  
  
 *架構名稱*  
 [輸入]架構名稱的字串搜尋模式。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串(")表示那些沒有架構的表。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 SchemaName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,則 SchemaName 是模式值參數;如果為 SQL_FALSE,則 *「架構名稱」* 是模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度2*  
 [輸入]長度在 **架構名稱*的字元中。  
  
 *表格名稱*  
 [輸入]表名稱的字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則表Name*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,*則表名稱*是模式值參數;如果為"表名稱",則表名稱是模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度3*  
 [輸入]=*表名*的字元的長度。  
  
 *表類型*  
 [輸入]要匹配的表類型的清單。  
  
 請注意,SQL_ATTR_METADATA_ID語句屬性對*表類型*參數沒有影響。 *表類型*是值清單參數,無論SQL_ATTR_METADATA_ID設置如何。  
  
 *名稱長度4*  
 [輸入]=*表類型*中的字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLTables**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_STMT的*句柄類型*和*敘述句柄*。 下表列出了 SQLTables 通常傳回的**SQLSTATE**值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|語句*處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。|  
|40001|序列化失敗|由於資源與另一個事務死鎖,事務被回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*目錄名稱*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID文句屬性設定為SQL_TRUE,*而 SchemaName*或*TableName*參數是空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用 SQLTables 時,此非同步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 長度參數之一的值小於 0,但不等於SQL_NTS。<br /><br /> 其中一個名稱長度參數的值超過相應名稱的最大長度值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了目錄,驅動程式或數據源不支援目錄。<br /><br /> 已指定架構,驅動程式或數據源不支援架構。<br /><br /> 為目錄名稱、表架構或表名稱指定了字串搜索模式,數據源不支援一個或多個這些參數的搜索模式。<br /><br /> 驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回請求的結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQLTables**列出了請求範圍內的所有表。 使用者可能擁有或可能沒有對這些表的 SELECT 許可權。 要檢查輔助功能,應用程式可以:  
  
-   致電**SQLGetInfo**並檢查SQL_ACCESSIBLE_TABLES信息類型。  
  
-   呼叫**SQLTable 特權**以檢查每個表的許可權。  
  
 否則,應用程式必須能夠處理使用者選擇未為其授予**SELECT**許可權的表的情況。  
  
 *架構名稱*和*表名稱*參數接受搜索模式。 如果SQL_ODBC_VERSION環境屬性SQL_OV_ODBC3,則*目錄名稱*參數接受搜索模式;如果環境屬性SQL_OV_ODBC3,則目錄名稱參數接受搜索模式。如果設置了SQL_OV_ODBC2,則不接受搜索模式。 如果設置了SQL_OV_ODBC3,則 ODBC 3 *.x*驅動程式將要求從*目錄名稱*參數中的通配符轉義才能從字面上處理。 關於有效搜尋模式的詳細資訊,請參考[模式值參數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 為了支援對目錄、架構和表類型的枚舉,為**SQLTable**的*目錄名稱*、*架構名稱*、*表格*名稱與*表類型*參數定義了以下特殊文意:  
  
-   如果*目錄名稱*為SQL_ALL_CATALOGS,*並且架構名稱*和*表名*為空字串,則結果集包含資料來源的有效目錄清單。 (除TABLE_CAT列外的所有列都包含 NUL。  
  
-   如果*SchemaName*是SQL_ALL_SCHEMAS,*目錄名稱*和*表名*為空字串,則結果集包含資料來源的有效架構清單。 (除TABLE_SCHEM列外的所有列都包含 NUL。  
  
-   如果*表類型*為SQL_ALL_TABLE_TYPES,*目錄名稱*、*架構名稱*和*表名稱*為空字串,則結果集包含資料來源的有效表類型清單。 (除TABLE_TYPE列外的所有列都包含 NUL。  
  
 如果*TableType*不是空字串,它必須包含感興趣類型的逗號分隔值清單;因此,它必須包含一個逗號分隔的值。每個值可以包含在單個引號 (') 或未引用,例如,"TABLE","視圖"或 TABLE,視圖。 應用程式應始終以大寫指定表類型;因此,應用程式應始終以大寫大小表示表類型。驅動程式應將表類型轉換為數據來源所需的任何情況。 如果數據來源不支援指定的表類型 **,SQLTables**不會返回該類型的任何結果。  
  
 **SQLTables**將結果作為標準結果集返回,由TABLE_TYPE、TABLE_CAT、TABLE_SCHEM和TABLE_NAME排序。 關於如何使用此資訊的資訊,請參考[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 要確定TABLE_CAT、TABLE_SCHEM和TABLE_NAME列的實際長度,應用程式可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN和SQL_MAX_TABLE_NAME_LEN資訊類型調用**SQLGetInfo。**  
  
 以下列已重新命名為 ODBC 3 *.x*。 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC 3 *.x*欄|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出了結果集中的列。 驅動程式可以定義第 5 列 (註釋) 以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目錄名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有目錄的表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|架構名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有架構的表。|  
|TABLE_NAME (ODBC 1.0)|3|Varchar|資料表名稱。|  
|TABLE_TYPE (ODBC 1.0)|4|Varchar|表類型名稱;下列:「TABLE」、「檢視」、「系統表」、「全球臨時」、「本地臨時」、「ALIAS」、「SYNONYM」或數據源特定類型名稱。<br /><br /> "ALIAS"和"SYNONYM"的含義特定於驅動程式。|  
|備註 (ODBC 1.0)|5|Varchar|表的說明。|  
  
## <a name="example"></a>範例  
 以下示例代碼不釋放句柄和連接。 有關代碼示例以釋放句柄和語句,請參閱[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)和[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)。  
  
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
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回欄或欄的權限|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|傳回表或表中的欄位|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回表統計資訊和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回表或表權權限|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
