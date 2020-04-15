---
title: SQLEndTran 函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLEndTran
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLEndTran
helpviewer_keywords:
- SQLEndTran function [ODBC]
ms.assetid: ff375ce1-eb50-4693-b1e6-70181a6dbf9f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cce7792e52fce4984f3da41e11d79c34b6b79e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302739"
---
# <a name="sqlendtran-function"></a>SQLEndTran 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLEndTran**請求對與連接關聯的所有語句的所有活動操作執行或回滾操作。 **SQLEndTran**還可以請求對與環境關聯的所有連接執行提交或回滾操作。  
  
> [!NOTE]  
>  有關驅動程式管理員將此功能映射到 ODBC 3 時的詳細資訊。*x*應用程式使用 ODBC 2。*x*驅動程式,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]句柄類型標識碼。 包含SQL_HANDLE_ENV(如果*句柄*是環境句柄)或SQL_HANDLE_DBC(如果*句柄*是連接句柄)。  
  
 *Handle*  
 [輸入]句柄,由*HandleType*指示的類型,指示事務的範圍。 有關詳細資訊,請參閱"註釋"。  
  
 *完成類型*  
 [輸入]以下兩個值之一:  
  
 SQL_COMMITSQL_ROLLBACK  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLEndTran**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以通過使用相應的*句柄類型*和*句柄*調用**SQLGetDiagRec**來獲取關聯的 SQLSTATE 值。 下表列出了**SQLEndTran**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08003|連線未開啟|(DM)*句柄類型*SQL_HANDLE_DBC,*並且句柄*未處於連接狀態。|  
|08007|交易期間連線失敗|*HandleType* SQL_HANDLE_DBC,在執行函數期間與*句柄*關聯的連接失敗,無法確定請求**的 COMMIT**或**ROLLBACK**是否發生在故障之前。|  
|25S01|交易狀態未知|*Handle*中的一個或多個連接未能完成指定結果的事務,結果未知。|  
|25S02|事務仍然處於活動狀態|驅動程序無法保證全域事務中的所有工作都可以以原子方式完成,並且事務仍然處於活動狀態。|  
|25S03|交易回滾|驅動程式無法保證全域事務中的所有工作都可以以原子方式完成,並且*在 Handle*中處於活動狀態的事務中的所有工作都回滾。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40002|完整性約束衝突|*完成類型*SQL_COMMIT,更改的承諾導致誠信約束違規。 因此,事務被回滾。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*szMessageText*緩衝區中返回的錯誤消息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|為*連接句柄*啟用了非同步處理。 呼叫此函數,並在它完成[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)執行之前在*ConnectHandle*上調用 。 然後在*連接處理*上再次調用該函數。<br /><br /> 調用該函數,並在它執行完**SQLCancelHandle**之前從多線程應用程式中的不同線程調用*了 ConnectHandle。*|  
|HY010|函式序列錯誤|(DM) 調用了與*ConnectHandle*關聯的語句句柄的非同步執行函數,並且在調用**SQLEndTran**時仍在執行。<br /><br /> (DM) 為*ConnectHandle*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用一個語句句柄**SQLExecute**,該句柄與*連接句柄*相關聯並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 為*HandleType*設置為SQL_HANDLE_DBC的*句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用為與*句柄*關聯的語句句柄**SQLExecDirect**之一,並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY012|無效的交易操作代碼|(DM) 為參數 *「完成類型」* 指定的值既不是SQL_COMMIT,也不是SQL_ROLLBACK。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY092|不合法屬性/選項識別碼|(DM) 為參數*HandleType*指定的值既不是SQL_HANDLE_ENV,也不是SQL_HANDLE_DBC。|  
|HY115|對於包含啟用非同步函數執行的連線的環境,不允許 SQLEndTran|(DM) 如果為環境中的連接啟用了連接函數的非同步執行,則無法將*句柄類型*設置為SQL_HANDLE_ENV。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱本主題的"註釋"部分。|  
|HYC00|沒有選擇選擇功能|驅動程式或數據源不支援**ROLLBACK**操作。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*連接句柄*關聯的驅動程式不支援該功能。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 對於 ODBC 3。*x*驅動程式,如果*HandleType*是SQL_HANDLE_ENV,*並且句柄*是有效的環境句柄,則驅動程式管理器將在與環境關聯的每個驅動程式中調用**SQLEndTran。** 對驅動程式的調用的*Handle*參數將是驅動程式的環境句柄。 對於 ODBC 2。*x*驅動程式,如果*HandleType*是SQL_HANDLE_ENV,*並且 Handle*是一個有效的環境句柄,並且該環境中有多個連接處於連接狀態,則驅動程式管理器將在驅動程式中為該環境中處於連接狀態的每個連接調用**SQLTransact**一次。 每個調用中的*Handle*參數將是連接的句柄。 在這兩種情況下,驅動程式將嘗試提交或回滾事務,具體取決於 *"完成類型"* 的值,該環境中處於連接狀態的所有連接。 非活動連接不會影響事務。  
  
> [!NOTE]  
>  **SQLEndTran**不能用於在共用環境中提交或回滾事務。 如果**SQLEndTran 呼叫 SQLEndTran,** 將傳回 SQLSTATE HY092(無效屬性/選項識別子),將傳回到*將句柄*設定為共享環境的句柄或共用環境中的連接句柄。  
  
 僅當驅動程式管理器收到每個連接的SQL_SUCCESS時,才會返回SQL_SUCCESS。 如果驅動程式管理器在一個或多個連接上接收SQL_ERROR,它將返回SQL_ERROR到應用程式,並將診斷資訊放置在環境的診斷數據結構中。 要確定在提交或回滾操作期間失敗的連接或連接,應用程式可以為每個連接調用**SQLGetDiagRec。**  
  
