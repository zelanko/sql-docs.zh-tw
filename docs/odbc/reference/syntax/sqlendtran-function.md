---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98a0f072af79c2c6e39d0cfc49e72cbeef1c2193
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344774"
---
# <a name="sqlendtran-function"></a>SQLEndTran 函數
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLEndTran**會針對與連接相關聯的所有語句, 要求所有作用中作業的認可或回復操作。 **SQLEndTran**也可以要求針對與環境相關聯的所有連接執行認可或復原作業。  
  
> [!NOTE]  
>  如需在 ODBC 3 時, 驅動程式管理員將此函式對應至哪個功能的詳細資訊。*x*應用程式正在使用 ODBC 2。*x*驅動程式, 請參閱[對應取代函式以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLEndTran(  
     SQLSMALLINT   HandleType,  
     SQLHANDLE     Handle,  
     SQLSMALLINT   CompletionType);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 源控制碼類型識別碼。 包含其中一個 SQL_HANDLE_ENV (如果*handle*是環境控制碼) 或 SQL_HANDLE_DBC (如果*handle*是連接控制碼)。  
  
 *Handle*  
 源*HandleType*所指示之類型的控制碼, 表示交易的範圍。 如需詳細資訊, 請參閱「批註」。  
  
 *CompletionType*  
 源下列兩個值的其中一個:  
  
 SQL_COMMIT SQL_ROLLBACK  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLEndTran**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫具有適當*SQLGetDiagRec*和*控制碼*的**HandleType**來取得相關聯的 SQLSTATE 值。 下表列出**SQLEndTran**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|08003|連接未開啟|(DM) *HandleType*已 SQL_HANDLE_DBC, 且*控制碼*不是處於線上狀態。|  
|08007|交易期間的連接失敗|*HandleType*是 SQL_HANDLE_DBC, 而且與*控制碼*相關聯的連接在函式執行期間失敗, 而且無法判斷要求的**認可**或**復原**是否發生在出.|  
|25S01|交易狀態不明|*控制碼*中的一或多個連接無法完成已指定結果的交易, 且結果為 unknown。|  
|25S02|交易仍在作用中|驅動程式無法保證全域交易中的所有工作都可以自動完成, 而且交易仍在作用中。|  
|25S03|交易已回復|驅動程式無法保證全域交易中的所有工作都可以自動完成, 而且在交易中作用中的所有工作都已回復  。|  
|40001|序列化失敗|因為另一筆交易發生資源鎖死, 所以交易已回復。|  
|40002|完整性條件約束違規|*CompletionType*是 SQL_COMMIT, 而變更的承諾會導致完整性條件約束違規。 因此, 交易已回復。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 SzMessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*ConnectionHandle*的非同步處理。 已呼叫函式, 且在完成執行[SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md)函式之前, 已在*ConnectionHandle*上呼叫該函式。 然後在*ConnectionHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 且在完成執行**SQLCancelHandle**之前, 已從多執行緒應用程式中的不同執行緒在*ConnectionHandle*上呼叫該函數。|  
|HY010|函數順序錯誤|(DM) 已針對與*ConnectionHandle*相關聯的語句控制碼呼叫非同步執行的函式, 且在呼叫**SQLEndTran**時仍在執行中。<br /><br /> (DM) 已針對*ConnectionHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> 已針對與*ConnectionHandle*相關聯的語句控制碼呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> (DM) 以非同步方式執行的函式 (不是這個) 已針對*HandleType*設定為 SQL_HANDLE_DBC, 且在呼叫此函式時仍在執行的*控制碼*呼叫。<br /><br /> (DM) **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults**已針對與*Handle*相關聯的其中一個語句控制碼呼叫, 並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。|  
|HY012|不正確交易作業程式碼|(DM) 為引數*CompletionType*指定的值不是 SQL_COMMIT 也不是 SQL_ROLLBACK。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY092|不正確屬性/選項識別碼|(DM) 為引數*HandleType*指定的值不是 SQL_HANDLE_ENV 也不是 SQL_HANDLE_DBC。|  
|HY115|如果環境中包含已啟用非同步函式執行的連接, 則不允許 SQLEndTran|如果環境中的連接已啟用非同步執行連接函式, 則 (DM) *HandleType*不能設定為 SQL_HANDLE_ENV。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需有關暫停狀態的詳細資訊, 請參閱本主題的批註一節。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援**復原**操作。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*ConnectionHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時, 就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING, 而且如果啟用通知模式, 則必須在控制碼上呼叫**SQLCompleteAsync** , 才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 適用于 ODBC 3。*x*驅動程式, 如果*HandleType*是 SQL_HANDLE_ENV, 而*handle*是有效的環境控制碼, 則驅動程式管理員會在與環境相關聯的每個驅動程式中呼叫**SQLEndTran** 。 驅動程式呼叫的*控制碼*引數將會是驅動程式的環境控制碼。 適用于 ODBC 2。*x*驅動程式, 如果*HandleType*是 SQL_HANDLE_ENV 且*控制碼*是有效的環境控制碼, 且該環境中有多個連線處於已連接狀態, 則驅動程式管理員會在驅動程式中呼叫**SQLTransact**針對該環境中處於線上狀態的每個連接一次。 每個呼叫中的*控制碼*引數將會是連接的控制碼。 不論是哪一種情況, 驅動程式都會嘗試認可或回復交易, 視*CompletionType*的值而定, 在該環境中所有處於線上狀態的連接上。 非使用中的連接不會影響交易。  
  
> [!NOTE]  
>  **SQLEndTran**無法用來在共用環境上認可或回復交易。 如果呼叫**SQLEndTran**時, 將*handle*設定為共用環境的控制碼或共用環境上的連接控制碼, 則會傳回 SQLSTATE HY092 (不正確屬性/選項識別碼)。  
  
 只有當驅動程式管理員收到每個連接的 SQL_SUCCESS 時, 才會傳回 SQL_SUCCESS。 如果驅動程式管理員在一或多個連線上收到 SQL_ERROR, 它會將 SQL_ERROR 傳回給應用程式, 並將診斷資訊放在環境的診斷資料結構中。 若要判斷認可或復原作業期間失敗的連接或連接, 應用程式可以針對每個連接呼叫**SQLGetDiagRec** 。  
  
> [!NOTE]  
>  驅動程式管理員不會模擬所有連接的全域交易, 因此不會使用兩階段認可通訊協定。  
  
 如果*CompletionType*為 SQL_COMMIT, 則**SQLEndTran**會針對與受影響連接相關聯之任何語句上的所有作用中作業發出 COMMIT 要求。 如果*CompletionType*為 SQL_ROLLBACK, 則**SQLEndTran**會針對與受影響連接相關聯之任何語句上的所有作用中作業發出 ROLLBACK 要求。 如果沒有作用中的交易, **SQLEndTran**會傳回 SQL_SUCCESS, 而不會影響任何資料來源。 如需詳細資訊, 請參閱認可[和回復交易](../../../odbc/reference/develop-app/committing-and-rolling-back-transactions.md)。  
  
 如果驅動程式處於手動認可模式 (藉由呼叫**SQLSetConnectAttr**並將 SQL_ATTR_AUTOCOMMIT 屬性設定為 SQL_AUTOCOMMIT_OFF), 則在交易中可包含的 SQL 語句時, 就會隱含地啟動新的交易。針對目前的資料來源執行。 如需詳細資訊, 請參閱[認可模式](../../../odbc/reference/develop-app/commit-mode.md)。  
  
 若要判斷交易作業如何影響資料指標, 應用程式會使用 SQL_CURSOR_ROLLBACK_BEHAVIOR 和 SQL_CURSOR_COMMIT_BEHAVIOR 選項來呼叫**SQLGetInfo** 。 如需詳細資訊, 請參閱下列段落, 也會查看[對資料指標和已備妥語句的交易影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_DELETE, 則**SQLEndTran**會關閉並刪除與該連接相關聯之所有語句上的所有開啟的資料指標, 並捨棄所有暫止的結果。 **SQLEndTran**會將任何出現在已配置 (未準備) 狀態中的語句保留;應用程式可以針對後續的 SQL 要求重複使用它們, 也可以呼叫**SQLFreeStmt**或**SQLFreeHandle**與 handletype 來的*HandleType*來將它們解除配置。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_CLOSE, 則**SQLEndTran**會在與連接相關聯的所有語句上關閉所有開啟的資料指標。 **SQLEndTran**會將任何出現在備妥狀態中的語句保留;應用程式可以針對與連接相關聯的語句呼叫**SQLExecute** , 而不需要先呼叫**SQLPrepare**。  
  
 如果 SQL_CURSOR_ROLLBACK_BEHAVIOR 或 SQL_CURSOR_COMMIT_BEHAVIOR 值等於 SQL_CB_PRESERVE, 則**SQLEndTran**不會影響與連接相關聯的開放式資料指標。 在呼叫**SQLEndTran**之前, 資料指標會保留在它們所指的資料列上。  
  
 對於支援交易的驅動程式和資料來源, 當沒有作用中交易時, 使用 SQL_COMMIT 或 SQL_ROLLBACK 呼叫**SQLEndTran**時, 會傳回 SQL_SUCCESS (表示沒有要認可或回復的工作), 而且不會影響資料來源。  
  
 當驅動程式處於自動認可模式時, 驅動程式管理員不會呼叫驅動程式中的**SQLEndTran** 。 **SQLEndTran**一律會傳回 SQL_SUCCESS, 而不論是否使用 SQL_COMMIT 或 SQL_ROLLBACK 的*CompletionType*來呼叫它。  
  
 不支援交易的驅動程式或資料來源 (**SQLGetInfo** *選項*SQL_TXN_CAPABLE 是 SQL_TC_NONE) 實際上一定會處於自動認可模式, 因此無論是否為, 一律會傳回 SQL_SUCCESS for **SQLEndTran**使用 SQL_COMMIT 或 SQL_ROLLBACK 的*CompletionType*呼叫。 這類驅動程式和資料來源在要求時, 不會實際回復交易。  
  
## <a name="suspended-state"></a>暫止狀態  
 在 Windows 7 之前發行的驅動程式管理員中, 如果**SQLEndTran**從驅動程式傳回 SQL_ERROR, 交易就會是作用中狀態。 不過, 交易可能已經在伺服器上成功認可, 但是用戶端上的驅動程式尚未收到通知 (例如, 因為發生網路錯誤)。 這會讓連接處於不正常的狀態。 從 Windows 7 開始, 當**SQLEndTran**傳回 SQL_ERROR 時, 連接可能處於暫停狀態。 在暫停的狀態中, 您可以呼叫唯讀函數。 最後, 應用程式應該在暫止的連接上呼叫**SQLDisconnect** , 以釋放資源。  
  
 如果下列所有條件都成立, 則連接將會進入暫停狀態:  
  
-   驅動程式會從**SQLEndTran**傳回 SQL_ERROR。  
  
-   驅動程式是 ODBC 3.8 版或更新版本。  
  
-   應用程式版本是3.8 或更新版本;或者, 重新編譯的 ODBC 2.x 或3.x 應用程式會透過**SQLCancelHandle**成功取消**SQLEndTran**函數。  
  
-   驅動程式未傳回下列其中一則訊息, 以確認交易未完成:  
  
    -   25S03:交易已回復  
  
    -   40001:序列化失敗  
  
    -   40002:完整性條件約束  
  
    -   HYC00:未執行的選擇性功能  
  
 如果在環境控制碼上呼叫**SQLEndTran** , 而且其中一個連線符合上述條件, 則連接到相同驅動程式的所有連線都會進入「已暫停」狀態。  
  
 在應用程式呼叫暫止連接上的**SQLDisconnect**之後, 連接可以用來重新連接到另一個資料來源或相同的資料來源。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消在連接控制碼上以非同步方式執行的函式。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|傳回驅動程式或資料來源的相關資訊|[SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
|釋放控制碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|釋放語句控制碼|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
