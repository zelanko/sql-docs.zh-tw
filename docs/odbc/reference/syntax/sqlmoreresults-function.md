---
title: SQLMoreResults 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLMoreResults
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLMoreResults
helpviewer_keywords:
- SQLMoreResults function [ODBC]
ms.assetid: bf169ed5-4d55-412c-b184-12065a726e89
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3ca7ed4f6bbcd31b8f67b95dc14a2c6c301b5a59
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138833"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLMoreResults**會判斷包含**SELECT**、 **UPDATE**、 **INSERT**或**DELETE**語句的語句是否有更多結果可供使用，如果是的話，則會初始化這些結果的處理。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLMoreResults**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLMoreResults**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|語句屬性的值在處理批次時變更。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死，所以交易已回復。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已**呼叫 SQLMoreResults**函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫**SQLMoreResults**函式。<br /><br /> 已**呼叫 SQLMoreResults**函式，在完成執行之前，會從多執行緒應用程式中的不同執行緒呼叫*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLMoreResults**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 **SELECT**語句會傳回結果集。 **UPDATE**、 **INSERT**和**DELETE**語句會傳回受影響的資料列計數。 如果其中任何一個語句是批次、以參數陣列（以遞增的參數順序編號，依其出現在批次中的順序），或在程式中提交，它們可以傳回多個結果集或資料列計數。 如需有關語句的批次和參數陣列的詳細資訊，請參閱[SQL 語句的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[參數值的陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 執行批次之後，應用程式會位於第一個結果集上。 應用程式可以在第一個或任何後續的結果集上呼叫**SQLBindCol**、 **SQLBulkOperations**、 **SQLFetch**、 **SQLGetData**、 **SQLFetchScroll**、 **SQLSetPos**和所有中繼資料函數，就像只有單一結果集一樣。 當第一個結果集完成後，應用程式會呼叫**SQLMoreResults** ，以移至下一個結果集。 如果有其他結果集或計數可供使用， **SQLMoreResults**會傳回 SQL_SUCCESS 並初始化結果集或計數以進行其他處理。 如果任何資料列計數產生的語句出現在結果集產生的語句之間，可以藉由呼叫**SQLMoreResults**來進行。在呼叫**UPDATE**、 **INSERT**或**DELETE**語句的**SQLMoreResults**之後，應用程式就可以呼叫**SQLRowCount**。  
  
 如果目前的結果集具有 unfetched 的資料列， **SQLMoreResults**會捨棄該結果集，並讓下一個結果集或計數可供使用。 如果所有結果都已處理，則**SQLMoreResults**會傳回 SQL_NO_DATA。 對於某些驅動程式，在處理所有結果集和資料列計數之前，無法使用輸出參數和傳回值。 針對這類驅動程式，當**SQLMoreResults**傳回 SQL_NO_DATA 時，輸出參數和傳回值就會變成可用。  
  
 針對先前的結果集所建立的任何系結仍會保持有效。 如果此結果集的資料行結構不同，則呼叫**SQLFetch**或**SQLFetchScroll**可能會導致錯誤或截斷。 為了避免這種情況，應用程式必須呼叫**SQLBindCol**來明確地重新系結（或藉由設定描述項欄位來這麼做）。 或者，應用程式可以使用 SQL_UNBIND 的*選項*來呼叫**SQLFreeStmt** ，以解除系結所有的資料行緩衝區。  
  
 語句屬性的值（例如資料指標類型、資料指標並行、索引鍵集大小或最大長度）可能會隨著應用程式透過呼叫**SQLMoreResults**而流覽批次而變更。 如果發生這種情況， **SQLMoreResults**會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。  
  
 使用 SQL_CLOSE 的*選項*呼叫**SQLCloseCursor**或**SQLFreeStmt** ，會捨棄執行批次後所提供的所有結果集和資料列計數。 語句控制碼會回到已配置或備妥的狀態。 呼叫**SQLCancel**在批次已執行且語句控制碼處於執行中、資料指標位置或非同步狀態時，取消非同步執行的函式，會導致在取消呼叫成功時，將會捨棄批次所產生的所有結果集和資料列計數。 然後，語句會回到備妥或已配置的狀態。  
  
 如果語句批次或程式與**SELECT**、 **UPDATE**、 **INSERT**和**DELETE**語句混合使用其他 SQL 語句，這些其他語句就不會影響**SQLMoreResults**。  
  
 如需詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果在語句批次中搜尋的 update、insert 或 delete 語句不會影響資料來源中的任何資料列， **SQLMoreResults**就會傳回 SQL_SUCCESS。 這與透過**SQLExecDirect**、 **SQLExecute**或**SQLParamData**執行之搜尋的 update、insert 或 delete 語句的大小寫不同，如果它不會影響資料來源中的任何資料列，則會傳回 SQL_NO_DATA。 如果應用程式在呼叫**SQLMoreResults**但不影響任何資料列後呼叫**SQLRowCount**來取得資料列計數，則**SQLRowCount**會傳回 SQL_NO_DATA。  
  
 如需結果處理函式之有效排序的詳細資訊，請參閱[附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需 SQL_PARAM_DATA_AVAILABLE 和資料流程輸出參數的詳細資訊，請參閱[使用 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>資料列計數的可用性  
 當批次包含多個連續的資料列計數產生語句時，這些資料列計數可能只會匯總成一個資料列計數。 例如，如果批次有五個 insert 語句，則某些資料來源就能夠傳回五個個別的資料列計數。 某些其他資料來源只會傳回一個代表五個個別資料列計數之總和的資料列計數。  
  
 當批次包含結果集產生和資料列計數產生語句的組合時，資料列計數可能完全無法使用。 與資料列計數可用性有關的驅動程式行為，會以透過**SQLGetInfo**呼叫提供的 SQL_BATCH_ROW_COUNT 資訊類型來列舉。 例如，假設批次包含**SELECT**，後面接著兩個**INSERT**和另一個**select**。 然後，可能會發生下列情況：  
  
-   目前無法使用對應到兩個**INSERT**語句的資料列計數。 第一次呼叫**SQLMoreResults**時，會將您定位在第二個**SELECT**語句的結果集上。  
  
-   對應至兩個**INSERT**語句的資料列計數可個別使用。 （對**SQLGetInfo**的呼叫不會傳回 SQL_BATCH_ROW_COUNT 資訊類型的 SQL_BRC_ROLLED_UP 位）。第一次呼叫**SQLMoreResults**時，會將您定位到第一個**插入**的資料列計數，而第二次呼叫會將您定位到第二個**插入**的資料列計數。 第三次呼叫**SQLMoreResults**時，會將您定位在第二個**SELECT**語句的結果集上。  
  
-   對應到這兩個**插入**的資料列計數會匯總成一個可用的單一資料列計數。 （呼叫**SQLGetInfo**會傳回 SQL_BATCH_ROW_COUNT 資訊類型的 SQL_BRC_ROLLED_UP 位）。第一次呼叫**SQLMoreResults**時，會將您定位在匯總的資料列計數上，而第二次呼叫**SQLMoreResults**時，會將您定位在第二個**SELECT**的結果集上。  
  
 某些驅動程式會使資料列計數僅適用于明確的批次，而不能用於預存程式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|正在提取部分或所有資料行|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
