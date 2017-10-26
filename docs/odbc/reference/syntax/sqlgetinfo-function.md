---
title: "SQLGetInfo 函數 |Microsoft 文件"
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
- SQLGetInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetInfo
helpviewer_keywords:
- SQLGetInfo function [ODBC]
ms.assetid: 49dceccc-d816-4ada-808c-4c6138dccb64
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 57ba22ee8645f1d3548be91adc9aafb4fc016c79
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetInfo**傳回與連接相關聯的驅動程式和資料來源的一般資訊。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetInfo(  
     SQLHDBC         ConnectionHandle,  
     SQLUSMALLINT    InfoType,  
     SQLPOINTER      InfoValuePtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *資訊類型*  
 [輸入]資訊類型。  
  
 *InfoValuePtr*  
 [輸出]這是要傳回資訊的緩衝區指標。 取決於*資訊類型*要求，傳回的資訊將會是下列其中一種： null 結尾字元字串、 SQLUSMALLINT 值、 SQLUINTEGER 位元遮罩，SQLUINTEGER 旗標、 SQLUINTEGER 二進位值，或SQLULEN 值。  
  
 如果*資訊類型*引數是 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT， *InfoValuePtr*引數是輸入和輸出。 （請參閱 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT 描述元，稍後在這個函式描述，如需詳細資訊）。  
  
 如果*InfoValuePtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回中所指向的緩衝區*InfoValuePtr*。  
  
 *Columnsize*  
 [輸入]長度\* *InfoValuePtr*緩衝區。 如果中的值* \*InfoValuePtr*不是字元字串或*InfoValuePtr*為 null 指標， *Columnsize*會忽略引數。 驅動程式假設大小* \*InfoValuePtr* SQLUSMALLINT 或 SQLUINTEGER，根據*資訊類型*。 如果* \*InfoValuePtr*是 Unicode 字串 (呼叫時**SQLGetInfoW**)、 *Columnsize* ，SQLSTATE hy090 以及 （如果引數必須是偶數。會傳回字串或緩衝區長度無效）。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不含字元資料的 null 終止字元） 的緩衝區指標可用來傳回中 **InfoValuePtr*。  
  
 若是字元資料，可用來傳回的位元組數目是否大於或等於*Columnsize*中的資訊\* *InfoValuePtr*會被截斷成*Columnsize* null 終止的長度減位元組字元，而且是以 null 結束的驅動程式。  
  
 對於所有其他類型的資料，值*Columnsize*會略過驅動程式會假設的大小和\* *InfoValuePtr*是 SQLUSMALLINT 或 SQLUINTEGER，取決於*資訊類型*。  
  
## <a name="return-value"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetInfo**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_DBC 和*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetInfo** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *InfoValuePtr*仍不夠大，無法傳回要求的資訊。 因此，資訊會被截斷。 中會傳回所要求的資訊未截斷格式長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連線。|(DM) 中的資訊類型要求*資訊類型*需要開啟的連接。 ODBC 所保留的資訊類型，可傳回僅 SQL_ODBC_VER 沒有開啟的連線。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY024|屬性值無效|(DM)*資訊類型*引數以前是 SQL_DRIVER_HSTMT，以及值所指向*InfoValuePtr*不是有效的陳述式控制代碼。<br /><br /> (DM)*資訊類型*引數以前是 SQL_DRIVER_HDESC，以及值所指向*InfoValuePtr*不是有效的描述項控制代碼。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*Columnsize*小於 0。<br /><br /> (DM) 指定的值*Columnsize*為奇數，和* \*InfoValuePtr*是 Unicode 資料類型。|  
|HY096|資訊類型超出範圍|指定的引數的值*資訊類型*對 ODBC 驅動程式支援的版本無效。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作的選擇性欄位|指定的引數的值*資訊類型*是驅動程式不支援的驅動程式專屬值。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式對應至*ConnectionHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 目前已定義的資訊類型會顯示在此區段中，稍後的 「 資訊類型 」預期的是多個將會利用不同的資料來源定義。 ODBC; 保留各種資訊類型驅動程式開發人員必須保留自己從開啟 群組的特定驅動程式使用的值。 **SQLGetInfo**不執行 Unicode 轉換或*thunking* (請參閱[附錄 a: ODBC 錯誤碼](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)的*ODBC 程式設計人員參考*) 的驅動程式定義*InfoTypes*。 如需詳細資訊，請參閱[驅動程式特定資料類型，描述元類型、 資訊類型、 診斷的型別，以及屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 傳回的資訊格式\* *InfoValuePtr*取決於*資訊類型*要求。 **SQLGetInfo**將五個不同的格式之一傳回資訊：  
  
-   以 null 結束的字元字串  
  
-   SQLUSMALLINT 值  
  
-   SQLUINTEGER 位元遮罩  
  
-   SQLUINTEGER 值  
  
-   SQLUINTEGER 二進位值  
  
 下列資訊類型的格式加註的類型描述中。 應用程式必須轉換中傳回的值 **InfoValuePtr*據此。 如需如何應用程式時，無法從 SQLUINTEGER 位元遮罩，擷取資料的範例，請參閱 < 程式碼範例 >。  
  
 驅動程式必須傳回每個定義下表中的資訊類型的值。 資訊類型不適用於驅動程式或資料來源，如果驅動程式會傳回其中一個值，如下表所示。  
  
 字元字串 （"Y"或"N"）  
 "N"  
  
 字元字串 （不"Y"或"N"）  
 空字串  
  
 SQLUSMALLINT  
 0  
  
 SQLUINTEGER 位元遮罩或 SQLUINTEGER 二進位值  
 0 L  
  
 例如，如果資料來源不支援的程序， **SQLGetInfo**傳回的值列於下表中的值*資訊類型*相關的程序。  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 空字串  
  
 **SQLGetInfo**傳回 SQLSTATE HY096 （無效的引數的值） 的值*資訊類型*會保留供 ODBC 的資訊類型的範圍中，但不是會由 ODBC 驅動程式支援的版本。 若要判斷哪些版本的 ODBC 驅動程式符合，應用程式呼叫**SQLGetInfo** SQL_DRIVER_ODBC_VER 資訊類型。 **SQLGetInfo**傳回 SQLSTATE HYC00 （未實作的選擇性功能） 的值*資訊類型*會保留供驅動程式特有的資訊類型的範圍中，但不是會受到此驅動程式。  
  
 所有呼叫**SQLGetInfo**需要開啟連接，除非*資訊類型*是 SQL_ODBC_VER，它會傳回版本的驅動程式管理員。  
  
## <a name="information-types"></a>資訊類型  
 此區段會列出所支援的資訊類型**SQLGetInfo**。 資訊類型以分類方式來分組，並依字母順序列出。 已加入或重新命名，針對 ODBC 3 的資訊類型*.x*也會列出。  
  
## <a name="driver-information"></a>驅動程式的資訊  
 下列值的*資訊類型*引數傳回的 ODBC 驅動程式，例如作用中陳述式、 資料來源名稱，以及介面標準相容性層級數目的相關資訊：  
  
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
>  當實作**SQLGetInfo**，驅動程式可以改善效能的資訊傳送，或從伺服器要求的次數降到最低。  
  
## <a name="dbms-product-information"></a>DBMS 的產品資訊  
 下列值的*資訊類型*引數傳回 DBMS 產品，例如 DBMS 名稱和版本的相關資訊：  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>資料來源資訊  
 下列值的*資訊類型*引數傳回的資料來源，例如資料指標的特性和交易功能的相關資訊：  
  
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
 下列值的*資訊類型*引數傳回的資料來源所支援的 SQL 陳述式的相關資訊。 這些資訊類型所描述的每項功能的 SQL 語法是 SQL 92 語法。 這些資訊的類型不會徹底描述整個 sql-92 文法。 相反地，它們會描述這些組件的資料來源通常會提供不同的支援層級的文法。 具體來說，涵蓋了大部分的 SQL 92 中的 DDL 陳述式。  
  
 應用程式應該判斷 SQL_SQL_CONFORMANCE 類型資訊，請從支援的文法的一般層級，並使用其他的資訊類型判斷所述的標準相容性層級的變化。  
  
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
 下列值的*資訊類型*引數傳回套用至識別碼和子句，在 SQL 陳述式，例如識別碼和選取清單中的資料行數目上限的最大長度限制的相關資訊。 驅動程式或資料來源可加諸限制。  
  
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
 下列值的*資訊類型*引數傳回的資料來源和驅動程式所支援的純量函數的相關資訊。 如需純量函數的詳細資訊，請參閱[附錄 e： 純量函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>轉換資訊  
 下列值的*資訊類型*引數傳回的資料來源可以將具有指定的 SQL 資料類型轉換的 SQL 資料型別清單**轉換**純量函數：  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>資訊類型加入 odbc 3.x  
 下列值的*資訊類型*引數已新增適用於 ODBC 3*.x*:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>資訊類型重新命名以 ODBC 3.x  
 下列值的*資訊類型*引數已重新命名為 ODBC 3*.x*。  
  
 SQL_ACTIVE_CONNECTIONS  
 SQL_MAX_DRIVER_CONNECTIONS  
  
 SQL_ACTIVE_STATEMENTS  
 SQL_MAX_CONCURRENT_ACTIVITIES  
  
 SQL_MAX_OWNER_NAME_LEN  
 SQL_MAX_SCHEMA_NAME_LEN  
  
 SQL_MAX_QUALIFIER_NAME_LEN  
 SQL_MAX_CATALOG_NAME_LEN  
  
 SQL_ODBC_SQL_OPT_IEF  
 SQL_INTEGRITY  
  
 SQL_OWNER_TERM  
 SQL_SCHEMA_TERM  
  
 SQL_OWNER_USAGE  
 SQL_SCHEMA_USAGE  
  
 SQL_QUALIFIER_LOCATION  
 SQL_CATALOG_LOCATION  
  
 SQL_QUALIFIER_NAME_SEPARATOR  
 SQL_CATALOG_NAME_SEPARATOR  
  
 SQL_QUALIFIER_TERM  
 SQL_CATALOG_TERM  
  
 SQL_QUALIFIER_USAGE  
 SQL_CATALOG_USAGE  
  
## <a name="information-types-deprecated-in-odbc-3x"></a>在 ODBC 中已被取代的資訊類型 3.x  
 下列值的*資訊類型*引數已被取代，在 ODBC 3*.x*。 ODBC 3*.x*驅動程式必須繼續支援這些資訊類型回溯相容性的 ODBC 2*.x*應用程式。 (如需有關這些類型的詳細資訊，請參閱[SQLGetInfo 支援](../../../odbc/reference/appendixes/sqlgetinfo-support.md)附錄 g： 驅動程式的指導方針回溯相容性中。)  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>資訊類型的描述  
 下表依字母順序列出每種資料類型、 ODBC 中，它引進，以及其描述的版本。  
  
 SQL_ACCESSIBLE_PROCEDURES ODBC (1.0)  
 字元字串： 如果使用者可以執行所有的程序所傳回"Y" **SQLProcedures**;"N"(如果可能有程序會傳回該使用者無法執行。  
  
 SQL_ACCESSIBLE_TABLES ODBC (1.0)  
 字元字串:"Y"(如果使用者是否保證**選取**所傳回的所有資料表的權限**SQLTables**;如果可能有資料表"N"會傳回使用者無法存取。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 指定的驅動程式可以支援的使用中環境的最大數目的 SQLUSMALLINT 值。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉支援彙總函式：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL 92 項目層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**ALTER 網域**陳述式，如 SQL 92，支援的資料來源中定義。 SQL 92 完整的層級相容驅動程式一定會傳回所有位元遮罩。 傳回值為"0"表示**ALTER 網域**不支援陳述式。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 的加入支援網域條件約束 （完整層級）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 網域 > \<set 網域預設子句 > 支援 （完整層級）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<條件約束名稱定義子句 > 支援命名 網域條件約束 （中介層級）  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop 網域條件約束子句 > 支援 （完整層級）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 網域 > \<drop 網域預設子句 > 支援 （完整層級）  
  
 下列的位元會指定支援\<條件約束屬性 > 如果\<加入網域的條件約束 > 支援 （設定 SQL_AD_ADD_DOMAIN_CONSTRAINT 位元）：  
  
 （完整的層級） SQL_AD_ADD_CONSTRAINT_DEFERRABLE SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE （完整的層級） SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED （完整的層級） SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE （完整的層級）  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**ALTER TABLE**資料來源所支援的陳述式。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<加入資料行 > 支援子句，來指定資料行定序 （完整的層級） 的設備 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<加入資料行 > 支援子句，指定資料行的預設值 （FIPS 過渡期的層級） 的功能 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<加入資料行 > 會支援 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<加入資料行 > 支援子句，來指定資料行條件約束 （FIPS 過渡期的層級） 的設備 (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<加入資料表條件約束 > 支援子句 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<條件約束名稱定義 > 來命名資料行和資料表條件約束 （中介層級） 支援 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<卸除資料行 > 支援串聯 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT =\<改變資料行 >\<卸除資料行預設子句 > 會支援 （中介層級） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<卸除資料行 > 支援限制 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<卸除資料行 > 支援限制 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT =\<改變資料行 >\<集資料行預設子句 > 會支援 （中介層級） (ODBC 3.0)  
  
 下列的位元會指定支援\<條件約束屬性 > 如果支援指定資料行或資料表條件約束 （設定 SQL_AT_ADD_CONSTRAINT 位元）：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED （完整的層級） (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （完整的層級） (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE （完整的層級） (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE （完整的層級） (ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 SQLUINTEGER 值，指出如果驅動程式可以函式以非同步方式執行連接控制代碼上。  
  
 SQL_ASYNC_DBC_CAPABLE = 驅動程式能夠以非同步方式執行連線函式。  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 驅動程式無法以非同步方式執行連線函式。  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 SQLUINTEGER 值，表示驅動程式中的非同步支援，層級：  
  
 SQL_AM_CONNECTION = 支援層級的非同步執行的連接。 請指定的連接控制代碼相關聯的所有陳述式控制代碼處於非同步模式或都在同步模式中。 在連接上的陳述式控制代碼不可以是非同步模式時相同的連接上的另一個陳述式控制代碼會在同步模式中，反之亦然。  
  
 SQL_AM_STATEMENT = 支援層級的非同步執行的陳述式。 當相同的連接上的其他陳述式控制代碼處於同步模式下，可以是在非同步模式中，連接控制代碼相關聯的某些陳述式控制代碼。  
  
 SQL_AM_NONE = 非同步模式不支援。  
  
 SQL_ASYNC_NOTIFICATION  
 SQLUINTEGER 值，指出驅動程式是否支援非同步通知：  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE**驅動程式支援非同步執行的通知。  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE**驅動程式不支援非同步執行的通知。  
  
 有兩個 ODBC 非同步作業的類別： 連接層級的非同步作業和陳述式層級的非同步作業。  如果驅動程式傳回 SQL_ASYNC_NOTIFICATION_CAPABLE，就必須支援通知，它可以在以非同步方式執行的所有 api。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 計算 SQLUINTEGER 位元遮罩，列舉資料列的可用性與驅動程式的行為。 連同類型資訊，請使用下列的位元遮罩：  
  
 SQL_BRC_ROLLED_UP = 連續的 INSERT、 DELETE 或 UPDATE 陳述式會彙總成一個資料列計數。 如果未設定此位元，就有一個資料列計數可供每個陳述式。  
  
 SQL_BRC_PROCEDURES = 資料列計數，如果任何項目，就可以使用預存程序中執行批次。 如果有資料列計數，它們可以復原或個別，根據提供的 SQL_BRC_ROLLED_UP 位元。  
  
 SQL_BRC_EXPLICIT = 資料列計數，如果任何項目，可用來直接呼叫批次執行時**SQLExecute**或**SQLExecDirect**。 如果有資料列計數，它們可以復原或個別，根據提供的 SQL_BRC_ROLLED_UP 位元。  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉批次的驅動程式的支援。 下列的位元遮罩用來判斷支援層級：  
  
 SQL_BS_SELECT_EXPLICIT = 驅動程式支援明確的批次可以有結果集產生陳述式。  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 驅動程式支援明確的批次可以有資料列計數產生陳述式。  
  
 SQL_BS_SELECT_PROC = 的驅動程式支援明確程序可以有結果集產生陳述式。  
  
 SQL_BS_ROW_COUNT_PROC = 的驅動程式支援明確程序可以有資料列計數產生陳述式。  
  
 SQL_BOOKMARK_PERSISTENCE (ODBC 2.0)  
 SQLUINTEGER 位元遮罩列舉保存書籤的作業。  
  
 下列的位元遮罩可與旗標一起使用，以判斷保存選項的書籤：  
  
 SQL_BP_CLOSE = 書籤是有效的應用程式呼叫之後**SQLFreeStmt** SQL_CLOSE 選項時，或**SQLCloseCursor**關閉與陳述式相關聯的游標。  
  
 SQL_BP_DELETE = 書籤的資料列為有效之後已刪除該資料列。  
  
 SQL_BP_DROP = 書籤是有效的應用程式呼叫之後**SQLFreeHandle**與*HandleType*卸除陳述式利用 SQL_HANDLE_STMT。  
  
 SQL_BP_TRANSACTION = 書籤是有效的應用程式會認可或回復交易之後。  
  
 SQL_BP_UPDATE = 書籤的資料列是有效之後該資料列中的任何資料行已更新，包括索引鍵資料行。  
  
 SQL_BP_OTHER_HSTMT = 與一個相關聯的書籤陳述式可以搭配另一個陳述式。 除非指定 SQL_BP_CLOSE 或 SQL_BP_DROP，則必須在開啟第一個陳述式資料指標。  
  
 SQL_CATALOG_LOCATION (ODBC 2.0)  
 SQLUSMALLINT 值，指出中限定的資料表名稱的目錄位置：  
  
 SQL_CL_STARTSQL_CL_END  
  
 例如，Xbase 驅動程式傳回 SQL_CL_START，因為目錄 (catalog) 名稱是資料表名稱，如同 \EMPDATA\EMP 的開頭。DBF。 ORACLE 伺服器驅動程式會傳回 SQL_CL_END，因為類別目錄會在資料表名稱結尾為ADMIN.EMP@EMPDATA。  
  
 SQL 92 完整的層級標準驅動程式一定會傳回 SQL_CL_START。 如果目錄不支援的資料來源，則會傳回值為 0。 若要判斷是否支援目錄，應用程式呼叫**SQLGetInfo** SQL_CATALOG_NAME 資訊類型。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_QUALIFIER_LOCATION。  
  
 SQL_CATALOG_NAME (ODBC 3.0)  
 字元字串:"Y"(如果伺服器支援類別目錄的名稱或"N"如果不存在。  
  
 SQL 92 完整的層級標準驅動程式一定會傳回"Y"。  
  
 SQL_CATALOG_NAME_SEPARATOR ODBC (1.0)  
 字元字串： 資料來源中定義的類別目錄名稱與之後或之前的限定的名稱項目之間的分隔符號的字元。  
  
 如果目錄不支援的資料來源，則會傳回空字串。 若要判斷是否支援目錄，應用程式呼叫**SQLGetInfo** SQL_CATALOG_NAME 資訊類型。 SQL 92 完整的層級標準驅動程式一律會傳回 「。 」。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_QUALIFIER_NAME_SEPARATOR。  
  
 SQL_CATALOG_TERM ODBC (1.0)  
 類別目錄使用; 的資料來源供應商的名稱的字元字串例如，「 資料庫 」 或者 「 目錄 」。 此字串可以在上方、 下方，或混合大小寫。  
  
 如果目錄不支援的資料來源，則會傳回空字串。 若要判斷是否支援目錄，應用程式呼叫**SQLGetInfo** SQL_CATALOG_NAME 資訊類型。 SQL 92 完整的層級標準驅動程式一定會傳回 「 目錄 」。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_QUALIFIER_TERM。  
  
 SQL_CATALOG_USAGE (ODBC 2.0)  
 SQLUINTEGER 位元遮罩列舉可以在其中使用的類別目錄的陳述式。  
  
 下列的位元遮罩用來決定要在其中使用的類別目錄：  
  
 SQL_CU_DML_STATEMENTS = 目錄都支援所有的資料操作語言陳述式：**選取**，**插入**，**更新**，**刪除**，而且如果支援，**選取更新**和定位 update 和 delete 陳述式。  
  
 SQL_CU_PROCEDURE_INVOCATION = 目錄支援 ODBC 程序引動過程陳述式中。  
  
 SQL_CU_TABLE_DEFINITION = 目錄都支援所有的資料表定義陳述式： **CREATE TABLE**， **CREATE VIEW**， **ALTER TABLE**，**卸除的資料表**，和**卸除檢視**。  
  
 SQL_CU_INDEX_DEFINITION = 目錄都支援所有的索引定義陳述式： **CREATE INDEX**和**DROP INDEX**。  
  
 SQL_CU_PRIVILEGE_DEFINITION = 目錄都支援所有的權限定義陳述式： **GRANT**和**撤銷**。  
  
 如果目錄不支援的資料來源，則會傳回值為 0。 若要判斷是否支援目錄，應用程式呼叫**SQLGetInfo** SQL_CATALOG_NAME 資訊類型。 SQL 92 完整的層級標準驅動程式一定會傳回所有這些位元組的位元遮罩。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_QUALIFIER_USAGE。  
  
 SQL_COLLATION_SEQ (ODBC 3.0)  
 定序順序的名稱。 這是字元字串，表示此伺服器的預設字元集的預設定序的名稱 (例如，' ISO 8859-1' 或 EBCDIC)。 如果這是未知，則會傳回空字串。 SQL 92 完整的層級標準驅動程式一定會傳回非空白字串。  
  
 SQL_COLUMN_ALIAS (ODBC 2.0)  
 字元字串:"Y"(如果資料來源支援的資料行別名。否則，"N"。  
  
 資料行別名是可以使用 AS 子句來指定選取清單中的資料行的替代名稱。 SQL 92 項目層級標準驅動程式一定會傳回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR ODBC (1.0)  
 SQLUSMALLINT 值，指出資料來源如何處理 NULL 的串連值含有非 NULL 值的字元資料類型資料行的字元資料類型資料行：  
  
 連接 = 結果為 NULL 值。  
  
 SQL_CB_NON_NULL = 結果為非 NULL 值的資料行或資料行的串連。  
  
 SQL 92 項目層級標準驅動程式一定會傳回連接。  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BIT SQL_CONVERT_CHAR SQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR (ODBC 1.0)  
 SQLUINTEGER 位元遮罩。 位元遮罩表示與資料來源所支援的轉換**轉換**純量函式中名為之型別的資料*資訊類型*。 如果位元遮罩等於零，資料來源不支援從資料的具名型別，包括轉換成相同的資料類型的任何轉換。  
  
 例如，若要判斷資料來源是否支援 SQL_INTEGER 資料轉換成 SQL_BIGINT 資料類型，應用程式呼叫**SQLGetInfo**與*資訊類型*SQL_CONVERT_INTEGER。 應用程式執行**AND** SQL_CVT_BIGINT 傳回位元遮罩與作業。 如果產生的值不是零，則支援轉換。  
  
 下列的位元遮罩用來判斷支援的轉換：  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0) SQL_CVT_DECIMAL (ODBC 1.0) SQL_CVT_DOUBLE (ODBC 1.0) SQL_CVT_FLOAT (ODBC 1.0) SQL_CVT_INTEGER (ODBC 1.0) SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) SQL_CVT_LONGVARBINARY (ODBC 1.0) SQL_CVT_LONGVARCHAR (ODBC 1.0) SQL_CVT_NUMERIC (ODBC 1.0) SQL_CVT_REAL ODBC 1.0) SQL_CVT_SMALLINT (ODBC 1.0) SQL_CVT_TIME (ODBC 1.0) SQL_CVT_時間戳記 (ODBC 1.0) SQL_CVT_TINYINT (ODBC 1.0) SQL_CVT_VARBINARY (ODBC 1.0) SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS ODBC (1.0)  
 SQLUINTEGER 位元遮罩列舉驅動程式和相關聯的資料來源所支援的純量的轉換函式。  
  
 下列的位元遮罩用來判斷支援的轉換函數：  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME ODBC (1.0)  
 指出是否支援資料表相互關聯名稱 SQLUSMALLINT 值：  
  
 SQL_CN_NONE = 相互關聯名稱不受支援。  
  
 SQL_CN_DIFFERENT = 相互關聯名稱支援，但必須與它們所代表的資料表的名稱不同。  
  
 SQL_CN_ANY = 相互關聯名稱支援，而且可以是任何有效的使用者定義名稱。  
  
 SQL 92 項目層級標準驅動程式一定會傳回 SQL_CN_ANY。  
  
 SQL_CREATE_ASSERTION (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**建立判斷提示**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CA_CREATE_ASSERTION  
  
 下列位元會指定支援的條件約束屬性是否支援明確指定條件約束屬性的能力 （請參閱 SQL_ALTER_TABLE 和 SQL_CREATE_TABLE 的資訊類型）：  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL 92 完整的層級標準驅動程式一定會傳回所有的這些選項的支援。 傳回值為"0"表示**建立判斷提示**不支援陳述式。  
  
 SQL_CREATE_CHARACTER_SET (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**建立字元集**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL 92 完整的層級標準驅動程式一定會傳回所有的這些選項的支援。 傳回值為"0"表示**建立字元集**不支援陳述式。  
  
 SQL_CREATE_COLLATION (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**建立定序**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CCOL_CREATE_COLLATION  
  
 支援 SQL 92 完整的層級標準驅動程式一定會傳回此選項。 傳回值為"0"表示**建立定序**不支援陳述式。  
  
 SQL_CREATE_DOMAIN (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**建立網域**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CDO_CREATE_DOMAIN = 建立網域支援陳述式 （中繼層級）。  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION =\<條件約束名稱定義 > 支援命名 網域條件約束 （中介層級）。  
  
 下列的位元會指定能夠建立資料行條件約束： SQL_CDO_DEFAULT = 支援指定網域條件約束 （中繼層級） SQL_CDO_CONSTRAINT = 支援指定網域的預設值 （中繼層級） SQL_CDO_COLLATION =指定網域的定序支援 （完整層級）  
  
 下列的位元會指定支援的條件約束屬性指定網域條件約束是否支援 （設定 SQL_CDO_DEFAULT）：  
  
 （完整的層級） SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE （完整的層級） SQL_CDO_CONSTRAINT_DEFERRABLE （完整的層級） SQL_CDO_CONSTRAINT_NON_DEFERRABLE （完整的層級）  
  
 傳回值為"0"表示**建立網域**不支援陳述式。  
  
 SQL_CREATE_SCHEMA (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**CREATE SCHEMA**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL 92 中繼層級標準驅動程式一定會傳回上述 SQL_CS_CREATE_SCHEMA 和 SQL_CS_AUTHORIZATION 選項支援。 此外，這些也必須支援在 sql-92 項目層級，但不是一定為 SQL 陳述式。 SQL 92 完整的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_CREATE_TABLE (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**CREATE TABLE**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CT_CREATE_TABLE = CREATE TABLE 陳述式支援。 （項目層級）  
  
 SQL_CT_TABLE_CONSTRAINT = 支援指定資料表條件約束 （FIPS 過渡期的層級）  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION =\<條件約束名稱定義 > 子句命名資料行和資料表條件約束 （中介層級） 的支援  
  
 下列的位元會指定建立暫存資料表的能力：  
  
 SQL_CT_COMMIT_PRESERVE = 已刪除資料列會保留在認可。 （完整的層級）SQL_CT_COMMIT_DELETE = 已刪除上認可的資料列都會被刪除。 （完整的層級）SQL_CT_GLOBAL_TEMPORARY = 全域可以建立暫存資料表。 （完整的層級）SQL_CT_LOCAL_TEMPORARY = 本機可以建立暫存資料表。 （完整的層級）  
  
 下列的位元會指定建立資料行條件約束的能力：  
  
 SQL_CT_COLUMN_CONSTRAINT = 支援指定資料行條件約束 （FIPS 過渡期的層級） SQL_CT_COLUMN_DEFAULT = 支援指定資料行的預設值 （FIPS 過渡期的層級） SQL_CT_COLUMN_COLLATION = 指定資料行定序支援 （完整的層級）  
  
 下列的位元會指定支援的條件約束屬性，指定資料行或資料表條件約束支援：  
  
 （完整的層級） SQL_CT_CONSTRAINT_INITIALLY_DEFERRED SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE （完整的層級） SQL_CT_CONSTRAINT_DEFERRABLE （完整的層級） SQL_CT_CONSTRAINT_NON_DEFERRABLE （完整的層級）  
  
 SQL_CREATE_TRANSLATION (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**建立轉譯**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 支援以 sql-92 完整的層級 – 一致驅動程式一定會傳回這些選項。 傳回值為"0"表示**建立轉譯**不支援陳述式。  
  
 SQL_CREATE_VIEW (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**CREATE VIEW**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 傳回值為"0"表示**CREATE VIEW**不支援陳述式。  
  
 SQL 92 項目層級標準驅動程式一定會傳回上述 SQL_CV_CREATE_VIEW 和 SQL_CV_CHECK_OPTION 選項支援。  
  
 SQL 92 完整的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR ODBC (1.0)  
 SQLUSMALLINT 值，指出如何**認可**作業會影響資料指標和備妥的陳述式中的資料來源 （資料來源認可交易時的行為）。  
  
 這個屬性的值會反映目前狀態的下一個設定： SQL_COPT_SS_PRESERVE_CURSORS。  
  
 SQL_CB_DELETE = 關閉資料指標，並刪除已備妥的陳述式。 若要使用游標同樣地，應用程式必須 reprepare 並重新執行陳述式。  
  
 SQL_CB_CLOSE = 關閉資料指標。 已備妥的陳述式的應用程式可以呼叫**SQLExecute**陳述式，而不需呼叫**SQLPrepare**一次。 SQL ODBC 驅動程式的預設值是 SQL_CB_CLOSE。 這表示當您將交易認可 SQL ODBC 驅動程式將會關閉您的資料指標。  
  
 SQL_CB_PRESERVE 如常 = 保留相同的位置中的資料指標**認可**作業。 應用程式可以繼續來提取資料，或是關閉資料指標，然後重新執行陳述式，而不重新準備。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR ODBC (1.0)  
 SQLUSMALLINT 值，指出如何**復原**作業會影響資料指標和資料來源中的已備妥陳述式：  
  
 SQL_CB_DELETE = 關閉資料指標，並刪除已備妥的陳述式。 若要使用游標同樣地，應用程式必須 reprepare 並重新執行陳述式。  
  
 SQL_CB_CLOSE = 關閉資料指標。 已備妥的陳述式的應用程式可以呼叫**SQLExecute**陳述式，而不需呼叫**SQLPrepare**一次。  
  
 SQL_CB_PRESERVE 如常 = 保留相同的位置中的資料指標**復原**作業。 應用程式可以繼續來提取資料，或是關閉資料指標，然後重新執行不含 repreparing 它的陳述式。  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 SQLUINTEGER 值，指出資料指標的敏感度的支援：  
  
 SQL_INSENSITIVE = 在相同交易內的任何其他資料指標所所有資料指標陳述式控制代碼顯示結果集而不會反映對其所做的任何變更。  
  
 SQL_UNSPECIFIED = 是未指定是否在陳述式控制代碼上的資料指標顯示的結果集，在相同交易內的另一個資料指標所做的變更。 資料指標陳述式控制代碼上的進行可能會看見無、 某些或所有這類變更。  
  
 SQL_SENSITIVE = 資料指標是在相同交易內的其他資料指標所做的變更影響。  
  
 支援的 SQL 92 項目層級標準驅動程式一定會傳回 SQL_UNSPECIFIED 選項。  
  
 支援以 sql-92 完整的層級 – 一致驅動程式一定會傳回 SQL_INSENSITIVE 選項。  
  
 SQL_DATA_SOURCE_NAME ODBC (1.0)  
 在連接期間所使用的資料來源名稱字串的字元字串。 如果應用程式呼叫**SQLConnect**，這是值*szDSN*引數。 如果應用程式呼叫**SQLDriverConnect**或**SQLBrowseConnect**，這是在連接字串傳遞至驅動程式中使用 DSN 關鍵字的值。 如果連接字串未包含**DSN**關鍵字 (例如包含時**驅動程式**關鍵字)，這是空字串。  
  
 SQL_DATA_SOURCE_READ_ONLY ODBC (1.0)  
 字元字串。 "Y"如果是其他資料來源設定為 READ ONLY 模式中，"N"。  
  
 這項特性僅屬於資料來源本身。它不是可讓您存取資料來源驅動程式的特性。 讀取/寫入的驅動程式可以搭配是唯讀的資料來源。 如果驅動程式是唯讀的它所有的資料來源必須是唯讀，必須傳回 SQL_DATA_SOURCE_READ_ONLY。  
  
 SQL_DATABASE_NAME ODBC (1.0)  
 在使用中，目前的資料庫名稱的字元字串，如果資料來源會定義稱為 「 資料庫 」 的具名的物件。  
  
> [!NOTE]  
>  在 ODBC 3*.x*，傳回的值，這個*資訊類型*也可以藉由呼叫傳回**SQLGetConnectAttr**與*屬性*SQL_ATTR_CURRENT_CATALOG 的引數。  
  
 SQL_DATETIME_LITERALS (ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉資料來源所支援的 SQL 92 datetime 常值。 請注意，這些在 sql-92 規格中所列的日期時間常值而且是分開定義由 ODBC datetime 常值逸出子句。 如需有關 ODBC datetime 常值的逸出子句的詳細資訊，請參閱[日期、 時間和時間戳記常值](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 FIPS 過渡期的層級標準驅動程式一定會傳回"1"的值在下列清單中的位元的位元遮罩。 值為"0"，不支援以 sql-92 datetime 常值的表示。  
  
 下列的位元遮罩用來判斷支援哪些常值：  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME ODBC (1.0)  
 驅動程式所存取的 DBMS 產品名稱的字元字串。  
  
 SQL_DBMS_VER ODBC (1.0)  
 字元字串，表示驅動程式所存取的 DBMS 產品版本。 版本是表單的 # #。 # #。 # # #，其中前兩個數字的主要版本、 下面兩個的數字是否為次要版本，而且最後四位數字的發行版本。 驅動程式必須呈現在這種形式的 DBMS 產品版本，但也可以附加 DBMS 特定產品版本。 例如，"04.01.0000 Rdb 4.1"。  
  
 SQL_DDL_INDEX (ODBC 3.0)  
 SQLUINTEGER 值，這個值表示支援建立和卸除的索引：  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION ODBC (1.0)  
 SQLUINTEGER 值，指出預設交易隔離等級支援的驅動程式或資料來源或如果資料來源不支援交易。 下列詞彙用來定義交易隔離等級：  
  
 **中途讀取**交易 1 變更資料列。 交易 2 會在交易 1 認可變更之前，讀取已變更的資料列。 如果交易 1 復原變更，交易 2 會有讀取會被視為已不存在的資料列。  
  
 **不可重複讀取**交易 1 中讀取的資料列。 交易 2 會更新或刪除該資料列，並認可此變更。 如果交易 1 嘗試重新讀取資料列，將會收到不同的資料列的值，或探索已刪除資料列。  
  
 **虛設項目**交易 1 讀取一組符合搜尋條件的資料列。 交易 2 會產生一或多個資料列 （透過插入或更新），符合搜尋條件。 如果交易 1 reexecutes 讀取資料列的陳述式，它會接收一組不同的資料列。  
  
 如果資料來源支援交易，驅動程式會傳回下列位元遮罩的其中一個：  
  
 SQL_TXN_READ_UNCOMMITTED = 中途讀取、 不可重複讀取和虛設項目。  
  
 SQL_TXN_READ_COMMITTED = 中途讀取，不能進行。 可能會有不可重複讀取和虛設項目。  
  
 SQL_TXN_REPEATABLE_READ = 中途讀取和不可重複讀取不可行。 可能會有虛設項目。  
  
 SQL_TXN_SERIALIZABLE = 交易是可序列化。 可序列化的交易不允許中途讀取、 不可重複讀取或虛設項目。  
  
 SQL_DESCRIBE_PARAMETER (ODBC 3.0)  
 字元字串:"Y"(如果可以描述參數;"N"，如果不是。  
  
 SQL 92 完整的層級標準驅動程式通常會傳回"Y"，因為它會支援**描述輸入**陳述式。 因為這並未直接指定基礎 SQL 支援，不過，描述參數可能不支援，即使是在 sql-92 完整的層級標準驅動程式。  
  
 SQL_DM_VER (ODBC 3.0)  
 驅動程式管理員的版本字串的字元字串。 版本是表單的 # #。 # #。 # # #。 # # #，其中：  
  
 兩個數字的第一個集合，主要的 ODBC 版本中做為常數 SQL_SPEC_MAJOR 所指定。  
  
 兩個數字的第二個集合，次要的 ODBC 版本中做為常數 SQL_SPEC_MINOR 所指定。  
  
 四位數字的第三組是驅動程式管理員主要組建編號。  
  
 四位數的上一組是驅動程式管理員次要組建數目。  
  
 Windows 7 驅動程式管理員版本是 03.80。 Windows 8 的驅動程式管理員版本是 03.81。  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 SQLUINTEGER 值，指出如果驅動程式支援可感知驅動程式共用。 (如需詳細資訊，請參閱[感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE 表示驅動程式可支援共用的可感知驅動程式的機制。  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 表示驅動程式不支援可感知驅動程式集區的機制。  
  
 不需要實作 SQL_DRIVER_AWARE_POOLING_SUPPORTED 驅動程式和驅動程式管理員不支援的驅動程式傳回值。  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV ODBC (1.0)  
 SQLULEN 值、 驅動程式的環境控制代碼或連接控制代碼引數所決定*資訊類型*。  
  
 這些資訊類型會實作由驅動程式管理員時。  
  
 SQL_DRIVER_HDESC (ODBC 3.0)  
 SQLULEN 值，取決於驅動程式管理員的描述項處理，必須傳遞在輸入中的驅動程式的描述項控制代碼\* *InfoValuePtr*從應用程式。 在此情況下， *InfoValuePtr*是這兩個的輸入和輸出引數。 輸入的描述元的控制代碼傳\* *InfoValuePtr*必須具有已明確或隱含地在配置*ConnectionHandle*。  
  
 應用程式應該複製一份驅動程式管理員的描述元之前它會呼叫處理**SQLGetInfo**使用此資訊類型，並確定此控制代碼不會覆寫輸出上。  
  
 此資訊類型會實作由驅動程式管理員時。  
  
 SQL_DRIVER_HLIB (ODBC 2.0)  
 為 SQLULEN 的值， *hinst*載入程式庫傳回給驅動程式管理員在 Microsoft Windows 作業系統或它的對等，另一個作業系統上的驅動程式 DLL 載入它。 僅針對指定的呼叫中的連接控制代碼的控制代碼無效**SQLGetInfo**。  
  
 此資訊類型會實作由驅動程式管理員時。  
  
 SQL_DRIVER_HSTMT ODBC (1.0)  
 SQLULEN 值，取決於驅動程式管理員陳述式控制代碼，必須傳遞在輸入中的驅動程式的陳述式控制代碼\* *InfoValuePtr*從應用程式。 在此情況下， *InfoValuePtr*是輸入和輸出引數。 輸入陳述式控制代碼傳\* *InfoValuePtr*必須配置的引數*ConnectionHandle*。  
  
 應用程式應該複製一份驅動程式管理員的陳述式之前它會呼叫處理**SQLGetInfo**使用此資訊類型，以確保控制代碼不會覆寫輸出上。  
  
 此資訊類型會實作由驅動程式管理員時。  
  
 SQL_DRIVER_NAME ODBC (1.0)  
 具有驅動程式用來存取資料來源的檔案名稱的字元字串。  
  
 SQL_DRIVER_ODBC_VER (ODBC 2.0)  
 ODBC 驅動程式支援的版本字串的字元字串。 版本是表單的 # #。 # #，其中前兩個數字的主要版本，而下面兩個位數的次要版本。 SQL_SPEC_MAJOR 和 SQL_SPEC_MINOR 定義主要和次要版本號碼。 如需本手冊中所述的 ODBC 版本，這些是 3，0，且驅動程式應該會傳回"03.00"。  
  
 ODBC 驅動程式管理員不會修改 SQLGetInfo(SQL_DRIVER_ODBC_VER) 維護現有應用程式的回溯相容性的傳回值。 驅動程式會指定將傳回的值。 不過，支援 C 資料類型擴充性的驅動程式必須傳回 3.8 （或更新版本） 時，應用程式呼叫**SQLSetEnvAttr** SQL_ATTR_ODBC_VERSION 設 3.8。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 SQL_DRIVER_VER ODBC (1.0)  
 具有驅動程式版本和 （選擇性） 描述的驅動程式的字元字串。 最少的版本是表單的 # #。 # #。 # # #，其中前兩個數字的主要版本、 下面兩個的數字是否為次要版本，而且最後四位數字的發行版本。  
  
 SQL_DROP_ASSERTION (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**卸除的判斷提示**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DA_DROP_ASSERTION  
  
 支援 SQL 92 完整的層級標準驅動程式一定會傳回此選項。  
  
 SQL_DROP_CHARACTER_SET (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**卸除字元集**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 支援 SQL 92 完整的層級標準驅動程式一定會傳回此選項。  
  
 SQL_DROP_COLLATION (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**卸除的定序**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DC_DROP_COLLATION  
  
 支援 SQL 92 完整的層級標準驅動程式一定會傳回此選項。  
  
 SQL_DROP_DOMAIN (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**卸除網域**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL 92 中繼層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_DROP_SCHEMA (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**DROP SCHEMA**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL 92 中繼層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_DROP_TABLE (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**DROP TABLE**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 過渡期的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_DROP_TRANSLATION (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**卸除轉譯**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DTR_DROP_TRANSLATION  
  
 支援 SQL 92 完整的層級標準驅動程式一定會傳回此選項。  
  
 SQL_DROP_VIEW (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**DROP VIEW**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 過渡期的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 SQLUINTEGER 位元遮罩描述驅動程式所支援的動態資料指標的屬性。 此位元遮罩包含的第一個屬性; 子集第二個子集，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA1_NEXT = A *Sqlfetchscroll*支援 SQL_FETCH_NEXT 的引數的呼叫中**SQLFetchScroll**當資料指標是動態資料指標。  
  
 SQL_CA1_ABSOLUTE = *Sqlfetchscroll* SQL_FETCH_FIRST、 SQL_FETCH_LAST 和 SQL_FETCH_ABSOLUTE 引數的呼叫中支援**SQLFetchScroll**當資料指標是動態資料指標。 （將會提取資料列集是獨立於目前的游標位置）。  
  
 SQL_CA1_RELATIVE = *Sqlfetchscroll* SQL_FETCH_PRIOR 和 sql_fetch_relative，但引數的呼叫中支援**SQLFetchScroll**當資料指標是動態資料指標。 （將會提取資料列集取決於目前的游標位置。 請注意，這分開 SQL_FETCH_NEXT 因為只有 SQL_FETCH_NEXT 支援順向資料指標中）。  
  
 SQL_CA1_BOOKMARK = A *Sqlfetchscroll*要使用 sql_fetch_bookmark 的引數的呼叫中，支援**SQLFetchScroll**當資料指標是動態資料指標。  
  
 SQL_CA1_LOCK_EXCLUSIVE = A *LockType* SQL_LOCK_EXCLUSIVE 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_LOCK_NO_CHANGE = A *LockType* SQL_LOCK_NO_CHANGE 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_LOCK_UNLOCK = A *LockType* SQL_LOCK_UNLOCK 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_POS_POSITION =*作業*SQL_POSITION 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_POS_UPDATE =*作業*SQL_UPDATE 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_POS_DELETE =*作業*SQL_DELETE 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_POS_REFRESH =*作業*SQL_REFRESH 引數的呼叫中支援**SQLSetPos**當資料指標是動態資料指標。  
  
 SQL_CA1_POSITIONED_UPDATE = 更新其中目前的 SQL 陳述式時資料指標是動態資料指標支援。 （SQL 92 項目層級標準驅動程式一定會傳回這個選項的支援。）  
  
 SQL_CA1_POSITIONED_DELETE = 刪除其中目前的 SQL 陳述式時資料指標是動態資料指標支援。 （SQL 92 項目層級標準驅動程式一定會傳回這個選項的支援。）  
  
 SQL_CA1_SELECT_FOR_UPDATE = 有選取時，資料指標是動態資料指標支援 UPDATE SQL 陳述式。 （SQL 92 項目層級標準驅動程式一定會傳回這個選項的支援。）  
  
 SQL_CA1_BULK_ADD =*作業*SQL_ADD 引數的呼叫中支援**SQLBulkOperations**當資料指標是動態資料指標。  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK =*作業*SQL_UPDATE_BY_BOOKMARK 引數的呼叫中支援**SQLBulkOperations**當資料指標是動態資料指標。  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK =*作業*SQL_DELETE_BY_BOOKMARK 引數的呼叫中支援**SQLBulkOperations**當資料指標是動態資料指標。  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK =*作業*SQL_FETCH_BY_BOOKMARK 引數的呼叫中支援**SQLBulkOperations**當資料指標是動態資料指標。  
  
 SQL 92 中繼層級標準驅動程式將通常傳回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項的支援，因為它支援透過內嵌擷取 SQL 陳述式的可捲動資料指標。 因為這不會直接判斷基礎的 SQL 支援，不過，可捲動資料指標可能不是，即使 sql-92 中繼層級標準驅動程式支援。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 SQLUINTEGER 位元遮罩描述驅動程式所支援的動態資料指標的屬性。 此位元遮罩包含屬性; 第二個的子集第一個子集，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 的唯讀動態資料指標，以允許任何更新，才支援。 （陳述式屬性 sql_attr_concurrency 設定可以是 SQL_CONCUR_READ_ONLY 動態資料指標）。  
  
 SQL_CA2_LOCK_CONCURRENCY = 動態資料指標使用的最低層級的鎖定足以確定支援，可以更新資料列。 （陳述式屬性 sql_attr_concurrency 設定可以是 SQL_CONCUR_LOCK 動態資料指標）。這些鎖定必須一致使用 SQL_ATTR_TXN_ISOLATION 連接屬性所設定的交易隔離等級。  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 動態資料指標使用開放式並行存取控制項比較的資料列版本，都支援。 （陳述式屬性 sql_attr_concurrency 設定可以是 SQL_CONCUR_ROWVER 動態資料指標）。  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 動態資料指標使用開放式並行存取控制項的比較值，都支援。 （陳述式屬性 sql_attr_concurrency 設定可以是 SQL_CONCUR_VALUES 動態資料指標）。  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = 加入資料列會顯示動態資料指標。這些資料列可以捲動資料指標。 （其中的這些資料列會加入到資料指標是驅動程式而定）。  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 已刪除資料列便無法再使用動態資料指標，並不會讓結果集;"孔 」動態資料指標捲動從已刪除的資料列之後，就無法返回該資料列。  
  
 SQL_CA2_SENSITIVITY_UPDATES = 更新資料列會顯示動態資料指標。如果動態資料指標從捲動，並傳回更新的資料列，資料指標所傳回的資料是更新的資料，而不是原始資料。  
  
 SQL_CA2_MAX_ROWS_SELECT = SQL_ATTR_MAX_ROWS 陳述式屬性會影響**選取**時資料指標是動態資料指標的陳述式。  
  
 SQL_CA2_MAX_ROWS_INSERT = SQL_ATTR_MAX_ROWS 陳述式屬性會影響**插入**時資料指標是動態資料指標的陳述式。  
  
 SQL_CA2_MAX_ROWS_DELETE = SQL_ATTR_MAX_ROWS 陳述式屬性會影響**刪除**時資料指標是動態資料指標的陳述式。  
  
 SQL_CA2_MAX_ROWS_UPDATE = SQL_ATTR_MAX_ROWS 陳述式屬性會影響**更新**時資料指標是動態資料指標的陳述式。  
  
 SQL_CA2_MAX_ROWS_CATALOG = SQL_ATTR_MAX_ROWS 陳述式屬性會影響**目錄**時資料指標是動態資料指標結果集。  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = SQL_ATTR_MAX_ROWS 陳述式屬性會影響**選取**，**插入**，**刪除**，和**更新**陳述式，和**目錄**結果集，資料指標的動態資料指標時。  
  
 SQL_CA2_CRC_EXACT = 的確切資料列計數時，可以使用 SQL_DIAG_CURSOR_ROW_COUNT 診斷欄位中資料指標是動態資料指標。  
  
 SQL_CA2_CRC_APPROXIMATE = 近似資料列計數時，可以使用 SQL_DIAG_CURSOR_ROW_COUNT 診斷欄位中資料指標是動態資料指標。  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = 驅動程式並不保證模擬定位更新或 delete 陳述式將會影響只有一個資料列，當資料指標是動態資料指標。應用程式的責任，若要確保這它。 (如果陳述式會影響多個資料列， **SQLExecute**或**SQLExecDirect**傳回 SQLSTATE 01001 [資料指標作業衝突]。)若要設定此行為，應用程式會呼叫**SQLSetStmtAttr**與 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 SQL_SC_NON_UNIQUE。  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = 驅動程式會嘗試以保證，模擬定位的 update 或 delete 陳述式會影響只有一個資料列資料指標的動態資料指標時。 驅動程式一律會執行這類陳述式，即使它們可能會影響多個資料列，例如當沒有唯一索引鍵。 (如果陳述式會影響多個資料列， **SQLExecute**或**SQLExecDirect**傳回 SQLSTATE 01001 [資料指標作業衝突]。)若要設定此行為，應用程式會呼叫**SQLSetStmtAttr**與 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 SQL_SC_TRY_UNIQUE。  
  
 SQL_CA2_SIMULATE_UNIQUE = 驅動程式模擬的保證定位的 update 或 delete 陳述式將會影響只有一個資料列，資料指標的動態資料指標時。 如果驅動程式指定的陳述式中，無法保證此**SQLExecDirect**或**SQLPrepare**傳回 SQLSTATE 01001 （資料指標作業衝突）。 若要設定此行為，應用程式會呼叫**SQLSetStmtAttr**與 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 SQL_SC_UNIQUE。  
  
 SQL_EXPRESSIONS_IN_ORDERBY ODBC (1.0)  
 字元字串:"Y"(如果資料來源支援的運算式中**ORDER BY**清單;"N"如果不存在。  
  
 SQL_FILE_USAGE (ODBC 2.0)  
 SQLUSMALLINT 值，指出如何將單一層驅動程式直接處理資料來源中的檔案：  
  
 SQL_FILE_NOT_SUPPORTED = 驅動程式不是單層驅動程式。 例如，ORACLE 驅動程式為兩層式驅動程式。  
  
 SQL_FILE_TABLE = 資料來源中的單一層驅動程式會視為檔案，做為資料表。 比方說，Xbase 驅動程式會將每個 Xbase 檔案視為資料表中。  
  
 SQL_FILE_CATALOG = 單層驅動程式將檔案資料來源為類別目錄中的。 例如，Microsoft Access 驅動程式會將每個 Microsoft Access 檔案視為完整的資料庫。  
  
 應用程式可以將此來決定使用者如何選取資料。 例如，Xbase 使用者通常將資料儲存在檔案中，而 ORACLE 和 Microsoft Access 的使用者通常將資料視為儲存在資料表中。  
  
 當使用者選取 Xbase 資料來源時，應用程式無法顯示 Windows**開啟舊檔**通用對話方塊中，當使用者選取 Microsoft Access 或 ORACLE 資料來源，則應用程式可以顯示自訂**選取資料表** 對話方塊。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 SQLUINTEGER 位元遮罩描述驅動程式支援順向資料指標的屬性。 此位元遮罩包含的第一個屬性; 子集第二個子集，請參閱 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 如需這些位元遮罩的描述，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （並以取代"順向資料指標 」，在描述中的 「 動態資料指標 」）。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 SQLUINTEGER 位元遮罩描述驅動程式支援順向資料指標的屬性。 此位元遮罩包含屬性; 第二個的子集第一個子集，請參閱 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 如需這些位元遮罩的描述，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 （並以取代"順向資料指標 」，在描述中的 「 動態資料指標 」）。  
  
 SQL_GETDATA_EXTENSIONS (ODBC 2.0)  
 列舉延伸模組 SQLUINTEGER 位元遮罩**SQLGetData**。  
  
 下列的位元遮罩旗標以及用來判斷何種常見的延伸模組，此驅動程式支援的**SQLGetData**:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData**可以針對任何未繫結的資料行，包括上次繫結資料行之前呼叫。 請注意，必須呼叫資料行的遞增資料行數目，除非 SQL_GD_ANY_ORDER 也會傳回順序。  
  
 SQL_GD_ANY_ORDER = **SQLGetData**可以針對未繫結的資料行，以任何順序呼叫。 請注意， **SQLGetData**上次繫結資料行，除非也會傳回 SQL_GD_ANY_COLUMN 後才能呼叫只對資料行。  
  
 SQL_GD_BLOCK = **SQLGetData**後，使用該資料列定位可以呼叫未繫結資料行 （其中資料列集大小大於 1） 的資料區塊中的任何資料列中**SQLSetPos**。  
  
 SQL_GD_BOUND = **SQLGetData**可以繫結的資料行解除繫結的資料行除了呼叫。 驅動程式無法傳回此值，除非它也會傳回 SQL_GD_ANY_COLUMN。  
  
 SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以呼叫以傳回輸出參數值。 如需詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
 **SQLGetData**無須傳回只能從上次繫結資料行之後, 會發生的未繫結資料行的資料會依照順序遞增資料行編號的呼叫，且不在資料列的區塊中的資料列。  
  
 如果驅動程式支援書籤 （固定長度或可變長度），就必須支援呼叫**SQLGetData**上資料行 0。 不論驅動程式傳回進行呼叫的這項支援無須**SQLGetInfo**與 SQL_GETDATA_EXTENSIONS*資訊類型*。  
  
 SQL_GROUP_BY (ODBC 2.0)  
 指定在資料行之間的關聯性的 SQLUSMALLINT 值**GROUP BY**子句和選取清單中的非彙總資料行：  
  
 SQL_GB_COLLATE = A **COLLATE**子句可以指定每個群組資料行的結尾。 (ODBC 3.0)  
  
 SQL_GB_NOT_SUPPORTED = **GROUP BY**子句不支援。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP BY**子句必須包含選取清單中的所有非彙總資料行。 它不能包含任何其他資料行。 例如，**選取部門、 MAX(SALARY) 從員工群組依部門**。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP BY**子句必須包含選取清單中的所有非彙總資料行。 它可以包含不在選取清單中的資料行。 例如，**選取部門、 MAX(SALARY) 從員工群組依部門、 年齡**。 (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = 中的資料行**GROUP BY**子句和 select 清單不相關。 選取清單中的 nongrouped，非彙總資料行的意義是資料來源而定。 例如，**選取部門、 薪資的員工群組依部門、 年齡**。 (ODBC 2.0)  
  
 支援的 SQL 92 項目層級標準驅動程式一定會傳回 SQL_GB_GROUP_BY_EQUALS_SELECT 選項。 支援以 sql-92 完整的層級 – 一致驅動程式一定會傳回 SQL_GB_COLLATE 選項。 如果不支援任何選項， **GROUP BY**子句不支援資料來源。  
  
 SQL_IDENTIFIER_CASE ODBC (1.0)  
 SQLUSMALLINT 值，如下所示：  
  
 SQL_IC_UPPER = SQL 中的識別項不區分大小寫，而且會儲存在系統目錄中的大寫。  
  
 SQL_IC_LOWER = SQL 中的識別項不區分大小寫，而且會儲存在系統目錄中的小寫。  
  
 則為 SQL_IC_SENSITIVE = SQL 中的識別碼會區分大小寫，而且會儲存在系統目錄中的混合大小寫。  
  
 SQL_IC_MIXED = SQL 中的識別項不區分大小寫，而且會儲存在系統目錄中的混合大小寫。  
  
 由於 SQL 92 中的識別項永遠不會區分大小寫，嚴格符合 sql-92 （任何層級） 的驅動程式永遠不會傳回，則為 SQL_IC_SENSITIVE 選項的支援。  
  
 SQL_IDENTIFIER_QUOTE_CHAR ODBC (1.0)  
 使用做為開始和結束分隔符號的加上引號的字元字串 （分隔） SQL 陳述式中的識別項。 （做為引數傳遞至 ODBC 函式的識別項不需要要使用引號）。如果資料來源不支援引號的識別碼，則會傳回空白。  
  
 這個字元字串也可以用於當 SQL_ATTR_METADATA_ID 「 連接 」 屬性設為 SQL_TRUE 引用目錄函式引數。  
  
 因為識別項的引號字元，以 sql-92 雙引號 （"），符合的驅動程式嚴格地以 sql-92 一定會傳回雙引號字元。  
  
 SQL_INDEX_KEYWORDS (ODBC 3.0)  
 SQLUINTEGER 位元遮罩，會列舉在 CREATE INDEX 陳述式中的驅動程式支援的關鍵字：  
  
 SQL_IK_NONE = 不支援任何關鍵字。  
  
 SQL_IK_ASC = ASC 支援關鍵字。  
  
 SQL_IK_DESC = DESC 關鍵字支援。  
  
 SQL_IK_ALL = 所有支援的關鍵字。  
  
 若要查看是否支援 CREATE INDEX 陳述式，應用程式呼叫**SQLGetInfo** SQL_DLL_INDEX 資訊類型。  
  
 SQL_INFO_SCHEMA_VIEWS (ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉 INFORMATION_SCHEMA 驅動程式支援的檢視。 在中，檢視和內容，INFORMATION_SCHEMA 是以 sql-92 定義。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷支援哪些檢視：  
  
 SQL_ISV_ASSERTIONS = 識別由指定使用者所擁有的類別目錄的判斷提示。 （完整的層級）  
  
 SQL_ISV_CHARACTER_SETS = 的識別設定類別目錄的字元可由指定使用者存取。 （中介層級）  
  
 SQL_ISV_CHECK_CONSTRAINTS = 識別檢查給定使用者所擁有的條件約束。 （中介層級）  
  
 SQL_ISV_COLLATIONS = 識別由指定使用者可以存取的類別目錄的字元定序。 （完整的層級）  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 取決於目錄中定義的網域和指定的使用者所擁有的類別目錄的識別資料行。 （中介層級）  
  
 SQL_ISV_COLUMN_PRIVILEGES = 識別保存可用或已授與指定之使用者的資料表的資料行上的權限。 （FIPS 過渡期的層級）  
  
 SQL_ISV_COLUMNS = 識別由指定使用者可以存取的永續性資料表的資料行。 （FIPS 過渡期的層級）  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = 類似 CONSTRAINT_TABLE_USAGE 檢視給定使用者所擁有的各種條件約束的識別資料行。 （中介層級）  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 識別條件約束所使用的資料表 (參考、 唯一的與判斷提示)，並指定使用者所擁有。 （中介層級）  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 識別由指定使用者可以存取的網域條件約束 （屬於類別目錄中的定義域）。 （中介層級）  
  
 SQL_ISV_DOMAINS = 定義使用者可以存取的目錄中的定義域的識別。 （中介層級）  
  
 SQL_ISV_KEY_COLUMN_USAGE = 識別資料行目錄中定義條件約束做為索引鍵所指定的使用者。 （中介層級）  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 識別由指定使用者所擁有的參考條件約束。 （中介層級）  
  
 SQL_ISV_SCHEMATA = 識別由指定使用者所擁有的結構描述。 （中介層級）  
  
 SQL_ISV_SQL_LANGUAGES = 的識別 SQL 實作所支援的 SQL 一致性層級、 選項和用語。 （中介層級）  
  
 SQL_ISV_TABLE_CONSTRAINTS = 識別由指定使用者所擁有的資料表條件約束。 （中介層級）  
  
 SQL_ISV_TABLE_PRIVILEGES = 識別保存的資料表可用或已授與指定之使用者的權限。 （FIPS 過渡期的層級）  
  
 SQL_ISV_TABLES = 保存的資料表定義可由指定使用者存取的目錄中的識別。 （FIPS 過渡期的層級）  
  
 SQL_ISV_TRANSLATIONS = 識別由指定使用者可以存取的類別目錄的字元轉譯。 （完整的層級）  
  
 SQL_ISV_USAGE_PRIVILEGES = 使用量權限可以取得或指定的使用者所擁有的目錄物件的識別。 （FIPS 過渡期的層級）  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 的識別所指定的使用者擁有所在的目錄檢視的資料行相依。 （中介層級）  
  
 SQL_ISV_VIEW_TABLE_USAGE = 的識別指定的使用者所擁有的資料表所在的目錄檢視的相依。 （中介層級）  
  
 SQL_ISV_VIEWS = 檢視的資料表定義中指定的使用者可以存取這個目錄的識別。 （FIPS 過渡期的層級）  
  
 SQL_INSERT_STATEMENT (ODBC 3.0)  
 表示支援 SQLUINTEGER 位元遮罩**插入**陳述式：  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL 92 項目層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_INTEGRITY ODBC (1.0)  
 字元字串:"Y"(如果資料來源支援 Integrity Enhancement Facility 中;"N"如果不存在。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_ODBC_SQL_OPT_IEF。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 SQLUINTEGER 描述位元遮罩的屬性索引鍵集資料指標所支援的驅動程式。 此位元遮罩包含的第一個屬性; 子集第二個子集，請參閱 SQL_KEYSET_CURSOR_ATTRIBUTES2。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 如需這些位元遮罩的描述，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （並以取代"索引鍵集驅動資料指標 」，在描述中的 「 動態資料指標 」）。  
  
 SQL 92 中繼層級標準驅動程式會通常傳回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項的支援，因為此驅動程式支援透過內嵌擷取 SQL 陳述式的可捲動資料指標。 因為這不會直接判斷基礎的 SQL 支援，不過，可捲動資料指標可能不是，即使 sql-92 中繼層級標準驅動程式支援。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 SQLUINTEGER 描述位元遮罩的屬性索引鍵集資料指標所支援的驅動程式。 此位元遮罩包含屬性; 第二個的子集第一個子集，請參閱 SQL_KEYSET_CURSOR_ATTRIBUTES1。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 如需這些位元遮罩的描述，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （並以取代"索引鍵集驅動資料指標 」，在描述中的 「 動態資料指標 」）。  
  
 SQL_KEYWORDS (ODBC 2.0)  
 字元字串，包含以逗號分隔清單的所有資料來源專用的關鍵字。 這份清單不包含特定的 ODBC 關鍵字或資料來源和 ODBC 使用的關鍵字。 此清單代表所有保留的關鍵字。互通的應用程式不應在物件名稱中使用這些字。  
  
 如需 ODBC 關鍵字的清單，請參閱[保留關鍵字](../../../odbc/reference/appendixes/reserved-keywords.md)中[附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 **#Define**值 SQL_ODBC_KEYWORDS 包含 ODBC 關鍵字的逗號分隔清單。  
  
 附錄 c: SQL 文法  
  
 SQL_LIKE_ESCAPE_CLAUSE (ODBC 2.0)  
 字元字串:"Y"(如果資料來源的百分比字元 （%），支援逸出字元和底線 (_) 字元在**像**述詞和驅動程式支援 ODBC 語法定義**像**述詞逸出字元。"N"則否。  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS (ODBC 3.0)  
 指定的驅動程式可以支援給定連接的非同步模式中的作用中並行陳述式的最大數目的 SQLUINTEGER 值。 如果沒有任何特定的限制或限制是未知的這個值會是零。  
  
 SQL_MAX_BINARY_LITERAL_LEN (ODBC 2.0)  
 指定的最大長度的 SQLUINTEGER 值 (十六進位字元組成，不含常值前置詞和後置詞所傳回的數字**SQLGetTypeInfo**) 的 SQL 陳述式中的常值的二進位檔。 例如，二進位常值 0xFFAA 長度為 4。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 SQL_MAX_CATALOG_NAME_LEN ODBC (1.0)  
 指定資料來源中的目錄名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 FIPS 完整的層級標準驅動程式會傳回至少 128。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_MAX_QUALIFIER_NAME_LEN。  
  
 SQL_MAX_CHAR_LITERAL_LEN (ODBC 2.0)  
 SQLUINTEGER 值，指定最大長度 (字元、 不含常值前置詞和後置詞所傳回的數字**SQLGetTypeInfo**) 的字元常值中的 SQL 陳述式。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 SQL_MAX_COLUMN_NAME_LEN ODBC (1.0)  
 資料來源中指定資料行名稱的長度上限 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 18。 FIPS 中繼層級標準驅動程式會傳回至少 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY (ODBC 2.0)  
 指定資料行中允許的數目上限的 SQLUSMALLINT 值**GROUP BY**子句。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 6。 FIPS 中繼層級標準驅動程式會傳回至少 15。  
  
 SQL_MAX_COLUMNS_IN_INDEX (ODBC 2.0)  
 SQLUSMALLINT 值，指定索引中允許的資料行數目上限。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY (ODBC 2.0)  
 指定資料行中允許的數目上限的 SQLUSMALLINT 值**ORDER BY**子句。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 6。 FIPS 中繼層級標準驅動程式會傳回至少 15。  
  
 SQL_MAX_COLUMNS_IN_SELECT (ODBC 2.0)  
 選取清單中，指定允許的資料行數目上限 SQLUSMALLINT 值。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少為 100。 FIPS 中繼層級標準驅動程式會傳回至少 250。  
  
 SQL_MAX_COLUMNS_IN_TABLE (ODBC 2.0)  
 指定的資料表中允許的資料行數目上限 SQLUSMALLINT 值。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少為 100。 FIPS 中繼層級標準驅動程式會傳回至少 250。  
  
 SQL_MAX_CONCURRENT_ACTIVITIES ODBC (1.0)  
 指定驅動程式可支援連線作用中陳述式的最大數目的 SQLUSMALLINT 值。 陳述式會定義為使用中，如果有暫止狀態，使用詞彙 「 結果 」 的意義的資料列的結果**選取**作業或受影響資料列**插入**，**更新**，或**刪除**作業 （例如資料列計數），或者如果它是在 NEED_DATA 狀態。 此值可反映出驅動程式或資料來源所加諸的限制。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_ACTIVE_STATEMENTS。  
  
 SQL_MAX_CURSOR_NAME_LEN ODBC (1.0)  
 指定資料來源中的資料指標名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 18。 FIPS 中繼層級標準驅動程式會傳回至少 128。  
  
 SQL_MAX_DRIVER_CONNECTIONS ODBC (1.0)  
 指定的驅動程式可以支援適用於環境的作用中連線數目上限的 SQLUSMALLINT 值。 此值可反映出驅動程式或資料來源所加諸的限制。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_ACTIVE_CONNECTIONS。  
  
 SQL_MAX_IDENTIFIER_LEN (ODBC 3.0)  
 SQLUSMALLINT 指出的大小上限以支援使用者定義名稱的資料來源中的字元。  
  
 FIPS 項目層級標準驅動程式會傳回至少 18。 FIPS 中繼層級標準驅動程式會傳回至少 128。  
  
 SQL_MAX_INDEX_SIZE (ODBC 2.0)  
 指定的索引合併欄位中允許的位元組數目上限 SQLUINTEGER 值。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 SQL_MAX_PROCEDURE_NAME_LEN ODBC (1.0)  
 指定資料來源中的程序名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 SQL_MAX_ROW_SIZE (ODBC 2.0)  
 指定的資料表中的單一資料列的最大長度 SQLUINTEGER 值。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 2000。 FIPS 中繼層級標準驅動程式會傳回至少 8000。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG (ODBC 3.0)  
 字元字串:"Y"如果 SQL_MAX_ROW_SIZE 類型資訊，請在資料列，會包含所有 SQL_LONGVARCHAR 與 SQL_LONGVARBINARY 資料行的長度，傳回的最大資料列大小"N"則否。  
  
 SQL_MAX_SCHEMA_NAME_LEN ODBC (1.0)  
 指定資料來源中的結構描述名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 18。 FIPS 中繼層級標準驅動程式會傳回至少 128。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_MAX_OWNER_NAME_LEN。  
  
 SQL_MAX_STATEMENT_LEN (ODBC 2.0)  
 指定 SQL 陳述式的最大長度 （字元數，包括空白字元） 的 SQLUINTEGER 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 SQL_MAX_TABLE_NAME_LEN ODBC (1.0)  
 指定資料來源中的資料表名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 18。 FIPS 中繼層級標準驅動程式會傳回至少 128。  
  
 SQL_MAX_TABLES_IN_SELECT (ODBC 2.0)  
 指定資料表中允許的最大數目的 SQLUSMALLINT 值**FROM**子句**選取**陳述式。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 FIPS 項目層級標準驅動程式會傳回至少 15。 FIPS 中繼層級標準驅動程式會傳回至少 50。  
  
 SQL_MAX_USER_NAME_LEN (ODBC 2.0)  
 指定資料來源中的使用者名稱的最大長度 SQLUSMALLINT 值。 如果沒有最大長度，或長度不知道，這個值設為零。  
  
 SQL_MULT_RESULT_SETS ODBC (1.0)  
 字元字串:"Y"(如果資料來源支援多個結果集，"N"，如果不存在。  
  
 如需有關多個結果集的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 SQL_MULTIPLE_ACTIVE_TXN ODBC (1.0)  
 字元字串:"Y"(如果此驅動程式支援多個使用中交易，在相同的時間，"N"，如果只有一筆交易可以在任何時間。  
  
 在分散式交易的情況下則不適用此資訊類型傳回的資訊。  
  
 SQL_NEED_LONG_DATA_LEN (ODBC 2.0)  
 字元字串： 如果不存在，將會傳送至資料來源，"N"的"Y"(如果資料來源需要的值的長度長資料 （資料類型是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型） 的值之前。 如需詳細資訊，請參閱[SQLBindParameter 函數](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 SQL_NON_NULLABLE_COLUMNS ODBC (1.0)  
 指定資料來源是否支援 NOT NULL 資料行中的 SQLUSMALLINT 值：  
  
 SQL_NNC_NULL = 所有資料行必須是可為 null。  
  
 SQL_NNC_NON_NULL = 資料行不可為 null。 (資料來源支援**NOT NULL**中的資料行條件約束**CREATE TABLE**陳述式。)  
  
 SQL 92 項目層級標準驅動程式會傳回 SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION (ODBC 2.0)  
 指定 Null 結果集內的排序的 SQLUSMALLINT 值：  
  
 SQL_NC_END = Null 排序結果集，不論 ASC 或 DESC 關鍵字的結尾。  
  
 SQL_NC_HIGH = Null 會排序在高階的結果集，根據 ASC 或 DESC 關鍵字。  
  
 SQL_NC_LOW = Null 排序結果集，根據 ASC 或 DESC 關鍵字的下限。  
  
 SQL_NC_START = Null 排序結果集，不論 ASC 或 DESC 關鍵字的開頭。  
  
 SQL_NUMERIC_FUNCTIONS ODBC (1.0)  
 注意： ODBC 1.0; 中的資訊類型所導入它引進的版本會標示每一個位元遮罩。  
  
 SQLUINTEGER 位元遮罩列舉支援的驅動程式和相關聯的資料來源之純量數值函式。  
  
 下列的位元遮罩用來判斷支援哪些數值的函式：  
  
 SQL_FN_NUM_ABS (ODBC 1.0) SQL_FN_NUM_ACOS (ODBC 1.0) SQL_FN_NUM_ASIN (ODBC 1.0) SQL_FN_NUM_ATAN (ODBC 1.0) SQL_FN_NUM_ATAN2 (ODBC 1.0) SQL_FN_NUM_CEILING (ODBC 1.0) SQL_FN_NUM_COS (ODBC 1.0) SQL_FN_NUM_COT (ODBC 1.0) SQL_FN_NUM_DEGREES (ODBC 2.0) SQL_FN_NUM_EXP (ODBC 1.0) SQL_FN_NUM_FLOOR (ODBC 1.0) SQL_FN_NUM_LOG (ODBC 1.0) SQL_FN_NUM_LOG10 (ODBC 2.0) SQL_FN_NUM_MOD (ODBC 1.0) SQL_FN_NUM_PI (ODBC 1.0) SQL_FN_NUM_POWER (ODBC 2.0) SQL_FN_NUM_RADIANS (ODBC 2.0) SQL_FN_NUM_RAND (ODBC 1.0) SQL_FN_NUM_ROUND (ODBC 2.0) SQL_FN_NUM_SIGN (ODBC 1.0) SQL_FN_NUM_SIN (ODBC 1.0) SQL_FN_NUM_SQRT (ODBC 1.0) SQL_FN_NUM_TAN (ODBC 1.0) SQL_FN_NUM_TRUNCATE (ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE (ODBC 3.0)  
 SQLUINTEGER 值，表示 ODBC 3 層級*.x*驅動程式符合的介面。  
  
 SQL_OIC_CORE： 應該符合所有的 ODBC 驅動程式的最低層級。 此層級包含基本介面項目，例如連線函式、 準備和執行 SQL 陳述式的函式，基本的結果集的中繼資料函數、 基本目錄函數等等。  
  
 SQL_OIC_LEVEL1: 層級包括核心標準相容性層級功能，加上可捲動資料指標，書籤，定位更新和刪除，等等。  
  
 為 SQL_OIC_LEVEL2: 層級包括層級 1 標準相容性層級功能，加上進階的功能，例如機密的資料指標。更新、 刪除和重新整理書籤。預存程序支援;目錄函數的主要和外部索引鍵。多個類別目錄支援;等等。  
  
 如需詳細資訊，請參閱[介面一致性層級](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 SQL_ODBC_VER ODBC (1.0)  
 ODBC 驅動程式管理員符合版本字串的字元字串。 版本是表單的 # #。 # #。 0000，其中前兩個數字的主要版本，而下面兩個位數的次要版本。 這被實作只能在驅動程式管理員。  
  
 SQL_OJ_CAPABILITIES (ODBC 2.01)  
 SQLUINTEGER 位元遮罩列舉支援的驅動程式和資料來源的外部聯結的類型。 下列的位元遮罩用來判斷哪些類型受到支援：  
  
 SQL_OJ_LEFT = 左外部聯結支援。  
  
 SQL_OJ_RIGHT = 右外部聯結支援。  
  
 SQL_OJ_FULL = 完整外部聯結支援。  
  
 SQL_OJ_NESTED = 巢狀外部聯結支援。  
  
 SQL_OJ_NOT_ORDERED = 外部聯結的 ON 子句中的名稱不一定要在其個別的資料表名稱的順序相同的資料行**外部聯結**子句。  
  
 SQL_OJ_INNER = 內部資料表 （在左方外部聯結的右方資料表） 或右方外部聯結左側資料表也可用在內部聯結。 這不適用於不需要內部的資料表中的完整外部聯結。  
  
 SQL_OJ_ALL_COMPARISON_OPS = 比較運算子的 ON 子句中可以是任何 ODBC 比較運算子。 如果未設定此位元，只有等於 （=） 比較運算子可用在外部聯結。  
  
 如果任何這些選項傳回的支援，則不支援任何外部聯結子句。  
  
 支援的相關資訊的 SELECT 陳述式的關聯式聯結運算子的 sql-92 所定義，請參閱 SQL_SQL92_RELATIONAL_JOIN_OPERATORS。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT (ODBC 2.0)  
 字元字串:"Y"如果中的資料行**ORDER BY**子句必須在選取清單中; 否則"N"。  
  
 SQL_PARAM_ARRAY_ROW_COUNTS (ODBC 3.0)  
 中的參數化的執行計數 SQLUINTEGER 列舉有關資料列的可用性的驅動程式的屬性。 具有下列值：  
  
 SQL_PARC_BATCH = 個別資料列計數可供每個參數集。 在概念上相當於驅動程式產生的 SQL 陳述式，針對陣列中設定每個參數的其中一個批次。 擴充的錯誤資訊可以擷取使用 SQL_PARAM_STATUS_PTR 描述項欄位。  
  
 SQL_PARC_NO_BATCH = 沒有只有一個資料列計數，也就是所產生的陳述式的整個陣列的參數執行累積的資料列計數。 在概念上相當於陳述式與完整的參數陣列視為一個不可部分完成單位。 錯誤的處理相同如同執行一個陳述式。  
  
 SQL_PARAM_ARRAY_SELECTS (ODBC 3.0)  
 列舉結果的可用性有關驅動程式的屬性 SQLUINTEGER 設定參數化的執行中。 具有下列值：  
  
 SQL_PAS_BATCH = 每一組參數的可用設定的一個結果。 在概念上相當於驅動程式產生的 SQL 陳述式，針對陣列中設定每個參數的其中一個批次。  
  
 SQL_PAS_NO_BATCH = 沒有只有一個結果集，這表示累計結果集會造成的陳述式的完整陣列的參數執行。 在概念上相當於陳述式與完整的參數陣列視為一個不可部分完成單位。  
  
 SQL_PAS_NO_SELECT = A 驅動程式不允許使用參數陣列來執行的結果集產生陳述式。  
  
 SQL_PROCEDURE_TERM ODBC (1.0)  
 程序; 資料來源供應商的名稱字元字串例如，「 資料庫程序 」、 「 預存程序 」，「 程序 」、 「 封裝 」 或 「 預存的查詢 」。  
  
 SQL_PROCEDURES ODBC (1.0)  
 字元字串:"Y"(如果資料來源支援程序，且驅動程式支援 ODBC 的程序引動過程語法;"N"則否。  
  
 SQL_POS_OPERATIONS (ODBC 2.0)  
 列舉中的支援作業 SQLINTEGER 位元遮罩**SQLSetPos**。  
  
 下列的位元遮罩是與旗標搭配使用，以判斷支援哪些選項。  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE (ODBC 2.0)  
 SQLUSMALLINT 值，如下所示：  
  
 SQL_IC_UPPER = 引號 SQL 中的識別項不區分大小寫，而且會儲存在系統目錄中的大寫。  
  
 SQL_IC_LOWER = 引號 SQL 中的識別項不區分大小寫，而且會儲存在系統目錄中的小寫。  
  
 則為 SQL_IC_SENSITIVE = 引號 SQL 中的識別碼會區分大小寫，而且會儲存在系統目錄中的混合大小寫。 （SQL 92 – 相容資料庫中，引號識別項是一律區分大小寫）。  
  
 SQL_IC_MIXED = 引號 SQL 中的識別項不區分大小寫，而且會儲存在系統目錄中的混合大小寫。  
  
 SQL 92 項目層級標準驅動程式一定會傳回，則為 SQL_IC_SENSITIVE。  
  
 SQL_ROW_UPDATES ODBC (1.0)  
 字元字串:"Y"(如果索引鍵集驅動或混合的資料指標會維護資料列版本，或所有的值提取資料列，且可以偵測到資料列所做的任何使用者自上次擷取資料列的任何更新。 （這只適用於更新，無法插入或刪除。）驅動程式可以傳回 SQL_ROW_UPDATED 旗標，為資料列狀態陣列時**SQLFetchScroll**呼叫。 否則，"N"。  
  
 SQL_SCHEMA_TERM ODBC (1.0)  
 結構描述; 資料來源供應商的名稱的字元字串例如，「 擁有者 」、 「 授權識別碼 」 或者 「 結構描述 」。  
  
 在上方、 下方，或混合的情況下，可以傳回的字元字串。  
  
 SQL 92 項目層級標準驅動程式一定會傳回 「 結構描述 」。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_OWNER_TERM。  
  
 SQL_SCHEMA_USAGE (ODBC 2.0)  
 SQLUINTEGER 位元遮罩列舉可以在其中使用結構描述的陳述式：  
  
 SQL_SU_DML_STATEMENTS = 支援結構描述中所有的資料操作語言陳述式：**選取**，**插入**，**更新**，**刪除**，而且如果支援，**選取更新**和定位 update 和 delete 陳述式。  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC 程序引動過程陳述式中支援結構描述。  
  
 SQL_SU_TABLE_DEFINITION = 支援結構描述中所有的資料表定義陳述式： **CREATE TABLE**， **CREATE VIEW**， **ALTER TABLE**，**卸除的資料表**，和**卸除檢視**。  
  
 SQL_SU_INDEX_DEFINITION = 支援結構描述中所有的索引定義陳述式： **CREATE INDEX**和**DROP INDEX**。  
  
 SQL_SU_PRIVILEGE_DEFINITION = 支援結構描述中所有特殊權限定義陳述式： **GRANT**和**撤銷**。  
  
 SQL 92 項目層級標準驅動程式一定會傳回 SQL_SU_DML_STATEMENTS、 SQL_SU_TABLE_DEFINITION 和 SQL_SU_PRIVILEGE_DEFINITION 選項，支援。  
  
 這*資訊類型*已重新命名為從 ODBC 2.0 ODBC 3.0*資訊類型*SQL_OWNER_USAGE。  
  
 SQL_SCROLL_OPTIONS ODBC (1.0)  
 注意： ODBC 1.0; 中的資訊類型所導入它引進的版本會標示每一個位元遮罩。  
  
 SQLUINTEGER 位元遮罩列舉支援可捲動資料指標捲動選項。  
  
 下列的位元遮罩用來判斷支援哪些選項：  
  
 SQL_SO_FORWARD_ONLY = 資料指標唯一捲動向前復原。 ODBC (1.0)  
  
 SQL_SO_STATIC = 資料的結果集是靜態。 (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = 此驅動程式會儲存和使用該索引鍵在結果集中的每個資料列。 ODBC (1.0)  
  
 SQL_SO_DYNAMIC = 驅動程式分開 （索引鍵集大小為資料列集大小相同） 的資料列集中的每個資料列的索引鍵。 ODBC (1.0)  
  
 SQL_SO_MIXED = 每個資料列索引鍵集，而索引鍵集大小的資料列集大小大於驅動程式會保留索引鍵。 資料指標為索引鍵集內索引鍵集驅動和動態外部索引鍵集。 ODBC (1.0)  
  
 可捲動資料指標的相關資訊，請參閱[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 SQL_SEARCH_PATTERN_ESCAPE ODBC (1.0)  
 字元字串，指定驅動程式支援做為搜尋模式中的有效字元允許使用的模式比對中繼字元底線 (_) 和百分比符號 （%） 逸出字元。 此逸出字元只適用於那些支援搜尋字串的目錄函式引數。 如果這個字串是空的驅動程式不支援搜尋模式的逸出字元。  
  
 因為此資訊類型不會指出的逸出字元的一般支援**像**述詞，sql-92 不包含這個字元字串的需求。  
  
 這*資訊類型*僅限於目錄函數。 如需搜尋的模式字串中逸出字元使用的說明，請參閱[模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 &LT; (ODBC 1.0)  
 字元字串的實際資料來源專用伺服器名稱。當資料來源名稱會使用於時很有用**SQLConnect**， **SQLDriverConnect**，和**SQLBrowseConnect**。  
  
 SQL_SPECIAL_CHARACTERS (ODBC 2.0)  
 字元字串，其中包含所有的特殊字元 （也就是之外的所有字元 a 到 z、 A 到 Z、 0 到 9 和底線），可用於識別項名稱，例如資料表名稱、 資料行名稱或在資料來源上的索引名稱。 例如，"#$^"。 如果識別項包含一或多個這些字元，識別碼必須是分隔的識別碼。  
  
 SQL_SQL_CONFORMANCE (ODBC 3.0)  
 表示 SQL 92 驅動程式支援的層級 SQLUINTEGER 值：  
  
 SQL_SC_SQL92_ENTRY = 項目層級 sql-92 相容。  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = FIPS 127-2 相容的過渡期等級。  
  
 SQL_SC_SQL92_FULL = 完整層級 sql-92 相容。  
  
 SQL_SC_ SQL92_INTERMEDIATE = 中繼層級 sql-92 相容。  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉 datetime 純量函數的驅動程式和相關聯的資料來源，支援以 sql-92 定義。  
  
 下列的位元遮罩用來判斷支援哪些 datetime 函式：  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 列舉中的外部索引鍵所支援的規則 SQLUINTEGER 位元遮罩**刪除**陳述式，以 sql-92 定義。  
  
 下列的位元遮罩用來判斷資料來源所支援的子句：  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 過渡期的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 列舉中的外部索引鍵所支援的規則 SQLUINTEGER 位元遮罩**更新**陳述式，以 sql-92 定義。  
  
 下列的位元遮罩用來判斷資料來源所支援的子句：  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL 92 完整的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 列舉中支援的子句 SQLUINTEGER 位元遮罩**GRANT**陳述式，以 sql-92 定義。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷資料來源所支援的子句：  
  
 SQL_SG_DELETE_TABLE （項目層級） SQL_SG_INSERT_COLUMN （中介層級） SQL_SG_INSERT_TABLE （項目層級） SQL_SG_REFERENCES_TABLE （項目層級） SQL_SG_REFERENCES_COLUMN （項目層級） SQL_SG_SELECT_TABLE （項目層級） SQL_SG_UPDATE_COLUMN (項目層級） SQL_SG_UPDATE_TABLE （項目層級） SQL_SG_USAGE_ON_DOMAIN （FIPS 過渡期的層級） SQL_SG_USAGE_ON_CHARACTER_SET （FIPS 過渡期的層級） SQL_SG_USAGE_ON_COLLATION （FIPS 過渡期的層級） SQL_SG_USAGE_ON_TRANSLATION (FIPS過渡期的層級） SQL_SG_WITH_GRANT_OPTION （項目層級）  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉數值純量函數的驅動程式和相關聯的資料來源，支援以 sql-92 定義。  
  
 下列的位元遮罩用來判斷支援哪些數值的函式：  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 列舉中支援的述詞 SQLUINTEGER 位元遮罩**選取**陳述式，以 sql-92 定義。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷資料來源所支援的選項：  
  
 SQL_SP_BETWEEN （項目層級） SQL_SP_COMPARISON （項目層級） SQL_SP_EXISTS （項目層級） SQL_SP_IN （項目層級） SQL_SP_ISNOTNULL （項目層級） SQL_SP_ISNULL （項目層級） SQL_SP_LIKE （項目層級） SQL_SP_MATCH_FULL （完整的層級） SQL_SP_MATCH_PARTIAL（完整的層級）（完整的層級） SQL_SP_MATCH_UNIQUE_FULL SQL_SP_MATCH_UNIQUE_PARTIAL （完整的層級） SQL_SP_OVERLAPS （FIPS 過渡期的層級） SQL_SP_QUANTIFIED_COMPARISON （項目層級） SQL_SP_UNIQUE （項目層級）  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 列舉中支援的關聯式聯結運算子 SQLUINTEGER 位元遮罩**選取**陳述式，以 sql-92 定義。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷資料來源所支援的選項：  
  
 SQL_SRJO_CORRESPONDING_CLAUSE （中介層級） SQL_SRJO_CROSS_JOIN （完整的層級） SQL_SRJO_EXCEPT_JOIN （中介層級） SQL_SRJO_FULL_OUTER_JOIN （中介層級） SQL_SRJO_INNER_JOIN （FIPS 過渡期的層級） SQL_SRJO_INTERSECT_JOIN（中介層級）SQL_SRJO_LEFT_OUTER_JOIN （FIPS 過渡期的層級） SQL_SRJO_NATURAL_JOIN （FIPS 過渡期的層級） SQL_SRJO_RIGHT_OUTER_JOIN （FIPS 過渡期的層級） SQL_SRJO_UNION_JOIN （完整的層級）  
  
 SQL_SRJO_INNER_JOIN 表示支援**內部聯結**語法，不適用於內部聯結功能。 支援**內部聯結**語法是 FIPS 過渡期，而內部聯結功能支援**項目**。  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 列舉中支援的子句 SQLUINTEGER 位元遮罩**撤銷**陳述式，如 SQL 92，支援的資料來源中定義。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷資料來源所支援的子句：  
  
 SQL_SR_CASCADE （FIPS 過渡期的層級） SQL_SR_DELETE_TABLE （項目層級） SQL_SR_GRANT_OPTION_FOR （中介層級） SQL_SR_INSERT_COLUMN （中介層級） SQL_SR_INSERT_TABLE （項目層級） SQL_SR_REFERENCES_COLUMN （項目層級） SQL_SR_REFERENCES_TABLE （項目層級） SQL_SR_RESTRICT （FIPS 過渡期的層級） SQL_SR_SELECT_TABLE （項目層級） SQL_SR_UPDATE_COLUMN （項目層級） SQL_SR_UPDATE_TABLE （項目層級） SQL_SR_USAGE_ON_DOMAIN （FIPS 過渡期的層級） SQL_SR_USAGE_ON_CHARACTER_SET （FIPS 過渡期的層級） SQL_SR_USAGE_ON_COLLATION （FIPS 過渡期的層級） SQL_SR_USAGE_ON_TRANSLATION （FIPS 過渡期的層級）  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 列舉支援的資料列值建構函式運算式 SQLUINTEGER 位元遮罩**選取**陳述式，以 sql-92 定義。 下列的位元遮罩用來判斷資料來源所支援的選項：  
  
 SQL_SRVC_VALUE_EXPRESSION SQL_SRVC_NULL SQL_SRVC_DEFAULT SQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉字串純量函數的驅動程式和相關聯的資料來源，支援以 sql-92 定義。  
  
 下列的位元遮罩用來判斷支援哪些字串函數：  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 SQLUINTEGER 位元遮罩中以 sql-92 定義列舉支援的值運算式。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷資料來源所支援的選項：  
  
 SQL_SVE_CASE （中介層級） SQL_SVE_CAST （FIPS 過渡期的層級） SQL_SVE_COALESCE （中介層級） SQL_SVE_NULLIF （中介層級）  
  
 SQL_STANDARD_CLI_CONFORMANCE (ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉 CLI 標準的項目，此驅動程式符合。 下列的位元遮罩用來判斷哪一個驅動程式符合的層級：  
  
 SQL_SCC_XOPEN_CLI_VERSION1: 驅動程式符合開啟群組 CLI 第 1 版。  
  
 SQL_SCC_ISO92_CLI: 驅動程式符合 ISO 92 CLI。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 SQLUINTEGER 位元遮罩描述驅動程式所支援的靜態資料指標的屬性。 此位元遮罩包含的第一個屬性; 子集第二個子集，請參閱 SQL_STATIC_CURSOR_ATTRIBUTES2。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 如需這些位元遮罩的描述，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 （並以取代說明中的 「 動態資料指標 」 的 「 靜態資料指標 」）。  
  
 SQL 92 中繼層級標準驅動程式會通常傳回 SQL_CA1_NEXT、 SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項的支援，因為此驅動程式支援透過內嵌擷取 SQL 陳述式的可捲動資料指標。 因為這不會直接判斷基礎的 SQL 支援，不過，可捲動資料指標可能不是，即使 sql-92 中繼層級標準驅動程式支援。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 SQLUINTEGER 位元遮罩描述驅動程式所支援的靜態資料指標的屬性。 此位元遮罩包含屬性; 第二個的子集第一個子集，請參閱 SQL_STATIC_CURSOR_ATTRIBUTES1。  
  
 下列的位元遮罩用來判斷支援哪些屬性：  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 如需這些位元遮罩的描述，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 （並以取代說明中的 「 動態資料指標 」 的 「 靜態資料指標 」）。  
  
 SQL_STRING_FUNCTIONS ODBC (1.0)  
 注意： ODBC 1.0; 中的資訊類型所導入它引進的版本會標示每一個位元遮罩。  
  
 SQLUINTEGER 位元遮罩列舉支援的驅動程式和相關聯的資料來源之純量的字串函式。  
  
 下列的位元遮罩用來判斷支援哪些字串函數：  
  
 SQL_FN_STR_ASCII (ODBC 1.0) SQL_FN_STR_BIT_LENGTH (ODBC 3.0) SQL_FN_STR_CHAR (ODBC 1.0) SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) SQL_FN_STR_CONCAT (ODBC 1.0) SQL_FN_STR_DIFFERENCE (ODBC 2.0) SQL_FN_STR_INSERT (ODBC1.0) SQL_FN_STR_LCASE (ODBC 1.0) SQL_FN_STR_LEFT (ODBC 1.0) SQL_FN_STR_LENGTH (ODBC 1.0) SQL_FN_STR_LOCATE (ODBC 1.0) SQL_FN_STR_LTRIM (ODBC 1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0) SQL_FN_STR_REPLACE (ODBC 1.0) SQL_FN_STR_RIGHT (ODBC 1.0) SQL_FN_STR_RTRIM (ODBC 1.0) SQL_FN_STR_SOUNDEX (ODBC 2.0) SQL_FN_STR_SPACE (ODBC 2.0) SQL_FN_STR_SUBSTRING (ODBC 1.0) SQL_FN_STR_UCASE (ODBC 1.0)  
  
 如果應用程式可以呼叫**尋找**具有純量函式*string_exp1*， *string_exp2*，和*啟動*引數，此驅動程式傳回 SQL_FN_STR_LOCATE 位元遮罩。 如果應用程式可以呼叫尋找純量函數中的，只有*string_exp1*和*string_exp2*引數，驅動程式會傳回 SQL_FN_STR_LOCATE_2 位元遮罩。 完全支援的驅動程式**尋找**純量函數會傳回這兩種位元遮罩。  
  
 (如需詳細資訊，請參閱[字串函數](../../../odbc/reference/appendixes/string-functions.md)附錄 E 中 」 的純量函數。")  
  
 SQL_SUBQUERIES (ODBC 2.0)  
 SQLUINTEGER 位元遮罩列舉支援子查詢的述詞：  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES 位元遮罩，表示支援子查詢的所有述詞，支援相互關聯子查詢。  
  
 SQL 92 項目層級標準驅動程式一定會傳回這些位元的所有設定的位元遮罩。  
  
 SQL_SYSTEM_FUNCTIONS ODBC (1.0)  
 SQLUINTEGER 位元遮罩列舉驅動程式和相關聯的資料來源所支援的純量系統函數。  
  
 下列的位元遮罩用來判斷支援哪些系統函數：  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM ODBC (1.0)  
 資料表; 資料來源供應商的名稱的字元字串例如，「 資料表 」 或者 「 檔案 」。  
  
 這個字元字串可以是上方、 下方，或混合大小寫。  
  
 SQL 92 項目層級標準驅動程式一定會傳回"table"。  
  
 SQL_TIMEDATE_ADD_INTERVALS (ODBC 2.0)  
 SQLUINTEGER 位元遮罩列舉驅動程式和 TIMESTAMPADD 純量函數的相關聯的資料來源所支援的時間戳記間隔。  
  
 下列的位元遮罩用來判斷支援哪些間隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 過渡期的層級標準驅動程式一定會傳回這些位元的所有設定的位元遮罩。  
  
 SQL_TIMEDATE_DIFF_INTERVALS (ODBC 2.0)  
 SQLUINTEGER 位元遮罩列舉驅動程式和 TIMESTAMPDIFF 純量函數的相關聯的資料來源所支援的時間戳記間隔。  
  
 下列的位元遮罩用來判斷支援哪些間隔：  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 過渡期的層級標準驅動程式一定會傳回這些位元的所有設定的位元遮罩。  
  
 SQL_TIMEDATE_FUNCTIONS ODBC (1.0)  
 注意： ODBC 1.0; 中的資訊類型所導入它引進的版本會標示每一個位元遮罩。  
  
 SQLUINTEGER 位元遮罩的純量的日期和時間函式的驅動程式和相關聯的資料來源所支援的列舉。  
  
 下列的位元遮罩用來判斷支援的日期和時間函數：  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0) SQL_FN_TD_CURRENT_TIME (ODBC 3.0) SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) SQL_FN_TD_CURDATE (ODBC 1.0) SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 2.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0) SQL_FN_TD_DAYOFWEEK (ODBC 1.0) SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0) SQL_FN_TD_HOUR (ODBC 1.0) SQL_FN_TD_MINUTE (ODBC 1.0) SQL_FN_TD_MONTH (ODBC 1.0) SQL_FN_TD_MONTHNAME (ODBC 2.0) SQL_FN_TD_NOW (ODBC 1.0) SQL_FN_TD_QUARTER (ODBC 1.0) SQL_FN_TD_第二個 (ODBC 1.0) SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) SQL_FN_TD_WEEK (ODBC 1.0) SQL_FN_TD_YEAR (ODBC 1.0)  
  
 SQL_TXN_CAPABLE ODBC (1.0)  
 注意： ODBC 1.0; 中的資訊類型所導入它引進的版本會標示每個傳回的值。  
  
 描述驅動程式或資料來源中的交易支援 SQLUSMALLINT 值：  
  
 SQL_TC_NONE = 不支援交易。 ODBC (1.0)  
  
 SQL_TC_DML = 交易可以包含僅資料操作語言 (DML) 陳述式 (**選取**，**插入**，**更新**，**刪除**). 資料定義語言 (DDL) 陳述式的交易原因發生錯誤。 ODBC (1.0)  
  
 SQL_TC_DDL_COMMIT = 交易可以包含僅 DML 陳述式。 DDL 陳述式 (**CREATE TABLE**， **DROP INDEX**等等) 中的交易原因發生交易認可。 (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = 交易可以包含僅 DML 陳述式。 在交易中發現的 DDL 陳述式都會被忽略。 (ODBC 2.0)  
  
 SQL_TC_ALL = 交易可以包含 DDL 陳述式和 DML 陳述式，以任何順序。 ODBC (1.0)  
  
 （支援的交易是以 sql-92 必要的因為 sql-92 標準驅動程式 [任何層級] 永遠不會傳回 SQL_TC_NONE。）  
  
 SQL_TXN_ISOLATION_OPTION ODBC (1.0)  
 SQLUINTEGER 位元遮罩列舉從驅動程式或資料來源可用的交易隔離等級。  
  
 下列的位元遮罩可用以及旗標來判斷支援哪些選項：  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 如需這些隔離等級的描述，請參閱 SQL_DEFAULT_TXN_ISOLATION 的描述。  
  
 若要設定交易隔離等級，應用程式呼叫**SQLSetConnectAttr**設定 SQL_ATTR_TXN_ISOLATION 屬性。 如需詳細資訊，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 支援的 SQL 92 項目層級標準驅動程式一定會傳回 sql_txn_serializable 的情況。 FIPS 過渡期的層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_UNION (ODBC 2.0)  
 列舉的支援 SQLUINTEGER 位元遮罩**UNION**子句：  
  
 SQL_U_UNION = 資料來源支援**UNION**子句。  
  
 SQL_U_UNION_ALL = 資料來源支援**所有**關鍵字**UNION**子句。 (**SQLGetInfo**在此情況下傳回 SQL_U_UNION 和 SQL_U_UNION_ALL。)  
  
 SQL 92 項目層級標準驅動程式一定會傳回這兩個選項的支援。  
  
 SQL_USER_NAME ODBC (1.0)  
 具有特定資料庫，可以不同於登入名稱中使用的名稱的字元字串。  
  
 SQL_XOPEN_CLI_YEAR (ODBC 3.0)  
 字元字串，表示與版本的 ODBC 驅動程式管理員完全符合 Open Group 規格的發行集的年份。  
  
 SQL_ACCESSIBLE_PROCEDURES ODBC (1.0)  
 字元字串： 如果使用者可以執行所有的程序所傳回"Y" **SQLProcedures**;"N"(如果可能有程序會傳回該使用者無法執行。  
  
 SQL_ACCESSIBLE_TABLES ODBC (1.0)  
 字元字串:"Y"(如果使用者是否保證**選取**所傳回的所有資料表的權限**SQLTables**;如果可能有資料表"N"會傳回使用者無法存取。  
  
 SQL_ACTIVE_ENVIRONMENTS (ODBC 3.0)  
 指定的驅動程式可以支援的使用中環境的最大數目的 SQLUSMALLINT 值。 如果沒有指定的限制或限制是未知的這個值設為零。  
  
 SQL_AGGREGATE_FUNCTIONS (ODBC 3.0)  
 SQLUINTEGER 位元遮罩列舉支援彙總函式：  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL 92 項目層級標準驅動程式一定會傳回所有的這些選項的支援。  
  
 SQL_ALTER_DOMAIN (ODBC 3.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**ALTER 網域**陳述式，如 SQL 92，支援的資料來源中定義。 SQL 92 完整的層級相容驅動程式一定會傳回所有的位元遮罩。 傳回值為"0"表示**ALTER 網域**不支援陳述式。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 的加入支援網域條件約束 （完整層級）  
  
 SQL_AD_ADD_DOMAIN_DEFAULT = \<alter 網域 > \<set 網域預設子句 > 支援 （完整層級）  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION =\<條件約束名稱定義子句 > 支援命名 網域條件約束 （中介層級）  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT = \<drop 網域條件約束子句 > 支援 （完整層級）  
  
 SQL_AD_DROP_DOMAIN_DEFAULT = \<alter 網域 > \<drop 網域預設子句 > 支援 （完整層級）  
  
 下列的位元會指定支援\<條件約束屬性 > 如果\<加入網域的條件約束 > 支援 （設定 SQL_AD_ADD_DOMAIN_CONSTRAINT 位元）：  
  
 （完整的層級） SQL_AD_ADD_CONSTRAINT_DEFERRABLE SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE （完整的層級） SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED （完整的層級） SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE （完整的層級）  
  
 SQL_ALTER_TABLE (ODBC 2.0)  
 列舉中的子句 SQLUINTEGER 位元遮罩**ALTER TABLE**資料來源所支援的陳述式。  
  
 必須支援這項功能的 SQL 92 或 FIPS 一致性層會顯示在每一個位元遮罩旁邊的括號。  
  
 下列的位元遮罩用來判斷支援哪些子句：  
  
 SQL_AT_ADD_COLUMN_COLLATION =\<加入資料行 > 支援子句，來指定資料行定序 （完整的層級） 的設備 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_DEFAULT =\<加入資料行 > 支援子句，指定資料行的預設值 （FIPS 過渡期的層級） 的功能 (ODBC 3.0)  
  
 SQL_AT_ADD_COLUMN_SINGLE =\<加入資料行 > 會支援 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT =\<加入資料行 > 支援子句，來指定資料行條件約束 （FIPS 過渡期的層級） 的設備 (ODBC 3.0)  
  
 SQL_AT_ADD_TABLE_CONSTRAINT =\<加入資料表條件約束 > 支援子句 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION =\<條件約束名稱定義 > 來命名資料行和資料表條件約束 （中介層級） 支援 (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_CASCADE =\<卸除資料行 > 支援串聯 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT =\<改變資料行 >\<卸除資料行預設子句 > 會支援 （中介層級） (ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_RESTRICT =\<卸除資料行 > 支援限制 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT =\<卸除資料行 > 支援限制 （FIPS 過渡期的層級） (ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT =\<改變資料行 >\<集資料行預設子句 > 會支援 （中介層級） (ODBC 3.0)  
  
 下列的位元會指定支援\<條件約束屬性 > 如果支援指定資料行或資料表條件約束 （設定 SQL_AT_ADD_CONSTRAINT 位元）：  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED （完整的層級） (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE （完整的層級） (ODBC 3.0) SQL_AT_CONSTRAINT_DEFERRABLE （完整的層級） (ODBC 3.0) SQL_AT_CONSTRAINT_NON_DEFERRABLE （完整的層級） (ODBC 3.0)  
  
 SQL_ASYNC_MODE (ODBC 3.0)  
 表示層級的驅動程式中的非同步支援 SQLUINTEGER 值：  
  
 SQL_AM_CONNECTION = 支援層級的非同步執行的連接。 請指定的連接控制代碼相關聯的所有陳述式控制代碼處於非同步模式或都在同步模式中。 在連接上的陳述式控制代碼不可以是非同步模式時相同的連接上的另一個陳述式控制代碼會在同步模式中，反之亦然。  
  
 SQL_AM_STATEMENT = 支援層級的非同步執行的陳述式。 而在相同連接上的其他陳述式控制代碼就是在同步模式下，可以是在非同步模式中，連接控制代碼相關聯的某些陳述式控制代碼。  
  
 SQL_AM_NONE = 非同步模式不支援。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 列舉相對於資料列的可用性驅動程式的行為 SQLUINTEGER 位元遮罩計算。 連同類型資訊，請使用下列的位元遮罩：  
  
 SQL_BRC_ROLLED_UP = 連續的 INSERT、 DELETE 或 UPDATE 陳述式會彙總成一個資料列計數。 如果未設定此位元，就有一個資料列計數可供每個陳述式。  
  
 SQL_BRC_PROCEDURES = 資料列計數，如果任何項目，就可以使用預存程序中執行批次。 如果有資料列計數，它們可以復原或個別，根據提供的 SQL_BRC_ROLLED_UP 位元。  
  
 SQL_BRC_EXPLICIT = 資料列計數，如果任何項目，可用來直接呼叫批次執行時**SQLExecute**或**SQLExecDirect**。 如果有資料列計數，它們可以復原或個別，根據提供的 SQL_BRC_ROLLED_UP 位元。  
  
## <a name="example"></a>範例  
 **SQLGetInfo**為 SQLUINTEGER 位元遮罩中傳回的支援選項清單 **InfoValuePtr*。 每個選項的位元遮罩是與旗標搭配使用，以判斷是否支援的選項。  
  
 例如，應用程式可以使用下列程式碼來判斷是否與連接相關聯的驅動程式所支援的子字串的純量函數。  
  
 如需其他範例使用**SQLGetInfo**，請參閱[SQLTables 函數](../../../odbc/reference/syntax/sqltables-function.md)。  
  
```  
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
 [SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 判斷驅動程式是否支援函式  
 [SQLGetFunctions 函式](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 傳回陳述式屬性的設定  
 [SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 傳回資料來源的資料類型的相關資訊  
 [SQLGetTypeInfo 函式](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

