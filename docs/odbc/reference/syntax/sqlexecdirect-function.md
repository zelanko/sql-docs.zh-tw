---
title: "SQLExecDirect 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fdf6183eda2b66263a8ff27664d046640b94ea95
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLExecDirect**執行可準備陳述式，使用參數標記變數的目前值，如果陳述式中存在的任何參數。 **SQLExecDirect**是最快速的方式提交一次執行的 SQL 陳述式。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *StatementText*  
 [輸入]要執行的 SQL 陳述式。  
  
 *TextLength*  
 [輸入]長度 **StatementText*以字元為單位。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_NO_DATA、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExecDirect**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_STMT 的和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLExecDirect** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01001|資料指標作業衝突|\**StatementText*自主定位的 update 或 delete 陳述式，和任何資料列或多個資料列已更新或刪除。 (如需更新多個資料列的詳細資訊，請參閱 SQL_ATTR_SIMULATE_CURSOR 描述*屬性*中**SQLSetStmtAttr**。)<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01003|集函數刪除了 NULL 值|引數*StatementText*包含 set 函式 (例如**AVG**， **MAX**， **MIN**等等)，但不是**計數**設定函式，並且在套用函數之前，也消除了值的 NULL 引數。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|傳回輸入/輸出的字串或二進位資料或輸出參數會導致非空白的字元或二進位資料為非 NULL 的截斷。 如果是字串值，它就是向右截斷。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01006|不會撤銷權限|\**StatementText*包含**撤銷**陳述式，而且使用者沒有指定的權限。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01007|未授與的權限|*\*StatementText*已**GRANT**陳述式，且使用者無法授權指定的權限。|  
