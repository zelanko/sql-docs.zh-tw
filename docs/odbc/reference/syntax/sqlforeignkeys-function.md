---
title: SQLForeignKeys 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f2769fb378a5ee989fb6a0351537edb3de03469
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285858"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLForeignKeys**可以傳回：  
  
-   指定之資料表中的外鍵清單（指定資料表中的資料行，參考其他資料表中的主鍵）。  
  
-   其他資料表中的外鍵清單，參考指定資料表中的主要索引鍵。  
  
 驅動程式會在指定的語句上，將每個清單當做結果集傳回。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *Sqlforeignkeys*  
 源主要索引鍵資料表目錄名稱。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有目錄的資料表。 *Sqlforeignkeys*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*sqlforeignkeys*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*sqlforeignkeys*是一般引數;它會以字面方式處理，而且其大小寫很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 源**Sqlforeignkeys*的長度（以字元為單位）。  
  
 *PKSchemaName*  
 源主要索引鍵資料表架構名稱。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有架構的資料表。 *PKSchemaName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*PKSchemaName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*PKSchemaName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength2*  
 源**PKSchemaName*的長度（以字元為單位）。  
  
 *PKTableName*  
 源主要索引鍵資料表名稱。 *PKTableName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*PKTableName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*PKTableName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength3*  
 源**PKTableName*的長度（以字元為單位）。  
  
 *FKCatalogName*  
 源外鍵資料表目錄名稱。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有目錄的資料表。 *FKCatalogName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*FKCatalogName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*FKCatalogName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength4*  
 源**FKCatalogName*的長度（以字元為單位）。  
  
 *FKSchemaName*  
 源外鍵資料表架構名稱。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，空字串（""）代表沒有架構的資料表。 *FKSchemaName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*FKSchemaName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*FKSchemaName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength5*  
 源**FKSchemaName*的長度（以字元為單位）。  
  
 *FKTableName*  
 源外鍵資料表名稱。 *FKTableName*不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將*FKTableName*視為識別碼，而且其大小寫不重要。 如果 SQL_FALSE，則*FKTableName*是一般引數;它會以字面方式處理，而且其大小寫很重要。  
  
 *NameLength6*  
 源**FKTableName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLForeignKeys**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLForeignKeys**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|已在*StatementHandle*上開啟資料指標，且已呼叫**SQLFetch**或**SQLFetchScroll** 。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 已在*StatementHandle*上開啟資料指標，但尚未呼叫**SQLFetch**或**SQLFetchScroll** 。|  
