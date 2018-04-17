---
title: SQLEndTran 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- SQLEndTran
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ea99ca26105d3c31330108979a5b182329aa6ba5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlendtran-function"></a>SQLEndTran 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLEndTran**要求認可或復原作業的所有作用中的作業與連接相關聯的所有陳述式。 **SQLEndTran**也可以要求認可或復原作業會執行與環境相關聯的所有連線。  
  
> [!NOTE]  
>  如需有關哪些驅動程式管理員將此函式可對應時 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式，請參閱[對應取代函式的應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]控制代碼類型的識別項。 包含任一 SQL_HANDLE_ENV (如果*處理*環境的控制代碼) 或利用 SQL_HANDLE_DBC (如果*處理*連接控制代碼)。  
  
 *Handle*  
 [輸入]所指定的類型的控制代碼， *HandleType*，指出在交易範圍。 如需詳細資訊，請參閱 「 註解 」。  
  
 *CompletionType*  
 [輸入]下列兩個值之一：  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLEndTran**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**適當*HandleType*和*處理*。 下表列出通常所傳回的 SQLSTATE 值**SQLEndTran** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連線。|(DM) *HandleType*已利用 SQL_HANDLE_DBC，而*處理*不是處於連線狀態。|  
|08007|在交易期間的連線失敗|*HandleType*已利用 SQL_HANDLE_DBC，並連接相關聯*處理*函式，執行期間失敗，而且無法判斷是否要求**認可**或**復原**失敗前發生。|  
|25S01|未知的交易狀態|一或多個連線中*處理*無法完成交易，且指定，其結果，結果不明。|  
|25S02|交易是仍在作用中|驅動程式無法保證以不可分割方式，完成所有工作中的全域交易，且交易仍在作用中。|  
|25S03|交易回復|驅動程式無法保證以不可分割方式，完成所有工作中的全域交易，且所有工作中的使用中交易*處理*已回復。|  
|40001|序列化失敗|交易已回復由於與另一個交易資源鎖死。|  
|40002|完整性條件約束違規|*CompletionType* SQL_COMMIT，且驗證，對承諾做出的變更會造成完整性條件約束違規。 如此一來，交易已回復。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*szMessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*ConnectionHandle*。 呼叫此函式，以及前完成執行[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*。 上一次呼叫函式則*ConnectionHandle*。<br /><br /> 呼叫此函式，以及前完成執行**SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒在多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的陳述式控制代碼*ConnectionHandle*還在執行時和**SQLEndTran**呼叫。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *ConnectionHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**與陳述式控制代碼相關聯的呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM)*處理*與*HandleType*設定為 SQL_HANDLE_DBC 和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**呼叫其中一個相關聯的陳述式控制代碼*處理*和傳回的 SQL_PARAM_DATA_AVAILABLE。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY012|無效的交易作業碼|(DM) 指定的引數的值*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK 都不是。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY092|屬性/選項識別碼無效|(DM) 指定的引數的值*HandleType*已 SQL_HANDLE_ENV 都利用 SQL_HANDLE_DBC。|  
|HY115|SQLEndTran 不允許的環境，包含與非同步函式執行啟用的連接|(DM) *HandleType*如果環境中的連接已啟用非同步執行的連線函式不能設定為 SQL_HANDLE_ENV。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱本主題的註解區段。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援**復原**作業。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 ODBC 3 中。*x*驅動程式，如果*HandleType*為 SQL_HANDLE_ENV 並*處理*是有效的環境控制代碼，則驅動程式管理員會呼叫**SQLEndTran**與環境相關聯的每個驅動程式中。 *處理*驅動程式呼叫的引數會在驅動程式的環境控制代碼。 ODBC 2。*x*驅動程式，如果*HandleType*為 SQL_HANDLE_ENV 並*處理*有效的環境的控制代碼，而且有多個連接的狀態，在該環境中，連接然後會呼叫驅動程式管理員**SQLTransact**中一次連接的狀態，在該環境中的每個連線的驅動程式。 *處理*每個呼叫中的引數將會連接的控制代碼。 在任一情況下，驅動程式會嘗試認可或回復交易，根據的值*CompletionType*，所有連線都處於連線狀態，在該環境上。 不在作用中連線不會影響交易。  
  
> [!NOTE]  
>  **SQLEndTran**無法認可或復原交易上的共用環境中使用。 SQLSTATE HY092 會傳回 （無效的屬性/選項識別碼），如果**SQLEndTran**呼叫*處理*設為其中一個共用環境的控制代碼或控制代碼上共用的連線環境。  
  
 只有當它所收到的每個連線 SQL_SUCCESS，驅動程式管理員會傳回 SQL_SUCCESS。 如果驅動程式管理員會在一個或多個連接上接收 SQL_ERROR，它會傳回 SQL_ERROR，應用程式，並診斷資訊會置於環境的診斷資料結構。 若要判斷哪些連線失敗認可或復原作業期間，應用程式可以呼叫**SQLGetDiagRec**每個連接。  
  
