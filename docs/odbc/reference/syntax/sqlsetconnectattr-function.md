---
title: "SQLSetConnectAttr 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetConnectAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectAttr
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC]
ms.assetid: 97fc7445-5a66-4eb9-8e77-10990b5fd685
caps.latest.revision: 83
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4006d05403781ada24cf43903cd14a971366e12a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**設定屬性，以管理連線的層面。  
  
> [!NOTE]  
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3*.x*應用程式使用 ODBC 2*.x*驅動程式，請參閱[向後的對應取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
 *Attribute*  
 [輸入]若要設定，屬性列在 [意見]。  
  
 *ValuePtr*  
 [輸入]要與相關聯的值指標*屬性*。 值而定*屬性*， *ValuePtr*會是不帶正負號的整數值，或將會指向以 null 結束的字元字串。 請注意，整數類資料類型的型別*屬性*引數不固定長度，請參閱 「 註解區段以瞭解詳細資料。  
  
 *StringLength*  
 [輸入]如果*屬性*是 ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度 **ValuePtr*。 字元字串資料，這個引數應該包含在字串中的位元組數目。  
  
 如果*屬性*是 ODBC 定義的屬性和*ValuePtr*是整數， *StringLength*會被忽略。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*StringLength*引數。 *StringLength*可以是下列值：  
  
-   如果*ValuePtr*是字元字串的指標，則*StringLength*是 SQL_NTS 之字串的長度。  
  
-   如果*ValuePtr*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR 結果 (*長度*) 中的巨集*StringLength*。 這樣做會放在負值*StringLength*。  
  
-   如果*ValuePtr*是字元字串或二進位字串以外的值的指標，則*StringLength*應該有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定長度的值，則*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConnectAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_DBC 和*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetConnectAttr** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
 驅動程式可能會傳回 SQL_SUCCESS_WITH_INFO，提供設定選項的結果的相關資訊。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02 的警告|選項值已變更|驅動程式不支援指定的值*ValuePtr*置換相似的值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08002|使用中的連接名稱|*屬性*引數以前是 SQL_ATTR_ODBC_CURSORS，和驅動程式已連接到資料來源。|  
|08003|未開啟連線。|(DM)*屬性*值指定所需的開啟連接，但*ConnectionHandle*不是處於連線狀態。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|*屬性*引數是 SQL_ATTR_CURRENT_CATALOG，且暫止的結果集。|  
|25000|本機交易中有不合法的作業|連接已在本機時嘗試藉由設定連接屬性 SQL_ATTR_ENLIST_IN_DTC 編列在分散式的交易連接 (DTC) 交易。<br /><br /> 連接已經登記在 DTC。<br /><br /> 已經登記在分散式的交易連接的連接，並由 SQL_ATTR_AUTOCOMMIT 設定為 sql_autocommit_off 時啟動本機交易。|  
|3D000|無效的目錄名稱|*屬性*引數是 SQL_CURRENT_CATALOG，且指定的目錄名稱無效。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*ConnectionHandle*。 **SQLSetConnectAttr**呼叫函式，和之前已完成執行， [SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*，然後按一下**SQLSetConnectAttr**上一次呼叫函式*ConnectionHandle*。<br /><br /> 或者， **SQLSetConnectAttr**呼叫函式，和之前已完成執行， **SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒中多執行緒的應用程式。|  
|HY009|無效的 null 指標使用|*屬性*引數所識別的字串值，所需的連接屬性和*ValuePtr*引數為 null 指標。|  
|HY010|函數順序錯誤|以非同步方式執行的函式的呼叫 (DM) *StatementHandle*聯*ConnectionHandle*還在執行時和**SQLSetConnectAttr**呼叫。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *ConnectionHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**呼叫其中一個相關聯的陳述式控制代碼*ConnectionHandle*並傳回 SQL_PARAM_DATA_AVAILABLE。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*聯*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLBrowseConnect**針對呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|HY011|現在無法設定屬性|*屬性*引數為 SQL_ATTR_TXN_ISOLATION，並已開啟的交易。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY024|屬性值無效|提供給指定*屬性*值，指定了無效的值中*ValuePtr*。 （驅動程式管理員會傳回這個僅適用於連接和陳述式屬性接受一組離散值，例如 SQL_ATTR_ACCESS_MODE 或 SQL_ATTR_ASYNC_ENABLE 的 SQLSTATE。 對於所有其他連接和陳述式屬性，驅動程式必須確認中指定的值*ValuePtr*。)<br /><br /> *屬性*引數是 SQL_ATTR_TRACEFILE 或 SQL_ATTR_TRANSLATE_LIB，和*ValuePtr*是空字串。|  
|HY090|字串或緩衝區長度無效|*(DM) \*ValuePtr*是字元字串，而*StringLength*引數為小於 0，但不是 SQL_NTS。|  
|HY092|屬性/選項識別碼無效|(DM) 指定的引數的值*屬性*對 ODBC 驅動程式支援的版本無效。<br /><br /> (DM) 指定的引數的值*屬性*唯讀屬性。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|(DM) 應用程式嘗試啟用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 與驅動程式不支援非同步連線作業的非同步函式執行。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HY121|在相同的時間，則無法啟用資料指標程式庫和可感知驅動程式共用|如需詳細資訊，請參閱[感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*有效的 ODBC 連接或陳述式屬性版本的 ODBC 驅動程式支援但不是支援此驅動程式。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入轉譯的連線指定的 DLL。 時，才可以傳回此錯誤*屬性*是 SQL_ATTR_TRANSLATE_LIB。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|SQL_ATTR_ASYNC_DBC_EVENT 設定 （在之後建立的連接），但是驅動程式不支援非同步通知。|  
  
 當*屬性*是陳述式屬性， **SQLSetConnectAttr**可以傳回任何所傳回的 Sqlstate **SQLSetStmtAttr**。  
  
## <a name="comments"></a>註解  
 如需連接屬性的一般資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 本節稍後; 資料表中會顯示目前定義的屬性和其功能的 ODBC 版本預期的是，將會利用不同的資料來源中定義更多屬性。 ODBC; 保留範圍的屬性驅動程式開發人員必須保留自己從開啟 群組的特定驅動程式使用的值。  
  
> [!NOTE]  
>  能夠在連接層級設定陳述式屬性，藉由呼叫**SQLSetConnectAttr**已被取代，在 ODBC 3*.x*。 ODBC 3*.x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC 3*.x*陳述式屬性不能在連接層級，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性，這些屬性為連接屬性和陳述式屬性，可能會設定在連接層級或陳述式層級設定。  
>   
>  ODBC 3*.x*驅動程式只需要支援這項功能，如果應使用 ODBC 2*.x*應用程式，設定 ODBC 2*.x*連接層級的陳述式選項。 如需詳細資訊，請參閱[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中附錄 g： 驅動程式的指導方針回溯相容性。  
  
 應用程式可以呼叫**SQLSetConnectAttr**在任何時間的時間之間配置和釋放連接。 已成功設定連線的應用程式的所有連接和陳述式屬性會一直都保存到**SQLFreeHandle**連接上呼叫。 比方說，如果應用程式呼叫**SQLSetConnectAttr**屬性保存之前連接到資料來源，即使**SQLSetConnectAttr**時應用程式連接到在驅動程式會失敗資料來源;如果應用程式來設定驅動程式特有屬性，即使應用程式連接到不同的驅動程式在連接上持續發生的屬性。  
  
 可以設定某些連接屬性，只有之前已建立連接。在建立連接之後，才可以設定其他項目。 下表指出必須在之前或在建立連接之後設定這些連接屬性。 *任一*指出之前或之後的連接，可以設定屬性。  
  
|Attribute|設定之前或之後的連接？|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之後|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|其中一個 [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之後|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之後|  
|SQL_ATTR_ASYNC_ENABLE|其中一個 [2]|  
|SQL_ATTR_AUTO_IPD|之前或之後|  
|SQL_ATTR_AUTOCOMMIT|其中一個 [5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之後|  
|SQL_ATTR_CURRENT_CATALOG|[1]|  
|SQL_ATTR_DBC_INFO_TOKEN|After|  
|SQL_ATTR_ENLIST_IN_DTC|After|  
|SQL_ATTR_LOGIN_TIMEOUT|之前|  
|SQL_ATTR_METADATA_ID|之前或之後|  
|SQL_ATTR_ODBC_CURSORS|之前|  
|SQL_ATTR_PACKET_SIZE|之前|  
|SQL_ATTR_QUIET_MODE|之前或之後|  
|SQL_ATTR_TRACE|之前或之後|  
|SQL_ATTR_TRACEFILE|之前或之後|  
|SQL_ATTR_TRANSLATE_LIB|After|  
|SQL_ATTR_TRANSLATE_OPTION|After|  
|SQL_ATTR_TXN_ISOLATION|其中一個 [3]|  
  
 [之前或連接之後，根據驅動程式，可以設定 1] SQL_ATTR_ACCESS_MODE 和 SQL_ATTR_CURRENT_CATALOG。 不過，互通的應用程式設定認證後才能連接因為有些驅動程式不支援變更這些連接之後。  
  
 [現用陳述式之前，必須設定 2] SQL_ATTR_ASYNC_ENABLE。  
  
 [只有當沒有任何開啟的交易在連接上可以設定 SQL_ATTR_TXN_ISOLATION 3]。 如果資料來源不支援指定的值，某些連接屬性支援值相似的替代\* *ValuePtr*。 在這種情況下，驅動程式會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。 例如，如果*屬性*是 SQL_ATTR_PACKET_SIZE 和\* *ValuePtr*超過最大的封包大小，驅動程式會以替代的最大值。 若要判斷替代的值，應用程式呼叫**SQLGetConnectAttr**。  
  
 [呼叫期間載入驅動程式 4] 如果 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 設定已開啟連接之前，驅動程式管理員會設定驅動程式的屬性**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**。 呼叫之前**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**，驅動程式管理員不知道哪一個驅動程式連接到並不知道是否驅動程式支援非同步連接作業。 因此，驅動程式管理員一律會傳回 SQL_SUCCESS。 但是，如果驅動程式不支援非同步連接的作業呼叫**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**將會失敗。  
  
 [5] 當 SQL_ATTR_AUTOCOMMIT 設定為 FALSE 時，應用程式應該呼叫 SQLEndTran(SQL_ROLLBACK)，如果任何 API 會傳回 SQL_ERROR，為確保交易一致性。  
  
 在中設定的資訊格式\* *ValuePtr*取決於指定的緩衝區*屬性*。 **SQLSetConnectAttr**會接受屬性中有兩種不同格式的資訊： null 結尾字元字串或整數值。 每個格式註屬性的描述中。 字元字串所指向*ValuePtr*引數的**SQLSetConnectAttr**長度為*StringLength*位元組。  
  
 *StringLength*會忽略引數如果長度定義屬性，在本例中為 ODBC 2 中引入的所有屬性*.x*或更早版本。  
  
|*Attribute*|*ValuePtr*內容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 值。 驅動程式或資料來源會使用 SQL_MODE_READ_ONLY 為連線不支援 SQL 陳述式而造成更新所需的指標。 此模式可以用來最佳化鎖定策略、 管理交易或適當的驅動程式或資料來源的其他區域。 若要避免這類陳述式不提交至資料來源不需要的驅動程式。 驅動程式和資料來源時要求處理不是唯讀時唯讀連接的 SQL 陳述式的行為是由實作定義。 預設值為 SQL_MODE_READ_WRITE。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|為事件處理常式的 SQLPOINTER 值。<br /><br /> 非同步函式完成的通知已啟用藉由呼叫**SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 屬性和指定的事件控制代碼。 **注意：**通知方法不支援資料指標程式庫。 如果它嘗試啟用的通知方法時，啟用透過 SQLSetConnectAttr，資料指標程式庫應用程式會收到錯誤訊息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|啟用或停用的連接控制代碼上的選取函式的非同步執行 SQLUINTEGER 值。 如需詳細資訊，請參閱[非同步執行 （輪詢方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 啟用指定的連接相關函式的非同步作業。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = （預設值） 停用指定的連接相關函式的非同步作業。<br /><br /> 設定 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 一律是同步的 （也就是說，它會永遠不會傳回 SQL_STILL_EXECUTING）。<br /><br /> 與 SQL_ATTR_ASYNC_ENABLE 啟用非同步執行的陳述式作業。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|指向內容結構 SQLPOINTER 值。<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**以這個屬性的函式。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|指向內容結構 SQLPOINTER 值。<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**以這個屬性的函式。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|SQLULEN 值，指定是否要以非同步方式執行的陳述式指定的連接上呼叫的函式：<br /><br /> SQL_ASYNC_ENABLE_OFF = 停用連線層級的非同步執行支援的陳述式作業 （預設值）。<br /><br /> 請 = 啟用連接層級的非同步執行的陳述式作業支援。<br /><br /> 這個屬性可以設定是否**SQLGetInfo**類型傳回 SQL_AM_CONNECTION 或 SQL_AM_STATEMENT SQL_ASYNC_MODE 資訊。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|唯讀 SQLUINTEGER 值，指定是否要在呼叫之後自動母體擴展 IPD **SQLPrepare**支援：<br /><br /> SQL_TRUE = 呼叫之後自動母體擴展 IPD **SQLPrepare**驅動程式支援。<br /><br /> SQL_FALSE = 呼叫之後自動母體擴展 IPD **SQLPrepare**驅動程式不支援。 不支援備妥陳述式的伺服器無法自動填入 IPD。<br /><br /> 如果 SQL_ATTR_AUTO_IPD 連接屬性會傳回 SQL_TRUE，陳述式屬性 SQL_ATTR_ENABLE_AUTO_IPD 可以將開啟或關閉 IPD 的自動擴展。 如果 SQL_ATTR_AUTO_IPD SQL_FALSE，SQL_ATTR_ENABLE_AUTO_IPD 無法設定為 SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD 的預設值等於 SQL_ATTR_AUTO_IPD 的值。<br /><br /> 此連接屬性可以由傳回**SQLGetConnectAttr**但無法由設定**SQLSetConnectAttr**。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|SQLUINTEGER 值，指定是否要使用自動認可或手動認可模式：<br /><br /> SQL_AUTOCOMMIT_OFF = 驅動程式會使用手動認可模式及應用程式必須明確地認可或回復交易與**SQLEndTran**。<br /><br /> SQL_AUTOCOMMIT_ON = 驅動程式會使用自動認可模式。 執行之後，立即就會認可每個陳述式。 這是預設值。 在此連接上任何開啟的交易就無法認可 SQL_ATTR_AUTOCOMMIT 設定為 SQL_AUTOCOMMIT_ON 從手動認可模式變更為自動認可模式時。<br /><br /> 如需詳細資訊，請參閱[認可模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要事項：**某些資料來源刪除存取計劃和關閉每次連接上所有陳述式的資料指標陳述式被認可; 自動認可模式可能會造成這種情形，每個東西陳述式執行之後，或資料指標時關閉查詢。 如需詳細資訊，請參閱 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊中的與類型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[效果的資料指標和備妥的陳述式上交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 當自動認可模式中執行批次時，兩件事，可能會。 Autocommitable 單元，可用來當做整個批次或批次中的每個陳述式會被視為 autocommitable 單位。 特定資料來源可以支援這些這兩種行為，而且可能會提供一種選擇其中一個。 它是驅動程式定義的批次會被視為 autocommitable 單位或批次內的每個個別陳述式是否 autocommitable。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|唯讀 SQLUINTEGER 值，指出連接的狀態。 如果 SQL_CD_TRUE，連線已中斷。 如果 SQL_CD_FALSE，連線仍在作用中。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|對應要等待完成，然後再傳回給應用程式在連接上的任何要求的秒數 SQLUINTEGER 值。 驅動程式應該會傳回 SQLSTATE HYT00 （逾時過期） 隨時都是可能的情況下，與查詢執行或登入沒有關聯的逾時時間。<br /><br /> 如果*ValuePtr*是等於 0 （預設值），還有不會逾時。|  
|SQL_ATTR_CURRENT_CATALOG (連接 ODBC 2.0)|字元字串，包含要供資料來源的目錄名稱。 例如，在 SQL Server 中，類別目錄是資料庫，因此驅動程式會將傳送**使用***資料庫*陳述式，以資料來源，其中*資料庫*中所指定的資料庫\* *ValuePtr*。 單一層驅動程式類別目錄可能是目錄，因此驅動程式會變更其目前的目錄中指定的目錄 **ValuePtr*。|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|SQLPOINTER 值用來設定傳回至雙位元組字元的連線資訊語彙基元控制代碼時[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)的 (\**pRating*) 參數不等於 100。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 僅限組。 不可能使用**SQLGetConnectAttr**或**SQLGetConnectOption**擷取此值。 驅動程式管理員**SQLSetConnectAttr**將不會接受 SQL_ATTR_DBC_INFO_TOKEN，因為應用程式不應將此屬性。<br /><br /> 如果驅動程式會傳回 SQL_ERROR 設定 SQL_ATTR_DBC_INFO_TOKEN 之後，將會釋放剛從集區取得的連接。 驅動程式管理員則會嘗試從集區取得另一個連接。 請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)如需詳細資訊。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|SQLPOINTER 值，指定是否要在 Microsoft 元件服務所協調的分散式交易中使用的 ODBC 驅動程式。<br /><br /> 傳遞的 DTC OLE 交易物件，指定將匯出到 SQL Server 或 sql_dtc_done 來結束連接的 DTC 關聯的交易。<br /><br /> 用戶端會呼叫 Microsoft 分散式交易協調器 (MS DTC) OLE itransactiondispenser:: Begintransaction 方法來開始 MS DTC 交易，並建立代表交易的 MS DTC 交易物件。 接著，應用程式呼叫 SQLSetConnectAttr SQL_ATTR_ENLIST_IN_DTC 選項與 ODBC 連接產生關聯的交易物件。 所有相關的資料庫活動都將在 MS DTC 交易的保護底下進行。 應用程式會呼叫 SQLSetConnectAttr 使用 sql_dtc_done 來結束連接的 DTC 關聯。 如需詳細資訊，請參閱 MS DTC 文件集。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|對應的登入要求傳回至應用程式之前完成的等候秒數 SQLUINTEGER 值。 預設為驅動程式而定。 如果*ValuePtr*為 0，在逾時停用，連線嘗試會無限期等候。<br /><br /> 如果指定的逾時超過資料來源中的最大登入逾時，驅動程式用取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|判斷目錄函數的字串引數的處理方式 SQLUINTEGER 值。<br /><br /> 如果 SQL_TRUE，目錄函數的字串引數會被視為識別項。 大小寫並不重要。 了非分隔的字串，請移除任何尾端的空格，驅動程式和字串會摺成大寫。 分隔的字串，請移除任何開頭或尾端空格，驅動程式，並依其字面只採用無論是與分隔符號之間。 如果其中一個這些引數設定為 null 指標，此函數會傳回 SQL_ERROR 並 SQLSTATE HY009 （使用無效的 null 指標）。<br /><br /> 如果 SQL_FALSE，目錄函數的字串引數不會視為識別項。 案例很重要。 它們可以包含字串的搜尋模式，根據的引數。<br /><br /> 預設值為 SQL_FALSE。<br /><br /> *TableType*引數的**SQLTables**，其可接受的值，清單不會受到這個屬性。<br /><br /> SQL_ATTR_METADATA_ID 也可以設定在陳述式層級上。 （它是唯一的連接屬性，而且也是陳述式屬性）。<br /><br /> 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS (連接 ODBC 2.0)|SQLULEN 值，指定驅動程式管理員如何使用 ODBC 資料指標程式庫：<br /><br /> SQL_CUR_USE_IF_NEEDED = 驅動程式管理員會使用 ODBC 資料指標程式庫，才需要它。 如果驅動程式支援 SQL_FETCH_PRIOR 選項中的**SQLFetchScroll**，驅動程式管理員會使用捲動功能的驅動程式。 否則，它會使用 ODBC 資料指標程式庫。<br /><br /> SQL_CUR_USE_ODBC = 驅動程式管理員會使用 ODBC 資料指標程式庫。<br /><br /> SQL_CUR_USE_DRIVER = 驅動程式管理員使用的驅動程式捲動的功能。 這是預設值。<br /><br /> 如需有關 ODBC 資料指標程式庫的詳細資訊，請參閱[附錄 f: ODBC 資料指標程式庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 **警告：** Windows 的未來版本將移除資料指標程式庫。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|SQLUINTEGER 值，指定網路封包大小 （位元組）。 **注意：**許多資料來源可能是不支援此選項，或只傳回，但無法設定網路封包大小。 <br /><br /> 如果指定的大小超過最大的封包大小，或小於最小的封包大小，此驅動程式用取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 如果應用程式會在建立連接之後設定封包大小，此驅動程式會傳回 SQLSTATE HY011 （屬性現在無法設定）。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|視窗控制代碼 (HWND)。<br /><br /> 如果視窗控制代碼為 null 指標，此驅動程式不會顯示任何對話方塊。<br /><br /> 如果視窗控制代碼不是 null 指標，它應該是父視窗控制代碼的應用程式。 這是預設值。 驅動程式會使用此控制代碼，來顯示對話方塊。 **注意：** SQL_ATTR_QUIET_MODE 連接屬性不適用於所顯示的對話方塊**SQLDriverConnect**。|  
|SQL_ATTR_TRACE (ODBC 1.0)|告知驅動程式管理員執行追蹤 SQLUINTEGER 值：<br /><br /> SQL_OPT_TRACE_OFF 追蹤 = off （預設值）<br /><br /> SQL_OPT_TRACE_ON = on 的追蹤<br /><br /> 開啟追蹤時，驅動程式管理員會寫入追蹤檔的每個 ODBC 函數呼叫。 **注意：**驅動程式管理員追蹤時，可以傳回 SQLSTATE IM013 （追蹤檔案錯誤） 從任何函式。 <br /><br /> 應用程式使用 SQL_ATTR_TRACEFILE 選項指定追蹤檔案。 如果檔案已經存在，則驅動程式管理員會附加到檔案。 否則，它會建立檔案。 如果追蹤為開啟狀態，而且尚未指定任何追蹤檔案，驅動程式管理員會寫入 SQL 的檔案。登入的根目錄。<br /><br /> 應用程式可以將變數設定**ODBCSharedTraceFlag**表示啟用動態追蹤。 所有目前正在執行的 ODBC 應用程式，然後啟用追蹤。 如果應用程式會關閉追蹤，僅對該應用程式會將它已經關閉。<br /><br /> 如果**追蹤**系統資訊的關鍵字設定為 1 時應用程式呼叫**SQLAllocHandle**與*HandleType* SQL_HANDLE_ENV 的所有啟用追蹤控制代碼。 啟用僅適用於應用程式呼叫**SQLAllocHandle**。<br /><br /> 呼叫**SQLSetConnectAttr**與*屬性*的 SQL_ATTR_TRACE 不需要*ConnectionHandle*引數是有效而且如果，則不會傳回 SQL_ERROR*ConnectionHandle*是 NULL。 這個屬性會套用到所有連線。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|以 null 結束的字元字串，包含追蹤檔案的名稱。<br /><br /> SQL_ATTR_TRACEFILE 屬性的預設值以指定**TraceFile**系統資訊的關鍵字。 如需詳細資訊，請參閱[ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)。<br /><br /> 呼叫**SQLSetConnectAttr**與*屬性*的 SQL_ATTR_ TRACEFILE 不需要*ConnectionHandle*為有效的引數，如果，則不會傳回 SQL_ERROR*ConnectionHandle*無效。 這個屬性會套用到所有連線。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|以 null 結束的字元字串，包含含有函式的程式庫名稱**SQLDriverToDataSource**和**SQLDataSourceToDriver**驅動程式會存取執行工作，例如字元集轉譯。 這個選項可能會指定是否驅動程式已連接到資料來源。 此屬性的設定會套用於連接。 如需轉譯資料的詳細資訊，請參閱[轉譯 Dll](../../../odbc/reference/develop-app/translation-dlls.md)和[轉譯 DLL 函式參考](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|32 位元旗標值傳遞至轉譯 DLL。 這個屬性可以指定是否驅動程式已連接到資料來源。 轉譯資料的相關資訊，請參閱[轉譯 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|32 位元位元遮罩，設定目前連接的交易隔離等級。 應用程式必須呼叫**SQLEndTran**認可或回復連接，然後再呼叫上所有開啟的交易**SQLSetConnectAttr**使用此選項。<br /><br /> 有效值*ValuePtr*可藉由呼叫**SQLGetInfo**與*資訊類型*等於 SQL_TXN_ISOLATION_OPTIONS。<br /><br /> 如需交易隔離等級的說明，請參閱 SQL_DEFAULT_TXN_ISOLATION 資訊類型的描述[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[交易隔離等級](../../../odbc/reference/develop-app/transaction-isolation-levels.md)。|  
  
 [1] 這些函式可以非同步方式呼叫，只有當描述元是實作描述項，不應用程式的描述項。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