> [!NOTE]  
>  驅動程式管理員不類比跨所有連接的全域事務,因此不使用兩階段提交協定。  
  
 如果 *"完成類型*"SQL_COMMIT,SQLEndTran 會針對與受影響的連接關聯的任何語句發出所有活動操作的**SQLEndTran**提交請求。 如果*完成類型***SQL_ROLLBACK,SQLEndTran**會針對與受影響的連接關聯的任何語句的所有活動操作發出回滾請求。 如果沒有事務處於活動狀態 **,SQLEndTran**將返回SQL_SUCCESS,對任何數據源沒有影響。 有關詳細資訊,請參閱[提交和回滾事務](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果驅動程式處於手動提交模式(通過調用**SQLSetConnect Attr,** 將SQL_ATTR_AUTOCOMMIT屬性設置為SQL_AUTOCOMMIT_OFF),則當對當前數據源執行可包含在事務中的 SQL 語句時,將隱式啟動新事務。 有關詳細資訊,請參閱[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 要確定事務操作如何影響游標,應用程式使用SQL_CURSOR_ROLLBACK_BEHAVIOR和SQL_CURSOR_COMMIT_BEHAVIOR選項調用**SQLGetInfo。** 有關詳細資訊,請參閱以下段落,並查看[事務對遊標和準備語句的影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果SQL_CURSOR_ROLLBACK_BEHAVIOR或SQL_CURSOR_COMMIT_BEHAVIOR值等於**SQL_CB_DELETE,SQLEndTran**將關閉並刪除與連接關聯的所有語句上的所有打開的遊標,並丟棄所有掛起的結果。 **SQLEndTran**將任何語句保留在已分配(未準備)狀態中;應用程式可以將它們重用為後續 SQL 請求,也可以調用**SQLFreeStmt**或**SQLFreeHandle,** 並帶有*SQL_HANDLE_STMT的句柄類型*來解調它們。  
  
 如果SQL_CURSOR_ROLLBACK_BEHAVIOR或SQL_CURSOR_COMMIT_BEHAVIOR值等於**SQL_CB_CLOSE,SQLEndTran**將關閉與連接關聯的所有語句上的所有打開游標。 **SQLEndTran**將任何語句保留在準備狀態中;應用程式可以呼叫**SQLExecute**以執行與連線關聯的語句,而無需首先呼叫**SQLPrepare**。  
  
 如果SQL_CURSOR_ROLLBACK_BEHAVIOR或SQL_CURSOR_COMMIT_BEHAVIOR值等於SQL_CB_PRESERVE,則**SQLEndTran**不會影響與連接關聯的打開游標。 游標停留在調用**SQLEndTran**之前指向的行中。  
  
 對於支援事務的驅動程式和數據源,在沒有任何事務處於活動狀態時使用SQL_COMMIT或SQL_ROLLBACK調用**SQLEndTran**返回SQL_SUCCESS(指示沒有要提交或回滾的工作),並且對數據源沒有影響。  
  
 當驅動程式處於自動提交模式時,驅動程式管理器不會在驅動程式中調用**SQLEndTran。** **SQLEndTran**始終返回SQL_SUCCESS,無論它是使用 SQL_COMMIT 的*完成類型*還是SQL_ROLLBACK調用。  
  
 不支援事務的驅動程式或資料來源 **(SQLGetInfo** *選項*SQL_TXN_CAPABLESQL_TC_NONE)實際上始終處於自動提交模式,因此無論是否使用完成*類型*SQL_COMMIT或SQL_ROLLBACK調用它們,始終返回**SQLEndTran** SQL_SUCCESS。 此類驅動程式和數據源實際上不會在請求時回滾事務。  
  
## <a name="suspended-state"></a>暫停狀態  
 在 Windows 7 之前發布的驅動程式管理器中,如果**SQLEndTran**從驅動程式返回SQL_ERROR,則事務處於活動狀態。 但是,事務可能在伺服器上成功提交,但用戶端上的驅動程式尚未收到通知(例如,因為發生了網路錯誤)。 這將使連接處於不良狀態。 從 Windows 7 開始,當**SQLEndTran**返回SQL_ERROR時,連接可能處於掛起狀態。 在掛起狀態下,可以調用唯讀函數。 最終,應用程式應在掛起的連接上調用**SQLDisconnect**以釋放資源。  
  
 如果以下所有條件都為 true,則連接將置於暫停狀態:  
  
-   驅動程式從**SQLEndTran**返回SQL_ERROR。  
  
-   驅動程式為 ODBC 版本 3.8 或更高版本。  
  
-   應用程式版本為 3.8 或更高版本;或重新編譯的 ODBC 2.x 或 3.x 應用程式通過**SQLCancelHandle**成功取消**SQLEndTran**函數。  
  
-   驅動程式未返回以下訊息之一,這些訊息確認事務未完成:  
  
    -   25S03: 事務回滾  
  
    -   40001: 序列化失敗  
  
    -   40002: 完整性規範  
  
    -   HYC00:未實作功能  
  
 如果在環境句柄上調用**SQLEndTran,** 並且其連接之一滿足上述條件,則連接到同一驅動程式的所有連接都將置於掛起狀態。  
  
 應用程式在掛起的連接上調用**SQLDisconnect**後,該連接可用於重新連接到其他數據源或同一數據來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消在連接句柄上異步運行的函數。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|傳回關於驅動程式或資料來源的資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|釋放手柄|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|釋放敘述|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