> [!NOTE]  
>  驅動程式管理員不會跨所有連線模擬全域交易，因此不會使用兩階段認可通訊協定。  
  
 如果*CompletionType*為 SQL_COMMIT， **SQLEndTran**發出所有作用中的作業，與受影響的連接相關聯的任何陳述式上的 commit 要求。 如果*CompletionType*是 SQL_ROLLBACK， **SQLEndTran**發出任何受影響的連接相關聯的陳述式上的所有作用中作業的復原要求。 如果沒有交易正在作用中， **SQLEndTran**時不會影響任何資料來源都會傳回 SQL_SUCCESS。 如需詳細資訊，請參閱[Committing 和循環回到交易](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果驅動程式為手動認可模式 (藉由呼叫**SQLSetConnectAttr**與 SQL_ATTR_AUTOCOMMIT 屬性設定為 sql_autocommit_off 時)，可以包含在 SQL 陳述式時，隱含地啟動新的交易針對目前的資料來源執行交易。 如需詳細資訊，請參閱[認可模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 若要判斷交易作業如何影響資料指標，應用程式呼叫**SQLGetInfo**與 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 選項。 如需詳細資訊，請參閱下列段落，請參閱[效果的資料指標和備妥的陳述式上交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_DELETE， **SQLEndTran**關閉和刪除所有開啟的資料指標與連接相關聯的所有陳述式，並捨棄所有擱置的結果。 **SQLEndTran**離開配置 （已取消準備） 的狀態; 中的任何陳述式的應用程式可以重複使用它們的後續 SQL 要求，或可以呼叫**SQLFreeStmt**或**SQLFreeHandle**與*HandleType*取消配置其利用 SQL_HANDLE_STMT。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_CLOSE， **SQLEndTran**關閉所有開啟的資料指標與連接相關聯的所有陳述式。 **SQLEndTran**離開任何陳述式出現在已備妥狀態，應用程式可以呼叫**SQLExecute**情況下先呼叫連接相關聯的陳述式**SQLPrepare**。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_PRESERVE， **SQLEndTran**不會影響與連接相關聯的開啟資料指標。 它們指向之前呼叫的資料列在資料指標維持**SQLEndTran**。  
  
 支援交易，呼叫的驅動程式和資料來源的**SQLEndTran** SQL_COMMIT 或 SQL_ROLLBACK 時沒有交易在使用中會傳回 SQL_SUCCESS （表示沒有任何因認可或回復）和資料來源上沒有作用。  
  
 在自動認可模式驅動程式時，驅動程式管理員不會呼叫**SQLEndTran**驅動程式中。 **SQLEndTran**永遠都會傳回 SQL_SUCCESS 不論是否使用呼叫*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。  
  
 不支援交易的驅動程式或資料來源 (**SQLGetInfo** *選項*SQL_TXN_CAPABLE 是 SQL_TC_NONE) 有效地永遠都處於自動認可模式，因此一律傳回 SQL_SUCCESS，如**SQLEndTran**使用的呼叫是否*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。 這類驅動程式和資料來源不實際回復交易時要求若要這樣做。  
  
## <a name="suspended-state"></a>暫停的狀態  
 作用中交易已在 Windows 7 之前發行的驅動程式管理員，如果**SQLEndTran**從驅動程式傳回 SQL_ERROR。 不過，很可能會有已成功認可交易的伺服器上，但用戶端上的驅動程式在沒有通知 （例如，因為發生網路錯誤）。 這可讓連線保持處於錯誤狀態。 Windows 7 時**SQLEndTran**傳回 SQL_ERROR，連接可能會在暫停狀態。 在暫停狀態，它可能會呼叫唯讀函式。 最後，應用程式應該呼叫**SQLDisconnect**暫停連線上釋放資源。  
  
 如果所有下列條件成立，連線將進入暫停狀態：  
  
-   驅動程式會傳回 SQL_ERROR 從**SQLEndTran**。  
  
-   驅動程式為 ODBC 3.8，或更新版本。  
  
-   應用程式版本為 3.8 或更新版本。或重新編譯的 ODBC 2.x 或 3.x 應用程式已成功取消**SQLEndTran**函式透過**SQLCancelHandle**。  
  
-   驅動程式未傳回下列訊息，確認交易未完成的其中一個：  
  
    -   25S03： 交易回復  
  
    -   40001： 序列化失敗  
  
    -   40002： 完整性條件約束  
  
    -   HYC00： 未實作的選擇性功能  
  
 如果**SQLEndTran**呼叫安全的環境控制代碼和其連線的其中一個符合上述條件，所有連線連接至相同的驅動程式將都進入暫停狀態。  
  
 應用程式呼叫之後**SQLDisconnect**上有暫止的連接，連接可以用來重新連線到另一個資料來源或相同的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消連接控制代碼上以非同步方式執行的函式。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|傳回的驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|釋放控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|釋放陳述式控制代碼|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
