---
title: SQLGetInfo 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
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
ms.openlocfilehash: 514922fd085cfd2ba19eb5c07dd844db82d55202
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303340"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetInfo**傳回有關與連接關聯的驅動程式和資料來源的一般資訊。  
  
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
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *資訊類型*  
 [輸入]資訊類型。  
  
 *資訊價值Ptr*  
 【輸出]指向要返回資訊的緩衝區的指標。 根據請求*的資訊類型*,傳回的資訊將如下:空端字元字串、SQLUSMALLINT 值、SQLUINTEGER 位罩、SQLUINTEGER 標誌、SQLUINTEGER 二進位值或 SQLULEN 值。  
  
 如果*InfoType*參數是SQL_DRIVER_HDESC或SQL_DRIVER_HSTMT,*則 InfoValuePtr*參數既是輸入參數,也是輸出參數。 (有關詳細資訊,請參閱此函數說明中的SQL_DRIVER_HDESC或SQL_DRIVER_HSTMT描述符。  
  
 如果*InfoValuePtr*為 NULL,*則 StringLengthPtr*仍將返回可用在*InfoValuePtr*指向的緩衝區中返回的位元總數(不包括字元資料的空終止字元)。  
  
 *緩衝區長度*  
 [輸入]\**資訊值Ptr*緩衝區的長度。 如果*\*InfoValuePtr*中的值不是字串,或者如果*InfoValuePtr*是空指標,則忽略*緩衝區長度*參數。 驅動程式假定*\*InfoValuePtr*的大小是 SQLUSMALLINT 或 SQLUINTEGER,具體取決於*資訊類型*。 如果*\*InfoValuePtr*是 Unicode 字串(在呼叫**SQLGetInfoW**時),*則緩衝區長度*參數必須是偶數;否則,將返回 SQLSTATE HY090(無效字串或緩衝區長度)。  
  
 *字串長度 Ptr*  
 【輸出]指向一個緩衝區的指標,用於返回可在 #*InfoValuePtr*中傳回的位元組總數(不包括字元資料的空終止字元)。  
  
 對於字元資料,如果可供返回的位元組數大於或等於*BufferLength,*\**則 InfoValuePtr*中的資訊將被截斷為*BufferLength*位元組減去空終止字元的長度,並且由驅動程式終止。  
  
 對所有其他類型的資料,*會忽略緩衝區長度*的值,並且驅動程式\*假定*InfoValuePtr*的大小為 SQLUSMALLINT 或 SQLUINTEGER,具體取決於*InfoType*。  
  
## <a name="return-value"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetInfo**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_DBC的*句柄類型*和*連接句柄*的*句柄*。 下表列出了**SQLGetInfo**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|緩衝區\* *InfoValuePtr*不夠大,無法返回所有請求的資訊。 因此,資訊被截斷。 在其未壓縮形式中請求的資訊的長度在 #*StringLengthPtr*中返回。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08003|連線未開啟|(DM)*資訊類型*中請求的資訊類型需要打開的連接。 在 ODBC 保留的資訊類型中,只有SQL_ODBC_VER無需打開的連接即可返回。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY024|不合法屬性值|(DM)*資訊類型*參數*SQL_DRIVER_HSTMT,InfoValuePtr*指向的值不是有效的語句句柄。<br /><br /> (DM) *infoType*參數*SQL_DRIVER_HDESC,InfoValuePtr*指向的值不是有效的描述符句柄。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*BufferLength*指定的值小於 0。<br /><br /> (DM) 為*BufferLength*指定的值是奇數*\*,InfoValuePtr*為 Unicode 資料類型。|  
|HY096|資訊類型範圍外|為參數*InfoType*指定的值對驅動程式支援的 ODBC 版本無效。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇性的欄位|為參數*InfoType*指定的值是驅動程式不支援的特定於驅動程式的值。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 對應於*連接句柄*的驅動程式不支援該功能。|  
  
