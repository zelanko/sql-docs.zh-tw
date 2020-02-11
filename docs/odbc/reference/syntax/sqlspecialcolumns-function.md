---
title: SQLSpecialColumns 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 15fa1269b733c9adc938b1880735ae2a4e5db731
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039560"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性：開啟群組  
  
 **摘要**  
 **SQLSpecialColumns**會抓取有關指定資料表內之資料行的下列資訊：  
  
-   可唯一識別資料表中之資料列的最佳資料行集。  
  
-   當交易更新資料列中的任何值時，會自動更新的資料行。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *IdentifierType*  
 源要傳回的資料行類型。 必須為下列其中一個值：  
  
 SQL_BEST_ROWID：藉由從資料行中抓取值來傳回最佳的一或多個資料行，以允許唯一識別指定之資料表中的任何資料列。 資料行可以是專為此用途而設計的虛擬資料行（如同 Oracle ROWID 或 Ingres TID），或資料表之任何唯一索引的資料行。  
  
 SQL_ROWVER：如果任何交易更新資料列中的任何值（如同 SQLBase ROWID 或 Sybase 時間戳記），則會傳回在指定的資料表中（如果有的話）自動更新的一個或多個資料行。  
  
 *CatalogName*  
 源資料表的目錄名稱。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有目錄的資料表。 *CatalogName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*CatalogName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*CatalogName*是一般引數;它會以字面方式處理，而且其大小寫很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 源**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 源資料表的架構名稱。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有架構的資料表。 *SchemaName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*SchemaName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*SchemaName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength2*  
 源**SchemaName*的長度（以字元為單位）。  
  
 *TableName*  
 源資料表名稱。 這個引數不可以是 null 指標。 *TableName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，會將*TableName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE， *TableName*就是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength3*  
 源**TableName*的長度（以字元為單位）。  
  
 *影響範圍*  
 源Rowid 的最小必要範圍。 傳回的 rowid 可能是較大的範圍。 必須是下列其中之一：  
  
 SQL_SCOPE_CURROW： rowid 只有在定位於該資料列時，才保證有效。 如果另一個交易已更新或刪除資料列，則稍後使用 rowid 重新選擇可能不會傳回資料列。  
  
 SQL_SCOPE_TRANSACTION：在目前交易的持續時間內，rowid 保證是有效的。  
  
 SQL_SCOPE_SESSION：在會話的持續時間（跨交易界限）保證 rowid 是有效的。  
  
 *Nullable*  
 源判斷是否要傳回可以有 Null 值的特殊資料行。 必須是下列其中之一：  
  
 SQL_NO_NullS：排除可以有 Null 值的特殊資料行。 某些驅動程式無法支援 SQL_NO_NullS，而且如果指定 SQL_NO_NullS，這些驅動程式將會傳回空的結果集。 應用程式應針對此案例做好準備，而且只有在絕對必要時才要求 SQL_NO_NullS。  
  
 SQL_NullABLE：傳回特殊資料行，即使它們可以有 Null 值也一樣。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSpecialColumns**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLSpecialColumns**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|已在*StatementHandle*上開啟資料指標，且已呼叫**SQLFetch**或**SQLFetchScroll** 。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式就會傳回此錯誤。<br /><br /> 已在*StatementHandle*上開啟資料指標，但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死，所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|*TableName*引數為 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE， *CatalogName*引數為 null 指標，而 SQL_CATALOG_NAME *InfoType*會傳回支援的目錄名稱。<br /><br /> （DM） SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，而*SchemaName*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLSpecialColumns**時，此函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）其中一個長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個長度引數的值超過對應名稱的最大長度值。 藉由呼叫具有*InfoType*值的**SQLGetInfo** ，即可取得每個名稱的最大長度： SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 或 SQL_MAX_TABLE_NAME_LEN。|  
|HY097|資料行類型超出範圍|（DM）指定了不正確*IdentifierType*值。|  
|HY098|範圍類型超出範圍|（DM）指定了不正確*範圍*值。|  
|HY099|可為 null 的類型超出範圍|（DM）指定了不正確*可為 null*值。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|已指定目錄，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定架構，而驅動程式或資料來源不支援架構。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回要求的結果集之前，查詢超時時間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 當 SQL_BEST_ROWID *IdentifierType*引數時， **SQLSpecialColumns**會傳回唯一識別資料表中每個資料列的資料行。 這些資料行一律可用於*選取清單*或**WHERE**子句中。 **SQLColumns**（用來傳回資料表資料行上的各種資訊）不一定會傳回唯一識別每個資料列的資料行，或是當交易更新資料列中的任何值時，自動更新的資料行。 例如， **SQLColumns**可能不會傳回 Oracle 虛擬資料行 ROWID。 這就是為什麼使用**SQLSpecialColumns**來傳回這些資料行的原因。 如需詳細資訊，請參閱[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果沒有可唯一識別資料表中每個資料列的資料行，則**SQLSpecialColumns**會傳回不含資料列的資料列集。後續對語句的**SQLFetch**或**SQLFetchScroll**呼叫會傳回 SQL_NO_DATA。  
  
 如果*IdentifierType*、 *Scope*或*Nullable*引數指定資料來源不支援的特性， **SQLSpecialColumns**會傳回空的結果集。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設為 SQL_TRUE，則*CatalogName*、 *SchemaName*和*TableName*引數會被視為識別碼，因此在某些情況下無法將它們設定為 null 指標。 （如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)）。  
  
 **SQLSpecialColumns**會以標準結果集的形式傳回結果，並依範圍排序。  
  
 ODBC 3.x 的下列資料行已經重新*命名。* 資料行名稱變更不會影響回溯相容性，因為應用程式會依資料行編號來系結。  
  