|01S02 的警告|選項值已變更|指定的陳述式屬性不實作工作狀況，造成無效的因此暫時取代相似的值。 (**SQLGetStmtAttr**可以呼叫以決定哪些暫時替代的值。)取代值無效， *StatementHandle*直到資料指標已關閉，此時陳述式屬性會還原為先前的值。 陳述式屬性可以變更為：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數位數截斷|傳回輸入/輸出的資料，或輸出參數已被截斷，使得數值資料類型的小數部分遭截斷或時間元件的時間、 時間戳記或時間間隔的資料類型的小數部分已被截斷。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07002|計數不正確的欄位|中指定的參數數目**SQLBindParameter**的 SQL 陳述式中所包含的參數數目少於\* *StatementText*。<br /><br /> **SQLBindParameter**呼叫*ParameterValuePtr*設為 null 指標， *StrLen_or_IndPtr*未設定為 SQL_NULL_DATA 或 SQL_DATA_AT_EXEC，和*了*未設定為 SQL_PARAM_OUTPUT，以便在指定的參數數目**SQLBindParameter**大於包含在 SQL 陳述式中的參數數目 **StatementText*。|  
|07006|受限制的資料類型屬性違規|所識別的資料值*ValueType*引數中的**SQLBindParameter**繫結的參數無法轉換成資料類型所識別的*ParameterType*引數中的**SQLBindParameter**。<br /><br /> 針對繫結為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 無法轉換成資料類型所識別的參數傳回的資料值*ValueType*引數中的**SQLBindParameter**。<br /><br /> （如果無法轉換一或多個資料列的資料值，但一個或多個資料列已成功地傳回，此函數會傳回 SQL_SUCCESS_WITH_INFO。）|  
|07007|Restricted 的參數值違規|參數型別 SQL_PARAM_INPUT_OUTPUT_STREAM 只用於傳送和接收資料，在組件中的參數。 此參數類型不允許輸入繫結的緩衝區。<br /><br /> 參數型別 SQL_PARAM_INPUT_OUTPUT，而且時，會發生這個錯誤\* *StrLen_or_IndPtr*中所指定**SQLBindParameter**不等於 SQL_NULL_DATA，SQL_DEFAULT_PARAM、 SQL_LEN_DATA_AT_EXEC(len) 或 SQL_DATA_AT_EXEC。|  
|07S01|無效的預設參數使用|參數值時，設定與**SQLBindParameter**、 已 SQL_DEFAULT_PARAM，和對應的參數沒有預設值。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|21S01|插入值清單與資料行清單不符|\**StatementText*包含**插入**陳述式，以及要插入值的數目不符合衍生資料表的程度。|  
|21S02|衍生資料表的程度與資料行清單不符|\**StatementText*包含**CREATE VIEW**陳述式，並不合格的資料行清單 (指定的檢視中的資料行數目*資料行識別碼*SQL 引數陳述式） 會包含更多個名稱中所定義的衍生資料表的資料行數目比*查詢規格*SQL 陳述式的引數。|  
|22001|字串資料，右側截斷|字元或二進位值的資料行的指派會導致的非空白的字元資料或非 null 的二進位資料截斷。|  
|22002|需要指標變數，但是未提供|NULL 資料繫結為輸出參數的*StrLen_or_IndPtr*設定**SQLBindParameter**為 null 指標。|  
|22003|數值超出範圍|**StatementText*包含 SQL 陳述式包含的繫結的數值參數或常值，且值造成要指派給相關聯的資料表資料行時會被截斷的數字 （相對於小數） 的整數部分。<br /><br /> 傳回一或多個輸入/輸出或輸出參數的數值 （以數字或字串） 可能已造成要截斷的數字 （相對於小數） 的整數部分。|  
|22007|無效的 datetime 格式|**StatementText*包含 SQL 陳述式包含日期、 時間戳記結構做為繫結的參數，但參數，分別無效的日期、 時間戳記。<br /><br /> 輸入/輸出或輸出參數已繫結至日期、 時間或時間戳記 C 結構，但傳回的參數中的值，分別無效的日期、 時間戳記。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22008|日期時間欄位溢位|**StatementText*包含 SQL 陳述式包含時計算，導致日期、 時間戳記結構的日期時間運算式不正確。<br /><br /> 日期時間運算式計算的輸入/輸出或輸出參數會導致日期、 時間或時間戳記 C 結構無效。|  
|22012|除數為零|**StatementText*包含 SQL 陳述式包含造成除數為零的算術運算式。<br /><br /> 輸出參數的除法中產生除以零或算術運算式計算的輸入/輸出。|  
|22015|間隔欄位溢位|*\*StatementText*包含精確數值或時間間隔參數，當轉換成 SQL 資料類型的間隔，導致遺失有效位數。<br /><br /> *\*StatementText*包含具有多個欄位的間隔參數，當轉換成數值資料類型資料行中，在沒有表示法的數值資料類型。<br /><br /> *\*StatementText*包含指派給間隔 SQL 類型的參數資料，而且 C 類型的值中的 SQL 類型的間隔沒有表示法。<br /><br /> 指派是精確數值或間隔造成失去有效位數為間隔 C 類型的 SQL 類型的輸入/輸出或輸出參數。<br /><br /> 當輸入/輸出或輸出參數已指派給間隔 C 結構時，時發生間隔資料結構中的資料沒有表示法。|  
|22018|轉換規格的字元值無效|*\*StatementText*包含 C 類型時精確或大約的數字、 日期時間或間隔資料類型; 資料行的 SQL 類型是字元資料類型; 和資料行中的值不是有效的常值的繫結 C 類型。<br /><br /> SQL 型別時傳回的輸入/輸出或輸出參數，為精確或大約的數字、 日期時間或間隔資料類型;C 類型已 SQL_C_CHAR;和資料行中的值不是有效的常值的繫結的 SQL 型別。|  
|22019|無效的逸出字元|\**StatementText*包含 SQL 陳述式包含**像**述詞，以及**逸出**中**其中**子句和逸出的長度之後的字元**逸出**不等於 1。|  
|22025|無效的逸出序列|\**StatementText*包含 SQL 陳述式包含"**像***模式值***逸出***逸出字元*」 中**其中**子句，而且之後的模式值的逸出字元的字元不是其中一個"%"或"_"。|  
|23000|完整性條件約束違規|**StatementText*包含 SQL 陳述式包含參數或常值。 參數值是 NULL，定義為 NOT NULL 相關聯的資料表資料行中的資料行、 資料行限制為只包含唯一值，卻提供了重複的值或違反某些其他的完整性條件約束。|  
|24000|指標狀態無效|資料指標置於*StatementHandle*由**SQLFetch**或**SQLFetchScroll**。 傳回這個錯誤是由驅動程式管理員如果**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標已開啟，但是不位於*StatementHandle*。<br /><br /> **StatementText*自主和定位更新或刪除陳述式中，指標置於結果集或結果集的結尾之後開始之前。|  
|34000|指標名稱無效|**StatementText*自主定位的 update 或 delete 陳述式，並正在執行之陳述式所參考的資料指標未開啟。|  
|3D000|無效的目錄名稱|中指定的目錄名稱*StatementText*無效。|  
|3F000|無效的結構描述名稱|中指定的結構描述名稱*StatementText*無效。|  
|40001|序列化失敗|交易已回復由於與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|相關聯的連接失敗，此函式，在執行期間，無法決定交易的狀態。|  
|42000|語法錯誤或存取違規|\**StatementText*包含 SQL 陳述式不是可準備或包含語法錯誤。<br /><br /> 使用者沒有執行 SQL 陳述式中所包含的權限 **StatementText*。|  
|42S01|基底資料表或檢視已經存在|\**StatementText*包含**CREATE TABLE**或**CREATE VIEW**陳述式和資料表名稱或檢視指定名稱已存在。|  
|42S02|基底資料表或檢視找不到|\**StatementText*包含**DROP TABLE**或**DROP VIEW**陳述式和指定的資料表名稱或檢視名稱不存在。<br /><br /> \**StatementText*包含**ALTER TABLE**陳述式和指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**CREATE VIEW**陳述式和資料表名稱或檢視查詢規格所定義的名稱不存在。<br /><br /> \**StatementText*包含**CREATE INDEX**陳述式和指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**GRANT**或**撤銷**陳述式和指定的資料表名稱或檢視名稱不存在。<br /><br /> \**StatementText*包含**選取**陳述式和指定的資料表名稱或檢視名稱不存在。<br /><br /> \**StatementText*包含**刪除**，**插入**，或**更新**陳述式和指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**陳述式，並指定條件約束 （參考資料表以外建立的一個） 中的資料表不存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**陳述式和指定的資料表名稱或檢視名稱不存在。|  
|42S11|已存在的索引|\**StatementText*包含**CREATE INDEX**陳述式和指定的索引名稱已存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**陳述式和指定的索引名稱已存在。|  
|42S12|找不到索引|\**StatementText*包含**DROP INDEX**陳述式和指定的索引名稱不存在。|  
|42S21|資料行已經存在|\**StatementText*包含**ALTER TABLE**陳述式，並在指定的資料行**新增**子句不是唯一的或識別基底資料表中現有的資料行。|  
|42S22|找不到資料行|\**StatementText*包含**CREATE INDEX**陳述式，和一或多個資料行不存在的資料行清單中指定的名稱。<br /><br /> \**StatementText*包含**GRANT**或**撤銷**陳述式，並指定資料行名稱不存在。<br /><br /> \**StatementText*包含**選取**，**刪除**，**插入**，或**更新**陳述式，並指定資料行名稱不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**陳述式，並指定條件約束 （參考資料表以外建立的一個） 中的資料行不存在。<br /><br /> \**StatementText*包含**CREATE SCHEMA**陳述式，並指定資料行名稱不存在。|  
|44000|WITH CHECK OPTION 違規|引數*StatementText*包含**插入**檢視的資料表上執行的陳述式或衍生自檢視資料表所建立的指定資料表**WITH CHECK OPTION**，好讓一或多個資料列受到**插入**陳述式將不再會出現在檢視的資料表。<br /><br /> 引數*StatementText*包含**更新**檢視的資料表上執行的陳述式或衍生自檢視資料表所建立的指定資料表**WITH CHECK OPTION**，好讓一或多個資料列受到**更新**陳述式將不再會出現在檢視的資料表。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|無效的 null 指標使用|(DM) **StatementText*為 null 指標。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLExecDirect**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數*TextLength*小於或等於 0，但不是等於 SQL_NTS。<br /><br /> 參數值時，設定與**SQLBindParameter**、 null 指標，且驗證的參數長度值不是 0，SQL_NULL_DATA、 SQL_DATA_AT_EXEC，SQL_DEFAULT_PARAM，或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 參數值時，設定與**SQLBindParameter**、 不是 null 指標，則為 C 資料類型為 SQL_C_BINARY 或 SQL_C_CHAR; 但參數長度值小於 0，但不是 SQL_NTS、 SQL_NULL_DATA、 SQL_DATA_AT_EXEC、 SQL_DEFAULT_參數，或小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 由繫結參數的長度值**SQLBindParameter**是設定為 SQL_DATA_AT_EXEC; 的 SQL 型別是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或的長資料來源特定的資料類型; 以及 SQL_NEED_LONG_DATA_LEN 資訊在中輸入**SQLGetInfo**已"Y"。|  
|HY105|無效的參數類型|指定的引數的值*了*中**SQLBindParameter**是 SQL_PARAM_OUTPUT，而參數是輸入的參數。|  
|HY109|無效的資料指標位置|\**StatementText*定位的 update 或 delete 陳述式，以及指標置於自主 (由**SQLSetPos**或**SQLFetchScroll**) 上的資料列都已刪除或無法提取。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，，並且 SQL_ATTR_CURSOR_TYPE 陳述式屬性設定為 驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 逾時期限透過設定**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 應用程式會呼叫**SQLExecDirect**傳送至資料來源的 SQL 陳述式。 如需有關直接執行的詳細資訊，請參閱[直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)。 驅動程式會修改使用形式的資料來源所使用的 SQL 陳述式，然後將它提交至資料來源。 特別是，驅動程式會修改用來定義某些功能在 SQL 中的逸出序列。 如需逸出序列的語法，請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。  
  
 應用程式可以包含 SQL 陳述式中的一個或多個參數標記。 若要包含的參數標記，應用程式會嵌入 SQL 陳述式的適當位置的問號 （？）。 如需參數的資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 如果 SQL 陳述式**選取**陳述式，如果應用程式呼叫**SQLSetCursorName**與陳述式中的資料指標，然後驅動程式會使用指定的資料指標。 否則，此驅動程式會產生資料指標名稱。  
  
 如果資料來源是在手動認可模式 （需要明確的交易初始），而且已經未起始交易，此驅動程式傳送的 SQL 陳述式之前，就會起始交易。 如需詳細資訊，請參閱[手動認可模式](../../../odbc/reference/develop-app/manual-commit-mode.md)。  
  
 如果應用程式使用**SQLExecDirect**提交**認可**或**復原**陳述式，就不會 DBMS 產品之間互通。 若要認可或回復交易，應用程式呼叫**SQLEndTran**。  
  
 如果**SQLExecDirect**遇到資料在執行中參數，它會傳回 SQL_NEED_DATA。 在應用程式傳送資料使用**SQLParamData**和**SQLPutData**。 請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，和[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 如果**SQLExecDirect**執行搜尋的 update、 insert 或 delete 陳述式，不會影響任何資料來源，呼叫端的資料列**SQLExecDirect**傳回 sql_no_data 為止。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 陳述式屬性的值大於 1，SQL 陳述式中包含至少一個參數標記， **SQLExecDirect**會執行每一組參數值從一次的 SQL 陳述式所指陣列*ParameterValuePointer*引數在呼叫**SQLBindParameter**。 如需詳細資訊，請參閱[參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 如果書籤已開啟且在執行的查詢可能不支援書籤，驅動程式應該嘗試強制轉型為書籤支援藉由變更屬性值，並傳回 SQLSTATE 01S02 環境 （選項值已變更）。 如果無法變更屬性，驅動程式應該會傳回 SQLSTATE HY024 （無效的屬性值）。  
  
> [!NOTE]  
>  當使用連接共用時，應用程式必須執行 SQL 陳述式變更資料庫或資料庫的內容，例如**使用***資料庫*變更的 SQL Server 中的陳述式資料來源所使用的目錄。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，和[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行認可或復原作業|[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料指標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|擷取部分或全部的資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回將資料傳送下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|傳送參數資料在執行階段|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

