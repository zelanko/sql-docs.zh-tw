---
title: SQL程式列函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedureColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedureColumns
helpviewer_keywords:
- SQLProcedureColumns function [ODBC]
ms.assetid: 4ca37b28-a6df-465b-8988-d422d37fc025
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d81e44b116ed6f26319d31430999a61a8a17f21
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306849"
---
# <a name="sqlprocedurecolumns-function"></a>SQLProcedureColumns 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLProcessColumns**傳回輸入和輸出參數的清單,以及構成指定過程的結果集的列。 驅動程式將返回資訊作為指定語句上的結果集。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLProcedureColumns(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     ProcName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *目錄名稱*  
 [輸入]過程目錄名稱。 如果驅動程式支援某些過程的目錄,但不支援其他過程的目錄,例如當驅動程式從不同的 DBMS 檢索數據時,空字串("")表示那些沒有目錄的過程。 *目錄名稱*不能包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則*目錄名稱*將被視為標識符,其大小寫不重要。 如果SQL_FALSE,目錄名稱是普通參數;如果為「*目錄名稱」,則為「目錄名稱」,* 但為「目錄名稱」,但為「目錄名稱」,但它被從字面上處理,它的情況很重要。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度在 **目錄名稱*的字元中。  
  
 *架構名稱*  
 [輸入]字串搜索模式的過程架構名稱。 如果驅動程式支援某些過程的架構,但不支援其他過程的架構(例如當驅動程式從不同的 DBMS 檢索數據時),空字串("")表示那些沒有架構的過程。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 SchemaName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,則 SchemaName 是模式值參數;如果為 SQL_FALSE,則 *「架構名稱」* 是模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度2*  
 [輸入]長度在 **架構名稱*的字元中。  
  
 *ProcName*  
 [輸入]字串搜尋模式的過程名稱。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 ProcName*被視為識別碼,其大小寫不重要。 如果*SQL_FALSE,ProcName*是模式值參數;如果為 SQL_FALSE,則 ProcName 是模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度3*  
 [輸入]長度在 =*ProcName*的字元中。  
  
 *ColumnName*  
 [輸入]字串搜尋模式的列名稱。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,則*ColumnName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,則「列名」是模式值參數;如果為「*列名稱」,* 則為「列名」,即為模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度4*  
 [輸入]長度以 =*列名*的字元表示。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQL 程式列**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT*Handle*的*句柄類型*和*敘述句柄*。 下表列出了**SQLAk**通常返回的 SQLSTATE 值,並解釋了此函數上下文中的每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|語句*處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLError**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*目錄名稱*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID敘述屬性設定為SQL_TRUE,*而 SchemaName、ProcName*或*列名**ProcName*參數是空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用 SQLAAK 函數時,此 aynschronous 函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY090|不合法的字串或緩衝區長度|(DM) 其中一個名稱長度參數的值小於 0,但不等於SQL_NTS。<br /><br /> 其中一個名稱長度參數的值超過相應目錄、架構、過程或列名稱的最大長度值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了過程目錄,驅動程式或數據源不支援目錄。<br /><br /> 已指定過程架構,驅動程式或數據源不支援架構。<br /><br /> 為過程架構、過程名稱或列名稱指定了字串搜索模式,數據源不支援一個或多個這些參數的搜索模式。<br /><br /> 驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|超時期限在數據源返回結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 此函數通常在語句執行之前用於檢索有關過程參數以及構成過程返回的結果集或集的列(如果有)的資訊。 如需詳細資訊，請參閱[程序](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  **SQL程式列**可能不會返回過程使用的所有列。 例如,驅動程式可能只返回有關過程使用的參數的資訊,而不是返回它生成的結果集中的列的資訊。  
  
 *架構名稱**、ProcName*和*列名*參數接受搜尋模式。 關於有效搜尋模式的詳細資訊,請參考[模式值參數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQL程式列**將結果作為標準結果集返回,按PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME和COLUMN_TYPE排序。 按以下順序為每個過程返回列名稱:返回值的名稱、過程調用中每個參數的名稱(按調用順序),然後返回過程返回的結果集中每個列的名稱(按列順序排列)。  
  
 應用程式應綁定相對於結果集末尾的特定於驅動程式的列。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
 要確定PROCEDURE_CAT、PROCEDURE_SCHEM、PROCEDURE_NAME和COLUMN_NAME列的實際長度,應用程式可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_PROCEDURE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN選項調用**SQLGetInfo。**  
  
 以下列已重新命名為 ODBC 3。*x*. . 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC 3.*x*欄|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|程式_OWNER|PROCEDURE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 以下列已添加到由 ODBC 3 的**SQL 過程列**返回的結果集中。*x*:  
  
-   COLUMN_DEF  
  
-   DATETIME_CODE  
  
-   CHAR_OCTET_LENGTH  
  
-   ORDINAL_POSITION  
  
-   IS_NULLABLE  
  
 下表列出了結果集中的列。 驅動程式可以定義第 19 欄(IS_NULLABLE)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|程序目錄名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些過程的目錄,但不支援其他過程的目錄(例如當驅動程式從不同的 DBMS 檢索數據時),它將返回一個空字串(""),用於那些沒有目錄的過程。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|過程架構名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些過程的架構,但不支援其他過程的架構(例如當驅動程式從不同的 DBMS 檢索數據時),它將返回一個空字串(""),用於那些沒有架構的過程。|  
|PROCEDURE_NAME (ODBC 2.0)|3|瓦爾查爾不是 NULL|程序名稱。 對於沒有名稱的過程,將返回一個空字串。|  
|COLUMN_NAME (ODBC 2.0)|4|瓦爾查爾不是 NULL|過程列名稱。 驅動程式返回沒有名稱的過程列的空字串。|  
|COLUMN_TYPE (ODBC 2.0)|5|Smallint 非 NULL|將程序列定義為參數或結果集列:<br /><br /> SQL_PARAM_TYPE_UNKNOWN:過程列是其類型未知參數。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT:過程列是輸入參數。 (ODBC 1.0)<br /><br /> SQL_PARAM_INPUT_OUTPUT:過程列是輸入/輸出參數。 (ODBC 1.0)<br /><br /> SQL_PARAM_OUTPUT:過程列是輸出參數。 (ODBC 2.0)<br /><br /> SQL_RETURN_VALUE:過程列是過程的返回值。 (ODBC 2.0)<br /><br /> SQL_RESULT_COL:過程列是結果集列。 (ODBC 1.0)|  
|DATA_TYPE (ODBC 2.0)|6|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或特定於驅動程式的 SQL 資料類型。 對於日期時間和間隔數據類型,此列返回簡潔的數據類型(例如,SQL_TYPE_TIME或SQL_INTERVAL_YEAR_TO_MONTH)。 有關有效的 ODBC SQL 資料類型的清單,請參閱附錄 D 中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md):資料類型。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。|  
|TYPE_NAME (ODBC 2.0)|7|瓦爾查爾不是 NULL|與數據源相關的數據類型名稱;例如,"CHAR","VARCHAR","金錢","長VARBINARY",或"CHAR ( ) BIT 數據"。|  
|COLUMN_SIZE (ODBC 2.0)|8|整數|數據源上過程列的列大小。 對於不適用的列大小資料類型,將傳回 NULL。 有關精度的詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):數據類型。|  
|BUFFER_LENGTH (ODBC 2.0)|9|整數|如果指定了SQL_C_DEFAULT,則在**SQLGetData**或**SQLFetch**操作上傳輸的數據的長度(以位元組為單位)。 對於數位資料,此大小可能與存儲在數據源上的數據的大小不同。 有關詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。"資料類型"。|  
|DECIMAL_DIGITS (ODBC 2.0)|10|Smallint|數據源上過程列的小數位數。 對於不適用十進位數字的數據類型,傳回 NULL。 有關十進位數字的詳細資訊,請參閱[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md),參見附錄 D:資料類型。|  
|NUM_PREC_RADIX (ODBC 2.0)|11|Smallint|對於數位數據類型,10 或 2。<br /><br /> 如果為 10,則COLUMN_SIZE和DECIMAL_DIGITS中的值將給出該列允許的十進位數字數。 例如,DECIMAL(12,5)列將返回NUM_PREC_RADIX 10、COLUMN_SIZE 12 和 DECIMAL_DIGITS 5;FLOAT 列可以返回 10 NUM_PREC_RADIX、COLUMN_SIZE 15 和 null DECIMAL_DIGITS。<br /><br /> 如果為 2,則COLUMN_SIZE和DECIMAL_DIGITS中的值給出列中允許的位數。 例如,FLOAT 列可以返回 NUM_PREC_RADIX 2、COLUMN_SIZE 53 和 DECIMAL_DIGITS NULL。<br /><br /> 對於不適用NUM_PREC_RADIX的數據類型,將返回 NULL。|  
|空值 (ODBC 2.0)|12|Smallint 非 NULL|將列是否接受 NULL 值:<br /><br /> SQL_NO_NULLS:過程列不接受 NULL 值。<br /><br /> SQL_NULLABLE:過程列接受 NULL 值。<br /><br /> SQL_NULLABLE_UNKNOWN:不知道過程列是否接受 NULL 值。|  
|備註 (ODBC 2.0)|13|Varchar|過程列的說明。|  
|COLUMN_DEF (ODBC 3.0)|14|Varchar|資料行的預設值。<br /><br /> 如果 NULL 被指定為預設值,則此列是單詞 NULL,而不是用引號括起來。 如果不進行截斷就無法表示預設值,則此列包含截斷,不包含單個引號。 如果未指定預設值,則此列為 NULL。<br /><br /> COLUMN_DEF的值可用於生成新的列定義,除非它包含 TRUNCATED 的值。|  
|SQL_DATA_TYPE (ODBC 3.0)|15|Smallint 非 NULL|SQL 資料類型的值,如它在描述符的SQL_DESC_TYPE欄位中顯示的。 此列與DATA_TYPE列相同,但日期時間和間隔數據類型除外。<br /><br /> 對於日期時間和間隔數據類型,結果集中的SQL_DATA_TYPE欄位將返回SQL_INTERVAL或SQL_DATETIME,SQL_DATETIME_SUB欄位將返回特定間隔或日期時間數據類型的子代碼。 ( 參見[附錄 D:資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|16|Smallint|日期時間和間隔數據類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|17|整數|字元或二進位數據類型列的最大長度(以位元組為單位)。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|ORDINAL_POSITION (ODBC 3.0)|18|整數不是 NULL|對於輸入和輸出參數,參數在過程定義中的序形位置(按增加參數順序,從 1 開始)。 對於返回值(如果有),返回 0。 對於結果集列,在結果集中的列的定位位置,結果集中的第一列為數位 1。 如果存在多個結果集,則以特定於驅動程式的方式返回列序形位置。|  
|IS_NULLABLE (ODBC 3.0)|19|Varchar|如果列不包含 NUL,則為"否"。<br /><br /> 如果列可以包含 NUL,則為"是"。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> 這個資料行的傳回值不同於 NULLABLE 資料行的傳回值。 (請參閱 NULLABLE 列的說明。|  
  
## <a name="code-example"></a>程式碼範例  
 請參考[過程呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料來源中的過程清單|[SQLProcedures 函數](../../../odbc/reference/syntax/sqlprocedures-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
