---
description: SQLMoreResults 函數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a23d806c1367636bc92a4a36b271d8d231070a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428930"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLMoreResults** 會判斷包含 **SELECT**、 **UPDATE**、 **INSERT**或 **DELETE** 語句的語句是否有更多結果，如果是，則會初始化這些結果的處理。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_NO_DATA、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLMoreResults**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLMoreResults** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01S02|選項值已變更|當正在處理批次時，語句屬性的值已變更。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|40001|序列化失敗|因為另一個交易發生資源鎖死，所以已回復交易。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 已**呼叫 SQLMoreResults**函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後，在*StatementHandle*上再次呼叫**SQLMoreResults**函數。<br /><br /> 已**呼叫 SQLMoreResults**函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒呼叫*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLMoreResults** 函式時，仍在執行此非同步函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 **SELECT** 語句會傳回結果集。 **UPDATE**、 **INSERT**和 **DELETE** 語句會傳回受影響資料列的計數。 如果批次處理這些語句中的任何一項，則會以參數陣列的形式提交 (以遞增的參數順序來排序、依它們出現在批次) 中的順序，或在程式中，它們可以傳回多個結果集或資料列計數。 如需有關語句和參數陣列的詳細資訊，請參閱 [SQL 語句的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md) 和 [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 執行批次之後，應用程式會置於第一個結果集上。 應用程式可以在第一個或任何後續的結果集上呼叫 **SQLBindCol**、 **SQLBulkOperations**、 **SQLFetch**、 **SQLGetData**、 **SQLFetchScroll**、 **SQLSetPos**和所有中繼資料函式，就像只有單一結果集一樣。 完成第一個結果集之後，應用程式會呼叫 **SQLMoreResults** ，以移至下一個結果集。 如果有另一個結果集或計數可用， **SQLMoreResults** 會傳回 SQL_SUCCESS，並初始化結果集或計數以進行其他處理。 如果任何資料列計數產生的語句出現在結果集產生的語句之間，則可以藉由呼叫**SQLMoreResults**來進行。針對**UPDATE**、 **INSERT**或**DELETE**語句呼叫**SQLMoreResults**之後，應用程式就可以呼叫**SQLRowCount**。  
  
 如果目前的結果集具有 unfetched 資料列， **SQLMoreResults** 會捨棄該結果集，並讓下一個結果集或計數可供使用。 如果已處理所有結果， **SQLMoreResults** 會傳回 SQL_NO_DATA。 針對某些驅動程式，在所有結果集和資料列計數都經過處理之後，才可以使用輸出參數和傳回值。 針對這類驅動程式，當 **SQLMoreResults** 傳回 SQL_NO_DATA 時，輸出參數和傳回值就會變成可用。  
  
 針對先前的結果集所建立的任何系結仍會保持有效。 如果這個結果集的資料行結構不同，則呼叫 **SQLFetch** 或 **SQLFetchScroll** 可能會導致錯誤或截斷。 若要避免這種情況，應用程式必須呼叫 **SQLBindCol** ，以明確地 (重新系結，或藉由將描述項欄位設定) 來進行。 或者，應用程式可以使用 SQL_UNBIND 的*選項*來呼叫**SQLFreeStmt** ，以解除系結所有資料行緩衝區。  
  
 語句屬性的值（例如資料指標類型、資料指標並行、索引鍵集大小或最大長度）可能會隨著應用程式透過呼叫 **SQLMoreResults**來流覽批次而變更。 如果發生這種情況， **SQLMoreResults** 會傳回 SQL_SUCCESS_WITH_INFO，而 SQLSTATE 01S02 (選項值已變更) 。  
  
 使用 SQL_CLOSE 的*選項*來呼叫**SQLCloseCursor**或**SQLFreeStmt** ，將會捨棄因為批次執行結果而提供的所有結果集和資料列計數。 語句控制碼會回到已配置或已備妥的狀態。 呼叫 **SQLCancel** 來取消非同步執行的函式（當批次已執行，且語句控制碼處於執行中、資料指標定位或非同步狀態時），會導致當取消呼叫成功時，會捨棄批次所產生的所有結果集和資料列計數。 然後，語句會回到已備妥或已配置的狀態。  
  
 如果一批語句或程式將其他 SQL 語句與 **SELECT**、 **UPDATE**、 **INSERT**和 **DELETE** 語句混合，則這些其他語句不會影響 **SQLMoreResults**。  
  
 如需詳細資訊，請參閱 [多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果在語句批次中搜尋的 update、insert 或 delete 語句不會影響資料來源中的任何資料列， **SQLMoreResults** 就會傳回 SQL_SUCCESS。 這與搜尋的 update、insert 或 delete 語句的案例不同，它會透過 **SQLExecDirect**、 **SQLExecute**或 **SQLParamData**來執行，如果它不會影響資料來源中的任何資料列，則會傳回 SQL_NO_DATA。 如果應用程式在呼叫**SQLMoreResults**時，呼叫**SQLRowCount**來取得資料列計數，並不會影響任何資料列，則**SQLRowCount**會傳回 SQL_NO_DATA。  
  
 如需有關結果處理函數之有效排序的詳細資訊，請參閱 [附錄 B： ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需 SQL_PARAM_DATA_AVAILABLE 和資料流程輸出參數的詳細資訊，請參閱 [使用 SQLGetData 來抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>資料列計數的可用性  
 當批次包含多個連續資料列計數產生的語句時，這些資料列計數可能只會匯總成一個資料列計數。 例如，如果批次有五個 insert 語句，則某些資料來源可以傳回五個個別的資料列計數。 某些其他資料來源只會傳回一個資料列計數，代表五個個別資料列計數的總和。  
  
 當批次包含結果集產生和資料列計數產生語句的組合時，資料列計數可能會或可能完全無法使用。 有關資料列計數可用性的驅動程式行為是透過呼叫 **SQLGetInfo**提供的 SQL_BATCH_ROW_COUNT 資訊類型來列舉。 例如，假設批次包含 **SELECT**，後面接著兩個 **INSERT**和另一個 **select**。 之後可能會發生下列情況：  
  
-   目前無法使用對應至兩個 **INSERT** 語句的資料列計數。 第一次呼叫 **SQLMoreResults** 時，會將您放在第二個 **SELECT** 語句的結果集上。  
  
-   分別提供對應至兩個 **INSERT** 語句的資料列計數。  (對 **SQLGetInfo** 的呼叫不會傳回 SQL_BATCH_ROW_COUNT 資訊類型的 SQL_BRC_ROLLED_UP 位。 ) **SQLMoreResults** 的第一個呼叫會將您定位到第一個 **插入**的資料列計數，而第二個呼叫會將您定位到第二個 **插入**的資料列計數。 第三次呼叫 **SQLMoreResults** 時，會將您放在第二個 **SELECT** 語句的結果集上。  
  
-   對應至兩個 **插入** 的資料列計數會匯總成一個可用的單一資料列計數。  (對 **SQLGetInfo** 的呼叫會傳回 SQL_BATCH_ROW_COUNT 資訊類型的 SQL_BRC_ROLLED_UP 位。 ) **SQLMoreResults** 的第一個呼叫會將您定位於匯總的資料列計數，而 **SQLMoreResults** 的第二個呼叫會將您定位到第二個 **SELECT**的結果集。  
  
 某些驅動程式讓資料列計數只適用于明確批次，而非預存程式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取部分或全部資料行|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
