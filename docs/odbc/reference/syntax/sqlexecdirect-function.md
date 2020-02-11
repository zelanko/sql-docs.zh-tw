---
title: SQLExecDirect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLExecDirect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLExecDirect
helpviewer_keywords:
- SQLExecDirect function [ODBC]
ms.assetid: 985fcee1-f204-425c-bdd1-deb0e7d7bbd9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0fa34020478308c1e0d5c5fe112bbeb04920f07e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003117"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 如果語句中有任何參數， **SQLExecDirect**就會使用參數標記變數的目前值來執行 preparable 語句。 **SQLExecDirect**是提交一次執行 SQL 語句的最快方式。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *StatementText*  
 源要執行的 SQL 語句。  
  
 *TextLength*  
 源**StatementText*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_NO_DATA、SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExecDirect**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLExecDirect**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01001|資料指標操作衝突|\**StatementText*包含定位的 update 或 delete 語句，而且未更新或刪除任何資料列或一個以上的資料列。 （如需有關多個資料列更新的詳細資訊，請參閱**SQLSetStmtAttr**中的 SQL_ATTR_SIMULATE_CURSOR*屬性*的描述）。<br /><br /> （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01003|已在 set 函式中排除 Null 值|引數*StatementText*包含 set 函數（例如**AVG**、 **MAX**、 **MIN**等等），但不是**COUNT** set 函式，而在套用函數之前已排除 Null 引數值。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|針對輸入/輸出或輸出參數傳回的字串或二進位資料，導致截斷非空白字元或非 Null 的二進位資料。 如果它是字串值，則會被右截斷。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01006|未撤銷許可權|\**StatementText*包含**REVOKE**語句，而使用者沒有指定的許可權。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01007|未授與許可權|StatementText 是**GRANT**語句，而且無法將指定的許可權授與使用者。 * \* *|  
