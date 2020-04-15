---
title: SQLExecDirect 函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5739e397467deb684a4cd6c7b13a507f30b53fa7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286108"
---
# <a name="sqlexecdirect-function"></a>SQLExecDirect 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLExecDirect**執行可準備語句,使用參數標記變數的當前值(如果語句中存在任何參數)。 **SQLExecDirect**是提交 SQL 語句進行一次性執行的最快方法。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLExecDirect(  
     SQLHSTMT     StatementHandle,  
     SQLCHAR *    StatementText,  
     SQLINTEGER   TextLength);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *語句文字*  
 [輸入]要執行的 SQL 語句。  
  
 *TextLength*  
 [輸入]長度 =*字元語句文字*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_NO_DATA、SQL_INVALID_HANDLE或SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLExecDirect**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*語句句柄*的*句柄*。 下表列出了**SQLExecDirect**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01001|游標操作衝突|\**語句文字*包含定位的更新或刪除語句,並且沒有更新或刪除任何行或多行。 (有關對多行的更新的詳細資訊,請參閱**SQLSetStmtAttr**中的SQL_ATTR_SIMULATE_CURSOR*屬性*的說明。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|01003|在設定函數中消除的 NULL 值|參數*語句文本*包含一個集函數(如**AVG、MAX、MIN**等),但不包括**COUNT**集函數,在應用函數之前消除**MAX****MIN**了 NULL 參數值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|為輸入/輸出或輸出參數返回的字串或二進位資料導致非空白字元或非 NULL 二進位資料的截斷。 如果它是一個字串值,它是右截斷的。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01006|未復原權限|\**語句文本*包含**REVOKE**語句,並且使用者沒有指定的許可權。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01007|未授予權限|語句文本是一個**GRANT**語句,無法授予使用者指定的*\** 許可權。|  
|01S02|選項值已變更|由於實現工作條件,指定的語句屬性無效,因此臨時替換了類似的值。 (可以調用**SQLGetStmtAttr**以確定臨時替換的值是什麼。替換值對*語句處理*有效,直到游標關閉,此時語句屬性將還原到其上一個值。 可以變更的語片屬性包括:<br /><br /> SQL_ATTR_CONCURRENCY SQL_ SQL_ ATTR_MAX_LENGTH SQL_ SQL_ ATTR_CURSOR_TYPE SQL_ATTR_CONCURRENCYATTR_CONCURRENCYATTR_QUERY_TIMEOUTSQL_ATTR_SIMULATE_CURSORATTR_QUERY_TIMEOUTATTR_MAX_ROWSATTR_QUERY_TIMEOUTATTR_QUERY_TIMEOUTATTR_KEYSET_SIZEATTR_KEYSET_SIZEATTR_KEYSET_SIZEATTR_QUERY_TIMEOUTATTR_QUERY_TIMEOUTSQL_<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S07|分數截斷|為輸入/輸出或輸出參數返回的數據被截斷,因此數位資料類型的小數部分被截斷或時間、時間戳或間隔數據類型的時間分量的分數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07002|COUNT 欄位不正確|**SQLBind參數**中指定的參數數小\*於*語句文本*中包含的 SQL 語句中的參數數。<br /><br /> **SQLBind參數**呼叫時 *,參數ValuePtr*設定為空指標 *,StrLen_or_IndPtr*未設置為SQL_NULL_DATA或SQL_DATA_AT_EXEC,*並且輸入輸出類型*未設置為SQL_PARAM_OUTPUT,因此**SQLBind 參數**中指定的參數數大於 #*語句文本*中包含的 SQL 語句中的參數數。|  
|07006|受限資料類型屬性衝突|綁定參數的**SQLBind 參數**中*的值類型*參數識別的資料值無法轉換為**SQLBind 參數**中的*參數類型*參數識別的資料類型。<br /><br /> 返回為SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT綁定的參數的數據值無法轉換為**SQLBind 參數**中*ValueType*參數標識的數據類型。<br /><br /> (如果無法轉換一個或多個行的數據值,但成功返回一個或多個行,則此函數將返回SQL_SUCCESS_WITH_INFO。|  
|07007|受限參數值衝突|參數類型SQL_PARAM_INPUT_OUTPUT_STREAM僅用於以零件發送和接收數據的參數。 此參數類型不允許輸入綁定緩衝區。<br /><br /> 當參數類型SQL_PARAM_INPUT_OUTPUT,並且\***SQLBind 參數**中指定的*StrLen_or_IndPtr*不等於SQL_NULL_DATA、SQL_DEFAULT_PARAM、SQL_LEN_DATA_AT_EXEC(len)或SQL_DATA_AT_EXEC時,將發生此錯誤。|  
|07S01|預設參數使用無效|使用**SQLBind 參數**設置的參數值SQL_DEFAULT_PARAM,並且相應的參數沒有預設值。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|21S01|插入值清單與列清單不匹配|\**語句文字*包含一個**INSERT**語句,要插入的值數與派生表的程度不匹配。|  
|21S02|衍生表的程度與列清單不符合|\**語句文字*包含**CREATE VIEW**語句,並且非限定列清單(SQL 語句的*列識別符*參數中為視圖指定的欄數)包含的名稱多於 SQL 語句*的查詢規範*參數定義的派生表中的欄數。|  
|22001|字串資料,右截斷|將字元或二進位值分配給列會導致非空白字元資料或非空二進位數據的截斷。|  
|22002|需要指標變數,但未提供|NULL 資料繫結到輸出參數,其*StrLen_or_IndPtr*由**SQLBind 參數**設定為空指標。|  
|22003|數值超範圍|**語句文字*包含包含綁定數值參數或文本的 SQL 語句,並且該值導致在分配給關聯的表列時,將數位的整個(而不是小數)部分被截斷。<br /><br /> 為一個或多個輸入/輸出或輸出參數返回數值(作為數位或字串)將導致數位的整個(而不是小數)部分被截斷。|  
|22007|不合法日期時間格式|**語句文字*包含一個 SQL 語句,該語句包含日期、時間或時間戳結構作為綁定參數,並且該參數分別是無效的日期、時間或時間戳。<br /><br /> 輸入/輸出或輸出參數綁定到日期、時間或時間戳 C 結構,傳回參數中的值分別為無效日期、時間或時間戳。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|22008|日期時間欄位溢出|**語句文字*包含一個 SQL 語句,其中包含一個日期時間表達式,該運算式在計算時導致日期、時間或時間戳結構無效。<br /><br /> 為輸入/輸出或輸出參數計算的 datetime 運算式會導致日期、時間或時間戳 C 結構無效。|  
|22012|除零|**語句文本*包含一個 SQL 語句,其中包含導致零除法的算術表達式。<br /><br /> 為輸入/輸出或輸出參數計算的算術表達式導致除以零。|  
|22015|間隔欄位溢出|語句文字包含一個精確的數位或間隔參數,當轉換為間隔 SQL 資料類型時,該參數會導致重要數位的*\** 損失。<br /><br /> 語句文字包含一個包含多個字段的間隔參數,當該欄位轉換為列中的數位數據類型時,數位數據類型中沒有表示形式。 * \* *<br /><br /> 語句文字包含分配給間隔 SQL 類型的參數數據,並且間隔 SQL 類型中沒有 C*\** 類型的值表示形式。<br /><br /> 將精確數位或間隔 SQL 類型的輸入/輸出或輸出參數分配給間隔 C 類型會導致有效數位遺失。<br /><br /> 當輸入/輸出參數分配給間隔 C 結構時,間隔數據結構中沒有數據的表示形式。|  
|22018|強制轉換規範的不合法字元值|語句文字包含一個 C 類型,該類型是精確或近似數位、日期時間或間隔數據*\** 類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。<br /><br /> 返回輸入/輸出或輸出參數時,SQL 類型是精確或近似的數位、日期時間或間隔數據類型;C 類型為SQL_C_CHAR;列中的值不是綁定 SQL 類型的有效文本。|  
|22019|不合法的字元|\**語句文本*包含一個 SQL 語句,該語句包含一個與**WHERE**子句中**帶有 ESCAPE 的** **LIKE**謂詞,**並且 ESCAPE**之後的轉義字元的長度不等於 1。|  
|22025|不合法序列|\**語句文本*包含一個 SQL 語句,該語句在**WHERE**子句中包含 **"LIKE**_模式值_ **ESCAPE** _轉義字元_",模式值中轉義字元後的角色不是"%"或"*"。|  
|23000|完整性約束衝突|**語句文字*包含包含參數或文字的 SQL 語句。 對於在關聯的表列中定義為"非 NULL"的列,參數值為 NULL,為僅包含唯一值的列提供了重複值,或者違反了某些其他完整性約束。|  
|24000|指標狀態無效|**通過 SQLFetch**或**SQLFetchScroll**在*語句處理*上定位了一個游標。 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> 游標已打開,但未放置在*語句處理*上。<br /><br /> **語句文字*包含定位的更新或刪除語句,游標位於結果集開始之前或結果集結束之後。|  
|34000|指標名稱無效|**語句文本*包含定位的更新或刪除語句,並且執行的語句引用的游標未打開。|  
|3D000|無效目錄名稱|*語句文字*中指定的目錄名稱無效。|  
|3F000|不合法的架構名稱|*語句文字*中指定的架構名稱無效。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|42000|語法錯誤或存取衝突|\**語句文字*包含一個不可預備的 SQL 語句或包含語法錯誤。<br /><br /> 使用者沒有執行 **語句文字*中包含的 SQL 語句的許可權。|  
|42S01|基本表或檢視已存在|\**語句文字*包含 **"創建表"** 或 **"創建檢視**"語句,指定的表名稱或視圖名稱已存在。|  
|42S02|找不到基本表或檢視|\**語句文字*包含**DROP TABLE**或**DROP VIEW**語句,並且指定的表名稱或檢視名稱不存在。<br /><br /> \**語句文字*包含**ALTER TABLE**語句,並且指定的表名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE VIEW**語句,查詢規範定義的表名稱或視圖名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE INDEX**語句,並且指定的表名稱不存在。<br /><br /> \**語句文字*包含一個**GRANT**或**REVOKE**語句,並且指定的表名稱或視圖名稱不存在。<br /><br /> \**語句文字*包含**SELECT**語句,並且指定的表名稱或檢視名稱不存在。<br /><br /> \**語句文字*包含**DELETE、INSERT**或**UPDATE**語句,並且指定**INSERT**的表名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE TABLE**語句,並且約束中指定的表(引用正在創建的表以外的表)不存在。<br /><br /> \**語句文字*包含一個**CREATE SCHEMA**語句,並且指定的表名稱或檢視名稱不存在。|  
|42S11|索引已存在|\**語句文字*包含一個**CREATE INDEX**語句,並且指定的索引名稱已經存在。<br /><br /> \**語句文字*包含一個**CREATE SCHEMA**語句,並且指定的索引名稱已經存在。|  
|42S12|找不到索引|\**語句文字*包含**DROP INDEX**語句,並且指定的索引名稱不存在。|  
|42S21|欄位已存在|\**語句文字*包含**ALTER TABLE**語句 **,ADD**子句中指定的列不是唯一的,或識別基表中的現有列。|  
|42S22|找不到欄|\**語句文字*包含**CREATE INDEX**語句,列清單中指定的一個或多個列名稱不存在。<br /><br /> \**語句文字*包含**GRANT**或**REVOKE**語句,並且指定的列名稱不存在。<br /><br /> \**語句文字*包含**SELECT、DELETE、****插入**或**更新**語句,並且**SELECT**指定的列名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE TABLE**語句,並且約束中指定的列(引用正在創建的表以外的表)不存在。<br /><br /> \**語句文字*包含一個**CREATE SCHEMA**語句,並且指定的列名稱不存在。|  
|44000|WITH CHECK OPTION 違規|參數*語句文字*包含在查看的表或從已查看表派生的表上執行的**INSERT**語句,該表是透過指定 **「使用 CHECK 選項**」創建的,這樣受**INSERT**語句影響的一個或多個行將不再存在於已查看的表中。<br /><br /> 參數*語句文字*包含在已查看的表或從已查看表派生的表上執行**的更新**語句,該表是通過指定 **「使用 CHECK 選項**」創建的,以便受**UPDATE**語句影響的一個或多個行不再存在於已查看的表中。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|(DM) =*語句文字*是一個空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLExecDirect**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 參數*文本長度*小於或等於 0,但不等於SQL_NTS。<br /><br /> 使用**SQLBindParameter**設置的參數值是空指標,參數長度值不是 0、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM或小於或等於SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 使用 SQLBind 參數設定的參數值不是空指標,而使用**SQLBind 參數**設置的參數值不是空指標。C 數據類型為SQL_C_BINARY或SQL_C_CHAR;參數長度值小於 0,但未SQL_NTS、SQL_NULL_DATA、SQL_DATA_AT_EXEC、SQL_DEFAULT_PARAM或小於或等於SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 由**SQLBind 參數**綁定的參數長度值設置為SQL_DATA_AT_EXEC;SQL 類型要麼是SQL_LONGVARCHAR、SQL_LONGVARBINARY,要麼是長數據源特定的數據類型;**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN資訊類型為"Y"。|  
|HY105|不合法參數型態|為**SQLBind 參數**中為參數*InputOutputType*指定的值SQL_PARAM_OUTPUT,該參數為輸入參數。|  
|HY109|游標位置無效|\**語句文字*包含定位的更新或刪除語句,並且游標被定位在已刪除或無法提取的行上(由**SQLSetPos**或**SQLFetchScroll)。**|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 應用程式呼叫**SQLExecDirect**向資料來源傳送 SQL 語句。 有關直接執行的詳細資訊,請參閱[直接執行](../../../odbc/reference/develop-app/direct-execution-odbc.md)。 驅動程式修改語句以使用數據來源使用的 SQL 形式,然後將其提交到數據源。 特別是,驅動程式修改用於在 SQL 中定義某些要素的轉義序列。 有關逸出序列的語法,請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。  
  
 應用程式可以在 SQL 語句中包含一個或多個參數標記。 要包含參數標記,應用程式在適當的位置將問號(?) 嵌入到 SQL 語句中。 有關參數的資訊,請參閱[敘述參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
 如果 SQL 語句是**SELECT**語句,並且應用程式稱為**SQLSetCursorName**將游標與語句相關聯,則驅動程式將使用指定的游標。 否則,驅動程式將生成游標名稱。  
  
 如果數據源處於手動提交模式(需要顯式事務啟動),並且尚未啟動事務,則驅動程式會在發送 SQL 語句之前啟動事務。 有關詳細資訊,請參閱[手動提交模式](../../../odbc/reference/develop-app/manual-commit-mode.md)。  
  
 如果應用程式使用**SQLExecDirect**提交**COMMIT**或**ROLLBACK**語句,則在 DBMS 產品之間無法互通。 要提交或回滾事務,應用程式將呼叫**SQLEndTran**。  
  
 如果**SQLExecDirect**遇到執行時的數據參數,它將返回SQL_NEED_DATA。 應用程式使用**SQLParam 資料和** **SQLPutData**發送數據。 請參考[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md)[、SQLParamData、SQLPutData](../../../odbc/reference/syntax/sqlparamdata-function.md)與[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)[送出長資料](../../../odbc/reference/develop-app/sending-long-data.md)。  
  
 如果**SQLExecDirect**執行搜尋的更新、插入或刪除不影響數據源上任何行的語句,則對**SQLExecDirect**的調用將返回SQL_NO_DATA。  
  
 如果SQL_ATTR_PARAMSET_SIZE語句屬性的值大於 1,並且 SQL 語句至少包含一個參數標記 **,SQLExecDirect**將針對呼叫**SQLBind 參數**中參數*中*指向的陣列中的每組參數值執行一次 SQL 語句。 有關詳細資訊,請參閱[參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 如果啟用書籤並執行不支援書籤的查詢,驅動程式應嘗試透過更改屬性值並返回 SQLSTATE 01S02(選項值已更改)來強制環境強制環境為支援書籤的環境。 如果無法更改屬性,驅動程式應返回 SQLSTATE HY024(無效屬性值)。  
  
> [!NOTE]  
>  使用連接池時,應用程式不得執行更改資料庫或資料庫上下文的 SQL 語句,例如 SQL Server 中的**USE** _資料庫_語句,該語句更改數據來源使用的目錄。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[SQLBindCol、SQLGetData](../../../odbc/reference/syntax/sqlbindcol-function.md)與[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)。 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行提交或回滾操作|[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|取得多行資料|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回游標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|取得資料欄的一部份或全部|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回下一個參數以送出資料|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|準備執行敘述|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|在執行時傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|設定游標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
