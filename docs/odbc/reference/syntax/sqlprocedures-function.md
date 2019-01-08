---
title: SQLProcedures 函式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 260406eddd6caef88035376a764c3e140547e6c4
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204667"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLProcedures**傳回儲存在特定資料來源中的程序名稱的清單。 *程序*是泛型的詞彙，用來描述*可執行物件*，或 具名的實體，可以使用輸入和輸出參數來叫用。 如需有關程序的詳細資訊，請參閱[程序](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *CatalogName*  
 [輸入]程序的目錄。 如果驅動程式支援的目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有目錄的資料表。 *CatalogName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*CatalogName*是一般的引數; 也就是，則會視為和其案例很重要。 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]中的字元長度 **CatalogName*。  
  
 *SchemaName*  
 [輸入]程序結構描述名稱的字串搜尋模式。 如果驅動程式支援的結構描述，對於某些程序，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示這些程序，並沒有結構描述。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *SchemaName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*SchemaName*模式值引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength2*  
 [輸入]中的字元長度 **SchemaName*。  
  
 *ProcName*  
 [輸入]程序名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *ProcName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*ProcName*模式值引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength3*  
 [輸入]中的字元長度 **ProcName*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLProcedures**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLProcedures** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|資料指標是開啟*StatementHandle*，並**SQLFetch**或是**SQLFetchScroll**呼叫。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標是開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*引數為 null 指標，以及 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*SchemaName*或是*ProcName*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 仍在呼叫此函式時執行此非同步函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 其中一個名稱的長度引數的值小於 0，但不是等於 SQL_NTS。<br /><br /> 其中一個名稱的長度引數的值超過最大長度值，對應的名稱。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定程序類別目錄，並在驅動程式或資料來源不支援目錄。<br /><br /> 指定程序結構描述，且驅動程式或資料來源不支援結構描述。<br /><br /> 程序結構描述或程序名稱所指定的字串搜尋模式和資料來源不支援搜尋模式的一個或多個這些引數。<br /><br /> 驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLProcedures**列出要求的範圍中的所有程序。 使用者可能會或可能沒有執行任何這些程序的權限。 若要檢查協助工具，應用程式可以呼叫**SQLGetInfo**並檢查 SQL_ACCESSIBLE_PROCEDURES 資訊值。 否則，應用程式必須能夠處理的情況下，使用者在選取的程序，它無法執行。 如需如何使用這項資訊，請參閱[程序](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLProcedures**標準的結果集，依 PROCEDURE_CAT、 PROCEDURE_SCHEMA 和程序名稱來排序的方式傳回結果。  
  
> [!NOTE]  
>  **SQLProcedures**可能不會傳回所有的程序。 應用程式可以使用任何有效的程序，不論它會傳回所**SQLProcedures**。  
  
 下列資料行已重新命名為 ODBC 3 *.x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3 *.x*資料行|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|程序 _OWNER|程序 _SCHEM|  
  
 若要判斷 PROCEDURE_CAT、 PROCEDURE_SCHEM 和程序名稱的資料行的實際長度，應用程式可以呼叫**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN、 與 SQL_MAX_SCHEMA_NAME_LEN，SQL_MAX_PROCEDURE_NAME_LEN 選項。  
  
 下表列出結果集內的資料行。 驅動程式，可以定義資料行 8 (PROCEDURE_TYPE) 以外的其他資料行。 應用程式應該取得存取權的驅動程式特有的資料行，倒數，從結果集的結尾，而不是指定明確的序數位置。 如需詳細資訊，請參閱 <<c0> [ 目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0)|1|Varchar|程序類別目錄識別碼;如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些程序，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 沒有目錄這些程序。|  
|PROCEDURE_SCHEM (ODBC 2.0)|2|Varchar|程序結構描述識別碼;如果不適用於資料來源，則為 NULL。 如果驅動程式支援結構描述對於某些程序，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 並沒有結構描述的程序。|  
|程序名稱 (ODBC 2.0)|3|非 NULL Varchar|程序識別碼。|  
|NUM_INPUT_PARAMS (ODBC 2.0)|4|N/A|保留供日後使用。 應用程式不應依賴這些結果資料行中傳回的資料。|  
|NUM_OUTPUT_PARAMS (ODBC 2.0)|5|N/A|保留供日後使用。 應用程式不應依賴這些結果資料行中傳回的資料。|  
|NUM_RESULT_SETS (ODBC 2.0)|6|N/A|保留供日後使用。 應用程式不應依賴這些結果資料行中傳回的資料。|  
|註解 (ODBC 2.0)|7|Varchar|程序的描述。|  
|PROCEDURE_TYPE (ODBC 2.0)|8|Smallint|定義的程序類型：<br /><br /> SQL_PT_UNKNOWN:無法判斷此程序是否會傳回值。<br /><br /> SQL_PT_PROCEDURE:傳回的物件是一個程序;也就是說，它並沒有傳回值。<br /><br /> 會：傳回的物件是函式;也就是說，它具有傳回值。|  
  
 *SchemaName*並*ProcName*引數接受搜尋模式。 如需有關有效的搜尋模式的詳細資訊，請參閱[模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|擷取單一資料列或順向方向中的資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回的驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|傳回參數和結果集的程序的資料行|[SQLProcedureColumns 函式](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|叫用預存程序的語法|[執行陳述式](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