|01S02|選項值已變更|因為執行中的工作狀況，而指定的語句屬性無效，所以暫時取代了類似的值。 （您可以呼叫**SQLGetStmtAttr**來判斷暫時替代的值是什麼）。替代值對*StatementHandle*有效，直到資料指標關閉為止，此時語句屬性會還原為先前的值。 可以變更的語句屬性包括：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數截斷|針對輸入/輸出或輸出參數傳回的資料已被截斷，因為數值資料類型的小數部分已截斷，或時間、時間戳記或間隔資料類型的時間元件小數部分已截斷。<br /><br /> （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07002|計數位段不正確|在**SQLBindParameter**中指定的參數數目小於\* *StatementText*中所含 SQL 語句中的參數數目。<br /><br /> 呼叫**SQLBindParameter**時， *ParameterValuePtr*設定為 null 指標， *StrLen_or_IndPtr*未設定為 SQL_Null_DATA 或 SQL_DATA_AT_EXEC，而且*InputOutputType*未設定為 SQL_PARAM_OUTPUT，因此**SQLBindParameter**中指定的參數數目大於 **StatementText*中包含之 SQL 語句中的參數數目。|  
|07006|限制的資料類型屬性違規|**SQLBindParameter**中的*ValueType*引數所識別的資料值，無法轉換為**SQLBindParameter**中的*ParameterType*引數所識別的資料類型。<br /><br /> 針對系結為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 的參數傳回的資料值無法轉換成**SQLBindParameter**中的*ValueType*引數所識別的資料類型。<br /><br /> （如果無法轉換一或多個資料列的資料值，但已成功傳回一或多個資料列，則此函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07007|限制的參數值違規|參數類型 SQL_PARAM_INPUT_OUTPUT_STREAM 只會用於傳送和接收部分資料的參數。 此參數類型不允許輸入系結緩衝區。<br /><br /> 當參數類型為 SQL_PARAM_INPUT_OUTPUT，且**SQLBindParameter**中指定的\* *StrLen_or_IndPtr*不等於 SQL_Null_DATA、SQL_DEFAULT_PARAM、SQL_LEN_DATA_AT_EXEC （LEN）或 SQL_DATA_AT_EXEC 時，就會發生這個錯誤。|  
|07S01|使用預設參數無效|參數值（以**SQLBindParameter**設定）為 SQL_DEFAULT_PARAM，而且對應的參數沒有預設值。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|21S01|插入值清單與資料行清單不相符|\**StatementText*包含**INSERT**語句，而要插入的值數目不符合衍生資料表的程度。|  
|21S02|衍生資料表的程度與資料行清單不符|\**StatementText*包含**CREATE VIEW**語句，而不合格的資料行清單（在 sql 語句的資料*行識別碼*引數中為 VIEW 指定的資料行數目）包含的名稱，比 sql 語句之*查詢規格*引數所定義的衍生資料表中的資料行數目還多。|  
|22001|字串資料，右截斷|將字元或二進位值指派給資料行時，就會截斷非空白字元資料或非 null 的二進位資料。|  
|22002|需要指標變數，但未提供|Null 資料已系結至輸出參數，其*StrLen_or_IndPtr*由**SQLBindParameter**設定為 null 指標。|  
|22003|數值超出範圍|**StatementText*包含 SQL 語句，其中包含系結的數值參數或常值，而當指派給相關聯的資料表資料行時，該值會導致整個（而不是小數）部分的數值被截斷。<br /><br /> 傳回一個或多個輸入/輸出或輸出參數的數值（例如數值或字串），會造成截斷的整個數位部分（相對於小數）。|  
|22007|不正確日期時間格式|**StatementText*包含包含日期、時間或時間戳記結構做為系結參數的 SQL 語句，而參數分別為不正確日期、時間或時間戳記。<br /><br /> 輸入/輸出或輸出參數已系結至日期、時間或時間戳記 C 結構，而傳回參數中的值分別為不正確日期、時間或時間戳記。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22008|Datetime 欄位溢位|**StatementText*包含 SQL 語句，其中包含的 datetime 運算式會在計算時產生不正確日期、時間或時間戳記結構。<br /><br /> 針對輸入/輸出或輸出參數計算的 datetime 運算式產生的日期、時間或時間戳記 C 結構無效。|  
|22012|除數為零|**StatementText*包含 SQL 語句，其中包含導致零除的算術運算式。<br /><br /> 針對輸入/輸出或輸出參數計算的算術運算式，導致零除。|  
|22015|間隔欄位溢位|StatementText 包含精確的數值或間隔參數，轉換成間隔 SQL 資料類型時，會導致有效位數遺失。 * \* *<br /><br /> StatementText 包含一個間隔參數，其中含有一個以上的欄位，當轉換成資料行中的數值資料類型時，不會有數值資料類型的標記法。 * \* *<br /><br /> StatementText 包含指派給間隔 sql 類型的參數資料，而且間隔 sql 類型中不會有 C 類型值的標記法。 * \* *<br /><br /> 指派輸入/輸出或輸出參數，其為間隔 C 類型的精確數值或間隔 SQL 類型會造成有效位數遺失。<br /><br /> 將輸入/輸出或輸出參數指派給 interval C 結構時，不會在間隔資料結構中呈現資料。|  
|22018|轉換規格的字元值無效|StatementText 包含屬於精確或近似數值、日期時間或間隔資料類型的 C 類型; * \* *資料行的 SQL 類型是字元資料類型;而資料行中的值不是系結 C 類型的有效常值。<br /><br /> 傳回輸入/輸出或輸出參數時，SQL 類型為精確或近似數值、日期時間或間隔資料類型;C 類型已 SQL_C_CHAR;而資料行中的值不是系結 SQL 類型的有效常值。|  
|22019|不正確換用字元|\**StatementText*包含包含**LIKE**述詞的 SQL 語句，**其中 WHERE**子句中具有**escape** ，而**escape**後面的逸出字元長度不等於1。|  
|22025|不正確轉義順序|\**StatementText*包含的 SQL 語句在**WHERE**子句中包含「**LIKE** _模式值_ **escape** _escape 字元_」，而模式值中的逸出字元後面的字元不是 "%" 或 "_" 其中之一。|  
|23000|完整性條件約束違規|**StatementText*包含包含參數或常值的 SQL 語句。 在相關聯資料表資料行中定義為 NOT Null 的資料行，參數值為 Null，針對限制只包含唯一值的資料行提供了重複的值，或違反了一些其他的完整性條件約束。|  
|24000|指標狀態無效|資料指標位於*StatementHandle* by **SQLFetch**或**SQLFetchScroll**。 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 資料指標已開啟，但未位於*StatementHandle*上。<br /><br /> **StatementText*包含定位的 update 或 delete 語句，且資料指標位於結果集開頭之前或結果集結尾的後面。|  
|34000|指標名稱無效|**StatementText*包含定位的 update 或 delete 語句，而正在執行的語句所參考的資料指標並未開啟。|  
|3D000|不正確目錄名稱|*StatementText*中指定的目錄名稱無效。|  
|3F000|不正確架構名稱|*StatementText*中指定的架構名稱無效。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死，所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|\**StatementText*包含未 preparable 或包含語法錯誤的 SQL 語句。<br /><br /> 使用者沒有許可權可執行 **StatementText*中包含的 SQL 語句。|  
|42S01|基表或視圖已經存在|\**StatementText*包含**CREATE TABLE**或**CREATE VIEW**語句，而且指定的資料表名稱或視圖名稱已經存在。|  
|42S02|找不到基表或視圖|\**StatementText*包含**Drop TABLE**或**drop VIEW**語句，而且指定的資料表名稱或視圖名稱不存在。<br /><br /> \**StatementText*包含**ALTER table**語句，但指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**CREATE VIEW**語句，且查詢規格所定義的資料表名稱或視圖名稱不存在。<br /><br /> \**StatementText*包含**CREATE INDEX**語句，且指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**GRANT**或**REVOKE**語句，而且指定的資料表名稱或視圖名稱不存在。<br /><br /> \**StatementText*包含**SELECT**語句，但指定的資料表名稱或視圖名稱不存在。<br /><br /> \**StatementText*包含**DELETE**、 **INSERT**或**UPDATE**語句，但指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**語句，而且在條件約束中指定的資料表（參考非所建立的資料表）不存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**語句，但指定的資料表名稱或視圖名稱不存在。|  
|42S11|索引已存在|\**StatementText*包含**CREATE index**語句，且指定的索引名稱已存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**語句，且指定的索引名稱已存在。|  
|42S12|找不到索引|\**StatementText*包含**DROP INDEX**語句，且指定的索引名稱不存在。|  
|42S21|資料行已經存在|\**StatementText*包含**ALTER TABLE**語句，而且**ADD**子句中指定的資料行不是唯一的，或者會識別基表中的現有資料行。|  
|42S22|找不到資料行|\**StatementText*包含**CREATE INDEX**語句，且資料行清單中所指定的一或多個資料行名稱不存在。<br /><br /> \**StatementText*包含**GRANT**或**REVOKE**語句，而且指定的資料行名稱不存在。<br /><br /> \**StatementText*包含**SELECT**、 **DELETE**、 **INSERT**或**UPDATE**語句，但指定的資料行名稱不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**語句，而且在條件約束中指定的資料行（參考非所建立的資料表）不存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**語句，但指定的資料行名稱不存在。|  
|44000|WITH CHECK OPTION 違規|引數*StatementText*包含在已查看的資料表上執行的**INSERT**語句，或是從透過指定**WITH CHECK 選項**所建立之已查看資料表的衍生資料表，如此一來，由**INSERT**語句所影響的一個或多個資料列將不會再出現在已查看的資料表中。<br /><br /> 引數*StatementText*包含在已查看的資料表上執行的**UPDATE**語句，或衍生自透過指定**WITH CHECK 選項**所建立之已查看資料表的資料表，如此一來，由**UPDATE**語句所影響的一個或多個資料列將不會再出現在已查看的資料表中。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已呼叫函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|（DM） **StatementText*是 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLExecDirect**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）引數*TextLength*小於或等於0，但不等於 SQL_NTS。<br /><br /> 使用**SQLBindParameter**設定的參數值為 null 指標，且參數長度值不是0、SQL_Null_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM 或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 使用**SQLBindParameter**設定的參數值不是 null 指標;C 資料類型已 SQL_C_BINARY 或 SQL_C_CHAR;參數長度值小於0，但不 SQL_NTS、SQL_Null_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM 或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> **SQLBindParameter**所系結的參數長度值已設定為 SQL_DATA_AT_EXEC;SQL 類型是 SQL_LONGVARCHAR、SQL_LONGVARBINARY，或是長資料來源特定的資料類型;而**SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型是 "Y"。|  
|HY105|不正確參數類型|為**SQLBindParameter**中的引數*InputOutputType*指定的值是 SQL_PARAM_OUTPUT，而參數是輸入參數。|  
|HY109|不正確資料指標位置|\**StatementText*包含定位的 update 或 delete 語句，而資料指標在已刪除或無法提取的資料列上，其位置為（by **SQLSetPos**或**SQLFetchScroll**）。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|在資料來源傳回結果集之前，查詢超時時間已過期。 超時期間是透過**SQLSetStmtAttr**設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 應用程式會呼叫**SQLExecDirect** ，將 SQL 語句傳送至資料來源。 如需直接執行的詳細資訊，請參閱[直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)。 驅動程式會修改語句，以使用資料來源所使用的 SQL 形式，然後將它提交至資料來源。 特別是，驅動程式會修改用來定義 SQL 中特定功能的 escape 序列。 如需逸出序列的語法，請參閱[ODBC 中的 Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。  
  
 應用程式可以在 SQL 語句中包含一個或多個參數標記。 為了包含參數標記，應用程式會將問號（？）內嵌在適當位置的 SQL 語句中。 如需參數的詳細資訊，請參閱[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 如果 SQL 語句是**SELECT**語句，而且如果應用程式呼叫**SQLSetCursorName**來關聯資料指標與語句，則驅動程式會使用指定的資料指標。 否則，驅動程式會產生資料指標名稱。  
  
 如果資料來源處於手動認可模式（需要明確的交易起始），而且尚未起始交易，則驅動程式會在傳送 SQL 語句之前起始交易。 如需詳細資訊，請參閱[手動認可模式](../../../odbc/reference/develop-app/manual-commit-mode.md)。  
  
 如果應用程式使用**SQLExecDirect**來提交**COMMIT**或**ROLLBACK**語句，則 DBMS 產品之間將無法互通。 若要認可或回復交易，應用程式會呼叫**SQLEndTran**。  
  
 如果**SQLExecDirect**遇到資料執行中參數，它會傳回 SQL_NEED_DATA。 應用程式會使用**SQLParamData**和**SQLPutData**來傳送資料。 請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)、 [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)、 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)和傳送[長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 如果**SQLExecDirect**執行的搜尋 update、insert 或 delete 語句不會影響資料來源中的任何資料列，則對**SQLExecDirect**的呼叫會傳回 SQL_NO_DATA。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 語句屬性的值大於1，而且 SQL 語句包含至少一個參數標記，則**SQLExecDirect**會針對**SQLBindParameter**的呼叫中*ParameterValuePointer*引數所指向的陣列，執行一次 sql 語句。 如需詳細資訊，請參閱[參數值的陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 如果書簽已開啟，而且執行的查詢無法支援書簽，則驅動程式應該嘗試藉由變更屬性值並傳回 SQLSTATE 01S02 （已變更的選項值），將環境強制轉型為支援書簽的一個。 如果無法變更屬性，驅動程式應該會傳回 SQLSTATE HY024 （不正確屬性值）。  
  
> [!NOTE]  
>  使用連接共用時，應用程式不能執行變更資料庫或資料庫內容的 SQL 語句，例如 SQL Server 中的**USE** _database_語句，這會變更資料來源所使用的目錄。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLGETDATA](../../../odbc/reference/syntax/sqlgetdata-function.md)和[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行認可或復原作業|[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料指標名稱|[SQLGetCursorName 函數](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|正在提取部分或所有資料行|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回用來傳送資料的下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|準備語句以執行|[SQLPrepare 函數](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|在執行時間傳送參數資料|[SQLPutData 函數](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函數](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
