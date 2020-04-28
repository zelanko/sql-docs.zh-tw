---
title: SQLColumnPrivileges 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e94c5524bcde3023bae3298c8dbb6d03347a0b8e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301265"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLColumnPrivileges**會傳回指定之資料表的資料行清單和相關聯的許可權。 驅動程式會在指定的*StatementHandle*上，以結果集的形式傳回信息。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *CatalogName*  
 源目錄名稱。 如果驅動程式支援某些目錄的名稱，但不適用於其他專案，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表不具有名稱的目錄。 *CatalogName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*CatalogName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*CatalogName*是一般引數;它會以字面方式處理，而且其大小寫很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 源**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 源架構名稱。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有架構的資料表。 *SchemaName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*SchemaName*視為識別碼。 如果 SQL_FALSE，則*SchemaName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength2*  
 源**SchemaName*的長度（以字元為單位）。  
  
 *TableName*  
 源資料表名稱。 這個引數不可以是 null 指標。 *TableName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，會將*TableName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE， *TableName*就是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength3*  
 源**TableName*的長度（以字元為單位）。  
  
 *ColumnName*  
 源資料行名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則*ColumnName*會被視為識別碼，而且其大小寫並不重要。 如果 SQL_FALSE， *ColumnName*就是模式值引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength4*  
 源**ColumnName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColumnPrivileges**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLColumnPrivileges**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|已在 StatementHandle 上開啟資料指標 *，* 且已呼叫**SQLFetch**或**SQLFetchScroll** 。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 已在*StatementHandle*上開啟資料指標，但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死，所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|*TableName*引數為 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE， *CatalogName*引數為 null 指標，而 SQL_CATALOG_NAME *InfoType*會傳回支援的目錄名稱。<br /><br /> （DM） SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，而*SchemaName*或*ColumnName*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫這個函式時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。|  
|||其中一個 name length 引數的值超過對應名稱的最大長度值。 （請參閱「留言」）。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|指定了目錄名稱，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定架構名稱，而驅動程式或資料來源不支援架構。<br /><br /> 已針對資料行名稱指定了字串搜尋模式，而此資料來源不支援該引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_CONCURRENCY 和 SQL_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前，查詢超時時間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>評價  
 **SQLColumnPrivileges**會以標準結果集的形式傳回結果，並依 TABLE_CAT、TABLE_SCHEM、TABLE_NAME、COLUMN_NAME 和許可權排序。  
  
> [!NOTE]  
>  **SQLColumnPrivileges**可能不會傳回所有資料行的許可權。 例如，驅動程式可能不會傳回虛擬資料行之許可權的相關資訊，例如 Oracle ROWID。 應用程式可以使用任何有效的資料行，無論**SQLColumnPrivileges**是否傳回它。  
  
 VARCHAR 資料行的長度不會顯示在資料表中;實際的長度取決於資料來源。 若要判斷 CATALOG_NAME、SCHEMA_NAME、TABLE_NAME 和 COLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫**SQLGetInfo** 。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 ODBC 3 的下列資料行已經重新命名。*x*。 資料行名稱變更不會影響回溯相容性，因為應用程式會依資料行編號來系結。  
  
|ODBC 2.0 資料行|ODBC 3。*x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出結果集中的資料行。 驅動程式可以定義超過 column 8 （IS_GRANTABLE）的其他資料行。 應用程式應該從結果集的結尾向下計算，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|評價|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT （ODBC 1.0）|1|Varchar|目錄識別碼;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串（""）。|  
|TABLE_SCHEM （ODBC 1.0）|2|Varchar|架構識別碼;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有架構的資料表傳回空字串（""）。|  
|TABLE_NAME （ODBC 1.0）|3|Varchar not Null|資料表識別碼。|  
|COLUMN_NAME （ODBC 1.0）|4|Varchar not Null|資料行名稱。 對於沒有名稱的資料行，驅動程式會傳回空字串。|  
|授權者（ODBC 1.0）|5|Varchar|授與許可權的使用者名稱;如果不適用於資料來源，則為 Null。<br /><br /> 對於 [被授與者] 資料行中的值是物件的擁有者的所有資料列而言，[授與者] 欄位將會是 "_SYSTEM"。|  
|被授與者（ODBC 1.0）|6|Varchar not Null|授與許可權之使用者的名稱。|  
|許可權（ODBC 1.0）|7|Varchar not Null|識別資料行許可權。 可能是下列其中一項（或在執行定義時，資料來源所支援的其他專案）：<br /><br /> SELECT：允許被授與者抓取資料行的資料。<br /><br /> INSERT：被授與者可以在插入相關聯資料表的新資料列中，提供資料行的資料。<br /><br /> UPDATE：允許被授與者更新資料行中的資料。<br /><br /> 參考：被授與者可以參考條件約束中的資料行（例如，唯一、參考或資料表檢查條件約束）。|  
|IS_GRANTABLE （ODBC 1.0）|8|Varchar|指出是否允許被授與者將許可權授予其他使用者;如果未知或不適用於資料來源，則為 "YES"、"NO" 或 "Null"。<br /><br /> 許可權可以是可授與或 not 可授與，但不能同時是兩者。 **SQLColumnPrivileges**所傳回的結果集永遠不會包含兩個數據列，但 IS_GRANTABLE 資料行以外的所有資料行都包含相同的值。|  
  
## <a name="code-example"></a>程式碼範例  
 如需類似函式的程式碼範例，請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回資料表或資料表的許可權|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|傳回資料來源中的資料表清單|[SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