|40001|序列化失敗|交易已回復，因為有另一個交易的資源鎖死。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|（DM） *PKTableName*和*FKTableName*這兩個引數都是 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE， *FKCatalogName*或*sqlforeignkeys*引數為 null 指標，而 SQL_CATALOG_NAME *InfoType*會傳回支援的目錄名稱。<br /><br /> （DM） SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，而*FKSchemaName*、 *PKSchemaName*、 *FKTableName*或*PKTableName*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫 SQLForeignKeys 函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。|  
|||其中一個 name length 引數的值超過對應名稱的最大長度值。 （請參閱「留言」）。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|指定了目錄名稱，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定架構名稱，而驅動程式或資料來源不支援架構。|  
|||驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前，查詢超時時間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>評價  
 如需如何使用此函數所傳回信息的詳細資訊，請參閱[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 如果\* *PKTableName*包含資料表名稱， **SQLForeignKeys**會傳回結果集，其中包含指定之資料表的主鍵，以及參考它的所有外鍵。 其他資料表中的外鍵清單不包含指向指定資料表中唯一條件約束的外鍵。  
  
 如果\* *FKTableName*包含資料表名稱， **SQLForeignKeys**會傳回結果集，其中包含指定之資料表中指向其他資料表之主鍵的所有外鍵，以及它們所參考之其他資料表中的主鍵。 指定資料表中的外鍵清單不包含參考其他資料表中 unique 條件約束的外鍵。  
  
 如果\* *PKTableName*和\* *FKTableName*都包含資料表名稱，**則 SQLForeignKeys**會傳回\* *FKTableName*中所指定之資料表的外鍵，這會參考 **PKTableName*中指定之資料表的主要索引鍵。 最多隻能有一個索引鍵。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLForeignKeys**會以標準結果集的形式傳回結果。 如果要求與主鍵相關聯的外鍵，則會依 FKTABLE_CAT、FKTABLE_SCHEM、FKTABLE_NAME 和 KEY_SEQ 排序結果集。 如果要求與外鍵相關聯的主鍵，則會依 PKTABLE_CAT、PKTABLE_SCHEM、PKTABLE_NAME 和 KEY_SEQ 排序結果集。 下表列出結果集中的資料行。  
  
 VARCHAR 資料行的長度不會顯示在資料表中;實際的長度取決於資料來源。 若要判斷 PKTABLE_CAT 或 FKTABLE_CAT、PKTABLE_SCHEM 或 FKTABLE_SCHEM、PKTABLE_NAME 或 FKTABLE_NAME 以及 PKCOLUMN_NAME 或 FKCOLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫**SQLGetInfo** 。  
  
 ODBC 3.x 的下列資料行已經重新命名 *。* 資料行名稱變更不會影響回溯相容性，因為應用程式會依資料行編號來系結。  
  
|ODBC 2.0 資料行|ODBC 3.x*資料行*|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 下表列出結果集中的資料行。 驅動程式可定義超出資料行14（備註）的其他資料行。 應用程式應該從結果集的結尾向下計算，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱[目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|評價|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT （ODBC 1.0）|1|Varchar|主要索引鍵資料表目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串（""）。|  
|PKTABLE_SCHEM （ODBC 1.0）|2|Varchar|主鍵資料表架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有架構的資料表傳回空字串（""）。|  
|PKTABLE_NAME （ODBC 1.0）|3|Varchar not Null|主要索引鍵資料表名稱。|  
|PKCOLUMN_NAME （ODBC 1.0）|4|Varchar not Null|主要索引鍵資料行名稱。 對於沒有名稱的資料行，驅動程式會傳回空字串。|  
|FKTABLE_CAT （ODBC 1.0）|5|Varchar|外鍵資料表目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串（""）。|  
|FKTABLE_SCHEM （ODBC 1.0）|6|Varchar|外鍵資料表架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不適用於其他資料表，例如當驅動程式從不同的 Dbms 抓取資料時，它會針對沒有架構的資料表傳回空字串（""）。|  
|FKTABLE_NAME （ODBC 1.0）|7|Varchar not Null|外鍵資料表名稱。|  
|FKCOLUMN_NAME （ODBC 1.0）|8|Varchar not Null|外鍵資料行名稱。 對於沒有名稱的資料行，驅動程式會傳回空字串。|  
|KEY_SEQ （ODBC 1.0）|9|Smallint 非 NULL|索引鍵中的資料行序號（從1開始）。|  
|UPDATE_RULE （ODBC 1.0）|10|Smallint|當 SQL 作業**更新**時，要套用至外鍵的動作。 可以具有下列其中一個值。 （參考的資料表是具有主鍵的資料表; 參考資料表是具有外鍵的資料表）。<br /><br /> SQL_CASCADE：當更新參考資料表的主鍵時，也會更新參考資料表的外鍵。<br /><br /> SQL_NO_ACTION：如果參考資料表的主鍵更新會在參考資料表中造成「無關聯參考」（也就是參考資料表中的資料列在參考資料表中不會有任何對應項），則會拒絕更新。 如果參考資料表的外鍵更新所導入的值不是所參考資料表之主鍵的值，則會拒絕更新。 （這個動作與 ODBC 2.x 中的 SQL_RESTRICT 動作相同 *）。*<br /><br /> SQL_SET_Null：當參考資料表中的一個或多個資料列更新時，如果變更了主鍵的一個或多個元件，則參考資料表中對應至已變更之主要索引鍵之元件的外鍵元件會在參考資料表的所有相符資料列中設為 Null。<br /><br /> SQL_SET_DEFAULT：當參考資料表中的一或多個資料列更新時，會變更主鍵的一個或多個元件時，參考資料表中對應至已變更之主要索引鍵之元件的外鍵元件，會在參考資料表的所有相符資料列中設定為適用的預設值。<br /><br /> 如果不適用於資料來源，則為 Null。|  
|DELETE_RULE （ODBC 1.0）|11|Smallint|當 SQL 作業為**刪除**時，要套用至外鍵的動作。 可以具有下列其中一個值。 （參考的資料表是具有主鍵的資料表; 參考資料表是具有外鍵的資料表）。<br /><br /> SQL_CASCADE：刪除參考資料表中的資料列時，也會一併刪除參考資料表中所有相符的資料列。<br /><br /> SQL_NO_ACTION：如果在參考資料表中的資料列刪除會在參考資料表中造成「無關聯參考」（也就是參考資料表中的資料列在參考資料表中不會有任何對應項），則更新會遭到拒絕。 （這個動作與 ODBC 2.x 中的 SQL_RESTRICT 動作相同 *）。*<br /><br /> SQL_SET_Null：當刪除參考資料表中的一個或多個資料列時，參考資料表的外鍵的每個元件都會在參考資料表的所有相符資料列中設為 Null。<br /><br /> SQL_SET_DEFAULT：刪除參考資料表中的一個或多個資料列時，參考資料表外鍵的每個元件都會設定為參考資料表中所有相符資料列的適用預設值。<br /><br /> 如果不適用於資料來源，則為 Null。|  
|FK_NAME （ODBC 2.0）|12|Varchar|外鍵名稱。 如果不適用於資料來源，則為 Null。|  
|PK_NAME （ODBC 2.0）|13|Varchar|主要金鑰名稱。 如果不適用於資料來源，則為 Null。|  
|DEFERRABILITY （ODBC 3.0）|14|Smallint|SQL_INITIALLY_DEFERRED、SQL_INITIALLY_IMMEDIATE SQL_NOT_DEFERRABLE。|  
  
## <a name="code-example"></a>程式碼範例  
 如下表所示，此範例使用三個數據表，名為 ORDERS、LINES 和 CUSTOMERS。  
  
|訂單|水平線|客戶|  
|------------|-----------|---------------|  
|訂單|訂單|CUSTID|  
|CUSTID|水平線|NAME|  
|OPENDATE|PARTID|應對|  
|人員|待|電話|  
|狀態|||  
  
 在 ORDERS 資料表中，CUSTID 會識別已進行銷售的客戶。 這是參考 CUSTOMERS 資料表中 CUSTID 的外鍵。  
  
 在 [行數] 資料表中，[訂單] 會識別與明細專案相關聯的銷售訂單。 這是參考 ORDERS 資料表中之「訂單」的外鍵。  
  
 這個範例會呼叫**SQLPrimaryKeys**來取得 ORDERS 資料表的主鍵。 結果集將會有一個資料列;下表顯示重要的資料行。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|訂單|訂單|1|  
  
 接下來，此範例會呼叫**SQLForeignKeys** ，以取得其他資料表中參考 ORDERS 資料表之主鍵的外鍵。 結果集將會有一個資料列;下表顯示重要的資料行。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|訂單|CUSTID|水平線|CUSTID|1|  
  
 最後，此範例會呼叫**SQLForeignKeys** ，以取得 ORDERS 資料表中參考其他資料表之主鍵的外鍵。 結果集將會有一個資料列;下表顯示重要的資料行。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|客戶|CUSTID|訂單|CUSTID|1|  
  
```cpp  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主要金鑰的資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|傳回資料表統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
