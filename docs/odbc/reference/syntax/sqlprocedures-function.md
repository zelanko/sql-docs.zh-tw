---
title: SQL程式功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLProcedures
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLProcedures
helpviewer_keywords:
- SQLProcedures function [ODBC]
ms.assetid: d0d9ef10-2fd4-44a5-9334-649f186f4ba0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4c8b8a9f22f6005d1af811e56485299bad3a425
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306839"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQL過程**傳回存儲在特定資料來源中的過程名稱清單。 *過程*是一個通用術語,用於描述*可執行物件*,或可以使用輸入和輸出參數呼叫的命名實體。 有關程式的詳細資訊,請參閱[過程](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLProcedures(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      ProcName,  
     SQLSMALLINT    NameLength3);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *目錄名稱*  
 [輸入]過程目錄。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),空字串("")表示那些沒有目錄的表。 *目錄名稱*不能包含字串搜尋模式。  
  
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
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQL 程式**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該*操作類型*為 SQL_HANDLE_STMT 和*敘述的句柄*。 *Handle* 下表列出了 SQLProcess 通常返回的**SQLSTATE**值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|語句*處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*目錄名稱*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID敘述屬性設定為SQL_TRUE,*而 SchemaName*或*ProcName*參數是空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用此函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 其中一個名稱長度參數的值小於 0,但不等於SQL_NTS。<br /><br /> 其中一個名稱長度參數的值超過相應名稱的最大長度值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了過程目錄,驅動程式或數據源不支援目錄。<br /><br /> 已指定過程架構,驅動程式或數據源不支援架構。<br /><br /> 為過程架構或過程名稱指定了字串搜索模式,數據源不支援一個或多個這些參數的搜索模式。<br /><br /> 驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回請求的結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援此功能。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQL程式**列出了請求範圍內的所有過程。 使用者可能或可能沒有執行這些過程的許可權。 要檢查輔助功能,應用程式可以調用**SQLGetInfo**並檢查SQL_ACCESSIBLE_PROCEDURES資訊值。 否則,應用程式必須能夠處理使用者選擇無法執行的過程的情況。 有關如何使用此資訊的資訊,請參閱[過程](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQL程式**將結果作為標準結果集返回,由PROCEDURE_CAT、PROCEDURE_SCHEMA和PROCEDURE_NAME排序。  
  
> [!NOTE]  
>  **SQL 程式**可能不會返回所有過程。 應用程式可以使用任何有效的過程,而不管它是否由**SQLProcess**返回。  
  
 以下列已重新命名為 ODBC 3 *.x*。 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC 3 *.x*欄|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|程式_OWNER|程式_SCHEM|  
  
 要確定PROCEDURE_CAT、PROCEDURE_SCHEM和PROCEDURE_NAME列的實際長度,應用程式可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN和SQL_MAX_PROCEDURE_NAME_LEN選項調用**SQLGetInfo。**  
  
 下表列出了結果集中的列。 驅動程式可以定義第 8 列(PROCEDURE_TYPE)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|過程目錄標識碼;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些過程的目錄,但不支援其他過程的目錄(例如當驅動程式從不同的 DBMS 檢索數據時),它將返回一個空字串(""),用於那些沒有目錄的過程。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|過程架構標識碼;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些過程的架構,但不支援其他過程的架構(例如當驅動程式從不同的 DBMS 檢索數據時),它將返回一個空字串(""),用於那些沒有架構的過程。|  
|PROCEDURE_NAME (ODBC 2.0)|3|瓦爾查爾不是 NULL|過程標識碼。|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/A|保留供未來使用。 應用程式不應依賴於這些結果列中返回的數據。|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/A|保留供未來使用。 應用程式不應依賴於這些結果列中返回的數據。|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/A|保留供未來使用。 應用程式不應依賴於這些結果列中返回的數據。|  
|備註 (ODBC 2.0)|7|Varchar|過程的說明。|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|定義程序類型:<br /><br /> SQL_PT_UNKNOWN:無法確定過程是否返回值。<br /><br /> SQL_PT_PROCEDURE:返回的對像是一個過程;也就是說,它沒有返回值。<br /><br /> SQL_PT_FUNCTION:返回的對像是函數;也就是說,它有一個返回值。|  
  
 *架構名稱*和*ProcName*參數接受搜尋模式。 關於有效搜尋模式的詳細資訊,請參考[模式值參數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[過程呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回關於驅動程式或資料來源的資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|傳回程序的參數與結果集列|[SQLProcedureColumns 函式](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|除除存程序的語法|[執行陳述式](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
