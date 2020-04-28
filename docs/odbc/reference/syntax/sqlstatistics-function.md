---
title: SQLStatistics 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2a5ef0b0e54e17a2dc091a98efc972fa608ef15
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302942"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLStatistics**會抓取單一資料表的統計資料清單，以及與資料表相關聯的索引。 驅動程式會以結果集的形式傳回信息。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *CatalogName*  
 源目錄名稱。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）會指出沒有目錄的資料表。 *CatalogName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*CatalogName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*CatalogName*是一般引數;它會以字面方式處理，而且其大小寫很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 源**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 源架構名稱。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）會指出沒有架構的資料表。 *SchemaName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*SchemaName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*SchemaName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength2*  
 源**SchemaName*的長度（以字元為單位）。  
  
 *TableName*  
 源資料表名稱。 這個引數不可以是 null 指標。 *SchemaName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，會將*TableName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE， *TableName*就是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength3*  
 源**TableName*的長度（以字元為單位）。  
  
 *唯一*  
 源索引的類型： SQL_INDEX_UNIQUE 或 SQL_INDEX_ALL。  
  
 *Reserved*  
 源指出結果集中的基數和分頁資料行的重要性。 下列選項只會影響基數和分頁資料行的傳回;即使不傳回基數和分頁，也會傳回索引資訊。  
  
 SQL_ENSURE 要求驅動程式會無條件地取得統計資料。 （僅符合開放式群組標準且不支援 ODBC 延伸模組的驅動程式將無法支援 SQL_ENSURE）。  
  
 SQL_QUICK 要求驅動程式只會在伺服器可供使用時，才會抓取基數和頁面。 在這個情況下，驅動程式無法確保這些值是否為最新的。 （寫入開放式群組標準的應用程式一律會*從 ODBC 3.x*相容的驅動程式取得 SQL_QUICK 行為）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLStatistics**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLStatistics**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|已在*StatementHandle*上開啟資料指標，且已呼叫**SQLFetch**或**SQLFetchScroll** 。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式就會傳回此錯誤。<br /><br /> 已在*StatementHandle*上開啟資料指標，但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。|  
