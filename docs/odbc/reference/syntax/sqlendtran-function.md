---
title: SQLEndTran 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 82045d5dbbee356f084d587100edfbafd4947f54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104636"
---
# <a name="sqlendtran-function"></a>SQLEndTran 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLEndTran**要求所有作用中的作業與連接相關聯的所有陳述式的認可或回復作業。 **SQLEndTran**也可以要求認可或復原作業會執行與環境相關聯的所有連線。  
  
> [!NOTE]  
>  如需哪些驅動程式管理員的詳細資訊時 ODBC 3 會對應到此函式。*x*應用程式正在使用的 ODBC 2。*x*驅動程式，請參閱[對應取代函式應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]控制代碼型別識別項。 包含任一 SQL_HANDLE_ENV (如果*處理*環境的控制代碼) 或利用 SQL_HANDLE_DBC (如果*處理*是連接控制代碼)。  
  
 *Handle*  
 [輸入]控制代碼所表示的型別*HandleType*，指出交易的範圍。 如需詳細資訊，請參閱 「 註解 」。  
  
 *CompletionType*  
 [輸入]下列兩個值之一：  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLEndTran**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**適當*HandleType*並*處理*。 下表列出通常所傳回的 SQLSTATE 值**SQLEndTran** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連接|(DM) *HandleType*已利用 SQL_HANDLE_DBC，而*處理*無法處於連線狀態。|  
|08007|在交易期間的連線失敗|*HandleType*已利用 SQL_HANDLE_DBC，並連接相關聯*處理*函式執行期間失敗，而且不能決定是否要求**認可**或是**ROLLBACK**失敗前發生。|  
|25S01|交易狀態未知|一或多個中的連線*處理*無法完成交易，且指定，其結果，且結果是未知。|  
|25S02|交易仍為使用|驅動程式無法保證以不可分割的方式，完成所有工作中的全域交易，交易仍為使用中。|  
|25S03|回復交易|驅動程式無法保證以不可分割的方式，完成所有工作中的全域交易，而且所有工作中的使用中交易*處理*已回復。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40002|完整性條件約束違規|*CompletionType* SQL_COMMIT，並為變更的認可會造成完整性條件約束違規。 如此一來，交易已回復。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*szMessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*ConnectionHandle*。 呼叫函式，並完成執行之前[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*。 然後在上一次呼叫函式*ConnectionHandle*。<br /><br /> 呼叫函式，並完成執行之前**SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒，多執行緒應用程式中。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫相關聯的陳述式控制代碼*ConnectionHandle*仍執行時並**SQLEndTran**呼叫。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *ConnectionHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**陳述式控制代碼相關聯的呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM)*處理*具有*HandleType*設定為 SQL_HANDLE_DBC 和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對其中一個相關聯的陳述式控制代碼呼叫*處理*和傳回的 SQL_PARAM_DATA_AVAILABLE。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY012|無效的交易作業碼|(DM) 引數指定的值*CompletionType*不是 SQL_COMMIT 或 SQL_ROLLBACK。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY092|屬性/選項識別碼無效|(DM) 引數指定的值*HandleType*不是 SQL_HANDLE_ENV 或利用 SQL_HANDLE_DBC。|  
|HY115|SQLEndTran 不允許使用啟用的非同步函式執行包含連線的環境|(DM) *HandleType*無法設定為 SQL_HANDLE_ENV 中，如果在環境中的連接已啟用的連線函式的非同步執行。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱本主題的註解區段。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援**ROLLBACK**作業。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 ODBC 3 中。*x*驅動程式，如果*HandleType*為 SQL_HANDLE_ENV 並*處理*是有效的環境控制代碼，則驅動程式管理員會呼叫**SQLEndTran**與環境相關聯的每個驅動程式中。 *處理*驅動程式呼叫的引數會驅動程式的環境控制代碼。 ODBC 2。*x*驅動程式，如果*HandleType*為 SQL_HANDLE_ENV 並*處理*有效的環境的控制代碼，而且有多個連線，連接的狀態，在該環境中，然後驅動程式管理員會呼叫**SQLTransact**中一次連接的狀態，在該環境中的每個連線的驅動程式。 *處理*每個呼叫中的引數將會連接的控制代碼。 在任一情況下，驅動程式會嘗試認可或回復交易，根據的值*CompletionType*，在所有的連線上所連接的狀態，在該環境。 未作用的連線不會影響交易。  
  
> [!NOTE]  
>  **SQLEndTran**無法認可或復原交易上的共用環境中使用。 SQLSTATE HY092 會傳回 （無效的屬性/選項識別碼），如果**SQLEndTran**呼叫*處理*設為其中一個共用的環境中的控制代碼或在共用連接的控制代碼環境。  
  
 它所收到的每個連線 SQL_SUCCESS，驅動程式管理員會傳回 SQL_SUCCESS。 如果驅動程式管理員在一或多個連接上收到 SQL_ERROR，該應用程式，會傳回 SQL_ERROR，並診斷的資訊會放在環境的診斷資料結構。 若要判斷哪些連線失敗認可或復原作業期間，應用程式可以呼叫**SQLGetDiagRec**針對每個連線。  
  
