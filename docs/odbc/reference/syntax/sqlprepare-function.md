---
title: SQL準備功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e9aedd665df2a943627207902d592d597c503c63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306879"
---
# <a name="sqlprepare-function"></a>SQLPrepare 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLPrepare**準備一個 SQL 字串進行執行。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *語句文字*  
 [輸入]SQL 文字字串。  
  
 *TextLength*  
 [輸入]長度 =*字元語句文字*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLPrepare**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了 SQLPrepare 通常返回的**SQLSTATE**值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|由於實現工作條件,指定的語句屬性無效,因此臨時替換了類似的值。 (可以調用**SQLGetStmtAttr**以確定臨時替換的值是什麼。在游標關閉之前,替換值對*語句處理*有效。 可以更改的語句屬性是:SQL_ATTR_CONCURRENCY SQL_ATTR_CURSOR_TYPESQL_ATTR_KEYSET_SIZESQL_ATTR_QUERY_TIMEOUTSQL_ATTR_QUERY_TIMEOUT SQL_ATTR_MAX_ROWSSQL_ATTR_KEYSET_SIZESQL_ATTR_MAX_LENGTH SQL_ATTR_SIMULATE_CURSORSQL_ATTR_CONCURRENCY<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|21S01|插入值清單與列清單不匹配|\**語句文字*包含一個**INSERT**語句,要插入的值數與派生表的程度不匹配。|  
|21S02|衍生表的程度與列清單不符合|\**語句文字*包含一個**CREATE VIEW**語句,並且指定的名稱數與查詢規範定義的派生表的程度不同。|  
|22018|強制轉換規範的不合法字元值|**語句文字*包含包含文本或參數的 SQL 語句,並且該值與關聯的表列的數據類型不相容。|  
|22019|不合法的字元|參數*語句文本*包含一個**LIKE**謂詞,其中包含**WHERE**子句中的**ESCAPE,** 並且**ESCAPE**之後的轉義字元的長度不等於 1。|  
|22025|不合法序列|參數*語句文本*在**WHERE**子句中包含 **「LIKE** _模式值_ **ESCAPE** _轉義字元_」,模式值中轉義字元之後的字元既不是"%"也不是"*"。|  
|24000|指標狀態無效|(DM)*語句處理*上打開一個游標,並且調用**了 SQLFetch**或**SQLFetchScroll。**<br /><br /> *語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。|  
|34000|指標名稱無效|\**語句文字*包含定位的**DELETE**或定位**的更新**,並且準備語句引用的游標未打開。|  
|3D000|無效目錄名稱|*語句文字*中指定的目錄名稱無效。|  
|3F000|不合法的架構名稱|*語句文字*中指定的架構名稱無效。|  
|42000|語法錯誤或存取衝突|\**語句文字*包含一個不可預備的 SQL 語句或包含語法錯誤。<br /><br /> **語句文本*包含一個聲明,用戶沒有所需的許可權。|  
|42S01|基本表或檢視已存在|\**語句文字*包含 **"創建表"** 或 **"創建檢視**"語句,指定的表名稱或視圖名稱已存在。|  
|42S02|找不到基本表或檢視|\**語句文字*包含**DROP TABLE**或**DROP VIEW**語句,並且指定的表名稱或檢視名稱不存在。<br /><br /> \**語句文字*包含**ALTER TABLE**語句,並且指定的表名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE VIEW**語句,查詢規範定義的表名稱或視圖名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE INDEX**語句,並且指定的表名稱不存在。<br /><br /> \**語句文字*包含一個**GRANT**或**REVOKE**語句,並且指定的表名稱或視圖名稱不存在。<br /><br /> \**語句文字*包含**SELECT**語句,並且指定的表名稱或檢視名稱不存在。<br /><br /> \**語句文字*包含**DELETE、INSERT**或**UPDATE**語句,並且指定**INSERT**的表名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE TABLE**語句,並且約束中指定的表(引用正在創建的表以外的表)不存在。|  
|42S11|索引已存在|\**語句文字*包含一個**CREATE INDEX**語句,並且指定的索引名稱已經存在。|  
|42S12|找不到索引|\**語句文字*包含**DROP INDEX**語句,並且指定的索引名稱不存在。|  
|42S21|欄位已存在|\**語句文字*包含**ALTER TABLE**語句 **,ADD**子句中指定的列不是唯一的,或識別基表中的現有列。|  
|42S22|找不到欄|\**語句文字*包含**CREATE INDEX**語句,列清單中指定的一個或多個列名稱不存在。<br /><br /> \**語句文字*包含**GRANT**或**REVOKE**語句,並且指定的列名稱不存在。<br /><br /> \**語句文字*包含**SELECT、DELETE、****插入**或**更新**語句,並且**SELECT**指定的列名稱不存在。<br /><br /> \**語句文字*包含一個**CREATE TABLE**語句,並且約束中指定的列(引用正在創建的表以外的表)不存在。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**在*語句句柄*上調用 ,然後在*語句句柄*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|(DM)*語句文字*是一個空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLPrepare**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 參數*文本長度*小於或等於 0,但不等於SQL_NTS。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|對於定義的游標類型,併發設置無效。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|超時期限在數據源返回結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 應用程式呼叫**SQLPrepare**將 SQL 語句發送到資料來源進行準備。 有關準備執行的詳細資訊,請參閱[準備執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。 應用程式可以在 SQL 語句中包含一個或多個參數標記。 要包含參數標記,應用程式在適當的位置將問號(?) 嵌入到 SQL 字串中。 有關參數的資訊,請參閱[敘述參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
> [!NOTE]  
>  如果應用程式使用**SQLPrepare**準備和**SQLExecute**提交**COMMIT**或**ROLLBACK**語句,則在 DBMS 產品之間無法互通。 要提交或回滾事務,請呼叫**SQLEndTran**。  
  
 驅動程式可以修改語句以使用數據來源使用的 SQL 形式,然後將其提交到數據源進行準備。 特別是,驅動程式修改用於定義某些功能的 SQL 語法的轉義序列。 (有關 SQL 語句語法的說明,請參閱 ODBC 和附錄 C[中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)[:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。對於驅動程式,語句句柄類似於嵌入 SQL 代碼中的語句標識符。 如果數據源支援語句標識符,驅動程式可以將語句標識符和參數值發送到數據源。  
  
 準備語句后,應用程式使用語句句柄在以後的函數調用中引用語句。 通過呼叫**SQLExecute**可以重新執行與敘述的點塊關聯的準備語句,直到應用程式使用 SQL_DROP 選項釋放對**SQLFreeStmt**的呼叫語句,或者直到語句句柄用於呼叫**SQLPrepare、SQLExecDirect**或**SQLExecDirect**目錄函數之一 **(SQLColumns、SQLTables**等) **SQLTables** 應用程式準備語句后,可以請求有關結果集格式的資訊。 對於某些實現,在**SQLPrepare**之後調用**SQLDescribeCol**或**SQLDescribeParam**可能不如在**SQLExecute**或**SQLExecDirect**之後調用函數更有效。  
  
 當應用程式呼叫**SQLPrepare**時,某些驅動程式無法返回語法錯誤或訪問衝突。 驅動程式可以處理語法錯誤和訪問衝突,只能處理語法錯誤,或者語法錯誤和訪問衝突。 因此,應用程式在調用後續相關函數(如 SQLNumCols、SQLDescribeCol、SQLCol**屬性**和**SQLExecute)** 時必須能夠**SQLNumResultCols****SQLDescribeCol**處理這些條件。  
  
 根據驅動程式和數據源的功能,在編寫語句(如果所有參數都已綁定)或執行語句(如果所有參數尚未綁定)時,可能會檢查參數資訊(如數據類型)。 為了達到最大互操作性,應用程式應在對同一語句上準備新的 SQL 語句之前取消綁定應用於舊 SQL 語句的所有參數。 這樣可以防止由於舊參數資訊應用於新語句而導致的錯誤。  
  
> [!IMPORTANT]  
>  通過顯式調用**SQLEndTran**或以自動提交模式工作來提交事務,可能會導致數據源刪除連接上所有語句的訪問計劃。 有關詳細資訊,請參閱[SQLGetInfo 中](../../../odbc/reference/syntax/sqlgetinfo-function.md)SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR資訊類型以及[事務對游標和準備敘述的影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md) [、SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)與[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置敘述|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|將緩衝區繫結到參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行提交或回滾操作|[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回受語句影響的行數|[SQLRowCount 函數](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|設定游標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
