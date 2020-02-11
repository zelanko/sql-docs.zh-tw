---
title: SQLTablePrivileges 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e63677180cc86f022550477bd598eaa61013d694
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039518"
---
# <a name="sqltableprivileges-function"></a>SQLTablePrivileges 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLTablePrivileges**會傳回資料表的清單，以及與每個資料表相關聯的許可權。 驅動程式會在指定的語句上，以結果集的形式傳回信息。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *CatalogName*  
 源資料表目錄。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有目錄的資料表。 *CatalogName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*CatalogName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*CatalogName*是一般引數;它會以字面方式處理，而且其大小寫很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 源**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 源架構名稱的字串搜尋模式。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有架構的資料表。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*SchemaName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*SchemaName*是模式值引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength2*  
 源**SchemaName*的長度（以字元為單位）。  
  
 *TableName*  
 源資料表名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，會將*TableName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE， *TableName*就是模式值引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength3*  
 源**TableName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLTablePrivileges**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLTablePrivileges**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|已在*StatementHandle*上開啟資料指標，且已呼叫**SQLFetch**或**SQLFetchScroll** 。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式就會傳回此錯誤。<br /><br /> 已在*StatementHandle*上開啟資料指標，但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死，所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已**呼叫 SQLTablePrivileges**函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫**SQLTablePrivileges**函式。<br /><br /> 已**呼叫 SQLTablePrivileges**函式，在完成執行之前，會從多執行緒應用程式中的不同執行緒呼叫*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE， *CatalogName*引數為 null 指標，而 SQL_CATALOG_NAME *InfoType*會傳回支援的目錄名稱。<br /><br /> （DM） SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，而*SchemaName*或*TableName*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLTablePrivileges**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個名稱長度引數的值超過對應限定詞或名稱的最大長度值。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|已指定目錄，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定架構，而驅動程式或資料來源不支援架構。<br /><br /> 已為數據表架構、資料表名稱或資料行名稱指定了字串搜尋模式，而資料來源不支援其中一個或多個引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前，查詢超時時間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 *SchemaName*和*TableName*引數接受搜尋模式。 如需有效搜尋模式的詳細資訊，請參閱[模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 **SQLTablePrivileges**會以標準結果集的形式傳回結果，依 TABLE_CAT、TABLE_SCHEM、TABLE_NAME、許可權和被授與者排序。  
  
 若要判斷 TABLE_CAT、TABLE_SCHEM 和 TABLE_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_TABLE_NAME_LEN 選項來呼叫**SQLGetInfo** 。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 ODBC 3.x 的下列資料行已經重新*命名。* 資料行名稱變更不會影響回溯相容性，因為應用程式會依資料行編號來系結。  
  
|ODBC 2.0 資料行|ODBC *3.x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出結果集中的資料行。 驅動程式可以定義超過 column 7 （IS_GRANTABLE）的其他資料行。 應用程式應該從結果集的結尾向下計算，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT （ODBC 1.0）|1|Varchar|目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串（""）。|  
|TABLE_SCHEM （ODBC 1.0）|2|Varchar|架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有架構的資料表傳回空字串（""）。|  
|TABLE_NAME （ODBC 1.0）|3|Varchar not Null|資料表名稱。|  
|授權者（ODBC 1.0）|4|Varchar|授與許可權的使用者名稱;如果不適用於資料來源，則為 Null。<br /><br /> 對於 [被授與者] 資料行中的值是物件的擁有者的所有資料列而言，[授與者] 欄位將會是 "_SYSTEM"。|  
|被授與者（ODBC 1.0）|5|Varchar not Null|授與許可權之使用者的名稱。|  
|許可權（ODBC 1.0）|6|Varchar not Null|資料表許可權。 可能是下列其中一項或資料來源特定的許可權。<br /><br /> SELECT：允許被授與者抓取資料表的一個或多個資料行的資料。<br /><br /> INSERT：被授與者可以將包含一或多個資料行之資料的新資料列插入資料表。<br /><br /> UPDATE：允許被授與者更新資料表的一個或多個資料行中的資料。<br /><br /> DELETE：允許被授與者從資料表中刪除資料列。<br /><br /> 參考：被授與者可以在條件約束中參考資料表的一個或多個資料行（例如，唯一、參考或資料表檢查條件約束）。<br /><br /> 指定資料表許可權的被授與者所允許的動作範圍與資料來源相關。 例如，UPDATE 許可權可能會允許被授與者更新一個資料來源上資料表中的所有資料行，而僅限於授與者在另一個資料來源上具有 UPDATE 許可權的資料行。|  
|IS_GRANTABLE （ODBC 1.0）|7|Varchar|指出是否允許被授與者將許可權授予其他使用者;「是」、「否」，或如果未知或不適用於資料來源，則為 Null。<br /><br /> 許可權可以是可授與或 not 可授與，但不能同時是兩者。 **SQLColumnPrivileges**所傳回的結果集永遠不會包含兩個數據列，但 IS_GRANTABLE 資料行以外的所有資料行都包含相同的值。|  
  
## <a name="code-example"></a>程式碼範例  
 如需類似函式的程式碼範例，請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回一或多個資料行的許可權|[SQLColumnPrivileges 函數](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函數](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料表統計資料和索引|[SQLStatistics 函數](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回資料來源中的資料表清單|[SQLTables 函數](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
