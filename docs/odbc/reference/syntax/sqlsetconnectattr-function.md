---
title: SQLSetConnectAttr 函式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8424462ddde4f99196e26d633fddfa5bb2ed6ee9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301934"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函數
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**會設定控制連接層面的屬性。  
  
> [!NOTE]
>  如需 ODBC 3.x 應用程式與 ODBC 2.x*驅動程式搭配*使用時，驅動程式管理員將此函式對應至哪個 *.x*功能的詳細資訊，請參閱對應取代函式[以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
  
 *特性*  
 源要設定的屬性，列在 [批註] 中。  
  
 *ValuePtr*  
 源要與*屬性*相關聯之值的指標。 視*屬性*的值而定， *valueptr 是*會是不帶正負號的整數值，或會指向以 null 結束的字元字串。 請注意，*屬性*引數的整數類型可能不是固定長度，請參閱批註一節以取得詳細資料。  
  
 *StringLength*  
 源如果*attribute*是 ODBC 定義的屬性，而且*valueptr 是*指向字元字串或二進位緩衝區，則此引數應該是 **valueptr 是*的長度。 如果是字元字串資料，這個引數應該包含字串中的位元組數目。  
  
 如果*attribute*是 ODBC 定義的屬性，而*valueptr 是*是整數，則會忽略*StringLength* 。  
  
 如果*屬性*是驅動程式定義的屬性，則應用程式會藉由設定*StringLength*引數，來指出該屬性對驅動程式管理員的本質。 *StringLength*可以有下列值：  
  
-   如果*valueptr 是*是字元字串的指標，則*StringLength*是字串或 SQL_NTS 的長度。  
  
-   如果*valueptr 是*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR （*長度*）宏的結果放在*StringLength*中。 這會將負數值放在*StringLength*中。  
  
-   如果*valueptr 是*是字元字串或二進位字串以外的值指標，則*StringLength*應具有 SQL_IS_POINTER 的值。  
  
-   如果*valueptr 是*包含固定長度的值，則*StringLength*會適當地 SQL_IS_INTEGER 或 SQL_IS_UINTEGER。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConnectAttr**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_DBC *HandleType*和*ConnectionHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLSetConnectAttr**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
 驅動程式可以傳回 SQL_SUCCESS_WITH_INFO，以提供有關設定選項之結果的資訊。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援在*valueptr 是*中指定的值，並會取代類似的值。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08002|使用中的連接名稱|*屬性*引數已 SQL_ATTR_ODBC_CURSORS，且驅動程式已連接至資料來源。|  
|08003|連接未開啟|（DM）指定的*屬性*值需要開啟的連接，但*ConnectionHandle*不是處於線上狀態。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|*屬性*引數已 SQL_ATTR_CURRENT_CATALOG，且結果集暫止。|  
|25000|在本機交易中的作業不合法|嘗試在分散式交易連接（DTC）中登錄時，連接是在本機交易中，SQL_ATTR_ENLIST_IN_DTC 設定連接屬性。<br /><br /> 已在 DTC 中登錄連接。<br /><br /> 連接已經登錄在分散式交易連接中，而本機交易是藉由將 SQL_ATTR_AUTOCOMMIT 設定為 SQL_AUTOCOMMIT_OFF 來啟動。|  
|3D000|不正確目錄名稱|*屬性*引數已 SQL_CURRENT_CATALOG，且指定的目錄名稱無效。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*ConnectionHandle*的非同步處理。 已呼叫**SQLSetConnectAttr**函式，在完成執行之前，會在*ConnectionHandle*上呼叫[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)，然後在*ConnectionHandle*上再次呼叫**SQLSetConnectAttr**函數。<br /><br /> 或者，已呼叫**SQLSetConnectAttr**函式，在完成執行之前，會從多執行緒應用程式中的不同執行緒在*ConnectionHandle*上呼叫**SQLCancelHandle** 。|  
|HY009|Null 指標的使用不正確|*屬性*引數已識別出需要字串值的連接屬性，而且*valueptr 是*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）針對與*ConnectionHandle*相關聯的*StatementHandle*呼叫非同步執行的函式，且在呼叫**SQLSetConnectAttr**時仍在執行中。<br /><br /> （DM）已針對*ConnectionHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> 已針對與*ConnectionHandle*相關聯的其中一個語句控制碼呼叫（DM） **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對與*StatementHandle*相關聯的*ConnectionHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並 SQL_NEED_DATA 傳回。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。<br /><br /> 已針對*ConnectionHandle*呼叫（DM） **SQLBrowseConnect** ，並傳回 SQL_NEED_DATA。 在**SQLBrowseConnect**傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS 之前，會呼叫這個函式。|  
|HY011|無法立即設定屬性|*屬性*引數已 SQL_ATTR_TXN_ISOLATION，而交易已開啟。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY024|不正確屬性值|給定指定的*屬性*值，在*valueptr 是*中指定了不正確值。 （驅動程式管理員只會針對接受一組離散值的連接和語句屬性傳回此 SQLSTATE，例如 SQL_ATTR_ACCESS_MODE 或 SQL_ATTR_ASYNC_ENABLE。 對於所有其他連接和語句屬性，驅動程式必須確認*valueptr 是*中指定的值）。<br /><br /> *屬性*引數已 SQL_ATTR_TRACEFILE 或 SQL_ATTR_TRANSLATE_LIB，而*valueptr 是*是空字串。|  
|HY090|不正確字串或緩衝區長度|*（DM） \*valueptr 是*是字元字串，而*StringLength*引數小於0，但不 SQL_NTS。|  
|HY092|不正確屬性/選項識別碼|（DM）為引數*屬性*指定的值，對於驅動程式所支援的 ODBC 版本而言是不正確。<br /><br /> （DM）為引數*屬性*指定的值為唯讀屬性。|  
|HY114|驅動程式不支援連接層級的非同步函式執行|（DM）應用程式嘗試為不支援非同步連接作業的驅動程式，使用 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 來啟用非同步函數執行。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HY121|資料指標程式庫和可感知驅動程式的共用無法同時啟用|如需詳細資訊，請參閱可[感知驅動程式的連接](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)共用。|  
|HYC00|未執行的選擇性功能|為引數*屬性*指定的值，對於驅動程式所支援但不受驅動程式支援的 odbc 版本而言，是有效的 odbc 連接或語句屬性。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*ConnectionHandle*相關聯的驅動程式不支援此功能。|  
|IM009|無法載入轉譯 DLL|驅動程式無法載入為連接指定的轉譯 DLL。 只有在 SQL_ATTR_TRANSLATE_LIB*屬性*時，才會傳回此錯誤。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
|S1118|驅動程式不支援非同步通知|已設定 SQL_ATTR_ASYNC_DBC_EVENT （建立連接之後），但驅動程式不支援非同步通知。|  
  
 當*Attribute*是語句屬性時， **SQLSetConnectAttr**可能會傳回**SQLSetStmtAttr**傳回的任何 SQLSTATEs。  
  
## <a name="comments"></a>評價  
 如需連接屬性的一般資訊，請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 本章節稍後的表格會顯示目前定義的屬性及其引進的 ODBC 版本。預期會定義更多屬性以利用不同的資料來源。 屬性的範圍是由 ODBC 所保留。驅動程式開發人員必須從開啟的群組中，保留自己的驅動程式特有的值。  
  
> [!NOTE]
>  藉由呼叫**SQLSetConnectAttr**在連接層級設定語句屬性的功能，已在 ODBC 3.x 中被*取代。* ODBC 3.x*應用程式絕對*不應在連接層級設定語句屬性。 ODBC 3.x*語句屬性*無法在連接層級設定，但 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性除外，這兩者都是連接屬性和語句屬性，而且可以在連接層級或語句層級設定。  
> 
>  如果 ODBC*3.x 驅動程式*應該與在連接層級設定 odbc*2.x 語句選項*的 odbc*2.x 應用程式*搭配使用，則只需要支援這種功能。 如需詳細資訊，請參閱附錄 G：驅動程式方針中的[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)，以取得回溯相容性。  
  
 應用程式可以在配置和釋放連接之間的任何時間，隨時呼叫**SQLSetConnectAttr** 。 應用程式為連接成功設定的所有連接和語句屬性都會保存，直到在連接上呼叫**SQLFreeHandle**為止。 例如，如果應用程式在連接到資料來源之前呼叫**SQLSetConnectAttr** ，則即使在應用程式連接到資料來源時，如果驅動程式中的**SQLSetConnectAttr**失敗，屬性仍然會保存。如果應用程式設定驅動程式特有的屬性，即使應用程式連接到連接上的其他驅動程式，屬性仍會保存。  
  
 某些連接屬性只能在建立連接之前設定;只有在建立連接之後，才能設定其他專案。 下表指出必須在建立連接之前或之後設定的連接屬性。 *這兩個*指示可以在連接之前或之後設定屬性。  
  
|屬性|在連接之前或之後設定？|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|可能是 [1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之後|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|可能是 [4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之後|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之後|  
|SQL_ATTR_ASYNC_ENABLE|可能是 [2]|  
|SQL_ATTR_AUTO_IPD|之前或之後|  
|SQL_ATTR_AUTOCOMMIT|可能是 [5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之後|  
|SQL_ATTR_CURRENT_CATALOG|可能是 [1]|  
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
|SQL_ATTR_TXN_ISOLATION|可能是 [3]|  
  
 [1] SQL_ATTR_ACCESS_MODE 和 SQL_ATTR_CURRENT_CATALOG 可以在連接之前或之後設定，視驅動程式而定。 不過，互通的應用程式會在連接之前設定它們，因為某些驅動程式不支援在連接之後變更這些專案。  
  
 [2] 必須先設定 SQL_ATTR_ASYNC_ENABLE，才有作用中的語句。  
  
 [3] 只有在連接上沒有開啟的交易時，才能設定 SQL_ATTR_TXN_ISOLATION。 如果資料來源不支援\* *valueptr 是*中指定的值，某些連接屬性支援類似值的替代。 在這種情況下，驅動程式會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。 例如，如果 SQL_ATTR_PACKET_SIZE*屬性*，而\* *valueptr 是*超過封包大小上限，則驅動程式會替代大小上限。 為了判斷替代值，應用程式會呼叫**SQLGetConnectAttr**。  
  
 [4] 如果在開啟連接之前設定 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE，驅動程式管理員會在呼叫**SQLBrowseConnect**、 **SQLConnect**或**SQLDriverConnect**期間載入驅動程式時，設定驅動程式的屬性。 在呼叫**SQLBrowseConnect**、 **SQLConnect**或**SQLDriverConnect**之前，驅動程式管理員不知道要連接的驅動程式，也不知道驅動程式是否支援非同步連接作業。 因此，驅動程式管理員一律會傳回 SQL_SUCCESS。 但是，萬一驅動程式不支援非同步連接作業， **SQLBrowseConnect**、 **SQLConnect**或**SQLDriverConnect**的呼叫將會失敗。  
  
 [5] 當 SQL_ATTR_AUTOCOMMIT 設定為 FALSE 時，如果有任何 API 傳回 SQL_ERROR 以確保交易一致性，應用程式應該呼叫 SQLEndTran （SQL_ROLLBACK）。  
  
 \* *Valueptr 是*緩衝區中設定的資訊格式取決於指定的*屬性*。 **SQLSetConnectAttr**會以兩種不同格式的其中一種來接受屬性資訊：以 null 結束的字元字串或整數值。 屬性的描述中會注明每個的格式。 **SQLSetConnectAttr**的*valueptr 是*引數所指向的字元字串長度為*StringLength*個位元組。  
  
 如果長度是由屬性所定義，則會忽略*StringLength*引數，如同 ODBC*2.x 或更*早版本中引進之所有屬性的情況。  
  
|*特性*|*Valueptr 是*內容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE （ODBC 1.0）|SQLUINTEGER 值。 驅動程式或資料來源會使用 SQL_MODE_READ_ONLY 做為指標，表示不需要連接，即可支援導致更新發生的 SQL 語句。 此模式可以用來將鎖定策略、交易管理或其他適用于驅動程式或資料來源的區域優化。 不需要驅動程式，就能防止這類語句提交至資料來源。 當系統要求在唯讀連接期間處理不是唯讀的 SQL 語句時，驅動程式和資料來源的行為會定義為「執行」。 預設值為 SQL_MODE_READ_WRITE。|  
|SQL_ATTR_ASYNC_DBC_EVENT （ODBC 3.8）|屬於事件控制碼的 SQLPOINTER 值。<br /><br /> 藉由呼叫具有 SQL_ATTR_ASYNC_STMT_EVENT 屬性的**SQLSetConnectAttr**並指定事件控制碼，即可啟用非同步函式完成的通知。 **注意：** 資料指標程式庫不支援通知方法。 當啟用通知方法時，如果應用程式嘗試透過 SQLSetConnectAttr 啟用資料指標程式庫，將會收到錯誤訊息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE （ODBC 3.8）|SQLUINTEGER 值，可在連接控制碼上啟用或停用選取之函數的非同步執行。 如需詳細資訊，請參閱[非同步執行（輪詢方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 針對指定的連接相關函數啟用非同步作業。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = （預設）停用指定之連接相關函式的非同步作業。<br /><br /> 設定 SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE 一律是同步的（也就是永遠不會傳回 SQL_STILL_EXECUTING）。<br /><br /> 使用 SQL_ATTR_ASYNC_ENABLE 啟用語句作業的非同步執行。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK （ODBC 3.8）|指向內容結構的 SQLPOINTER 值。<br /><br /> 只有驅動程式管理員可以使用這個屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT （ODBC 3.8）|指向內容結構的 SQLPOINTER 值。<br /><br /> 只有驅動程式管理員可以使用這個屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_ASYNC_ENABLE （ODBC 3.0）|SQLULEN 值，指定在指定的連接上搭配語句呼叫的函數是否以非同步方式執行：<br /><br /> SQL_ASYNC_ENABLE_OFF = 針對語句作業停用連接層級非同步執行支援（預設值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 針對語句作業啟用連接層級非同步執行支援。<br /><br /> 您可以設定這個屬性，不論 SQL_ASYNC_MODE 資訊類型的**SQLGetInfo**會傳回 SQL_AM_CONNECTION 還是 SQL_AM_STATEMENT。|  
|SQL_ATTR_AUTO_IPD （ODBC 3.0）|唯讀 SQLUINTEGER 值，指定是否支援在呼叫**SQLPrepare**之後自動填入 IPD：<br /><br /> SQL_TRUE = 驅動程式支援**SQLPrepare**呼叫之後自動填入 IPD。<br /><br /> SQL_FALSE = 驅動程式不支援在呼叫**SQLPrepare**之後自動填入 IPD。 不支援備妥語句的伺服器將無法自動填入 IPD。<br /><br /> 如果 SQL_ATTR_AUTO_IPD 連接屬性傳回 SQL_TRUE，則可以將語句屬性 SQL_ATTR_ENABLE_AUTO_IPD 設定為開啟或關閉 IPD 的自動填入。 如果 SQL_ATTR_AUTO_IPD 是 SQL_FALSE，SQL_ATTR_ENABLE_AUTO_IPD 無法設定為 SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD 的預設值等於 SQL_ATTR_AUTO_IPD 的值。<br /><br /> 這個連接屬性可以由**SQLGetConnectAttr**傳回，但無法由**SQLSetConnectAttr**設定。|  
|SQL_ATTR_AUTOCOMMIT （ODBC 1.0）|SQLUINTEGER 值，指定是否要使用自動認可或手動認可模式：<br /><br /> SQL_AUTOCOMMIT_OFF = 驅動程式會使用手動認可模式，而且應用程式必須使用**SQLEndTran**明確認可或回復交易。<br /><br /> SQL_AUTOCOMMIT_ON = 驅動程式會使用自動認可模式。 每個語句會在執行後立即認可。 這是預設值。 當 SQL_ATTR_AUTOCOMMIT 設定為 SQL_AUTOCOMMIT_ON 從手動認可模式變更為自動認可模式時，就會認可連接上的任何開啟的交易。<br /><br /> 如需詳細資訊，請參閱[認可模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要事項：** 某些資料來源會刪除存取計畫，並在每次認可語句時，關閉連接上所有語句的資料指標;自動認可模式可能會導致這種情況發生在每個 nonquery 語句執行之後，或當查詢的資料指標關閉時。 如需詳細資訊，請參閱 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[對資料指標和準備語句的交易影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 在自動認可模式中執行批次時，可能會發生兩件事。 整個批次可以視為 autocommitable 單位，或批次中的每個語句視為 autocommitable 單位。 某些資料來源可以同時支援這兩種行為，並可提供選擇其中一個的方式。 不論是將批次視為 autocommitable 單位，或批次中的每個個別語句是否 autocommitable，都是驅動程式定義的。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> （ODBC 3.5）|唯讀 SQLUINTEGER 值，指出連接的狀態。 如果 SQL_CD_TRUE，連接就會遺失。 如果 SQL_CD_FALSE，連接仍在使用中。|  
|SQL_ATTR_CONNECTION_TIMEOUT （ODBC 3.0）|SQLUINTEGER 值，對應至要等候連接完成的任何要求，然後再返回應用程式的秒數。 此驅動程式應該會在任何情況下傳回 SQLSTATE HYT00 （超時時間已過期），這可能會在未與查詢執行或登入相關聯的情況中發生。<br /><br /> 如果*valueptr 是*等於0（預設值），則不會有任何 timeout。|  
|SQL_ATTR_CURRENT_CATALOG （ODBC 2.0）|包含資料來源所要使用之目錄名稱的字元字串。 例如，在 SQL Server 中，目錄是資料庫，因此，驅動程式會將**USE** _database_語句傳送到資料來源，其中*database*是\* *valueptr 是*中指定的資料庫。 若是單層驅動程式，目錄可能是目錄，因此驅動程式會將其目前目錄變更為 **valueptr 是*中指定的目錄。|  
|SQL_ATTR_DBC_INFO_TOKEN （ODBC 3。8|當[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)的（\**pRating*）參數不等於100時，用來將連接資訊 token 設回 DBC 控制碼的 SQLPOINTER 值。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN 僅限設定。 不可能使用**SQLGetConnectAttr**或**SQLGetConnectOption**來抓取此值。 因為應用程式不應設定此屬性，所以驅動程式管理員的**SQLSetConnectAttr**將不會接受 SQL_ATTR_DBC_INFO_TOKEN。<br /><br /> 如果在設定 SQL_ATTR_DBC_INFO_TOKEN 之後，驅動程式會傳回 SQL_ERROR，則只會釋放從集區取得的連接。 然後，驅動程式管理員會嘗試從集區取得另一個連接。 如需詳細資訊，請參閱[在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|SQL_ATTR_ENLIST_IN_DTC （ODBC 3.0）|SQLPOINTER 值，指定是否要在由 Microsoft 元件服務協調的分散式交易中使用 ODBC 驅動程式。<br /><br /> 傳遞 DTC OLE transaction 物件，以指定要匯出至 SQL Server 的交易，或 SQL_DTC_DONE 以結束連線的 DTC 關聯。<br /><br /> 用戶端會呼叫 Microsoft 分散式交易協調器（MS DTC） OLE ITransactionDispenser：： BeginTransaction 方法來開始 MS DTC 交易，並建立代表交易的 MS DTC 交易對象。 然後，應用程式會使用 SQL_ATTR_ENLIST_IN_DTC 選項呼叫 SQLSetConnectAttr，使交易對象與 ODBC 連接產生關聯。 所有相關的資料庫活動都將在 MS DTC 交易的保護底下進行。 此應用程式會使用 SQL_DTC_DONE 來呼叫 SQLSetConnectAttr，以便結束連接的 DTC 關聯。 如需詳細資訊，請參閱 MS DTC 文件集。|  
|SQL_ATTR_LOGIN_TIMEOUT （ODBC 1.0）|SQLUINTEGER 值，對應至等候登入要求完成的秒數，然後再返回應用程式。 預設值為 [驅動程式相依]。 如果*valueptr 是*為0，則會停用超時，而連線嘗試會無限期等候。<br /><br /> 如果指定的超時時間超過資料來源中的登入超時上限，則驅動程式會替代該值，並傳回 SQLSTATE 01S02 （已變更的選項值）。|  
|SQL_ATTR_METADATA_ID （ODBC 3.0）|決定如何處理目錄函數之字串引數的 SQLUINTEGER 值。<br /><br /> 如果 SQL_TRUE，則會將目錄函數的字串引數視為識別碼。 這種情況並不重要。 若為 nondelimited 字串，驅動程式會移除任何尾端空格，而字串會折迭為大寫。 若為分隔字串，驅動程式會移除任何開頭或尾端空格，並以字面意義地接受分隔符號之間的任何字元。 如果其中一個引數設定為 null 指標，此函式會傳回 SQL_ERROR 並 SQLSTATE HY009 （null 指標的用法無效）。<br /><br /> 如果 SQL_FALSE，則不會將目錄函式的字串引數視為識別碼。 這種情況很重要。 視引數而定，它們可以包含字串搜尋模式。<br /><br /> 預設值為 SQL_FALSE。<br /><br /> **SQLTables**的*TableType*引數（接受值清單）不會受到此屬性的影響。<br /><br /> 您也可以在語句層級上設定 SQL_ATTR_METADATA_ID。 （這是唯一同時為語句屬性的連接屬性）。<br /><br /> 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS （ODBC 2.0）|指定驅動程式管理員如何使用 ODBC 資料指標程式庫的 SQLULEN 值：<br /><br /> SQL_CUR_USE_IF_NEEDED = 驅動程式管理員僅在需要時才使用 ODBC 資料指標程式庫。 如果驅動程式支援**SQLFetchScroll**中的 SQL_FETCH_PRIOR 選項，驅動程式管理員會使用驅動程式的滾動功能。 否則，它會使用 ODBC 資料指標程式庫。<br /><br /> SQL_CUR_USE_ODBC = 驅動程式管理員使用 ODBC 資料指標程式庫。<br /><br /> SQL_CUR_USE_DRIVER = 驅動程式管理員會使用驅動程式的滾動功能。 這是預設值。<br /><br /> 如需有關 ODBC 資料指標程式庫的詳細資訊，請參閱[附錄 F： odbc 資料指標程式庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 **警告：** 在未來的 Windows 版本中，將會移除資料指標程式庫。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。|  
|SQL_ATTR_PACKET_SIZE （ODBC 2.0）|指定網路封包大小（以位元組為單位）的 SQLUINTEGER 值。 **注意：** 許多資料來源都不支援此選項，或只能傳回但不會設定網路封包大小。 <br /><br /> 如果指定的大小超過封包大小上限或小於最小封包大小，則驅動程式會替代該值，並傳回 SQLSTATE 01S02 （已變更的選項值）。<br /><br /> 如果應用程式在建立連接之後設定封包大小，驅動程式會傳回 SQLSTATE HY011 （現在無法設定屬性）。|  
|SQL_ATTR_QUIET_MODE （ODBC 2.0）|視窗控制碼（HWND）。<br /><br /> 如果視窗控制碼是 null 指標，驅動程式不會顯示任何對話方塊。<br /><br /> 如果視窗控制碼不是 null 指標，它應該是應用程式的父視窗控制碼。 這是預設值。 驅動程式會使用此控制碼來顯示對話方塊。 **注意：** SQL_ATTR_QUIET_MODE 連接屬性不適用於**SQLDriverConnect**所顯示的對話方塊。|  
|SQL_ATTR_TRACE （ODBC 1.0）|SQLUINTEGER 值，告訴驅動程式管理員是否要執行追蹤：<br /><br /> SQL_OPT_TRACE_OFF = 關閉追蹤（預設值）<br /><br /> SQL_OPT_TRACE_ON = 追蹤<br /><br /> 當追蹤開啟時，驅動程式管理員會將每個 ODBC 函式呼叫寫入追蹤檔案。 **注意：** 當追蹤開啟時，驅動程式管理員可以從任何函式傳回 SQLSTATE IM013 （追蹤檔案錯誤）。 <br /><br /> 應用程式會使用 [SQL_ATTR_TRACEFILE] 選項來指定追蹤檔案。 如果檔案已經存在，驅動程式管理員會附加至檔案。 否則，它會建立檔案。 如果追蹤已開啟且未指定任何追蹤檔，驅動程式管理員會寫入至檔案 SQL。登入根目錄。<br /><br /> 應用程式可以設定變數**ODBCSharedTraceFlag** ，以動態方式啟用追蹤。 接著會針對目前正在執行的所有 ODBC 應用程式啟用追蹤。 如果應用程式關閉追蹤，它只會針對該應用程式關閉。<br /><br /> 當應用程式以 SQL_HANDLE_ENV 的*HandleType*呼叫**SQLAllocHandle**時，如果系統資訊中的**Trace**關鍵字設為1，則會針對所有控制碼啟用追蹤。 只有呼叫**SQLAllocHandle**的應用程式才會啟用此功能。<br /><br /> 使用 SQL_ATTR_TRACE 的*屬性*呼叫**SQLSetConnectAttr**不需要有效的*ConnectionHandle*引數，而且如果*ConnectionHandle*為 Null，則不會傳回 SQL_ERROR。 這個屬性會套用至所有連接。|  
|SQL_ATTR_TRACEFILE （ODBC 1.0）|以 null 結束的字元字串，包含追蹤檔的名稱。<br /><br /> SQL_ATTR_TRACEFILE 屬性的預設值是以系統資訊中的**TRACEFILE**關鍵字指定。 如需詳細資訊，請參閱[ODBC](../../../odbc/reference/install/odbc-subkey.md)子機碼。<br /><br /> 使用 SQL_ATTR_ TRACEFILE 的*屬性*呼叫**SQLSetConnectAttr**不需要有效的*ConnectionHandle*引數，也不會在*ConnectionHandle*無效時傳回 SQL_ERROR。 這個屬性會套用至所有連接。|  
|SQL_ATTR_TRANSLATE_LIB （ODBC 1.0）|以 null 結束的字元字串，其中包含包含**SQLDriverToDataSource**和**SQLDataSourceToDriver**函式的程式庫名稱，而驅動程式會存取這些函式來執行字元集轉譯之類的工作。 只有當驅動程式已連接到資料來源時，才能指定此選項。 這個屬性的設定會跨連接保存。 如需翻譯資料的詳細資訊，請參閱[轉譯 dll](../../../odbc/reference/develop-app/translation-dlls.md)和[轉譯 dll 函數參考](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION （ODBC 1.0）|傳遞至轉譯 DLL 的32位旗標值。 只有當驅動程式已連接到資料來源時，才能指定這個屬性。 如需翻譯資料的詳細資訊，請參閱[轉譯 dll](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION （ODBC 1.0）|32位位元遮罩，可設定目前連接的交易隔離等級。 應用程式必須呼叫**SQLEndTran** ，才能在使用此選項呼叫**SQLSetConnectAttr**之前，認可或回復連接上所有開啟的交易。<br /><br /> 藉由呼叫**SQLGetInfo**並將*InfoType*等於 SQL_TXN_ISOLATION_OPTIONS，即可判斷*valueptr 是*的有效值。<br /><br /> 如需交易隔離等級的描述，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[交易隔離等級](../../../odbc/reference/develop-app/transaction-isolation-levels.md)中的 SQL_DEFAULT_TXN_ISOLATION 資訊類型的描述。|  
  
 [1] 只有當描述項是一個執行描述項，而不是應用程式描述項時，才能以非同步方式呼叫這些函數。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