|40001|序列化失敗|交易已回復，因為有另一個交易的資源鎖死。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|*TableName*引數為 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE， *CatalogName*引數為 null 指標，而 SQL_CATALOG_NAME *InfoType*會傳回支援的目錄名稱。<br /><br /> （DM） SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，而*SchemaName*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLStatistics**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個 name length 引數的值超過對應名稱的最大長度值。|  
|HY100|唯一性選項類型超出範圍|（DM）指定了不正確*唯一*值。|  
|HY101|精確度選項類型超出範圍|（DM）指定了不正確*保留*值。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|已指定目錄，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定架構，而驅動程式或資料來源不支援架構。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回要求的結果集之前，查詢超時時間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>評價  
 **SQLStatistics**會以標準結果集的形式傳回單一資料表的相關資訊，並依 NON_UNIQUE、類型、INDEX_QUALIFIER、INDEX_NAME 和 ORDINAL_POSITION 排序。 結果集會結合資料表的統計資料資訊（在結果集的 [基數] 和 [頁數] 資料行中），其中包含每個索引的相關資訊。 如需如何使用這項資訊的詳細資訊，請參閱[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 若要判斷 TABLE_CAT、TABLE_SCHEM、TABLE_NAME 和 COLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫**SQLGetInfo** 。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 ODBC 3.x 的下列資料行已經重新*命名。* 資料行名稱變更不會影響回溯相容性，因為應用程式會依資料行編號來系結。  
  
|ODBC 2.0 資料行|ODBC *3.x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 下表列出結果集中的資料行。 驅動程式可以定義超過 column 13 （FILTER_CONDITION）的其他資料行。 應用程式應該從結果集的結尾向下計算，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|評價|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT （ODBC 1.0）|1|Varchar|套用統計資料或索引之資料表的目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串（""）。|  
|TABLE_SCHEM （ODBC 1.0）|2|Varchar|套用統計資料或索引之資料表的架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有架構的資料表傳回空字串（""）。|  
|TABLE_NAME （ODBC 1.0）|3|Varchar not Null|要套用統計資料或索引之資料表的資料表名稱。|  
|NON_UNIQUE （ODBC 1.0）|4|Smallint|指出索引是否不允許重複的值：<br /><br /> SQL_TRUE 索引值是否可以是非唯一的。<br /><br /> 如果索引值必須是唯一的，則 SQL_FALSE。<br /><br /> 如果類型為 SQL_TABLE_STAT，則會傳回 Null。|  
|INDEX_QUALIFIER （ODBC 1.0）|5|Varchar|用來限定索引名稱執行**DROP INDEX**的識別碼。如果資料來源不支援索引限定詞，或如果 SQL_TABLE_STAT 類型，則會傳回 Null。 如果在此資料行中傳回非 null 值，就必須使用它來限定**DROP INDEX**語句上的索引名稱;否則，應該使用 TABLE_SCHEM 來限定索引名稱。|  
|INDEX_NAME （ODBC 1.0）|6|Varchar|索引名稱;如果類型為 SQL_TABLE_STAT，則會傳回 Null。|  
|類型（ODBC 1.0）|7|Smallint 非 NULL|傳回的資訊類型：<br /><br /> SQL_TABLE_STAT 表示資料表的統計資料（在 [基數] 或 [分頁] 資料行中）。<br /><br /> SQL_INDEX_BTREE 表示 B 型樹狀目錄索引。<br /><br /> SQL_INDEX_CLUSTERED 表示叢集索引。<br /><br /> SQL_INDEX_CONTENT 表示內容索引。<br /><br /> SQL_INDEX_HASHED 表示雜湊索引。<br /><br /> SQL_INDEX_OTHER 表示另一種索引類型。|  
|ORDINAL_POSITION （ODBC 1.0）|8|Smallint|索引中的資料行序號（從1開始）;如果類型為 SQL_TABLE_STAT，則會傳回 Null。|  
|COLUMN_NAME （ODBC 1.0）|9|Varchar|資料行名稱。 如果資料行是以運算式為基礎，例如薪資 + 優點，則會傳回運算式;如果無法判斷運算式，則會傳回空字串。 如果類型為 SQL_TABLE_STAT，則會傳回 Null。|  
|ASC_OR_DESC （ODBC 1.0）|10|Char(1)|資料行的排序次序： "A" 表示遞增;"D" 表示遞減;如果資料來源不支援資料行排序次序，或如果 SQL_TABLE_STAT 類型，則會傳回 Null。|  
|基數（ODBC 1.0）|11|整數|資料表或索引的基數;如果類型為 SQL_TABLE_STAT，則為數據表中的資料列數目。如果未 SQL_TABLE_STAT 類型，則為索引中的唯一值數目。如果資料來源無法使用此值，則會傳回 Null。|  
|頁面（ODBC 1.0）|12|整數|用來儲存索引或資料表的頁面數目;如果類型為 SQL_TABLE_STAT，則為數據表的頁數。如果未 SQL_TABLE_STAT 類型，則為索引的頁面數目。如果資料來源無法使用值，或如果不適用於資料來源，則會傳回 Null。|  
|FILTER_CONDITION （ODBC 2.0）|13|Varchar|如果索引是篩選的索引，這就是篩選準則，例如薪資 > 30000;如果無法判斷篩選準則，這就是空字串。<br /><br /> 如果索引不是篩選索引，則無法判斷索引是否為篩選索引，或類型為 SQL_TABLE_STAT，則為 Null。|  
  
 如果結果集中的資料列對應到資料表，驅動程式會將類型設定為 SQL_TABLE_STAT，並將 NON_UNIQUE、INDEX_QUALIFIER、INDEX_NAME、ORDINAL_POSITION、COLUMN_NAME 和 ASC_OR_DESC 設定為 Null。 如果資料來源無法使用基數或分頁，驅動程式會將其設定為 Null。  
  
## <a name="code-example"></a>程式碼範例  
 如需類似函式的程式碼範例，請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以順向方向提取單一資料列或資料區塊。|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回外鍵的資料行|[SQLForeignKeys 函數](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|傳回主要金鑰的資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
