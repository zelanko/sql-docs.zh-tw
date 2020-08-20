---
description: SQLProcedures 函數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c4e44a708f96883891d44d629fdd3c945eb283a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487144"
---
# <a name="sqlprocedures-function"></a>SQLProcedures 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLProcedures** 會傳回儲存在特定資料來源中的程式名稱清單。 *程式是* 用來描述可 *執行物件*的泛型詞彙，或可使用輸入和輸出參數叫用的命名實體。 如需有關程式的詳細資訊，請參閱 [程式](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
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
 *StatementHandle*  
 輸出語句控制碼。  
  
 *CatalogName*  
 輸出程式目錄。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示這些資料表沒有目錄。 *CatalogName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *CatalogName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *CatalogName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。 如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 輸出**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 輸出程式架構名稱的字串搜尋模式。 如果驅動程式支援某些程式的架構，但不支援其他程式的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示那些沒有架構的程式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *SchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *SchemaName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength2*  
 輸出**SchemaName*的長度（以字元為單位）。  
  
 *ProcName*  
 輸出程式名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *ProcName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *ProcName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength3*  
 輸出**ProcName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLProcedures**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLProcedures** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在 *StatementHandle*上開啟了資料指標，且已呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 如果 **SQLFetch** 或 **SQLFetchScroll** 尚未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果 **SQLFetch** 或 **SQLFetchScroll** 已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 在 *StatementHandle*上開啟了資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一個交易發生資源鎖死，所以已回復交易。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在 *StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效|SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE、 *CatalogName* 引數為 null 指標，且 SQL_CATALOG_NAME *InfoType* 會傳回支援的目錄名稱。<br /><br />  (DM) SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，且 *SchemaName* 或 *ProcName* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 這個非同步函式在呼叫此函式時仍在執行中。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個名稱長度引數的值超過對應名稱的最大長度值。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|已指定程式目錄，而驅動程式或資料來源不支援目錄。<br /><br /> 已指定程式架構，而驅動程式或資料來源不支援架構。<br /><br /> 為程式架構或程式名稱指定了字串搜尋模式，且資料來源不支援一或多個這些引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而且 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回要求的結果集之前過期。 Timeout 期限是透過 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 **SQLProcedures** 會列出要求範圍內的所有程式。 使用者不一定會擁有執行上述任何程式的許可權。 若要檢查協助工具，應用程式可以呼叫 **SQLGetInfo** 並檢查 SQL_ACCESSIBLE_PROCEDURES 資訊值。 否則，應用程式必須能夠處理使用者選取無法執行之程式的情況。 如需有關如何使用此資訊的詳細資訊，請參閱 [程式](../../../odbc/reference/develop-app/procedures-odbc.md)。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱 [目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLProcedures** 會以標準結果集的形式傳回結果，並依 PROCEDURE_CAT、PROCEDURE_SCHEMA 和 PROCEDURE_NAME 排序。  
  
> [!NOTE]  
>  **SQLProcedures** 可能不會傳回所有的程式。 應用程式可以使用任何有效的程式，無論 **SQLProcedures**是否傳回。  
  
 已重新命名 ODBC 3.x 的下列資料行 *。* 資料行名稱的變更不會影響回溯相容性，因為應用程式會依資料行編號進行系結。  
  
|ODBC 2.0 資料行|ODBC 3.x*資料行*|  
|---------------------|-----------------------|  
|PROCEDURE_QUALIFIER|PROCEDURE_CAT|  
|程式 _OWNER|程式 _SCHEM|  
  
 若要判斷 PROCEDURE_CAT、PROCEDURE_SCHEM 和 PROCEDURE_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_PROCEDURE_NAME_LEN 選項來呼叫 **SQLGetInfo** 。  
  
 下表列出結果集中的資料行。 資料行8以外的其他資料行 (PROCEDURE_TYPE) 可以由驅動程式定義。 應用程式應該從結果集的結尾算下，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱 [目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PROCEDURE_CAT (ODBC 2.0) |1|Varchar|程式目錄識別碼;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些程式的目錄，但不支援其他程式的目錄，例如，當驅動程式從不同的 Dbms 取得資料時，它會針對沒有目錄的那些程式傳回空字串 ( "" ) 。|  
|PROCEDURE_SCHEM (ODBC 2.0) |2|Varchar|程式架構識別碼;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些程式的架構，但不支援其他程式的架構，例如，當驅動程式從不同的 Dbms 取得資料時，它會針對沒有架構的程式傳回空字串 ( "" ) 。|  
|PROCEDURE_NAME (ODBC 2.0) |3|Varchar not Null|程式識別碼。|  
|NUM_INPUT_PARAMS (ODBC 2.0) |4|N/A|保留供未來使用。 應用程式不應依賴這些結果資料行所傳回的資料。|  
|NUM_OUTPUT_PARAMS (ODBC 2.0) |5|N/A|保留供未來使用。 應用程式不應依賴這些結果資料行所傳回的資料。|  
|NUM_RESULT_SETS (ODBC 2.0) |6|N/A|保留供未來使用。 應用程式不應依賴這些結果資料行所傳回的資料。|  
| (ODBC 2.0) 的備註|7|Varchar|程式的描述。|  
|PROCEDURE_TYPE (ODBC 2.0) |8|Smallint|定義程式類型：<br /><br /> SQL_PT_UNKNOWN：無法判斷程式是否傳回值。<br /><br /> SQL_PT_PROCEDURE：傳回的物件是程式;也就是說，它沒有傳回值。<br /><br /> SQL_PT_FUNCTION：傳回的物件是函數;也就是說，它有傳回值。|  
  
 *SchemaName*和*ProcName*引數接受搜尋模式。 如需有效搜尋模式的詳細資訊，請參閱 [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱 [程序呼叫](../../../odbc/reference/develop-app/procedure-calls.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回驅動程式或資料來源的相關資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|傳回程序的參數和結果集資料行|[SQLProcedureColumns 函式](../../../odbc/reference/syntax/sqlprocedurecolumns-function.md)|  
|叫用預存程式的語法|[執行陳述式](../../../odbc/reference/develop-app/executing-statements-odbc.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
