---
description: SQLEndTran 函數
title: SQLEndTran 函式 |Microsoft Docs
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
ms.openlocfilehash: fea27beb03c19dd9499175678ecfdcb7759a73f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461128"
---
# <a name="sqlendtran-function"></a>SQLEndTran 函數
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLEndTran** 會針對與連接相關聯的所有語句，要求所有使用中作業的認可或回復作業。 **SQLEndTran** 也可以要求對與環境相關聯的所有連接執行認可或回復作業。  
  
> [!NOTE]  
>  如需有關驅動程式管理員如何將此函式對應至 ODBC 3 的詳細資訊。*x* 應用程式正在使用 ODBC 2。*x* 驅動程式，請參閱對應取代函式 [以提供應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 輸出控制碼類型識別碼。 包含 SQL_HANDLE_ENV * (如果控制碼是* 環境控制碼) 或 SQL_HANDLE_DBC (如果 *句* 柄是連接處理常式) 。  
  
 *Handle*  
 輸出 *HandleType*所表示之類型的控制碼，表示交易的範圍。 如需詳細資訊，請參閱「批註」。  
  
 *CompletionType*  
 輸出下列兩個值的其中一個：  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLEndTran**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由使用適當的*HandleType*和*控制碼*呼叫**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出 **SQLEndTran** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08003|連接未開啟| (DM) *HandleType* 是 SQL_HANDLE_DBC 的，且 *控制碼* 未處於已線上狀態。|  
|08007|交易期間的連接失敗|*HandleType*已 SQL_HANDLE_DBC，且在函式執行期間與*控制碼*相關聯的連接失敗，而且無法判斷是否在失敗前發生要求的**認可**或**回復**。|  
|25S01|交易狀態不明|*控制碼*中有一或多個連接無法完成具有指定之結果的交易，且結果未知。|  
|25S02|交易仍在使用中|驅動程式無法保證全域交易中的所有工作都能以不可部分完成的方式完成，而且交易仍在使用中。|  
|25S03|交易已回復|驅動程式無法保證全域交易中的所有工作都能以不可部分完成的方式完成，而且 *交易中使用中的* 所有工作都會回復。|  
|40001|序列化失敗|因為另一個交易發生資源鎖死，所以已回復交易。|  
|40002|完整性條件約束違規|*CompletionType* SQL_COMMIT，而變更的承諾會導致完整性條件約束違規。 因此，交易已復原。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* szMessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*ConnectionHandle*已啟用非同步處理。 在*ConnectionHandle*上呼叫函式，且在完成執行[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)函式之前，會呼叫此函式。 然後在 *ConnectionHandle*上再次呼叫該函式。<br /><br /> 從多執行緒應用程式*中的不同*執行緒呼叫函式時，會呼叫此函式，並在其完成執行**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式是針對與 *ConnectionHandle* 相關聯的語句控制碼呼叫，並且在呼叫 **SQLEndTran** 時仍在執行中。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *ConnectionHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos** 為與 *ConnectionHandle* 相關聯的語句控制碼呼叫，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對*HandleType*設定為 SQL_HANDLE_DBC 的*控制碼*呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResults** 的其中一個與 *控制碼* 和傳回 SQL_PARAM_DATA_AVAILABLE 相關聯的語句控制碼。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY012|不正確交易操作程式碼| (DM) 為引數 *CompletionType* 指定的值不 SQL_COMMIT 或 SQL_ROLLBACK。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY092|不正確屬性/選項識別碼| (DM) 為引數 *HandleType* 指定的值不 SQL_HANDLE_ENV 或 SQL_HANDLE_DBC。|  
|HY115|包含已啟用非同步函式執行之連接的環境不允許 SQLEndTran|如果環境中的連接已啟用非同步執行連線函式， (DM) *HandleType* 就無法設定為 SQL_HANDLE_ENV。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱本主題的「批註」一節。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援 **復原** 操作。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *ConnectionHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 適用于 ODBC 3。*x* 驅動程式，如果 *HandleType* 是 SQL_HANDLE_ENV 且 *控制碼* 是有效的環境控制碼，則驅動程式管理員會在與環境相關聯的每個驅動程式中呼叫 **SQLEndTran** 。 驅動程式呼叫的 *控制碼* 引數將會是驅動程式的環境控制碼。 適用于 ODBC 2。*x* 驅動程式，如果 *HandleType* 是 SQL_HANDLE_ENV 且 *控制碼* 是有效的環境控制碼，且該環境中有多個連線處於線上狀態，則驅動程式管理員會在該環境中的每個連線都呼叫驅動程式中的 **SQLTransact** 一次。 每次呼叫中的 *控制碼* 引數都會是連接的控制碼。 無論是哪一種情況，驅動程式都會嘗試認可或復原交易，這取決於在該環境上線上狀態的所有連接上， *CompletionType*的值。 非使用中的連接不會影響交易。  
  
> [!NOTE]  
>  **SQLEndTran** 無法用來認可或回復共用環境上的交易。 如果將*控制碼*設定為共用環境控制碼的控制碼或共用環境上連接的控制碼 **，則會**傳回 SQLSTATE HY092 (不正確屬性/選項識別碼) 。  
  
 驅動程式管理員只會在收到每個連線的 SQL_SUCCESS 時，才會傳回 SQL_SUCCESS。 如果驅動程式管理員收到一或多個連線的 SQL_ERROR，則會將 SQL_ERROR 傳回給應用程式，而診斷資訊會放在環境的診斷資料結構中。 若要判斷認可或復原作業期間失敗的連接或連接，應用程式可以呼叫每個連接的 **SQLGetDiagRec** 。  
  
> [!NOTE]  
>  驅動程式管理員不會模擬所有連接間的全域交易，因此不會使用兩階段認可通訊協定。  
  
 如果 *CompletionType* 是 SQL_COMMIT， **SQLEndTran** 就會針對任何與受影響連接相關聯的語句，發出認可要求，以進行所有使用中的作業。 如果 SQL_ROLLBACK *CompletionType* ， **SQLEndTran** 就會針對任何與受影響連接相關聯的語句，發出回復要求。 如果沒有作用中的交易， **SQLEndTran** 會傳回 SQL_SUCCESS，且不會影響任何資料來源。 如需詳細資訊，請參閱認可 [和回復交易](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果驅動程式處於手動認可模式 (藉由呼叫 **SQLSetConnectAttr** ，並將 SQL_ATTR_AUTOCOMMIT 屬性設定為 SQL_AUTOCOMMIT_OFF) ，則會在交易中包含的 SQL 語句針對目前的資料來源執行時，以隱含方式啟動新的交易。 如需詳細資訊，請參閱 [認可模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 為了判斷交易作業對資料指標的影響，應用程式會使用 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 選項來呼叫 **SQLGetInfo** 。 如需詳細資訊，請參閱下列段落，也會看到 [對資料指標和已備妥語句的交易效果](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_DELETE， **SQLEndTran** 會關閉並刪除與連接相關聯之所有語句上的所有開啟的資料指標，並捨棄所有暫止的結果。 **SQLEndTran** 會將任何存在於已配置 (未準備) 狀態的語句保留;應用程式可以重複使用它們來進行後續的 SQL 要求，或呼叫 **SQLFreeStmt** 或 **SQLFreeHandle** 和 *HandleType* 的 SQL_HANDLE_STMT 來將它們解除配置。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_CLOSE， **SQLEndTran** 會在與連接相關聯的所有語句上，關閉所有開啟的資料指標。 **SQLEndTran** 會將任何出現在備妥狀態的語句保留;應用程式可以呼叫 **SQLExecute** 來取得與連接相關聯的語句，而不需要先呼叫 **SQLPrepare**。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_PRESERVE， **SQLEndTran** 就不會影響與連接相關聯的開啟資料指標。 在呼叫 **SQLEndTran**之前，資料指標會保留在它們所指向的資料列上。  
  
 若為支援交易的驅動程式和資料來源，則在沒有任何交易作用時，使用 SQL_COMMIT 或 SQL_ROLLBACK 來呼叫 **SQLEndTran** 會傳回 SQL_SUCCESS (指出沒有要認可或) 回復的工作，而且不會影響資料來源。  
  
 當驅動程式處於自動認可模式時，驅動程式管理員不會在驅動程式中呼叫 **SQLEndTran** 。 **SQLEndTran** 一律會傳回 SQL_SUCCESS，不論是否以 SQL_COMMIT 或 SQL_ROLLBACK 的 *CompletionType* 來呼叫它。  
  
 不支援交易的驅動程式或資料來源 (**SQLGetInfo** *選項* SQL_TXN_CAPABLE SQL_TC_NONE) 實際上一律處於自動認可模式，因此一律會傳回 **SQLEndTran** 的 SQL_SUCCESS，不論是否以 SQL_COMMIT 或 SQL_ROLLBACK 的 *CompletionType* 來呼叫它們。 這類驅動程式和資料來源在要求時，不會實際回復交易。  
  
## <a name="suspended-state"></a>暫止狀態  
 在 Windows 7 之前發行的驅動程式管理員中，如果 **SQLEndTran** 從驅動程式傳回 SQL_ERROR，交易就會處於作用中狀態。 不過，交易可能已在伺服器上成功認可，但用戶端上的驅動程式未收到 (的通知，因為) 發生網路錯誤。 這會讓連線處於不良狀態。 從 Windows 7 開始，當 **SQLEndTran** 傳回 SQL_ERROR 時，連接可能會處於暫停狀態。 處於暫停狀態時，可以呼叫唯讀函式。 最後，應用程式應該在暫停的連接上呼叫 **SQLDisconnect** ，以釋放資源。  
  
 如果下列所有條件都成立，連接將會進入暫停狀態：  
  
-   驅動程式會從 **SQLEndTran**傳回 SQL_ERROR。  
  
-   驅動程式是 ODBC 3.8 版或更新版本。  
  
-   應用程式版本是3.8 或更新版本;或者，重新編譯的 ODBC 2.x 或3.x 應用程式成功地透過**SQLCancelHandle**取消**SQLEndTran**函式。  
  
-   驅動程式未傳回下列其中一則訊息，確認交易未完成：  
  
    -   25S03：交易已復原  
  
    -   40001：序列化失敗  
  
    -   40002：完整性條件約束  
  
    -   HYC00：未執行選用功能  
  
 如果在環境控制碼上呼叫 **SQLEndTran** ，且其中一個連線符合上述條件，則連接到相同驅動程式的所有連接都會進入暫停狀態。  
  
 當應用程式在暫停的連接上呼叫 **SQLDisconnect** 之後，就可以使用該連接來重新連接到另一個資料來源或相同的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消在連接控制碼上以非同步方式執行的函式。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|傳回驅動程式或資料來源的相關資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|釋放控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|釋放語句控制碼|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法) ](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
