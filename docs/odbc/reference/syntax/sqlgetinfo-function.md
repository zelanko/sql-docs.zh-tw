---
title: SQLGetInfo 函式 |Microsoft Docs
ms.custom: ''
ms.date: 05/28/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce6c9e6032201f41eae058c9553f9bd61c4f079
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279572"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函數

**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLGetInfo**會傳回與連接相關聯的驅動程式和資料來源的一般資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  

 *ConnectionHandle*  
 [輸入] 連線控制代碼。  
  
 *InfoType*  
 源資訊的類型。  
  
 *InfoValuePtr*  
 輸出要傳回信息的緩衝區指標。 根據所要求的*InfoType*而定，傳回的資訊將會是下列其中一項：以 null 結束的字元字串、SQLUSMALLINT 值、SQLUINTEGER 位元遮罩、SQLUINTEGER 旗標、SQLUINTEGER 二進位值或 SQLULEN 值。  
  
 如果*InfoType*引數 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT，則*InfoValuePtr*引數為輸入和輸出。 如需詳細資訊， (參閱此函式描述中的 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT 描述元。 )   
  
 如果*InfoValuePtr*為 Null， *StringLengthPtr*仍會傳回位元組總數， (排除字元資料的 Null 終止字元，) 可在*InfoValuePtr*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 源\* *InfoValuePtr*緩衝區的長度。 如果* \* InfoValuePtr*中的值不是字元字串，或如果*InfoValuePtr*是 null 指標，則會忽略*BufferLength*引數。 驅動程式會假設* \* InfoValuePtr*的大小為 SQLUSMALLINT 或 SQLUINTEGER （根據*InfoType*）。 如果* \* InfoValuePtr*是在呼叫**SQLGetInfoW**) 時 (的 Unicode 字串， *BufferLength*引數必須是偶數; 如果不是，則會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 。  
  
 *StringLengthPtr*  
 輸出緩衝區的指標，會在其中傳回位元組總數 (排除字元資料的 null 終止字元，) 可在 **InfoValuePtr*中傳回。  
  
 若是字元資料，如果傳回的位元組數目大於或等於*BufferLength*，則 InfoValuePtr 中的資訊 \* *InfoValuePtr*會截斷為*BufferLength*位元組減去 null 終止字元的長度，並由驅動程式以 null 終止。  
  
 對於所有其他類型的資料，會忽略*BufferLength*的值，而驅動程式會假設 \* *INFOVALUEPTR*的大小為 SQLUSMALLINT 或 SQLUINTEGER，視*InfoType*而定。  
  
## <a name="returns"></a>傳回  

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  

 當**SQLGetInfo**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_DBC *HandleType*和*ConnectionHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLGetInfo**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *InfoValuePtr*不夠大，無法傳回所有要求的資訊。 因此，此資訊已遭截斷。 在 **StringLengthPtr*中，會傳回其 untruncated 表單中所要求的資訊長度。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08003|連接未開啟| (DM) 在*InfoType*中要求的資訊類型需要開啟連接。 在 ODBC 所保留的資訊類型中，只有在沒有開啟連接的情況下，才會傳回 SQL_ODBC_VER。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 * \* MessageText*緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|已針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY024|不正確屬性值| (DM) 已 SQL_DRIVER_HSTMT *InfoType*引數，且*InfoValuePtr*所指向的值不是有效的語句控制碼。<br /><br />  (DM) 已 SQL_DRIVER_HDESC *InfoType*引數，且*InfoValuePtr*所指向的值不是有效的描述項控制碼。|  
|HY090|不正確字串或緩衝區長度| (DM) 為引數*BufferLength*指定的值小於0。<br /><br />  (DM) 為*BufferLength*指定的值是奇數，而* \* InfoValuePtr*是 Unicode 資料類型。|  
|HY096|資訊類型超出範圍|為引數*InfoType*指定的值對驅動程式所支援的 ODBC 版本無效。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran](sqlendtran-function.md)函式。|  
|HYC00|未執行選擇性欄位|針對引數*InfoType*所指定的值，是驅動程式不支援的驅動程式特定值。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能| (DM) 對應至*ConnectionHandle*的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  

 本章節稍後的「資訊類型」中會顯示目前定義的資訊類型;預期會有更多的定義，以利用不同的資料來源。 資訊類型的範圍是由 ODBC 所保留;驅動程式開發人員必須從開啟的群組中，保留自己的驅動程式特有的值。 **SQLGetInfo**不會執行 Unicode 轉換或*Thunking* (請參閱[附錄 A：](../appendixes/appendix-a-odbc-error-codes.md) odbc 程式設計*人員參考*) 的 odbc 錯誤碼，以取得驅動程式定義的*InfoTypes*。 如需詳細資訊，請參閱[驅動程式特有的資料類型、描述項類型、資訊類型、診斷類型和屬性](../develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 InfoValuePtr 中傳回的資訊格式 \* *InfoValuePtr*取決於所要求的*InfoType* 。 **SQLGetInfo**會以五種不同格式的其中一種來傳回信息：  
  
- 以 null 結束的字元字串  
  
- SQLUSMALLINT 值  
  
- SQLUINTEGER 位元遮罩  
  
- SQLUINTEGER 值  
  
- SQLUINTEGER 二進位值  
  
 類型的描述中會注明下列每個資訊類型的格式。 應用程式必須據以轉換 **InfoValuePtr*中傳回的值。 如需應用程式如何從 SQLUINTEGER 的位元遮罩取得資料的範例，請參閱「程式碼範例」。  
  
 驅動程式必須針對下表中定義的每個資訊類型傳回值。 如果資訊類型不適用於驅動程式或資料來源，驅動程式會傳回下表所列的其中一個值。  

|||
|-|-|
|字元字串 ( "Y" 或 "N" ) |"N"|
|字元字串 (不是 "Y" 或 "N" ) |空字串|
|SQLUSMALLINT|0|
|SQLUINTEGER 位元遮罩或 SQLUINTEGER 二進位值|0L|
  
 例如，如果資料來源不支援程式， **SQLGetInfo**會針對與程式相關的*InfoType*值，傳回下表所列的值。  

|||
|-|-|
|SQL_PROCEDURES|"N"|
|SQL_ACCESSIBLE_PROCEDURES|"N"|
|SQL_MAX_PROCEDURE_NAME_LEN|0|
|SQL_PROCEDURE_TERM|空字串|
  
 **SQLGetInfo**會傳回 SQLSTATE HY096 (不正確引數值) *，這些*值位於保留供 ODBC 使用的資訊類型範圍內，但不是由驅動程式所支援的 ODBC 版本所定義。 為了判斷驅動程式符合哪個版本的 ODBC，應用程式會使用 SQL_DRIVER_ODBC_VER 資訊類型來呼叫**SQLGetInfo** 。 **SQLGetInfo**會傳回 SQLSTATE HYC00 (選擇性功能未針對*InfoType*的值所實) 作為，這是保留供驅動程式特定使用，但驅動程式不支援的資訊類型範圍內。  
  
 所有對**SQLGetInfo**的呼叫都需要開啟的連接，但當*InfoType*是 SQL_ODBC_VER 時，會傳回驅動程式管理員的版本。  
  
## <a name="information-types"></a>資訊類型  

 本節列出**SQLGetInfo**所支援的資訊類型。 資訊類型會分組 categorically，並依字母順序列出。 也會列出針對 ODBC 3.x 加入或重新命名*的資訊*類型。  
  
## <a name="driver-information"></a>驅動程式資訊  

 下列*InfoType*引數的值會傳回 ODBC 驅動程式的相關資訊，例如使用中語句的數目、資料來源名稱和介面標準合規性層級：  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_FILE_USAGE|  
|SQL_ASYNC_MODE|SQL_GETDATA_EXTENSIONS|  
|SQL_ASYNC_NOTIFICATION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_BATCH_ROW_COUNT|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_BATCH_SUPPORT|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_DATA_SOURCE_NAME|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|SQL_MAX_CONCURRENT_ACTIVITIES|  
|SQL_DRIVER_HDBC|SQL_MAX_DRIVER_CONNECTIONS|  
|SQL_DRIVER_HDESC|SQL_ODBC_INTERFACE_CONFORMANCE|  
|SQL_DRIVER_HENV|SQL_ODBC_STANDARD_CLI_CONFORMANCE|  
|SQL_DRIVER_HLIB|SQL_ODBC_VER|  
|SQL_DRIVER_HSTMT|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_DRIVER_NAME|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DRIVER_ODBC_VER|SQL_ROW_UPDATES|  
|SQL_DRIVER_VER|SQL_SEARCH_PATTERN_ESCAPE|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|SQL_SERVER_NAME|  
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|SQL_STATIC_CURSOR_ATTRIBUTES2|  
  
> [!NOTE]  
> 在執行**SQLGetInfo**時，驅動程式可以將資訊從伺服器傳送或要求的次數減至最少，藉此改善效能。  
  
## <a name="dbms-product-information"></a>DBMS 產品資訊  

 下列*InfoType*引數的值會傳回 dbms 產品的相關資訊，例如 dbms 名稱和版本：  

|||
|-|-|
|SQL_DATABASE_NAME|SQL_DBMS_NAME|
|SQL_DBMS_VER||
  
## <a name="data-source-information"></a>資料來源資訊  

 下列*InfoType*引數的值會傳回資料來源的相關資訊，例如資料指標特性和交易功能：  
  
|||  
|-|-|  
|SQL_ACCESSIBLE_PROCEDURES|SQL_MULT_RESULT_SETS|  
|SQL_ACCESSIBLE_TABLES|SQL_MULTIPLE_ACTIVE_TXN|  
|SQL_BOOKMARK_PERSISTENCE|SQL_NEED_LONG_DATA_LEN|  
|SQL_CATALOG_TERM|SQL_NULL_COLLATION|  
|SQL_COLLATION_SEQ|SQL_PROCEDURE_TERM|  
|SQL_CONCAT_NULL_BEHAVIOR|SQL_SCHEMA_TERM|  
|SQL_CURSOR_COMMIT_BEHAVIOR|SQL_SCROLL_OPTIONS|  
|SQL_CURSOR_ROLLBACK_BEHAVIOR|SQL_TABLE_TERM|  
|SQL_CURSOR_SENSITIVITY|SQL_TXN_CAPABLE|  
|SQL_DATA_SOURCE_READ_ONLY|SQL_TXN_ISOLATION_OPTION|  
|SQL_DEFAULT_TXN_ISOLATION|SQL_USER_NAME|  
|SQL_DESCRIBE_PARAMETER||  
  
## <a name="supported-sql"></a>支援的 SQL  

 下列*InfoType*引數的值會傳回資料來源所支援之 SQL 語句的相關資訊。 這些資訊類型所描述之每項功能的 SQL 語法都是 SQL-92 語法。 這些資訊類型並不會詳盡說明整個 SQL-92 文法。 相反地，它們會描述文法中的那些部分，其中的資料來源通常會提供不同層級的支援。 具體而言，SQL-92 中大部分的 DDL 語句都會涵蓋在內。  
  
 應用程式應該從 SQL_SQL_CONFORMANCE 資訊類型判斷支援的文法一般層級，並使用其他資訊類型來判斷來自所述標準合規性層級的變化。  
  
|||  
|-|-|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DROP_TABLE|  
|SQL_ALTER_DOMAIN|SQL_DROP_TRANSLATION|  
|SQL_ALTER_SCHEMA|SQL_DROP_VIEW|  
|SQL_ALTER_TABLE|SQL_EXPRESSIONS_IN_ORDERBY|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_GROUP_BY|  
|SQL_CATALOG_LOCATION|SQL_IDENTIFIER_CASE|  
|SQL_CATALOG_NAME|SQL_IDENTIFIER_QUOTE_CHAR|  
|SQL_CATALOG_NAME_SEPARATOR|SQL_INDEX_KEYWORDS|  
|SQL_CATALOG_USAGE|SQL_INSERT_STATEMENT|  
|SQL_COLUMN_ALIAS|SQL_INTEGRITY|  
|SQL_CORRELATION_NAME|SQL_KEYWORDS|  
|SQL_CREATE_ASSERTION|SQL_LIKE_ESCAPE_CLAUSE|  
|SQL_CREATE_CHARACTER_SET|SQL_NON_NULLABLE_COLUMNS|  
|SQL_CREATE_COLLATION|SQL_SQL_CONFORMANCE|  
|SQL_CREATE_DOMAIN|SQL_OJ_CAPABILITIES|  
|SQL_CREATE_SCHEMA|SQL_ORDER_BY_COLUMNS_IN_SELECT|  
|SQL_CREATE_TABLE|SQL_OUTER_JOINS|  
|SQL_CREATE_TRANSLATION|SQL_PROCEDURES|  
|SQL_DDL_INDEX|SQL_QUOTED_IDENTIFIER_CASE|  
|SQL_DROP_ASSERTION|SQL_SCHEMA_USAGE|  
|SQL_DROP_CHARACTER_SET|SQL_SPECIAL_CHARACTERS|  
|SQL_DROP_COLLATION|SQL_SUBQUERIES|  
|SQL_DROP_DOMAIN|SQL_UNION|  
|SQL_DROP_SCHEMA||  
  
## <a name="sql-limits"></a>SQL 限制  

 下列*InfoType*引數的值會傳回套用至 SQL 語句中的識別碼和子句之限制的相關資訊，例如識別碼的最大長度和選取清單中的最大資料行數目。 驅動程式或資料來源可能會加諸限制。  
  
|||  
|-|-|  
|SQL_MAX_BINARY_LITERAL_LEN|SQL_MAX_IDENTIFIER_LEN|  
|SQL_MAX_CATALOG_NAME_LEN|SQL_MAX_INDEX_SIZE|  
|SQL_MAX_CHAR_LITERAL_LEN|SQL_MAX_PROCEDURE_NAME_LEN|  
|SQL_MAX_COLUMN_NAME_LEN|SQL_MAX_ROW_SIZE|  
|SQL_MAX_COLUMNS_IN_GROUP_BY|SQL_MAX_ROW_SIZE_INCLUDES_LONG|  
|SQL_MAX_COLUMNS_IN_INDEX|SQL_MAX_SCHEMA_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_ORDER_BY|SQL_MAX_STATEMENT_LEN|  
|SQL_MAX_COLUMNS_IN_SELECT|SQL_MAX_TABLE_NAME_LEN|  
|SQL_MAX_COLUMNS_IN_TABLE|SQL_MAX_TABLES_IN_SELECT|  
|SQL_MAX_CURSOR_NAME_LEN|SQL_MAX_USER_NAME_LEN|  
  
## <a name="scalar-function-information"></a>純量函數資訊  

 下列*InfoType*引數的值會傳回資料來源和驅動程式所支援之純量函數的相關資訊。 如需純量函式的詳細資訊，請參閱[附錄 E：](../appendixes/appendix-e-scalar-functions.md)純量函數。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>轉換資訊  

 *InfoType*引數的下列值會傳回 sql 資料類型的清單，資料來源可以使用**convert**純量函數來轉換指定的 sql 資料類型：  
  
|||  
|-|-|  
|SQL_CONVERT_BIGINT|SQL_CONVERT_LONGVARBINARY|  
|SQL_CONVERT_BINARY|SQL_CONVERT_LONGVARCHAR|  
|SQL_CONVERT_BIT|SQL_CONVERT_NUMERIC|  
|SQL_CONVERT_CHAR|SQL_CONVERT_REAL|  
|SQL_CONVERT_DATE|SQL_CONVERT_SMALLINT|  
|SQL_CONVERT_DECIMAL|SQL_CONVERT_TIME|  
|SQL_CONVERT_DOUBLE|SQL_CONVERT_TIMESTAMP|  
|SQL_CONVERT_FLOAT|SQL_CONVERT_TINYINT|  
|SQL_CONVERT_INTEGER|SQL_CONVERT_VARBINARY|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_CONVERT_VARCHAR|  
|SQL_CONVERT_INTERVAL_DAY_TIME||  
  
## <a name="information-types-added-for-odbc-3x"></a>為 ODBC 3.x 新增的資訊類型  

 ODBC 3.x 已加入下列*InfoType*引數的值：  
  
|||  
|-|-|  
|SQL_ACTIVE_ENVIRONMENTS|SQL_DRIVER_AWARE_POOLING_SUPPORTED|  
|SQL_AGGREGATE_FUNCTIONS|SQL_DRIVER_HDESC|  
|SQL_ALTER_DOMAIN|SQL_DROP_ASSERTION|  
|SQL_ALTER_SCHEMA|SQL_DROP_CHARACTER_SET|  
|SQL_ANSI_SQL_DATETIME_LITERALS|SQL_DROP_COLLATION|  
|SQL_ASYNC_DBC_FUNCTIONS|SQL_DROP_DOMAIN|  
|SQL_ASYNC_MODE|SQL_DROP_SCHEMA|  
|SQL_ASYNC_NOTIFICATION|SQL_DROP_TABLE|  
|SQL_BATCH_ROW_COUNT|SQL_DROP_TRANSLATION|  
|SQL_BATCH_SUPPORT|SQL_DROP_VIEW|  
|SQL_CATALOG_NAME|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|  
|SQL_COLLATION_SEQ|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
|SQL_CONVERT_INTERVAL_YEAR_MONTH|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|  
|SQL_CONVERT_INTERVAL_DAY_TIME|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_ASSERTION|SQL_INFO_SCHEMA_VIEWS|  
|SQL_CREATE_CHARACTER_SET|SQL_INSERT_STATEMENT|  
|SQL_CREATE_COLLATION|SQL_KEYSET_CURSOR_ATTRIBUTES1|  
|SQL_CREATE_DOMAIN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
|SQL_CREATE_SCHEMA|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|  
|SQL_CREATE_TABLE|SQL_MAX_IDENTIFIER_LEN|  
|SQL_CREATE_TRANSLATION|SQL_PARAM_ARRAY_ROW_COUNTS|  
|SQL_CURSOR_SENSITIVITY|SQL_PARAM_ARRAY_SELECTS|  
|SQL_DDL_INDEX|SQL_STATIC_CURSOR_ATTRIBUTES1|  
|SQL_DESCRIBE_PARAMETER|SQL_STATIC_CURSOR_ATTRIBUTES2|  
|SQL_DM_VER|SQL_XOPEN_CLI_YEAR|  
  
## <a name="information-types-renamed-for-odbc-3x"></a>為 ODBC 3.x 重新命名的資訊類型  

 ODBC 3.x 的下列*InfoType*引數值已經重新命名。  

|舊名稱|新名稱|  
|-|-|  
|SQL_ACTIVE_CONNECTIONS|SQL_MAX_DRIVER_CONNECTIONS|
|SQL_ACTIVE_STATEMENTS|SQL_MAX_CONCURRENT_ACTIVITIES|
|SQL_MAX_OWNER_NAME_LEN|SQL_MAX_SCHEMA_NAME_LEN|
|SQL_MAX_QUALIFIER_NAME_LEN|SQL_MAX_CATALOG_NAME_LEN|
|SQL_ODBC_SQL_OPT_IEF|SQL_INTEGRITY|
|SQL_OWNER_TERM|SQL_SCHEMA_TERM|
|SQL_OWNER_USAGE|SQL_SCHEMA_USAGE|
|SQL_QUALIFIER_LOCATION|SQL_CATALOG_LOCATION|
|SQL_QUALIFIER_NAME_SEPARATOR|SQL_CATALOG_NAME_SEPARATOR|
|SQL_QUALIFIER_TERM|SQL_CATALOG_TERM|
|SQL_QUALIFIER_USAGE|SQL_CATALOG_USAGE|
  
## <a name="information-types-deprecated-in-odbc-3x"></a>ODBC 3.x 中已淘汰的資訊類型  

 ODBC 3.x 中的下列*InfoType*引數值已被取代。 ODBC 3.x 驅動程式必須繼續支援這些資訊類型，以提供與 ODBC 2.x 應用程式的回溯相容性。  (需這些類型的詳細資訊，請參閱附錄 G：驅動程式指導方針中的[SQLGetInfo 支援](../appendixes/sqlgetinfo-support.md)，以取得回溯相容性。 )   
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>資訊類型描述  

下表依字母順序列出每種資訊類型、引進它的 ODBC 版本，以及其描述。  
  
|資訊類型|ODBC 版本|描述|
|-|-|-|
|SQL_ACCESSIBLE_PROCEDURES|1.0|字元字串：如果使用者可以執行**SQLProcedures**所傳回的所有程式，則為 "Y";如果可能會傳回使用者無法執行的程式，則為 "N"。|
|SQL_ACCESSIBLE_TABLES|1.0|字元字串： "Y"，如果使用者保證對**SQLTables**所傳回的所有資料表具有**SELECT**許可權，如果可能會傳回使用者無法存取的資料表，則為 "N"。|
|SQL_ACTIVE_ENVIRONMENTS|3.0|SQLUSMALLINT 值，指定驅動程式可支援的作用中環境數目上限。 如果沒有指定的限制，或限制不明，此值會設定為零。|
|SQL_AGGREGATE_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩列舉彙總函式的支援：<br/>SQL_AF_ALL<br/>SQL_AF_AVG<br/>SQL_AF_COUNT<br/>SQL_AF_DISTINCT<br/>SQL_AF_MAX<br/>SQL_AF_MIN<br/>SQL_AF_SUM<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_ALTER_DOMAIN|3.0|SQLUINTEGER 位元遮罩，用來列舉**ALTER DOMAIN**語句中的子句（如 SQL-92 中所定義，由資料來源所支援）。 SQL-92 完整層級相容的驅動程式一律會傳回所有的位元遮罩。 傳回值 "0" 表示不支援**ALTER DOMAIN**語句。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_AD_ADD_DOMAIN_CONSTRAINT = (完整層級支援新增網域條件約束) <br/>\<alter domain> \<set domain default clause> (完整層級支援 SQL_AD_ADD_DOMAIN_DEFAULT =) <br/>SQL_AD_CONSTRAINT_NAME_DEFINITION = \<constraint name definition clause> 支援命名網域條件約束 (中繼層級) <br/>\<drop domain constraint clause> (完整層級支援 SQL_AD_DROP_DOMAIN_CONSTRAINT =) <br/>\<alter domain> \<drop domain default clause> (完整層級支援 SQL_AD_DROP_DOMAIN_DEFAULT =) <br/><br/>\<constraint attributes>如果 \<add domain constraint> 支援， (SQL_AD_ADD_DOMAIN_CONSTRAINT 位設定) ，下列位會指定支援的：<br/>SQL_AD_ADD_CONSTRAINT_DEFERRABLE (完整層級) <br/>SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (完整層級) <br/>SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (完整層級) <br/>SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級) |
|SQL_ALTER_TABLE|2.0|SQLUINTEGER 位元遮罩，列舉資料來源所支援之**ALTER TABLE**語句中的子句。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>支援 SQL_AT_ADD_COLUMN_COLLATION = \<add column> 子句，其具備指定資料行定序 (完整層級)  (ODBC 3.0 的功能) <br/>支援 SQL_AT_ADD_COLUMN_DEFAULT = \<add column> 子句，而設備可指定資料行預設值 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_ADD_COLUMN_SINGLE = \<add column> 支援 (FIPS 過渡層級)  (ODBC 3.0) <br/>支援 SQL_AT_ADD_CONSTRAINT = \<add column> 子句，並可指定 (FIPS 過渡層級的資料行條件約束)  (ODBC 3.0) <br/>SQL_AT_ADD_TABLE_CONSTRAINT = \<add table constraint> 子句支援 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 支援命名資料行和資料表條件約束， (中繼層級)  (ODBC 3.0) <br/>SQL_AT_DROP_COLUMN_CASCADE = \<drop column> CASCADE 支援 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_DROP_COLUMN_DEFAULT = \<alter column> \<drop column default clause> 支援 (中繼層級)  (ODBC 3.0) <br/>SQL_AT_DROP_COLUMN_RESTRICT = \<drop column> 限制支援 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0) <br/>SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<drop column> 限制支援 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_SET_COLUMN_DEFAULT = \<alter column> \<set column default clause> 支援 (中繼層級)  (ODBC 3.0) <br/><br/>\<constraint attributes>如果支援指定資料行或資料表條件約束， (SQL_AT_ADD_CONSTRAINT 位設定) ，下列位會指定支援：<br/>SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (完整層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_DEFERRABLE (完整層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_NON_DEFERRABLE (完整層級)  (ODBC 3.0) |
|SQL_ASYNC_DBC_FUNCTIONS|3.8|SQLUINTEGER 值，指出驅動程式能否以非同步方式在連接控制碼上執行函數。<br/><br/>SQL_ASYNC_DBC_CAPABLE = 驅動程式可以非同步執行連接功能。<br/>SQL_ASYNC_DBC_NOT_CAPABLE = 驅動程式無法以非同步方式執行連接功能。|
|SQL_ASYNC_MODE|3.0|指出驅動程式中非同步支援層級的 SQLUINTEGER 值：<br/><br/>SQL_AM_CONNECTION = 支援連接層級非同步執行。 所有與給定連接控制碼相關聯的語句控制碼都處於非同步模式或全都處於同步模式。 連接上的語句控制碼不能處於非同步模式，而相同連接上的另一個語句控制碼處於同步模式，反之亦然。<br/>支援 SQL_AM_STATEMENT = 語句層級非同步執行。 某些與連接控制碼相關聯的語句控制碼可以處於非同步模式，而相同連接上的其他語句控制碼則處於同步模式。<br/>SQL_AM_NONE = 不支援非同步模式。|
|SQL_ASYNC_NOTIFICATION|3.8|指出驅動程式是否支援非同步通知的 SQLUINTEGER 值：<br/><br/>SQL_ASYNC_NOTIFICATION_CAPABLE = 驅動程式支援非同步執行通知。<br/>SQL_ASYNC_NOTIFICATION_NOT_CAPABLE = 驅動程式不支援非同步執行通知。<br/><br/>ODBC 非同步作業有兩種類別：連接層級非同步作業和語句層級非同步作業。  如果驅動程式傳回 SQL_ASYNC_NOTIFICATION_CAPABLE，它必須支援可非同步執行之所有 Api 的通知。|
|SQL_BATCH_ROW_COUNT|3.0|SQLUINTEGER 位元遮罩，可列舉與資料列計數可用性有關的驅動程式行為。 下列位元遮罩會與資訊類型一起使用：<br/><br/>SQL_BRC_ROLLED_UP = 連續 INSERT、DELETE 或 UPDATE 語句的資料列計數會匯總成一個。 如果未設定此位，每個語句都可以使用資料列計數。<br/>SQL_BRC_PROCEDURES = 在預存程式中執行批次時，可以使用資料列計數（如果有的話）。 如果有可用的資料列計數，視 SQL_BRC_ROLLED_UP 位而定，您可以匯總或個別使用它們。<br/>SQL_BRC_EXPLICIT = 當直接呼叫**SQLExecute**或**SQLExecDirect**來執行批次時，可以使用資料列計數（如果有的話）。 如果有可用的資料列計數，視 SQL_BRC_ROLLED_UP 位而定，您可以匯總或個別使用它們。|
|SQL_BATCH_SUPPORT|3.0|SQLUINTEGER 的位元遮罩，列舉驅動程式對批次的支援。 下列位元遮罩是用來判斷支援的層級：<br/><br/>SQL_BS_SELECT_EXPLICIT = 驅動程式支援可產生結果集產生語句的明確批次。<br/>SQL_BS_ROW_COUNT_EXPLICIT = 驅動程式支援可擁有資料列計數產生語句的明確批次。<br/>SQL_BS_SELECT_PROC = 驅動程式支援可產生結果集產生語句的明確程式。<br/>SQL_BS_ROW_COUNT_PROC = 驅動程式支援可讓資料列計數產生語句的明確程式。|
|SQL_BOOKMARK_PERSISTENCE|2.0|SQLUINTEGER 的位元遮罩，可列舉書簽保存的作業。 下列位元遮罩會與旗標一起使用，以判斷書簽會保存哪些選項：<br/><br/>SQL_BP_CLOSE = 當應用程式使用 SQL_CLOSE 選項呼叫**SQLFreeStmt** ，或是**SQLCloseCursor**關閉與語句相關聯的資料指標之後，書簽是有效的。<br/>SQL_BP_DELETE = 資料列的書簽在刪除該資料列之後有效。<br/>SQL_BP_DROP = 當應用程式呼叫具有*HandleType* SQL_HANDLE_STMT 的**SQLFreeHandle**來卸載語句之後，書簽是有效的。<br/>SQL_BP_TRANSACTION = 在應用程式認可或回復交易之後，書簽是有效的。<br/>SQL_BP_UPDATE = 在更新該資料列中的任何資料行之後，資料列的書簽是有效的，包括索引鍵資料行。<br/>SQL_BP_OTHER_HSTMT = 與一個語句相關聯的書簽可以與另一個語句搭配使用。 除非指定 SQL_BP_CLOSE 或 SQL_BP_DROP，否則第一個語句上的資料指標必須是開啟的。|
|SQL_CATALOG_LOCATION|2.0|SQLUSMALLINT 值，指出目錄在限定資料表名稱中的位置：<br/><br/>SQL_CL_START<br/>SQL_CL_END<br/>例如，Xbase 驅動程式會傳回 SQL_CL_START，因為目錄 (目錄) 名稱是在資料表名稱的開頭，如 \EMPDATA\EMP。DBF. ORACLE 伺服器驅動程式會傳回 SQL_CL_END，因為目錄位於資料表名稱的結尾，如所示 ADMIN.EMP@EMPDATA 。<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回 SQL_CL_START。 如果資料來源不支援目錄，則會傳回0值。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫**SQLGetInfo** 。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_LOCATION 重新命名為 odbc 3.0。|
|SQL_CATALOG_NAME|3.0|字元字串：如果伺服器支援目錄名稱，則為 "Y"，否則為 "N"。<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回 "Y"。|
|SQL_CATALOG_NAME_SEPARATOR|1.0|字元字串：資料來源在目錄名稱與其後或之前的限定名稱元素之間定義為分隔符號的字元。<br/><br/>如果資料來源不支援目錄，則會傳回空字串。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫**SQLGetInfo** 。 符合 SQL 92 完整層級的驅動程式一律會傳回 "."。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_NAME_SEPARATOR 重新命名為 odbc 3.0。|
|SQL_CATALOG_TERM|1.0|具有目錄之資料來源廠商名稱的字元字串;例如，"database" 或 "directory"。 這個字串可以是大寫、小寫或混合大小寫。<br/><br/>如果資料來源不支援目錄，則會傳回空字串。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫**SQLGetInfo** 。 符合 SQL 92 完整層級的驅動程式一律會傳回「目錄」。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_TERM 重新命名為 odbc 3.0。|
|SQL_CATALOG_USAGE|2.0|SQLUINTEGER 的位元遮罩，列舉可以使用目錄的語句。<br/><br/>下列位元遮罩可用來判斷目錄的使用位置：<br/>SQL_CU_DML_STATEMENTS = 所有資料操作語言語句都支援目錄： **select**、 **INSERT**、 **UPDATE**、 **DELETE**和 if 支援，請**選取以取得 update**和定位 update 和 DELETE 子句。<br/>SQL_CU_PROCEDURE_INVOCATION = ODBC 程序呼叫語句中支援目錄。<br/>SQL_CU_TABLE_DEFINITION = 所有資料表定義語句都支援目錄： **CREATE TABLE**、 **CREATE VIEW**、 **ALTER TABLE**、 **drop table**和**drop VIEW**。<br/>SQL_CU_INDEX_DEFINITION = 所有索引定義語句中都支援目錄： **CREATE INDEX**和**DROP INDEX**。<br/>SQL_CU_PRIVILEGE_DEFINITION = 擁有權限定義語句中都支援目錄： **GRANT**和**REVOKE**。<br/><br/>如果資料來源不支援目錄，則會傳回0值。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫**SQLGetInfo** 。 符合 SQL 92 完整層級的驅動程式一律會傳回具有所有這些位集的位元遮罩。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_USAGE 重新命名為 odbc 3.0。|
|SQL_COLLATION_SEQ|3.0|定序順序的名稱。 這是一個字元字串，表示此伺服器預設字元集的預設定序名稱 (例如 ' ISO 8859-1 ' 或 EBCDIC) 。 如果這是未知的，則會傳回空字串。 符合 SQL 92 完整層級的驅動程式一律會傳回非空白字串。|
|SQL_COLUMN_ALIAS|2.0|字元字串：如果資料來源支援資料行別名，則為 "Y";否則為 "N"。<br/><br/>資料行別名是可以使用 AS 子句，針對選取清單中的資料行指定的替代名稱。 符合 SQL 92 專案層級的驅動程式一律會傳回 "Y"。|
|SQL_CONCAT_NULL_BEHAVIOR|1.0|SQLUSMALLINT 值，指出資料來源如何處理 Null 值字元資料類型資料行與非 Null 值字元資料類型資料行的串連：<br/>SQL_CB_Null = 結果為 Null 值。<br/>SQL_CB_NON_Null = Result 會串連非 Null 值的資料行或資料行。<br/><br/>符合 SQL 92 專案層級的驅動程式一律會傳回 SQL_CB_Null。|
|SQL_CONVERT_BIGINT<br/>SQL_CONVERT_BINARY<br/>SQL_CONVERT_BIT<br/>SQL_CONVERT_CHAR<br/>SQL_CONVERT_GUID<br/>SQL_CONVERT_DATE<br/>SQL_CONVERT_DECIMAL<br/>SQL_CONVERT_DOUBLE<br/>SQL_CONVERT_FLOAT<br/>SQL_CONVERT_INTEGER<br/>SQL_CONVERT_INTERVAL_YEAR_MONTH<br/>SQL_CONVERT_INTERVAL_DAY_TIME<br/>SQL_CONVERT_LONGVARBINARY<br/>SQL_CONVERT_LONGVARCHAR<br/>SQL_CONVERT_NUMERIC<br/>SQL_CONVERT_REAL<br/>SQL_CONVERT_SMALLINT<br/>SQL_CONVERT_TIME<br/>SQL_CONVERT_TIMESTAMP<br/>SQL_CONVERT_TINYINT<br/>SQL_CONVERT_VARBINARY<br/>SQL_CONVERT_VARCHAR|1.0|SQLUINTEGER 位元遮罩。 位元遮罩指出資料來源所支援的轉換，以及*InfoType*中名為之型別資料的**CONVERT**純量函數。 如果位元遮罩等於零，則資料來源不支援從已命名類型的資料進行任何轉換，包括轉換成相同的資料類型。<br/><br/>例如，若要判斷資料來源是否支援將 SQL_INTEGER 資料轉換成 SQL_BIGINT 資料類型，應用程式會以 SQL_CONVERT_INTEGER 的*InfoType*呼叫**SQLGetInfo** 。 應用程式會使用傳回的位元遮罩和 SQL_CVT_BIGINT 來執行**AND**運算。 如果產生的值不是零，則會支援轉換。<br/><br/>下列位元遮罩是用來決定支援的轉換：<br/>SQL_CVT_BIGINT (ODBC 1.0) <br/>SQL_CVT_BINARY (ODBC 1.0) <br/>SQL_CVT_BIT (ODBC 1.0) <br/>SQL_CVT_GUID (ODBC 3.5) <br/>SQL_CVT_CHAR (ODBC 1.0) <br/>SQL_CVT_DATE (ODBC 1.0) <br/>SQL_CVT_DECIMAL (ODBC 1.0) <br/>SQL_CVT_DOUBLE (ODBC 1.0) <br/>SQL_CVT_FLOAT (ODBC 1.0) <br/>SQL_CVT_INTEGER (ODBC 1.0) <br/>SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) <br/>SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) <br/>SQL_CVT_LONGVARBINARY (ODBC 1.0) <br/>SQL_CVT_LONGVARCHAR (ODBC 1.0) <br/>SQL_CVT_NUMERIC (ODBC 1.0) <br/>SQL_CVT_REAL (ODBC 1.0) <br/>SQL_CVT_SMALLINT (ODBC 1.0) <br/>SQL_CVT_TIME (ODBC 1.0) <br/>SQL_CVT_TIMESTAMP (ODBC 1.0) <br/>SQL_CVT_TINYINT (ODBC 1.0) <br/>SQL_CVT_VARBINARY (ODBC 1.0) <br/>SQL_CVT_VARCHAR (ODBC 1.0) |
|SQL_CONVERT_FUNCTIONS|1.0|SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量轉換函式。<br/><br/>下列位元遮罩是用來決定支援的轉換函式：<br/>SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT|
|SQL_CORRELATION_NAME|1.0|SQLUSMALLINT 值，指出是否支援資料表相互關聯名稱：<br/>SQL_CN_NONE = 不支援相互關聯名稱。<br/>SQL_CN_DIFFERENT = 支援相互關聯名稱，但必須與它們所代表的資料表名稱不同。<br/>SQL_CN_ANY = 相互關聯名稱是支援的，而且可以是任何有效的使用者定義名稱。<br/><br/>符合 SQL 92 專案層級的驅動程式一律會傳回 SQL_CN_ANY。|
|SQL_CREATE_ASSERTION|3.0|SQLUINTEGER 位元遮罩，列舉**CREATE**判斷提示語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_CA_CREATE_ASSERTION<br/><br/>如果支援明確指定條件約束屬性的能力，下列位會指定支援的條件約束屬性 (參閱 SQL_ALTER_TABLE 和 SQL_CREATE_TABLE 資訊類型) ：<br/>SQL_CA_CONSTRAINT_INITIALLY_DEFERRED<br/>SQL_CA_CONSTRAINT_INITIALLY_IMMEDIATE<br/>SQL_CA_CONSTRAINT_DEFERRABLE<br/>SQL_CA_CONSTRAINT_NON_DEFERRABLE<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回所有這些選項，並受到支援。 傳回值 "0" 表示不支援**CREATE ASSERTION**語句。|
|SQL_CREATE_CHARACTER_SET|3.0|SQLUINTEGER 位元遮罩，列舉**CREATE CHARACTER SET**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_CCS_CREATE_CHARACTER_SET<br/>SQL_CCS_COLLATE_CLAUSE<br/>SQL_CCS_LIMITED_COLLATION<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回所有這些選項，並受到支援。 傳回值 "0" 表示不支援**CREATE CHARACTER SET**語句。|
|SQL_CREATE_COLLATION|3.0|SQLUINTEGER 位元遮罩，用來列舉**CREATE 定序**語句中的子句（如 SQL-92 中所定義），資料來源所支援。<br/><br/>下列位元遮罩是用來判斷支援的子句：<br/>SQL_CCOL_CREATE_COLLATION<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回此選項支援。 傳回值 "0" 表示不支援 CREATE 定**序**語句。|
|SQL_CREATE_DOMAIN|3.0|SQLUINTEGER 位元遮罩，列舉**CREATE DOMAIN**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_CDO_CREATE_DOMAIN = (中繼層級) 支援 CREATE DOMAIN 語句。<br/>SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 支援命名 (中繼層級) 的定義域條件約束。<br/><br/>下列位指定建立資料行條件約束的能力：<br/>SQL_CDO_DEFAULT = (中繼層級支援指定網域條件約束) <br/>SQL_CDO_CONSTRAINT = (中繼層級支援指定網域預設值) <br/>SQL_CDO_COLLATION = (完整層級支援指定定義域定序) <br/><br/>如果支援指定網域條件約束，下列位會指定支援的條件約束屬性 (SQL_CDO_DEFAULT 設定) ：<br/>SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (完整層級) <br/>SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級) <br/>SQL_CDO_CONSTRAINT_DEFERRABLE (完整層級) <br/>SQL_CDO_CONSTRAINT_NON_DEFERRABLE (完整層級) <br/><br/>傳回值 "0" 表示不支援**CREATE DOMAIN**語句。|
|SQL_CREATE_SCHEMA|3.0|SQLUINTEGER 位元遮罩，用來列舉**CREATE SCHEMA**語句中的子句（如 SQL-92 中所定義），資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_CS_CREATE_SCHEMA<br/>SQL_CS_AUTHORIZATION<br/>SQL_CS_DEFAULT_CHARACTER_SET<br/><br/>符合 SQL 92 中繼層級的驅動程式一律會傳回所支援的 SQL_CS_CREATE_SCHEMA 和 SQL_CS_AUTHORIZATION 選項。 這些也必須在 SQL-92 專案層級支援，但不一定是 SQL 語句。 符合 SQL 92 完整層級的驅動程式一律會傳回所有這些選項，並受到支援。|
|SQL_CREATE_TABLE|3.0|SQLUINTEGER 位元遮罩，列舉在**CREATE TABLE**語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_CT_CREATE_TABLE = 支援 CREATE TABLE 語句。  (的進入層級) <br/>SQL_CT_TABLE_CONSTRAINT = (FIPS 過渡層級支援指定資料表條件約束) <br/>SQL_CT_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 子句支援將資料行和資料表條件約束命名 (中繼層級) <br/><br/>下列位指定建立臨時表的能力：<br/>SQL_CT_COMMIT_PRESERVE = 已刪除的資料列會在認可時保留。  (完整層級) <br/>SQL_CT_COMMIT_DELETE = 已刪除的資料列會在認可時刪除。  (完整層級) <br/>SQL_CT_GLOBAL_TEMPORARY = 可以建立全域臨時表。  (完整層級) <br/>SQL_CT_LOCAL_TEMPORARY = 可以建立本機臨時表。  (完整層級) <br/><br/>下列位指定建立資料行條件約束的能力：<br/>SQL_CT_COLUMN_CONSTRAINT = (FIPS 過渡層級支援指定資料行條件約束) <br/>SQL_CT_COLUMN_DEFAULT = (FIPS 過渡層級支援指定資料行預設值) <br/>SQL_CT_COLUMN_COLLATION = (完整層級支援指定資料行定序) <br/><br/>如果支援指定資料行或資料表條件約束，下列位會指定支援的條件約束屬性：<br/>SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (完整層級) <br/>SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級) <br/>SQL_CT_CONSTRAINT_DEFERRABLE (完整層級) <br/>SQL_CT_CONSTRAINT_NON_DEFERRABLE (完整層級) |
|SQL_CREATE_TRANSLATION|3.0|SQLUINTEGER 位元遮罩，列舉**CREATE 轉譯**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來判斷支援的子句：<br/>SQL_CTR_CREATE_TRANSLATION<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回這些選項，並受到支援。 傳回值 "0" 表示不支援**CREATE 轉譯**語句。|
|SQL_CREATE_VIEW||3.0|SQLUINTEGER 位元遮罩，列舉**CREATE VIEW**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_CV_CREATE_VIEW<br/>SQL_CV_CHECK_OPTION<br/>SQL_CV_CASCADED<br/>SQL_CV_LOCAL<br/><br/>傳回值 "0" 表示不支援**CREATE VIEW**語句。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_CV_CREATE_VIEW 並支援 SQL_CV_CHECK_OPTION 選項。<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回所有這些選項，並受到支援。|
|SQL_CURSOR_COMMIT_BEHAVIOR|1.0|SQLUSMALLINT 值，指出當您認可交易) 時，**認可**作業如何影響資料來源中的資料指標和備妥的語句 (資料來源的行為。<br/><br/>這個屬性的值會反映下一個設定的目前狀態： SQL_COPT_SS_PRESERVE_CURSORS。<br/>SQL_CB_DELETE = 關閉資料指標並刪除備妥的語句。 若要再次使用資料指標，應用程式必須 reprepare 並重新執行語句。<br/>SQL_CB_CLOSE = 關閉資料指標。 對於備妥的語句，應用程式可以在語句上呼叫**SQLExecute** ，而不需要再次呼叫**SQLPrepare** 。 SQL ODBC 驅動程式的預設值為 SQL_CB_CLOSE。 這表示當您認可交易時，SQL ODBC 驅動程式會關閉您的資料指標 (s) 。<br/>SQL_CB_PRESERVE = 保留與**認可**作業之前相同位置的資料指標。 應用程式可以繼續提取資料，也可以在不 repreparing 的情況下，關閉游標並重新執行語句。|
|SQL_CURSOR_ROLLBACK_BEHAVIOR|1.0|SQLUSMALLINT 值，指出**復原**作業如何影響資料來源中的資料指標和已備妥的語句：<br/>SQL_CB_DELETE = 關閉資料指標並刪除備妥的語句。 若要再次使用資料指標，應用程式必須 reprepare 並重新執行語句。<br/>SQL_CB_CLOSE = 關閉資料指標。 對於備妥的語句，應用程式可以在語句上呼叫**SQLExecute** ，而不需要再次呼叫**SQLPrepare** 。<br/>SQL_CB_PRESERVE = 保留與**復原**作業之前相同位置的資料指標。 應用程式可以繼續提取資料，也可以在不 repreparing 的情況下，關閉游標並重新執行語句。|
|SQL_CURSOR_SENSITIVITY|3.0|指出資料指標敏感度支援的 SQLUINTEGER 值：<br/>SQL_INSENSITIVE = 語句控制碼上的所有資料指標都會顯示結果集，而不會反映相同交易內任何其他資料指標所做的任何變更。<br/>SQL_UNSPECIFIED = 未指定語句控制碼上的資料指標是否會讓相同交易內的另一個資料指標看到對結果集所做的變更。 語句控制碼上的資料指標可能會使無、部分或所有這類變更變成可見。<br/>SQL_SENSITIVE = 資料指標對於相同交易內的其他資料指標所做的變更很敏感。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_UNSPECIFIED 選項（如受支援）。<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回支援的 SQL_INSENSITIVE 選項。|
|SQL_DATA_SOURCE_NAME|1.0|具有連接期間所使用之資料來源名稱的字元字串。 如果應用程式呼叫**SQLConnect**，這就是*szDSN*引數的值。 如果應用程式呼叫**SQLDriverConnect**或**SQLBrowseConnect**，這就是傳遞給驅動程式之連接字串中的 DSN 關鍵字值。 如果連接字串未包含**DSN**關鍵字 (例如，當它包含**DRIVER**關鍵字) 時，這就是空字串。|
|SQL_DATA_SOURCE_READ_ONLY|1.0|字元字串。 如果資料來源設定為唯讀模式，則為 "Y"，否則為 "N"。<br/><br/>此特性僅適用于資料來源本身;它不是可讓您存取資料來源之驅動程式的特性。 讀取/寫入的驅動程式可以搭配唯讀的資料來源使用。 如果驅動程式是唯讀的，其所有資料來源都必須是唯讀的，而且必須傳回 SQL_DATA_SOURCE_READ_ONLY。|
|SQL_DATABASE_NAME|1.0|如果資料來源定義名為 "database" 的命名物件，則為具有目前使用中資料庫名稱的字元字串。<br/><br/>在 ODBC 3.x 中，也可以藉由呼叫具有 SQL_ATTR_CURRENT_CATALOG 之*屬性*引數的**SQLGetConnectAttr** ，來傳回此*InfoType*傳回的值。|
|SQL_DATETIME_LITERALS|3.0|SQLUINTEGER 位元遮罩，列舉資料來源所支援的 SQL-92 日期時間常值。 請注意，這些是以 SQL-92 規格列出的日期時間常值，而且與 ODBC 所定義的日期時間常值 escape 子句不同。 如需 ODBC datetime 常值 escape 子句的詳細資訊，請參閱[日期、時間和時間戳記常](../develop-app/date-time-and-timestamp-literals.md)值。<br/><br/> 符合 FIPS 轉換等級的驅動程式一律會針對下列清單中的位，傳回位元遮罩中的 "1" 值。 值為 "0" 表示不支援 SQL-92 日期時間常值。<br/><br/>下列位元遮罩是用來決定支援的常值：<br/>SQL_DL_SQL92_DATE<br/>SQL_DL_SQL92_TIME<br/>SQL_DL_SQL92_TIMESTAMP<br/>SQL_DL_SQL92_INTERVAL_YEAR<br/>SQL_DL_SQL92_INTERVAL_MONTH<br/>SQL_DL_SQL92_INTERVAL_DAY<br/>SQL_DL_SQL92_INTERVAL_HOUR<br/>SQL_DL_SQL92_INTERVAL_MINUTE<br/>SQL_DL_SQL92_INTERVAL_SECOND<br/>SQL_DL_SQL92_INTERVAL_YEAR_TO_MONTH<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_HOUR<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTE<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_SECOND<br/>SQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTE<br/>SQL_DL_SQL92_INTERVAL_HOUR_TO_SECOND<br/>SQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND|
|SQL_DBMS_NAME|1.0|具有驅動程式所存取之 DBMS 產品名稱的字元字串。|
|SQL_DBMS_VER|1.0|表示驅動程式所存取之 DBMS 產品版本的字元字串。 版本的格式為 # #. # #. # # # #，其中前兩個數字是主要版本，接下來兩個數字是次要版本，而最後四個數字是發行版本。 驅動程式必須以這種形式轉譯 DBMS 產品版本，但也可以附加 DBMS 產品特定版本。 例如，"04.01.0000 Rdb 4.1"。|
|SQL_DDL_INDEX|3.0|表示支援建立和卸載索引的 SQLUINTEGER 值：<br/>SQL_DI_CREATE_INDEX<br/>SQL_DI_DROP_INDEX|
|SQL_DEFAULT_TXN_ISOLATION|1.0|SQLUINTEGER 值，指出驅動程式或資料來源所支援的預設交易隔離等級，如果資料來源不支援交易，則為零。 下列詞彙可用來定義交易隔離等級：<br/>中途**讀取**交易1會變更資料列。 交易2會在交易1認可變更之前讀取已變更的資料列。 如果交易1回復變更，交易2就會讀取被視為從未存在的資料列。<br/>**不可重複的讀取**交易1讀取資料列。 Transaction 2 會更新或刪除該資料列，並認可這種變更。 如果交易1嘗試重新讀取資料列，則會收到不同的資料列值，或發現資料列已被刪除。<br/>**Phantom**虛設交易1會讀取符合某些搜尋條件的一組資料列。 交易2會透過符合搜尋條件的插入或更新) ，產生一或多個資料列 (。 如果交易1重新執行讀取資料列的語句，它會接收一組不同的資料列。<br/><br/>如果資料來源支援交易，驅動程式會傳回下列其中一個位元遮罩：<br/>SQL_TXN_READ_UNCOMMITTED = 可能發生中途讀取、不可重複的讀取和幻像。<br/>SQL_TXN_READ_COMMITTED = 不可能進行中途讀取。 不可重複的讀取和幻像是可行的。<br/>SQL_TXN_REPEATABLE_READ = 不可能有中途讀取和不可重複的讀取。 可以是幻像。<br/>SQL_TXN_SERIALIZABLE = 交易可序列化。 可序列化的交易不允許中途讀取、不可重複的讀取或幻像。|
|SQL_DESCRIBE_PARAMETER|3.0|字元字串：如果可以描述參數，則為 "Y";"N"，否則為。<br/><br/>SQL-92 完整層級一致的驅動程式通常會傳回 "Y"，因為它會支援**描述輸入**語句。 不過，這並不會直接指定基礎 SQL 支援，但可能不支援描述參數，即使是在符合 SQL-92 的完整層級驅動程式中也一樣。|
|SQL_DM_VER|3.0|具有驅動程式管理員版本的字元字串。 版本的格式為 # #. # #. # # # #. # # # #，其中：<br/>第一組的兩個數字是主要的 ODBC 版本，如同常數 SQL_SPEC_MAJOR 所提供的。<br/>第二組的兩個數字是次要的 ODBC 版本，如同常數 SQL_SPEC_MINOR 所提供的。<br/>第三組的四個數字是驅動程式管理員的主要組建編號。<br/>最後一組四個數字是驅動程式管理員的次要組建編號。<br/>Windows 7 驅動程式管理員版本為03.80。 Windows 8 驅動程式管理員版本為03.81。|
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|3.8|SQLUINTEGER 值，指出驅動程式是否支援可感知驅動程式的共用。  (需詳細資訊，請參閱可[感知驅動程式的連接](../develop-app/driver-aware-connection-pooling.md)共用。<br/><br/>SQL_DRIVER_AWARE_POOLING_CAPABLE 指出驅動程式可以支援可感知驅動程式的共用機制。<br/>SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 指出驅動程式無法支援可感知驅動程式的共用機制。<br/><br/>驅動程式不需要執行 SQL_DRIVER_AWARE_POOLING_SUPPORTED，驅動程式管理員將不會接受驅動程式的傳回值。|
|SQL_DRIVER_HDBCSQL_DRIVER_HENV|1.0|SQLULEN 值，驅動程式的環境控制碼或連接控制碼，由引數*InfoType*決定。<br/><br/>這些資訊類型是由驅動程式管理員單獨執行。|
|SQL_DRIVER_HDESC|3.0|驅動程式管理員的描述項控制碼所決定的 SQLULEN 值，其必須 \* 從應用程式傳入*InfoValuePtr*中的輸入。 在此情況下， *InfoValuePtr*同時為輸入和輸出引數。 傳入 InfoValuePtr 的輸入描述元控制碼 \* *InfoValuePtr*必須已明確或隱含配置在*ConnectionHandle*上。<br/><br/>應用程式應該在使用此資訊類型呼叫**SQLGetInfo**之前，建立驅動程式管理員的描述項控制碼複本，以確保在輸出時不會覆寫該控制碼。<br/><br/>此資訊類型是由驅動程式管理員單獨執行。|
|SQL_DRIVER_HLIB|2.0|SQLULEN 值、載入程式庫中的*hinst*在載入 Microsoft Windows 作業系統上的驅動程式 DLL 時傳回給驅動程式管理員，或在另一個作業系統上的對等。 控制碼僅適用于呼叫**SQLGetInfo**時所指定的連接控制碼。<br/><br/>此資訊類型是由驅動程式管理員單獨執行。|
|SQL_DRIVER_HSTMT|1.0|驅動程式管理員語句控制碼所決定的 SQLULEN 值，驅動程式的語句控制碼，必須 \* 從應用程式傳入*InfoValuePtr*中的輸入。 在此情況下， *InfoValuePtr*同時為輸入和輸出引數。 傳入 InfoValuePtr 的輸入語句控制碼必須已配置 \* *InfoValuePtr*在引數*ConnectionHandle*上。<br/><br/>應用程式應該在使用此資訊類型呼叫**SQLGetInfo**之前，建立驅動程式管理員的語句控制碼複本，以確保在輸出時不會覆寫該控制碼。<br/><br/>此資訊類型是由驅動程式管理員單獨執行。|
|SQL_DRIVER_NAME|1.0|含有用來存取資料來源之驅動程式檔案名的字元字串。|
|SQL_DRIVER_ODBC_VER|2.0|具有驅動程式支援之 ODBC 版本的字元字串。 版本的格式為 # #. # #，其中前兩個數字是主要版本，而後面兩個數字是次要版本。 SQL_SPEC_MAJOR 和 SQL_SPEC_MINOR 定義主要和次要版本號碼。 針對本手冊中所述的 ODBC 版本，這些是3和0，而驅動程式應該會傳回 "03.00"。<br/><br/>ODBC 驅動程式管理員不會修改 SQLGetInfo (的傳回值 SQL_DRIVER_ODBC_VER) 來維持現有應用程式的回溯相容性。 驅動程式會指定要傳回的值。 不過，當應用程式呼叫**SQLSetEnvAttr**以將 SQL_ATTR_ODBC_VERSION 設定為3.8 時，支援 C 資料類型擴充性的驅動程式必須傳回 3.8 (或更高的) 。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../develop-app/c-data-types-in-odbc.md)。|
|SQL_DRIVER_VER|1.0|含有驅動程式版本的字元字串，以及選擇性的驅動程式描述。 版本至少是 # #. # #. # # # # 形式，其中前兩個數字是主要版本，接下來兩個數字是次要版本，而最後四個數字是發行版本。|
|SQL_DROP_ASSERTION|3.0|SQLUINTEGER 位元遮罩，列舉**DROP**判斷提示語句中的子句（如 SQL-92 中所定義，由資料來源所支援）。<br/><br/>下列位元遮罩是用來判斷支援的子句：<br/>SQL_DA_DROP_ASSERTION<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回此選項支援。|
|SQL_DROP_CHARACTER_SET|3.0|SQLUINTEGER 位元遮罩，列舉**DROP CHARACTER SET**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來判斷支援的子句：<br/>SQL_DCS_DROP_CHARACTER_SET<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回此選項支援。|
|SQL_DROP_COLLATION|3.0|SQLUINTEGER 位元遮罩，列舉**DROP 定序**語句中的子句（如 SQL-92 中所定義，由資料來源所支援）。<br/><br/>下列位元遮罩是用來判斷支援的子句：<br/>SQL_DC_DROP_COLLATION<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回此選項支援。|
|SQL_DROP_DOMAIN|3.0|SQLUINTEGER 位元遮罩，列舉**DROP DOMAIN**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_DD_DROP_DOMAIN<br/>SQL_DD_CASCADE<br/>SQL_DD_RESTRICT<br/><br/>符合 SQL 92 中繼層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_DROP_SCHEMA|3.0|SQLUINTEGER 位元遮罩，列舉**DROP SCHEMA**語句中的子句，如 SQL-92 中所定義，資料來源所支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_DS_DROP_SCHEMA<br/>SQL_DS_CASCADE<br/>SQL_DS_RESTRICT<br/><br/>符合 SQL 92 中繼層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_DROP_TABLE|3.0|SQLUINTEGER 位元遮罩，列舉**DROP TABLE**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_DT_DROP_TABLE<br/>SQL_DT_CASCADE<br/>SQL_DT_RESTRICT<br/><br/>符合 FIPS 轉換層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_DROP_TRANSLATION|3.0|SQLUINTEGER 位元遮罩，列舉**DROP 轉譯**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來判斷支援的子句：<br/>SQL_DTR_DROP_TRANSLATION<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回此選項支援。|
|SQL_DROP_VIEW|3.0|SQLUINTEGER 位元遮罩，列舉**DROP VIEW**語句中的子句（如 SQL-92 中所定義），由資料來源支援。<br/><br/>下列位元遮罩是用來決定支援的子句：<br/>SQL_DV_DROP_VIEW<br/>SQL_DV_CASCADE<br/>SQL_DV_RESTRICT<br/><br/>符合 FIPS 轉換層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援之動態資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA1_NEXT = 當資料指標是動態資料指標時， **SQLFetchScroll**呼叫中支援 SQL_FETCH_NEXT 的*FetchOrientation*引數。<br/>當資料指標是動態資料指標時， **SQLFetchScroll**呼叫中支援 SQL_FETCH_FIRST、SQL_FETCH_LAST 和 SQL_FETCH_ABSOLUTE 的*FetchOrientation*引數。 SQL_CA1_ABSOLUTE  (將提取的資料列集與目前的資料指標位置無關。 ) <br/>SQL_CA1_RELATIVE = 當資料指標是動態資料指標時， **SQLFetchScroll**呼叫中支援的 SQL_FETCH_PRIOR 和 SQL_FETCH_RELATIVE 的*FetchOrientation*引數。  (將提取的資料列集，取決於目前的資料指標位置。 請注意，這會與 SQL_FETCH_NEXT 分開，因為在順向資料指標中，只支援 SQL_FETCH_NEXT。 ) <br/>SQL_CA1_BOOKMARK = 當資料指標是動態資料指標時， **SQLFetchScroll**呼叫中支援 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數。<br/>SQL_CA1_LOCK_EXCLUSIVE = 當資料指標是動態資料指標時， **SQLSetPos**呼叫中支援 SQL_LOCK_EXCLUSIVE 的*LockType*引數。<br/>SQL_CA1_LOCK_NO_CHANGE = 當資料指標是動態資料指標時， **SQLSetPos**呼叫中支援 SQL_LOCK_NO_CHANGE 的*LockType*引數。<br/>SQL_CA1_LOCK_UNLOCK = 當資料指標是動態資料指標時， **SQLSetPos**呼叫中支援 SQL_LOCK_UNLOCK 的*LockType*引數。<br/>SQL_CA1_POS_POSITION = 當資料指標是動態資料指標時，呼叫**SQLSetPos**時支援*SQL_POSITION 的作業引數*。<br/>SQL_CA1_POS_UPDATE = 當資料指標是動態資料指標時，呼叫**SQLSetPos**時支援*SQL_UPDATE 的作業引數*。<br/>SQL_CA1_POS_DELETE = 當資料指標是動態資料指標時，呼叫**SQLSetPos**時支援*SQL_DELETE 的作業引數*。<br/>SQL_CA1_POS_REFRESH = 當資料指標是動態資料指標時，呼叫**SQLSetPos**時支援*SQL_REFRESH 的作業引數*。<br/>SQL_CA1_POSITIONED_UPDATE = 當資料指標是動態資料指標時，支援目前 SQL 語句的更新。  (符合 SQL-92 專案等級的驅動程式一律會傳回此選項支援。 ) <br/>SQL_CA1_POSITIONED_DELETE = 刪除，當資料指標是動態資料指標時，就會支援目前的 SQL 語句。  (符合 SQL-92 專案等級的驅動程式一律會傳回此選項支援。 ) <br/>SQL_CA1_SELECT_FOR_UPDATE = 當資料指標是動態資料指標時，支援 UPDATE SQL 語句的 SELECT。  (符合 SQL-92 專案等級的驅動程式一律會傳回此選項支援。 ) <br/>SQL_CA1_BULK_ADD = 當資料指標是動態資料指標時，呼叫**SQLBulkOperations**時支援*SQL_ADD 的作業引數*。<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK = 當資料指標是動態資料指標時，呼叫**SQLBulkOperations**時支援*SQL_UPDATE_BY_BOOKMARK 的作業引數*。<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK = 當資料指標是動態資料指標時，呼叫**SQLBulkOperations**時支援*SQL_DELETE_BY_BOOKMARK 的作業引數*。<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK = 當資料指標是動態資料指標時，呼叫**SQLBulkOperations**時支援*SQL_FETCH_BY_BOOKMARK 的作業引數*。<br/><br/>符合 SQL 92 中繼層級的驅動程式通常會傳回所支援的 SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項，因為它支援透過內嵌 SQL FETCH 語句的可滾動資料指標。 由於這不會直接判斷基礎 SQL 支援，因此，即使是 SQL-92 中繼層級一致的驅動程式，也可能不支援可滾動的資料指標。|
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援之動態資料指標的屬性。 此位元遮罩包含屬性的第二個子集;如需第一個子集，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA2_READ_ONLY_CONCURRENCY = 不允許任何更新的唯讀動態資料指標。  (可以 SQL_CONCUR_READ_ONLY 動態資料指標) 的 SQL_ATTR_CONCURRENCY 語句屬性。<br/>SQL_CA2_LOCK_CONCURRENCY = 使用最低鎖定層級來確保可更新資料列的動態資料指標。  (可以 SQL_CONCUR_LOCK 動態資料指標的 SQL_ATTR_CONCURRENCY 語句屬性。 ) 這些鎖定必須與 SQL_ATTR_TXN_ISOLATION 連接屬性所設定的交易隔離等級一致。<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY = 支援使用開放式並行存取控制來比較資料列版本的動態資料指標。  (可以 SQL_CONCUR_ROWVER 動態資料指標的 SQL_ATTR_CONCURRENCY 語句屬性。 ) <br/>SQL_CA2_OPT_VALUES_CONCURRENCY = 支援使用開放式並行存取控制比較值的動態資料指標。  (可以 SQL_CONCUR_VALUES 動態資料指標的 SQL_ATTR_CONCURRENCY 語句屬性。 ) <br/>SQL_CA2_SENSITIVITY_ADDITIONS = 動態資料指標可以看到已加入的資料列;游標可以滾動到那些資料列。 將這些資料列加入至資料指標的 (會與驅動程式相關。 ) <br/>SQL_CA2_SENSITIVITY_DELETIONS = 已刪除的資料列無法再供動態資料指標使用，而且不會在結果集中留下「洞」;動態資料指標從已刪除的資料列中滾動之後，就無法返回該資料列。<br/>SQL_CA2_SENSITIVITY_UPDATES = 動態資料指標可以看到資料列的更新;如果動態資料指標從中滾動並返回更新的資料列，則資料指標所傳回的資料就是更新的資料，而不是原始資料。<br/>SQL_CA2_MAX_ROWS_SELECT = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響**SELECT**語句。<br/>SQL_CA2_MAX_ROWS_INSERT = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響**INSERT**語句。<br/>SQL_CA2_MAX_ROWS_DELETE = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響**DELETE**語句。<br/>SQL_CA2_MAX_ROWS_UPDATE = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響**UPDATE**語句。<br/>SQL_CA2_MAX_ROWS_CATALOG = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響**目錄**結果集。<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響**SELECT**、 **INSERT**、 **DELETE**和**UPDATE**語句，以及**目錄**結果集。<br/>SQL_CA2_CRC_EXACT = 當資料指標是動態資料指標時，[SQL_DIAG_CURSOR_ROW_COUNT 診斷] 欄位中可以使用精確的資料列計數。<br/>SQL_CA2_CRC_APPROXIMATE = 當資料指標是動態資料指標時，[SQL_DIAG_CURSOR_ROW_COUNT 診斷] 欄位中提供大約的資料列計數。<br/>SQL_CA2_SIMULATE_NON_UNIQUE = 驅動程式不保證當資料指標是動態資料指標時，模擬的定點更新或刪除語句將只會影響一個資料列;應用程式必須負責確保這一點。  (如果語句會影響一個以上的資料列， **SQLExecute**或**SQLEXECDIRECT**會傳回 SQLSTATE 01001 [資料指標作業衝突]。 ) 若要設定此行為，應用程式會呼叫**SQLSetStmtAttr** ，並將 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 [SQL_SC_NON_UNIQUE]。<br/>SQL_CA2_SIMULATE_TRY_UNIQUE = 驅動程式會嘗試保證當資料指標是動態資料指標時，模擬的定點更新或刪除語句將只會影響一個資料列。 驅動程式一律會執行這類語句，即使它們可能會影響一個以上的資料列，例如沒有唯一索引鍵時。  (如果語句會影響一個以上的資料列， **SQLExecute**或**SQLEXECDIRECT**會傳回 SQLSTATE 01001 [資料指標作業衝突]。 ) 若要設定此行為，應用程式會呼叫**SQLSetStmtAttr** ，並將 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 [SQL_SC_TRY_UNIQUE]。<br/>SQL_CA2_SIMULATE_UNIQUE = 驅動程式保證當資料指標是動態資料指標時，模擬的定點更新或刪除語句將只會影響一個資料列。 如果驅動程式無法保證指定語句的這個， **SQLExecDirect**或**SQLPREPARE**會傳回 SQLSTATE 01001， (資料指標作業衝突) 。 若要設定此行為，應用程式會呼叫**SQLSetStmtAttr** ，並將 SQL_ATTR_SIMULATE_CURSOR 屬性設為 SQL_SC_UNIQUE。|
|SQL_EXPRESSIONS_IN_ORDERBY|1.0|字元字串：如果資料來源支援**ORDER BY**清單中的運算式，則為 "Y";如果不是，則為 "N"。|
|SQL_FILE_USAGE|2.0|SQLUSMALLINT 值，指出單一層驅動程式如何直接處理資料來源中的檔案：<br/>SQL_FILE_NOT_SUPPORTED = 驅動程式不是一層式驅動程式。 例如，ORACLE 驅動程式是兩層式的驅動程式。<br/>SQL_FILE_TABLE = 單一層驅動程式會將資料來源中的檔案視為資料表。 例如，Xbase 驅動程式會將每個 Xbase 檔案視為一個資料表。<br/>SQL_FILE_CATALOG = 單一層驅動程式會將資料來源中的檔案視為目錄。 例如，Microsoft Access 驅動程式會將每個 Microsoft Access 檔案視為完整的資料庫。<br/><br/>應用程式可能會使用此來判斷使用者如何選取資料。 例如，Xbase 使用者通常會將資料視為儲存在檔案中，而 ORACLE 和 Microsoft Access 使用者通常會將資料視為儲存在資料表中。<br/><br/>當使用者選取 Xbase 資料來源時，應用程式可能會顯示 [Windows 檔案**開啟**通用] 對話方塊;當使用者選取 Microsoft Access 或 ORACLE 資料來源時，應用程式可能會顯示自訂的 [**選取資料表**] 對話方塊。|
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式所支援之順向資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA1_NEXT<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在 [描述]) 中，將「順向資料指標」替換為「動態資料指標」。|
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式所支援之順向資料指標的屬性。 此位元遮罩包含屬性的第二個子集;如需第一個子集，請參閱 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (，並在 [描述]) 中，將「順向資料指標」替換為「動態資料指標」。|
|SQL_GETDATA_EXTENSIONS|2.0|SQLUINTEGER 的位元遮罩，列舉要**SQLGetData**的延伸。<br/><br/>下列位元遮罩會與旗標一起使用，以判斷驅動程式支援哪些通用延伸模組來進行**SQLGetData**：<br/>SQL_GD_ANY_COLUMN = **SQLGetData**可以針對任何未系結的資料行呼叫，包括最後一個系結資料行之前的資料行。 請注意，除非也傳回 SQL_GD_ANY_ORDER，否則必須以遞增的資料行編號順序來呼叫資料行。<br/>您可以依任何順序，針對未系結的資料行呼叫 SQL_GD_ANY_ORDER = **SQLGetData** 。 請注意，除非也傳回 SQL_GD_ANY_COLUMN，否則只能針對最後一個系結資料行之後的資料行呼叫**SQLGetData** 。<br/>SQL_GD_BLOCK = **SQLGetData**可以針對區塊中的任何資料列中的未系結資料行呼叫， (中的資料列集大小在使用**SQLSetPos**定位到該資料列之後大於 1) 。<br/>除了未系結的資料行之外，也可以針對系結的資料行呼叫 SQL_GD_BOUND = **SQLGetData** 。 驅動程式無法傳回此值，除非它也會傳回 SQL_GD_ANY_COLUMN。<br/>SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以呼叫以傳回輸出參數值。 如需詳細資訊，請參閱[使用 SQLGetData 抓取輸出參數](../develop-app/retrieving-output-parameters-using-sqlgetdata.md)。<br/><br/>只有在最後一個系結資料行之後所呼叫的未系結資料行中，才需要**SQLGetData** ，才會傳回資料。<br/><br/>如果驅動程式支援書簽 (固定長度或可變長度的) ，它就必須支援在資料行0上呼叫**SQLGetData** 。 無論使用 SQL_GETDATA_EXTENSIONS *InfoType*呼叫**SQLGetInfo**時，驅動程式傳回的內容為何，都需要這項支援。|
|SQL_GROUP_BY|2.0|SQLUSMALLINT 值，指定**GROUP BY**子句中的資料行與選取清單中的非匯總資料行之間的關聯性：<br/>SQL_GB_COLLATE = 可以在每個群組資料行的結尾指定**COLLATE**子句。  (ODBC 3.0) <br/>SQL_GB_NOT_SUPPORTED = **GROUP BY**子句不受支援。  (ODBC 2.0) <br/>SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP by**子句必須包含選取清單中的所有非匯總資料行。 它不能包含任何其他資料行。 例如，**選取 [部門]、[員工] 群組中的 [最大 (薪資) （依部門）**。  (ODBC 2.0) <br/>SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP by**子句必須包含選取清單中的所有非匯總資料行。 它可以包含不在選取清單中的資料行。 例如，**選取 [部門]、[員工] 群組中的 [最大 (薪資) （依部門、年齡）**。  (ODBC 2.0) <br/>SQL_GB_NO_RELATION = **GROUP by**子句中的資料行與選取清單不相關。 在選取清單中，nongrouped、非匯總資料行的意義與資料來源相關。 例如，**選取 [部門]、[員工] 群組中的 [薪資]、[年齡**]。  (ODBC 2.0) <br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_GB_GROUP_BY_EQUALS_SELECT 選項（如受支援）。 符合 SQL 92 完整層級的驅動程式一律會傳回支援的 SQL_GB_COLLATE 選項。 如果不支援任何選項，則資料來源不支援**GROUP by**子句。|
|SQL_IDENTIFIER_CASE|1.0|SQLUSMALLINT 值，如下所示：<br/>SQL_IC_UPPER = SQL 中的識別碼不區分大小寫，而且會以大寫儲存在系統目錄中。<br/>SQL_IC_LOWER = SQL 中的識別碼不區分大小寫，而且在系統目錄中是以小寫的方式儲存。<br/>SQL_IC_SENSITIVE = SQL 中的識別碼會區分大小寫，並以混合大小寫儲存在系統目錄中。<br/>SQL_IC_MIXED = SQL 中的識別碼不區分大小寫，而且會以混合大小寫儲存在系統目錄中。<br/><br/>由於 SQL-92 中的識別碼永遠不會區分大小寫，因此嚴格符合 SQL-92 的驅動程式 (任何層級) 一律不會傳回所支援的 SQL_IC_SENSITIVE 選項。|
|SQL_IDENTIFIER_QUOTE_CHAR|1.0|字元字串，用來當做 SQL 語句中加上引號之 (分隔) 識別碼的開始和結束分隔符號。 當做引數傳遞至 ODBC 函數的 (識別碼不需要加上引號。 ) 如果資料來源不支援引號識別碼，則會傳回空白。<br/><br/>當連接屬性 SQL_ATTR_METADATA_ID 設定為 SQL_TRUE 時，這個字元字串也可以用來括住目錄函式引數。<br/><br/>由於 SQL-92 中的識別碼引號字元是雙引號 ( 「) ，因此嚴格符合 SQL-92 的驅動程式一律會傳回雙引號字元。|
|SQL_INDEX_KEYWORDS|3.0|SQLUINTEGER 位元遮罩，可列舉驅動程式所支援之 CREATE INDEX 語句中的關鍵字：<br/>SQL_IK_NONE = 不支援任何關鍵字。<br/>支援 SQL_IK_ASC = ASC 關鍵字。<br/>支援 SQL_IK_DESC = DESC 關鍵字。<br/>SQL_IK_ALL = 支援所有關鍵詞。<br/><br/>若要查看是否支援 CREATE INDEX 語句，應用程式會使用 SQL_DLL_INDEX 資訊類型來呼叫**SQLGetInfo** 。|
|SQL_INFO_SCHEMA_VIEWS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式支援的 INFORMATION_SCHEMA 中的 views。 中的 views 和的內容，INFORMATION_SCHEMA 如 SQL-92 中所定義。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來決定支援的視圖：<br/>SQL_ISV_ASSERTIONS = 識別指定使用者所擁有的目錄判斷提示。  (完整層級) <br/>SQL_ISV_CHARACTER_SETS = 識別可由指定使用者存取的目錄字元集。  (中繼層級) <br/>SQL_ISV_CHECK_CONSTRAINTS = 識別指定使用者所擁有的 CHECK 條件約束。  (中繼層級) <br/>SQL_ISV_COLLATIONS = 識別可由指定使用者存取之類別目錄的字元定序。  (完整層級) <br/>SQL_ISV_COLUMN_DOMAIN_USAGE = 識別目錄的資料行，其相依于目錄中定義且由指定使用者所擁有的網域。  (中繼層級) <br/>SQL_ISV_COLUMN_PRIVILEGES = 識別可由指定使用者存取或授與之持續性資料表的資料行許可權。  (FIPS 過渡層級) <br/>SQL_ISV_COLUMNS = 識別可由指定使用者存取之持續性資料表的資料行。  (FIPS 過渡層級) <br/>SQL_ISV_CONSTRAINT_COLUMN_USAGE = 類似 CONSTRAINT_TABLE_USAGE view，會針對指定使用者所擁有的各種條件約束來識別資料行。  (中繼層級) <br/>SQL_ISV_CONSTRAINT_TABLE_USAGE = 識別條件約束所使用的資料表 (參考、唯一和判斷提示) ，而且是由指定使用者所擁有。  (中繼層級) <br/>SQL_ISV_DOMAIN_CONSTRAINTS = 識別目錄) 中可由指定使用者存取之網域的網域條件約束 (。  (中繼層級) <br/>SQL_ISV_DOMAINS = 識別在目錄中所定義的網域，而使用者可以存取該目錄。  (中繼層級) <br/>SQL_ISV_KEY_COLUMN_USAGE = 識別目錄中定義的資料行，這些資料行會受到指定使用者的索引鍵限制。  (中繼層級) <br/>SQL_ISV_REFERENTIAL_CONSTRAINTS = 識別指定使用者所擁有的參考條件約束。  (中繼層級) <br/>SQL_ISV_SCHEMATA = 識別指定使用者所擁有的架構。  (中繼層級) <br/>SQL_ISV_SQL_LANGUAGES = 識別 sql 執行所支援的 SQL 一致性層級、選項和方言。  (中繼層級) <br/>SQL_ISV_TABLE_CONSTRAINTS = 識別指定使用者所擁有的資料表條件約束。  (中繼層級) <br/>SQL_ISV_TABLE_PRIVILEGES = 識別可由指定使用者存取或授與之持續性資料表的許可權。  (FIPS 過渡層級) <br/>SQL_ISV_TABLES = 識別在目錄中所定義且可由指定使用者存取的持續性資料表。  (FIPS 過渡層級) <br/>SQL_ISV_TRANSLATIONS = 識別可由指定使用者存取之目錄的字元翻譯。  (完整層級) <br/>SQL_ISV_USAGE_PRIVILEGES = 識別指定的使用者可以使用或擁有之目錄物件的許可權。  (FIPS 過渡層級) <br/>SQL_ISV_VIEW_COLUMN_USAGE = 識別由指定使用者所擁有之目錄的瀏覽器所相依的資料行。  (中繼層級) <br/>SQL_ISV_VIEW_TABLE_USAGE = 識別由指定使用者所擁有之目錄的瀏覽器所相依的資料表。  (中繼層級) <br/>SQL_ISV_VIEWS = 識別此目錄中所定義且可由指定使用者存取的已查看資料表。  (FIPS 過渡層級) |
|SQL_INSERT_STATEMENT|3.0|指出**INSERT**語句支援的 SQLUINTEGER 位元遮罩：<br/>SQL_IS_INSERT_LITERALS<br/>SQL_IS_INSERT_SEARCHED<br/>SQL_IS_SELECT_INTO<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_INTEGRITY|1.0|字元字串： "Y" （如果資料來源支援完整性增強功能）。如果不是，則為 "N"。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_ODBC_SQL_OPT_IEF 重新命名為 odbc 3.0。|
|SQL_KEYSET_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援的索引鍵集資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_KEYSET_CURSOR_ATTRIBUTES2。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA1_NEXT<br/>SQL_CA1_ABSOLUTE<br/>SQL_CA1_RELATIVE<br/>SQL_CA1_BOOKMARK<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在 [描述]) 中替代「動態資料指標」的「索引鍵集驅動資料指標」。<br/><br/>SQL-92 中繼層級一致的驅動程式通常會傳回所支援的 SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項，因為驅動程式支援透過內嵌 SQL FETCH 語句的可滾動資料指標。 由於這不會直接判斷基礎 SQL 支援，因此，即使是 SQL-92 中繼層級一致的驅動程式，也可能不支援可滾動的資料指標。|
|SQL_KEYSET_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援的索引鍵集資料指標的屬性。 此位元遮罩包含屬性的第二個子集;如需第一個子集，請參閱 SQL_KEYSET_CURSOR_ATTRIBUTES1。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在 [描述]) 中替代「動態資料指標」的「索引鍵集驅動資料指標」。|
|SQL_KEYWORDS|2.0|包含所有資料來源特定關鍵字之逗號分隔清單的字元字串。 此清單不包含資料來源和 ODBC 所使用之 ODBC 或關鍵字特有的關鍵字。 此清單代表所有保留關鍵字;互通的應用程式不應該在物件名稱中使用這些字。<br/><br/>如需 ODBC 關鍵字的清單，請參閱[附錄 C： SQL 文法](../appendixes/appendix-c-sql-grammar.md)中的[保留關鍵字](../appendixes/reserved-keywords.md)。 **#Define**值 SQL_ODBC_KEYWORDS 包含以逗號分隔的 ODBC 關鍵字清單。|
|SQL_LIKE_ESCAPE_CLAUSE|2.0|字元字串：如果資料來源支援在**LIKE**述詞中使用% 字元 (% ) 和底線字元 (_) 的 escape 字元，而且驅動程式支援 ODBC 語法來定義**like**述詞 escape 字元，則為 "Y"。否則為 "N"。|
|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|3.0|SQLUINTEGER 值，指定在非同步模式中，驅動程式可以在指定連接上支援的作用中並行語句數目上限。 如果沒有特定限制，或限制不明，則此值為零。|
|SQL_MAX_BINARY_LITERAL_LEN|2.0|SQLUINTEGER 值，指定十六進位字元 (的最大長度，不包括在 SQL 語句中，二進位常值的**SQLGetTypeInfo**) 所傳回的常值前置詞和尾碼。 例如，二進位常值0xFFAA 的長度為4。 如果沒有最大長度，或長度不明，則此值會設定為零。|
|SQL_MAX_CATALOG_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中目錄名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 的完整層級驅動程式至少會傳回128。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN 重新命名為 odbc 3.0。|
|SQL_MAX_CHAR_LITERAL_LEN|2.0|SQLUINTEGER 值，指定字元數的最大長度 (，但不包括在 SQL 語句中字元常值的**SQLGetTypeInfo**) 所傳回的常值前置詞和尾碼。 如果沒有最大長度，或長度不明，則此值會設定為零。|
|SQL_MAX_COLUMN_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中資料行名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式將會傳回至少18個。 符合 FIPS 中繼層級的驅動程式至少會傳回128。|
|SQL_MAX_COLUMNS_IN_GROUP_BY|2.0|SQLUSMALLINT 值，指定**GROUP BY**子句中允許的最大資料行數目。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回6。 符合 FIPS 中繼層級的驅動程式會傳回至少15個。|
|SQL_MAX_COLUMNS_IN_INDEX|2.0|SQLUSMALLINT 值，指定索引中允許的最大資料行數目。 如果沒有指定的限制，或限制不明，此值會設定為零。|
|SQL_MAX_COLUMNS_IN_ORDER_BY|2.0|SQLUSMALLINT 值，指定**ORDER BY**子句中所允許的最大資料行數目。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回6。 符合 FIPS 中繼層級的驅動程式會傳回至少15個。|
|SQL_MAX_COLUMNS_IN_SELECT|2.0|SQLUSMALLINT 值，指定選取清單中所允許的最大資料行數目。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回100。 符合 FIPS 中繼層級的驅動程式至少會傳回250。|
|SQL_MAX_COLUMNS_IN_TABLE|2.0|SQLUSMALLINT 值，指定資料表中允許的最大資料行數目。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回100。 符合 FIPS 中繼層級的驅動程式至少會傳回250。|
|SQL_MAX_CONCURRENT_ACTIVITIES|1.0|SQLUSMALLINT 值，指定驅動程式可支援連接的最大使用中語句數目。 如果語句具有暫止的結果，且「結果」一詞表示**SELECT**作業中的資料列或受**插入**、**更新**或**刪除**作業影響的資料列 (例如，資料列計數) 或處於 NEED_DATA 狀態，則會將它定義為作用中。 這個值可以反映驅動程式或資料來源所加諸的限制。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_ACTIVE_STATEMENTS 重新命名為 odbc 3.0。|
|SQL_MAX_CURSOR_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中游標名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式將會傳回至少18個。 符合 FIPS 中繼層級的驅動程式至少會傳回128。|
|SQL_MAX_DRIVER_CONNECTIONS|1.0|SQLUSMALLINT 值，指定驅動程式可以為環境支援的作用中連接數目上限。 這個值可以反映驅動程式或資料來源所加諸的限制。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_ACTIVE_CONNECTIONS 重新命名為 odbc 3.0。|
|SQL_MAX_IDENTIFIER_LEN|3.0|SQLUSMALLINT，指出資料來源針對使用者定義名稱所支援的大小上限（以字元為單位）。<br/><br/>符合 FIPS 專案等級的驅動程式將會傳回至少18個。 符合 FIPS 中繼層級的驅動程式至少會傳回128。|
|SQL_MAX_INDEX_SIZE|2.0|SQLUINTEGER 值，指定索引之合併欄位中所允許的最大位元組數目。 如果沒有指定的限制，或限制不明，此值會設定為零。|
|SQL_MAX_PROCEDURE_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中程式名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。|
|SQL_MAX_ROW_SIZE|2.0|SQLUINTEGER 值，指定資料表中單一資料列的最大長度。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回2000。 符合 FIPS 中繼層級的驅動程式至少會傳回8000。|
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|3.0|字元字串：如果 SQL_MAX_ROW_SIZE 資訊類型傳回的最大資料列大小包含資料列中所有 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 資料行的長度，則為 "Y";否則為 "N"。|
|SQL_MAX_SCHEMA_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中架構名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式將會傳回至少18個。 符合 FIPS 中繼層級的驅動程式至少會傳回128。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_MAX_OWNER_NAME_LEN 重新命名為 odbc 3.0。|
|SQL_MAX_STATEMENT_LEN|2.0|SQLUINTEGER 值，指定最大長度 (的字元數，包括 SQL 語句的空白字元) 。 如果沒有最大長度，或長度不明，則此值會設定為零。|
|SQL_MAX_TABLE_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中資料表名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式將會傳回至少18個。 符合 FIPS 中繼層級的驅動程式至少會傳回128。|
|SQL_MAX_TABLES_IN_SELECT|2.0|SQLUSMALLINT 值，指定**SELECT**語句的**from**子句中所允許的最大資料表數目。 如果沒有指定的限制，或限制不明，此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式會傳回至少15個。 符合 FIPS 中繼層級的驅動程式至少會傳回50。|
|SQL_MAX_USER_NAME_LEN|2.0|SQLUSMALLINT 值，指定資料來源中使用者名稱的最大長度。 如果沒有最大長度，或長度不明，則此值會設定為零。|
|SQL_MULT_RESULT_SETS|1.0|字元字串：如果資料來源支援多個結果集，則為 "Y"，否則為 "N"。<br/><br/>如需多個結果集的詳細資訊，請參閱[多個結果](../develop-app/multiple-results.md)。|
|SQL_MULTIPLE_ACTIVE_TXN|1.0|字元字串：如果驅動程式同時支援一個以上的使用中交易，則為 "Y"，如果每次只能有一個交易可以使用，則為 "N"。<br/><br/>針對此資訊類型傳回的資訊，在分散式交易的情況下並不適用。|
|SQL_NEED_LONG_DATA_LEN|2.0|字元字串： "Y" 如果資料來源需要 long 資料值的長度， (資料類型是 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或長資料來源特定資料類型) 在該值傳送至資料來源之前，則為 "N"，否則為 "N"。 如需詳細資訊，請參閱[SQLBindParameter](sqlbindparameter-function.md)函式和[SQLSetPos 函數](sqlsetpos-function.md)。|
|SQL_NON_NULLABLE_COLUMNS|1.0|SQLUSMALLINT 值，指定資料來源在資料行中是否支援 NOT Null：<br/>SQL_NNC_Null = 所有資料行都必須是可為 null。<br/>SQL_NNC_NON_Null = 資料行不可為 null。  (資料來源支援**CREATE TABLE**語句中的**NOT Null**資料行條件約束。 ) <br/><br/>符合 SQL-92 專案層級的驅動程式將會傳回 SQL_NNC_NON_Null。|
|SQL_NULL_COLLATION|2.0|SQLUSMALLINT 值，指定在結果集中排序 Null 的位置：<br/>SQL_NC_END = Null 會在結果集的結尾進行排序，不論 ASC 或 DESC 關鍵字為何。<br/>SQL_NC_HIGH = Null 會在結果集的高階處排序，視 ASC 或 DESC 關鍵字而定。<br/>SQL_NC_LOW = Null 會在結果集的低端排序，視 ASC 或 DESC 關鍵字而定。<br/>SQL_NC_START = Null 會在結果集的開頭進行排序，不論 ASC 或 DESC 關鍵字為何。|
|SQL_NUMERIC_FUNCTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進的;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量數值函數。<br/><br/>下列位元遮罩是用來決定支援的數值函數：<br/>SQL_FN_NUM_ABS (ODBC 1.0) <br/>SQL_FN_NUM_ACOS (ODBC 1.0) <br/>SQL_FN_NUM_ASIN (ODBC 1.0) <br/>SQL_FN_NUM_ATAN (ODBC 1.0) <br/>SQL_FN_NUM_ATAN2 (ODBC 1.0) <br/>SQL_FN_NUM_CEILING (ODBC 1.0) <br/>SQL_FN_NUM_COS (ODBC 1.0) <br/>SQL_FN_NUM_COT (ODBC 1.0) <br/>SQL_FN_NUM_DEGREES (ODBC 2.0) <br/>SQL_FN_NUM_EXP (ODBC 1.0) <br/>SQL_FN_NUM_FLOOR (ODBC 1.0) <br/>SQL_FN_NUM_LOG (ODBC 1.0) <br/>SQL_FN_NUM_LOG10 (ODBC 2.0) <br/>SQL_FN_NUM_MOD (ODBC 1.0) <br/>SQL_FN_NUM_PI (ODBC 1.0) <br/>SQL_FN_NUM_POWER (ODBC 2.0) <br/>SQL_FN_NUM_RADIANS (ODBC 2.0) <br/>SQL_FN_NUM_RAND (ODBC 1.0) <br/>SQL_FN_NUM_ROUND (ODBC 2.0) <br/>SQL_FN_NUM_SIGN (ODBC 1.0) <br/>SQL_FN_NUM_SIN (ODBC 1.0) <br/>SQL_FN_NUM_SQRT (ODBC 1.0) <br/>SQL_FN_NUM_TAN (ODBC 1.0) <br/>SQL_FN_NUM_TRUNCATE (ODBC 2.0) |
|SQL_ODBC_INTERFACE_CONFORMANCE|3.0|SQLUINTEGER 值，表示驅動程式符合之 ODBC*3.x 介面的層級。*<br/><br/>SQL_OIC_CORE：所有 ODBC 驅動程式預期會符合的最低層級。 此層級包含基本介面專案，例如連接函數、準備和執行 SQL 語句的函式、基本結果集中繼資料函數、基本目錄函數等等。<br/>SQL_OIC_LEVEL1：包含核心標準合規性層級功能的層級，以及可滾動的資料指標、書簽、定點更新和刪除等。<br/>SQL_OIC_LEVEL2：層級，包括層級1標準合規性層級功能，以及敏感性資料指標之類的先進功能。依書簽更新、刪除和重新整理;預存程式支援;主鍵和外鍵的目錄函數;多目錄支援;以此類推。<br/><br/>如需詳細資訊，請參閱[介面一致性層級](../develop-app/interface-conformance-levels.md)。|
|SQL_ODBC_VER|1.0|具有驅動程式管理員所符合之 ODBC 版本的字元字串。 版本的格式為 # #. # #. 0000，其中前兩個數字是主要版本，而後面兩個數字是次要版本。 這只會在驅動程式管理員中執行。|
|SQL_OJ_CAPABILITIES|2.01|SQLUINTEGER 的位元遮罩，列舉驅動程式和資料來源所支援的外部聯結類型。 下列位元遮罩是用來決定支援的類型：<br/>SQL_OJ_LEFT = 支援左方外部聯結。<br/>SQL_OJ_RIGHT = 支援右方外部聯結。<br/>SQL_OJ_FULL = 支援完整外部聯結。<br/>SQL_OJ_NESTED = 支援嵌套的外部聯結。<br/>SQL_OJ_NOT_ORDERED = 外部聯結之 ON 子句中的資料行名稱，其順序不一定要與**外部聯結**子句中各自的資料表名稱相同。<br/>SQL_OJ_INNER = 內部資料表 (左方外部聯結中的右資料表，或右外部聯結中的左資料表) 也可以用於內部聯結。 這並不適用于沒有內部資料表的完整外部聯結。<br/>SQL_OJ_ALL_COMPARISON_OPS = ON 子句中的比較運算子可以是任何 ODBC 比較運算子。 如果未設定此位，則只有 equals (=) 比較運算子可以用於外部聯結。<br/><br/>如果這些選項都不是以支援的方式傳回，則不支援任何外部聯結子句。<br/><br/>如需 SELECT 語句（如 SQL-92 所定義）中關聯式聯結運算子支援的詳細資訊，請參閱 SQL_SQL92_RELATIONAL_JOIN_OPERATORS。|
|SQL_ORDER_BY_COLUMNS_IN_SELECT|2.0|字元字串：如果**ORDER BY**子句中的資料行必須在選取清單中，則為 "Y";否則為 "N"。|
|SQL_PARAM_ARRAY_ROW_COUNTS|3.0|SQLUINTEGER，列舉與參數化執行中的資料列計數可用性有關的驅動程式屬性。 具有下列值：<br/>SQL_PARC_BATCH = 每個參數集都有個別的資料列計數。 這在概念上相當於產生 SQL 語句批次的驅動程式，陣列中的每個參數集各一個。 您可以使用 [SQL_PARAM_STATUS_PTR 描述元] 欄位來抓取擴充的錯誤資訊。<br/>SQL_PARC_NO_BATCH = 只有一個可用的資料列計數，這是針對整個參數陣列執行語句所產生的累計資料列計數。 這在概念上相當於將語句連同完整的參數陣列視為一個不可部分完成的單位。 錯誤的處理方式與執行一個語句相同。|
|SQL_PARAM_ARRAY_SELECTS|3.0|SQLUINTEGER，列舉有關參數化執行中結果集可用性的驅動程式屬性。 具有下列值：<br/>SQL_PAS_BATCH = 每個參數集都有一個可用的結果集。 這在概念上相當於產生 SQL 語句批次的驅動程式，陣列中的每個參數集各一個。<br/>SQL_PAS_NO_BATCH = 只有一個可用的結果集，這代表針對完整參數陣列執行語句所產生的累計結果集。 這在概念上相當於將語句連同完整的參數陣列視為一個不可部分完成的單位。<br/>SQL_PAS_NO_SELECT = 驅動程式不允許以參數陣列執行結果集產生的語句。|
|SQL_POS_OPERATIONS|2.0|SQLINTEGER 位元遮罩，列舉**SQLSetPos**中的支援作業。<br/><br/>下列位元遮罩會與旗標一起使用，以判斷支援的選項。<br/>SQL_POS_POSITION (ODBC 2.0) <br/>SQL_POS_REFRESH (ODBC 2.0) <br/>SQL_POS_UPDATE (ODBC 2.0) <br/>SQL_POS_DELETE (ODBC 2.0) <br/>SQL_POS_ADD (ODBC 2.0) |
|SQL_PROCEDURE_TERM|1.0|包含程式之資料來源廠商名稱的字元字串;例如，「資料庫程式」、「預存程式」、「程式」、「封裝」或「預存查詢」。|
|SQL_PROCEDURES|1.0|字元字串：如果資料來源支援程式，而且驅動程式支援 ODBC 程序呼叫語法，則為 "Y";否則為 "N"。|
|SQL_QUOTED_IDENTIFIER_CASE|2.0|SQLUSMALLINT 值，如下所示：<br/>SQL_IC_UPPER = SQL 中的引號識別碼不區分大小寫，而且會以大寫儲存在系統目錄中。<br/>SQL_IC_LOWER = SQL 中的引號識別碼不區分大小寫，而且在系統目錄中會以小寫儲存。<br/>SQL_IC_SENSITIVE = SQL 中以引號括住的識別碼會區分大小寫，而且會以混合大小寫儲存在系統目錄中。  (在 SQL-92 相容的資料庫中，加上引號的識別碼一律區分大小寫。 ) <br/>SQL_IC_MIXED = SQL 中的引號識別碼不區分大小寫，而且會以混合大小寫儲存在系統目錄中。<br/><br/>符合 SQL 92 專案層級的驅動程式一律會傳回 SQL_IC_SENSITIVE。|
|SQL_ROW_UPDATES|1.0|字元字串：如果索引鍵集驅動或混合資料指標針對所有提取的資料列維護資料列版本或值，因此可以偵測自上次提取資料列之後，任何使用者對資料列所做的任何更新。  (這只適用于更新，而不是刪除或插入。 ) 驅動程式會在呼叫**SQLFetchScroll**時，將 SQL_ROW_UPDATED 旗標傳回至資料列狀態陣列。 否則為 "N"。|
|SQL_SCHEMA_TERM|1.0|具有架構之資料來源廠商名稱的字元字串;例如，「擁有者」、「授權識別碼」或「架構」。<br/><br/>字元字串可以用大寫、小寫或混合大小寫的方式傳回。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 "schema"。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_OWNER_TERM 重新命名為 odbc 3.0。|
|SQL_SCHEMA_USAGE|2.0|SQLUINTEGER 位元遮罩，列舉可以使用架構的語句：<br/>SQL_SU_DML_STATEMENTS = 所有資料操作語言語句都支援架構： **select**、 **INSERT**、 **UPDATE**、 **DELETE**和 if 支援，請**選取以取得 update**和定位 update 和 DELETE 子句。<br/>SQL_SU_PROCEDURE_INVOCATION = ODBC 程序呼叫語句中支援的架構。<br/>SQL_SU_TABLE_DEFINITION = 所有資料表定義語句都支援架構： **CREATE TABLE**、 **CREATE VIEW**、 **ALTER TABLE**、 **drop table**和**drop VIEW**。<br/>SQL_SU_INDEX_DEFINITION = 所有索引定義語句中都支援架構： **CREATE INDEX**和**DROP INDEX**。<br/>SQL_SU_PRIVILEGE_DEFINITION = 擁有權限定義語句中都支援架構： **GRANT**和**REVOKE**。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_SU_DML_STATEMENTS、SQL_SU_TABLE_DEFINITION 和 SQL_SU_PRIVILEGE_DEFINITION 選項（如受支援）。<br/><br/>此*InfoType*已從 Odbc 2.0 *InfoType* SQL_OWNER_USAGE 重新命名為 odbc 3.0。|
|SQL_SCROLL_OPTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進的;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，用來列舉可滾動資料指標所支援的捲軸選項。<br/><br/>下列位元遮罩是用來決定支援的選項：<br/>SQL_SO_FORWARD_ONLY = 資料指標只向前滾動。  (ODBC 1.0) <br/>SQL_SO_STATIC = 結果集中的資料是靜態的。  (ODBC 2.0) <br/>SQL_SO_KEYSET_DRIVEN = 驅動程式會儲存並使用結果集中每個資料列的索引鍵。  (ODBC 1.0) <br/>SQL_SO_DYNAMIC = 驅動程式會保留資料列集內每個資料列的索引鍵， (金鑰集大小與資料列集大小) 相同。  (ODBC 1.0) <br/>SQL_SO_MIXED = 驅動程式會針對索引鍵集中的每個資料列保留金鑰，而索引鍵集大小則大於資料列集大小。 資料指標是索引鍵集內的索引鍵集驅動，而且在索引鍵集外的動態。  (ODBC 1.0) <br/><br/>如需可滾動資料指標的詳細資訊，請參閱可[滾動資料指標](../develop-app/scrollable-cursors.md)。|
|SQL_SEARCH_PATTERN_ESCAPE|1.0|指定驅動程式支援的字元字串做為 escape 字元，允許使用模式比對元字元底線 (_) 和百分比符號 (% ) 做為搜尋模式中的有效字元。 此 escape 字元僅適用于支援搜尋字串的目錄函數引數。 如果這個字串是空的，則驅動程式不支援搜尋模式的 escape 字元。<br/><br/>因為此資訊類型不表示一般支援**LIKE**述詞中的 escape 字元，所以 SQL-92 不會包含此字元字串的需求。<br/><br/>此*InfoType*僅限於目錄功能。 如需在搜尋模式字串中使用 escape 字元的說明，請參閱[模式值引數](../develop-app/pattern-value-arguments.md)。|
|SQL_SERVER_NAME|1.0|具有實際資料來源特定伺服器名稱的字元字串;在**SQLConnect**、 **SQLDriverConnect**和**SQLBrowseConnect**期間使用資料來源名稱時很有用。|
|SQL_SPECIAL_CHARACTERS|2.0|包含所有特殊字元的字元字串 (也就是，除了 a 到 z、A 到 Z、0到9和底線) 以外的所有字元，可用於識別碼名稱中，例如資料表名稱、資料行名稱或索引名稱。 例如，"# $ ^"。 如果識別碼包含其中一或多個字元，則識別碼必須是分隔的識別碼。|
|SQL_SQL_CONFORMANCE|3.0|SQLUINTEGER 值，指出驅動程式支援的 SQL-92 層級：<br/>SQL_SC_SQL92_ENTRY = 進入層級 SQL-92 相容。<br/>SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 過渡層級相容。<br/>SQL_SC_SQL92_FULL = 完整層級的 SQL-92 相容。<br/>SQL_SC_ SQL92_INTERMEDIATE = 中繼層級 SQL-92 相容。|
|SQL_SQL92_DATETIME_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的 datetime 純量函數，如 SQL-92 中所定義。<br/><br/>下列位元遮罩是用來決定支援的日期時間函數：<br/>SQL_SDF_CURRENT_DATE<br/>SQL_SDF_CURRENT_TIME<br/>SQL_SDF_CURRENT_TIMESTAMP|
|SQL_SQL92_FOREIGN_KEY_DELETE_RULE|3.0|SQLUINTEGER 位元遮罩，列舉**DELETE**語句中的外鍵所支援的規則，如 SQL-92 中所定義。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的子句：<br/>SQL_SFKD_CASCADE<br/>SQL_SFKD_NO_ACTION<br/>SQL_SFKD_SET_DEFAULT<br/>SQL_SFKD_SET_Null<br/><br/>符合 FIPS 轉換層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_SQL92_FOREIGN_KEY_UPDATE_RULE|3.0|SQLUINTEGER 位元遮罩，列舉**UPDATE**語句中的外鍵支援的規則，如 SQL-92 中所定義。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的子句：<br/>SQL_SFKU_CASCADE<br/>SQL_SFKU_NO_ACTION<br/>SQL_SFKU_SET_DEFAULT<br/>SQL_SFKU_SET_Null<br/><br/>符合 SQL 92 完整層級的驅動程式一律會傳回所有這些選項，並受到支援。|
|SQL_SQL92_GRANT|3.0|SQLUINTEGER 位元遮罩，列舉**GRANT**語句中支援的子句，如 SQL-92 中所定義。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的子句：<br/>SQL_SG_DELETE_TABLE (專案層級) <br/>SQL_SG_INSERT_COLUMN (中繼層級) <br/>SQL_SG_INSERT_TABLE (專案層級) <br/>SQL_SG_REFERENCES_TABLE (專案層級) <br/>SQL_SG_REFERENCES_COLUMN (專案層級) <br/>SQL_SG_SELECT_TABLE (專案層級) <br/>SQL_SG_UPDATE_COLUMN (專案層級) <br/>SQL_SG_UPDATE_TABLE (專案層級) <br/>SQL_SG_USAGE_ON_DOMAIN (FIPS 過渡層級) <br/>SQL_SG_USAGE_ON_CHARACTER_SET (FIPS 過渡層級) <br/>SQL_SG_USAGE_ON_COLLATION (FIPS 過渡層級) <br/>SQL_SG_USAGE_ON_TRANSLATION (FIPS 過渡層級) <br/>SQL_SG_WITH_GRANT_OPTION (專案層級) |
|SQL_SQL92_NUMERIC_VALUE_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯的資料來源所支援的數值純量函數（如 SQL-92 中所定義）。<br/><br/>下列位元遮罩是用來決定支援的數值函數：<br/>SQL_SNVF_BIT_LENGTH<br/>SQL_SNVF_CHAR_LENGTH<br/>SQL_SNVF_CHARACTER_LENGTH<br/>SQL_SNVF_EXTRACT<br/>SQL_SNVF_OCTET_LENGTH<br/>SQL_SNVF_POSITION|
|SQL_SQL92_PREDICATES|3.0|SQLUINTEGER 位元遮罩，列舉**SELECT**語句中支援的述詞，如 SQL-92 中所定義。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的選項：<br/>SQL_SP_BETWEEN (專案層級) <br/>SQL_SP_COMPARISON (專案層級) <br/>SQL_SP_EXISTS (專案層級) <br/>SQL_SP_IN (專案層級) <br/>SQL_SP_ISNOTNull (專案層級) <br/>SQL_SP_ISNull (專案層級) <br/>SQL_SP_LIKE (專案層級) <br/>SQL_SP_MATCH_FULL (完整層級) <br/>SQL_SP_MATCH_PARTIAL (完整層級) <br/>SQL_SP_MATCH_UNIQUE_FULL (完整層級) <br/>SQL_SP_MATCH_UNIQUE_PARTIAL (完整層級) <br/>SQL_SP_OVERLAPS (FIPS 過渡層級) <br/>SQL_SP_QUANTIFIED_COMPARISON (專案層級) <br/>SQL_SP_UNIQUE (專案層級) |
|SQL_SQL92_RELATIONAL_JOIN_OPERATORS|3.0|SQLUINTEGER 位元遮罩，列舉**SELECT**語句中所支援的關聯式聯結運算子，如 SQL-92 中所定義。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的選項：<br/>SQL_SRJO_CORRESPONDING_CLAUSE (中繼層級) <br/>SQL_SRJO_CROSS_JOIN (完整層級) <br/>SQL_SRJO_EXCEPT_JOIN (中繼層級) <br/>SQL_SRJO_FULL_OUTER_JOIN (中繼層級) <br/>SQL_SRJO_INNER_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_INTERSECT_JOIN (中繼層級) <br/>SQL_SRJO_LEFT_OUTER_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_NATURAL_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_RIGHT_OUTER_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_UNION_JOIN (完整層級) <br/><br/>SQL_SRJO_INNER_JOIN 表示**內部聯結**語法的支援，而不是內部聯結功能的支援。 **內部聯結**語法的支援是 FIPS 過渡，而內部聯結功能的支援則是**專案**。|
|SQL_SQL92_REVOKE|3.0|SQLUINTEGER 位元遮罩，列舉由資料來源支援的**REVOKE**語句（如 SQL-92 中所定義）所支援的子句。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的子句：<br/>SQL_SR_CASCADE (FIPS 過渡層級) <br/>SQL_SR_DELETE_TABLE (專案層級) <br/>SQL_SR_GRANT_OPTION_FOR (中繼層級) <br/>SQL_SR_INSERT_COLUMN (中繼層級) <br/>SQL_SR_INSERT_TABLE (專案層級) <br/>SQL_SR_REFERENCES_COLUMN (專案層級) <br/>SQL_SR_REFERENCES_TABLE (專案層級) <br/>SQL_SR_RESTRICT (FIPS 過渡層級) <br/>SQL_SR_SELECT_TABLE (專案層級) <br/>SQL_SR_UPDATE_COLUMN (專案層級) <br/>SQL_SR_UPDATE_TABLE (專案層級) <br/>SQL_SR_USAGE_ON_DOMAIN (FIPS 過渡層級) <br/>SQL_SR_USAGE_ON_CHARACTER_SET (FIPS 過渡層級) <br/>SQL_SR_USAGE_ON_COLLATION (FIPS 過渡層級) <br/>SQL_SR_USAGE_ON_TRANSLATION (FIPS 過渡層級) |
|SQL_SQL92_ROW_VALUE_CONSTRUCTOR|3.0|SQLUINTEGER 位元遮罩，列舉**SELECT**語句中支援的資料列值函數運算式，如 SQL-92 中所定義。 下列位元遮罩是用來判斷資料來源所支援的選項：<br/>SQL_SRVC_VALUE_EXPRESSION<br/>SQL_SRVC_Null<br/>SQL_SRVC_DEFAULT<br/>SQL_SRVC_ROW_SUBQUERY|
|SQL_SQL92_STRING_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩，用來列舉驅動程式支援的字串純量函數和相關聯的資料來源（如 SQL-92 中所定義）。<br/><br/>下列位元遮罩是用來決定支援的字串函數：<br/>SQL_SSF_CONVERT<br/>SQL_SSF_LOWERSQL_SSF_UPPER<br/>SQL_SSF_SUBSTRING<br/>SQL_SSF_TRANSLATE<br/>SQL_SSF_TRIM_BOTH<br/>SQL_SSF_TRIM_LEADING<br/>SQL_SSF_TRIM_TRAILING|
|SQL_SQL92_VALUE_EXPRESSIONS|3.0|SQLUINTEGER 位元遮罩，列舉支援的值運算式（如 SQL-92 中所定義）。<br/><br/>這項功能必須受到支援的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁邊的括弧中。<br/><br/>下列位元遮罩是用來判斷資料來源所支援的選項：<br/>SQL_SVE_CASE (中繼層級) <br/>SQL_SVE_CAST (FIPS 過渡層級) <br/>SQL_SVE_COALESCE (中繼層級) <br/>SQL_SVE_NullIF (中繼層級) |
|SQL_STANDARD_CLI_CONFORMANCE|3.0|SQLUINTEGER 的位元遮罩，列舉驅動程式符合的 CLI 標準或標準。 下列位元遮罩是用來判斷驅動程式符合的層級：<br/>SQL_SCC_XOPEN_CLI_VERSION1：此驅動程式符合 Open Group CLI 第1版。<br/>SQL_SCC_ISO92_CLI：此驅動程式符合 ISO 92 CLI。|
|SQL_STATIC_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 的位元遮罩，描述驅動程式所支援之靜態資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_STATIC_CURSOR_ATTRIBUTES2。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA1_NEXT<br/>SQL_CA1_ABSOLUTE<br/>SQL_CA1_RELATIVE<br/>SQL_CA1_BOOKMARK<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在 [描述]) 中，將「靜態資料指標」替換為「動態資料指標」。<br/><br/>SQL-92 中繼層級一致的驅動程式通常會傳回所支援的 SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項，因為驅動程式支援透過內嵌 SQL FETCH 語句的可滾動資料指標。 由於這不會直接判斷基礎 SQL 支援，因此，即使是 SQL-92 中繼層級一致的驅動程式，也可能不支援可滾動的資料指標。|
|SQL_STATIC_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 的位元遮罩，描述驅動程式所支援之靜態資料指標的屬性。 此位元遮罩包含屬性的第二個子集;如需第一個子集，請參閱 SQL_STATIC_CURSOR_ATTRIBUTES1。<br/><br/>下列位元遮罩是用來決定支援的屬性：<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (，並在 [描述]) 中，將「靜態資料指標」替換為「動態資料指標」。|
|SQL_STRING_FUNCTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進的;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，用來列舉驅動程式和相關聯資料來源所支援的純量字串函數。<br/><br/>下列位元遮罩是用來決定支援的字串函數：<br/>SQL_FN_STR_ASCII (ODBC 1.0) <br/>SQL_FN_STR_BIT_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_CHAR (ODBC 1.0) <br/>SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_CONCAT (ODBC 1.0) <br/>SQL_FN_STR_DIFFERENCE (ODBC 2.0) <br/>SQL_FN_STR_INSERT (ODBC 1.0) <br/>SQL_FN_STR_LCASE (ODBC 1.0) <br/>SQL_FN_STR_LEFT (ODBC 1.0) <br/>SQL_FN_STR_LENGTH (ODBC 1.0) <br/>SQL_FN_STR_LOCATE (ODBC 1.0) <br/>SQL_FN_STR_LTRIM (ODBC 1.0) <br/>SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_POSITION (ODBC 3.0) <br/>SQL_FN_STR_REPEAT (ODBC 1.0) <br/>SQL_FN_STR_REPLACE (ODBC 1.0) <br/>SQL_FN_STR_RIGHT (ODBC 1.0) <br/>SQL_FN_STR_RTRIM (ODBC 1.0) <br/>SQL_FN_STR_SOUNDEX (ODBC 2.0) <br/>SQL_FN_STR_SPACE (ODBC 2.0) <br/>SQL_FN_STR_SUBSTRING (ODBC 1.0) <br/>SQL_FN_STR_UCASE (ODBC 1.0) <br/><br/>如果應用程式可以使用*string_exp1*、 *string_exp2*和*Start*引數來呼叫**尋找**純量函數，驅動程式會傳回 SQL_FN_STR_LOCATE 的位元遮罩。 如果應用程式可以呼叫僅具有*string_exp1*和*string_exp2*引數的尋找純量函數，則驅動程式會傳回 SQL_FN_STR_LOCATE_2 的位元遮罩。 完全支援「**尋找**純量函數」的驅動程式會傳回這兩個位遮罩。<br/><br/> (需詳細資訊，請參閱附錄 E 的「純量函數」中的[字串函數](../appendixes/string-functions.md)。) |
|SQL_SUBQUERIES|2.0|SQLUINTEGER 位元遮罩，列舉支援子查詢的述詞：<br/>SQL_SQ_CORRELATED_SUBQUERIES<br/>SQL_SQ_COMPARISON<br/>SQL_SQ_EXISTS<br/>SQL_SQ_INSQL_SQ_QUANTIFIED<br/><br/>SQL_SQ_CORRELATED_SUBQUERIES 位元遮罩表示支援子查詢的所有述詞都支援相互關聯的子查詢。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回所有這些位都已設定的位元遮罩。|
|SQL_SYSTEM_FUNCTIONS|1.0|SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量系統函數。<br/><br/>下列位元遮罩是用來判斷支援哪些系統函數：<br/>SQL_FN_SYS_DBNAME<br/>SQL_FN_SYS_IFNull<br/>SQL_FN_SYS_USERNAME|
|SQL_TABLE_TERM|1.0|具有資料表之資料來源廠商名稱的字元字串;例如，"table" 或 "file"。<br/><br/>這個字元字串可以是大寫、小寫或混合大小寫。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 "table"。|
|SQL_TIMEDATE_ADD_INTERVALS|2.0|SQLUINTEGER 位元遮罩，列舉 TIMESTAMPADD 純量函數的驅動程式所支援的時間戳記間隔和相關聯的資料來源。<br/><br/>下列位元遮罩是用來決定支援的間隔：<br/>SQL_FN_TSI_FRAC_SECOND<br/>SQL_FN_TSI_SECOND<br/>SQL_FN_TSI_MINUTE<br/>SQL_FN_TSI_HOUR<br/>SQL_FN_TSI_DAY<br/>SQL_FN_TSI_WEEK<br/>SQL_FN_TSI_MONTH<br/>SQL_FN_TSI_QUARTER<br/>SQL_FN_TSI_YEAR<br/><br/>符合 FIPS 轉換等級的驅動程式一律會傳回位元遮罩，其中所有的位都已設定。|
|SQL_TIMEDATE_DIFF_INTERVALS|2.0|SQLUINTEGER 位元遮罩，列舉 TIMESTAMPDIFF 純量函數的驅動程式所支援的時間戳記間隔和相關聯的資料來源。<br/><br/>下列位元遮罩是用來決定支援的間隔：<br/>SQL_FN_TSI_FRAC_SECOND<br/>SQL_FN_TSI_SECOND<br/>SQL_FN_TSI_MINUTE<br/>SQL_FN_TSI_HOUR<br/>SQL_FN_TSI_DAY<br/>SQL_FN_TSI_WEEK<br/>SQL_FN_TSI_MONTH<br/>SQL_FN_TSI_QUARTER<br/>SQL_FN_TSI_YEAR<br/><br/>符合 FIPS 轉換等級的驅動程式一律會傳回位元遮罩，其中所有的位都已設定。|
|SQL_TIMEDATE_FUNCTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進的;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量日期和時間函數。<br/><br/>下列位元遮罩是用來決定支援的日期和時間函數：<br/>SQL_FN_TD_CURRENT_DATE (ODBC 3.0) <br/>SQL_FN_TD_CURRENT_TIME (ODBC 3.0) <br/>SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) <br/>SQL_FN_TD_CURDATE (ODBC 1.0) <br/>SQL_FN_TD_CURTIME (ODBC 1.0) <br/>SQL_FN_TD_DAYNAME (ODBC 2.0) <br/>SQL_FN_TD_DAYOFMONTH (ODBC 1.0) <br/>SQL_FN_TD_DAYOFWEEK (ODBC 1.0) <br/>SQL_FN_TD_DAYOFYEAR (ODBC 1.0) <br/>SQL_FN_TD_EXTRACT (ODBC 3.0) <br/>SQL_FN_TD_HOUR (ODBC 1.0) <br/>SQL_FN_TD_MINUTE (ODBC 1.0) <br/>SQL_FN_TD_MONTH (ODBC 1.0) <br/>SQL_FN_TD_MONTHNAME (ODBC 2.0) <br/>SQL_FN_TD_NOW (ODBC 1.0) <br/>SQL_FN_TD_QUARTER (ODBC 1.0) <br/>SQL_FN_TD_SECOND (ODBC 1.0) <br/>SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) <br/>SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) <br/>SQL_FN_TD_WEEK (ODBC 1.0) <br/>SQL_FN_TD_YEAR (ODBC 1.0) |
|SQL_TXN_CAPABLE|1.0|注意：此資訊類型是在 ODBC 1.0 中引進的;每個傳回值都會標示其引進的版本。<br/><br/>描述驅動程式或資料來源中交易支援的 SQLUSMALLINT 值：<br/>SQL_TC_NONE = 不支援的交易。  (ODBC 1.0) <br/>SQL_TC_DML = 交易只能包含 (DML) 語句 (**SELECT**、 **INSERT**、 **UPDATE**、 **DELETE**) 的資料操作語言。 在交易中遇到的資料定義語言 (DDL) 語句會造成錯誤。  (ODBC 1.0) <br/>SQL_TC_DDL_COMMIT = 交易只能包含 DML 語句。 DDL 語句 (在交易中遇到的) **CREATE TABLE**、 **DROP INDEX**等等，而導致交易被認可。  (ODBC 2.0) <br/>SQL_TC_DDL_IGNORE = 交易只能包含 DML 語句。 在交易中遇到的 DDL 語句會被忽略。  (ODBC 2.0) <br/>SQL_TC_ALL = 交易可以包含 DDL 語句和 DML 語句（依任何順序）。  (ODBC 1.0) <br/><br/> (因為在 SQL-92 中必須支援交易，所以符合 SQL-92 的驅動程式 [任何層級] 永遠不會傳回 SQL_TC_NONE。 ) |
|SQL_TXN_ISOLATION_OPTION|1.0|SQLUINTEGER 的位元遮罩，列舉驅動程式或資料來源中可用的交易隔離等級。<br/><br/>下列位元遮罩會與旗標一起使用，以判斷支援的選項：<br/>SQL_TXN_READ_UNCOMMITTED<br/>SQL_TXN_READ_COMMITTED<br/>SQL_TXN_REPEATABLE_READ<br/>SQL_TXN_SERIALIZABLE<br/><br/>如需這些隔離等級的說明，請參閱 SQL_DEFAULT_TXN_ISOLATION 的描述。<br/><br/>若要設定交易隔離等級，應用程式會呼叫**SQLSetConnectAttr**來設定 SQL_ATTR_TXN_ISOLATION 屬性。 如需詳細資訊，請參閱[SQLSetConnectAttr 函數](sqlsetconnectattr-function.md)。<br/><br/>符合 SQL 92 專案層級的驅動程式一律會傳回 SQL_TXN_SERIALIZABLE 支援。 符合 FIPS 轉換層級的驅動程式一律會傳回所有這些選項（如有支援）。|
|SQL_UNION|2.0|列舉**UNION**子句支援的 SQLUINTEGER 位元遮罩：<br/>SQL_U_UNION = 資料來源支援**UNION**子句。<br/>SQL_U_UNION_ALL = 資料來源支援**UNION**子句中的**ALL**關鍵字。 在此情況下， (**SQLGetInfo**會傳回 SQL_U_UNION 和 SQL_U_UNION_ALL。 ) <br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回這兩個選項的支援。|
|SQL_USER_NAME|1.0|在特定資料庫中使用名稱的字元字串，可以與登入名稱不同。|
|SQL_XOPEN_CLI_YEAR|3.0|字元字串，指出發行群組規格的發行年份，而此版本的 ODBC 驅動程式管理員會完全符合此標準。|
  
