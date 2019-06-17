---
title: SQLSetConnectAttr 函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 53ab6ddfb8253b1df877c6e20df43f8327f0f2e5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537392"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**設定控管連線層面的屬性。  
  
> [!NOTE]
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3 *.x*應用程式正在使用的 ODBC 2 *.x*驅動程式，請參閱[對應為向後取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入] 連線控制代碼。  
  
 *Attribute*  
 [輸入]若要設定，屬性列在 [註解。]  
  
 *ValuePtr*  
 [輸入]要與相關聯的值的指標*屬性*。 值而定*屬性*， *ValuePtr*會是不帶正負號的整數值，或將指向 null 結束的字元字串。 請注意，整數類資料類型*屬性*引數不固定的長度，請參閱 < 註解區段，如需詳細資料。  
  
 *StringLength*  
 [輸入]如果*屬性*ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度 **ValuePtr*。 字元字串資料，這個引數應該包含在字串中的位元組數目。  
  
 如果*屬性*ODBC 定義的屬性和*ValuePtr*是一個整數， *StringLength*會被忽略。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*StringLength*引數。 *StringLength*可以有下列值：  
  
-   如果*ValuePtr*是字元字串的指標，則*StringLength*是 sql_nts; 之字串的長度。  
  
-   如果*ValuePtr*為二進位的緩衝區的指標，則應用程式會放 SQL_LEN_BINARY_ATTR 的結果 (*長度*) 中的巨集*StringLength*。 這會放在負值*StringLength*。  
  
-   如果*ValuePtr*是字元字串或二進位字串以外的值的指標，則*StringLength*應有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定長度的值，則*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConnectAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_DBC 並*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetConnectAttr** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
 驅動程式可能會傳回 SQL_SUCCESS_WITH_INFO，提供設定選項的結果的相關資訊。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援指定的值*ValuePtr*和類似的值已被取代。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08002|使用中的連接名稱|*屬性*引數為 SQL_ATTR_ODBC_CURSORS，和驅動程式已連接到資料來源。|  