|ODBC 2.0 資料行|ODBC *3.x*資料行|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 若要判斷 COLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫**SQLGetInfo** 。  
  
 下表列出結果集中的資料行。 驅動程式可以定義超過 column 8 （PSEUDO_COLUMN）的其他資料行。 應用程式應該從結果集的結尾向下計算，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|範圍（ODBC 1.0）|1|Smallint|Rowid 的實際範圍。 包含下列其中一個值：<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> 當*IdentifierType* SQL_ROWVER 時，會傳回 Null。 如需每個值的說明，請參閱本節前面的「語法」中的「*範圍*描述」。|  
|COLUMN_NAME （ODBC 1.0）|2|Varchar not Null|資料行名稱。 對於沒有名稱的資料行，驅動程式會傳回空字串。|  
|DATA_TYPE （ODBC 1.0）|3|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式特有的 SQL 資料類型。 如需有效 ODBC SQL 資料類型的清單，請參閱[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。 如需有關驅動程式特定 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。|  
|TYPE_NAME （ODBC 1.0）|4|Varchar not Null|與資料來源相關的資料類型名稱;例如，"CHAR"、"VARCHAR"、"MONEY"、"LONG VARBINARY" 或 "CHAR （） FOR BIT DATA"。|  
|COLUMN_SIZE （ODBC 1.0）|5|整數|資料來源上的資料行大小。 如需有關資料行大小的詳細資訊，請參閱資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH （ODBC 1.0）|6|整數|指定 SQL_C_DEFAULT 時，在**SQLGetData**或**SQLFetch**作業上傳輸的資料長度（以位元組為單位）。 針對數值資料，此大小可能會與儲存在資料來源上的資料大小不同。 這個值與字元或二進位資料的 COLUMN_SIZE 資料行相同。 如需詳細資訊，請參閱資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS （ODBC 1.0）|7|Smallint|資料來源上資料行的小數位數。 十進位數不適用的資料類型會傳回 Null。 如需有關十進位數的詳細資訊，請參閱資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN （ODBC 2.0）|8|Smallint|指出資料行是否為虛擬資料行，例如 Oracle ROWID：<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO**注意：** 為了達到最大互通性，虛擬資料行不應以**SQLGetInfo**所傳回的識別碼引號字元括住。|  
  
 在應用程式抓取 SQL_BEST_ROWID 的值之後，應用程式可以使用這些值在定義的範圍內重新選擇該資料列。 **SELECT**語句保證不會傳回任何資料列或一個資料列。  
  
 如果應用程式根據 rowid 資料行或資料行來 reselects 資料列，但找不到資料列，則應用程式可以假設資料列已被刪除或已修改 rowid 資料行。 相反的不是 true：即使 rowid 尚未變更，資料列中的其他資料行也可能已經變更。  
  
 針對資料行類型 SQL_BEST_ROWID 傳回的資料行，適用于需要在結果集內向前和向後復原的應用程式，以從一組資料列中取得最新的資料。 在定位於該資料列時，一定不會變更 rowid 的一或多個資料行。  
  
 即使資料指標不在資料列上，rowid 的一或多個資料行仍會保持有效;應用程式可以藉由檢查結果集中的 [範圍] 資料行來判斷這一點。  
  
 針對資料行類型 SQL_ROWVER 傳回的資料行，對於需要檢查是否已在使用 rowid 問題資料列時，是否已更新指定資料列中的任何資料行的應用程式非常有用。 例如，在使用 rowid 重新選取資料列之後，應用程式可以比較 SQL_ROWVER 資料行中先前的值與剛提取的值。 如果 SQL_ROWVER 資料行中的值與先前的值不同，則應用程式可以警示使用者顯示的資料已變更。  
  
## <a name="code-example"></a>程式碼範例  
 如需類似函式的程式碼範例，請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函數](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主要金鑰的資料行|[SQLPrimaryKeys 函數](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
