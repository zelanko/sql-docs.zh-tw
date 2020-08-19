---
description: SQLColumns 函數
title: SQLColumns 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5fc96b275badf5eab68f78e863648c3a73eaab6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448771"
---
# <a name="sqlcolumns-function"></a>SQLColumns 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：開啟群組  
  
 **總結**  
 **SQLColumns** 會傳回指定資料表中的資料行名稱清單。 驅動程式會在指定的 *StatementHandle*上以結果集的形式傳回此資訊。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *CatalogName*  
 輸出目錄名稱。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 指出這些資料表沒有目錄。 *CatalogName* 不能包含字串搜尋模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *CatalogName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *CatalogName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。 如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 輸出**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 輸出架構名稱的字串搜尋模式。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 指出這些資料表沒有架構。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *SchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *SchemaName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength2*  
 輸出**SchemaName*的長度（以字元為單位）。  
  
 *名*  
 輸出資料表名稱的字串搜尋模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *TableName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *TableName* 是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength3*  
 輸出**TableName*的長度（以字元為單位）。  
  
 *ColumnName*  
 輸出資料行名稱的字串搜尋模式。  
  
> [!NOTE]  
>  如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE，則會將 *ColumnName* 視為識別碼，且其大小寫並不重要。 如果 SQL_FALSE， *ColumnName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength4*  
 輸出**ColumnName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColumns**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLColumns** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在 *StatementHandle*上開啟了資料指標，且已呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 如果 **SQLFetch** 或 **SQLFetchScroll** 尚未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果 **SQLFetch** 或 **SQLFetchScroll** 已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 在 *StatementHandle* 上開啟了資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。|  