|08003|未開啟連接|(DM)*屬性*值，指定所需的開啟連接，但*ConnectionHandle*無法處於連線狀態。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|*屬性*引數是 SQL_ATTR_CURRENT_CATALOG，且暫止的結果集。|  
|25000|在本機交易中的作業不合法|連接已在嘗試編列在分散式的交易連接 (DTC)，藉由設定連接屬性 SQL_ATTR_ENLIST_IN_DTC 本機交易中。<br /><br /> 連線已經登錄在 DTC 中。<br /><br /> 連線已經登錄在分散式的交易連接，並由 SQL_ATTR_AUTOCOMMIT 設定為 sql_autocommit_off 時啟動本機交易。|  
|3D000|無效的目錄名稱|*屬性*引數是 SQL_CURRENT_CATALOG，且指定的目錄名稱無效。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*ConnectionHandle*。 **SQLSetConnectAttr**呼叫函式，和之前執行，完成[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*，然後**SQLSetConnectAttr**在上一次呼叫函式*ConnectionHandle*。<br /><br /> 或者， **SQLSetConnectAttr**呼叫函式，和之前執行，完成**SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒中多執行緒的應用程式。|  
|HY009|使用無效的 null 指標|*屬性*引數識別的連接屬性，需要字串值，而*ValuePtr*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 的呼叫以非同步方式執行的函式*StatementHandle*聯*ConnectionHandle*仍執行時和**SQLSetConnectAttr**呼叫。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *ConnectionHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對其中一個相關聯的陳述式控制代碼呼叫*ConnectionHandle*且傳回 SQL_PARAM_DATA_AVAILABLE。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*相關聯*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLBrowseConnect**針對呼叫*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS。|  
|HY011|現在無法設定屬性|*屬性*引數為 SQL_ATTR_TXN_ISOLATION，並已開啟的交易。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY024|屬性值無效|提供給指定的*屬性*值，指定了無效的值中*ValuePtr*。 （驅動程式管理員會傳回這個僅適用於連接和陳述式屬性接受一組特定的值，例如 SQL_ATTR_ACCESS_MODE 或 sql_attr_async_enable 設定 SQLSTATE。 對於所有其他連接和陳述式屬性，驅動程式必須確認在指定的值*ValuePtr*。)<br /><br /> *屬性*引數為 SQL_ATTR_TRACEFILE 或 SQL_ATTR_TRANSLATE_LIB，及*ValuePtr*是空字串。|  
|HY090|字串或緩衝區長度無效|*(DM) \*ValuePtr*是字元字串，而*StringLength*引數為小於 0，但不是 sql_nts;。|  
|HY092|屬性/選項識別碼無效|(DM) 引數指定的值*屬性*ODBC 驅動程式支援的版本無效。<br /><br /> (DM) 引數指定的值*屬性*是唯讀的屬性。|  
|HY114|驅動程式不支援連接層級非同步函式執行|(DM) 應用程式嘗試啟用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 與驅動程式不支援非同步連接作業的非同步函式執行。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HY121|在此同時，則無法啟用資料指標程式庫和可感知驅動程式的共用|如需詳細資訊，請參閱 <<c0> [ 感知驅動程式的連接共用](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*是有效的 ODBC 連接，或驅動程式支援版本的 ODBC 陳述式屬性，但不是支援此驅動程式。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入轉譯 DLL 所指定的連接。 可傳回此錯誤時，才*屬性*是 SQL_ATTR_TRANSLATE_LIB。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
|S1118|驅動程式不支援非同步通知|SQL_ATTR_ASYNC_DBC_EVENT 設定 （之後建立的連接），但驅動程式不支援非同步通知。|  
  
 當*屬性*陳述式的屬性**SQLSetConnectAttr**可以傳回任何所傳回的 Sqlstate **SQLSetStmtAttr**。  
  
## <a name="comments"></a>註解  
 如需連接屬性的一般資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 在本節中，稍後表顯示目前定義的屬性，並在其中引進的 ODBC 版本預期的是，會利用不同的資料來源中定義其他屬性。 ODBC; 保留範圍的屬性驅動程式開發人員必須保留供自己從 Open Group 的驅動程式專屬使用的值。  
  
> [!NOTE]
>  能夠在連接層級設定陳述式屬性，藉由呼叫**SQLSetConnectAttr**已被取代，在 ODBC 3 *.x*。 ODBC 3 *.x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC 3 *.x*陳述式屬性無法設定在連接層級，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性，這是連接屬性和陳述式屬性，而且可以是在連接層級或陳述式層級設定。  
> 
>  ODBC 3 *.x*驅動程式只需要支援這項功能，如果應該使用 ODBC 2 *.x*應用程式，設定 ODBC 2 *.x*連接層級的陳述式選項。 如需詳細資訊，請參閱 < [SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
 應用程式可以呼叫**SQLSetConnectAttr**在任何時間的時間之間的連線是配置和釋放。 已成功設定連線的應用程式的所有連接和陳述式屬性一直都保存到**SQLFreeHandle**連接上呼叫。 比方說，如果應用程式呼叫**SQLSetConnectAttr**連線到資料來源之前，此屬性仍然存在即使**SQLSetConnectAttr**時應用程式連接到在驅動程式會失敗資料來源;如果應用程式設定的驅動程式特定屬性，即使應用程式連接到不同的驅動程式在連接上，也會保存屬性。  
  
 可以設定某些連接屬性，只有之前已建立連線;只有在建立連接之後，才可以設定其他項目。 下表指出之前或之後建立的連接必須設定這些連接屬性。 *任一*表示之前或之後連接，可以設定屬性。  
  
|屬性|設定之前或之後連線？|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|Either[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之後|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|Either[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之後|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之後|  
|SQL_ATTR_ASYNC_ENABLE|Either[2]|  
|SQL_ATTR_AUTO_IPD|之前或之後|  
|SQL_ATTR_AUTOCOMMIT|Either[5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之後|  
|SQL_ATTR_CURRENT_CATALOG|Either[1]|  
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
|SQL_ATTR_TXN_ISOLATION|Either[3]|  
  
 [之前或之後連接，取決於驅動程式，可以設定 1] SQL_ATTR_ACCESS_MODE 和 SQL_ATTR_CURRENT_CATALOG。 不過，互通的應用程式設定，這些連接之前因為有些驅動程式不支援變更這些連接之後。  
  
 [現用陳述式之前，必須設定 2] sql_attr_async_enable 設定。  
  
 [只有在連接上沒有開啟的交易，則可以設定 3] SQL_ATTR_TXN_ISOLATION。 如果資料來源不支援指定的值，有些連接屬性支援類似的值替換\* *ValuePtr*。 在此情況下，驅動程式會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。 例如，如果*屬性*是 SQL_ATTR_PACKET_SIZE 並\* *ValuePtr*超過最大的封包大小，此驅動程式會以替代的最大值。 若要判斷已取代的值，應用程式會呼叫**SQLGetConnectAttr**。  
  
 [在呼叫期間載入驅動程式 4] 如果 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 設定已開啟連接之前，驅動程式管理員會設定驅動程式的屬性**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**。 若要在呼叫之前**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**，驅動程式管理員不知道哪一個驅動程式連接到並不知道是否驅動程式支援非同步連接作業。 因此，驅動程式管理員一律會傳回 SQL_SUCCESS。 但是，如果驅動程式不支援非同步連接作業，呼叫**SQLBrowseConnect**， **SQLConnect**，或**SQLDriverConnect**將會失敗。  
  
 [5] 當 SQL_ATTR_AUTOCOMMIT 設定為 FALSE 時，如果應用程式應該呼叫 SQLEndTran(SQL_ROLLBACK) 任何 API 會傳回 SQL_ERROR，以確保交易一致性。  
  
 在中設定的資訊格式\* *ValuePtr*取決於指定的緩衝區*屬性*。 **SQLSetConnectAttr**會接受兩個不同的格式之一的屬性資訊： null 結束的字元字串或整數值。 屬性的描述中註明的每個格式。 字元字串所指向*ValuePtr*引數**SQLSetConnectAttr**具有長度*StringLength*位元組。  
  
 *StringLength*會忽略引數如果長度定義屬性，在此情況下，ODBC 2 中引進的所有屬性 *.x*或更早版本。  
  
|*Attribute*|*ValuePtr*內容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUINTEGER 值。 SQL_MODE_READ_ONLY 做驅動程式或資料來源的連線不需要支援會導致更新發生的 SQL 陳述式的指標。 這種模式可用來最佳化鎖定策略、 交易管理或其他適當的驅動程式或資料來源的區域。 若要避免這類陳述式提交給資料來源不需要的驅動程式。 驅動程式和資料來源時要求處理不是唯讀的唯讀狀態連線期間的 SQL 陳述式的行為是由實作定義。 預設值為 SQL_MODE_READ_WRITE。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|為事件處理常式的 SQLPOINTER 值。<br /><br /> 非同步函式完成的通知已藉由呼叫**SQLSetConnectAttr** SQL_ATTR_ASYNC_STMT_EVENT 屬性和指定的事件控制代碼。 **注意：** 資料指標程式庫不支援的通知方法。 如果它嘗試啟用的通知方法時啟用 SQLSetConnectAttr，透過資料指標程式庫，應用程式會收到錯誤訊息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|SQLUINTEGER 值啟用或停用的連接控制代碼上的選取函式的非同步執行。 如需詳細資訊，請參閱 <<c0> [ 非同步執行 （輪詢的方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 啟用指定的連接相關的函式的非同步作業。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = （預設值） 停用指定的連接相關的函式的非同步作業。<br /><br /> 設定 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 一定是同步 （亦即，它會永遠不會傳回 SQL_STILL_EXECUTING）。<br /><br /> 非同步執行的陳述式作業都與 sql_attr_async_enable 設定。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|Context 結構會指向 SQLPOINTER 值。<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**具有此屬性的函式。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|Context 結構會指向 SQLPOINTER 值。<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**具有此屬性的函式。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|SQLULEN 值，這個值指定是否要以非同步方式執行的陳述式指定的連接上呼叫的函式：<br /><br /> SQL_ASYNC_ENABLE_OFF = 停用連接層級的非同步執行支援的陳述式作業 （預設值）。<br /><br /> Sql_async_enable_on，然後 = 啟用連接層級的非同步執行的陳述式作業支援。<br /><br /> 這個屬性可以設定是否**SQLGetInfo** SQL_ASYNC_MODE 資訊類型會傳回 SQL_AM_CONNECTION 或 SQL_AM_STATEMENT。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|唯讀 SQLUINTEGER 值，指定是否在呼叫之後自動填入 IPD **SQLPrepare**支援：<br /><br /> SQL_TRUE = 呼叫之後，自動填入 IPD **SQLPrepare**支援的驅動程式。<br /><br /> SQL_FALSE = 呼叫之後，自動填入 IPD **SQLPrepare**驅動程式不支援。 不支援備妥陳述式的伺服器將無法自動填入 IPD。<br /><br /> 如果 SQL_ATTR_AUTO_IPD 連接屬性會傳回 SQL_TRUE，陳述式屬性 SQL_ATTR_ENABLE_AUTO_IPD 可以設定為開啟或關閉自動填入 IPD 中。 如果 SQL_ATTR_AUTO_IPD SQL_FALSE，SQL_ATTR_ENABLE_AUTO_IPD 無法設定為 SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD 的預設值等於 SQL_ATTR_AUTO_IPD 的值。<br /><br /> 可傳回此連接屬性**SQLGetConnectAttr**但不能設定**SQLSetConnectAttr**。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|SQLUINTEGER 值，這個值指定是否要使用自動認可] 或 [手動認可模式：<br /><br /> SQL_AUTOCOMMIT_OFF = 驅動程式會使用手動認可模式和應用程式必須明確地認可或回復交易**SQLEndTran**。<br /><br /> SQL_AUTOCOMMIT_ON = 驅動程式會使用自動認可模式。 立即在執行之後，就會認可每個陳述式。 這是預設值。 SQL_ATTR_AUTOCOMMIT 設定為 SQL_AUTOCOMMIT_ON 從手動認可模式變更為 自動認可模式時，會認可任何開啟的交易，在此連接上。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 認可模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要：** 某些資料來源刪除存取方案，並關閉資料指標陳述式是認可; 每次連接上所有陳述式自動認可模式可能會造成這種情形，每個 nonquery 陳述式之後，或關閉查詢。 如需詳細資訊，請參閱 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊中的和類型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)並[影響的資料指標和已備妥的陳述式上交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 批次執行時自動認可模式中，兩件事是可能的。 整個批次可以視為 autocommitable 單位，或批次中的每個陳述式會被視為 autocommitable 單位。 特定資料來源可以支援這兩種這些行為，而且可能會提供一種選擇其中一種。 它是驅動程式定義的批次會被視為 autocommitable 單元，或在批次中的每個個別陳述式是否 autocommitable。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|唯讀 SQLUINTEGER 值，指出連接的狀態。 如果 SQL_CD_TRUE，連線已遺失。 如果 SQL_CD_FALSE，連接仍然有效。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|SQLUINTEGER 值，對應到等候完成，然後再回到應用程式在連接上的任何要求的秒數。 驅動程式應該會傳回 SQLSTATE HYT00 （逾時過期），可能未與查詢執行或登入相關聯的情況下的逾時時間它在任何時候。<br /><br /> 如果*ValuePtr*會等於 0 （預設值），沒有任何逾時。|  
|SQL_ATTR_CURRENT_CATALOG (連接 ODBC 2.0)|字元字串，包含要供資料來源的目錄名稱。 例如，在 SQL Server 中，目錄是資料庫，因此驅動程式會將傳送**使用**_資料庫_陳述式，以資料來源，其中*資料庫*在指定的資料庫\* *ValuePtr*。 單層式架構的驅動程式，類別目錄可能是目錄，讓驅動程式會變更其目前的目錄中指定的目錄為 **ValuePtr*。|  
|SQL_ATTR_DBC_INFO_TOKEN (ODBC 3.8|用來設定的 SQLPOINTER 值回至雙位元組字元的連線資訊語彙基元控制代碼[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)的 (\**pRating*) 參數不等於 100。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 僅限集。 不可以使用**SQLGetConnectAttr**或是**SQLGetConnectOption**擷取此值。 驅動程式管理員**SQLSetConnectAttr**將不會接受 SQL_ATTR_DBC_INFO_TOKEN，因為應用程式不應將此屬性。<br /><br /> 如果驅動程式會傳回 SQL_ERROR，設定 SQL_ATTR_DBC_INFO_TOKEN 之後，只要從集區取得的連接會被釋放。 接著，驅動程式管理員將會嘗試從集區取得另一個連線。 請參閱[ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)如需詳細資訊。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|SQLPOINTER 值，指定是否要在由 Microsoft 元件服務所協調的分散式交易中使用的 ODBC 驅動程式。<br /><br /> 傳遞 DTC OLE 交易物件，指定要匯出至 SQL Server 或 sql_dtc_done 來結束連接的 DTC 關聯的交易。<br /><br /> 用戶端會呼叫 Microsoft 分散式交易協調器 (MS DTC) OLE itransactiondispenser:: Begintransaction 方法來開始 MS DTC 交易，並建立代表此交易的 MS DTC 交易物件。 接著，應用程式會呼叫 SQLSetConnectAttr SQL_ATTR_ENLIST_IN_DTC 選項與 ODBC 連接產生關聯的交易物件。 所有相關的資料庫活動都將在 MS DTC 交易的保護底下進行。 應用程式會呼叫使用 sql_dtc_done 來 SQLSetConnectAttr 來結束連接的 DTC 關聯。 如需詳細資訊，請參閱 MS DTC 文件集。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|SQLUINTEGER 值，對應至要等候完成，然後再回到應用程式的登入要求的秒數。 預設會驅動程式而異。 如果*ValuePtr*為 0、 停用逾時和連線嘗試會無限期等候。<br /><br /> 如果指定的逾時超過資料來源中的最大的登入逾時，驅動程式取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|決定如何處理目錄函數的字串引數的 SQLUINTEGER 值。<br /><br /> 如果 SQL_TRUE，目錄函數的字串引數會被視為識別碼。 如此並不重要。 針對了非分隔的字串，驅動程式會移除任何尾端的空格，並為大寫的字串摺疊。 針對分隔的字串，驅動程式會移除任何開頭或尾端空格，且實際上會就分隔符號之間的任何。 如果這些引數的其中一個設定為 null 指標，函式會傳回 SQL_ERROR 並 SQLSTATE HY009 （使用無效的 null 指標）。<br /><br /> 如果 SQL_FALSE，目錄函數的字串引數不會被視為識別碼。 案例很重要。 它們可以包含字串的搜尋模式，根據引數。<br /><br /> 預設值為 SQL_FALSE。<br /><br /> *TableType*引數**SQLTables**，後者會採用值的清單，不會影響這個屬性。<br /><br /> SQL_ATTR_METADATA_ID 也可以設定在陳述式層級上。 （它是唯一的連接屬性，同時也是陳述式屬性）。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|SQLULEN 值，指定驅動程式管理員如何使用 ODBC 資料指標程式庫：<br /><br /> SQL_CUR_USE_IF_NEEDED = 驅動程式管理員會使用 ODBC 資料指標程式庫，才需要它。 如果驅動程式支援 SQL_FETCH_PRIOR 選項**SQLFetchScroll**，驅動程式管理員使用的驅動程式的捲動功能。 否則，它會使用 ODBC 資料指標程式庫。<br /><br /> SQL_CUR_USE_ODBC = 驅動程式管理員會使用 ODBC 資料指標程式庫。<br /><br /> SQL_CUR_USE_DRIVER = 驅動程式管理員使用的驅動程式的捲動功能。 這是預設值。<br /><br /> 如需有關 ODBC 資料指標程式庫的詳細資訊，請參閱[附錄 f:ODBC 資料指標程式庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 **警告：** Windows 的未來版本將移除資料指標程式庫。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|SQLUINTEGER 值，指定網路封包大小 （位元組）。 **注意：** 許多資料來源可能是不支援此選項，或只傳回，但不是設定 network packet size。 <br /><br /> 如果指定的大小超過最大的封包大小，或小於最小的封包大小，此驅動程式取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 如果已建立連線之後，應用程式會設定封包大小，此驅動程式會傳回 SQLSTATE HY011 （屬性現在無法設定）。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|視窗控制代碼 (HWND)。<br /><br /> 如果是 null 指標的視窗控制代碼，驅動程式不會顯示任何對話方塊。<br /><br /> 如果視窗控制代碼不是 null 指標，它應該是應用程式的父視窗控制代碼。 這是預設值。 驅動程式會使用此控制代碼，來顯示對話方塊。 **注意：** SQL_ATTR_QUIET_MODE 連接屬性不適用於所顯示的對話方塊**SQLDriverConnect**。|  
|SQL_ATTR_TRACE (ODBC 1.0)|告知驅動程式管理員執行追蹤 SQLUINTEGER 值：<br /><br /> SQL_OPT_TRACE_OFF = off （預設值） 的追蹤<br /><br /> SQL_OPT_TRACE_ON = on 的追蹤<br /><br /> 開啟追蹤時，驅動程式管理員會寫入追蹤檔的每個 ODBC 函式呼叫。 **注意：** 開啟追蹤時，驅動程式管理員可以傳回 SQLSTATE IM013 （追蹤檔案時發生錯誤） 從任何函式。 <br /><br /> 應用程式使用 SQL_ATTR_TRACEFILE 選項，指定追蹤檔案。 如果檔案已經存在，則驅動程式管理員會附加到檔案。 否則，它會建立該檔案。 如果追蹤已開啟且已指定任何追蹤檔案，驅動程式管理員就會寫入 SQL 檔案。登入的根目錄。<br /><br /> 應用程式可設定變數**ODBCSharedTraceFlag**表示啟用動態追蹤。 然後啟用所有目前執行的 ODBC 應用程式的追蹤。 如果應用程式將會關閉追蹤，它會關閉僅對該應用程式。<br /><br /> 如果**追蹤**應用程式呼叫時，將會設定為 1 的系統資訊 中的關鍵字**SQLAllocHandle**具有*HandleType* SQL_HANDLE_ENV 的所有啟用追蹤控制代碼。 它只能針對呼叫應用程式已啟用**SQLAllocHandle**。<br /><br /> 呼叫**SQLSetConnectAttr**具有*屬性*SQL_ATTR_TRACE 的不需要*ConnectionHandle*引數是有效而且如果，則不會傳回 SQL_ERROR*ConnectionHandle*是 NULL。 此屬性套用至所有連線。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|Null 結束的字元字串，包含在追蹤檔案的名稱。<br /><br /> 指定 SQL_ATTR_TRACEFILE 屬性的預設值**TraceFile**系統資訊 中的關鍵字。 如需詳細資訊，請參閱 < [ODBC 子機碼](../../../odbc/reference/install/odbc-subkey.md)。<br /><br /> 呼叫**SQLSetConnectAttr**具有*屬性*SQL_ATTR_ TRACEFILE 的不需要*ConnectionHandle*為有效的引數而且如果，則不會傳回 SQL_ERROR*ConnectionHandle*無效。 此屬性套用至所有連線。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|Null 結束的字元字串，包含程式庫內含的函式名稱**SQLDriverToDataSource**並**SQLDataSourceToDriver**驅動程式存取以執行工作，例如字元集轉譯。 這個選項可能會指定是否驅動程式已連線到資料來源。 此屬性的設定會保存到連線。 如需有關轉譯資料的詳細資訊，請參閱[轉譯 Dll](../../../odbc/reference/develop-app/translation-dlls.md)並[轉譯 DLL 函式參考](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|32 位元旗標值傳遞至轉譯 DLL。 此屬性可指定是否驅動程式已連線到資料來源。 轉譯資料的相關資訊，請參閱[轉譯 Dll](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|32 位元的位元遮罩，以設定目前連接的交易隔離等級。 應用程式必須呼叫**SQLEndTran**認可或回復連線，然後再呼叫所有開啟的交易**SQLSetConnectAttr**使用此選項。<br /><br /> 有效值*ValuePtr*可藉由呼叫**SQLGetInfo**具有*資訊類型*SQL_TXN_ISOLATION_OPTIONS 相等。<br /><br /> 如需交易隔離等級的說明，請參閱 SQL_DEFAULT_TXN_ISOLATION 類型資訊，請在說明[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)並[交易隔離等級](../../../odbc/reference/develop-app/transaction-isolation-levels.md)。|  
  
 [1] 這些函式可以非同步呼叫，只有當描述項是實作描述項，不應用程式描述項。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
