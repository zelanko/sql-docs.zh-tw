---
title: SQLMoreResults 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1905665f1505cd484a6d2ab5c1f83008efc2298
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlmoreresults-function"></a>SQLMoreResults 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ODBC  
  
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
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_NO_DATA、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLMoreResults**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLMoreResults** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02 的警告|選項值已變更|處理變更批次陳述式屬性的值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|40001|序列化失敗|交易已回復由於與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法決定交易的狀態。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 **SQLMoreResults**呼叫函式和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*. 然後在**SQLMoreResults**上一次呼叫函式*StatementHandle*。<br /><br /> **SQLMoreResults**呼叫函式和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒在多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLMoreResults**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **選取**陳述式會傳回結果集。 **更新**，**插入**，和**刪除**陳述式會傳回受影響的資料列計數。 如果任何這些陳述式會批次處理，提交具有陣列參數 （以遞增順序排列的參數，批次中出現的順序編號），或在程序，它們可以傳回多個結果集或資料列計數。 陳述式的批次和參數陣列的相關資訊，請參閱[批次的 SQL 陳述式](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 在執行批次之後, 應用程式位於第一個結果集。 應用程式可以呼叫**SQLBindCol**， **SQLBulkOperations**， **SQLFetch**， **SQLGetData**， **SQLFetchScroll**， **SQLSetPos**，所有中繼資料函式，第一次或任何後續的結果集，就只是單一結果集時一樣。 一旦透過第一個結果集，應用程式就會呼叫**SQLMoreResults**移至下一個結果集。 如果另一個結果集或計數，則**SQLMoreResults**都會傳回 SQL_SUCCESS，並初始化的結果集或進行其他處理的計數。 如果任何資料列計數 – 產生陳述式出現在其間結果集-產生的陳述式，依呼叫逐步執行**SQLMoreResults**。在呼叫**SQLMoreResults**如**更新**，**插入**，或**刪除**陳述式，應用程式可以呼叫**SQLRowCount**。  
  
 如果沒有目前未提取資料列結果集， **SQLMoreResults**會捨棄該結果集，並讓下一個結果集，或計算可用。 如果已處理所有結果， **SQLMoreResults**傳回 sql_no_data 為止。 有些驅動程式中，輸出參數和傳回值不可以使用的直到處理所有結果集和資料列計數。 這類的驅動程式的輸出參數和傳回值變成可用時**SQLMoreResults**傳回 sql_no_data 為止。  
  
 任何繫結所建立的前一個結果集仍保持有效。 如果資料行結構不同，此結果集，然後呼叫**SQLFetch**或**SQLFetchScroll**可能會導致錯誤或截斷。 若要防止這個情況，應用程式必須呼叫**SQLBindCol**明確地視需要重新繫結 （或可以透過設定描述項欄位）。 或者，應用程式可以呼叫**SQLFreeStmt**與*選項*SQL_UNBIND 解除繫結的所有資料行緩衝區。  
  
 應用程式巡覽至呼叫批次的陳述式屬性，例如資料指標類型、 資料指標並行、 索引鍵集大小或最大長度，值可能會變更**SQLMoreResults**。 如果發生這種情況， **SQLMoreResults**會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。  
  
 呼叫**SQLCloseCursor**，或**SQLFreeStmt**與*選項*的 SQL_CLOSE，就會捨棄所有結果集和可用的執行結果的資料列計數批次。 陳述式控制代碼傳回至配置或已備妥狀態。 呼叫**SQLCancel**取消非同步執行的函式已經執行批次陳述式控制代碼會在執行資料指標定位或非同步狀態會導致所有都結果集和資料列計數如果取消 5d; 呼叫成功，正在捨棄批次產生。 然後，陳述式傳回的備妥或已配置的狀態。  
  
 如果批次陳述式或程序中混合其他 SQL 陳述式與**選取**，**更新**，**插入**，和**刪除**陳述式，這些陳述式不會影響**SQLMoreResults**。  
  
 如需詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果搜尋的 update、 insert 或 delete 陳述式中的陳述式批次不會影響資料來源的任何資料列**SQLMoreResults**都會傳回 SQL_SUCCESS。 這是不同的大小寫的搜尋更新、 插入或刪除陳述式執行時透過**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，如果它不會影響任何資料列在資料來源會傳回 sql_no_data 為止。 如果應用程式呼叫**SQLRowCount**呼叫之後擷取的資料列計數**SQLMoreResults**不受影響任何資料列， **SQLRowCount**會傳回 sql_no_data 為止。  
  
 如需有關有效排序的結果處理函式，請參閱[附錄 b: ODBC 狀態轉換表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 如需 SQL_PARAM_DATA_AVAILABLE 和資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="availability-of-row-counts"></a>資料列計數的可用性  
 當批次包含多個連續的資料列計數 – 產生陳述式時，很可能在這些資料列數會彙總到一個資料列計數。 例如，如果批次具有五個 insert 陳述式，則某些資料來源必須能夠傳回五個個別的資料列計數。 特定資料來源傳回只有一個資料列計數，表示五個個別的資料列計數的總和。  
  
 當批次包含結果集： 產生和資料列計數-產生的陳述式的組合時，資料列計數可能會或可能無法完全。 相對於資料列計數的可用性驅動程式的行為會列舉在 SQL_BATCH_ROW_COUNT 類型資訊，可透過呼叫**SQLGetInfo**。 例如，假設 批次包含**選取**，後面緊接著兩個**插入**s，而另一個**選取**。 然後可能會在下列情況：  
  
-   資料列計數對應到兩個**插入**陳述式完全不使用。 第一次呼叫**SQLMoreResults**會放在第二個結果集上**選取**陳述式。  
  
-   資料列計數對應到兩個**插入**陳述式會個別使用。 (呼叫**SQLGetInfo**不會傳回 SQL_BATCH_ROW_COUNT 資訊類型的 SQL_BRC_ROLLED_UP 位元。)第一次呼叫**SQLMoreResults**會放在第一個資料列計數**插入**，第二個呼叫會將您放在第二個資料列計數和**插入**。 第三個呼叫**SQLMoreResults**會放在第二個結果集上**選取**陳述式。  
  
-   資料列計數對應到兩個**插入**成一個可用的單一資料列計數彙總。 (呼叫**SQLGetInfo**傳回 SQL_BATCH_ROW_COUNT 資訊類型的位元 SQL_BRC_ROLLED_UP。)第一次呼叫**SQLMoreResults**會放在彙總資料列計數和第二個呼叫**SQLMoreResults**會放在第二個結果集上**選取**.  
  
 特定驅動程式提供資料列計數只能用於明確的批次，不能用於預存程序。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取單一資料列或資料區塊的順向的方向|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|擷取部分或全部的資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
  
## <a name="see-also"></a>請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