|40001|序列化失敗|交易已復原，因為另一個交易發生資源鎖死。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在 *StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效|SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE、 *CatalogName* 引數為 null 指標，且 SQL_CATALOG_NAME *InfoType* 會傳回支援的目錄名稱。<br /><br />  (DM) SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，且 *SchemaName*、 *TableName*或 *ColumnName* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLColumns** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。|  
|||其中一個名稱長度引數的值超過對應目錄或名稱的最大長度值。 藉由呼叫 **SQLGetInfo** 和 *InfoType* 值，即可取得每個目錄或名稱的最大長度。  (請參閱「批註」。) |  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|指定了目錄名稱，而驅動程式或資料來源不支援目錄。<br /><br /> 指定了架構名稱，而驅動程式或資料來源不支援架構。<br /><br /> 為架構名稱、資料表名稱或資料行名稱指定了字串搜尋模式，且資料來源不支援一或多個這些引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而且 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回結果集之前過期。 Timeout 期限是透過 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 此函數通常會在語句執行之前使用，以從資料來源的目錄中取得資料表或資料表的資料行相關資訊。 **SQLColumns** 可用於取出 **SQLTables**所傳回之所有類型專案的資料。 除了基表之外，這可能包含 (但不限於) 的視圖、同義字、系統資料表等等。 相反地， **SQLColAttribute** 和 **SQLDescribeCol** 函數會描述結果集中的資料行，而函數 **SQLNumResultCols** 會傳回結果集中的資料行數目。 如需詳細資訊，請參閱 [目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱 [目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLColumns** 會以 TABLE_CAT、TABLE_SCHEM、TABLE_NAME 和 ORDINAL_POSITION 排序的標準結果集傳回結果。  
  
> [!NOTE]  
>  當應用程式與 ODBC 2 搭配使用時。*x* 驅動程式，不會在結果集中傳回任何 ORDINAL_POSITION 資料行。 因此，在使用 ODBC 2 時。*x* 驅動程式， **SQLColumns** 所傳回之資料行清單中的資料行順序，不一定會與應用程式對該資料表中的所有資料行執行 SELECT 語句時所傳回的資料行順序相同。  
  
> [!NOTE]  
>  **SQLColumns** 可能不會傳回所有資料行。 例如，驅動程式可能不會傳回虛擬資料行的相關資訊，例如 Oracle ROWID。 應用程式可以使用任何有效的資料行，不論是否由 **SQLColumns**傳回。  
>   
>  **SQLColumns**不會傳回**SQLStatistics**可傳回的部分資料行。 例如， **SQLColumns** 不會傳回透過運算式或篩選建立之索引中的資料行，例如薪資 + 權益或部門 = 0012。  
  
 VARCHAR 資料行的長度不會顯示在資料表中;實際的長度取決於資料來源。 若要判斷 TABLE_CAT、TABLE_SCHEM、TABLE_NAME 和 COLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫 **SQLGetInfo** 。  
  
 下列資料行已經重新命名為 ODBC 3。*x*。 資料行名稱的變更不會影響回溯相容性，因為應用程式會依資料行編號進行系結。  
  
|ODBC 2.0 資料行|ODBC 3。*x* 資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 下列資料行已加入至 **SQLColumns** for ODBC 3 所傳回的結果集。*x*：  

:::row:::
    :::column:::
        CHAR_OCTET_LENGTH  
        COLUMN_DEF  
    :::column-end:::
    :::column:::
        IS_NULLABLE  
        ORDINAL_POSITION  
    :::column-end:::
    :::column:::
        SQL_DATA_TYPE  
        SQL_DATETIME_SUB  
    :::column-end:::
:::row-end:::

 下表列出結果集中的資料行。 資料行18以外的其他資料行 (IS_NullABLE) 可以由驅動程式定義。 應用程式應該從結果集的結尾算下，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱 [目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行<br /><br /> number|資料類型|註解|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0) |1|Varchar|目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄，例如當驅動程式從不同 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串 ( "" ) 。|  
|TABLE_SCHEM (ODBC 1.0) |2|Varchar|架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則會針對沒有架構的資料表傳回空字串 ( "" ) 。|  
|TABLE_NAME (ODBC 1.0) |3|Varchar not Null|資料表名稱。|  
|COLUMN_NAME (ODBC 1.0) |4|Varchar not Null|資料行名稱。 驅動程式會針對沒有名稱的資料行傳回空字串。|  
|DATA_TYPE (ODBC 1.0) |5|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式特定的 SQL 資料類型。 若為 datetime 和 interval 資料類型，這個資料行會傳回精確的資料類型 (例如 SQL_TYPE_DATE 或 SQL_INTERVAL_YEAR_TO_MONTH，而不是 SQL_DATETIME 或 SQL_INTERVAL) 等 nonconcise 資料類型。 如需有效 ODBC SQL 資料類型的清單，請參閱附錄 D：資料類型中的 [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md) 。 如需有關驅動程式特定的 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。<br /><br /> 針對 ODBC 3 傳回的資料類型。*x* 和 ODBC 2。*x* 應用程式可能會不同。 如需詳細資訊，請參閱回溯 [相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|TYPE_NAME (ODBC 1.0) |6|Varchar not Null|與資料來源相關的資料類型名稱;例如，「CHAR」、「VARCHAR」、「MONEY」、「LONG VARBINAR」或「CHAR ( ) FOR BIT DATA」。|  
|COLUMN_SIZE (ODBC 1.0) |7|整數|如果 DATA_TYPE SQL_CHAR 或 SQL_VARCHAR，則此資料行包含資料行的最大長度（以字元為單位）。 若為 datetime 資料類型，這是在轉換成字元時顯示值所需的字元總數。 若為數值資料類型，則根據 NUM_PREC_RADIX 資料行，這是資料行中允許的總位數或總位數。 針對 interval 資料類型，這是間隔常值的字元標記法中的字元數 (如間隔前置精確度的定義，請參閱附錄 D：資料類型) 的 [間隔資料類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md) 。 如需詳細資訊，請參閱附錄 D：資料類型中的資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 。|  
|BUFFER_LENGTH (ODBC 1.0) |8|整數|如果指定 SQL_C_DEFAULT，則為 SQLGetData、SQLFetch 或 SQLFetchScroll 作業傳送的資料長度（以位元組為單位）。 若為數值資料，此大小可能與儲存在資料來源上的資料大小不同。 此值可能與字元資料的 COLUMN_SIZE 資料行不同。 如需長度的詳細資訊，請參閱附錄 D：資料類型中的資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 。|  
|DECIMAL_DIGITS (ODBC 1.0) |9|Smallint|小數點右邊的有效位數總數。 針對 SQL_TYPE_TIME 和 SQL_TYPE_TIMESTAMP，此資料行包含小數秒陣列件中的位數。 對於其他資料類型，這是資料來源上的資料行的小數位數。 如果是包含時間元件的間隔資料類型，這個資料行會包含小數點右邊的位數， (小數秒數) 。 如果是不包含時間元件的間隔資料類型，這個資料行就是0。 如需小數位數的詳細資訊，請參閱附錄 D：資料類型中的資料 [行大小、十進位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 。 如果 DECIMAL_DIGITS 不適用的資料類型，則會傳回 Null。|  
|NUM_PREC_RADIX (ODBC 1.0) |10|Smallint|若為數值資料類型，可以是10或2。 如果是10，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值會提供資料行允許的小數位數。 例如，DECIMAL (12，5) 的資料行會傳回 NUM_PREC_RADIX 10、COLUMN_SIZE 12 以及5的 DECIMAL_DIGITS;FLOAT 資料行可能會傳回10的 NUM_PREC_RADIX、COLUMN_SIZE 為15，以及 Null DECIMAL_DIGITS。<br /><br /> 如果是2，COLUMN_SIZE 和 DECIMAL_DIGITS 中的值會提供資料行中允許的位數。 例如，FLOAT 資料行可能會傳回2的基數、53的 COLUMN_SIZE，以及 Null 的 DECIMAL_DIGITS。<br /><br /> 如果 NUM_PREC_RADIX 不適用的資料類型，則會傳回 Null。|  
|可為 Null (ODBC 1.0) |11|Smallint 非 NULL|如果資料行不能包含 Null 值，則為 SQL_NO_NullS。<br /><br /> 如果資料行接受 Null 值，則為 SQL_NullABLE。<br /><br /> SQL_NullABLE_UNKNOWN 如果不知道資料行是否接受 Null 值，則為。<br /><br /> 針對這個資料行所傳回的值與 IS_NullABLE 資料行所傳回的值不同。 可為 Null 的資料行表示資料行可接受 Null，但無法表示資料行不接受 Null 的確定性。 IS_NullABLE 資料行指出資料行不能接受 Null，但無法表示資料行接受 Null 的確定性。|  
| (ODBC 1.0) 的備註|12|Varchar|資料行的描述。|  
|COLUMN_DEF (ODBC 3.0) |13|Varchar|資料行的預設值。 如果此資料行中的值是以引號括住，則應該將其解釋為字串。<br /><br /> 如果指定 Null 做為預設值，此資料行就是 Null 這個字，而不是以引號括住。 如果無法在不截斷的情況下表示預設值，此資料行會包含截斷的，而不包含單引號。 如果未指定任何預設值，則這個資料行是 Null。<br /><br /> COLUMN_DEF 的值可以用來產生新的資料行定義，除非它包含截斷的值。|  
|SQL_DATA_TYPE (ODBC 3.0) |14|Smallint 非 NULL|SQL 資料類型，出現在 IRD 的 SQL_DESC_TYPE 記錄] 欄位中。 這可以是 ODBC SQL 資料類型或驅動程式特定的 SQL 資料類型。 除了 datetime 和 interval 資料類型以外，這個資料行與 DATA_TYPE 資料行相同。 這個資料行會傳回 nonconcise 資料類型 (例如 SQL_DATETIME 或 SQL_INTERVAL) ，而不是 DATETIME 和 INTERVAL 資料類型的精確資料類型 (例如 SQL_TYPE_DATE 或 SQL_INTERVAL_YEAR_TO_MONTH) 。 如果這個資料行傳回 SQL_DATETIME 或 SQL_INTERVAL，就可以從 SQL_DATETIME_SUB 資料行判斷特定的資料類型。 如需有效 ODBC SQL 資料類型的清單，請參閱附錄 D：資料類型中的 [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md) 。 如需有關驅動程式特定的 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。<br /><br /> 針對 ODBC 3 傳回的資料類型。*x* 和 ODBC 2。*x* 應用程式可能會不同。 如需詳細資訊，請參閱回溯 [相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|SQL_DATETIME_SUB (ODBC 3.0) |15|Smallint|Datetime 和 interval 資料類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。 如需 datetime 和 interval 子代碼的詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「SQL_DESC_DATETIME_INTERVAL_CODE」。|  
|CHAR_OCTET_LENGTH (ODBC 3.0) |16|整數|字元或二進位資料類型資料行的最大長度（以位元組為單位）。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|ORDINAL_POSITION (ODBC 3.0) |17|整數不是 NULL|資料行在資料表中的序數位置。 資料表中的第一個資料行是數位1。|  
|IS_NullABLE (ODBC 3.0) |18|Varchar|如果資料行不包含 Null，則為 "NO"。<br /><br /> 如果資料行可以包含 Null，則為 "YES"。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> 針對這個資料行所傳回的值與可為 Null 資料行傳回的值不同。  (查看可為 Null 資料行的描述。 ) |  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會宣告 **SQLColumns**所傳回之結果集的緩衝區。 它會呼叫 **SQLColumns** ，以傳回描述 EMPLOYEE 資料表中每個資料行的結果集。 然後，它會呼叫 **SQLBindCol** ，將結果集中的資料行系結至緩衝區。 最後，應用程式會使用 **SQLFetch** 提取每個資料列，並進行處理。  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料行或資料行的許可權|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回可唯一識別資料列或由交易自動更新之資料行的資料行|[SQLSpecialColumns 函式](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|傳回資料表統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回資料來源中的資料表清單|[SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)|  
|傳回資料表或資料表的許可權|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