## <a name="comments"></a>註解  
 當前定義的信息類型顯示在「信息類型」中,本節後面的部分將顯示這些類型;預計將定義更多,以利用不同的數據源。 ODBC 保留一系列信息類型;驅動程式開發人員必須從 Open Group 為其特定於驅動程式使用保留值。 **SQLGetInfo**不執行用於驅動程式定義的*InfoType 的*Unicode 轉換或*分項*(參見[附錄 A:ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md) *程式設計師參考的*ODBC 錯誤代碼)。 有關詳細資訊,請參閱[特定於驅動程式的資料類型、描述符類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 \**在 InfoValuePtr*中傳回的資訊格式來取得*的資訊型態*。 **SQLGetInfo**將以五種不同格式之一傳回資訊:  
  
-   空終止字串  
  
-   SQLUSMALLINT 值  
  
-   SQLUINTEGER 位罩  
  
-   SQLUinTEGER 值  
  
-   SQLUinTEGER 二進位值  
  
 以下每種資訊類型的格式都記錄在類型的描述中。 應用程式必須相應地在 #*InfoValuePtr*中轉換傳回的值。 有關應用程式如何從 SQLUINTEGER 位掩碼檢索數據的範例,請參閱「代碼示例」。  
  
 驅動程式必須為下表中定義的每種資訊類型返回一個值。 如果資訊類型不適用於驅動程式或數據源,則驅動程式將返回下表中列出的值之一。  
  
 字串("Y"或"N")  
 "N"  
  
 字串(不是"Y"或"N")  
 空字串  
  
 SQLUSMALLINT  
 0  
  
 SQLUinteGER 位罩或 SQLUINTEGER 二進位值  
 0L  
  
 例如,如果資料源不支援過程 **,SQLGetInfo**將返回下表中列出的與過程相關的*InfoType*值的值。  
  
 SQL_PROCEDURES  
 "N"  
  
 SQL_ACCESSIBLE_PROCEDURES  
 "N"  
  
 SQL_MAX_PROCEDURE_NAME_LEN  
 0  
  
 SQL_PROCEDURE_TERM  
 空字串  
  
 **SQLGetInfo**傳回 SQLSTATE HY096(無效參數值),用於*InfoType*的值,這些值位於為 ODBC 保留以供使用的資訊類型範圍內,但不受驅動程式支援的 ODBC 版本定義。 要確定驅動程式符合的 ODBC 版本,應用程式使用SQL_DRIVER_ODBC_VER資訊類型呼叫**SQLGetInfo。** **SQLGetInfo**傳回 SQLSTATE HYC00(未實現可選功能)*的資訊類型*值,這些值在為特定於驅動程式使用而保留的資訊類型範圍內,但驅動程式不支援。  
  
 對**SQLGetInfo**的所有呼叫都需要開啟的連接,除非*資訊類型*SQL_ODBC_VER,這將返回驅動程式管理器的版本。  
  
## <a name="information-types"></a>資訊類型  
 本節列出了**SQLGetInfo**支援的資訊類型。 資訊類型按分類和按字母順序列出。 還列出了為 ODBC 3 *.x*添加或重命名的資訊類型。  
  
## <a name="driver-information"></a>驅動程式資訊  
 *InfoType*參數的以下值傳回有關 ODBC 驅動程式的資訊,例如活動敘述的數量、資料源名稱和介面標準符合性級別:  
  
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
>  實現**SQLGetInfo**時,驅動程式可以通過最小化從伺服器發送或請求資訊的次數來提高性能。  
  
## <a name="dbms-product-information"></a>DBMS 產品資訊  
 *InfoType*參數的以下值傳回有關 DBMS 產品的資訊,例如 DBMS 名稱和版本:  
  
 SQL_DATABASE_NAMESQL_DBMS_NAMESQL_DBMS_VER  
  
## <a name="data-source-information"></a>資料來源資訊  
 *InfoType*參數的以下值傳回有關資料來源的資訊,例如游標特徵和事務功能:  
  
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
 *InfoType*參數的以下值傳回有關資料來源支援的 SQL 語句的資訊。 這些資訊類型描述的每個功能的 SQL 語法是 SQL-92 語法。 這些資訊類型不能詳盡地描述整個 SQL-92 語法。 相反,它們描述了數據源通常為其提供不同級別的支援的語法部分。 具體來說,SQL-92 中的大多數 DDL 語句都包括在內。  
  
 應用程式應從SQL_SQL_CONFORMANCE資訊類型確定支援的語法的一般級別,並使用其他資訊類型來確定與規定標準合規性級別的變體。  
  
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
 *InfoType*參數的以下值傳回有關應用於 SQL 語句中的識別碼和子句的限制的資訊,例如識別符的最大長度和選擇清單中的最大欄數。 驅動程序或數據源都可以施加限制。  
  
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
  
## <a name="scalar-function-information"></a>標點函數資訊  
 *InfoType*參數的以下值返回有關資料源和驅動程式支援的標量函數的資訊。 有關標量函數的詳細資訊,請參閱附錄[E:標點函數](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)。  
  
|||  
|-|-|  
|SQL_CONVERT_FUNCTIONS|SQL_TIMEDATE_ADD_INTERVALS|  
|SQL_NUMERIC_FUNCTIONS|SQL_TIMEDATE_DIFF_INTERVALS|  
|SQL_STRING_FUNCTIONS|SQL_TIMEDATE_FUNCTIONS|  
|SQL_SYSTEM_FUNCTIONS||  
  
## <a name="conversion-information"></a>轉換資訊  
 *InfoType*參數的以下值傳回 SQL 資料型態的清單,資料來源可以使用**CONVERT**標量函數會指定的 SQL 資料型態轉換為這些類型:  
  
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
  
## <a name="information-types-added-for-odbc-3x"></a>為 ODBC 3.x 新增的資訊型態  
 為 ODBC 3 *.x*新增了*InfoType*參數的以下值:  
  
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
  
## <a name="information-types-renamed-for-odbc-3x"></a>為 ODBC 3.x 重新命名的資訊型態  
 *InfoType*參數的以下值已重新命名為 ODBC 3 *.x*。  
  
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
  
## <a name="information-types-deprecated-in-odbc-3x"></a>在 ODBC 3.x 中棄用的資訊型態  
 在 ODBC 3 *.x*中,已棄用*InfoType*參數的以下值。 ODBC 3 *.x*驅動程式必須繼續支援這些資訊類型,以便與 ODBC 2 *.x*應用程式向後相容。 (有關這些類型的的詳細資訊,請參閱附錄 G 中的[SQLGetInfo 支援](../../../odbc/reference/appendixes/sqlgetinfo-support.md):向後相容性的驅動程式指南。  
  
|||  
|-|-|  
|SQL_FETCH_DIRECTION|SQL_POS_OPERATIONS|  
|SQL_LOCK_TYPES|SQL_POSITIONED_STATEMENTS|  
|SQL_ODBC_API_CONFORMANCE|SQL_SCROLL_CONCURRENCY|  
|SQL_ODBC_SQL_CONFORMANCE|SQL_STATIC_SENSITIVITY|  
  
## <a name="information-type-descriptions"></a>資訊類型描述  
 下表按字母順序出了每種資訊類型、介紹其內容的ODBC版本及其說明。  
  
 SQL_ACCESSIBLE_PROCEDURES(ODBC 1.0)  
 字串字串:「Y」,如果用戶可以執行**SQL 程式**傳回的所有過程;如果返回過程時可能返回使用者無法執行,則為"N"。  
  
 SQL_ACCESSIBLE_TABLES(ODBC 1.0)  
 字串字串:「Y」,**如果使用者保證選擇** **SQLTables**傳回的所有表的許可權;如果返回的表是使用者無法訪問的表,則為"N"。  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 指定驅動程式可以支援的最大活動環境數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位罩對聚合函數支援:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 符合入門級的驅動程序將始終返回所有這些選項(如支援)。  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**了在**SQL-92 中定義的 ALTER DOMAIN 語句中子句,數據源支援。 SQL-92 完全符合級別的驅動程序將始終返回所有位掩碼。 返回值"0"表示不支援 ALTER **DOMAIN**語句。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 支援新增網域約束(完整等級)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<=\<變更網域>>受支援的網域預設子句(完整等級)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<=>为命名域约束(中間等級)支援規範名稱定義子句  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= 支援>刪除網域  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<=\<變更網域>刪除網域預設子句>支援(完整等級)  
  
 如果\<支援>添加域\<約束 (設定SQL_AD_ADD_DOMAIN_CONSTRAINT位),以下位指定支援的約束屬性>:  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE(全級別)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE(全級別)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED(全級別)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE(全級別)  
  
 SQL_ALTER_TABLE(ODBC 2.0)  
 SQLUINTEGER 位罩,枚舉資料來源支援的**ALTER TABLE**語句中子句。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= 支援新增欄>子句,具有指定欄位規則(完整等級)(ODBC 3.0)的功能  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= 支援新增欄>子句,具有指定列預設值(FIPS 過渡等級)(ODBC 3.0)的功能  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= 支援新增欄>(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<= 支援新增欄>子句,具有指定欄位約束(FIPS 過渡等級)(ODBC 3.0)的功能  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= 支援>項(FIPS過渡等級)(ODBC 3.0)新增表約束  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<=>为命名列和表约束(中間等級)(ODBC 3.0)支援規範名稱定義  
  
 支援SQL_AT_DROP_COLUMN_CASCADE \<= 丟棄列> CASCADE(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<=\<變更欄>刪除列預設子句>支援(中級級別)(ODBC 3.0)  
  
 支援SQL_AT_DROP_COLUMN_RESTRICT \<= 下拉列>限制(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 支援SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<=>约束的放置列(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<=\<更改欄>設定列預設子句>支援(中級級別)(ODBC 3.0)  
  
 如果支援指定欄或表\<約束(設定SQL_AT_ADD_CONSTRAINT位),以下位將指定支援約束屬性>:  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED(全級) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (全級別) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE(完整級別)(ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE(全級)(ODBC 3.0)  
  
 SQL_ASYNC_DBC_FUNCTIONS (ODBC 3.8)  
 SQLUINTEGER 值,指示驅動程式是否可以在連接句柄上異步執行函數。  
  
 SQL_ASYNC_DBC_CAPABLE = 驅動程式可以非同步執行連接函數。  
  
 SQL_ASYNC_DBC_NOT_CAPABLE = 驅動程式無法非同步執行連接函數。  
  
 SQL_ASYNC_MODE(ODBC 3.0)  
 指示驅動程式中非同步支援等級的 SQLUINTEGER 值:  
  
 SQL_AM_CONNECTION = 支援連接級非同步執行。 與給定連接句柄關聯的所有語句句柄都處於非同步模式,或者所有語句句柄都處於同步模式。 連接上的語句句柄不能處於非同步模式,而同一連接上的另一個語句句柄處於同步模式,反之亦然。  
  
 SQL_AM_STATEMENT = 支援語句級非同步執行。 與連接句柄關聯的某些語句句柄可能處於異步模式,而同一連接上的其他語句句柄處於同步模式。  
  
 不支援SQL_AM_NONE = 不支援非同步模式。  
  
 SQL_ASYNC_NOTIFICATION  
 指示驅動程式是否支援非同步通知的 SQLUINTEGER 值:  
  
-   **SQL_ASYNC_NOTIFICATION_CAPABLE**驅動程式支援非同步執行通知。  
  
-   **SQL_ASYNC_NOTIFICATION_NOT_CAPABLE**驅動程式不支援非同步執行通知。  
  
 ODBC 非同步操作分為兩類:連接級非同步操作和語句級非同步操作。  如果驅動程式返回SQL_ASYNC_NOTIFICATION_CAPABLE,它必須支援它可以通過非同步執行的所有API的通知。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 SQLUINTEGER 位掩碼,用於枚舉驅動程序相對於行計數的可用性的行為。 以下位遮罩與資訊型態使用:  
  
 SQL_BRC_ROLLED_UP = 連續插入、刪除或更新語句的行計數匯總為一個。 如果未設置此位,則行計數可用於每個語句。  
  
 SQL_BRC_PROCEDURES = 在存儲過程中執行批處理時,行計數(如果有)可用。 如果行計數可用,則它們可以匯總或單獨可用,具體取決於SQL_BRC_ROLLED_UP位。  
  
 SQL_BRC_EXPLICIT = 當通過調用 SQLExecute 或**SQLExecDirect**直接執行批處理時**SQLExecDirect**,行計數(如果有)可用。 如果行計數可用,則它們可以匯總或單獨可用,具體取決於SQL_BRC_ROLLED_UP位。  
  
 SQL_BATCH_SUPPORT (ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式對批處理的支援。 以下位遮罩支援哪個等級:  
  
 SQL_BS_SELECT_EXPLICIT = 驅動程式支援具有結果集生成語句的顯式批處理。  
  
 SQL_BS_ROW_COUNT_EXPLICIT = 驅動程式支援具有行計數生成語句的顯式批處理。  
  
 SQL_BS_SELECT_PROC = 驅動程式支援具有結果集生成語句的顯式過程。  
  
 SQL_BS_ROW_COUNT_PROC = 驅動程式支援具有行計數生成語句的顯式過程。  
  
 SQL_BOOKMARK_PERSISTENCE(ODBC 2.0)  
 SQLUINTEGER 位掩碼,枚舉書簽持續存在的操作。  
  
 以下位遮罩與標誌一起使用,以確定書籤保留的選項:  
  
 SQL_BP_CLOSE = 書籤在應用程式使用SQL_CLOSE選項呼叫**SQLFreeStmt**後有效,或者**SQLCloseCursor**關閉與語句關聯的遊標。  
  
 SQL_BP_DELETE = 刪除該行后,行的書籤有效。  
  
 SQL_BP_DROP = 書籤在應用程式呼叫**SQLFreeHandle**且*具有SQL_HANDLE_STMT的句柄類型*以刪除文句後有效。  
  
 SQL_BP_TRANSACTION = 書籤在應用程式提交或回滾事務後有效。  
  
 SQL_BP_UPDATE = 該行的書籤在該行中的任何列(包括鍵列)更新后有效。  
  
 SQL_BP_OTHER_HSTMT = 與一個語句關聯的書籤可以與另一個語句一起使用。 除非指定SQL_BP_CLOSE或SQL_BP_DROP,否則第一個語句上的游標必須打開。  
  
 SQL_CATALOG_LOCATION(ODBC 2.0)  
 指示目錄在限定表名稱中的位置的 SQLUSMALLINT 值:  
  
 SQL_CL_STARTSQL_CL_END  
  
 例如,Xbase 驅動程式返回SQL_CL_START因為目錄(目錄)名稱位於表名稱的開頭,如 [EMPDATA_EMP] 中所示。Dbf。 ORACLE 伺服器驅動程式傳回SQL_CL_END因為目錄位於表格中的末尾,ADMIN.EMP@EMPDATA如中 。  
  
 SQL-92 完全符合級別的驅動程序將始終返回SQL_CL_START。 如果數據源不支援目錄,則返回值 0。 要確定是否支援目錄,應用程式使用SQL_CATALOG_NAME資訊類型呼叫**SQLGetInfo。**  
  
 此*資訊類型*已重命名為 ODBC 3.0 從 ODBC 2.0*資訊類型*SQL_QUALIFIER_LOCATION。  
  
 SQL_CATALOG_NAME(ODBC 3.0)  
 字串字串:「Y」,如果伺服器支援目錄名稱,則不支援"N"。  
  
 SQL-92 完全符合級別的驅動程序將始終返回"Y"。  
  
 SQL_CATALOG_NAME_SEPARATOR(ODBC 1.0)  
 字串:資料來源定義為目錄名稱與目錄名稱之後或其後面的限定名稱元素之間的分隔符的字元或字元。  
  
 如果數據源不支援目錄,則返回空字串。 要確定是否支援目錄,應用程式使用SQL_CATALOG_NAME資訊類型呼叫**SQLGetInfo。** SQL-92 完全符合級別的驅動程序將始終返回。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_QUALIFIER_NAME_SEPARATOR重新命名為 ODBC 3.0。  
  
 SQL_CATALOG_TERM(ODBC 1.0)  
 具有目錄數據源供應商名稱的字串;例如,"資料庫"或"目錄"。 此字串可以是上部、下部或混合大小寫。  
  
 如果數據源不支援目錄,則返回空字串。 要確定是否支援目錄,應用程式使用SQL_CATALOG_NAME資訊類型呼叫**SQLGetInfo。** SQL-92 符合電平的驅動程序將始終返回"目錄"。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_QUALIFIER_TERM重新命名為 ODBC 3.0。  
  
 SQL_CATALOG_USAGE(ODBC 2.0)  
 SQLUINTEGER 位掩碼,枚舉了可以使用目錄的語句。  
  
 以下位遮罩目錄的使用位置:  
  
 SQL_CU_DML_STATEMENTS = 所有資料操作語言語句都支援目錄:**選擇**、**插入**、**更新**、**刪除**等,如果支援,**請選擇更新**並定位更新和刪除語句。  
  
 SQL_CU_PROCEDURE_INVOCATION = ODBC 過程呼叫語句中支援目錄。  
  
 SQL_CU_TABLE_DEFINITION = 所有表定義語片都支援目錄:**建立表**,**建立檢視**,**變更表****、 DROP TABLE**與 DROP**檢視**。  
  
 SQL_CU_INDEX_DEFINITION = 所有索引定義語句都支援目錄:**建立索引**與**DROP INDEX**。  
  
 SQL_CU_PRIVILEGE_DEFINITION = 所有權限定義語句都支援目錄 **:GRANT**和**REVOKE**。  
  
 如果數據源不支援目錄,則返回值 0。 要確定是否支援目錄,應用程式使用SQL_CATALOG_NAME資訊類型呼叫**SQLGetInfo。** SQL-92 符合電平的驅動程序將始終返回具有所有這些位集的位掩碼。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_QUALIFIER_USAGE重命名為 ODBC 3.0。  
  
 SQL_COLLATION_SEQ(ODBC 3.0)  
 排序規則序列的名稱。 這是一個字串,指示此伺服器的預設字元集的預設排序規則的名稱(例如,ISO 8859-1'或 EBCDIC)。 如果未知,將返回一個空字串。 SQL-92 符合電平的驅動程序將始終返回非空字串。  
  
 SQL_COLUMN_ALIAS(ODBC 2.0)  
 字串字串:「Y」,如果數據源支援列別名;如果數據源支援列別名,則為「Y」;否則,"N"。  
  
 列別名是可以使用 AS 子句為選擇清單中的列指定的替代名稱。 SQL-92 符合入門級的驅動程序將始終返回"Y"。  
  
 SQL_CONCAT_NULL_BEHAVIOR(ODBC 1.0)  
 SQLUSMALLINT 值,指示資料來源如何處理 NULL 值字元資料類型列與非 NULL 值字元資料類型列的串聯:  
  
 SQL_CB_NULL = 結果為 NULL 值。  
  
 SQL_CB_NON_NULL = 結果是非 NULL 值列或列的串聯。  
  
 SQL-92 符合入門級的驅動程序將始終返回SQL_CB_NULL。  
  
 SQL_CONVERT_BIGINTSQL_CONVERT_BINARYSQL_CONVERT_BITSQL_CONVERT_CHARSQL_CONVERT_GUIDSQL_CONVERT_DATESQL_CONVERT_DECIMALSQL_CONVERT_DOUBLESQL_CONVERT_FLOATSQL_CONVERT_INTEGERSQL_CONVERT_INTERVAL_YEAR_MONTHSQL_CONVERT_INTERVAL_DAY_TIMESQL_CONVERT_LONGVARBINARYSQL_CONVERT_LONGVARCHARSQL_CONVERT_NUMERICSQL_CONVERT_REALSQL_CONVERT_SMALLINTSQL_CONVERT_TIMESQL_CONVERT_TIMESTAMPSQL_CONVERT_TINYINTSQL_CONVERT_VARBINARYSQL_CONVERT_VARCHAR(ODBC 1.0)  
 SQLUINTEGER 位掩碼。 位遮罩資料來源支援的轉換,該函數具有**CONVERT**標量函數,用於*在 InfoType*中命名的類型的資料。 如果位掩碼等於零,數據源不支援從命名類型的數據進行任何轉換,包括轉換為相同的數據類型。  
  
 例如,要確定數據來源是否支援將SQL_INTEGER資料轉換為SQL_BIGINT資料類型,應用程式使用SQL_CONVERT_INTEGER*的資訊類型*呼叫**SQLGetInfo。** 應用程式對返回的位掩碼和SQL_CVT_BIGINT執行**AND**操作。 如果生成的值為非零,則支援轉換。  
  
 以下位遮罩支援哪些轉換:  
  
 SQL_CVT_BIGINT (ODBC 1.0) SQL_CVT_BINARY (ODBC 1.0) SQL_CVT_BIT (ODBC 1.0) SQL_CVT_GUID (ODBC 3.5) SQL_CVT_CHAR (ODBC 1.0) SQL_CVT_DATE (ODBC 1.0)SQL_CVT_DECIMAL (ODBC 1.0)SQL_CVT_DOUBLE (ODBC 1 .0)SQL_CVT_FLOAT (ODBC 1.0)SQL_CVT_INTEGER (ODBC 1.0)SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0)SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0)SQL_CVT_LONGVARBINARY (ODBC 1.0)SQL_CVT_LONGVARCHAR (ODBC 1.0)SQL_CVT_NUMERIC (ODBC 1.0)SQL_CVT_REAL ODBC 1.0)SQL_CVT_SMALLINT (ODBC 1.0)SQL_CVT_TIME (ODBC 1.0)SQL_CVT_TIMESTAMP (ODBC 1.0)SQL_CVT_TINYINT (ODBC 1.0)SQL_CVT_VARBINARY (ODBC 1.0)SQL_CVT_VARCHAR (ODBC 1.0)  
  
 SQL_CONVERT_FUNCTIONS(ODBC 1.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的標量轉換函數。  
  
 以下位遮罩支援哪些轉換函數:  
  
 SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT  
  
 SQL_CORRELATION_NAME(ODBC 1.0)  
 指示是否支援表關聯名稱的 SQLUSMALLINT 值:  
  
 SQL_CN_NONE = 不支援關聯名稱。  
  
 SQL_CN_DIFFERENT = 關聯名稱受支援,但必須不同於它們表示的表的名稱。  
  
 SQL_CN_ANY = 關聯名稱受支援,可以是任何有效的使用者定義的名稱。  
  
 SQL-92 符合入門級的驅動程序將始終返回SQL_CN_ANY。  
  
 SQL_CREATE_ASSERTION(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了**創建 ASSERTION**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CA_CREATE_ASSERTION  
  
 如果支援顯示式指定約束屬性的能力(請參閱SQL_ALTER_TABLE和SQL_CREATE_TABLE資訊類型),則以下位指定受支援的約束屬性:  
  
 SQL_CA_CONSTRAINT_INITIALLY_DEFERREDSQL_CA_CONSTRAINT_INITIALLY_IMMEDIATESQL_CA_CONSTRAINT_DEFERRABLESQL_CA_CONSTRAINT_NON_DEFERRABLE  
  
 SQL-92 完全符合級別的驅動程式將始終返回所有這些選項(如支援)。 返回值"0"表示不支援 CREATE **ASSERTION**語句。  
  
 SQL_CREATE_CHARACTER_SET(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了在 SQL-92 中定義的**CREATE 字元集**語句中子句,數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CCS_CREATE_CHARACTER_SETSQL_CCS_COLLATE_CLAUSESQL_CCS_LIMITED_COLLATION  
  
 SQL-92 完全符合級別的驅動程式將始終返回所有這些選項(如支援)。 返回值"0"表示不支援 CREATE**字元集**語句。  
  
 SQL_CREATE_COLLATION(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了**創建拼貼**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CCOL_CREATE_COLLATION  
  
 SQL-92 完全符合級別的驅動程式將始終返回此選項作為支援。 返回值"0"表示不支援 CREATE**拼貼**語句。  
  
 SQL_CREATE_DOMAIN(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了 CREATE **DOMAIN**語句中的條款,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CDO_CREATE_DOMAIN = 支援 CREATE DOMAIN 語句(中級級別)。  
  
 SQL_CDO_CONSTRAINT_NAME_DEFINITION \<= 命名域約束(中間級別)>支持约束名称定义。  
  
 以下位指定建立欄約束的能力:SQL_CDO_DEFAULT = 支援指定網域約束(中間等級)SQL_CDO_CONSTRAINT = 指定網域預設值(中間等級)SQL_CDO_COLLATION = 支援指定網列規則(完整等級)  
  
 如果支援指定網域約束(SQL_CDO_DEFAULT設定),則以下位指定受支援的約束屬性:  
  
 SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED(全級別)SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE(全級別)SQL_CDO_CONSTRAINT_DEFERRABLE(全級別)SQL_CDO_CONSTRAINT_NON_DEFERRABLE(全級)  
  
 返回值"0"表示不支援 CREATE **DOMAIN**語句。  
  
 SQL_CREATE_SCHEMA(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了**創建 SCHEMA**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CS_CREATE_SCHEMASQL_CS_AUTHORIZATIONSQL_CS_DEFAULT_CHARACTER_SET  
  
 SQL-92 符合級別的中間驅動程序將始終返回SQL_CS_CREATE_SCHEMA,並SQL_CS_AUTHORIZATION選項。 在 SQL-92 條目級別也必須支援這些語句,但不一定作為 SQL 語句。 SQL-92 完全符合級別的驅動程式將始終返回所有這些選項(如支援)。  
  
 SQL_CREATE_TABLE(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了**創建表**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CT_CREATE_TABLE = 支援建立表語句。 (入門級)  
  
 SQL_CT_TABLE_CONSTRAINT = 支援指定表規範(FIPS 過渡等級)  
  
 SQL_CT_CONSTRAINT_NAME_DEFINITION\<= 命名欄與表約束(中間等級)支援規範名稱定義>子句  
  
 以下位指定建立暫存表的能力:  
  
 SQL_CT_COMMIT_PRESERVE = 刪除的行在提交時保留。 (全階)SQL_CT_COMMIT_DELETE = 刪除的行在提交時被刪除。 (全階)SQL_CT_GLOBAL_TEMPORARY = 可以建立全域臨時表。 (全階)SQL_CT_LOCAL_TEMPORARY = 可以創建本地臨時表。 (全階)  
  
 以下位指定建立欄位的限制的能力:  
  
 SQL_CT_COLUMN_CONSTRAINT = 支援指定欄位約束(FIPS 過渡等級)SQL_CT_COLUMN_DEFAULT = 支援指定欄預設值 (FIPS 過渡等級) SQL_CT_COLUMN_COLLATION = 支援指定欄位規則(完整等級)  
  
 如果支援指定欄位或表約束,則以下位指定受支援的約束屬性:  
  
 SQL_CT_CONSTRAINT_INITIALLY_DEFERRED(全級別)SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE(全級別)SQL_CT_CONSTRAINT_DEFERRABLE(全級別)SQL_CT_CONSTRAINT_NON_DEFERRABLE(全級)  
  
 SQL_CREATE_TRANSLATION(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了**創建轉換**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CTR_CREATE_TRANSLATION  
  
 SQL-92 完全符合級別的驅動程式將始終返回這些選項(如支援)。 返回值"0"表示不支援 CREATE**轉換**語句。  
  
 SQL_CREATE_VIEW(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉了**創建視圖**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_CV_CREATE_VIEWSQL_CV_CHECK_OPTIONSQL_CV_CASCADEDSQL_CV_LOCAL  
  
 返回值"0"表示不支援 CREATE **VIEW**語句。  
  
 SQL-92 符合入門級的驅動程式將始終返回SQL_CV_CREATE_VIEW,並SQL_CV_CHECK_OPTION選項(  
  
 SQL-92 完全符合級別的驅動程式將始終返回所有這些選項(如支援)。  
  
 SQL_CURSOR_COMMIT_BEHAVIOR(ODBC 1.0)  
 SQLUSMALLINT 值,指示**COMMIT**操作如何影響數據源中的游標和已準備的語句(提交事務時數據源的行為)。  
  
 此屬性的值將反映下一個設置的當前狀態:SQL_COPT_SS_PRESERVE_CURSORS。  
  
 SQL_CB_DELETE = 關閉遊標並刪除準備好的語句。 要再次使用遊標,應用程式必須重新準備並重新執行語句。  
  
 SQL_CB_CLOSE = 關閉游標。 對於準備好的語句,應用程式可以在語句上調用**SQLExecute,** 而無需再次調用**SQLPrepare。** SQL ODBC 驅動程式的預設值為SQL_CB_CLOSE。 這意味著 SQL ODBC 驅動程式將在提交事務時關閉游標。  
  
 SQL_CB_PRESERVE = 將游標保留在與**COMMIT**操作之前相同的位置。 應用程式可以繼續提取數據,也可以關閉游標並重新執行語句,而無需重新準備它。  
  
 SQL_CURSOR_ROLLBACK_BEHAVIOR(ODBC 1.0)  
 SQLUSMALLINT 值,指示**ROLLBACK**操作如何影響資料來源中的遊標和已準備的語句:  
  
 SQL_CB_DELETE = 關閉遊標並刪除準備好的語句。 要再次使用遊標,應用程式必須重新準備並重新執行語句。  
  
 SQL_CB_CLOSE = 關閉游標。 對於準備好的語句,應用程式可以在語句上調用**SQLExecute,** 而無需再次調用**SQLPrepare。**  
  
 SQL_CB_PRESERVE = 將游標保留在與**ROLLBACK**操作之前相同的位置。 應用程式可以繼續提取數據,也可以關閉游標並重新執行語句,而無需重新準備它。  
  
 SQL_CURSOR_SENSITIVITY (ODBC 3.0)  
 指示對游標敏感度的支援的 SQLUINTEGER 值:  
  
 SQL_INSENSITIVE = 語句句柄上的所有遊標都顯示結果集,而不反映同一事務中任何其他游標對它所做的任何更改。  
  
 SQL_UNSPECIFIED = 未指定語句句柄上的游標是否使同一事務中另一個游標對結果集所做的更改可見。 語句句柄上的游標可能使任何、某些或所有此類更改都變得可見。  
  
 SQL_SENSITIVE = 游標對同一事務中其他游標所做的更改很敏感。  
  
 SQL-92 符合入門級的驅動程序將始終返回支援SQL_UNSPECIFIED選項。  
  
 SQL-92 完全符合級別的驅動程式將始終返回支援SQL_INSENSITIVE選項。  
  
 SQL_DATA_SOURCE_NAME(ODBC 1.0)  
 連線期間使用的具有資料源名稱的字串。 如果應用程式稱為**SQLConnect**,則這是*szDSN*參數的值。 如果應用程式稱為**SQLDriverConnect**或**SQLBrowseConnect,** 則這是傳遞給驅動程式的連接字串中的 DSN 關鍵字的值。 如果連接字串不包含**DSN**關鍵字(例如,當它包含**DRIVER**關鍵字時),則這是一個空字串。  
  
 SQL_DATA_SOURCE_READ_ONLY(ODBC 1.0)  
 字元字串。 如果數據源設置為"唯讀"模式,"N"(如果是否則)。  
  
 此特性僅與數據源本身有關;它不是啟用對數據源的驅動程式的特徵。 讀/寫驅動程式可與唯讀的資料來源一起使用。 如果驅動程式是唯讀的,則其所有資料源都必須為唯讀,並且必須返回SQL_DATA_SOURCE_READ_ONLY。  
  
 SQL_DATABASE_NAME(ODBC 1.0)  
 如果數據來源定義名為「資料庫」的命名物件,則具有目前資料庫名稱的字串。  
  
> [!NOTE]
>  在 ODBC 3 *.x*中,還可以透過呼叫**SQLGetConnectAttr**傳回此*InfoType*傳回的值,該*參數的屬性*參數為SQL_ATTR_CURRENT_CATALOG。  
  
 SQL_DATETIME_LITERALS(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,枚舉資料來源支援的 SQL-92 約會時間文本。 請注意,這些是 SQL-92 規範中列出的日期時間文本,與 ODBC 定義的日期時間文本轉義子句是分開的。 有關 ODBC 日期時間文字轉義子句的詳細資訊,請參閱[日期、時間和時間戳文字](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)。  
  
 FIPS 過渡電平一致性驅動程式將始終返回位掩碼中以下清單中位的"1"值。 值"0"表示不支援 SQL-92 約會時間文本。  
  
 以下位遮罩支援哪些文字:  
  
 SQL_DL_SQL92_DATESQL_DL_SQL92_TIMESQL_DL_SQL92_TIMESTAMPSQL_DL_SQL92_INTERVAL_YEARSQL_DL_SQL92_INTERVAL_MONTHSQL_DL_SQL92_INTERVAL_DAYSQL_DL_SQL92_INTERVAL_HOURSQL_DL_SQL92_INTERVAL_MINUTESQL_DL_SQL92_INTERVAL_SECONDSQL_DL_SQL92_INTERVAL_YEAR_TO_MONTHSQL_DL_SQL92_INTERVAL_DAY_TO_HOUR  
  
 SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTESQL_DL_SQL92_INTERVAL_DAY_TO_SECONDSQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTESQL_DL_SQL92_INTERVAL_HOUR_TO_SECONDSQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND  
  
 SQL_DBMS_NAME(ODBC 1.0)  
 驅動程式訪問的帶有 DBMS 產品名稱的字串。  
  
 SQL_DBMS_VER(ODBC 1.0)  
 指示驅動程式訪問的 DBMS 產品版本的字串。 版本是表單[.]*,其中前兩位數位是主要版本,后兩位數位是次要版本,最後四位數位是發佈版本。 驅動程序必須在此窗體中呈現 DBMS 產品版本,但還可以追加特定於 DBMS 的產品版本。 例如,"04.01.0000 Rdb 4.1"。  
  
 SQL_DDL_INDEX(ODBC 3.0)  
 指示對索引建立與刪除的 SQLUINTEGER 值:  
  
 SQL_DI_CREATE_INDEXSQL_DI_DROP_INDEX  
  
 SQL_DEFAULT_TXN_ISOLATION(ODBC 1.0)  
 一個 SQLUINTEGER 值,指示驅動程式或數據源支援的預設事務隔離等級,如果數據源不支援事務,則為零。 以下字語用於定義事務隔離等級:  
  
 **髒讀**事務 1 更改一行。 事務 2 在事務 1 提交更改之前讀取已更改的行。 如果事務 1 回滾更改,事務 2 將讀取被認為從未存在的行。  
  
 **無法重複讀取**事務 1 讀取一行。 事務2 更新或刪除該行並提交此更改。 如果事務 1 嘗試重讀該行,它將接收不同的行值或發現該行已被刪除。  
  
 **幻影**事務 1 讀取一組滿足某些搜尋條件的行。 事務 2 生成一個或多個行(通過插入或更新)與搜索條件匹配。 如果事務 1 重新執行讀取行的語句,它將接收一組不同的行。  
  
 如果資料來源支援事務,驅動程式將傳回以下位遮罩之一:  
  
 SQL_TXN_READ_UNCOMMITTED = 髒讀、不可重複讀取和幻像是可能的。  
  
 SQL_TXN_READ_COMMITTED = 無法進行髒讀。 不可重複讀取和幻像是可能的。  
  
 SQL_TXN_REPEATABLE_READ = 無法進行髒讀和不可重複讀取。 幻影是可能的。  
  
 SQL_TXN_SERIALIZABLE = 事務是可序列化的。 可序列化事務不允許髒讀、不可重複讀取或幻象。  
  
 SQL_DESCRIBE_PARAMETER(ODBC 3.0)  
 字元字串:「Y」,如果參數可以描述;"N",如果不是。  
  
 SQL-92 完全符合電平的驅動程式通常會返回"Y",因為它將支援 DESCRIBE **INPUT**語句。 但是,由於這不能直接指定基礎 SQL 支援,因此即使在 SQL-92 完全符合級別的驅動程式中,也不支援描述參數。  
  
 SQL_DM_VER(ODBC 3.0)  
 具有驅動程式管理器版本的字串。 版本是表單 [.]*,其中:  
  
 第一組兩位數位是主要 ODBC 版本,由常量SQL_SPEC_MAJOR給出。  
  
 第二組兩位數位是次要 ODBC 版本,由常量SQL_SPEC_MINOR給出。  
  
 第三組四位數位是驅動程式管理器的主要內部版本號。  
  
 最後一組四位數位是驅動程式管理員的次要內部版本號。  
  
 Windows 7 驅動程式管理器版本是 03.80。 Windows 8 驅動程式管理器版本是 03.81。  
  
 SQL_DRIVER_AWARE_POOLING_SUPPORTED (ODBC 3.8)  
 一個 SQLUINTEGER 值,指示驅動程式是否支援驅動程式感知池。 (有關詳細資訊,請參閱[驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。  
  
 SQL_DRIVER_AWARE_POOLING_CAPABLE表示驅動程式可以支援驅動程式感知池機制。  
  
 SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE表示驅動程式不支援驅動程式感知池機制。  
  
 驅動程式不需要實現SQL_DRIVER_AWARE_POOLING_SUPPORTED,駕駛員管理器將不尊重驅動程式的返回值。  
  
 SQL_DRIVER_HDBCSQL_DRIVER_HENV(ODBC 1.0)  
 SQLULEN 值,驅動程式的環境句柄或連接句柄,由參數*InfoType*確定。  
  
 這些信息類型僅由驅動程式管理員實現。  
  
 SQL_DRIVER_HDESC(ODBC 3.0)  
 SQLULEN 值,驅動程式的描述符句柄由驅動程式管理員的描述符句柄確定,必須\*在*應用程式中的 InfoValuePtr*中的輸入傳遞該值。 在這種情況下 *,InfoValuePtr*既是輸入參數,也是輸出參數。 在\**InfoValuePtr*中傳遞的輸入描述符句柄必須在*ConnectHandle*上顯式或隱式分配。  
  
 應用程式應在使用此資訊類型呼叫**SQLGetInfo**之前複製驅動程式管理器的描述符句柄,以確保該句柄不會在輸出時覆蓋。  
  
 此資訊類型僅由驅動程式管理員實現。  
  
 SQL_DRIVER_HLIB(ODBC 2.0)  
 SQLULEN 值,載入庫中*的 hinst*在 Microsoft Windows 作業系統上載入驅動程式 DLL 或在另一個作業系統上載入驅動程式 DLL 時傳回到驅動程式管理器。 該句柄僅對**SQLGetInfo**呼叫中指定的連接句柄有效。  
  
 此資訊類型僅由驅動程式管理員實現。  
  
 SQL_DRIVER_HSTMT(ODBC 1.0)  
 SQLULEN 值,驅動程式語句句柄由驅動程式管理器語句句柄確定,必須\*在*應用程式中的 InfoValuePtr*中的輸入傳遞該值。 在這種情況下 *,InfoValuePtr*既是輸入參數,也是輸出參數。 \**在 InfoValuePtr*中傳遞的輸入語句句柄必須在參數*ConnectHandle*上分配。  
  
 應用程式應在使用此資訊類型調用**SQLGetInfo**之前複製驅動程式管理器的語句句柄,以確保該句柄不會在輸出時被覆蓋。  
  
 此資訊類型僅由驅動程式管理員實現。  
  
 SQL_DRIVER_NAME(ODBC 1.0)  
 具有用於存取資料來源的驅動程式的檔案名的字串。  
  
 SQL_DRIVER_ODBC_VER(ODBC 2.0)  
 具有驅動程式支援的 ODBC 版本的字串。 版本是表單 #.#,其中前兩位數位是主要版本,後兩位數位是次要版本。 SQL_SPEC_MAJOR和SQL_SPEC_MINOR定義主要版本號和次要版本號。 對於本手冊中描述的 ODBC 版本,這些版本為 3 和 0,驅動程式應返回"03.00"。  
  
 ODBC 驅動程式管理員不會修改 SQLGetInfo(SQL_DRIVER_ODBC_VER) 的傳回值,以保持現有應用程式的向後相容性。 驅動程式指定將返回的值。 但是,當應用程式調用**SQLSetEnvAttr**將SQL_ATTR_ODBC_VERSION設置為 3.8 時,支援 C 資料類型擴展性的驅動程式必須返回 3.8(或更高)。 關於詳細資訊,請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 SQL_DRIVER_VER(ODBC 1.0)  
 具有驅動程式版本和可選的驅動程式說明的字串。 至少,版本是窗體 [.]*,其中前兩位數位是主要版本,接下來的兩位數位是次要版本,最後四位數位是發佈版本。  
  
 SQL_DROP_ASSERTION(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉在 SQL-92 中定義的**DROP ASSERTION**語句中子句,數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DA_DROP_ASSERTION  
  
 SQL-92 完全符合級別的驅動程式將始終返回此選項作為支援。  
  
 SQL_DROP_CHARACTER_SET(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉在 SQL-92 中定義的**DROP 字元集**語句中子句,數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DCS_DROP_CHARACTER_SET  
  
 SQL-92 完全符合級別的驅動程式將始終返回此選項作為支援。  
  
 SQL_DROP_COLLATION(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉在 SQL-92 中定義的**DROP COLLATION**語句中子句,數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DC_DROP_COLLATION  
  
 SQL-92 完全符合級別的驅動程式將始終返回此選項作為支援。  
  
 SQL_DROP_DOMAIN(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**DROP DOMAIN**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DD_DROP_DOMAINSQL_DD_CASCADESQL_DD_RESTRICT  
  
 SQL-92 中間等級一致性驅動程序將始終返回所有這些選項(如支援)。  
  
 SQL_DROP_SCHEMA(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**DROP SCHEMA**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DS_DROP_SCHEMASQL_DS_CASCADESQL_DS_RESTRICT  
  
 SQL-92 中間等級一致性驅動程序將始終返回所有這些選項(如支援)。  
  
 SQL_DROP_TABLE(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**DROP TABLE**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DT_DROP_TABLESQL_DT_CASCADESQL_DT_RESTRICT  
  
 FIPS 過渡電平符合性驅動程式將始終返回支援的所有這些選項。  
  
 SQL_DROP_TRANSLATION(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**DROP 轉換**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DTR_DROP_TRANSLATION  
  
 SQL-92 完全符合級別的驅動程式將始終返回此選項作為支援。  
  
 SQL_DROP_VIEW(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**DROP VIEW**語句中子句,如 SQL-92 中定義,由數據源支援。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_DV_DROP_VIEWSQL_DV_CASCADESQL_DV_RESTRICT  
  
 FIPS 過渡電平符合性驅動程式將始終返回支援的所有這些選項。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,用於描述驅動程式支援的動態游標的屬性。 此位掩碼包含屬性的第一個子集;對於第二個子集,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES2。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA1_NEXT = 當游標是動態游標時,對**SQLFetchScroll**的調用中支援SQL_FETCH_NEXT的*提取方向*參數。  
  
 SQL_CA1_ABSOLUTE = 當游標是動態游標時,對**SQLFetchScroll**的調用中支援 SQL_FETCH_FIRST、SQL_FETCH_LAST和SQL_FETCH_ABSOLUTE的*Fetch 方向*參數。 (要提取的行集與當前游標位置無關。  
  
 SQL_CA1_RELATIVE = 當游標是動態游標時,對**SQLFetchScroll**的調用中支援SQL_FETCH_PRIOR和SQL_FETCH_RELATIVE的*Fetch 方向*參數。 (要提取的行集取決於當前游標位置。 請注意,這與SQL_FETCH_NEXT分開,因為在僅轉發游標中,僅支援SQL_FETCH_NEXT。  
  
 SQL_CA1_BOOKMARK = 當游標是動態游標時,對**SQLFetchScroll**的調用中支援SQL_FETCH_BOOKMARK的*提取方向*參數。  
  
 SQL_CA1_LOCK_EXCLUSIVE = 當游標是動態游標時,對**SQLSetPos**的調用中支援 SQL_LOCK_EXCLUSIVE的*LockType*參數。  
  
 SQL_CA1_LOCK_NO_CHANGE = 當游標是動態游標時,對**SQLSetPos**的調用中支援 SQL_LOCK_NO_CHANGE的*LockType*參數。  
  
 SQL_CA1_LOCK_UNLOCK = 當游標是動態游標時,對**SQLSetPos**的調用中支援 SQL_LOCK_UNLOCK的*LockType*參數。  
  
 SQL_CA1_POS_POSITION = 當游標是動態游標時,對**SQLSetPos**的調用中支援SQL_POSITION*的操作*參數。  
  
 SQL_CA1_POS_UPDATE = 當游標是動態游標時,對**SQLSetPos**的調用中支援SQL_UPDATE*的操作*參數。  
  
 SQL_CA1_POS_DELETE = 當游標是動態游標時,對**SQLSetPos**的調用中支援SQL_DELETE*的操作*參數。  
  
 SQL_CA1_POS_REFRESH = 當游標是動態游標時,對**SQLSetPos**的調用中支援SQL_REFRESH*的操作*參數。  
  
 SQL_CA1_POSITIONED_UPDATE = 當游標是動態游標時,支援 SQL 語句的更新。 (SQL-92 符合入門級的驅動程序將始終返回此選項作為支援。  
  
 SQL_CA1_POSITIONED_DELETE = 當游標是動態游標時,支援 SQL 語句的刪除。 (SQL-92 符合入門級的驅動程序將始終返回此選項作為支援。  
  
 SQL_CA1_SELECT_FOR_UPDATE = 當游標是動態游標時,支援選擇更新 SQL 語句。 (SQL-92 符合入門級的驅動程序將始終返回此選項作為支援。  
  
 SQL_CA1_BULK_ADD = 當游標是動態游標時,對**SQLBulk 操作**的調用中支援SQL_ADD*的操作*參數。  
  
 SQL_CA1_BULK_UPDATE_BY_BOOKMARK = 當游標是動態游標時,對**SQLBulk 操作**的調用支援SQL_UPDATE_BY_BOOKMARK*的操作*參數。  
  
 SQL_CA1_BULK_DELETE_BY_BOOKMARK = 當游標是動態游標時,對**SQLBulk 操作**的調用中支援SQL_DELETE_BY_BOOKMARK*的操作*參數。  
  
 SQL_CA1_BULK_FETCH_BY_BOOKMARK = 當游標是動態游標時,對**SQLBulk 操作**的調用中支援SQL_FETCH_BY_BOOKMARK*的操作*參數。  
  
 SQL-92 中間等級一致性驅動程式通常會返回支援SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和SQL_CA1_RELATIVE選項,因為它支援通過嵌入式 SQL FETCH 語句滾動遊標。 但是,由於這不能直接確定基礎 SQL 支援,因此即使對於 SQL-92 符合級別的驅動程式,也不支援可滾動遊標。  
  
 SQL_DYNAMIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,用於描述驅動程式支援的動態游標的屬性。 此位掩碼包含屬性的第二個子集;有關第一個子集,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES1。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA2_READ_ONLY_CONCURRENCY = 支援唯讀動態遊標,不允許更新。 (可以SQL_CONCUR_READ_ONLY動態游標SQL_ATTR_CONCURRENCY語句屬性)。  
  
 SQL_CA2_LOCK_CONCURRENCY = 支援使用足夠確保可以更新行的最低水平的動態游標。 (可以SQL_CONCUR_LOCK動態游標SQL_ATTR_CONCURRENCY語句屬性。這些鎖必須與SQL_ATTR_TXN_ISOLATION連接屬性設置的事務隔離級別一致。  
  
 SQL_CA2_OPT_ROWVER_CONCURRENCY = 支援使用比較行版本的樂觀併發控件的動態游標。 (可以SQL_CONCUR_ROWVERSQL_ATTR_CONCURRENCY語句屬性。  
  
 SQL_CA2_OPT_VALUES_CONCURRENCY = 支援使用樂觀併發控件比較值的動態游標。 (可以SQL_CONCUR_VALUESSQL_ATTR_CONCURRENCY語句屬性。  
  
 SQL_CA2_SENSITIVITY_ADDITIONS = 添加的行對動態游標可見;游標可以滾動到這些行。 (將這些行添加到游標的位置與驅動程序相關。  
  
 SQL_CA2_SENSITIVITY_DELETIONS = 已刪除的行不再可用於動態游標,並且不會在結果集中留下「孔」;動態游標從已刪除的行滾動後,無法返回到該行。  
  
 SQL_CA2_SENSITIVITY_UPDATES = 對行的更新對動態游標可見;如果動態游標從中滾動並返回到更新的行,則游標返回的數據是更新的數據,而不是原始數據。  
  
 SQL_CA2_MAX_ROWS_SELECT = 當游標是動態游標時,SQL_ATTR_MAX_ROWS語句屬性會影響**SELECT**語句。  
  
 SQL_CA2_MAX_ROWS_INSERT = 當游標是動態游標時,SQL_ATTR_MAX_ROWS語句屬性會影響**INSERT**語句。  
  
 SQL_CA2_MAX_ROWS_DELETE = 當游標是動態游標時,SQL_ATTR_MAX_ROWS語句屬性會影響**DELETE**語句。  
  
 SQL_CA2_MAX_ROWS_UPDATE = 當游標是動態游標時,SQL_ATTR_MAX_ROWS語句屬性會影響**UPDATE**語句。  
  
 SQL_CA2_MAX_ROWS_CATALOG = 當游標是動態游標時,SQL_ATTR_MAX_ROWS語句屬性會影響**CATALOG**結果集。  
  
 SQL_CA2_MAX_ROWS_AFFECTS_ALL = 當游標是動態游標時,SQL_ATTR_MAX_ROWS語句屬性**CATALOG****SELECT**會影響**SELECT、INSERT、DELETE**和**UPDATE**語句以及**DELETE**CATALOG 結果集。  
  
 SQL_CA2_CRC_EXACT = 當游標是動態游標時,SQL_DIAG_CURSOR_ROW_COUNT診斷欄位中提供準確的行計數。  
  
 SQL_CA2_CRC_APPROXIMATE = 當游標是動態游標時,SQL_DIAG_CURSOR_ROW_COUNT診斷欄位中有近似行計數可用。  
  
 SQL_CA2_SIMULATE_NON_UNIQUE = 驅動程式不保證當游標是動態游標時,類比定位更新或刪除語句僅影響一行;保證這是應用程序的責任。 (如果語句影響多行 **,SQLExecute**或**SQLExecDirect**將返回 SQLSTATE 01001 [Cursor 操作衝突]。要設置此行為,應用程式調用**SQLSetStmtAttr,SQL_ATTR_SIMULATE_CURSOR**屬性設置為SQL_SC_NON_UNIQUE。  
  
 SQL_CA2_SIMULATE_TRY_UNIQUE = 驅動程式嘗試保證當游標是動態游標時,類比定位更新或刪除語句僅影響一行。 驅動程序始終執行此類語句,即使它們可能會影響多個行,例如沒有唯一鍵時。 (如果語句影響多行 **,SQLExecute**或**SQLExecDirect**將返回 SQLSTATE 01001 [Cursor 操作衝突]。要設置此行為,應用程式將**SQLSetStmtAttr**調用,SQL_ATTR_SIMULATE_CURSOR屬性設置為SQL_SC_TRY_UNIQUE。  
  
 SQL_CA2_SIMULATE_UNIQUE = 驅動程式保證當游標是動態游標時,類比定位更新或刪除語句將僅影響一行。 如果驅動程式無法保證給定語句的此操作 **,SQLExecDirect**或**SQLPrepare**返回 SQLSTATE 01001(Cursor 操作衝突)。 要設置此行為,應用程式調用**SQLSetStmtAttr,SQL_ATTR_SIMULATE_CURSOR**屬性設置為SQL_SC_UNIQUE。  
  
 SQL_EXPRESSIONS_IN_ORDERBY(ODBC 1.0)  
 字串:如果資料源支援 ORDER BY 列表中的運算式,則為"Y";如果數據源支援**ORDER BY**列表中的運算式,則為"Y";"N",如果它沒有。  
  
 SQL_FILE_USAGE(ODBC 2.0)  
 SQLUSMALLINT 值,指示單層驅動程式如何直接處理資料來源中的檔案:  
  
 SQL_FILE_NOT_SUPPORTED = 驅動程式不是單層驅動程式。 例如,ORACLE 驅動程式是雙層驅動程式。  
  
 SQL_FILE_TABLE = 單層驅動程式將資料來源中的檔案視為表。 例如,Xbase 驅動程式將每個 Xbase 檔案視為表。  
  
 SQL_FILE_CATALOG = 單層驅動程式將資料來源中的檔案視為目錄。 例如,Microsoft Access 驅動程式將每個 Microsoft Access 檔案視為一個完整的資料庫。  
  
 應用程式可能用它來確定使用者如何選擇數據。 例如,Xbase 使用者通常認為數據存儲在檔中,而 ORACLE 和 Microsoft Access 使用者通常認為數據存儲在表中。  
  
 當使用者選擇 Xbase 資料來源時,應用程式可以顯示 Windows 檔打開通用對話框;當使用者選擇 Xbase 資料來源時,應用程式可以顯示「Windows**檔案打開**」通用對話框。當使用者選擇 Microsoft Access 或 ORACLE 數據源時,應用程式可以顯示自定義**選擇表**對話方塊。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,用於描述驅動程式支援的僅轉發游標的屬性。 此位掩碼包含屬性的第一個子集;對於第二個子集,請參閱SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA1_NEXTSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有關這些位掩碼的說明,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES1(並在說明中用"僅前進游標"代替"動態游標")。  
  
 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,用於描述驅動程式支援的僅轉發游標的屬性。 此位掩碼包含屬性的第二個子集;對於第一個子集,請參閱SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有關這些位掩碼的說明,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES2(並在說明中用"僅前進游標"代替"動態游標")。  
  
 SQL_GETDATA_EXTENSIONS(ODBC 2.0)  
 SQLUINTEGER 位掩碼枚舉到**SQLGetData**上。  
  
 以下位遮罩與旗標一起使用,以確定驅動程式支援**SQLGetData**的通用延伸:  
  
 SQL_GD_ANY_COLUMN = **SQLGetData**可以調用任何未綁定列,包括最後一個綁定列之前的列。 請注意,除非還返回SQL_GD_ANY_ORDER,否則必須按升序按列數的順序調用列。  
  
 SQL_GD_ANY_ORDER = **SQLGetData**可以按任意順序調用未綁定列。 請注意,除非還返回SQL_GD_ANY_COLUMN,否則只能為最後一個綁定列之後的列調用**SQLGetData。**  
  
 SQL_GD_BLOCK = **SQLGetData**在使用**SQLSetPos**定位到該行後,可以調用數據塊中的任何行中的未綁定列(其中行集大小大於 1) 的數據。  
  
 SQL_GD_BOUND = 除了未綁定列之外,還可以為綁定列調用**SQLGetData。** 驅動程式無法返回此值,除非它還返回SQL_GD_ANY_COLUMN。  
  
 可以調用 SQL_GD_OUTPUT_PARAMS = **SQLGetData**來傳回輸出參數值。 有關詳細資訊,請參閱使用[SQLGetData 檢索輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
 **SQLGetData**需要僅從最後一個綁定列之後發生的未綁定列返回數據,按增加列數的順序調用,並且不在行塊中的行中。  
  
 如果驅動程式支援書籤(固定長度或可變長度),則必須支援在列 0 上調用**SQLGetData。** 無論驅動程式返回什麼來調用**SQLGetInfo,SQL_GETDATA_EXTENSIONS** *InfoType*都需要什麼,都需要這種支援。  
  
 SQL_GROUP_BY(ODBC 2.0)  
 SQLUSMALLINT 值,用於指定**GROUP BY**子句中的列與選擇清單中的非聚合列之間的關係:  
  
 SQL_GB_COLLATE = 可以在每個分組列的末尾指定**COLLATE**子句。 (ODBC 3.0)  
  
 不支援SQL_GB_NOT_SUPPORTED =**組 BY**子句。 (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP BY**子句必須包含選擇清單中的所有非聚合列。 它不能包含任何其他列。 例如,**按部門從員工組中選擇部門、最大值(工資)。** (ODBC 2.0)  
  
 SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP BY**子句必須包含選擇清單中的所有非聚合列。 它可以包含不在選擇清單中的欄。 例如,**按部門、年齡從員工組中選擇部門、最高(工資)。** (ODBC 2.0)  
  
 SQL_GB_NO_RELATION = GROUP **BY**子句中的列和選擇清單中的列不相關。 選擇清單中非分組的非聚合列的含義與數據源相關。 例如,**依單位、年齡從員工群組中選擇部門、薪酬**。 (ODBC 2.0)  
  
 SQL-92 符合入門級的驅動程序將始終返回支援SQL_GB_GROUP_BY_EQUALS_SELECT選項。 SQL-92 完全符合級別的驅動程式將始終返回支援SQL_GB_COLLATE選項。 如果沒有支援任何選項,資料源不支援**GROUP BY**子句。  
  
 SQL_IDENTIFIER_CASE(ODBC 1.0)  
 SQLUSMALLINT 值如下所示:  
  
 SQL_IC_UPPER = SQL 中的識別碼不區分大小寫,儲存在系統目錄中的大寫中。  
  
 SQL_IC_LOWER = SQL 中的識別碼不區分大小寫,儲存在系統目錄中的小寫中。  
  
 SQL_IC_SENSITIVE = SQL 中的識別碼區分大小寫,儲存在系統目錄中的混合情況下。  
  
 SQL_IC_MIXED = SQL 中的識別碼不區分大小寫,儲存在系統目錄中的混合情況下。  
  
 由於 SQL-92 中的標識符從不區分大小寫,因此嚴格遵循 SQL-92(任何級別)的驅動程式永遠不會返回受支援的SQL_IC_SENSITIVE選項。  
  
 SQL_IDENTIFIER_QUOTE_CHAR(ODBC 1.0)  
 用作 SQL 語句中引用(分隔)識別符的開始和結束分隔符號的字串。 (作為 ODBC 函數的參數傳遞給的標識符不必引用。如果數據源不支援引號標識符,則返回空白。  
  
 當連接屬性SQL_ATTR_METADATA_ID設置為SQL_TRUE時,此字串還可用於引用目錄函數參數。  
  
 由於 SQL-92 中的標識符引號字元是雙引號 (),因此嚴格遵守 SQL-92 的驅動程式將始終返回雙引號字元。  
  
 SQL_INDEX_KEYWORDS(ODBC 3.0)  
 SQLUINTEGER 位罩,用於枚舉驅動程式支援的 CREATE INDEX 語句中的關鍵字:  
  
 SQL_IK_NONE = 不支援任何關鍵字。  
  
 SQL_IK_ASC = 支援 ASC 關鍵字。  
  
 SQL_IK_DESC = 支援 DESC 關鍵字。  
  
 SQL_IK_ALL = 支援所有關鍵字。  
  
 要查看是否支援 CREATE INDEX 語句,應用程式使用SQL_DLL_INDEX資訊類型呼叫**SQLGetInfo。**  
  
 SQL_INFO_SCHEMA_VIEWS(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式支援的INFORMATION_SCHEMA中的視圖。 INFORMATION_SCHEMA中的檢視和內容在 SQL-92 中定義。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩支援哪些檢視:  
  
 SQL_ISV_ASSERTIONS = 標識由給定用戶擁有的目錄斷言。 (全階)  
  
 SQL_ISV_CHARACTER_SETS = 識別給定使用者可以存取的目錄的字元集。 (中級)  
  
 SQL_ISV_CHECK_CONSTRAINTS = 標識給定用戶擁有的 CHECK 約束。 (中級)  
  
 SQL_ISV_COLLATIONS = 標識給定使用者可以存取的目錄的字元排序規則。 (全階)  
  
 SQL_ISV_COLUMN_DOMAIN_USAGE = 標識目錄的列,這些列取決於目錄中定義的域,並且由給定用戶擁有。 (中級)  
  
 SQL_ISV_COLUMN_PRIVILEGES = 標識給定使用者可用或授予的持久表列上的許可權。 (FIPS 過渡等級)  
  
 SQL_ISV_COLUMNS = 標識給定使用者可以存取的持久表的列。 (FIPS 過渡等級)  
  
 SQL_ISV_CONSTRAINT_COLUMN_USAGE = 與CONSTRAINT_TABLE_USAGE視圖類似,列標識給定用戶擁有的各種約束。 (中級)  
  
 SQL_ISV_CONSTRAINT_TABLE_USAGE = 標識約束(引用、唯一和斷言)使用的表,並且由給定用戶擁有。 (中級)  
  
 SQL_ISV_DOMAIN_CONSTRAINTS = 標識給定使用者可以存取的網域約束(目錄中的網域)。 (中級)  
  
 SQL_ISV_DOMAINS = 識別目錄中定義的使用者可以存取的網域。 (中級)  
  
 SQL_ISV_KEY_COLUMN_USAGE = 標識目錄中定義的由給定用戶作為鍵約束的列。 (中級)  
  
 SQL_ISV_REFERENTIAL_CONSTRAINTS = 標識給定用戶擁有的引用約束。 (中級)  
  
 SQL_ISV_SCHEMATA = 標識給定用戶擁有的架構。 (中級)  
  
 SQL_ISV_SQL_LANGUAGES = 識別 SQL 支援支援的 SQL 一致性等級、選項和方言。 (中級)  
  
 SQL_ISV_TABLE_CONSTRAINTS = 標識給定用戶擁有的表約束。 (中級)  
  
 SQL_ISV_TABLE_PRIVILEGES = 標識給定使用者可用或授予的持久表上的許可權。 (FIPS 過渡等級)  
  
 SQL_ISV_TABLES = 標識目錄中定義的持久表,該表可以由給定用戶訪問。 (FIPS 過渡等級)  
  
 SQL_ISV_TRANSLATIONS = 標識給定使用者可以存取的目錄的字元轉換。 (全階)  
  
 SQL_ISV_USAGE_PRIVILEGES = 識別給定使用者可用或擁有的目錄物件的 USAGE 許可權。 (FIPS 過渡等級)  
  
 SQL_ISV_VIEW_COLUMN_USAGE = 標識給定用戶擁有的目錄視圖所依賴的列。 (中級)  
  
 SQL_ISV_VIEW_TABLE_USAGE = 標識給定用戶擁有的目錄視圖所依賴的表。 (中級)  
  
 SQL_ISV_VIEWS = 識別此目錄中定義的由給定使用者可以訪問的已查看的表。 (FIPS 過渡等級)  
  
 SQL_INSERT_STATEMENT(ODBC 3.0)  
 指示對**插入**語句支援的 SQLUINTEGER 位元遮罩:  
  
 SQL_IS_INSERT_LITERALS  
  
 SQL_IS_INSERT_SEARCHED  
  
 SQL_IS_SELECT_INTO  
  
 SQL-92 符合入門級的驅動程序將始終返回所有這些選項(如支援)。  
  
 SQL_INTEGRITY(ODBC 1.0)  
 字串:如果數據源支援完整性增強工具,則為「Y」;"N",如果它沒有。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_ODBC_SQL_OPT_IEF重命名為 ODBC 3.0。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,用於描述驅動程式支援的鍵集游標的屬性。 此位掩碼包含屬性的第一個子集;對於第二個子集,請參閱SQL_KEYSET_CURSOR_ATTRIBUTES2。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有關這些位掩碼的說明,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES1(並在說明中用"鍵集驅動游標"代替"動態游標")。  
  
 SQL-92 中間等級一致性驅動程式通常會返回SQL_CA1_NEXT、SQL_CA1_ABSOLUTE和SQL_CA1_RELATIVE選項(如支援),因為驅動程式支援通過嵌入式 SQL FETCH 語句滾動遊標。 但是,由於這不能直接確定基礎 SQL 支援,因此即使對於 SQL-92 符合級別的驅動程式,也不支援可滾動遊標。  
  
 SQL_KEYSET_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 一個 SQLUINTEGER 位罩,用於描述驅動程式支援的鍵集游標的屬性。 此位掩碼包含屬性的第二個子集;有關第一個子集,請參閱SQL_KEYSET_CURSOR_ATTRIBUTES1。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有關這些位掩碼的說明,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES1(並在說明中用"鍵集驅動游標"代替"動態游標")。  
  
 SQL_KEYWORDS(ODBC 2.0)  
 包含所有資料來源特定關鍵字的逗號分隔清單的字串。 此清單不包含特定於 ODBC 的關鍵字或資料源和 ODBC 使用的關鍵字。 此清單表示所有保留的關鍵字;可互通的應用程式不應在物件名稱中使用這些單詞。  
  
 有關 ODBC 關鍵字的清單,請參閱附錄 C 中的[保留關鍵字](../../../odbc/reference/appendixes/reserved-keywords.md)[:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 **#define**值SQL_ODBC_KEYWORDS包含 ODBC 關鍵字的逗號分隔清單。  
  
 附錄 C：SQL 文法  
  
 SQL_LIKE_ESCAPE_CLAUSE(ODBC 2.0)  
 字串:如果數據源支援百分比字元 (%) 的轉義字元,"Y"和下劃線字元 (*) 在**LIKE**謂詞和驅動程式支援 ODBC 語法定義**LIKE**謂詞轉義字元;否則為"N"。  
  
 SQL_MAX_ASYNC_CONCURRENT_STATEMENTS(ODBC 3.0)  
 SQLUINTEGER 值,用於指定驅動程式在給定連接上支援的最大活動併發語句數。 如果沒有特定限制或限制未知,則此值為零。  
  
 SQL_MAX_BINARY_LITERAL_LEN(ODBC 2.0)  
 SQLUINTEGER 值,用於指定 SQL 語句中二進位元文字的最大長度(十六進位元數,不包括**SQLGetTypeInfo**返回的文本首碼和後綴)。 例如,二進位文本 0xFFAA 的長度為 4。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 SQL_MAX_CATALOG_NAME_LEN(ODBC 1.0)  
 指定數據源中目錄名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 FIPS 全電平符合性驅動程式將返回至少 128。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_MAX_QUALIFIER_NAME_LEN重新命名為 ODBC 3.0。  
  
 SQL_MAX_CHAR_LITERAL_LEN(ODBC 2.0)  
 SQLUINTEGER 值,用於指定 SQL 語句中字元文字的最大長度(字元數,不包括**SQLGetTypeInfo**傳回的文字前置碼和後綴)。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 SQL_MAX_COLUMN_NAME_LEN(ODBC 1.0)  
 指定數據源中列名的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 18 個。 FIPS 中級電平符合性驅動程式將返回至少 128。  
  
 SQL_MAX_COLUMNS_IN_GROUP_BY(ODBC 2.0)  
 指定**GROUP BY**子句中允許的最大列數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少6個。 FIPS 中級級別符合要求的驅動程式將返回至少 15 個。  
  
 SQL_MAX_COLUMNS_IN_INDEX(ODBC 2.0)  
 指定索引中允許的最大列數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 SQL_MAX_COLUMNS_IN_ORDER_BY(ODBC 2.0)  
 指定**ORDER BY**子句中允許的最大列數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少6個。 FIPS 中級級別符合要求的驅動程式將返回至少 15 個。  
  
 SQL_MAX_COLUMNS_IN_SELECT(ODBC 2.0)  
 指定選擇清單中允許的最大列數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 100 個。 FIPS 中級電平符合性驅動程式將返回至少 250 個。  
  
 SQL_MAX_COLUMNS_IN_TABLE(ODBC 2.0)  
 指定表中允許的最大列數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 100 個。 FIPS 中級電平符合性驅動程式將返回至少 250 個。  
  
 SQL_MAX_CONCURRENT_ACTIVITIES(ODBC 1.0)  
 SQLUSMALLINT 值,用於指定驅動程式可以支援連接的最大活動語句數。 如果語句的結果掛起,則語句定義為活動,術語"結果"表示**SELECT**操作中的行或受**INSERT、UPDATE**或**DELETE**操作(如行計數)影響的行,或者如果該**UPDATE**語句處於NEED_DATA狀態。 此值可以反映驅動程式或數據源施加的限制。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 此*資訊類型*已重新命名為 ODBC 3.0 從 ODBC 2.0*資訊類型*SQL_ACTIVE_STATEMENTS。  
  
 SQL_MAX_CURSOR_NAME_LEN(ODBC 1.0)  
 指定數據源中游標名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 18 個。 FIPS 中級電平符合性驅動程式將返回至少 128。  
  
 SQL_MAX_DRIVER_CONNECTIONS(ODBC 1.0)  
 SQLUSMALLINT 值,用於指定驅動程式可以支援環境的最大活動連接數。 此值可以反映驅動程式或數據源施加的限制。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 此*資訊類型*已重新命名為 ODBC 3.0 從 ODBC 2.0*資訊類型*SQL_ACTIVE_CONNECTIONS。  
  
 SQL_MAX_IDENTIFIER_LEN(ODBC 3.0)  
 一種 SQLUSMALLINT,用於指示數據來源支援使用者定義名稱的最大大小字元。  
  
 FIPS 符合等級的驅動程式將返回至少 18 個。 FIPS 中級電平符合性驅動程式將返回至少 128。  
  
 SQL_MAX_INDEX_SIZE(ODBC 2.0)  
 指定索引組合欄位中允許的最大位元組數的 SQLUINTEGER 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 SQL_MAX_PROCEDURE_NAME_LEN(ODBC 1.0)  
 指定數據源中過程名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 SQL_MAX_ROW_SIZE(ODBC 2.0)  
 指定表中單個行的最大長度的 SQLUINTEGER 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 FIPS 入門級符合要求的驅動程式將返回至少 2,000。 FIPS 中級級別符合要求的驅動程式將返回至少 8,000。  
  
 SQL_MAX_ROW_SIZE_INCLUDES_LONG(ODBC 3.0)  
 字串:如果為SQL_MAX_ROW_SIZE資訊類型返回的最大行大小包括行中所有SQL_LONGVARCHAR和SQL_LONGVARBINARY列的長度,"Y";否則為"N"。  
  
 SQL_MAX_SCHEMA_NAME_LEN(ODBC 1.0)  
 指定數據源中架構名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 18 個。 FIPS 中級電平符合性驅動程式將返回至少 128。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_MAX_OWNER_NAME_LEN重新命名為 ODBC 3.0。  
  
 SQL_MAX_STATEMENT_LEN(ODBC 2.0)  
 指定 SQL 語句的最大長度(字元數,包括空格)的 SQLUINTEGER 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 SQL_MAX_TABLE_NAME_LEN(ODBC 1.0)  
 指定數據源中表名稱的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 18 個。 FIPS 中級電平符合性驅動程式將返回至少 128。  
  
 SQL_MAX_TABLES_IN_SELECT(ODBC 2.0)  
 指定**SELECT**語句 FROM 的**FROM**子句中允許的最大表數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 FIPS 符合等級的驅動程式將返回至少 15 個。 FIPS 中級級別符合要求的驅動程式將返回至少 50 個。  
  
 SQL_MAX_USER_NAME_LEN(ODBC 2.0)  
 指定數據源中使用者名的最大長度的 SQLUSMALLINT 值。 如果沒有最大長度或長度未知,則此值設置為零。  
  
 SQL_MULT_RESULT_SETS(ODBC 1.0)  
 字串字串:「Y」,如果數據源支援多個結果集,則"N"(如果不支援)。  
  
 有關多個結果集的詳細資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)集。  
  
 SQL_MULTIPLE_ACTIVE_TXN(ODBC 1.0)  
 字串字串:「Y」如果驅動程式同時支援多個活動事務,「N」如果在任何時候只能有一個事務處於活動狀態。  
  
 為此資訊類型返回的資訊不適用於分散式事務。  
  
 SQL_NEED_LONG_DATA_LEN(ODBC 2.0)  
 字串:如果數據源需要長數據值的長度(數據類型為SQL_LONGVARCHAR、SQL_LONGVARBINARY 或長數據源特定的數據類型)的長度,則"Y"將該值發送到數據源,如果沒有,則為"N"。 有關詳細資訊,請參閱[SQLBind 參數函數](../../../odbc/reference/syntax/sqlbindparameter-function.md)與[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
 SQL_NON_NULLABLE_COLUMNS(ODBC 1.0)  
 SQLUSMALLINT 值,用於指定資料來源是否支援列中的非 NULL:  
  
 SQL_NNC_NULL = 所有列都必須為空。  
  
 SQL_NNC_NON_NULL = 列不能為空。 (資料來源支援**CREATE TABLE**語句中的 **'非 NULL"** 欄位約束。  
  
 SQL-92 符合入門級的驅動程式將返回SQL_NNC_NON_NULL。  
  
 SQL_NULL_COLLATION(ODBC 2.0)  
 SQLUSMALLINT 值,用於指定在結果集中對 NUL 的排序位置:  
  
 SQL_NC_END = NUL 在結果集的末尾排序,而不考慮 ASC 或 DESC 關鍵字。  
  
 SQL_NC_HIGH = NUL 在結果集的高端排序,具體取決於 ASC 或 DESC 關鍵字。  
  
 SQL_NC_LOW = NUL 在結果集的低端排序,具體取決於 ASC 或 DESC 關鍵字。  
  
 SQL_NC_START = NUL 在結果集的開頭進行排序,而不考慮 ASC 或 DESC 關鍵字。  
  
 SQL_NUMERIC_FUNCTIONS(ODBC 1.0)  
 注意:資訊類型在 ODBC 1.0 中引入;每個位掩碼都標有引入它的版本。  
  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的標量數位函數。  
  
 以下位遮罩支援哪些數值函數:  
  
 SQL_FN_NUM_ABS (ODBC 1.0)SQL_FN_NUM_ACOS (ODBC 1.0)SQL_FN_NUM_ASIN (ODBC 1.0)SQL_FN_NUM_ATAN (ODBC 1.0)SQL_FN_NUM_ATAN2 (ODBC 1.0)SQL_FN_NUM_CEILING (ODBC 1.0)SQL_FN_NUM_COS (ODBC 1.0)SQL_FN_NUM_COT (ODBC 1 .0)SQL_FN_NUM_DEGREES (ODBC 1.0)SQL_FN_NUM_EXP (ODBC 1.0)SQL_FN_NUM_FLOOR(ODBC 1.0)SQL_FN_NUM_LOG(ODBC 1.0)SQL_FN_NUM_LOG10(ODBC 1.0)SQL_FN_NUM_LOG10(ODBC 1.0)SQL_FN_NUM_LOG10(ODBC 1.0)SQL_FN_NUM_MOD (ODBC 1.0)SQL_FN_NUM_PI (ODBC 1.0)SQL_FN_NUM_POWER (ODBC 2.0)SQL_FN_NUM_RADIANS (ODBC 2.0)SQL_FN_NUM_RAND (ODBC 1.0)SQL_FN_NUM_ROUND (ODBC 2.0)SQL_FN_NUM_SIGN (ODBC 1.0)SQL_FN_NUM_SIN (ODBC 1.0)SQL_FN_NUM_SQRT (ODBC 1.0)SQL_FN_NUM_TAN(ODBC 1.0)SQL_FN_NUM_TRUNCATE(ODBC 1.0)SQL_FN_NUM_TRUNCATE(ODBC 2.0)  
  
 SQL_ODBC_INTERFACE_CONFORMANCE(ODBC 3.0)  
 一個 SQLUINTEGER 值,指示驅動程式符合的 ODBC 3 *.x*介面的級別。  
  
 SQL_OIC_CORE:所有 ODBC 驅動程式應遵守的最低水準。 此級別包括基本介面元素,如連接函數、用於準備和執行 SQL 語句的函數、基本結果集元數據函數、基本目錄函數等。  
  
 SQL_OIC_LEVEL1:包含核心標準合規性級別功能的級別,以及可滾動的游標、書籤、定位更新和刪除等。  
  
 SQL_OIC_LEVEL2:包括 1 級標準符合性級別功能以及高級功能(如敏感游標)的級別;按書籤更新、刪除和刷新;存儲程式支援;主鍵和外鍵的目錄函數;多目錄支援;等等。  
  
 有關詳細資訊,請參閱[介面一致性級別](../../../odbc/reference/develop-app/interface-conformance-levels.md)。  
  
 SQL_ODBC_VER(ODBC 1.0)  
 具有驅動程式管理員符合的 ODBC 版本的字串。 版本是表單 #._._.0000,其中前兩位數位是主要版本,後兩位數位是次要版本。 這僅在驅動程式管理器中實現。  
  
 SQL_OJ_CAPABILITIES(ODBC 2.01)  
 一個 SQLUINTEGER 位元遮罩,枚舉驅動程式和資料來源支援的外部聯接的類型。 以下位遮罩要決定哪些型態受支援:  
  
 SQL_OJ_LEFT = 支援左外部聯接。  
  
 SQL_OJ_RIGHT = 支援右外部聯接。  
  
 SQL_OJ_FULL = 支援完全外部聯接。  
  
 SQL_OJ_NESTED = 支援嵌套外部聯接。  
  
 SQL_OJ_NOT_ORDERED = 外部聯接的 ON 子句中的列名稱不必與**OUTER JOIN**子句中的相應表名的順序相同。  
  
 SQL_OJ_INNER = 內部表(左外部聯接中的右表或右外部聯接中的左表)也可以在內部聯接中使用。 這不適用於沒有內部表的完整外部聯接。  
  
 SQL_OJ_ALL_COMPARISON_OPS = ON 子句中的比較運算元可以是任何 ODBC 比較運算符。 如果未設置此位,則外部聯接中只能使用等 (*) 比較運算符。  
  
 如果未返回這些選項作為支援,則不支援外部聯接子句。  
  
 有關 SQL-92 定義的 SELECT 語句中關係聯接運算符的支援的資訊,請參閱SQL_SQL92_RELATIONAL_JOIN_OPERATORS。  
  
 SQL_ORDER_BY_COLUMNS_IN_SELECT(ODBC 2.0)  
 字串:如果 ORDER BY 子句中的列必須位於選擇清單中,則為"Y";如果**ORDER BY**子句中的列必須位於選擇清單中,則為"Y";否則,"N"。  
  
 SQL_PARAM_ARRAY_ROW_COUNTS(ODBC 3.0)  
 在參數化執行中,對驅動程式的屬性進行枚舉,瞭解行計數的可用性。 具有以下值:  
  
 SQL_PARC_BATCH = 每個參數集都可用於單個行計數。 這在概念上等效於生成一批 SQL 語句的驅動程式,該語句針對陣列中設置的每個參數一個。 可以使用SQL_PARAM_STATUS_PTR描述符欄位檢索擴展的錯誤資訊。  
  
 SQL_PARC_NO_BATCH = 只有一個行計數可用,即執行整個參數陣列的語句所產生的累積行計數。 這在概念上等效於將語句與完整參數陣列一起作為一個原子單元處理。 錯誤的處理方式與執行一個語句相同。  
  
 SQL_PARAM_ARRAY_SELECTS(ODBC 3.0)  
 一個 SQLUINTEGER,枚舉驅動程式的屬性,說明參數化執行中結果集的可用性。 具有以下值:  
  
 SQL_PAS_BATCH = 每組參數都有一個結果集可用。 這在概念上等效於生成一批 SQL 語句的驅動程式,該語句針對陣列中設置的每個參數一個。  
  
 SQL_PAS_NO_BATCH = 只有一個結果集可用,它表示執行整個參數陣列的語句所產生的累積結果集。 這在概念上等效於將語句與完整參數陣列一起作為一個原子單元處理。  
  
 SQL_PAS_NO_SELECT = 驅動程式不允許使用參數陣列執行結果集生成語句。  
  
 SQL_PROCEDURE_TERM(ODBC 1.0)  
 具有過程的數據源供應商名稱的字串;例如,"數據庫過程"、"存儲過程"、"過程"、"包"或"存儲查詢"。  
  
 SQL_PROCEDURES(ODBC 1.0)  
 字串字串:「Y」,如果數據源支援過程,並且驅動程式支援 ODBC 過程呼叫語法;如果資料源支援過程呼叫語法,則為「Y」,否則為"N"。  
  
 SQL_POS_OPERATIONS(ODBC 2.0)  
 在**SQLSetPos**中枚舉支援操作的 SQLINTEGER 位掩碼。  
  
 以下位掩碼與標誌一起使用,以確定支援哪些選項。  
  
 SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)  
  
 SQL_QUOTED_IDENTIFIER_CASE(ODBC 2.0)  
 SQLUSMALLINT 值如下所示:  
  
 SQL_IC_UPPER = SQL 中的參考識別子不區分大小寫,儲存在系統目錄中的大寫中。  
  
 SQL_IC_LOWER = SQL 中的參考識別碼不區分大小寫,儲存在系統目錄中小寫。  
  
 SQL_IC_SENSITIVE = SQL 中的參考識別符區分大小寫,存儲在系統目錄中的混合情況下。 (在符合 SQL-92 的資料庫中,引用的標識符始終對大小寫敏感。  
  
 SQL_IC_MIXED = SQL 中的引用識別碼不區分大小寫,儲存在系統目錄中的混合情況下。  
  
 SQL-92 符合入門級的驅動程序將始終返回SQL_IC_SENSITIVE。  
  
 SQL_ROW_UPDATES(ODBC 1.0)  
 字串:「Y」,如果鍵集驅動或混合游標維護所有提取行的行版本或值,因此可以檢測自上次提取該行以來任何使用者對行所做的任何更新。 (這僅適用於更新,不適用於刪除或插入。呼叫**SQLFetchScroll**時,驅動程式可以將SQL_ROW_UPDATED標誌返回到行狀態陣列。 否則,"N"。  
  
 SQL_SCHEMA_TERM(ODBC 1.0)  
 具有數據源供應商名稱的架構的字串;例如,"擁有者"、"授權ID"或"架構"。  
  
 字元字串可以在上部、下部或混合情況下返回。  
  
 SQL-92 符合入門級的驅動程序將始終返回"架構"。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_OWNER_TERM重命名為 ODBC 3.0。  
  
 SQL_SCHEMA_USAGE(ODBC 2.0)  
 SQLUINTEGER 位元,enk:enctt,可以使用架構的語句:  
  
 SQL_SU_DML_STATEMENTS = 架構在所有資料操作語言語句中都受支援:**選擇**、**插入**、**更新**、**刪除**等,如果支援,**請選擇更新**並定位更新和刪除語句。  
  
 SQL_SU_PROCEDURE_INVOCATION = ODBC 過程呼叫敘述支援架構。  
  
 SQL_SU_TABLE_DEFINITION = 所有表定義語片都支援架構:**建立表**,**建立檢視**、**變更表****、DROP TABLE**與 DROP**檢視**。  
  
 SQL_SU_INDEX_DEFINITION = 所有索引定義語句都支援架構:**建立索引**與**DROP INDEX**。  
  
 SQL_SU_PRIVILEGE_DEFINITION = 所有權限定義語句都支援架構 **:GRANT**和**REVOKE**。  
  
 SQL-92 符合入門級的驅動程序將始終返回SQL_SU_DML_STATEMENTS、SQL_SU_TABLE_DEFINITION和SQL_SU_PRIVILEGE_DEFINITION選項(如支援)。  
  
 此*資訊類型*已從 ODBC 2.0*資訊類型*SQL_OWNER_USAGE重新命名為 ODBC 3.0。  
  
 SQL_SCROLL_OPTIONS(ODBC 1.0)  
 注意:資訊類型在 ODBC 1.0 中引入;每個位掩碼都標有引入它的版本。  
  
 SQLUINTEGER 位掩碼,枚舉可滾動游標支援的滾動選項。  
  
 以下位遮罩要決定哪些選項受支援:  
  
 SQL_SO_FORWARD_ONLY = 游標僅向前滾動。 (ODBC 1.0)  
  
 SQL_SO_STATIC = 結果集中的數據是靜態的。 (ODBC 2.0)  
  
 SQL_SO_KEYSET_DRIVEN = 驅動程式保存並使用結果集中每行的鍵。 (ODBC 1.0)  
  
 SQL_SO_DYNAMIC = 驅動程式保留行集中每行的鍵(鍵集大小與行集大小相同)。 (ODBC 1.0)  
  
 SQL_SO_MIXED = 驅動程式保留鍵集中每行的鍵,並且鍵集大小大於行集大小。 游標在鍵集中內鍵集驅動,在鍵集外部動態。 (ODBC 1.0)  
  
 有關可滾動游標的資訊,請參閱[可捲軸游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 SQL_SEARCH_PATTERN_ESCAPE(ODBC 1.0)  
 指定驅動程式支援哪些內容的字串,允許使用模式符合元字元下劃線 (*) 和百分比符號 (%)作為搜索模式中的有效字元。 此轉義字元僅適用於支援搜索字串的目錄函數參數。 如果此字串為空,則驅動程式不支援搜索模式轉義字元。  
  
 由於此資訊類型不表示**LIKE**謂詞中轉義字元的一般支援,因此 SQL-92 不包括對此字元字串的要求。  
  
 此資訊*類型*僅限於目錄函數。 有關在搜尋模式字串中使用轉義元的說明,請參閱[模式值參數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 SQL_SERVER_NAME(ODBC 1.0)  
 具有實際數據來源特定伺服器名稱的字串;在**SQLConnect** **、SQLDriverConnect****和**( .  
  
 SQL_SPECIAL_CHARACTERS(ODBC 2.0)  
 一個字串,其中包含數據源上可用於標識符名稱(如表名、列名或索引名稱)的所有特殊字元(即除 z、A 到 Z、0 到 Z 和下劃線之外的所有字元)。 例如,"$+"。 如果標識碼包含一個或多個這些字元,則標識碼必須是分隔識別元。  
  
 SQL_SQL_CONFORMANCE(ODBC 3.0)  
 指示驅動程式支援的 SQL-92 的 SQLUINTEGER 值:  
  
 SQL_SC_SQL92_ENTRY = 符合入門級 SQL-92。  
  
 SQL_SC_FIPS127_2_TRANSITIONAL = 符合 FIPS 127-2 過渡電平。  
  
 SQL_SC_SQL92_FULL = 符合全級別 SQL-92。  
  
 SQL_SC_SQL92_INTERMEDIATE = 符合中級 SQL-92 標準。  
  
 SQL_SQL92_DATETIME_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的約會時間標量函數,如 SQL-92 中定義的那樣。  
  
 以下位遮罩檔用於確定哪些日期時間函數受支援:  
  
 SQL_SDF_CURRENT_DATESQL_SDF_CURRENT_TIMESQL_SDF_CURRENT_TIMESTAMP  
  
 SQL_SQL92_FOREIGN_KEY_DELETE_RULE(ODBC 3.0)  
 SQLUINTEGER 位元遮罩 **,Enrle DeLETE**語句中支援的規則,如 SQL-92 中定義的那樣。  
  
 以下位遮罩資料來源支援哪些子句:  
  
 SQL_SFKD_CASCADESQL_SFKD_NO_ACTIONSQL_SFKD_SET_DEFAULTSQL_SFKD_SET_NULL  
  
 FIPS 過渡電平符合性驅動程式將始終返回支援的所有這些選項。  
  
 SQL_SQL92_FOREIGN_KEY_UPDATE_RULE(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**更新**語句中支援的規則,如 SQL-92 中定義的那樣。  
  
 以下位遮罩資料來源支援哪些子句:  
  
 SQL_SFKU_CASCADESQL_SFKU_NO_ACTIONSQL_SFKU_SET_DEFAULTSQL_SFKU_SET_NULL  
  
 SQL-92 完全符合級別的驅動程式將始終返回所有這些選項(如支援)。  
  
 SQL_SQL92_GRANT(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**在 GRANT**語句中支援的子句,如 SQL-92 中定義的那樣。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩資料來源支援哪些子句:  
  
 SQL_SG_DELETE_TABLE(入門級)SQL_SG_INSERT_COLUMN(中級)SQL_SG_INSERT_COLUMN(中級)SQL_SG_INSERT_TABLE(入門級)SQL_SG_REFERENCES_TABLE(入門級)SQL_SG_REFERENCES_COLUMN(入門級)SQL_SG_SELECT_TABLE(入門級)SQL_SG_UPDATE_COLUMN(入門級)SQL_SG_UPDATE_TABLE(入門級)SQL_SG_USAGE_ON_DOMAIN(FIPS過渡級別)SQL_SG_USAGE_ON_CHARACTER_SET(FIPS過渡級別)SQL_SG_USAGE_ON_COLLATION(FIPS過渡級別)SQL_SG_USAGE_ON_TRANSLATION(FIPS過渡級別)等級)SQL_SG_WITH_GRANT_OPTION(入門級)  
  
 SQL_SQL92_NUMERIC_VALUE_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的數位值標量函數,如 SQL-92 中定義的那樣。  
  
 以下位遮罩支援哪些數值函數:  
  
 SQL_SNVF_BIT_LENGTHSQL_SNVF_CHAR_LENGTHSQL_SNVF_CHARACTER_LENGTHSQL_SNVF_EXTRACTSQL_SNVF_OCTET_LENGTHSQL_SNVF_POSITION  
  
 SQL_SQL92_PREDICATES(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**SELECT**語句中支援的謂詞,如 SQL-92 中定義的那樣。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩資料來源支援哪些選項:  
  
 SQL_SP_BETWEEN(入門級)SQL_SP_COMPARISON(入門級)SQL_SP_EXISTS(入門級)SQL_SP_IN(入門級)SQL_SP_ISNOTNULL SQL_SP_IN(入門級)SQL_SP_ISNULL(入門級)SQL_SP_LIKE(入門級)SQL_SP_MATCH_FULL(滿級)SQL_SP_MATCH_PARTIAL(滿級)SQL_SP_MATCH_UNIQUE_FULL(滿級)SQL_SP_MATCH_UNIQUE_PARTIAL(滿級)SQL_SP_OVERLAPS(FIPS 過渡級別)SQL_SP_QUANTIFIED_COMPARISON(入門級)SQL_SP_UNIQUE(入門級)  
  
 SQL_SQL92_RELATIONAL_JOIN_OPERATORS(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**SELECT**語句中支持的關係聯接運算符,如 SQL-92 中定義的那樣。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩資料來源支援哪些選項:  
  
 SQL_SRJO_CORRESPONDING_CLAUSE(中級)SQL_SRJO_CROSS_JOIN(全級)SQL_SRJO_EXCEPT_JOIN(中級)SQL_SRJO_FULL_OUTER_JOIN(中級)SQL_SRJO_INNER_JOIN(中級)SQL_SRJO_INNER_JOIN(中級過渡級別)SQL_SRJO_INTERSECT_JOIN(中級)SQL_SRJO_LEFT_OUTER_JOIN(FIPS過渡級別)SQL_SRJO_NATURAL_JOIN(FIPS過渡級別)SQL_SRJO_RIGHT_OUTER_JOIN(FIPS過渡級別)SQL_SRJO_UNION_JOIN(全級)  
  
 SQL_SRJO_INNER_JOIN表示對內部**JOIN**語法的支援,而不是內部聯接功能的支援。 對內部**JOIN**語法的支援是 FIPS 過渡,而對內部聯接功能的支援是**ENTRY**。  
  
 SQL_SQL92_REVOKE(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**了 REVOKE**語句中支援的子句,如 SQL-92 中定義,數據源支援。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩資料來源支援哪些子句:  
  
 SQL_SR_CASCADE(FIPS過渡級別)SQL_SR_DELETE_TABLE(入門級)SQL_SR_GRANT_OPTION_FOR(中級)SQL_SR_INSERT_COLUMN(中級)SQL_SR_INSERT_TABLE(入門級)SQL_SR_REFERENCES_COLUMN(入門級)SQL_SR_REFERENCES_TABLE(入門級)SQL_SR_RESTRICT(FIPS過渡級別)SQL_SR_SELECT_TABLE(入門級)SQL_SR_UPDATE_COLUMN(入門級)SQL_SR_UPDATE_TABLE(入門級)SQL_SR_USAGE_ON_DOMAIN(FIPS過渡級別)SQL_SR_USAGE_ON_CHARACTER_SET(FIPS過渡等級)SQL_SR_USAGE_ON_COLLATION(FIPS過渡等級)SQL_SR_USAGE_ON_TRANSLATION(FIPS過渡等級)  
  
 SQL_SQL92_ROW_VALUE_CONSTRUCTOR(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**SELECT**語句中支援的行值構造函數運算式,如 SQL-92 中定義的那樣。 以下位遮罩資料來源支援哪些選項:  
  
 SQL_SRVC_VALUE_EXPRESSIONSQL_SRVC_NULLSQL_SRVC_DEFAULTSQL_SRVC_ROW_SUBQUERY  
  
 SQL_SQL92_STRING_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的字串標量函數,如 SQL-92 中定義的那樣。  
  
 以下位遮罩支援哪些字串函數:  
  
 SQL_SSF_CONVERTSQL_SSF_LOWERSQL_SSF_UPPERSQL_SSF_SUBSTRINGSQL_SSF_TRANSLATESQL_SSF_TRIM_BOTHSQL_SSF_TRIM_LEADINGSQL_SSF_TRIM_TRAILING  
  
 SQL_SQL92_VALUE_EXPRESSIONS(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉 SQL-92 中定義的受支援的值運算式。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩資料來源支援哪些選項:  
  
 SQL_SVE_CASE(中級)SQL_SVE_CAST(FIPS過渡級別)SQL_SVE_COALESCE(中級)SQL_SVE_NULLIF(中級)  
  
 SQL_STANDARD_CLI_CONFORMANCE(ODBC 3.0)  
 一個 SQLUINTEGER 位元遮罩,枚舉驅動程式符合的 CLI 標準或標準。 以下位遮罩驅動程式符合的等級:  
  
 SQL_SCC_XOPEN_CLI_VERSION1:驅動程式符合開放組 CLI 版本 1。  
  
 SQL_SCC_ISO92_CLI:驅動程式符合 ISO 92 CLI。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES1(ODBC 3.0)  
 描述驅動程式支援的靜態游標的屬性的 SQLUINTEGER 位元遮罩。 此位掩碼包含屬性的第一個子集;對於第二個子集,請參閱SQL_STATIC_CURSOR_ATTRIBUTES2。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA1_NEXTSQL_CA1_ABSOLUTESQL_CA1_RELATIVESQL_CA1_BOOKMARKSQL_CA1_LOCK_NO_CHANGESQL_CA1_LOCK_EXCLUSIVESQL_CA1_LOCK_UNLOCKSQL_CA1_POS_POSITIONSQL_CA1_POS_UPDATESQL_CA1_POS_DELETESQL_CA1_POS_REFRESHSQL_CA1_POSITIONED_UPDATESQL_CA1_POSITIONED_DELETESQL_CA1_SELECT_FOR_UPDATESQL_CA1_BULK_ADDSQL_CA1_BULK_UPDATE_BY_BOOKMARKSQL_CA1_BULK_DELETE_BY_BOOKMARKSQL_CA1_BULK_FETCH_BY_BOOKMARK  
  
 有關這些位掩碼的說明,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES1(並在說明中用"靜態游標"代替"動態游標")。  
  
 SQL-92 中間等級一致性驅動程式通常會返回SQL_CA1_NEXT、SQL_CA1_ABSOLUTE和SQL_CA1_RELATIVE選項(如支援),因為驅動程式支援通過嵌入式 SQL FETCH 語句滾動遊標。 但是,由於這不能直接確定基礎 SQL 支援,因此即使對於 SQL-92 符合級別的驅動程式,也不支援可滾動遊標。  
  
 SQL_STATIC_CURSOR_ATTRIBUTES2(ODBC 3.0)  
 描述驅動程式支援的靜態游標的屬性的 SQLUINTEGER 位元遮罩。 此位掩碼包含屬性的第二個子集;對於第一個子集,請參閱SQL_STATIC_CURSOR_ATTRIBUTES1。  
  
 以下位遮罩要確定哪些屬性受支援:  
  
 SQL_CA2_READ_ONLY_CONCURRENCYSQL_CA2_LOCK_CONCURRENCYSQL_CA2_OPT_ROWVER_CONCURRENCYSQL_CA2_OPT_VALUES_CONCURRENCYSQL_CA2_SENSITIVITY_ADDITIONSSQL_CA2_SENSITIVITY_DELETIONSSQL_CA2_SENSITIVITY_UPDATESSQL_CA2_MAX_ROWS_SELECTSQL_CA2_MAX_ROWS_INSERTSQL_CA2_MAX_ROWS_DELETESQL_CA2_MAX_ROWS_UPDATESQL_CA2_MAX_ROWS_CATALOGSQL_CA2_MAX_ROWS_AFFECTS_ALLSQL_CA2_CRC_EXACTSQL_CA2_CRC_APPROXIMATESQL_CA2_SIMULATE_NON_UNIQUESQL_CA2_SIMULATE_TRY_UNIQUESQL_CA2_SIMULATE_UNIQUE  
  
 有關這些位掩碼的說明,請參閱SQL_DYNAMIC_CURSOR_ATTRIBUTES2(並在說明中用"靜態游標"代替"動態游標")。  
  
 SQL_STRING_FUNCTIONS(ODBC 1.0)  
 注意:資訊類型在 ODBC 1.0 中引入;每個位掩碼都標有引入它的版本。  
  
 SQLUINTEGER 位罩,枚舉驅動程式和相關資料來源支援的標量字串函數。  
  
 以下位遮罩支援哪些字串函數:  
  
 SQL_FN_STR_ASCII (ODBC 1.0)SQL_FN_STR_BIT_LENGTH (ODBC 3.0)SQL_FN_STR_CHAR (ODBC 1.0)SQL_FN_STR_CHAR_LENGTH (ODBC 3.0)SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0)SQL_FN_STR_CONCAT (ODBC 3.0)SQL_FN_STR_CONCAT (ODBC 1.0)SQL_FN_STR_DIFFERENCE (ODBC 1 .0)SQL_FN_STR_INSERT (ODBC 1.0)SQL_FN_STR_LCASE (ODBC 1.0)SQL_FN_STR_LEFT (ODBC 1.0)SQL_FN_STR_LENGTH(ODBC 1.0)SQL_FN_STR_LOCATE(ODBC 1.0)SQL_FN_STR_LTRIM(ODBC 1.0)SQL_FN_STR_LTRIM(ODBC 1.0)1.0) SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) SQL_FN_STR_POSITION (ODBC 3.0) SQL_FN_STR_REPEAT (ODBC 1.0)SQL_FN_STR_REPLACE (ODBC 1.0)SQL_FN_STR_RIGHT (ODBC 1.0)SQL_FN_STR_RTRIM (ODBC 1.0)SQL_FN_STR_SOUNDEX (ODBC 2.0)SQL_FN_STR_SPACE (ODBC 2.0)SQL_FN_STR_SUBSTRING (ODBC 1.0)SQL_FN_STR_UCASE(ODBC 1.0)  
  
 如果應用程式可以使用*string_exp1**string_exp1、string_exp2*呼叫**LOCATE**標量函數和*啟動*參數,則驅動程式返回SQL_FN_STR_LOCATE位掩碼。 如果應用程式只能調用 STRING_EXP1*和**string_exp2*參數的 LOCATE 標量函數,則驅動程式將返回SQL_FN_STR_LOCATE_2位掩碼。 完全支援**LOCATE**標量函數的驅動程式將返回兩個位掩碼。  
  
 (有關詳細資訊,請參閱附錄 E 中的[字串函數](../../../odbc/reference/appendixes/string-functions.md)"斯卡拉爾函數"。  
  
 SQL_SUBQUERIES(ODBC 2.0)  
 SQLUINTEGER 位掩碼,枚舉支援子查詢的謂詞:  
  
 SQL_SQ_CORRELATED_SUBQUERIESSQL_SQ_COMPARISONSQL_SQ_EXISTSSQL_SQ_INSQL_SQ_QUANTIFIED  
  
 SQL_SQ_CORRELATED_SUBQUERIES位掩碼表示支援子查詢的所有謂詞都支持相關的子查詢。  
  
 SQL-92 符合入門級的驅動程序將始終返回一個位掩碼,其中設置所有這些位。  
  
 SQL_SYSTEM_FUNCTIONS(ODBC 1.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的標量系統函數。  
  
 以下位遮罩支援哪些系統功能:  
  
 SQL_FN_SYS_DBNAMESQL_FN_SYS_IFNULLSQL_FN_SYS_USERNAME  
  
 SQL_TABLE_TERM(ODBC 1.0)  
 具有表的數據源供應商名稱的字串;例如,"表"或"檔"。  
  
 此字串可以是上部、下部或混合大小寫。  
  
 SQL-92 符合入門級的驅動程序將始終返回"表"。  
  
 SQL_TIMEDATE_ADD_INTERVALS(ODBC 2.0)  
 SQLUINTEGER 位掩碼,枚舉了 TIMESTAMPADD 標量函數的驅動程式和相關數據源支援的時間戳間隔。  
  
 以下位遮罩支援哪些間隔:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 過渡電平一致性驅動程式將始終返回一個位掩碼,其中設置所有這些位。  
  
 SQL_TIMEDATE_DIFF_INTERVALS(ODBC 2.0)  
 SQLUINTEGER 位掩碼,枚舉了 TIMESTAMPDIFF 標量函數的驅動程式和相關數據源支援的時間戳間隔。  
  
 以下位遮罩支援哪些間隔:  
  
 SQL_FN_TSI_FRAC_SECONDSQL_FN_TSI_SECONDSQL_FN_TSI_MINUTESQL_FN_TSI_HOURSQL_FN_TSI_DAYSQL_FN_TSI_WEEKSQL_FN_TSI_MONTHSQL_FN_TSI_QUARTERSQL_FN_TSI_YEAR  
  
 FIPS 過渡電平一致性驅動程式將始終返回一個位掩碼,其中設置所有這些位。  
  
 SQL_TIMEDATE_FUNCTIONS(ODBC 1.0)  
 注意:資訊類型在 ODBC 1.0 中引入;每個位掩碼都標有引入它的版本。  
  
 SQLUINTEGER 位掩碼,枚舉驅動程式和相關數據源支援的標量日期和時間函數。  
  
 以下位遮罩支援哪些日期和時間函數:  
  
 SQL_FN_TD_CURRENT_DATE ODBC 3.0)SQL_FN_TD_CURRENT_TIME (ODBC 3.0)SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0)SQL_FN_TD_CURDATE (ODBC 1.0)SQL_FN_TD_CURTIME (ODBC 1.0) SQL_FN_TD_DAYNAME (ODBC 1.0) SQL_FN_TD_DAYOFMONTH (ODBC 1.0)SQL_FN_TD_DAYOFWEEK (ODBC 1 .0)SQL_FN_TD_DAYOFYEAR (ODBC 1.0) SQL_FN_TD_EXTRACT (ODBC 3.0)SQL_FN_TD_HOUR (ODBC 1.0)SQL_FN_TD_MINUTE(ODBC 1.0)SQL_FN_TD_MONTH(ODBC 1.0)SQL_FN_TD_MONTH(ODBC 1.0)SQL_FN_TD_MONTH(ODBC 1.0)1.0)SQL_FN_TD_MONTHNAME (ODBC 2.0)SQL_FN_TD_NOW (ODBC 1.0)SQL_FN_TD_QUARTER (ODBC 1.0)SQL_FN_TD_SECOND (ODBC 1.0)SQL_FN_TD_TIMESTAMPADD (ODBC 2.0)SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0)SQL_FN_TD_WEEK (ODBC 1.0)SQL_FN_TD_YEAR(ODBC 1.0)  
  
 SQL_TXN_CAPABLE(ODBC 1.0)  
 注意:資訊類型在 ODBC 1.0 中引入;每個返回值都標有引入該值的版本。  
  
 描述驅動程式或資料來源中的事務支援的 SQLUSMALLINT 值:  
  
 SQL_TC_NONE = 不支援事務。 (ODBC 1.0)  
  
 SQL_TC_DML = 事務只能包含資料操作語言 (DML) 語句 **(SELECT,****插入**、**更新**、**刪除**). 事務中遇到的數據定義語言 (DDL) 語句會導致錯誤。 (ODBC 1.0)  
  
 SQL_TC_DDL_COMMIT = 事務只能包含 DML 語句。 事務中遇到的 DDL 語句(**創建表****、DROP INDEX**等)會導致提交事務。 (ODBC 2.0)  
  
 SQL_TC_DDL_IGNORE = 事務只能包含 DML 語句。 忽略事務中遇到的 DDL 語句。 (ODBC 2.0)  
  
 SQL_TC_ALL = 事務可以按任何順序包含 DDL 語句和 DML 語句。 (ODBC 1.0)  
  
 (由於 SQL-92 中必須支援事務,因此 SQL-92 符合的驅動程式[任何級別]永遠不會返回SQL_TC_NONE。  
  
 SQL_TXN_ISOLATION_OPTION(ODBC 1.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程式或數據源中可用的事務隔離級別。  
  
 以下位遮罩與標誌一起使用,以確定支援哪些選項:  
  
 SQL_TXN_READ_UNCOMMITTEDSQL_TXN_READ_COMMITTEDSQL_TXN_REPEATABLE_READSQL_TXN_SERIALIZABLE  
  
 有關這些隔離級別的說明,請參閱SQL_DEFAULT_TXN_ISOLATION的說明。  
  
 要設置事務隔離等級,應用程式調用**SQLSetConnectAttr**來設置SQL_ATTR_TXN_ISOLATION屬性。 有關詳細資訊,請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
 SQL-92 符合入門級的驅動程序將始終返回SQL_TXN_SERIALIZABLE支援。 FIPS 過渡電平符合性驅動程式將始終返回支援的所有這些選項。  
  
 SQL_UNION(ODBC 2.0)  
 Enting SQLUINTEGER 位元遮罩:**UNION**  
  
 SQL_U_UNION = 資料源支援**UNION**子句。  
  
 SQL_U_UNION_ALL = 資料來源支援**UNION**子句中的**ALL**關鍵字。 (在這種情況下 **,SQLGetInfo**將返回SQL_U_UNION和SQL_U_UNION_ALL。  
  
 SQL-92 符合入門級的驅動程序將始終返回這兩個選項作為支援。  
  
 SQL_USER_NAME(ODBC 1.0)  
 具有特定資料庫中使用的名稱的字串,該字串可能不同於登錄名。  
  
 SQL_XOPEN_CLI_YEAR(ODBC 3.0)  
 指示 OPENGROUP 規範發佈年份的字串,ODBC 驅動程式管理器的版本完全符合該規範。  
  
 SQL_ACCESSIBLE_PROCEDURES(ODBC 1.0)  
 字串字串:「Y」,如果用戶可以執行**SQL 程式**傳回的所有過程;如果返回過程時可能返回使用者無法執行,則為"N"。  
  
 SQL_ACCESSIBLE_TABLES(ODBC 1.0)  
 字串字串:「Y」,**如果使用者保證選擇** **SQLTables**傳回的所有表的許可權;如果返回的表是使用者無法訪問的表,則為"N"。  
  
 SQL_ACTIVE_ENVIRONMENTS(ODBC 3.0)  
 指定驅動程式可以支援的最大活動環境數的 SQLUSMALLINT 值。 如果沒有指定限制或限制未知,則此值設置為零。  
  
 SQL_AGGREGATE_FUNCTIONS(ODBC 3.0)  
 SQLUINTEGER 位罩對聚合函數支援:  
  
 SQL_AF_ALLSQL_AF_AVGSQL_AF_COUNTSQL_AF_DISTINCTSQL_AF_MAXSQL_AF_MINSQL_AF_SUM  
  
 SQL-92 符合入門級的驅動程序將始終返回所有這些選項(如支援)。  
  
 SQL_ALTER_DOMAIN(ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉**了在**SQL-92 中定義的 ALTER DOMAIN 語句中子句,數據源支援。 SQL-92 完全符合級別的驅動程序將始終返回所有位掩碼。 返回值"0"表示不支援 ALTER **DOMAIN**語句。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_AD_ADD_DOMAIN_CONSTRAINT = 支援新增網域約束(完整等級)  
  
 SQL_AD_ADD_DOMAIN_DEFAULT \<=\<變更網域>>受支援的網域預設子句(完整等級)  
  
 SQL_AD_CONSTRAINT_NAME_DEFINITION \<=>为命名域约束(中間等級)支援規範名稱定義子句  
  
 SQL_AD_DROP_DOMAIN_CONSTRAINT \<= 支援>刪除網域  
  
 SQL_AD_DROP_DOMAIN_DEFAULT \<=\<變更網域>刪除網域預設子句>支援(完整等級)  
  
 如果\<支援>添加域\<約束 (設定SQL_AD_ADD_DOMAIN_CONSTRAINT位),以下位指定支援的約束屬性>:  
  
 SQL_AD_ADD_CONSTRAINT_DEFERRABLE(全級別)SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE(全級別)SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED(全級別)SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE(全級別)  
  
 SQL_ALTER_TABLE(ODBC 2.0)  
 SQLUINTEGER 位罩,枚舉資料來源支援的**ALTER TABLE**語句中子句。  
  
 必須支援此功能的 SQL-92 或 FIPS 一致性級別顯示在每個位掩碼旁邊的括弧中。  
  
 以下位遮罩用於確定哪些子句受支援:  
  
 SQL_AT_ADD_COLUMN_COLLATION \<= 支援新增欄>子句,具有指定欄位規則(完整等級)(ODBC 3.0)的功能  
  
 SQL_AT_ADD_COLUMN_DEFAULT \<= 支援新增欄>子句,具有指定列預設值(FIPS 過渡等級)(ODBC 3.0)的功能  
  
 SQL_AT_ADD_COLUMN_SINGLE \<= 支援新增欄>(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_ADD_CONSTRAINT \<= 支援新增欄>子句,具有指定欄位約束(FIPS 過渡等級)(ODBC 3.0)的功能  
  
 SQL_AT_ADD_TABLE_CONSTRAINT \<= 支援>項(FIPS過渡等級)(ODBC 3.0)新增表約束  
  
 SQL_AT_CONSTRAINT_NAME_DEFINITION \<=>为命名列和表约束(中間等級)(ODBC 3.0)支援規範名稱定義  
  
 支援SQL_AT_DROP_COLUMN_CASCADE \<= 丟棄列> CASCADE(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_DROP_COLUMN_DEFAULT \<=\<變更欄>刪除列預設子句>支援(中級級別)(ODBC 3.0)  
  
 支援SQL_AT_DROP_COLUMN_RESTRICT \<= 下拉列>限制(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0)  
  
 支援SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT \<=>约束的放置列(FIPS 過渡等級)(ODBC 3.0)  
  
 SQL_AT_SET_COLUMN_DEFAULT \<=\<更改欄>設定列預設子句>支援(中級級別)(ODBC 3.0)  
  
 如果支援指定欄或表\<約束(設定SQL_AT_ADD_CONSTRAINT位),以下位將指定支援約束屬性>:  
  
 SQL_AT_CONSTRAINT_INITIALLY_DEFERRED(全級) (ODBC 3.0) SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (全級別) (ODBC 3.0)SQL_AT_CONSTRAINT_DEFERRABLE(完整級別)(ODBC 3.0)SQL_AT_CONSTRAINT_NON_DEFERRABLE(全級)(ODBC 3.0)  
  
 SQL_ASYNC_MODE(ODBC 3.0)  
 指示驅動程式中非同步支援等級的 SQLUINTEGER 值:  
  
 SQL_AM_CONNECTION = 支援連接級非同步執行。 與給定連接句柄關聯的所有語句句柄都處於非同步模式,或者所有語句句柄都處於同步模式。 連接上的語句句柄不能處於非同步模式,而同一連接上的另一個語句句柄處於同步模式,反之亦然。  
  
 SQL_AM_STATEMENT = 支援語句級非同步執行。 與連接句柄關聯的某些語句句柄可以處於異步模式,而同一連接上的其他語句句柄處於同步模式。  
  
 不支援SQL_AM_NONE = 不支援非同步模式。  
  
 SQL_BATCH_ROW_COUNT (ODBC 3.0)  
 SQLUINTEGER 位掩碼,枚舉驅動程序相對於行計數的可用性的行為。 以下位遮罩與資訊型態使用:  
  
 SQL_BRC_ROLLED_UP = 連續插入、刪除或更新語句的行計數匯總為一個。 如果未設置此位,則行計數可用於每個語句。  
  
 SQL_BRC_PROCEDURES = 在存儲過程中執行批處理時,行計數(如果有)可用。 如果行計數可用,則它們可以匯總或單獨可用,具體取決於SQL_BRC_ROLLED_UP位。  
  
 SQL_BRC_EXPLICIT = 當通過調用 SQLExecute 或**SQLExecDirect**直接執行批處理時**SQLExecDirect**,行計數(如果有)可用。 如果行計數可用,則它們可以匯總或單獨可用,具體取決於SQL_BRC_ROLLED_UP位。  
  
## <a name="example"></a>範例  
 **SQLGetInfo**在 #*InfoValuePtr*中傳回支援的選項清單作為 SQLUINTEGER 位罩。 每個選項的位掩碼與標誌一起使用,以確定該選項是否受支援。  
  
 例如,應用程式可以使用以下代碼來確定與連接關聯的驅動程式是否支援 SUBSTRING 標量函數。  
  
 有關使用**SQLGetInfo**的另一個範例,請參閱[SQLTables 函數](../../../odbc/reference/syntax/sqltables-function.md)。  
  
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
 傳回連線屬性的設定  
 [SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)  
  
 確定驅動程式是否支援函數  
 [SQLGetFunctions 函式](../../../odbc/reference/syntax/sqlgetfunctions-function.md)  
  
 傳回敘述屬性的設定  
 [SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)  
  
 傳回關於資料來源資料型態的資訊  
 [SQLGetTypeInfo 函式](../../../odbc/reference/syntax/sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
