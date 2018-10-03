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
manager: craigg
ms.openlocfilehash: c26111571eb505640acee035cba37d617b43c481
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849936"
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函數
**合規性**  
 版本導入： ODBC 1.0 標準相容性： ODBC  
  
 **摘要**  
 **SQLMoreResults**判斷是否可以使用在上一個陳述式，其中包含更多結果**選取**，**更新**，**插入**，或**刪除**陳述式和初始化若是如此，處理這些結果。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLMoreResults(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE，還是 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLMoreResults**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLMoreResults** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|正在處理的變更視為批次陳述式屬性值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 **SQLMoreResults**呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*. 然後**SQLMoreResults**在上一次呼叫函式*StatementHandle*。<br /><br /> **SQLMoreResults**呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒，多執行緒應用程式中。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLMoreResults**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **選取**陳述式會傳回結果集。 **更新**，**插入**，以及**刪除**陳述式會傳回受影響的資料列計數。 如果任何這些陳述式的批次處理送出陣列的參數 （以遞增的參數順序，批次中出現的順序編號），或在程序中，它們可以傳回多個結果集或資料列計數。 陳述式的批次和參數陣列的相關資訊，請參閱[批次的 SQL 陳述式](../../../odbc/reference/develop-app/batches-of-sql-statements.md)並[參數值的陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 執行批次之後, 應用程式位於第一個結果集。 應用程式可以呼叫**SQLBindCol**， **SQLBulkOperations**， **SQLFetch**， **SQLGetData**， **SQLFetchScroll**， **SQLSetPos**，所有中繼資料函式，第一個或任何後續的結果集，就像它就只是單一結果集一樣。 一旦完成第一個結果集，應用程式會呼叫**SQLMoreResults**移至下一個結果集。 如果另一個結果集或計數，則**SQLMoreResults**都會傳回 SQL_SUCCESS，並初始化的結果集或進行其他處理的計數。 如果任何資料列計數 – 產生陳述式出現在結果集-產生的陳述式，請依呼叫逐步執行**SQLMoreResults**。之後呼叫**SQLMoreResults** for**更新**，**插入**，或**刪除**陳述式中，應用程式可以呼叫**SQLRowCount**。  
  
 如果沒有目前未提取資料列結果集， **SQLMoreResults**會捨棄該結果集，並讓下一個結果集，或計算可用。 如果已處理所有結果， **SQLMoreResults**傳回 sql_no_data 為止。 有些驅動程式，為輸出參數和傳回值無法使用。 直到已經處理所有結果集和資料列計數 這類驅動程式中，輸出參數和傳回值變成可用時**SQLMoreResults**傳回 sql_no_data 為止。  
  
 任何繫結所建立的前一個結果集仍保持有效。 如果資料行結構不同，此結果集，然後呼叫**SQLFetch**或是**SQLFetchScroll**可能會導致錯誤或截斷。 若要避免這個問題，應用程式必須呼叫**SQLBindCol**明確地視需要重新繫結 （或設定描述項欄位）。 或者，應用程式可以呼叫**SQLFreeStmt**具有*選項*SQL_UNBIND 解除繫結所有資料行緩衝區。  
  
 應用程式巡覽至呼叫批次的陳述式屬性，例如資料指標類型、 資料指標並行、 索引鍵集大小或最大長度，值可能會變更**SQLMoreResults**。 如果發生這種情況**SQLMoreResults**會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。  
  
 呼叫**SQLCloseCursor**，或**SQLFreeStmt**具有*選項*的 SQL_CLOSE，捨棄所有結果集和可用的執行結果的資料列計數批次。 陳述式控制代碼所傳回的已配置或已備妥的狀態。 呼叫**SQLCancel**取消非同步執行的函式，當批次已經執行陳述式控制代碼中執行，資料指標位置，或非同步狀態中的所有結果集產生且資料列計數如果成功取消呼叫被丟棄批次產生。 然後，陳述式傳回的已備妥或已配置的狀態。  
  
 如果批次陳述式或程序中混合使用其他 SQL 陳述式**選取 **，**更新**，**插入**，以及**刪除**陳述式，這些陳述式不會影響**SQLMoreResults**。  
  
 如需詳細資訊，請參閱 <<c0> [ 多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果搜尋 update、 insert 或 delete 陳述式在批次陳述式不會影響資料來源，在任何資料列**SQLMoreResults**都會傳回 SQL_SUCCESS。 這點不同於大小寫的搜尋更新、 插入或刪除透過執行陳述式**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，如果它不會影響在資料來源的任何資料列，則傳回 sql_no_data 為止。 如果應用程式呼叫**SQLRowCount**在呼叫之後擷取的資料列計數**SQLMoreResults**具有不受影響的任何資料列， **SQLRowCount**會傳回 sql_no_data 為止。  
  
 如需有關有效的排序結果處理函式的詳細資訊，請參閱[附錄 b: ODBC 狀態轉換資料表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需有關 SQL_PARAM_DATA_AVAILABLE 和資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>資料列計數的可用性  
 當批次包含多個連續的資料列計數 – 產生陳述式時，就可以在這些資料列計數會彙總，到只在一個資料列計數。 比方說，如果批次中有五個 insert 陳述式，則某些資料來源是能夠傳回五個個別的資料列計數。 特定資料來源傳回只有一個資料列計數，表示五個個別的資料列計數的總和。  
  
 當批次包含結果集 – 產生和資料列計數-產生的陳述式的組合時，資料列計數可能會或可能無法完全。 相對於資料列計數的可用性驅動程式的行為會列舉在 SQL_BATCH_ROW_COUNT 資訊類型，可透過呼叫**SQLGetInfo**。 例如，假設 批次包含**選取 **，後面兩個**插入**s，而另一個**選取**。 下列情況下便可以：  
  
-   資料列計數對應到兩個**插入**陳述式完全不提供。 第一次呼叫**SQLMoreResults**放置您的第二個結果集上**選取**陳述式。  
  
-   資料列計數對應到兩個**插入**陳述式會個別提供。 (呼叫**SQLGetInfo**不會傳回 SQL_BRC_ROLLED_UP 位元 SQL_BATCH_ROW_COUNT 資訊類型。)第一次呼叫**SQLMoreResults**將會置於您的第一個資料列計數**插入**，和第二次呼叫會將您放在第二個資料列計數**插入**。 第三個呼叫**SQLMoreResults**放置您的第二個結果集上**選取**陳述式。  
  
-   資料列計數對應到兩個**插入**會彙總成一個單一資料列計數所提供。 (呼叫**SQLGetInfo**傳回 SQL_BATCH_ROW_COUNT 資訊類型的位元 SQL_BRC_ROLLED_UP。)第一次呼叫**SQLMoreResults**放置您彙總資料列計數和第二個呼叫上**SQLMoreResults**放置您的第二個結果集上**選取**.  
  
 特定驅動程式提供資料列計數只會針對明確的批次，不能用於預存程序。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取單一資料列或順向方向中的資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|正在擷取部分或全部的資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