> [!NOTE]  
>  驅動程式管理員不會跨所有連接模擬全域交易，並因此不會使用兩階段交易認可通訊協定。  
  
 如果*CompletionType*是 SQL_COMMIT， **SQLEndTran**發出與受影響的連接相關聯的任何陳述式上的所有作用中作業的 commit 要求。 如果*CompletionType*是 SQL_ROLLBACK， **SQLEndTran**發出與受影響的連接相關聯的任何陳述式上的所有作用中作業的復原要求。 如果沒有交易正在作用中， **SQLEndTran**時不會影響任何資料來源都會傳回 SQL_SUCCESS。 如需詳細資訊，請參閱 < [Committing 和循環回到交易](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果驅動程式為手動認可模式 (藉由呼叫**SQLSetConnectAttr**與 SQL_ATTR_AUTOCOMMIT 屬性設定為 sql_autocommit_off 時)，可以包含在 SQL 陳述式時，隱含地啟動新的交易針對目前的資料來源執行交易。 如需詳細資訊，請參閱 <<c0> [ 認可模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 若要判斷交易作業如何影響資料指標，應用程式會呼叫**SQLGetInfo**使用 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 選項。 如需詳細資訊，請參閱下列段落，還可以看到[效果的資料指標和已備妥的陳述式上交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_DELETE， **SQLEndTran**關閉並刪除所有與連接相關聯的所有陳述式開啟的資料指標並捨棄所有暫止的結果。 **SQLEndTran**離開已配置 （已取消準備） 的狀態; 中任何陳述式應用程式可以重複使用它們來 SQL 的後續要求，或可以呼叫**SQLFreeStmt**或是**SQLFreeHandle**與*HandleType*解除配置的利用 SQL_HANDLE_STMT。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_CLOSE， **SQLEndTran**關閉所有開啟的資料指標與連接相關聯的所有陳述式。 **SQLEndTran**離開已準備就緒的狀態; 中任何陳述式的應用程式可以呼叫**SQLExecute**陳述式相關聯的連接，但是未先呼叫**SQLPrepare**。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_PRESERVE， **SQLEndTran**並不會影響與連接相關聯的開啟資料指標。 資料指標停留在它們指向之前呼叫的資料列**SQLEndTran**。  
  
 支援交易，呼叫的驅動程式和資料來源**SQLEndTran** SQL_COMMIT 或 SQL_ROLLBACK 當任何交易不在使用會傳回 SQL_SUCCESS （表示沒有任何因認可或回復）並對資料來源沒有任何作用。  
  
 在自動認可模式驅動程式時，驅動程式管理員不會呼叫**SQLEndTran**驅動程式中。 **SQLEndTran**一律會傳回 SQL_SUCCESS，不論是否使用呼叫*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。  
  
 不支援交易的驅動程式或資料來源 (**SQLGetInfo** *選項*SQL_TXN_CAPABLE 是 SQL_TC_NONE) 實際上永遠都處於自動認可模式，並因此一律會傳回 SQL_SUCCESS，如**SQLEndTran**使用的呼叫是否*CompletionType* SQL_COMMIT 或 SQL_ROLLBACK。 這類驅動程式和資料來源不實際回復交易時要求若要這樣做。  
  
## <a name="suspended-state"></a>暫止的狀態  
 在 Windows 7 之前發行的驅動程式管理員，交易正在作用中如果**SQLEndTran**從驅動程式傳回 SQL_ERROR。 不過，很可能必須已成功認可交易的伺服器上，但用戶端上的驅動程式有不通知 （例如，因為發生網路錯誤）。 這會將連線保持在不正常的狀態。 從 Windows 7 開始時**SQLEndTran**傳回 SQL_ERROR，連接可能會在暫停狀態。 在暫停狀態，就可以呼叫唯寫的函式。 最後，應用程式應該呼叫**SQLDisconnect**上暫止的連線，以釋放資源。  
  
 如果下列條件全部成立，連線便會置於暫停狀態：  
  
-   驅動程式會傳回 SQL_ERROR，從**SQLEndTran**。  
  
-   驅動程式為 ODBC 3.8，或更新版本。  
  
-   應用程式版本為 3.8 或更新版本;或重新編譯的 ODBC 2.x 或 3.x 應用程式已成功取消**SQLEndTran**函式透過**SQLCancelHandle**。  
  
-   驅動程式未傳回下列訊息，確認交易未完成的其中一個：  
  
    -   25S03:回復交易  
  
    -   40001:序列化失敗  
  
    -   40002:完整性條件約束  
  
    -   HYC00:未實作選擇性功能  
  
 如果**SQLEndTran**呼叫安全的環境控制代碼和其連線的其中一個符合上述條件，連接到相同的驅動程式的所有連線將會都進入暫停狀態。  
  
 應用程式呼叫後**SQLDisconnect**暫止的連線，連線可用來重新連線到另一個資料來源或相同的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|正在取消連接控制代碼上以非同步方式執行的函式。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|傳回的驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|釋放控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|釋放陳述式控制代碼|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
