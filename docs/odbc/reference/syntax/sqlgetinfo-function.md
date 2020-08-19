---
description: SQLGetInfo 函數
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
ms.openlocfilehash: b60dcdd90c71e1790464f24cd34dedfaa22e7c61
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421272"
---
# <a name="sqlgetinfo-function"></a>SQLGetInfo 函數

**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetInfo** 會傳回與連接相關聯之驅動程式和資料來源的一般資訊。  
  
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
 輸出資訊類型。  
  
 *InfoValuePtr*  
 出要傳回信息的緩衝區指標。 視所要求的 *InfoType* 而定，傳回的資訊將會是下列其中一項：以 null 終止的字元字串、SQLUSMALLINT 值、SQLUINTEGER 的位元遮罩、SQLUINTEGER 旗標、SQLUINTEGER 二進位值或 SQLULEN 值。  
  
 如果 *InfoType* 引數 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT， *InfoValuePtr* 引數就會是輸入和輸出。  (如需詳細資訊，請參閱此函數描述中的 SQL_DRIVER_HDESC 或 SQL_DRIVER_HSTMT 描述項。 )   
  
 如果 *InfoValuePtr* 為 Null， *StringLengthPtr* 仍會傳回位元組總數 (排除字元資料的 Null 終止字元) 可在 *InfoValuePtr*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出\* *InfoValuePtr*緩衝區的長度。 如果* \* InfoValuePtr*中的值不是字元字串，或*InfoValuePtr*為 null 指標，則會忽略*BufferLength*引數。 驅動程式會假設* \* InfoValuePtr*的大小是 SQLUSMALLINT 或 SQLUINTEGER，以*InfoType*為基礎。 如果* \* InfoValuePtr*是在呼叫**SQLGetInfoW**) 時 (的 Unicode 字串，則*BufferLength*引數必須是偶數; 如果不是，則會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 。  
  
 *StringLengthPtr*  
 出緩衝區的指標，此緩衝區會傳回位元組總數 (排除字元資料的 null 終止字元) 可在 **InfoValuePtr*中傳回。  
  
 若為字元資料，如果可傳回的位元組數目大於或等於*BufferLength*，InfoValuePtr 中的資訊 \* *InfoValuePtr*就會截斷為*BufferLength*位元組減去 null 終止字元的長度，而且驅動程式會以 null 終止。  
  
 對於所有其他類型的資料，會忽略*BufferLength*的值，而驅動程式會假設 \* *INFOVALUEPTR*的大小為 SQLUSMALLINT 或 SQLUINTEGER，視*InfoType*而定。  
  
## <a name="returns"></a>傳回  

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  

 當**SQLGetInfo**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DBC）和*ConnectionHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLGetInfo** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *InfoValuePtr*不夠大，無法傳回所有要求的資訊。 因此，此資訊已被截斷。 Untruncated 表單中所要求資訊的長度會在 **StringLengthPtr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08003|連接未開啟| (DM) *InfoType* 要求的資訊類型需要開啟連接。 在 ODBC 所保留的資訊類型中，只有在沒有開啟連接的情況下，才會傳回 SQL_ODBC_VER。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤|針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY024|不正確屬性值| (DM) *InfoType* 引數是 SQL_DRIVER_HSTMT 的，而且 *InfoValuePtr* 所指向的值不是有效的語句控制碼。<br /><br />  (DM) *InfoType* 引數是 SQL_DRIVER_HDESC 的，而且 *InfoValuePtr* 所指向的值不是有效的描述項控制碼。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *BufferLength* 指定的值小於0。<br /><br />  (DM) 為*BufferLength*指定的值是奇數，而* \* InfoValuePtr*則是 Unicode 資料類型。|  
|HY096|資訊類型超出範圍|針對引數 *InfoType* 指定的值對驅動程式支援的 ODBC 版本無效。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](sqlendtran-function.md)。|  
|HYC00|選用欄位未實作為|針對引數 *InfoType* 指定的值是驅動程式不支援的驅動程式專用值。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 對應至 *ConnectionHandle* 的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  

 目前定義的資訊類型會顯示在本節稍後的「資訊類型」中;預期會有更多的定義，以利用不同的資料來源。 ODBC 會保留一系列的資訊類型，驅動程式開發人員必須從開啟的群組中保留自己的驅動程式特定使用值。 **SQLGetInfo**不會執行 Unicode 轉換或*Thunking* (請參閱[附錄 A：](../appendixes/appendix-a-odbc-error-codes.md)適用于驅動程式定義*InfoTypes*之 Odbc 程式設計*人員參考*) 的 odbc 錯誤碼。 如需詳細資訊，請參閱 [驅動程式特定的資料類型、描述項類型、資訊類型、診斷類型與屬性](../develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。 InfoValuePtr 中傳回的資訊格式 \* *InfoValuePtr*取決於要求的*InfoType* 。 **SQLGetInfo** 會以下列五種不同格式的其中一種傳回信息：  
  
- 以 null 結束的字元字串  
  
- SQLUSMALLINT 值  
  
- SQLUINTEGER 位元遮罩  
  
- SQLUINTEGER 值  
  
- SQLUINTEGER 二進位值  
  
 下列每個資訊類型的格式都會注明于類型的描述中。 應用程式必須據以轉換 **InfoValuePtr* 中傳回的值。 如需應用程式如何從 SQLUINTEGER 位元遮罩取得資料的範例，請參閱「程式碼範例」。  
  
 驅動程式必須針對下表中定義的每個資訊類型傳回值。 如果資訊類型不適用於驅動程式或資料來源，驅動程式會傳回下表所列的其中一個值。  

|資訊類型|值|
|-|-|
|字元字串 ( "Y" 或 "N" ) |"N"|
|字元字串 (非 "Y" 或 "N" ) |空字串|
|SQLUSMALLINT|0|
|SQLUINTEGER 位元遮罩或 SQLUINTEGER 二進位值|0L|
  
 例如，如果資料來源不支援程式， **SQLGetInfo** 會傳回下表所列的值，以取得與程式相關的 *InfoType* 值。  

|InfoType|值|
|-|-|
|SQL_PROCEDURES|"N"|
|SQL_ACCESSIBLE_PROCEDURES|"N"|
|SQL_MAX_PROCEDURE_NAME_LEN|0|
|SQL_PROCEDURE_TERM|空字串|
  
 **SQLGetInfo** 會傳回 SQLSTATE HY096 (不正確引數值) 值為的 *InfoType* 值，這些值是保留供 ODBC 使用，但不是由驅動程式支援的 ODBC 版本所定義。 為了判斷驅動程式符合的 ODBC 版本，應用程式會使用 SQL_DRIVER_ODBC_VER 資訊類型來呼叫 **SQLGetInfo** 。 **SQLGetInfo** 會傳回 SQLSTATE HYC00 (選用功能，而不是針對屬於驅動程式專用用途但驅動程式不支援之資訊類型範圍內的 *InfoType* 值所執行的) 。  
  
 **SQLGetInfo**的所有呼叫都需要開啟連線，但在*InfoType* SQL_ODBC_VER 時，會傳回驅動程式管理員的版本。  
  
## <a name="information-types"></a>資訊類型  

 本節列出 **SQLGetInfo**所支援的資訊類型。 系統會將資訊類型分組 categorically，並依字母順序列出。 也會列出已針對 ODBC 3.x 新增或重新命名的資訊*類型。*  
  
## <a name="driver-information"></a>驅動程式資訊  

 下列 *InfoType* 引數的值會傳回 ODBC 驅動程式的相關資訊，例如使用中語句的數目、資料來源名稱，以及介面標準合規性層級：  

:::row:::
    :::column:::
        SQL_ACTIVE_ENVIRONMENTS  
        SQL_ASYNC_DBC_FUNCTIONS  
        SQL_ASYNC_MODE  
        SQL_ASYNC_NOTIFICATION  
        SQL_BATCH_ROW_COUNT  
        SQL_BATCH_SUPPORT  
        SQL_DATA_SOURCE_NAME  
        SQL_DRIVER_AWARE_POOLING_SUPPORTED  
        SQL_DRIVER_HDBC  
        SQL_DRIVER_HDESC  
        SQL_DRIVER_HENV  
        SQL_DRIVER_HLIB  
        SQL_DRIVER_HSTMT  
        SQL_DRIVER_NAME  
        SQL_DRIVER_ODBC_VER  
        SQL_DRIVER_VER  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES1  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES2  
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1  
    :::column-end:::
    :::column:::
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2  
        SQL_FILE_USAGE  
        SQL_GETDATA_EXTENSIONS  
        SQL_INFO_SCHEMA_VIEWS  
        SQL_KEYSET_CURSOR_ATTRIBUTES1  
        SQL_KEYSET_CURSOR_ATTRIBUTES2  
        SQL_MAX_ASYNC_CONCURRENT_STATEMENTS  
        SQL_MAX_CONCURRENT_ACTIVITIES  
        SQL_MAX_DRIVER_CONNECTIONS  
        SQL_ODBC_INTERFACE_CONFORMANCE  
        SQL_ODBC_STANDARD_CLI_CONFORMANCE  
        SQL_ODBC_VER  
        SQL_PARAM_ARRAY_ROW_COUNTS  
        SQL_PARAM_ARRAY_SELECTS  
        SQL_ROW_UPDATES  
        SQL_SEARCH_PATTERN_ESCAPE  
        SQL_SERVER_NAME  
        SQL_STATIC_CURSOR_ATTRIBUTES1  
        SQL_STATIC_CURSOR_ATTRIBUTES2  
    :::column-end:::
:::row-end:::

> [!NOTE]  
> 在執行 **SQLGetInfo**時，驅動程式可以將資訊從伺服器傳送或要求的次數降到最低，藉以改善效能。  
  
## <a name="dbms-product-information"></a>DBMS 產品資訊  

 下列 *InfoType* 引數的值會傳回 dbms 產品的相關資訊，例如 dbms 名稱和版本：  

:::row:::
    :::column:::
        SQL_DATABASE_NAME  
        SQL_DBMS_NAME  
    :::column-end:::
    :::column:::
        SQL_DBMS_VER  
    :::column-end:::
:::row-end:::

## <a name="data-source-information"></a>資料來源資訊  

 下列 *InfoType* 引數的值會傳回資料來源的相關資訊，例如資料指標特性和交易功能：  

:::row:::
    :::column:::
        SQL_ACCESSIBLE_PROCEDURES  
        SQL_ACCESSIBLE_TABLES  
        SQL_BOOKMARK_PERSISTENCE  
        SQL_CATALOG_TERM  
        SQL_COLLATION_SEQ  
        SQL_CONCAT_NULL_BEHAVIOR  
        SQL_CURSOR_COMMIT_BEHAVIOR  
        SQL_CURSOR_ROLLBACK_BEHAVIOR  
        SQL_CURSOR_SENSITIVITY  
        SQL_DATA_SOURCE_READ_ONLY  
        SQL_DEFAULT_TXN_ISOLATION  
        SQL_DESCRIBE_PARAMETER  
    :::column-end:::
    :::column:::
        SQL_MULT_RESULT_SETS  
        SQL_MULTIPLE_ACTIVE_TXN  
        SQL_NEED_LONG_DATA_LEN  
        SQL_NULL_COLLATION  
        SQL_PROCEDURE_TERM  
        SQL_SCHEMA_TERM  
        SQL_SCROLL_OPTIONS  
        SQL_TABLE_TERM  
        SQL_TXN_CAPABLE  
        SQL_TXN_ISOLATION_OPTION  
        SQL_USER_NAME  
    :::column-end:::
:::row-end:::

## <a name="supported-sql"></a>支援的 SQL  

 下列 *InfoType* 引數的值會傳回資料來源所支援之 SQL 語句的相關資訊。 這些資訊類型所描述之每項功能的 SQL 語法都是 SQL-92 語法。 這些資訊類型不會徹底描述整個 SQL-92 文法。 相反地，它們會描述文法的部分，而這些部分的資料來源通常會提供不同的支援層級。 具體而言，SQL-92 中大部分的 DDL 語句都涵蓋在內。  
  
 應用程式應該從 SQL_SQL_CONFORMANCE 資訊類型判斷支援的文法的一般層級，並使用其他資訊類型來判斷所述標準合規性層級的變化。  

:::row:::
    :::column:::
        SQL_AGGREGATE_FUNCTIONS  
        SQL_ALTER_DOMAIN  
        SQL_ALTER_SCHEMA  
        SQL_ALTER_TABLE  
        SQL_ANSI_SQL_DATETIME_LITERALS  
        SQL_CATALOG_LOCATION  
        SQL_CATALOG_NAME  
        SQL_CATALOG_NAME_SEPARATOR  
        SQL_CATALOG_USAGE  
        SQL_COLUMN_ALIAS  
        SQL_CORRELATION_NAME  
        SQL_CREATE_ASSERTION  
        SQL_CREATE_CHARACTER_SET  
        SQL_CREATE_COLLATION  
        SQL_CREATE_DOMAIN  
        SQL_CREATE_SCHEMA  
        SQL_CREATE_TABLE  
        SQL_CREATE_TRANSLATION  
        SQL_DDL_INDEX  
        SQL_DROP_ASSERTION  
        SQL_DROP_CHARACTER_SET  
        SQL_DROP_COLLATION  
        SQL_DROP_DOMAIN  
        SQL_DROP_SCHEMA  
    :::column-end:::
    :::column:::
        SQL_DROP_TABLE  
        SQL_DROP_TRANSLATION  
        SQL_DROP_VIEW  
        SQL_EXPRESSIONS_IN_ORDERBY  
        SQL_GROUP_BY  
        SQL_IDENTIFIER_CASE  
        SQL_IDENTIFIER_QUOTE_CHAR  
        SQL_INDEX_KEYWORDS  
        SQL_INSERT_STATEMENT  
        SQL_INTEGRITY  
        SQL_KEYWORDS  
        SQL_LIKE_ESCAPE_CLAUSE  
        SQL_NON_NULLABLE_COLUMNS  
        SQL_OJ_CAPABILITIES  
        SQL_ORDER_BY_COLUMNS_IN_SELECT  
        SQL_OUTER_JOINS  
        SQL_PROCEDURES  
        SQL_QUOTED_IDENTIFIER_CASE  
        SQL_SCHEMA_USAGE  
        SQL_SPECIAL_CHARACTERS  
        SQL_SQL_CONFORMANCE  
        SQL_SUBQUERIES  
        SQL_UNION  
    :::column-end:::
:::row-end:::

## <a name="sql-limits"></a>SQL 限制  

 下列 *InfoType* 引數的值會傳回在 SQL 語句中套用至識別碼和子句之限制的相關資訊，例如識別碼的最大長度和選取清單中的資料行數目上限。 限制可以由驅動程式或資料來源加諸。  

:::row:::
    :::column:::
        SQL_MAX_BINARY_LITERAL_LEN  
        SQL_MAX_CATALOG_NAME_LEN  
        SQL_MAX_CHAR_LITERAL_LEN  
        SQL_MAX_COLUMN_NAME_LEN  
        SQL_MAX_COLUMNS_IN_GROUP_BY  
        SQL_MAX_COLUMNS_IN_INDEX  
        SQL_MAX_COLUMNS_IN_ORDER_BY  
        SQL_MAX_COLUMNS_IN_SELECT  
        SQL_MAX_COLUMNS_IN_TABLE  
        SQL_MAX_CURSOR_NAME_LEN  
    :::column-end:::
    :::column:::
        SQL_MAX_IDENTIFIER_LEN  
        SQL_MAX_INDEX_SIZE  
        SQL_MAX_PROCEDURE_NAME_LEN  
        SQL_MAX_ROW_SIZE  
        SQL_MAX_ROW_SIZE_INCLUDES_LONG  
        SQL_MAX_SCHEMA_NAME_LEN  
        SQL_MAX_STATEMENT_LEN  
        SQL_MAX_TABLE_NAME_LEN  
        SQL_MAX_TABLES_IN_SELECT  
        SQL_MAX_USER_NAME_LEN  
    :::column-end:::
:::row-end:::

## <a name="scalar-function-information"></a>純量函數資訊  

 下列 *InfoType* 引數的值會傳回資料來源和驅動程式所支援之純量函數的相關資訊。 如需純量函數的詳細資訊，請參閱 [附錄 E：](../appendixes/appendix-e-scalar-functions.md)純量函數。  

:::row:::
    :::column:::
        SQL_CONVERT_FUNCTIONS  
        SQL_NUMERIC_FUNCTIONS  
        SQL_STRING_FUNCTIONS  
        SQL_SYSTEM_FUNCTIONS  
    :::column-end:::
    :::column:::
        SQL_TIMEDATE_ADD_INTERVALS  
        SQL_TIMEDATE_DIFF_INTERVALS  
        SQL_TIMEDATE_FUNCTIONS  
    :::column-end:::
:::row-end:::

## <a name="conversion-information"></a>轉換資訊  

 下列 *InfoType* 引數的值會傳回 sql 資料類型的清單，資料來源可以使用 **convert** 純量函數來轉換指定的 sql 資料類型：  

:::row:::
    :::column:::
        SQL_CONVERT_BIGINT  
        SQL_CONVERT_BINARY  
        SQL_CONVERT_BIT  
        SQL_CONVERT_CHAR  
        SQL_CONVERT_DATE  
        SQL_CONVERT_DECIMAL  
        SQL_CONVERT_DOUBLE  
        SQL_CONVERT_FLOAT  
        SQL_CONVERT_INTEGER  
        SQL_CONVERT_INTERVAL_DAY_TIME  
        SQL_CONVERT_INTERVAL_YEAR_MONTH  
    :::column-end:::
    :::column:::
        SQL_CONVERT_LONGVARBINARY  
        SQL_CONVERT_LONGVARCHAR  
        SQL_CONVERT_NUMERIC  
        SQL_CONVERT_REAL  
        SQL_CONVERT_SMALLINT  
        SQL_CONVERT_TIME  
        SQL_CONVERT_TIMESTAMP  
        SQL_CONVERT_TINYINT  
        SQL_CONVERT_VARBINARY  
        SQL_CONVERT_VARCHAR  
    :::column-end:::
:::row-end:::

## <a name="information-types-added-for-odbc-3x"></a>針對 ODBC 3.x 新增的資訊類型  

 ODBC 3.x 已加入下列 *InfoType* 引數的值：  

:::row:::
    :::column:::
        SQL_ACTIVE_ENVIRONMENTS  
        SQL_AGGREGATE_FUNCTIONS  
        SQL_ALTER_DOMAIN  
        SQL_ALTER_SCHEMA  
        SQL_ANSI_SQL_DATETIME_LITERALS  
        SQL_ASYNC_DBC_FUNCTIONS  
        SQL_ASYNC_MODE  
        SQL_ASYNC_NOTIFICATION  
        SQL_BATCH_ROW_COUNT  
        SQL_BATCH_SUPPORT  
        SQL_CATALOG_NAME  
        SQL_COLLATION_SEQ  
        SQL_CONVERT_INTERVAL_DAY_TIME  
        SQL_CONVERT_INTERVAL_YEAR_MONTH  
        SQL_CREATE_ASSERTION  
        SQL_CREATE_CHARACTER_SET  
        SQL_CREATE_COLLATION  
        SQL_CREATE_DOMAIN  
        SQL_CREATE_SCHEMA  
        SQL_CREATE_TABLE  
        SQL_CREATE_TRANSLATION  
        SQL_CURSOR_SENSITIVITY  
        SQL_DDL_INDEX  
        SQL_DESCRIBE_PARAMETER  
        SQL_DM_VER  
    :::column-end:::
    :::column:::
        SQL_DRIVER_AWARE_POOLING_SUPPORTED  
        SQL_DRIVER_HDESC  
        SQL_DROP_ASSERTION  
        SQL_DROP_CHARACTER_SET  
        SQL_DROP_COLLATION  
        SQL_DROP_DOMAIN  
        SQL_DROP_SCHEMA  
        SQL_DROP_TABLE  
        SQL_DROP_TRANSLATION  
        SQL_DROP_VIEW  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES1  
        SQL_DYNAMIC_CURSOR_ATTRIBUTES2  
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1  
        SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2  
        SQL_INFO_SCHEMA_VIEWS  
        SQL_INSERT_STATEMENT  
        SQL_KEYSET_CURSOR_ATTRIBUTES1  
        SQL_KEYSET_CURSOR_ATTRIBUTES2  
        SQL_MAX_ASYNC_CONCURRENT_STATEMENTS  
        SQL_MAX_IDENTIFIER_LEN  
        SQL_PARAM_ARRAY_ROW_COUNTS  
        SQL_PARAM_ARRAY_SELECTS  
        SQL_STATIC_CURSOR_ATTRIBUTES1  
        SQL_STATIC_CURSOR_ATTRIBUTES2  
        SQL_XOPEN_CLI_YEAR  
    :::column-end:::
:::row-end:::

## <a name="information-types-renamed-for-odbc-3x"></a>重新命名 ODBC 3.x 的資訊類型  

 ODBC 3.x 已重新命名 *InfoType* 引數的下列值。  

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

 ODBC 3.x 中的下列 *InfoType* 引數值已被取代。 ODBC 3.x 驅動程式必須繼續支援這些資訊類型，以便與 ODBC 2.x 應用程式回溯相容。  (如需這些類型的詳細資訊，請參閱附錄 G：適用于回溯相容性的驅動程式指導方針中的 [SQLGetInfo 支援](../appendixes/sqlgetinfo-support.md) 。 )   

:::row:::
    :::column:::
        SQL_FETCH_DIRECTION  
        SQL_LOCK_TYPES  
        SQL_ODBC_API_CONFORMANCE  
        SQL_ODBC_SQL_CONFORMANCE  
    :::column-end:::
    :::column:::
        SQL_POS_OPERATIONS  
        SQL_POSITIONED_STATEMENTS  
        SQL_SCROLL_CONCURRENCY  
        SQL_STATIC_SENSITIVITY  
    :::column-end:::
:::row-end:::

## <a name="information-type-descriptions"></a>資訊類型描述  

下表依字母順序列出每個資訊類型、所引進之 ODBC 的版本，以及其描述。  
  
|資訊類型|ODBC 版本|描述|
|-|-|-|
|SQL_ACCESSIBLE_PROCEDURES|1.0|字元字串：如果使用者可以執行 **SQLProcedures**傳回的所有程式，則為 "Y";如果有可能傳回使用者無法執行的程式，則為 "N"。|
|SQL_ACCESSIBLE_TABLES|1.0|字元字串： "Y" 如果使用者保證對**SQLTables**傳回的所有資料表具有**SELECT**許可權;如果使用者無法存取，則為 "N" （如果可能傳回資料表）。|
|SQL_ACTIVE_ENVIRONMENTS|3.0|SQLUSMALLINT 值，指定驅動程式可支援之作用中環境的最大數目。 如果沒有指定的限制或限制未知，此值會設為零。|
|SQL_AGGREGATE_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩列舉彙總函式的支援：<br/>SQL_AF_ALL<br/>SQL_AF_AVG<br/>SQL_AF_COUNT<br/>SQL_AF_DISTINCT<br/>SQL_AF_MAX<br/>SQL_AF_MIN<br/>SQL_AF_SUM<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回所有這些選項。|
|SQL_ALTER_DOMAIN|3.0|SQLUINTEGER 位元遮罩，用於列舉 **ALTER DOMAIN** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。 SQL-92 完整層級相容的驅動程式一律會傳回所有的位元遮罩。 傳回值為 "0" 表示不支援 **ALTER DOMAIN** 語句。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_AD_ADD_DOMAIN_CONSTRAINT = (完整層級支援加入網域條件約束) <br/>\<alter domain> \<set domain default clause> (完整層級支援 SQL_AD_ADD_DOMAIN_DEFAULT =) <br/>SQL_AD_CONSTRAINT_NAME_DEFINITION = \<constraint name definition clause> 支援命名網域條件約束 (中繼層級) <br/>\<drop domain constraint clause> (完整層級支援 SQL_AD_DROP_DOMAIN_CONSTRAINT =) <br/>\<alter domain> \<drop domain default clause> (完整層級支援 SQL_AD_DROP_DOMAIN_DEFAULT =) <br/><br/>\<constraint attributes>如果 \<add domain constraint> (SQL_AD_ADD_DOMAIN_CONSTRAINT 位設定) ，則下列位會指定支援的支援：<br/>SQL_AD_ADD_CONSTRAINT_DEFERRABLE (完整層級) <br/>SQL_AD_ADD_CONSTRAINT_NON_DEFERRABLE (完整層級) <br/>SQL_AD_ADD_CONSTRAINT_INITIALLY_DEFERRED (完整層級) <br/>SQL_AD_ADD_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級) |
|SQL_ALTER_TABLE|2.0|SQLUINTEGER 位元遮罩，列舉資料來源所支援的 **ALTER TABLE** 語句中的子句。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>支援 SQL_AT_ADD_COLUMN_COLLATION = \<add column> 子句，而設備可指定資料行定序 (完整層級)  (ODBC 3.0) <br/>支援 SQL_AT_ADD_COLUMN_DEFAULT = \<add column> 子句，而設備可指定資料行預設值 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_ADD_COLUMN_SINGLE = \<add column> (FIPS 過渡層級的支援)  (ODBC 3.0) <br/>支援 SQL_AT_ADD_CONSTRAINT = \<add column> 子句，而設備可指定資料行條件約束 (FIPS 過渡層級)  (ODBC 3.0) <br/>\<add table constraint> (FIPS 過渡層級)  (ODBC 3.0 中支援 SQL_AT_ADD_TABLE_CONSTRAINT = 子句) <br/>SQL_AT_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 支援將資料行和資料表條件約束命名 (中繼層級)  (ODBC 3.0) <br/>SQL_AT_DROP_COLUMN_CASCADE = \<drop column> CASCADE 支援 (FIPS 過渡層級)  (ODBC 3.0) <br/>SQL_AT_DROP_COLUMN_DEFAULT = \<alter column> \<drop column default clause> 支援 (中繼層級)  (ODBC 3.0) <br/>SQL_AT_DROP_COLUMN_RESTRICT = \<drop column> RESTRICT (FIPS 過渡層級的支援)  (ODBC 3.0) <br/>SQL_AT_DROP_TABLE_CONSTRAINT_CASCADE (ODBC 3.0) <br/>SQL_AT_DROP_TABLE_CONSTRAINT_RESTRICT = \<drop column> RESTRICT (FIPS 過渡層級的支援)  (ODBC 3.0) <br/>SQL_AT_SET_COLUMN_DEFAULT = \<alter column> \<set column default clause> 支援 (中繼層級)  (ODBC 3.0) <br/><br/>下列位會指定支援 \<constraint attributes> 指定資料行或資料表條件約束 (SQL_AT_ADD_CONSTRAINT 位設定) ：<br/>SQL_AT_CONSTRAINT_INITIALLY_DEFERRED (完整層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_DEFERRABLE (完整層級)  (ODBC 3.0) <br/>SQL_AT_CONSTRAINT_NON_DEFERRABLE (完整層級)  (ODBC 3.0) |
|SQL_ASYNC_DBC_FUNCTIONS|3.8|SQLUINTEGER 值，指出驅動程式是否可以在連接控制碼上以非同步方式執行函數。<br/><br/>SQL_ASYNC_DBC_CAPABLE = 驅動程式可以非同步執行連接函數。<br/>SQL_ASYNC_DBC_NOT_CAPABLE = 驅動程式無法以非同步方式執行連接函數。|
|SQL_ASYNC_MODE|3.0|SQLUINTEGER 值，指出驅動程式中的非同步支援層級：<br/><br/>SQL_AM_CONNECTION = 支援連接層級的非同步執行。 與指定之連接控制碼相關聯的所有語句控制碼都處於非同步模式，或全部都處於同步模式。 在相同連接上的另一個語句控制碼處於同步模式時，連接上的語句控制碼不可以是非同步模式，反之亦然。<br/>SQL_AM_STATEMENT = 語句層級的非同步執行支援。 與連接控制碼相關聯的某些語句控制碼可以處於非同步模式，而相同連接上的其他語句控制碼則處於同步模式。<br/>SQL_AM_NONE = 不支援非同步模式。|
|SQL_ASYNC_NOTIFICATION|3.8|SQLUINTEGER 值，指出驅動程式是否支援非同步通知：<br/><br/>SQL_ASYNC_NOTIFICATION_CAPABLE = 驅動程式支援非同步執行通知。<br/>SQL_ASYNC_NOTIFICATION_NOT_CAPABLE = 驅動程式不支援非同步執行通知。<br/><br/>ODBC 非同步作業有兩種類別：連接層級非同步作業和語句層級非同步作業。  如果驅動程式傳回 SQL_ASYNC_NOTIFICATION_CAPABLE，它必須支援可非同步執行之所有 Api 的通知。|
|SQL_BATCH_ROW_COUNT|3.0|SQLUINTEGER 位元遮罩，其會列舉有關資料列計數可用性的驅動程式行為。 下列位元遮罩會與資訊類型一起使用：<br/><br/>SQL_BRC_ROLLED_UP = 連續 INSERT、DELETE 或 UPDATE 語句的資料列計數會匯總成一個。 如果未設定此位，每個語句都可以使用資料列計數。<br/>SQL_BRC_PROCEDURES = 在預存程式中執行批次時，可使用資料列計數（如果有的話）。 如果有可用的資料列計數，您可以根據 SQL_BRC_ROLLED_UP 位來匯總或個別提供資料列計數。<br/>當您透過呼叫 **SQLExecute** 或 **SQLExecDirect**直接執行批次時，可使用 SQL_BRC_EXPLICIT = 資料列計數（如果有的話）。 如果有可用的資料列計數，您可以根據 SQL_BRC_ROLLED_UP 位來匯總或個別提供資料列計數。|
|SQL_BATCH_SUPPORT|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式對批次的支援。 下列位元遮罩可用來判斷支援的層級：<br/><br/>SQL_BS_SELECT_EXPLICIT = 驅動程式支援可擁有結果集產生語句的明確批次。<br/>SQL_BS_ROW_COUNT_EXPLICIT = 驅動程式支援可具有資料列計數產生語句的明確批次。<br/>SQL_BS_SELECT_PROC = 驅動程式支援可擁有結果集產生語句的明確程式。<br/>SQL_BS_ROW_COUNT_PROC = 驅動程式支援可具有資料列計數產生語句的明確程式。|
|SQL_BOOKMARK_PERSISTENCE|2.0|SQLUINTEGER 位元遮罩，用於列舉書簽保存的作業。 下列位元遮罩會與旗標一起使用，以判斷書簽保存的選項：<br/><br/>SQL_BP_CLOSE = 書簽在應用程式使用 SQL_CLOSE 選項呼叫 **SQLFreeStmt** 之後有效，或 **SQLCloseCursor** 以關閉與語句相關聯的資料指標。<br/>SQL_BP_DELETE = 在刪除資料列之後，資料列的書簽會是有效的。<br/>SQL_BP_DROP = 當應用程式呼叫具有*HandleType* SQL_HANDLE_STMT 的**SQLFreeHandle** ，以卸載語句之後，書簽會是有效的。<br/>SQL_BP_TRANSACTION = 書簽在應用程式認可或回復交易後有效。<br/>SQL_BP_UPDATE = 如果資料列中的任何資料行已更新（包括索引鍵資料行），則資料列的書簽會是有效的。<br/>SQL_BP_OTHER_HSTMT = 與某個語句相關聯的書簽可與另一個語句一起使用。 除非指定了 SQL_BP_CLOSE 或 SQL_BP_DROP，否則必須開啟第一個語句的資料指標。|
|SQL_CATALOG_LOCATION|2.0|SQLUSMALLINT 值，指出目錄在限定資料表名稱中的位置：<br/><br/>SQL_CL_START<br/>SQL_CL_END<br/>例如，Xbase 驅動程式會傳回 SQL_CL_START，因為目錄 (目錄) 名稱是在資料表名稱的開頭，如同 \EMPDATA\EMP。Dbf。 ORACLE 伺服器驅動程式會傳回 SQL_CL_END，因為目錄位於資料表名稱的結尾，如下所示 ADMIN.EMP@EMPDATA 。<br/><br/>符合 SQL 92 的完整等級標準驅動程式一律會傳回 SQL_CL_START。 如果資料來源不支援目錄，則會傳回0值。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫 **SQLGetInfo** 。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_LOCATION 重新命名為 odbc 3.0。|
|SQL_CATALOG_NAME|3.0|字元字串：若伺服器支援目錄名稱，則為 "Y"，否則為 "N"。<br/><br/>符合 SQL 92 的完整等級標準驅動程式一律會傳回 "Y"。|
|SQL_CATALOG_NAME_SEPARATOR|1.0|字元字串：資料來源在目錄名稱和其後或之前的限定名稱專案之間定義為分隔符號的字元。<br/><br/>如果資料來源不支援目錄，則會傳回空字串。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫 **SQLGetInfo** 。 符合 SQL 92 的完整等級標準驅動程式一律會傳回 "."。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_NAME_SEPARATOR 重新命名為 odbc 3.0。|
|SQL_CATALOG_TERM|1.0|具有目錄之資料來源廠商名稱的字元字串;例如，「資料庫」或「目錄」。 這個字串可以是大寫、小寫或混合大小寫。<br/><br/>如果資料來源不支援目錄，則會傳回空字串。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫 **SQLGetInfo** 。 符合 SQL 92 的完整等級標準驅動程式一律會傳回「目錄」。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_TERM 重新命名為 odbc 3.0。|
|SQL_CATALOG_USAGE|2.0|SQLUINTEGER 位元遮罩，列舉可以使用目錄的語句。<br/><br/>下列位元遮罩可用來決定可以使用目錄的位置：<br/>SQL_CU_DML_STATEMENTS = 目錄在所有資料操作語言語句中都受到支援： **select**、 **INSERT**、 **UPDATE**、 **DELETE**和（如果支援的話），請 **選取 update** 和定點更新和刪除語句。<br/>SQL_CU_PROCEDURE_INVOCATION = ODBC 程序呼叫語句中支援目錄。<br/>SQL_CU_TABLE_DEFINITION = 所有資料表定義語句都支援目錄： **CREATE TABLE**、 **CREATE VIEW**、 **ALTER Table**、 **drop table**和 **drop VIEW**。<br/>SQL_CU_INDEX_DEFINITION = 所有索引定義語句都支援目錄： **CREATE INDEX** 和 **DROP INDEX**。<br/>SQL_CU_PRIVILEGE_DEFINITION = 擁有權限定義語句都支援目錄： **GRANT** 和 **REVOKE**。<br/><br/>如果資料來源不支援目錄，則會傳回0值。 為了判斷是否支援目錄，應用程式會使用 SQL_CATALOG_NAME 資訊類型來呼叫 **SQLGetInfo** 。 符合 SQL 92 的完整等級標準驅動程式一律會傳回所有設定的位元遮罩。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_QUALIFIER_USAGE 重新命名為 odbc 3.0。|
|SQL_COLLATION_SEQ|3.0|定序順序的名稱。 這是一個字元字串，表示此伺服器預設字元集的預設定序名稱 (例如 ' ISO 8859-1 ' 或 EBCDIC) 。 如果這是未知的，則會傳回空字串。 符合 SQL 92 的完整等級標準驅動程式一律會傳回非空白字串。|
|SQL_COLUMN_ALIAS|2.0|字元字串：如果資料來源支援資料行別名，則為 "Y";否則為 "N"。<br/><br/>您可以使用 AS 子句，在選取清單中指定資料行別名的替代名稱。 符合 SQL-92 專案層級的驅動程式一律會傳回 "Y"。|
|SQL_CONCAT_NULL_BEHAVIOR|1.0|SQLUSMALLINT 值，指出資料來源如何處理 Null 值字元資料類型資料行與非 Null 值字元資料類型資料行的串連：<br/>SQL_CB_Null = 結果為 Null 值。<br/>SQL_CB_NON_Null = 結果為非 Null 值資料行或資料行的串連。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_CB_Null。|
|SQL_CONVERT_BIGINT<br/>SQL_CONVERT_BINARY<br/>SQL_CONVERT_BIT<br/>SQL_CONVERT_CHAR<br/>SQL_CONVERT_GUID<br/>SQL_CONVERT_DATE<br/>SQL_CONVERT_DECIMAL<br/>SQL_CONVERT_DOUBLE<br/>SQL_CONVERT_FLOAT<br/>SQL_CONVERT_INTEGER<br/>SQL_CONVERT_INTERVAL_YEAR_MONTH<br/>SQL_CONVERT_INTERVAL_DAY_TIME<br/>SQL_CONVERT_LONGVARBINARY<br/>SQL_CONVERT_LONGVARCHAR<br/>SQL_CONVERT_NUMERIC<br/>SQL_CONVERT_REAL<br/>SQL_CONVERT_SMALLINT<br/>SQL_CONVERT_TIME<br/>SQL_CONVERT_TIMESTAMP<br/>SQL_CONVERT_TINYINT<br/>SQL_CONVERT_VARBINARY<br/>SQL_CONVERT_VARCHAR|1.0|SQLUINTEGER 位元遮罩。 位元遮罩表示資料來源所支援的轉換，以及在*InfoType*中名為之型別資料的**CONVERT**純量函數。 如果位元遮罩等於零，則資料來源不支援從命名類型的資料進行任何轉換，包括轉換成相同的資料類型。<br/><br/>例如，若要判斷資料來源是否支援將 SQL_INTEGER 資料轉換成 SQL_BIGINT 資料類型，應用程式會以 SQL_CONVERT_INTEGER 的*InfoType*呼叫**SQLGetInfo** 。 應用程式會使用傳回的位元遮罩和 SQL_CVT_BIGINT 來執行 **和** 操作。 如果產生的值為非零值，則會支援轉換。<br/><br/>下列位元遮罩可用來判斷支援的轉換：<br/>SQL_CVT_BIGINT (ODBC 1.0) <br/>SQL_CVT_BINARY (ODBC 1.0) <br/>SQL_CVT_BIT (ODBC 1.0) <br/>SQL_CVT_GUID (ODBC 3.5) <br/>SQL_CVT_CHAR (ODBC 1.0) <br/>SQL_CVT_DATE (ODBC 1.0) <br/>SQL_CVT_DECIMAL (ODBC 1.0) <br/>SQL_CVT_DOUBLE (ODBC 1.0) <br/>SQL_CVT_FLOAT (ODBC 1.0) <br/>SQL_CVT_INTEGER (ODBC 1.0) <br/>SQL_CVT_INTERVAL_YEAR_MONTH (ODBC 3.0) <br/>SQL_CVT_INTERVAL_DAY_TIME (ODBC 3.0) <br/>SQL_CVT_LONGVARBINARY (ODBC 1.0) <br/>SQL_CVT_LONGVARCHAR (ODBC 1.0) <br/>SQL_CVT_NUMERIC (ODBC 1.0) <br/>SQL_CVT_REAL (ODBC 1.0) <br/>SQL_CVT_SMALLINT (ODBC 1.0) <br/>SQL_CVT_TIME (ODBC 1.0) <br/>SQL_CVT_TIMESTAMP (ODBC 1.0) <br/>SQL_CVT_TINYINT (ODBC 1.0) <br/>SQL_CVT_VARBINARY (ODBC 1.0) <br/>SQL_CVT_VARCHAR (ODBC 1.0) |
|SQL_CONVERT_FUNCTIONS|1.0|SQLUINTEGER 位元遮罩，用來列舉驅動程式和相關聯資料來源所支援的純量轉換函數。<br/><br/>下列位元遮罩可用來判斷支援的轉換函數：<br/>SQL_FN_CVT_CASTSQL_FN_CVT_CONVERT|
|SQL_CORRELATION_NAME|1.0|SQLUSMALLINT 值，指出是否支援資料表相互關聯名稱：<br/>SQL_CN_NONE = 不支援相互關聯名稱。<br/>SQL_CN_DIFFERENT = 支援相互關聯名稱，但必須與它們所代表之資料表的名稱不同。<br/>SQL_CN_ANY = 支援相互關聯名稱，而且可以是任何有效的使用者定義名稱。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_CN_ANY。|
|SQL_CREATE_ASSERTION|3.0|SQLUINTEGER 位元遮罩，用來列舉 **CREATE** 判斷提示語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CA_CREATE_ASSERTION<br/><br/>如果支援指定條件約束屬性的功能，下列位會指定支援的條件約束屬性 (請參閱 SQL_ALTER_TABLE 和 SQL_CREATE_TABLE 資訊類型) ：<br/>SQL_CA_CONSTRAINT_INITIALLY_DEFERRED<br/>SQL_CA_CONSTRAINT_INITIALLY_IMMEDIATE<br/>SQL_CA_CONSTRAINT_DEFERRABLE<br/>SQL_CA_CONSTRAINT_NON_DEFERRABLE<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回所有這些選項的支援。 傳回值為 "0" 表示不支援 **CREATE ASSERTION** 語句。|
|SQL_CREATE_CHARACTER_SET|3.0|SQLUINTEGER 位元遮罩，用來列舉 **CREATE CHARACTER SET** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CCS_CREATE_CHARACTER_SET<br/>SQL_CCS_COLLATE_CLAUSE<br/>SQL_CCS_LIMITED_COLLATION<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回所有這些選項的支援。 傳回值為 "0" 表示不支援 **CREATE CHARACTER SET** 語句。|
|SQL_CREATE_COLLATION|3.0|SQLUINTEGER 位元遮罩，用來列舉 **CREATE 定序** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CCOL_CREATE_COLLATION<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回此選項的支援。 傳回值為 "0" 表示不支援 **CREATE 定序** 語句。|
|SQL_CREATE_DOMAIN|3.0|SQLUINTEGER 位元遮罩，用來列舉 **CREATE DOMAIN** 語句中的子句，如 SQL-92 中所定義，資料來源支援這些子句。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CDO_CREATE_DOMAIN = (中繼層級) 支援 CREATE DOMAIN 語句。<br/>SQL_CDO_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 支援 (中繼層級) 命名網域條件約束。<br/><br/>下列位指定建立資料行條件約束的能力：<br/>SQL_CDO_DEFAULT = (中繼層級支援指定網域條件約束) <br/>SQL_CDO_CONSTRAINT = (中繼層級支援指定網域預設值) <br/>SQL_CDO_COLLATION = (完整層級支援指定網域定序) <br/><br/>如果支援指定網域條件約束，則下列位會指定支援的條件約束屬性 (SQL_CDO_DEFAULT 設定) ：<br/>SQL_CDO_CONSTRAINT_INITIALLY_DEFERRED (完整層級) <br/>SQL_CDO_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級) <br/>SQL_CDO_CONSTRAINT_DEFERRABLE (完整層級) <br/>SQL_CDO_CONSTRAINT_NON_DEFERRABLE (完整層級) <br/><br/>傳回值為 "0" 表示不支援 **CREATE DOMAIN** 語句。|
|SQL_CREATE_SCHEMA|3.0|SQLUINTEGER 位元遮罩，用於列舉 **CREATE SCHEMA** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CS_CREATE_SCHEMA<br/>SQL_CS_AUTHORIZATION<br/>SQL_CS_DEFAULT_CHARACTER_SET<br/><br/>符合 SQL-92 中繼等級標準的驅動程式一律會傳回所支援的 SQL_CS_CREATE_SCHEMA 和 SQL_CS_AUTHORIZATION 選項。 這些也必須在 SQL-92 專案層級支援，但不一定是 SQL 語句。 符合 SQL-92 的完整等級標準驅動程式一律會傳回所有這些選項的支援。|
|SQL_CREATE_TABLE|3.0|SQLUINTEGER 位元遮罩，用來列舉 **CREATE TABLE** 語句中的子句，如 SQL-92 中所定義，資料來源所支援。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CT_CREATE_TABLE = 支援 CREATE TABLE 語句。  (專案層級) <br/>SQL_CT_TABLE_CONSTRAINT = (FIPS 過渡層級支援指定資料表條件約束) <br/>SQL_CT_CONSTRAINT_NAME_DEFINITION = \<constraint name definition> 子句可用於將資料行和資料表條件約束命名 (中繼層級) <br/><br/>下列位指定建立臨時表的能力：<br/>SQL_CT_COMMIT_PRESERVE = 已刪除的資料列會保留在認可上。  (完整層級) <br/>SQL_CT_COMMIT_DELETE = 已刪除的資料列會在認可時刪除。  (完整層級) <br/>SQL_CT_GLOBAL_TEMPORARY = 可以建立全域臨時表。  (完整層級) <br/>SQL_CT_LOCAL_TEMPORARY = 可以建立本機臨時表。  (完整層級) <br/><br/>下列位指定建立資料行條件約束的能力：<br/>SQL_CT_COLUMN_CONSTRAINT = (FIPS 過渡層級支援指定資料行條件約束) <br/>SQL_CT_COLUMN_DEFAULT = (FIPS 過渡層級支援指定資料行預設值) <br/>SQL_CT_COLUMN_COLLATION = (完整層級支援指定資料行定序) <br/><br/>如果支援指定資料行或資料表條件約束，下列位會指定支援的條件約束屬性：<br/>SQL_CT_CONSTRAINT_INITIALLY_DEFERRED (完整層級) <br/>SQL_CT_CONSTRAINT_INITIALLY_IMMEDIATE (完整層級) <br/>SQL_CT_CONSTRAINT_DEFERRABLE (完整層級) <br/>SQL_CT_CONSTRAINT_NON_DEFERRABLE (完整層級) |
|SQL_CREATE_TRANSLATION|3.0|SQLUINTEGER 位元遮罩，列舉資料來源所支援之 **CREATE 轉譯** 語句中的子句，如 SQL-92 中所定義。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CTR_CREATE_TRANSLATION<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回這些選項的支援。 傳回值為 "0" 表示不支援 **CREATE 轉譯** 語句。|
|SQL_CREATE_VIEW|3.0|SQLUINTEGER 位元遮罩，用來列舉 **CREATE VIEW** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_CV_CREATE_VIEW<br/>SQL_CV_CHECK_OPTION<br/>SQL_CV_CASCADED<br/>SQL_CV_LOCAL<br/><br/>傳回值為 "0" 表示不支援 **CREATE VIEW** 語句。<br/><br/>符合 SQL-92 專案等級標準的驅動程式一律會傳回支援的 SQL_CV_CREATE_VIEW 和 SQL_CV_CHECK_OPTION 選項。<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回所有這些選項的支援。|
|SQL_CURSOR_COMMIT_BEHAVIOR|1.0|SQLUSMALLINT 值，指出當您認可交易) 時， **認可** 作業如何影響資料來源中的資料指標和備妥的語句 (資料來源的行為。<br/><br/>這個屬性的值會反映下一個設定的目前狀態： SQL_COPT_SS_PRESERVE_CURSORS。<br/>SQL_CB_DELETE = 關閉資料指標，並刪除備妥的語句。 若要再次使用資料指標，應用程式必須 reprepare 並重新執行語句。<br/>SQL_CB_CLOSE = Close 資料指標。 針對備妥的語句，應用程式可以在語句上呼叫 **SQLExecute** ，而不需要再次呼叫 **SQLPrepare** 。 SQL ODBC 驅動程式的預設值為 SQL_CB_CLOSE。 這表示當您認可交易時，SQL ODBC 驅動程式將會關閉資料指標 (s) 。<br/>SQL_CB_PRESERVE = 將資料指標保留在 **認可** 作業之前的相同位置。 應用程式可以繼續提取資料，也可以關閉資料指標並重新執行語句，而不需 repreparing。|
|SQL_CURSOR_ROLLBACK_BEHAVIOR|1.0|SQLUSMALLINT 值，指出 **復原** 作業如何影響資料來源中的資料指標和備妥的語句：<br/>SQL_CB_DELETE = 關閉資料指標，並刪除備妥的語句。 若要再次使用資料指標，應用程式必須 reprepare 並重新執行語句。<br/>SQL_CB_CLOSE = Close 資料指標。 針對備妥的語句，應用程式可以在語句上呼叫 **SQLExecute** ，而不需要再次呼叫 **SQLPrepare** 。<br/>SQL_CB_PRESERVE = 將資料指標保留在 **ROLLBACK** 作業之前的相同位置。 應用程式可以繼續提取資料，也可以關閉資料指標並重新執行語句，而不需 repreparing。|
|SQL_CURSOR_SENSITIVITY|3.0|SQLUINTEGER 值，指出資料指標敏感度的支援：<br/>SQL_INSENSITIVE = 語句控制碼上的所有資料指標都會顯示結果集，而不會反映相同交易中任何其他資料指標所做的任何變更。<br/>SQL_UNSPECIFIED = 未指定語句控制碼上的資料指標是否會顯示相同交易中另一個資料指標對結果集所做的變更。 語句控制碼上的資料指標可能會顯示為無、部分或所有這類變更。<br/>SQL_SENSITIVE = 資料指標對相同交易中的其他資料指標所做的變更很敏感。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回支援的 SQL_UNSPECIFIED 選項。<br/><br/>符合 SQL 92 的完整等級標準驅動程式一律會傳回支援的 SQL_INSENSITIVE 選項。|
|SQL_DATA_SOURCE_NAME|1.0|具有在連接期間使用之資料來源名稱的字元字串。 如果是名為 **SQLConnect**的應用程式，這就是 *szDSN* 引數的值。 如果應用程式呼叫 **SQLDriverConnect** 或 **SQLBrowseConnect**，這就是傳遞至驅動程式之連接字串中的 DSN 關鍵字值。 如果連接字串未包含 **DSN** 關鍵字 (例如，當它包含 **DRIVER** 關鍵字) 時，這就是空字串。|
|SQL_DATA_SOURCE_READ_ONLY|1.0|字元字串。 如果資料來源設定為唯讀模式，則為 "Y"，否則為 "N"。<br/><br/>此特性僅適用于資料來源本身;它不是可讓您存取資料來源之驅動程式的特性。 可讀取/寫入的驅動程式可搭配唯讀的資料來源使用。 如果驅動程式是唯讀的，它的所有資料來源都必須是唯讀的，而且必須傳回 SQL_DATA_SOURCE_READ_ONLY。|
|SQL_DATABASE_NAME|1.0|如果資料來源定義名為 "database" 的命名物件，則為使用中目前資料庫名稱的字元字串。<br/><br/>在 ODBC 3.x 中，藉由呼叫**SQLGetConnectAttr**與 SQL_ATTR_CURRENT_CATALOG 的*屬性*引數，也可以傳回這個*InfoType*的傳回值。|
|SQL_DATETIME_LITERALS|3.0|SQLUINTEGER 位元遮罩，可列舉資料來源所支援的 SQL-92 datetime 常值。 請注意，這些是 SQL-92 規格中所列的日期時間常值，而且與 ODBC 所定義的日期時間常值 escape 子句不同。 如需 ODBC datetime 常值 escape 子句的詳細資訊，請參閱 [日期、時間和時間戳記常](../develop-app/date-time-and-timestamp-literals.md)值。<br/><br/> 符合 FIPS 過渡等級標準的驅動程式一律會在下列清單中的位位元遮罩中傳回 "1" 值。 值為 "0" 表示不支援 SQL-92 datetime 常值。<br/><br/>下列位元遮罩可用來判斷支援的常值：<br/>SQL_DL_SQL92_DATE<br/>SQL_DL_SQL92_TIME<br/>SQL_DL_SQL92_TIMESTAMP<br/>SQL_DL_SQL92_INTERVAL_YEAR<br/>SQL_DL_SQL92_INTERVAL_MONTH<br/>SQL_DL_SQL92_INTERVAL_DAY<br/>SQL_DL_SQL92_INTERVAL_HOUR<br/>SQL_DL_SQL92_INTERVAL_MINUTE<br/>SQL_DL_SQL92_INTERVAL_SECOND<br/>SQL_DL_SQL92_INTERVAL_YEAR_TO_MONTH<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_HOUR<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_MINUTE<br/>SQL_DL_SQL92_INTERVAL_DAY_TO_SECOND<br/>SQL_DL_SQL92_INTERVAL_HOUR_TO_MINUTE<br/>SQL_DL_SQL92_INTERVAL_HOUR_TO_SECOND<br/>SQL_DL_SQL92_INTERVAL_MINUTE_TO_SECOND|
|SQL_DBMS_NAME|1.0|具有驅動程式所存取 DBMS 產品名稱的字元字串。|
|SQL_DBMS_VER|1.0|字元字串，指出驅動程式所存取之 DBMS 產品的版本。 版本的格式為 # #. # #. # # # #，其中前兩個數字是主要版本，接下來的兩個數字是次要版本，而最後四個數字是發行版本。 驅動程式必須以這個格式轉譯 DBMS 產品版本，但也可以附加 DBMS 產品特定版本。 例如，"04.01.0000 Rdb 4.1"。|
|SQL_DDL_INDEX|3.0|表示支援建立和卸載索引的 SQLUINTEGER 值：<br/>SQL_DI_CREATE_INDEX<br/>SQL_DI_DROP_INDEX|
|SQL_DEFAULT_TXN_ISOLATION|1.0|SQLUINTEGER 值，指出驅動程式或資料來源所支援的預設交易隔離等級，如果資料來源不支援交易，則為零。 下列詞彙是用來定義交易隔離等級：<br/>中途**讀取**交易1會變更資料列。 交易2會在交易1認可變更之前，讀取已變更的資料列。 如果交易1復原變更，交易2將會讀取一個被視為永遠不存在的資料列。<br/>**不可重複的讀取** 交易1讀取資料列。 交易2會更新或刪除該資料列，並認可此變更。 如果交易1嘗試重新讀取資料列，則會收到不同的資料列值，或發現資料列已被刪除。<br/>**虛構** 交易1會讀取符合某些搜尋準則的一組資料列。 交易2會透過符合搜尋準則的插入或更新) 來產生一或多個資料列 (。 如果交易1重新執行讀取資料列的語句，則會接收一組不同的資料列。<br/><br/>如果資料來源支援交易，驅動程式會傳回下列其中一個位元遮罩：<br/>SQL_TXN_READ_UNCOMMITTED = 中途讀取、不可重複的讀取和幻像是可行的。<br/>SQL_TXN_READ_COMMITTED = 不可能發生中途讀取。 不可重複的讀取和幻像是可行的。<br/>SQL_TXN_REPEATABLE_READ = 中途讀取和不可重複的讀取是不可能的。 可以有幻像。<br/>SQL_TXN_SERIALIZABLE = 交易可序列化。 可序列化交易不允許中途讀取、不可重複的讀取或幻像。|
|SQL_DESCRIBE_PARAMETER|3.0|字元字串：如果可以描述參數，則為 "Y";"N"，否則為。<br/><br/>SQL-92 完整層級一致的驅動程式通常會傳回 "Y"，因為它將支援 **描述輸入** 語句。 因為這並不會直接指定基礎 SQL 支援，所以可能不支援描述參數，即使在符合 SQL-92 的完整等級的驅動程式中也是如此。|
|SQL_DM_VER|3.0|具有驅動程式管理員版本的字元字串。 版本的格式為 # #. # #. # # # #. # # # #，其中：<br/>這兩個數字的第一組是主要 ODBC 版本，如常數 SQL_SPEC_MAJOR 所提供。<br/>這兩個數字的第二組是次要 ODBC 版本，如常數 SQL_SPEC_MINOR 所提供。<br/>第三組四個數字是驅動程式管理員主要組建編號。<br/>四個數字的最後一組是驅動程式管理員次要組建編號。<br/>Windows 7 驅動程式管理員版本為03.80。 Windows 8 驅動程式管理員版本為03.81。|
|SQL_DRIVER_AWARE_POOLING_SUPPORTED|3.8|SQLUINTEGER 值，指出驅動程式是否支援驅動程式感知的共用。  (需詳細資訊，請參閱 [驅動程式感知的連接](../develop-app/driver-aware-connection-pooling.md)共用。<br/><br/>SQL_DRIVER_AWARE_POOLING_CAPABLE 指出驅動程式可支援驅動程式感知的共用機制。<br/>SQL_DRIVER_AWARE_POOLING_NOT_CAPABLE 指出驅動程式無法支援驅動程式感知的共用機制。<br/><br/>驅動程式不需要執行 SQL_DRIVER_AWARE_POOLING_SUPPORTED，驅動程式管理員將不會接受驅動程式的傳回值。|
|SQL_DRIVER_HDBCSQL_DRIVER_HENV|1.0|SQLULEN 值、驅動程式的環境控制碼或連接控制碼（由引數 *InfoType*所決定）。<br/><br/>這些資訊類型只由驅動程式管理員來執行。|
|SQL_DRIVER_HDESC|3.0|SQLULEN 值，驅動程式管理員的描述項控制碼所決定的驅動程式描述項控制碼，必須 \* 從應用程式傳遞至*InfoValuePtr*中的輸入。 在此情況下， *InfoValuePtr* 同時為輸入和輸出引數。 在 InfoValuePtr 中傳遞的輸入描述項控制碼 \* *InfoValuePtr*必須明確或隱含地在*ConnectionHandle*上進行配置。<br/><br/>應用程式必須先複製驅動程式管理員的描述項控制碼，才能使用這種資訊類型來呼叫 **SQLGetInfo** ，以確保在輸出時不會覆寫控制碼。<br/><br/>此資訊類型只由驅動程式管理員來執行。|
|SQL_DRIVER_HLIB|2.0|SQLULEN 值，當載入器載入 Microsoft Windows 作業系統上的驅動程式 DLL 或在另一個作業系統上的對等專案時，會從載入程式庫將 *hinst* 傳回至驅動程式管理員。 控制碼只對 **SQLGetInfo**呼叫中指定的連接控制碼有效。<br/><br/>此資訊類型只由驅動程式管理員來執行。|
|SQL_DRIVER_HSTMT|1.0|SQLULEN 值，驅動程式管理員語句控制碼所決定的驅動程式語句控制碼，必須從應用程式傳遞至 \* *InfoValuePtr*中的輸入。 在此情況下， *InfoValuePtr* 同時為輸入和輸出引數。 在 InfoValuePtr 中傳遞的輸入語句控制碼必須已經配置 \* *InfoValuePtr*在引數*ConnectionHandle*上。<br/><br/>應用程式必須先複製驅動程式管理員的語句控制碼，然後才能使用此資訊類型來呼叫 **SQLGetInfo** ，以確保在輸出時不會覆寫該控制碼。<br/><br/>此資訊類型只由驅動程式管理員來執行。|
|SQL_DRIVER_NAME|1.0|字元字串，其中包含用來存取資料來源之驅動程式的檔案名。|
|SQL_DRIVER_ODBC_VER|2.0|具有驅動程式支援之 ODBC 版本的字元字串。 版本的格式為 # #. # #，其中前兩個數字是主要版本，而下兩個數字是次要版本。 SQL_SPEC_MAJOR 和 SQL_SPEC_MINOR 定義主要和次要版本號碼。 針對此手冊中所述的 ODBC 版本，這些是3和0，而驅動程式應該會傳回 "03.00"。<br/><br/>ODBC 驅動程式管理員不會修改 SQLGetInfo (的傳回值 SQL_DRIVER_ODBC_VER) 來維持現有應用程式的回溯相容性。 驅動程式會指定將傳回的值。 不過，支援 C 資料類型擴充性的驅動程式必須在應用程式呼叫 **SQLSetEnvAttr** 以將 SQL_ATTR_ODBC_VERSION 設定為3.8 時，傳回 3.8 (或更高的) 。 如需詳細資訊，請參閱 [ODBC 中的 C 資料類型](../develop-app/c-data-types-in-odbc.md)。|
|SQL_DRIVER_VER|1.0|具有驅動程式版本的字元字串，以及驅動程式的選擇性描述。 版本的最小值為 # #. # #. # # # #，其中前兩個數字是主要版本，接下來的兩個數字是次要版本，而最後四個數字是發行版本。|
|SQL_DROP_ASSERTION|3.0|SQLUINTEGER 位元遮罩，其會列舉 **DROP** 判斷提示語句中的子句，如 SQL-92 中所定義的資料來源所支援的子句。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DA_DROP_ASSERTION<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回此選項的支援。|
|SQL_DROP_CHARACTER_SET|3.0|SQLUINTEGER 位元遮罩，用來列舉 **放置字元集** 語句中的子句，如 SQL-92 中所定義，資料來源所支援的子句。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DCS_DROP_CHARACTER_SET<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回此選項的支援。|
|SQL_DROP_COLLATION|3.0|SQLUINTEGER 位元遮罩，列舉 **DROP 定序** 語句中的子句，如 SQL-92 中所定義，資料來源所支援的子句。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DC_DROP_COLLATION<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回此選項的支援。|
|SQL_DROP_DOMAIN|3.0|SQLUINTEGER 位元遮罩，可列舉資料來源所支援的 **DROP DOMAIN** 語句中的子句，如 SQL-92 中所定義。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DD_DROP_DOMAIN<br/>SQL_DD_CASCADE<br/>SQL_DD_RESTRICT<br/><br/>符合 SQL-92 中繼等級標準的驅動程式一律會傳回所有這些選項的支援。|
|SQL_DROP_SCHEMA|3.0|SQLUINTEGER 位元遮罩，用來列舉 **DROP SCHEMA** 語句中的子句，如 SQL-92 中所定義的資料來源所支援的子句。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DS_DROP_SCHEMA<br/>SQL_DS_CASCADE<br/>SQL_DS_RESTRICT<br/><br/>符合 SQL-92 中繼等級標準的驅動程式一律會傳回所有這些選項的支援。|
|SQL_DROP_TABLE|3.0|SQLUINTEGER 位元遮罩，用來列舉 **DROP TABLE** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DT_DROP_TABLE<br/>SQL_DT_CASCADE<br/>SQL_DT_RESTRICT<br/><br/>符合 FIPS 過渡等級標準的驅動程式一律會傳回所有這些選項的支援。|
|SQL_DROP_TRANSLATION|3.0|SQLUINTEGER 位元遮罩，用來列舉卸載 **轉譯** 語句中的子句，如 SQL-92 中所定義，由資料來源支援。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DTR_DROP_TRANSLATION<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回此選項的支援。|
|SQL_DROP_VIEW|3.0|SQLUINTEGER 位元遮罩，用來列舉 **DROP VIEW** 語句中的子句，如 SQL-92 中所定義，資料來源所支援的子句。<br/><br/>下列位元遮罩可用來判斷支援的子句：<br/>SQL_DV_DROP_VIEW<br/>SQL_DV_CASCADE<br/>SQL_DV_RESTRICT<br/><br/>符合 FIPS 過渡等級標準的驅動程式一律會傳回所有這些選項的支援。|
|SQL_DYNAMIC_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援的動態資料指標屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA1_NEXT = 當資料指標為動態資料指標時，對**SQLFetchScroll**的呼叫中支援 SQL_FETCH_NEXT 的*FetchOrientation*引數。<br/>SQL_CA1_ABSOLUTE = 當資料指標為動態資料指標時， **SQLFetchScroll**呼叫中支援 SQL_FETCH_FIRST、SQL_FETCH_LAST 和 SQL_FETCH_ABSOLUTE 的*FetchOrientation*引數。  (將提取的資料列集與目前的資料指標位置無關。 ) <br/>SQL_CA1_RELATIVE = 當資料指標為動態資料指標時， **SQLFetchScroll**呼叫中支援 SQL_FETCH_PRIOR 和 SQL_FETCH_RELATIVE 的*FetchOrientation*引數。  (將提取的資料列集取決於目前的資料指標位置。 請注意，這會與 SQL_FETCH_NEXT 分隔，因為在順向資料指標中，只支援 SQL_FETCH_NEXT。 ) <br/>SQL_CA1_BOOKMARK = 當資料指標為動態資料指標時，對**SQLFetchScroll**的呼叫中支援 SQL_FETCH_BOOKMARK 的*FetchOrientation*引數。<br/>SQL_CA1_LOCK_EXCLUSIVE = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_LOCK_EXCLUSIVE 的*LockType*引數。<br/>SQL_CA1_LOCK_NO_CHANGE = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_LOCK_NO_CHANGE 的*LockType*引數。<br/>SQL_CA1_LOCK_UNLOCK = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_LOCK_UNLOCK 的*LockType*引數。<br/>SQL_CA1_POS_POSITION = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_POSITION 的*操作*引數。<br/>SQL_CA1_POS_UPDATE = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_UPDATE 的*操作*引數。<br/>SQL_CA1_POS_DELETE = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_DELETE 的*操作*引數。<br/>SQL_CA1_POS_REFRESH = 當資料指標為動態資料指標時，對**SQLSetPos**的呼叫中支援 SQL_REFRESH 的*操作*引數。<br/>SQL_CA1_POSITIONED_UPDATE = 當資料指標為動態資料指標時，支援目前 SQL 語句的更新。  (符合 SQL-92 專案層級的驅動程式一律會根據支援傳回此選項。 ) <br/>SQL_CA1_POSITIONED_DELETE = 刪除：當資料指標是動態資料指標時，支援目前的 SQL 語句。  (符合 SQL-92 專案層級的驅動程式一律會根據支援傳回此選項。 ) <br/>SQL_CA1_SELECT_FOR_UPDATE = 當資料指標是動態資料指標時，支援 SELECT FOR UPDATE SQL 語句。  (符合 SQL-92 專案層級的驅動程式一律會根據支援傳回此選項。 ) <br/>SQL_CA1_BULK_ADD = 當資料指標為動態資料指標時，對**SQLBulkOperations**的呼叫中支援 SQL_ADD 的*操作*引數。<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK = 當資料指標為動態資料指標時，對**SQLBulkOperations**的呼叫中支援 SQL_UPDATE_BY_BOOKMARK 的*操作*引數。<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK = 當資料指標為動態資料指標時，對**SQLBulkOperations**的呼叫中支援 SQL_DELETE_BY_BOOKMARK 的*操作*引數。<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK = 當資料指標為動態資料指標時，對**SQLBulkOperations**的呼叫中支援 SQL_FETCH_BY_BOOKMARK 的*操作*引數。<br/><br/>符合 SQL-92 中繼等級標準的驅動程式通常會傳回所支援的 SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項，因為它支援透過內嵌 SQL FETCH 語句的可滾動資料指標。 不過，因為這不會直接判斷基礎 SQL 支援，所以即使是針對 SQL-92 中繼層級的驅動程式，也可能不支援可滾動的資料指標。|
|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援的動態資料指標屬性。 此位元遮罩包含第二個屬性子集;如需第一個子集，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA2_READ_ONLY_CONCURRENCY = 唯讀動態資料指標，不允許任何更新，因此可支援。  (SQL_ATTR_CONCURRENCY 語句屬性可以 SQL_CONCUR_READ_ONLY 動態資料指標) 。<br/>SQL_CA2_LOCK_CONCURRENCY = 動態資料指標，其使用最低層級的鎖定，以確保可支援更新資料列。  (動態資料指標可以 SQL_CONCUR_LOCK SQL_ATTR_CONCURRENCY 語句屬性。 ) 這些鎖定必須與 SQL_ATTR_TXN_ISOLATION 連接屬性所設定的交易隔離等級一致。<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY = 支援使用開放式並行存取控制比較資料列版本的動態資料指標。  (動態資料指標可以 SQL_CONCUR_ROWVER SQL_ATTR_CONCURRENCY 的語句屬性。 ) <br/>SQL_CA2_OPT_VALUES_CONCURRENCY = 支援使用開放式並行存取控制比較值的動態資料指標。  (動態資料指標可以 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 的語句屬性。 ) <br/>SQL_CA2_SENSITIVITY_ADDITIONS = 動態資料指標可以看見新增的資料列;游標可以滾動至這些資料列。  (將這些資料列新增至資料指標的位置會與驅動程式相依。 ) <br/>SQL_CA2_SENSITIVITY_DELETIONS = 動態資料指標無法再使用已刪除的資料列，也不會在結果集中留下 "洞";動態資料指標從已刪除的資料列中滾動之後，就無法返回該資料列。<br/>SQL_CA2_SENSITIVITY_UPDATES = 動態資料指標可以看到資料列的更新;如果動態資料指標從和傳回已更新的資料列，資料指標所傳回的資料就會是更新的資料，而不是原始資料。<br/>SQL_CA2_MAX_ROWS_SELECT = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響 **SELECT** 語句。<br/>SQL_CA2_MAX_ROWS_INSERT = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響 **INSERT** 語句。<br/>SQL_CA2_MAX_ROWS_DELETE = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響 **DELETE** 語句。<br/>SQL_CA2_MAX_ROWS_UPDATE = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響 **UPDATE** 語句。<br/>SQL_CA2_MAX_ROWS_CATALOG = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響 **目錄** 結果集。<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL = 當資料指標是動態資料指標時，SQL_ATTR_MAX_ROWS 語句屬性會影響 **SELECT**、 **INSERT**、 **DELETE**和 **UPDATE** 語句，以及 **目錄** 結果集。<br/>SQL_CA2_CRC_EXACT = 當資料指標是動態資料指標時，SQL_DIAG_CURSOR_ROW_COUNT 診斷欄位中可以使用確切的資料列計數。<br/>SQL_CA2_CRC_APPROXIMATE = 當資料指標是動態資料指標時，[SQL_DIAG_CURSOR_ROW_COUNT 診斷] 欄位中可以使用大約的資料列計數。<br/>SQL_CA2_SIMULATE_NON_UNIQUE = 驅動程式不保證當資料指標是動態資料指標時，模擬定位的 update 或 delete 語句只會影響一個資料列;應用程式必須負責確保這一點。  (如果語句會影響多個資料列， **SQLExecute** 或 **SQLEXECDIRECT** 會傳回 SQLSTATE 01001 [Cursor operation 衝突]。 ) 若要設定此行為，應用程式會呼叫 **SQLSetStmtAttr** ，並將 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 SQL_SC_NON_UNIQUE。<br/>SQL_CA2_SIMULATE_TRY_UNIQUE = 當資料指標為動態資料指標時，驅動程式會嘗試保證模擬定位的 update 或 delete 語句只會影響一個資料列。 驅動程式一律會執行這類語句，即使它們可能會影響一個以上的資料列，例如當沒有唯一索引鍵時。  (如果語句會影響多個資料列， **SQLExecute** 或 **SQLEXECDIRECT** 會傳回 SQLSTATE 01001 [Cursor operation 衝突]。 ) 若要設定此行為，應用程式會呼叫 **SQLSetStmtAttr** ，並將 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 SQL_SC_TRY_UNIQUE。<br/>SQL_CA2_SIMULATE_UNIQUE = 驅動程式保證當資料指標是動態資料指標時，模擬定位的 update 或 delete 語句將只會影響一個資料列。 如果驅動程式無法針對指定的語句保證這一點， **SQLExecDirect** 或 **SQLPREPARE** 會傳回 SQLSTATE 01001 (資料指標作業衝突) 。 若要設定此行為，應用程式會呼叫 **SQLSetStmtAttr** ，並將 SQL_ATTR_SIMULATE_CURSOR 屬性設定為 SQL_SC_UNIQUE。|
|SQL_EXPRESSIONS_IN_ORDERBY|1.0|字元字串：如果資料來源支援 **ORDER BY** 清單中的運算式，則為 "Y";如果不是，則為 "N"。|
|SQL_FILE_USAGE|2.0|SQLUSMALLINT 值，指出單一層驅動程式如何直接處理資料來源中的檔案：<br/>SQL_FILE_NOT_SUPPORTED = 驅動程式不是單一層級的驅動程式。 例如，ORACLE 驅動程式是兩層式的驅動程式。<br/>SQL_FILE_TABLE = 單一層驅動程式會將資料來源中的檔案視為資料表。 例如，Xbase 驅動程式會將每個 Xbase 檔案視為資料表。<br/>SQL_FILE_CATALOG = 單一層驅動程式會將資料來源中的檔案視為目錄。 例如，Microsoft Access 驅動程式會將每個 Microsoft Access 檔案視為完整的資料庫。<br/><br/>應用程式可能會使用這個來判斷使用者將如何選取資料。 例如，Xbase 使用者通常會將資料視為儲存在檔案中，而 ORACLE 和 Microsoft Access 使用者通常會將資料視為儲存在資料表中的資料。<br/><br/>當使用者選取 Xbase 資料來源時，應用程式可能會顯示 [Windows 檔案 **開啟** ] 通用對話方塊;當使用者選取 Microsoft Access 或 ORACLE 資料來源時，應用程式可能會顯示自訂的 [ **選取資料表** ] 對話方塊。|
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援的順向資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA1_NEXT<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在描述) 中替代「動態資料指標」的「順向資料指標」。|
|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援的順向資料指標的屬性。 此位元遮罩包含第二個屬性子集;如需第一個子集，請參閱 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (，並在描述) 中替代「動態資料指標」的「順向資料指標」。|
|SQL_GETDATA_EXTENSIONS|2.0|SQLUINTEGER 位元遮罩，列舉 **SQLGetData**的延伸。<br/><br/>下列位元遮罩會與旗標一起使用，以判斷驅動程式支援 **SQLGetData**的一般擴充功能：<br/>您可以針對任何未系結的資料行呼叫 SQL_GD_ANY_COLUMN = **SQLGetData** ，包括最後一個系結資料行之前的資料行。 請注意，除非也傳回 SQL_GD_ANY_ORDER，否則資料行必須以遞增資料行編號的順序來呼叫。<br/>SQL_GD_ANY_ORDER = **SQLGetData** 可以針對未系結的資料行以任何順序呼叫。 請注意，除非也傳回 SQL_GD_ANY_COLUMN，否則只能針對最後一個系結資料行之後的資料行呼叫 **SQLGetData** 。<br/>您可以針對 (區塊中任何資料列的未系結資料行呼叫 SQL_GD_BLOCK = **SQLGetData** ，其中資料列集大小在使用 **SQLSetPos**定位至該資料列之後，資料列集大小大於 1) 。<br/>除了未系結的資料行之外，也可以針對系結資料行呼叫 SQL_GD_BOUND = **SQLGetData** 。 驅動程式無法傳回此值，除非它也傳回 SQL_GD_ANY_COLUMN。<br/>您可以呼叫 SQL_GD_OUTPUT_PARAMS = **SQLGetData** 來傳回輸出參數值。 如需詳細資訊，請參閱 [使用 SQLGetData 來取出輸出參數](../develop-app/retrieving-output-parameters-using-sqlgetdata.md)。<br/><br/>**SQLGetData** 只需要從上一個系結資料行之後發生的未系結資料行傳回資料，並依遞增資料行編號的順序呼叫，而不是在資料列區塊中的資料列中。<br/><br/>如果驅動程式支援書簽 (固定長度或可變長度的) ，它必須支援在資料行0上呼叫 **SQLGetData** 。 不論驅動程式針對使用 SQL_GETDATA_EXTENSIONS *InfoType*的**SQLGetInfo**呼叫所傳回的內容為何，都需要此支援。|
|SQL_GROUP_BY|2.0|SQLUSMALLINT 值，指定 **GROUP BY** 子句中的資料行與選取清單中的非匯總資料行之間的關聯性：<br/>SQL_GB_COLLATE = 可以在每個群組資料行的結尾指定 **COLLATE** 子句。  (ODBC 3.0) <br/>不支援 SQL_GB_NOT_SUPPORTED = **GROUP BY** 子句。  (ODBC 2.0) <br/>SQL_GB_GROUP_BY_EQUALS_SELECT = **GROUP by** 子句必須包含選取清單中的所有非匯總資料行。 它不能包含任何其他資料行。 例如， **從員工群組依部門選取 [部門]、[最大 (薪資) **。  (ODBC 2.0) <br/>SQL_GB_GROUP_BY_CONTAINS_SELECT = **GROUP by** 子句必須包含選取清單中的所有非匯總資料行。 它可以包含不在選取清單中的資料行。 例如， **從員工群組依部門、年齡 (選取 [部門]、[最大薪資) **。  (ODBC 2.0) <br/>SQL_GB_NO_RELATION = **GROUP by** 子句中的資料行與選取清單之間的資料行無關。 在選取清單中 nongrouped、非匯總資料行的意義與資料來源相依。 例如， **從員工群組依部門、年齡選取部門、薪資**。  (ODBC 2.0) <br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回支援的 SQL_GB_GROUP_BY_EQUALS_SELECT 選項。 符合 SQL 92 的完整等級標準驅動程式一律會傳回支援的 SQL_GB_COLLATE 選項。 如果不支援任何選項，則資料來源不支援 **GROUP by** 子句。|
|SQL_IDENTIFIER_CASE|1.0|SQLUSMALLINT 值如下：<br/>SQL_IC_UPPER = SQL 中的識別碼不區分大小寫，而且會以大寫儲存在系統目錄中。<br/>SQL_IC_LOWER = SQL 中的識別碼不區分大小寫，而且會以小寫儲存在系統目錄中。<br/>SQL_IC_SENSITIVE = SQL 中的識別碼會區分大小寫，且會儲存在系統目錄中的混合式情況下。<br/>SQL_IC_MIXED = SQL 中的識別碼不區分大小寫，且會儲存在系統目錄中的混合式案例中。<br/><br/>因為 SQL-92 中的識別碼永遠不區分大小寫，所以嚴格符合 SQL-92 的驅動程式 (任何層級) 將永遠不會傳回所支援的 SQL_IC_SENSITIVE 選項。|
|SQL_IDENTIFIER_QUOTE_CHAR|1.0|在 SQL 語句中，用來當做引號 (分隔) 識別碼之開頭和結尾分隔符號的字元字串。 以引數形式傳遞給 ODBC 函數的 (識別碼不需要加上引號。 ) 如果資料來源不支援引號識別碼，則會傳回空白。<br/><br/>當連接屬性 SQL_ATTR_METADATA_ID 設定為 SQL_TRUE 時，此字元字串也可以用於引號類別目錄函數引數。<br/><br/>因為 SQL-92 中的識別碼引號字元是雙引號 ( ") ，所以嚴格符合 SQL-92 的驅動程式一律會傳回雙引號字元。|
|SQL_INDEX_KEYWORDS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式所支援之 CREATE INDEX 語句中的關鍵字：<br/>SQL_IK_NONE = 不支援任何關鍵字。<br/>支援 SQL_IK_ASC = ASC 關鍵字。<br/>支援 SQL_IK_DESC = DESC 關鍵字。<br/>SQL_IK_ALL = 支援所有關鍵詞。<br/><br/>為了查看是否支援 CREATE INDEX 語句，應用程式會使用 SQL_DLL_INDEX 資訊類型來呼叫 **SQLGetInfo** 。|
|SQL_INFO_SCHEMA_VIEWS|3.0|SQLUINTEGER 位元遮罩，用來列舉驅動程式所支援之 INFORMATION_SCHEMA 中的 views。 中的 views 和 INFORMATION_SCHEMA 的內容如 SQL-92 中所定義。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩可用來判斷支援的視圖：<br/>SQL_ISV_ASSERTIONS = 識別由指定使用者所擁有的目錄判斷提示。  (完整層級) <br/>SQL_ISV_CHARACTER_SETS = 識別可由指定使用者存取的目錄字元組。  (中繼層級) <br/>SQL_ISV_CHECK_CONSTRAINTS = 識別指定使用者所擁有的檢查條件約束。  (中繼層級) <br/>SQL_ISV_COLLATIONS = 識別可由指定使用者存取之目錄的字元定序。  (完整層級) <br/>SQL_ISV_COLUMN_DOMAIN_USAGE = 識別目錄的資料行，該目錄相依于目錄中定義的網域，且由指定使用者所擁有。  (中繼層級) <br/>SQL_ISV_COLUMN_PRIVILEGES = 識別可供指定使用者使用或授與之持續性資料表資料行的許可權。  (FIPS 過渡層級) <br/>SQL_ISV_COLUMNS = 識別可由指定使用者存取之持續性資料表的資料行。  (FIPS 過渡層級) <br/>SQL_ISV_CONSTRAINT_COLUMN_USAGE = 類似于 CONSTRAINT_TABLE_USAGE 視圖，則會針對指定使用者所擁有的各種條件約束來識別資料行。  (中繼層級) <br/>SQL_ISV_CONSTRAINT_TABLE_USAGE = 識別條件約束所使用的資料表 (參考、唯一和判斷提示) ，且由指定使用者所擁有。  (中繼層級) <br/>SQL_ISV_DOMAIN_CONSTRAINTS = 識別目錄) 中可由指定使用者存取之網域的網域條件約束 (。  (中繼層級) <br/>SQL_ISV_DOMAINS = 識別在目錄中所定義且可由使用者存取的定義域。  (中繼層級) <br/>SQL_ISV_KEY_COLUMN_USAGE = 識別在目錄中定義的資料行，這些資料行會由指定的使用者所限制為索引鍵。  (中繼層級) <br/>SQL_ISV_REFERENTIAL_CONSTRAINTS = 識別指定使用者所擁有的參考條件約束。  (中繼層級) <br/>SQL_ISV_SCHEMATA = 識別指定使用者所擁有的架構。  (中繼層級) <br/>SQL_ISV_SQL_LANGUAGES = 識別 sql 的一致性層級、選項以及 SQL 執行所支援的方言。  (中繼層級) <br/>SQL_ISV_TABLE_CONSTRAINTS = 識別由指定使用者所擁有的資料表條件約束。  (中繼層級) <br/>SQL_ISV_TABLE_PRIVILEGES = 識別可由指定使用者使用或授與之持續性資料表的許可權。  (FIPS 過渡層級) <br/>SQL_ISV_TABLES = 識別可由指定使用者存取的目錄中所定義的持續性資料表。  (FIPS 過渡層級) <br/>SQL_ISV_TRANSLATIONS = 識別可由指定使用者存取之目錄的字元翻譯。  (完整層級) <br/>SQL_ISV_USAGE_PRIVILEGES = 識別類別目錄物件的許可權，這些物件可供指定的使用者使用或擁有。  (FIPS 過渡層級) <br/>SQL_ISV_VIEW_COLUMN_USAGE = 識別指定之使用者所擁有之目錄的視圖相依的資料行。  (中繼層級) <br/>SQL_ISV_VIEW_TABLE_USAGE = 識別指定使用者所擁有之目錄的視圖相依的資料表。  (中繼層級) <br/>SQL_ISV_VIEWS = 識別在此目錄中定義的已查看資料表，可由指定的使用者存取。  (FIPS 過渡層級) |
|SQL_INSERT_STATEMENT|3.0|SQLUINTEGER 位元遮罩，表示支援 **INSERT** 語句：<br/>SQL_IS_INSERT_LITERALS<br/>SQL_IS_INSERT_SEARCHED<br/>SQL_IS_SELECT_INTO<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回所有這些選項。|
|SQL_INTEGRITY|1.0|字元字串：如果資料來源支援完整性增強功能，則為 "Y";如果不是，則為 "N"。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_ODBC_SQL_OPT_IEF 重新命名為 odbc 3.0。|
|SQL_KEYSET_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式所支援之索引鍵集資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_KEYSET_CURSOR_ATTRIBUTES2。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA1_NEXT<br/>SQL_CA1_ABSOLUTE<br/>SQL_CA1_RELATIVE<br/>SQL_CA1_BOOKMARK<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在描述) 中替代「動態資料指標」的「索引鍵集驅動的資料指標」。<br/><br/>因為驅動程式支援透過內嵌 SQL FETCH 語句進行滾動的資料指標，所以 SQL-92 中繼等級一致的驅動程式通常會傳回所支援的 SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項。 不過，因為這不會直接判斷基礎 SQL 支援，所以即使是針對 SQL-92 中繼層級的驅動程式，也可能不支援可滾動的資料指標。|
|SQL_KEYSET_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式所支援之索引鍵集資料指標的屬性。 此位元遮罩包含第二個屬性子集;如需第一個子集，請參閱 SQL_KEYSET_CURSOR_ATTRIBUTES1。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在描述) 中替代「動態資料指標」的「索引鍵集驅動的資料指標」。|
|SQL_KEYWORDS|2.0|字元字串，其中包含所有資料來源特定關鍵字的逗號分隔清單。 這份清單不包含資料來源和 ODBC 所使用之 ODBC 或關鍵字的特定關鍵字。 此清單代表所有保留的關鍵字;互通的應用程式不應在物件名稱中使用這些字組。<br/><br/>如需 ODBC 關鍵字的清單，請參閱[附錄 C： SQL 文法](../appendixes/appendix-c-sql-grammar.md)中的[保留關鍵字](../appendixes/reserved-keywords.md)。 **#Define**值 SQL_ODBC_KEYWORDS 包含以逗號分隔的 ODBC 關鍵字清單。|
|SQL_LIKE_ESCAPE_CLAUSE|2.0|字元字串： "Y" 如果資料來源支援對 **等** 述詞中的百分比字元 (% ) 和底線字元 (_) ，且驅動程式支援 ODBC 語法來定義 **like** 述詞 escape 字元;否則為 "N"。|
|SQL_MAX_ASYNC_CONCURRENT_STATEMENTS|3.0|SQLUINTEGER 值，指定在指定的連接上，驅動程式可支援之使用中並行語句的最大數目。 如果沒有特定限制或限制未知，則此值為零。|
|SQL_MAX_BINARY_LITERAL_LEN|2.0|SQLUINTEGER 值，指定十六進位字元數的最大長度 (數目，不包括 SQL 語句中的二進位常值 **SQLGetTypeInfo**) 所傳回的常值前置詞和尾碼。 例如，二進位常值0xFFAA 的長度為4。 如果沒有最大長度或長度不明，則此值會設定為零。|
|SQL_MAX_CATALOG_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中目錄名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 完整等級的驅動程式將會傳回至少128。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_MAX_QUALIFIER_NAME_LEN 重新命名為 odbc 3.0。|
|SQL_MAX_CHAR_LITERAL_LEN|2.0|SQLUINTEGER 值，指定字元數的最大長度 (，不包括 SQL 語句中字元常值的 **SQLGetTypeInfo**) 所傳回的常值前置詞和尾碼。 如果沒有最大長度或長度不明，則此值會設定為零。|
|SQL_MAX_COLUMN_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中資料行名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回18。 符合 FIPS 中繼等級標準的驅動程式至少會傳回128。|
|SQL_MAX_COLUMNS_IN_GROUP_BY|2.0|SQLUSMALLINT 值，指定 **GROUP BY** 子句中允許的最大資料行數目。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回6。 符合 FIPS 中繼等級標準的驅動程式至少會傳回15個。|
|SQL_MAX_COLUMNS_IN_INDEX|2.0|SQLUSMALLINT 值，指定索引中允許的資料行數目上限。 如果沒有指定的限制或限制未知，此值會設為零。|
|SQL_MAX_COLUMNS_IN_ORDER_BY|2.0|SQLUSMALLINT 值，指定 **ORDER BY** 子句中所允許的最大資料行數目。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回6。 符合 FIPS 中繼等級標準的驅動程式至少會傳回15個。|
|SQL_MAX_COLUMNS_IN_SELECT|2.0|SQLUSMALLINT 值，指定選取清單中允許的資料行數目上限。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回100。 符合 FIPS 中繼等級標準的驅動程式至少會傳回250。|
|SQL_MAX_COLUMNS_IN_TABLE|2.0|SQLUSMALLINT 值，指定資料表中允許的資料行數目上限。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回100。 符合 FIPS 中繼等級標準的驅動程式至少會傳回250。|
|SQL_MAX_CONCURRENT_ACTIVITIES|1.0|SQLUSMALLINT 值，指定驅動程式可支援的連接使用中語句的最大數目。 如果語句的結果暫止，則語句會定義為作用中，而「結果」一詞表示來自 **選取** 作業的資料列，或是受到 **插入**、 **更新**或 **刪除** 作業影響的資料列 (例如資料列計數) 或處於 NEED_DATA 狀態。 此值可反映驅動程式或資料來源所加諸的限制。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_ACTIVE_STATEMENTS 重新命名為 odbc 3.0。|
|SQL_MAX_CURSOR_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中資料指標名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回18。 符合 FIPS 中繼等級標準的驅動程式至少會傳回128。|
|SQL_MAX_DRIVER_CONNECTIONS|1.0|SQLUSMALLINT 值，指定驅動程式可針對環境支援的作用中連接數目上限。 此值可反映驅動程式或資料來源所加諸的限制。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_ACTIVE_CONNECTIONS 重新命名為 odbc 3.0。|
|SQL_MAX_IDENTIFIER_LEN|3.0|SQLUSMALLINT，表示資料來源針對使用者定義名稱所支援的大小上限（以字元為單位）。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回18。 符合 FIPS 中繼等級標準的驅動程式至少會傳回128。|
|SQL_MAX_INDEX_SIZE|2.0|SQLUINTEGER 值，指定索引的結合欄位中允許的最大位元組數目。 如果沒有指定的限制或限制未知，此值會設為零。|
|SQL_MAX_PROCEDURE_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中程式名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。|
|SQL_MAX_ROW_SIZE|2.0|SQLUINTEGER 值，指定資料表中單一資料列的最大長度。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回2000。 符合 FIPS 中繼等級標準的驅動程式至少會傳回8000。|
|SQL_MAX_ROW_SIZE_INCLUDES_LONG|3.0|字元字串：如果針對 SQL_MAX_ROW_SIZE 資訊類型傳回的最大資料列大小包含資料列中所有 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 資料行的長度，則為 "Y";否則為 "N"。|
|SQL_MAX_SCHEMA_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中架構名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回18。 符合 FIPS 中繼等級標準的驅動程式至少會傳回128。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_MAX_OWNER_NAME_LEN 重新命名為 odbc 3.0。|
|SQL_MAX_STATEMENT_LEN|2.0|SQLUINTEGER 值，指定字元數的最大長度 (，包括 SQL 語句的空白字元) 。 如果沒有最大長度或長度不明，則此值會設定為零。|
|SQL_MAX_TABLE_NAME_LEN|1.0|SQLUSMALLINT 值，指定資料來源中資料表名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回18。 符合 FIPS 中繼等級標準的驅動程式至少會傳回128。|
|SQL_MAX_TABLES_IN_SELECT|2.0|SQLUSMALLINT 值，指定**SELECT**語句之**FROM**子句中所允許的最大資料表數目。 如果沒有指定的限制或限制未知，此值會設為零。<br/><br/>符合 FIPS 專案等級的驅動程式至少會傳回15。 符合 FIPS 中繼等級標準的驅動程式至少會傳回50。|
|SQL_MAX_USER_NAME_LEN|2.0|SQLUSMALLINT 值，指定資料來源中使用者名稱的最大長度。 如果沒有最大長度或長度不明，則此值會設定為零。|
|SQL_MULT_RESULT_SETS|1.0|如果資料來源支援多個結果集，則為 "Y" 字元字串：如果不支援，則為 "N"。<br/><br/>如需多個結果集的詳細資訊，請參閱 [多個結果](../develop-app/multiple-results.md)。|
|SQL_MULTIPLE_ACTIVE_TXN|1.0|字元字串：如果驅動程式同時支援一個以上的使用中交易，則為 "Y"，如果每次只能有一個交易處於作用中狀態，則為 "N"。<br/><br/>在分散式交易的情況下，不會套用此資訊類型所傳回的資訊。|
|SQL_NEED_LONG_DATA_LEN|2.0|字元字串： "Y" 如果資料來源需要長資料值的長度 (資料類型是 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定資料類型) 在該值傳送到資料來源之前，如果不是，則為 "N"。 如需詳細資訊，請參閱 [SQLBindParameter 函數](sqlbindparameter-function.md) 和 [SQLSetPos 函數](sqlsetpos-function.md)。|
|SQL_NON_NULLABLE_COLUMNS|1.0|SQLUSMALLINT 值，指定資料來源在資料行中是否支援 NOT Null：<br/>SQL_NNC_Null = 所有資料行必須可為 null。<br/>SQL_NNC_NON_Null = 資料行不可為 null。  (資料來源在**CREATE TABLE**語句中支援**NOT Null**資料行條件約束。 ) <br/><br/>符合 SQL-92 專案層級的驅動程式將會傳回 SQL_NNC_NON_Null。|
|SQL_NULL_COLLATION|2.0|SQLUSMALLINT 值，指定在結果集中排序 Null 的位置：<br/>SQL_NC_END = Null 會在結果集的結尾進行排序，不論 ASC 或 DESC 關鍵字為何。<br/>SQL_NC_HIGH = Null 會根據 ASC 或 DESC 關鍵字，在結果集的高階端進行排序。<br/>SQL_NC_LOW = Null 會在結果集的低端排序，視 ASC 或 DESC 關鍵字而定。<br/>SQL_NC_START = Null 會在結果集的開頭進行排序，不論 ASC 或 DESC 關鍵字為何。|
|SQL_NUMERIC_FUNCTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量數值函數。<br/><br/>下列位元遮罩可用來判斷支援的數值函數：<br/>SQL_FN_NUM_ABS (ODBC 1.0) <br/>SQL_FN_NUM_ACOS (ODBC 1.0) <br/>SQL_FN_NUM_ASIN (ODBC 1.0) <br/>SQL_FN_NUM_ATAN (ODBC 1.0) <br/>SQL_FN_NUM_ATAN2 (ODBC 1.0) <br/>SQL_FN_NUM_CEILING (ODBC 1.0) <br/>SQL_FN_NUM_COS (ODBC 1.0) <br/>SQL_FN_NUM_COT (ODBC 1.0) <br/>SQL_FN_NUM_DEGREES (ODBC 2.0) <br/>SQL_FN_NUM_EXP (ODBC 1.0) <br/>SQL_FN_NUM_FLOOR (ODBC 1.0) <br/>SQL_FN_NUM_LOG (ODBC 1.0) <br/>SQL_FN_NUM_LOG10 (ODBC 2.0) <br/>SQL_FN_NUM_MOD (ODBC 1.0) <br/>SQL_FN_NUM_PI (ODBC 1.0) <br/>SQL_FN_NUM_POWER (ODBC 2.0) <br/>SQL_FN_NUM_RADIANS (ODBC 2.0) <br/>SQL_FN_NUM_RAND (ODBC 1.0) <br/>SQL_FN_NUM_ROUND (ODBC 2.0) <br/>SQL_FN_NUM_SIGN (ODBC 1.0) <br/>SQL_FN_NUM_SIN (ODBC 1.0) <br/>SQL_FN_NUM_SQRT (ODBC 1.0) <br/>SQL_FN_NUM_TAN (ODBC 1.0) <br/>SQL_FN_NUM_TRUNCATE (ODBC 2.0) |
|SQL_ODBC_INTERFACE_CONFORMANCE|3.0|SQLUINTEGER 值，指出驅動程式符合的 ODBC*3.x 介面層級。*<br/><br/>SQL_OIC_CORE：所有 ODBC 驅動程式預期符合的最低層級。 此層級包含基本介面元素，例如連接函數、準備和執行 SQL 語句的函式、基本結果集中繼資料函式、基本目錄函數等等。<br/>SQL_OIC_LEVEL1：包含核心標準合規性層級功能的層級，加上可滾動的資料指標、書簽、定點更新和刪除等等。<br/>SQL_OIC_LEVEL2：層級，包括層級1標準合規性層級功能，以及敏感性資料指標等先進的功能;依書簽更新、刪除及重新整理;預存程式支援;主鍵和外鍵的目錄功能;多目錄支援;依此類推。<br/><br/>如需詳細資訊，請參閱 [介面一致性層級](../develop-app/interface-conformance-levels.md)。|
|SQL_ODBC_VER|1.0|包含驅動程式管理員所符合之 ODBC 版本的字元字串。 版本的格式為 # #. # #. 0000，其中前兩位數是主要版本，而下兩個數字是次要版本。 這只會在驅動程式管理員中執行。|
|SQL_OJ_CAPABILITIES|2.01|SQLUINTEGER 位元遮罩，列舉驅動程式和資料來源所支援的外部聯結類型。 以下是用來判斷支援哪些類型的位元遮罩：<br/>SQL_OJ_LEFT = 支援左方外部聯結。<br/>SQL_OJ_RIGHT = 支援 Right outer join。<br/>SQL_OJ_FULL = 支援完整外部聯結。<br/>SQL_OJ_NESTED = 支援 Nested outer join。<br/>SQL_OJ_NOT_ORDERED = 外部聯結的 ON 子句中的資料行名稱不一定要與其在 **OUTER join** 子句中各自資料表名稱的順序相同。<br/>SQL_OJ_INNER = 內部資料表 (左方外部聯結中的右邊資料表或右外部聯結中的左資料表) 也可以在內部聯結中使用。 這並不適用于沒有內部資料表的完整外部聯結。<br/>SQL_OJ_ALL_COMPARISON_OPS = ON 子句中的比較運算子可以是任何 ODBC 比較運算子。 如果未設定此位，則只可在外部聯結中使用 equals (=) 比較運算子。<br/><br/>如果這些選項都未以支援的方式傳回，則不支援任何外部聯結子句。<br/><br/>如需 SELECT 語句中關聯式聯結運算子支援的詳細資訊（如 SQL-92 所定義），請參閱 SQL_SQL92_RELATIONAL_JOIN_OPERATORS。|
|SQL_ORDER_BY_COLUMNS_IN_SELECT|2.0|字元字串：如果 **ORDER BY** 子句中的資料行必須在選取清單中，則為 "Y";否則為 "N"。|
|SQL_PARAM_ARRAY_ROW_COUNTS|3.0|SQLUINTEGER，列舉驅動程式在參數化執行中資料列計數可用性的相關屬性。 具有下列值：<br/>SQL_PARC_BATCH = 個別的資料列計數適用于每組參數。 這在概念上相當於產生 SQL 語句批次的驅動程式，而該驅動程式會針對陣列中的每個參數設定一個。 您可以使用 SQL_PARAM_STATUS_PTR 描述項欄位來抓取擴充的錯誤資訊。<br/>SQL_PARC_NO_BATCH = 只有一個可用的資料列計數，也就是執行整個參數陣列的語句所產生的累計資料列計數。 這在概念上相當於將語句連同完整的參數陣列視為一個不可部分完成的單位。 錯誤的處理方式與執行一個語句時相同。|
|SQL_PARAM_ARRAY_SELECTS|3.0|SQLUINTEGER，列舉驅動程式在參數化執行中的結果集可用性的相關屬性。 具有下列值：<br/>SQL_PAS_BATCH = 每一組參數都有一個可用的結果集。 這在概念上相當於產生 SQL 語句批次的驅動程式，而該驅動程式會針對陣列中的每個參數設定一個。<br/>SQL_PAS_NO_BATCH = 只有一個可用的結果集，代表針對完整參數陣列執行語句所產生的累計結果集。 這在概念上相當於將語句連同完整的參數陣列視為一個不可部分完成的單位。<br/>SQL_PAS_NO_SELECT = 驅動程式不允許使用參數陣列來執行結果集產生的語句。|
|SQL_POS_OPERATIONS|2.0|SQLINTEGER 位元遮罩，列舉 **SQLSetPos**中的支援作業。<br/><br/>下列位元遮罩會與旗標一起使用，以決定支援哪些選項。<br/>SQL_POS_POSITION (ODBC 2.0) <br/>SQL_POS_REFRESH (ODBC 2.0) <br/>SQL_POS_UPDATE (ODBC 2.0) <br/>SQL_POS_DELETE (ODBC 2.0) <br/>SQL_POS_ADD (ODBC 2.0) |
|SQL_PROCEDURE_TERM|1.0|具有程式之資料來源廠商名稱的字元字串;例如，「資料庫程式」、「預存程式」、「程式」、「封裝」或「預存查詢」。|
|SQL_PROCEDURES|1.0|字元字串：如果資料來源支援程式，且驅動程式支援 ODBC 程序呼叫語法，則為 "Y";否則為 "N"。|
|SQL_QUOTED_IDENTIFIER_CASE|2.0|SQLUSMALLINT 值如下：<br/>SQL_IC_UPPER = SQL 中引號的識別碼不區分大小寫，而且會以大寫儲存在系統目錄中。<br/>SQL_IC_LOWER = SQL 中引號的識別碼不區分大小寫，而且會以小寫儲存在系統目錄中。<br/>SQL_IC_SENSITIVE = SQL 中的引號識別碼會區分大小寫，而且會以混合的大小寫方式儲存在系統目錄中。 在符合 SQL 92 規範的資料庫中 (，引號識別碼一律會區分大小寫。 ) <br/>SQL_IC_MIXED = SQL 中的引號識別碼不區分大小寫，而且會儲存在系統目錄中的混合大小寫。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_IC_SENSITIVE。|
|SQL_ROW_UPDATES|1.0|字元字串： "Y" 如果索引鍵集驅動或混合的資料指標維護所有已提取資料列的資料列版本或值，因此可以偵測自上次提取資料列之後，任何使用者對資料列所做的任何更新。  (這只適用于更新，不會刪除或插入。 ) 當呼叫 **SQLFetchScroll** 時，驅動程式可能會將 SQL_ROW_UPDATED 旗標傳回到資料列狀態陣列。 否則為 "N"。|
|SQL_SCHEMA_TERM|1.0|具有架構之資料來源廠商名稱的字元字串;例如，「擁有者」、「授權識別碼」或「架構」。<br/><br/>字元字串可以用大寫、小寫或混合大小寫方式傳回。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回「架構」。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_OWNER_TERM 重新命名為 odbc 3.0。|
|SQL_SCHEMA_USAGE|2.0|SQLUINTEGER 位元遮罩，列舉可在其中使用架構的語句：<br/>SQL_SU_DML_STATEMENTS = 所有資料操作語言語句中都支援架構： **select**、 **INSERT**、 **UPDATE**、 **DELETE**，以及如果支援的話，請 **選取 update** 和定點更新和刪除語句。<br/>SQL_SU_PROCEDURE_INVOCATION = ODBC 程序呼叫語句中支援的架構。<br/>SQL_SU_TABLE_DEFINITION = 所有資料表定義語句都支援架構： **CREATE TABLE**、 **CREATE VIEW**、 **ALTER Table**、 **drop table**和 **drop VIEW**。<br/>SQL_SU_INDEX_DEFINITION = 所有索引定義語句都支援架構： **CREATE INDEX** 和 **DROP INDEX**。<br/>SQL_SU_PRIVILEGE_DEFINITION = 擁有權限定義語句都支援架構： **GRANT** 和 **REVOKE**。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回支援的 SQL_SU_DML_STATEMENTS、SQL_SU_TABLE_DEFINITION 和 SQL_SU_PRIVILEGE_DEFINITION 選項。<br/><br/>此 *InfoType* 已從 Odbc 2.0 *InfoType* SQL_OWNER_USAGE 重新命名為 odbc 3.0。|
|SQL_SCROLL_OPTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，可列舉可滾動資料指標所支援的捲軸選項。<br/><br/>下列位元遮罩可用來判斷支援的選項：<br/>SQL_SO_FORWARD_ONLY = 資料指標只向前滾動。  (ODBC 1.0) <br/>SQL_SO_STATIC = 結果集中的資料是靜態的。  (ODBC 2.0) <br/>SQL_SO_KEYSET_DRIVEN = 驅動程式會儲存並使用結果集中每個資料列的索引鍵。  (ODBC 1.0) <br/>SQL_SO_DYNAMIC = 驅動程式會保留資料列集中每個資料列的索引鍵， (索引鍵集大小與) 的資料列集大小相同。  (ODBC 1.0) <br/>SQL_SO_MIXED = 驅動程式會保留索引鍵集中每個資料列的索引鍵，而且索引鍵集大小大於資料列集大小。 資料指標是索引鍵集內的索引鍵集，且在索引鍵集外部是動態的。  (ODBC 1.0) <br/><br/>如需可滾動資料指標的詳細資訊，請參閱可 [滾動資料指標](../develop-app/scrollable-cursors.md)。|
|SQL_SEARCH_PATTERN_ESCAPE|1.0|指定驅動程式支援作為 escape 字元的字元字串，可讓您在搜尋模式中使用模式比對元字元 (_) 和百分比符號 (% ) 做為有效的字元。 這個 escape 字元只適用于支援搜尋字串的這些目錄函數引數。 如果這個字串是空的，驅動程式不支援搜尋模式的 escape 字元。<br/><br/>因為這種資訊類型不表示對 **LIKE** 述詞中的 escape 字元具有一般支援，所以 SQL-92 不包含此字元字串的需求。<br/><br/>此 *InfoType* 僅限於目錄函數。 如需在搜尋模式字串中使用 escape 字元的描述，請參閱 [模式值引數](../develop-app/pattern-value-arguments.md)。|
|SQL_SERVER_NAME|1.0|具有實際資料來源特定伺服器名稱的字元字串;在 **SQLConnect**、 **SQLDriverConnect**和 **SQLBrowseConnect**期間使用資料來源名稱時很有用。|
|SQL_SPECIAL_CHARACTERS|2.0|包含所有特殊字元的字元字串 (也就是，a 到 z、A 到 Z、0到9的所有字元，以及可用於識別碼名稱的底線) ，例如資料表名稱、資料行名稱或索引名稱（位於資料來源）。 例如「# $ ^」。 如果識別碼包含一或多個這些字元，則識別碼必須是分隔的識別碼。|
|SQL_SQL_CONFORMANCE|3.0|SQLUINTEGER 值，指出驅動程式支援的 SQL-92 層級：<br/>SQL_SC_SQL92_ENTRY = 符合專案層級的 SQL-92。<br/>SQL_SC_FIPS127_2_TRANSITIONAL = 符合 FIPS 127-2 的過渡等級。<br/>SQL_SC_SQL92_FULL = 完整層級的 SQL-92 相容。<br/>SQL_SC_ SQL92_INTERMEDIATE = 中繼層級 SQL-92 相容。|
|SQL_SQL92_DATETIME_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的 datetime 純量函數，如 SQL-92 中所定義。<br/><br/>下列位元遮罩可用來判斷支援的日期時間函數：<br/>SQL_SDF_CURRENT_DATE<br/>SQL_SDF_CURRENT_TIME<br/>SQL_SDF_CURRENT_TIMESTAMP|
|SQL_SQL92_FOREIGN_KEY_DELETE_RULE|3.0|SQLUINTEGER 位元遮罩，列舉 **DELETE** 語句中的外鍵所支援的規則，如 SQL-92 中所定義。<br/><br/>下列位元遮罩用來判斷資料來源所支援的子句：<br/>SQL_SFKD_CASCADE<br/>SQL_SFKD_NO_ACTION<br/>SQL_SFKD_SET_DEFAULT<br/>SQL_SFKD_SET_Null<br/><br/>符合 FIPS 過渡等級標準的驅動程式一律會傳回所有這些選項的支援。|
|SQL_SQL92_FOREIGN_KEY_UPDATE_RULE|3.0|SQLUINTEGER 位元遮罩，用於列舉 **UPDATE** 語句中的外鍵所支援的規則，如 SQL-92 中所定義。<br/><br/>下列位元遮罩用來判斷資料來源所支援的子句：<br/>SQL_SFKU_CASCADE<br/>SQL_SFKU_NO_ACTION<br/>SQL_SFKU_SET_DEFAULT<br/>SQL_SFKU_SET_Null<br/><br/>符合 SQL-92 的完整等級標準驅動程式一律會傳回所有這些選項的支援。|
|SQL_SQL92_GRANT|3.0|SQLUINTEGER 位元遮罩，列舉 **GRANT** 語句中所支援的子句，如 SQL-92 中所定義。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩用來判斷資料來源所支援的子句：<br/>SQL_SG_DELETE_TABLE (專案層級) <br/>SQL_SG_INSERT_COLUMN (中繼層級) <br/>SQL_SG_INSERT_TABLE (專案層級) <br/>SQL_SG_REFERENCES_TABLE (專案層級) <br/>SQL_SG_REFERENCES_COLUMN (專案層級) <br/>SQL_SG_SELECT_TABLE (專案層級) <br/>SQL_SG_UPDATE_COLUMN (專案層級) <br/>SQL_SG_UPDATE_TABLE (專案層級) <br/>SQL_SG_USAGE_ON_DOMAIN (FIPS 過渡層級) <br/>SQL_SG_USAGE_ON_CHARACTER_SET (FIPS 過渡層級) <br/>SQL_SG_USAGE_ON_COLLATION (FIPS 過渡層級) <br/>SQL_SG_USAGE_ON_TRANSLATION (FIPS 過渡層級) <br/>SQL_SG_WITH_GRANT_OPTION (專案層級) |
|SQL_SQL92_NUMERIC_VALUE_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式所支援的數值純量函數以及相關聯的資料來源（如 SQL-92 中所定義）。<br/><br/>下列位元遮罩可用來判斷支援的數值函數：<br/>SQL_SNVF_BIT_LENGTH<br/>SQL_SNVF_CHAR_LENGTH<br/>SQL_SNVF_CHARACTER_LENGTH<br/>SQL_SNVF_EXTRACT<br/>SQL_SNVF_OCTET_LENGTH<br/>SQL_SNVF_POSITION|
|SQL_SQL92_PREDICATES|3.0|SQLUINTEGER 位元遮罩，列舉 **SELECT** 語句中所支援的述詞，如 SQL-92 中所定義。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩用來判斷資料來源支援的選項：<br/>SQL_SP_BETWEEN (專案層級) <br/>SQL_SP_COMPARISON (專案層級) <br/>SQL_SP_EXISTS (專案層級) <br/>SQL_SP_IN (專案層級) <br/>SQL_SP_ISNOTNull (專案層級) <br/>SQL_SP_ISNull (專案層級) <br/>SQL_SP_LIKE (專案層級) <br/>SQL_SP_MATCH_FULL (完整層級) <br/>SQL_SP_MATCH_PARTIAL (完整層級) <br/>SQL_SP_MATCH_UNIQUE_FULL (完整層級) <br/>SQL_SP_MATCH_UNIQUE_PARTIAL (完整層級) <br/>SQL_SP_OVERLAPS (FIPS 過渡層級) <br/>SQL_SP_QUANTIFIED_COMPARISON (專案層級) <br/>SQL_SP_UNIQUE (專案層級) |
|SQL_SQL92_RELATIONAL_JOIN_OPERATORS|3.0|SQLUINTEGER 位元遮罩，列舉 **SELECT** 語句中所支援的關聯式聯結運算子，如 SQL-92 中所定義。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩用來判斷資料來源支援的選項：<br/>SQL_SRJO_CORRESPONDING_CLAUSE (中繼層級) <br/>SQL_SRJO_CROSS_JOIN (完整層級) <br/>SQL_SRJO_EXCEPT_JOIN (中繼層級) <br/>SQL_SRJO_FULL_OUTER_JOIN (中繼層級) <br/>SQL_SRJO_INNER_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_INTERSECT_JOIN (中繼層級) <br/>SQL_SRJO_LEFT_OUTER_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_NATURAL_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_RIGHT_OUTER_JOIN (FIPS 過渡層級) <br/>SQL_SRJO_UNION_JOIN (完整層級) <br/><br/>SQL_SRJO_INNER_JOIN 指出對 **內部** 聯結語法的支援，而不是內部聯接功能的支援。 **內部聯結**語法的支援是 FIPS 轉換，而內部聯結功能的支援是**進入**。|
|SQL_SQL92_REVOKE|3.0|SQLUINTEGER 位元遮罩，可列舉資料來源所支援的 **REVOKE** 語句所支援的子句，如 SQL-92 中所定義。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩用來判斷資料來源所支援的子句：<br/>SQL_SR_CASCADE (FIPS 過渡層級) <br/>SQL_SR_DELETE_TABLE (專案層級) <br/>SQL_SR_GRANT_OPTION_FOR (中繼層級) <br/>SQL_SR_INSERT_COLUMN (中繼層級) <br/>SQL_SR_INSERT_TABLE (專案層級) <br/>SQL_SR_REFERENCES_COLUMN (專案層級) <br/>SQL_SR_REFERENCES_TABLE (專案層級) <br/>SQL_SR_RESTRICT (FIPS 過渡層級) <br/>SQL_SR_SELECT_TABLE (專案層級) <br/>SQL_SR_UPDATE_COLUMN (專案層級) <br/>SQL_SR_UPDATE_TABLE (專案層級) <br/>SQL_SR_USAGE_ON_DOMAIN (FIPS 過渡層級) <br/>SQL_SR_USAGE_ON_CHARACTER_SET (FIPS 過渡層級) <br/>SQL_SR_USAGE_ON_COLLATION (FIPS 過渡層級) <br/>SQL_SR_USAGE_ON_TRANSLATION (FIPS 過渡層級) |
|SQL_SQL92_ROW_VALUE_CONSTRUCTOR|3.0|SQLUINTEGER 位元遮罩，列舉 **SELECT** 語句中所支援的資料列值函式運算式，如 SQL-92 中所定義。 下列位元遮罩用來判斷資料來源支援的選項：<br/>SQL_SRVC_VALUE_EXPRESSION<br/>SQL_SRVC_Null<br/>SQL_SRVC_DEFAULT<br/>SQL_SRVC_ROW_SUBQUERY|
|SQL_SQL92_STRING_FUNCTIONS|3.0|SQLUINTEGER 位元遮罩，列舉驅動程式所支援的字串純量函數和相關聯的資料來源（如 SQL-92 中所定義）。<br/><br/>下列位元遮罩可用來判斷支援的字串函數：<br/>SQL_SSF_CONVERT<br/>SQL_SSF_LOWERSQL_SSF_UPPER<br/>SQL_SSF_SUBSTRING<br/>SQL_SSF_TRANSLATE<br/>SQL_SSF_TRIM_BOTH<br/>SQL_SSF_TRIM_LEADING<br/>SQL_SSF_TRIM_TRAILING|
|SQL_SQL92_VALUE_EXPRESSIONS|3.0|SQLUINTEGER 位元遮罩，可列舉支援的值運算式，如 SQL-92 中所定義。<br/><br/>必須支援這項功能的 SQL-92 或 FIPS 一致性層級會顯示在每個位元遮罩旁的括弧中。<br/><br/>下列位元遮罩用來判斷資料來源支援的選項：<br/>SQL_SVE_CASE (中繼層級) <br/>SQL_SVE_CAST (FIPS 過渡層級) <br/>SQL_SVE_COALESCE (中繼層級) <br/>SQL_SVE_NullIF (中繼層級) |
|SQL_STANDARD_CLI_CONFORMANCE|3.0|SQLUINTEGER 位元遮罩，可列舉驅動程式符合的 CLI 標準或標準。 下列位元遮罩可用來決定驅動程式符合的層級：<br/>SQL_SCC_XOPEN_CLI_VERSION1：驅動程式符合 Open Group CLI 第1版。<br/>SQL_SCC_ISO92_CLI：驅動程式符合 ISO 92 CLI。|
|SQL_STATIC_CURSOR_ATTRIBUTES1|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援之靜態資料指標的屬性。 此位元遮罩包含屬性的第一個子集;如需第二個子集，請參閱 SQL_STATIC_CURSOR_ATTRIBUTES2。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA1_NEXT<br/>SQL_CA1_ABSOLUTE<br/>SQL_CA1_RELATIVE<br/>SQL_CA1_BOOKMARK<br/>SQL_CA1_LOCK_NO_CHANGE<br/>SQL_CA1_LOCK_EXCLUSIVE<br/>SQL_CA1_LOCK_UNLOCK<br/>SQL_CA1_POS_POSITION<br/>SQL_CA1_POS_UPDATE<br/>SQL_CA1_POS_DELETE<br/>SQL_CA1_POS_REFRESH<br/>SQL_CA1_POSITIONED_UPDATE<br/>SQL_CA1_POSITIONED_DELETE<br/>SQL_CA1_SELECT_FOR_UPDATE<br/>SQL_CA1_BULK_ADD<br/>SQL_CA1_BULK_UPDATE_BY_BOOKMARK<br/>SQL_CA1_BULK_DELETE_BY_BOOKMARK<br/>SQL_CA1_BULK_FETCH_BY_BOOKMARK<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 (，並在 [描述]) 中，以「動態資料指標」取代「靜態資料指標」。<br/><br/>因為驅動程式支援透過內嵌 SQL FETCH 語句進行滾動的資料指標，所以 SQL-92 中繼等級一致的驅動程式通常會傳回所支援的 SQL_CA1_NEXT、SQL_CA1_ABSOLUTE 和 SQL_CA1_RELATIVE 選項。 不過，因為這不會直接判斷基礎 SQL 支援，所以即使是針對 SQL-92 中繼層級的驅動程式，也可能不支援可滾動的資料指標。|
|SQL_STATIC_CURSOR_ATTRIBUTES2|3.0|SQLUINTEGER 位元遮罩，描述驅動程式支援之靜態資料指標的屬性。 此位元遮罩包含第二個屬性子集;如需第一個子集，請參閱 SQL_STATIC_CURSOR_ATTRIBUTES1。<br/><br/>以下是用來判斷支援哪些屬性的位元遮罩：<br/>SQL_CA2_READ_ONLY_CONCURRENCY<br/>SQL_CA2_LOCK_CONCURRENCY<br/>SQL_CA2_OPT_ROWVER_CONCURRENCY<br/>SQL_CA2_OPT_VALUES_CONCURRENCY<br/>SQL_CA2_SENSITIVITY_ADDITIONS<br/>SQL_CA2_SENSITIVITY_DELETIONS<br/>SQL_CA2_SENSITIVITY_UPDATES<br/>SQL_CA2_MAX_ROWS_SELECT<br/>SQL_CA2_MAX_ROWS_INSERT<br/>SQL_CA2_MAX_ROWS_DELETE<br/>SQL_CA2_MAX_ROWS_UPDATE<br/>SQL_CA2_MAX_ROWS_CATALOG<br/>SQL_CA2_MAX_ROWS_AFFECTS_ALL<br/>SQL_CA2_CRC_EXACT<br/>SQL_CA2_CRC_APPROXIMATE<br/>SQL_CA2_SIMULATE_NON_UNIQUE<br/>SQL_CA2_SIMULATE_TRY_UNIQUE<br/>SQL_CA2_SIMULATE_UNIQUE<br/><br/>如需這些位元遮罩的說明，請參閱 SQL_DYNAMIC_CURSOR_ATTRIBUTES2 (，並在 [描述]) 中，以「動態資料指標」取代「靜態資料指標」。|
|SQL_STRING_FUNCTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量字串函數。<br/><br/>下列位元遮罩可用來判斷支援的字串函數：<br/>SQL_FN_STR_ASCII (ODBC 1.0) <br/>SQL_FN_STR_BIT_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_CHAR (ODBC 1.0) <br/>SQL_FN_STR_CHAR_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_CHARACTER_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_CONCAT (ODBC 1.0) <br/>SQL_FN_STR_DIFFERENCE (ODBC 2.0) <br/>SQL_FN_STR_INSERT (ODBC 1.0) <br/>SQL_FN_STR_LCASE (ODBC 1.0) <br/>SQL_FN_STR_LEFT (ODBC 1.0) <br/>SQL_FN_STR_LENGTH (ODBC 1.0) <br/>SQL_FN_STR_LOCATE (ODBC 1.0) <br/>SQL_FN_STR_LTRIM (ODBC 1.0) <br/>SQL_FN_STR_OCTET_LENGTH (ODBC 3.0) <br/>SQL_FN_STR_POSITION (ODBC 3.0) <br/>SQL_FN_STR_REPEAT (ODBC 1.0) <br/>SQL_FN_STR_REPLACE (ODBC 1.0) <br/>SQL_FN_STR_RIGHT (ODBC 1.0) <br/>SQL_FN_STR_RTRIM (ODBC 1.0) <br/>SQL_FN_STR_SOUNDEX (ODBC 2.0) <br/>SQL_FN_STR_SPACE (ODBC 2.0) <br/>SQL_FN_STR_SUBSTRING (ODBC 1.0) <br/>SQL_FN_STR_UCASE (ODBC 1.0) <br/><br/>如果應用程式可以使用*string_exp1*、 *string_exp2*和*Start*引數來呼叫**尋找**純量函數，驅動程式會傳回 SQL_FN_STR_LOCATE 位元遮罩。 如果應用程式只能使用 *string_exp1* 和 *string_exp2* 引數來呼叫尋找純量函數，驅動程式會傳回 SQL_FN_STR_LOCATE_2 位元遮罩。 完全支援 **尋找** 純量函數的驅動程式會傳回兩個位遮罩。<br/><br/> (需詳細資訊，請參閱附錄 E 中的 [字串](../appendixes/string-functions.md) 函式「純量函數」。) |
|SQL_SUBQUERIES|2.0|SQLUINTEGER 位元遮罩，可列舉支援子查詢的述詞：<br/>SQL_SQ_CORRELATED_SUBQUERIES<br/>SQL_SQ_COMPARISON<br/>SQL_SQ_EXISTS<br/>SQL_SQ_INSQL_SQ_QUANTIFIED<br/><br/>SQL_SQ_CORRELATED_SUBQUERIES 位元遮罩表示支援子查詢的所有述詞都支援相互關聯的子查詢。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回位元遮罩，其中所有位都已設定。|
|SQL_SYSTEM_FUNCTIONS|1.0|SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量系統函數。<br/><br/>下列位元遮罩可用來判斷支援的系統函數：<br/>SQL_FN_SYS_DBNAME<br/>SQL_FN_SYS_IFNull<br/>SQL_FN_SYS_USERNAME|
|SQL_TABLE_TERM|1.0|具有資料表之資料來源廠商名稱的字元字串;例如，"table" 或 "file"。<br/><br/>此字元字串可以是大寫、小寫或混合大小寫。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 "table"。|
|SQL_TIMEDATE_ADD_INTERVALS|2.0|SQLUINTEGER 位元遮罩，列舉 TIMESTAMPADD 純量函數的驅動程式和相關聯資料來源所支援的時間戳記間隔。<br/><br/>下列位元遮罩可用來判斷支援的間隔：<br/>SQL_FN_TSI_FRAC_SECOND<br/>SQL_FN_TSI_SECOND<br/>SQL_FN_TSI_MINUTE<br/>SQL_FN_TSI_HOUR<br/>SQL_FN_TSI_DAY<br/>SQL_FN_TSI_WEEK<br/>SQL_FN_TSI_MONTH<br/>SQL_FN_TSI_QUARTER<br/>SQL_FN_TSI_YEAR<br/><br/>符合 FIPS 過渡等級標準的驅動程式一律會傳回位元遮罩，其中所有的位都已設定。|
|SQL_TIMEDATE_DIFF_INTERVALS|2.0|SQLUINTEGER 位元遮罩，列舉 TIMESTAMPDIFF 純量函數的驅動程式和相關聯資料來源所支援的時間戳記間隔。<br/><br/>下列位元遮罩可用來判斷支援的間隔：<br/>SQL_FN_TSI_FRAC_SECOND<br/>SQL_FN_TSI_SECOND<br/>SQL_FN_TSI_MINUTE<br/>SQL_FN_TSI_HOUR<br/>SQL_FN_TSI_DAY<br/>SQL_FN_TSI_WEEK<br/>SQL_FN_TSI_MONTH<br/>SQL_FN_TSI_QUARTER<br/>SQL_FN_TSI_YEAR<br/><br/>符合 FIPS 過渡等級標準的驅動程式一律會傳回位元遮罩，其中所有的位都已設定。|
|SQL_TIMEDATE_FUNCTIONS|1.0|注意：此資訊類型是在 ODBC 1.0 中引進;每個位元遮罩都會標示其引進的版本。<br/><br/>SQLUINTEGER 位元遮罩，列舉驅動程式和相關聯資料來源所支援的純量日期和時間函數。<br/><br/>下列位元遮罩可用來判斷支援的日期和時間函數：<br/>SQL_FN_TD_CURRENT_DATE (ODBC 3.0) <br/>SQL_FN_TD_CURRENT_TIME (ODBC 3.0) <br/>SQL_FN_TD_CURRENT_TIMESTAMP (ODBC 3.0) <br/>SQL_FN_TD_CURDATE (ODBC 1.0) <br/>SQL_FN_TD_CURTIME (ODBC 1.0) <br/>SQL_FN_TD_DAYNAME (ODBC 2.0) <br/>SQL_FN_TD_DAYOFMONTH (ODBC 1.0) <br/>SQL_FN_TD_DAYOFWEEK (ODBC 1.0) <br/>SQL_FN_TD_DAYOFYEAR (ODBC 1.0) <br/>SQL_FN_TD_EXTRACT (ODBC 3.0) <br/>SQL_FN_TD_HOUR (ODBC 1.0) <br/>SQL_FN_TD_MINUTE (ODBC 1.0) <br/>SQL_FN_TD_MONTH (ODBC 1.0) <br/>SQL_FN_TD_MONTHNAME (ODBC 2.0) <br/>SQL_FN_TD_NOW (ODBC 1.0) <br/>SQL_FN_TD_QUARTER (ODBC 1.0) <br/>SQL_FN_TD_SECOND (ODBC 1.0) <br/>SQL_FN_TD_TIMESTAMPADD (ODBC 2.0) <br/>SQL_FN_TD_TIMESTAMPDIFF (ODBC 2.0) <br/>SQL_FN_TD_WEEK (ODBC 1.0) <br/>SQL_FN_TD_YEAR (ODBC 1.0) |
|SQL_TXN_CAPABLE|1.0|注意：此資訊類型是在 ODBC 1.0 中引進;每個傳回值都會標示其引進的版本。<br/><br/>描述驅動程式或資料來源中交易支援的 SQLUSMALLINT 值：<br/>SQL_TC_NONE = 不支援的交易。  (ODBC 1.0) <br/>SQL_TC_DML = 交易只能包含資料操作語言 (DML) 語句 (**SELECT**、 **INSERT**、 **UPDATE**、 **DELETE**) 。 在交易中遇到的資料定義語言 (DDL) 語句會導致錯誤。  (ODBC 1.0) <br/>SQL_TC_DDL_COMMIT = 交易只能包含 DML 語句。 DDL 語句 (**CREATE TABLE**、 **DROP INDEX**等) 在交易中遇到的會導致交易認可。  (ODBC 2.0) <br/>SQL_TC_DDL_IGNORE = 交易只能包含 DML 語句。 在交易中遇到的 DDL 語句會被忽略。  (ODBC 2.0) <br/>SQL_TC_ALL = 交易可依任何順序包含 DDL 語句和 DML 語句。  (ODBC 1.0) <br/><br/> (因為 SQL-92 中必須有交易支援，所以符合 SQL 92 標準的驅動程式 [任何層級] 將永遠不會傳回 SQL_TC_NONE。 ) |
|SQL_TXN_ISOLATION_OPTION|1.0|SQLUINTEGER 位元遮罩，可列舉驅動程式或資料來源中可用的交易隔離等級。<br/><br/>下列位元遮罩會與旗標一起使用，以判斷支援的選項：<br/>SQL_TXN_READ_UNCOMMITTED<br/>SQL_TXN_READ_COMMITTED<br/>SQL_TXN_REPEATABLE_READ<br/>SQL_TXN_SERIALIZABLE<br/><br/>如需這些隔離等級的說明，請參閱 SQL_DEFAULT_TXN_ISOLATION 的描述。<br/><br/>為了設定交易隔離等級，應用程式會呼叫 **SQLSetConnectAttr** 來設定 SQL_ATTR_TXN_ISOLATION 屬性。 如需詳細資訊，請參閱 [SQLSetConnectAttr 函數](sqlsetconnectattr-function.md)。<br/><br/>符合 SQL-92 專案層級的驅動程式一律會傳回 SQL_TXN_SERIALIZABLE，並受到支援。 符合 FIPS 過渡等級標準的驅動程式一律會傳回所有這些選項的支援。|
|SQL_UNION|2.0|列舉 **UNION** 子句支援的 SQLUINTEGER 位元遮罩：<br/>SQL_U_UNION = 資料來源支援 **UNION** 子句。<br/>SQL_U_UNION_ALL = 資料來源支援**UNION**子句中的**ALL**關鍵字。 在此情況下， (**SQLGetInfo** 會傳回 SQL_U_UNION 和 SQL_U_UNION_ALL。 ) <br/><br/>符合 SQL-92 專案層級的驅動程式一律會將這兩個選項都傳回支援。|
|SQL_USER_NAME|1.0|在特定資料庫中使用之名稱的字元字串，可能與登入名稱不同。|
|SQL_XOPEN_CLI_YEAR|3.0|表示發行群組規格發行年份的字元字串，其中 ODBC 驅動程式管理員的版本完全符合。|
  
## <a name="example"></a>範例  

 **SQLGetInfo** 會傳回支援的選項清單，做為 **INFOVALUEPTR*中的 SQLUINTEGER 位元遮罩。 每個選項的位元遮罩都會與旗標一起使用，以判斷是否支援此選項。  
  
 例如，應用程式可以使用下列程式碼來判斷與連接相關聯的驅動程式是否支援子字串純量函數。  
  
 如需使用 **SQLGetInfo**的另一個範例，請參閱 [SQLTables 函數](sqltables-function.md)。  
  
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
  
 判斷驅動程式是否支援函式  
 [SQLGetFunctions 函式](sqlgetfunctions-function.md)  
  
 傳回語句屬性的設定  
 [SQLGetStmtAttr 函式](sqlgetstmtattr-function.md)  
  
 傳回資料來源資料類型的相關資訊  
 [SQLGetTypeInfo 函式](sqlgettypeinfo-function.md)  
  
## <a name="see-also"></a>另請參閱  

 [ODBC API 參考](odbc-api-reference.md)  
 [ODBC 標頭檔](../install/odbc-header-files.md)