## <a name="example"></a>範例  

 **SQLGetInfo**會傳回支援的選項清單，做為 **INFOVALUEPTR*中的 SQLUINTEGER 位元遮罩。 每個選項的位元遮罩會與旗標一起使用，以判斷是否支援此選項。  
  
 例如，應用程式可以使用下列程式碼來判斷與連接相關聯的驅動程式是否支援 SUBSTRING 純量函數。  
  
 如需使用**SQLGetInfo**的另一個範例，請參閱[SQLTables 函數](sqltables-function.md)。  
  
```cpp  
SQLUINTEGER fFuncs;  
  
SQLGetInfo(hdbc,  
           SQL_STRING_FUNCTIONS,  
           (SQLPOINTER)&fFuncs,  
           sizeof(fFuncs),  
           NULL);  
  
// SUBSTRING supported  
if (fFuncs & SQL_FN_STR_SUBSTRING)  
   ;   // do something  
  
// SUBSTRING not supported  
else  
   ;   // do something else  
```  
  
## <a name="related-functions"></a>相關函數  

 傳回連接屬性的設定  
 [SQLGetConnectAttr 函數](sqlgetconnectattr-function.md)  
  
 判斷驅動程式是否支援函數  
 [SQLGetFunctions 函式](sqlgetfunctions-function.md)  
  
 傳回語句屬性的設定  
 [SQLGetStmtAttr 函式](sqlgetstmtattr-function.md)  
  
 傳回資料來源資料類型的相關資訊  
 [SQLGetTypeInfo 函式](sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>另請參閱  

 [ODBC API 參考](odbc-api-reference.md)  
 [ODBC 標頭檔](../install/odbc-header-files.md)
