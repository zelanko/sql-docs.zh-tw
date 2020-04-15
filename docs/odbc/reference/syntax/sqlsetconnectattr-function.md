---
title: SQLSetConnectAttr 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301934"
---
# <a name="sqlsetconnectattr-function"></a>SQLSetConnectAttr 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLSetConnectAttr**設置控制連接方面的屬性。  
  
> [!NOTE]
>  有關驅動程式管理員將此功能映射到 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式時的詳細資訊,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetConnectAttr(  
     SQLHDBC       ConnectionHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
 *屬性*  
 [輸入]要設置的屬性,列在"註釋"中。  
  
 *ValuePtr*  
 [輸入]指向要與*屬性*關聯的值的指標。 根據*屬性*的值 *,ValuePtr*將是一個未簽名的整數值,或將指向一個空端接的字串。 請注意,*屬性*參數的整數類型可能不是固定長度,請參閱註釋部分瞭解詳細資訊。  
  
 *字串長度*  
 [輸入]如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*指向字串或二進位緩衝區,則此參數應為 **ValuePtr*的長度。 對於字串資料,此參數應包含字串中的位元組數。  
  
 如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*是整數,則忽略*字串長度*。  
  
 如果*屬性*是驅動程式定義的屬性,則應用程式通過設置*StringLength*參數指示該屬性對驅動程式管理員的性質。 *字串長度*可以具有以下值:  
  
-   如果*ValuePtr*是指向字串的指標,則*StringLength*是字串的長度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*StringLength 中*。 這將在*字串長度*中放置負值。  
  
-   如果*ValuePtr*是指向字串或二進位元字串以外的值的指標,則*StringLength*應具有該值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定長度值,則*StringLength*會根據需要SQL_IS_INTEGER或SQL_IS_UINTEGER。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetConnectAttr**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_DBC的*句柄類型*和*連接句柄*的*句柄*。 下表列出了**SQLSetConnectAttr**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
 驅動程式可以返回SQL_SUCCESS_WITH_INFO以提供有關設置選項的結果的資訊。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|驅動程式不支援*ValuePtr*中指定的值,並替換了類似的值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08002|使用的連線名稱|*屬性*參數已SQL_ATTR_ODBC_CURSORS,並且驅動程式已連接到數據源。|  
|08003|連線未開啟|(DM) 指定了需要打開連接*的屬性*值,但*ConnectHandle*未處於連接狀態。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|*屬性*參數SQL_ATTR_CURRENT_CATALOG,並且結果集處於掛起狀態。|  
|25000|本地交易中的非法操作|當嘗試通過設置連接屬性SQL_ATTR_ENLIST_IN_DTC在分散式事務連接 (DTC) 中登記時,連接位於本地事務中。<br /><br /> 已在 DTC 中登記了連接。<br /><br /> 已登記在分散式事務連接中連接,並通過將SQL_ATTR_AUTOCOMMIT設置為SQL_AUTOCOMMIT_OFF啟動本地事務。|  
|3D000|無效目錄名稱|*屬性*參數SQL_CURRENT_CATALOG,指定的目錄名稱無效。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|為*連接句柄*啟用了非同步處理。 **SQLSetConnectAttr**函數被調用,在完成執行之前,在*ConnectHandle*上調用[了 SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md),然後在*ConnectHandle*上再次調用**SQLSetConnectAttr**函數。<br /><br /> 或者,調用**SQLSetConnectAttr**函數,在完成執行之前,SQLCancelHandle 是從多線程應用程式中的不同線程調用的**ConnectHandle。** *ConnectionHandle*|  
|HY009|不合法的空白指標|*屬性*參數標識了需要字串值的連接屬性 *,ValuePtr*參數為空指標。|  
|HY010|函式序列錯誤|(DM) 調用了與*ConnectHandle*關聯的*語句句柄*的非同步執行函數,並且在調用**SQLSetConnectAttr**時仍在執行。<br /><br /> (DM) 為*ConnectHandle*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用,用於與*連接句柄*關聯的語句句柄**SQLExecDirect**之一,並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用一個語句句柄,該*語句句柄*與*連接句柄*相關聯並返回SQL_NEED_DATA。 **SQLExecute** **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) **SQLBrowseConnect**被調用用於*連接句柄*並返回SQL_NEED_DATA。 在**SQLBrowseConnect**返回SQL_SUCCESS_WITH_INFO或SQL_SUCCESS之前調用此功能。|  
|HY011|無法立即設定屬性|*屬性*參數SQL_ATTR_TXN_ISOLATION,並且事務處於打開狀態。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY024|不合法屬性值|給定指定的*屬性*值,在*ValuePtr*中指定了無效值。 (驅動程式管理員僅對接受一組離散值(如SQL_ATTR_ACCESS_MODE或SQL_ATTR_ASYNC_ENABLE)的連接和語句屬性返回此 SQLSTATE。 對所有其他連線與敘述屬性,驅動程式必須驗證*ValuePtr*中指定的值 。<br /><br /> *屬性*參數是SQL_ATTR_TRACEFILE或*SQL_ATTR_TRANSLATE_LIB,ValuePtr*是一個空字串。|  
|HY090|不合法的字串或緩衝區長度|*(DM) \*ValuePtr*是一個字串,*字串長度*參數小於 0,但沒有SQL_NTS。|  
|HY092|不合法屬性/選項識別碼|(DM) 為參數*屬性*指定的值對驅動程式支援的 ODBC 版本無效。<br /><br /> (DM) 為參數*屬性*指定的值是唯讀屬性。|  
|HY114|驅動程式不支援連接層數執行|(DM) 應用程式嘗試為不支援非同步連接操作的驅動程式啟用具有SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE非同步函數執行。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HY121|無法同時啟用游標庫和驅動程式感知池|有關詳細資訊,請參閱[驅動程式感知連接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)。|  
|HYC00|沒有選擇選擇功能|為參數*屬性*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC 連接或語句屬性,但驅動程式不支援該驅動程式。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*連接句柄*關聯的驅動程式不支援該功能。|  
|IM009|無法載入轉換 DLL|驅動程式無法載入為連接指定的轉換 DLL。 僅當*屬性*SQL_ATTR_TRANSLATE_LIB時,才能返回此錯誤。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
|S1118|驅動程式不支援非同步通知|SQL_ATTR_ASYNC_DBC_EVENT已設置(在建立連接後),但驅動程式不支援非同步通知。|  
  
 當*屬性*是語句屬性時 **,SQLSetConnectAttr**可以返回**SQLSetStmtAttr**返回的任何 SQLStatEs。  
  
## <a name="comments"></a>註解  
 有關連線屬性的一般資訊,請參閱[連接屬性](../../../odbc/reference/develop-app/connection-attributes.md)。  
  
 當前定義的屬性及其引入的 ODBC 版本在本節後面的表中顯示;預計將定義更多的屬性以利用不同的數據來源。 ODBC 保留一系列屬性;驅動程式開發人員必須從 Open Group 為其特定於驅動程式使用保留值。  
  
> [!NOTE]
>  通過調用**SQLSetConnect Attr**在連接級別設置語句屬性的能力已在 ODBC 3 *.x*中被棄用。 ODBC 3 *.x*應用程式絕不應在連接級別設置語句屬性。 ODBC 3 *.x*語句屬性無法在連接級別設置,但SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE屬性除外,這些屬性既是連接屬性,也是語句屬性,可以在連接級別或語句級別設置。  
> 
>  ODBC 3 *.x*驅動程式僅需要支援此功能,如果它們應與在連接級別設置 ODBC 2 *.x*語句選項的 ODBC 2 *.x*應用程式配合使用。 有關詳細資訊,請參閱附錄 G 中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md):向後相容性的驅動程式指南。  
  
 應用程式可以在分配和釋放連接之間的任何時間調用**SQLSetConnect Attr。** 應用程式為連接成功設定的所有連接和語句屬性將一直持續到在連接上調用**SQLFreeHandle**為止。 例如,如果應用程式在連接到數據源之前調用**SQLSetConnectAttr,** 則即使**SQLSetConnectAttr**在驅動程式中失敗,當應用程式連接到數據來源時,該屬性也會保留。如果應用程式設置特定於驅動程式的屬性,則即使應用程式連接到連接上的不同驅動程式,該屬性也會保留。  
  
 某些連接屬性只能在建立連接之前進行設置;其他連接只能在建立連接後進行設置。 下表指示必須在建立連接之前或之後設置的連接屬性。 *任一表示*可以在連接之前或之後設置該屬性。  
  
|屬性|在連接之前還是之後設置?|  
|---------------|-------------------------------------|  
|SQL_ATTR_ACCESS_MODE|要麼[1]|  
|SQL_ATTR_ASYNC_DBC_EVENT|之前或之後|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE|要麼[4]|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK|之前或之後|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT|之前或之後|  
|SQL_ATTR_ASYNC_ENABLE|要麼[2]|  
|SQL_ATTR_AUTO_IPD|之前或之後|  
|SQL_ATTR_AUTOCOMMIT|要麼[5]|  
|SQL_ATTR_CONNECTION_DEAD|After|  
|SQL_ATTR_CONNECTION_TIMEOUT|之前或之後|  
|SQL_ATTR_CURRENT_CATALOG|要麼[1]|  
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
|SQL_ATTR_TXN_ISOLATION|要麼[3]|  
  
 [1] SQL_ATTR_ACCESS_MODE和SQL_ATTR_CURRENT_CATALOG可在連接之前或連接後設置,具體取決於驅動程式。 但是,可互通的應用程式在連接前設置它們,因為某些驅動程式不支援在連接後更改它們。  
  
 [2] SQL_ATTR_ASYNC_ENABLE必須在有活動語句之前設置。  
  
 {3} 僅當連接上沒有未結交易記錄時,才能設置SQL_ATTR_TXN_ISOLATION。 如果數據來源不支援\**ValuePtr*中指定的值,則某些連接屬性支援替換類似的值。 在這種情況下,驅動程式返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02(選項值已更改)。 例如,如果*屬性*為\**SQL_ATTR_PACKET_SIZE,ValuePtr*超過最大數據包大小,則驅動程式將替換最大大小。 要確定取代值,應用程式呼叫**SQLGetConnectAttr**。  
  
 [4] 如果在連接打開之前設置了SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE,則在調用**SQLBrowseConnect、SQLConnect**或**SQLDriverConnect**期間載入驅動程式時,**SQLConnect**驅動程式管理器將 設置驅動程式的屬性。 在調用**SQLBrowseConnect** **、SQLConnect**或**SQLDriverConnect**之前,驅動程式管理員不知道要連接到哪個驅動程式,也不知道驅動程式是否支援非同步連接操作。 因此,驅動程式管理器始終返回SQL_SUCCESS。 但是,如果驅動程式不支援非同步連接操作,則對**SQLBrowseConnect、SQLConnect**或**SQLConnect** **SQLDriverConnect**的呼叫將失敗。  
  
 [5] 當SQL_ATTR_AUTOCOMMIT設置為 FALSE 時,如果任何 API 返回SQL_ERROR以確保事務一致性,則應用程式應調用 SQLEndTran(SQL_ROLLBACK)。  
  
 \* *ValuePtr*緩衝區中設定的資訊格式來指定的*屬性*。 **SQLSetConnectAttr**將接受兩種不同格式之一的屬性資訊:空端字元字串或整數值。 每個格式在屬性的說明中註明。 **SQLSetConnectAttr** *的 ValuePtr*參數指向的字串的長度為*字串長度位元組*。  
  
 如果長度由屬性定義,則忽略*StringLength*參數,ODBC 2 *.x*或更早版本中引入的所有屬性就是這種情況。  
  
|*屬性*|*價值 Ptr*內容|  
|-----------------|-------------------------|  
|SQL_ATTR_ACCESS_MODE (ODBC 1.0)|SQLUinTEGER 值。 驅動程式或數據源使用SQL_MODE_READ_ONLY作為指示,指示不支援導致發生更新的 SQL 語句不需要連接。 此模式可用於優化鎖定策略、事務管理或驅動程式或數據源的其他領域。 不需要驅動程式來防止此類語句提交到數據源。 當要求驅動程式和數據源處理唯讀連接期間未讀的 SQL 語句時,驅動程式和數據來源的行為是實現定義的。 SQL_MODE_READ_WRITE為預設值。|  
|SQL_ATTR_ASYNC_DBC_EVENT (ODBC 3.8)|作為事件句柄的 SQLPOINTER 值。<br /><br /> 通過使用SQL_ATTR_ASYNC_STMT_EVENT屬性調用**SQLSetConnectAttr**並指定事件句柄,啟用非同步函數完成通知。 **註:** 游標庫不支援通知方法。 如果應用程式嘗試在啟用通知方法時通過 SQLSetConnectAttr 啟用游標庫,則會收到錯誤消息。|  
|SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE (ODBC 3.8)|啟用或禁用連接句柄上所選函數的非同步執行的 SQLUINTEGER 值。 有關詳細資訊,請參閱[非同步執行(輪詢方法)。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)<br /><br /> SQL_ASYNC_DBC_ENABLE_ON = 為指定的連接相關功能啟用非同步操作。<br /><br /> SQL_ASYNC_DBC_ENABLE_OFF = (預設) 停用指定連接相關函數的非同步操作。<br /><br /> 設置SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE始終是同步的(也就是說,它永遠不會返回SQL_STILL_EXECUTING)。<br /><br /> 使用SQL_ATTR_ASYNC_ENABLE啟用語句操作的非同步執行。|  
|SQL_ATTR_ASYNC_DBC_PCALLBACK (ODBC 3.8)|指向上下文結構的 SQLPOINTER 值。<br /><br /> 只有驅動程式管理器可以使用此屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_ASYNC_DBC_PCONTEXT (ODBC 3.8)|指向上下文結構的 SQLPOINTER 值。<br /><br /> 只有驅動程式管理器可以使用此屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 3.0)|SQLULEN 值,用於指定是否非同步執行使用指定連接上語句呼叫的函數:<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用語句操作的連接級非同步執行支援(預設值)。<br /><br /> SQL_ASYNC_ENABLE_ON = 為語句操作啟用連接級非同步執行支援。<br /><br /> 是否可以設置此屬性,無論是具有SQL_ASYNC_MODE資訊類型的**SQLGetInfo**返回SQL_AM_CONNECTION還是SQL_AM_STATEMENT。|  
|SQL_ATTR_AUTO_IPD (ODBC 3.0)|唯讀 SQLUINTEGER 值,用於指定是否支援呼叫**SQLPrepare**後 IPD 的自動填充:<br /><br /> SQL_TRUE = 驅動程式支援呼叫**SQLPrepare**後 IPD 的自動填充。<br /><br /> SQL_FALSE = 驅動程式不支援呼叫**SQLPrepare**後 IPD 的自動填充。 不支援準備好的語句的伺服器將無法自動填充 IPD。<br /><br /> 如果為SQL_ATTR_AUTO_IPD連接屬性返回SQL_TRUE,則可以將語句屬性SQL_ATTR_ENABLE_AUTO_IPD設置為打開或關閉 IPD 的自動填充。 如果SQL_ATTR_AUTO_IPDSQL_FALSE,則無法將SQL_ATTR_ENABLE_AUTO_IPD設置為SQL_TRUE。 SQL_ATTR_ENABLE_AUTO_IPD的預設值等於SQL_ATTR_AUTO_IPD的值。<br /><br /> 此連接屬性可以由**SQLGetConnectAttr**返回,但不能由**SQLSetConnectAttr**設置。|  
|SQL_ATTR_AUTOCOMMIT (ODBC 1.0)|指定使用自動提交模式還是手動提交模式的 SQLUINTEGER 值:<br /><br /> SQL_AUTOCOMMIT_OFF = 驅動程式使用手動提交模式,應用程式必須顯式提交或回滾**SQLEndTran**的事務。<br /><br /> SQL_AUTOCOMMIT_ON = 驅動程式使用自動提交模式。 每個語句在執行后立即提交。 這是預設值。 當SQL_ATTR_AUTOCOMMIT設置為 SQL_AUTOCOMMIT_ON從手動提交模式更改為自動提交模式時,將提交連接上的任何未結事務。<br /><br /> 有關詳細資訊,請參閱[提交模式](../../../odbc/reference/develop-app/commit-mode.md)。 **重要提示:** 在每次提交語句時,某些數據源都會刪除訪問計劃並關閉連接上所有語句的遊標;自動提交模式可能導致在執行每個非查詢語句或為查詢關閉游標時發生這種情況。 有關詳細資訊,請參閱[SQLGetInfo 中](../../../odbc/reference/syntax/sqlgetinfo-function.md)SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR資訊類型以及[事務對游標和準備敘述的影響](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。 <br /><br /> 當批處理在自動提交模式下執行時,有兩件事是可能的。 可以將整個批處理視為自動提交單元,或者批處理中的每個語句都被視為自動提交單元。 某些數據源可以同時支援這些行為,並可能提供一種選擇其中一種行為的方法。 它是驅動程式定義的是批處理是否被視為可自動提交單元,還是批處理中的每個語句都是可自動提交的。|  
|SQL_ATTR_CONNECTION_DEAD<br /><br /> (ODBC 3.5)|指示連接狀態的唯讀 SQLUINTE 格值。 如果SQL_CD_TRUE,連接已丟失。 如果SQL_CD_FALSE,則連接仍然處於活動狀態。|  
|SQL_ATTR_CONNECTION_TIMEOUT (ODBC 3.0)|SQLUINTEGER 值對應於等待連接上的任何請求完成,然後再返回到應用程式。 驅動程式應隨時返回 SQLSTATE HYT00(超時已過期),以便在與查詢執行或登錄無關的情況下超時。<br /><br /> 如果*ValuePtr*等於 0(預設值),則沒有超時。|  
|SQL_ATTR_CURRENT_CATALOG (ODBC 2.0)|包含資料來源要使用的目錄名稱的字串。 例如,在 SQL Server 中,目錄是一個資料庫,因此驅動程式向資料來源發送**USE**_資料庫_語句,其中*資料庫*是\**ValuePtr*中指定的資料庫。 對於單層驅動程式,目錄可能是目錄,因此驅動程式將其當前目錄更改為 [*ValuePtr*中指定的目錄》。|  
|SQL_ATTR_DBC_INFO_TOKEN(ODBC 3.8)|當[SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)\*的 (*pbb*) 參數不等於 100 時,用於將連接資訊權杖重新設定到 DBC 句柄的 SQLPOINTER 值。<br /><br /> SQL_ATTR_DBC_INFO_TOKEN是僅設置的。 無法使用**SQLGetConnect Attr**或**SQLGetConnectOption**檢索此值。 驅動程式管理員的**SQLSetConnectAttr**不會接受SQL_ATTR_DBC_INFO_TOKEN,因為應用程式不應設置此屬性。<br /><br /> 如果驅動程式在設置SQL_ATTR_DBC_INFO_TOKEN后返回SQL_ERROR,則剛剛從池中獲取的連接將被釋放。 然後,驅動程式管理器將嘗試從池中獲取另一個連接。 有關詳細資訊[,請參閱在 ODBC 驅動程式中開發連接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。|  
|SQL_ATTR_ENLIST_IN_DTC (ODBC 3.0)|SQLPOINTER 值,用於指定在Microsoft元件服務協調的分散式事務中是否使用ODBC驅動程式。<br /><br /> 傳遞指定要匯出到 SQL Server 的事務或SQL_DTC_DONE以結束連接的 DTC 關聯的 DTC OLE 事務物件。<br /><br /> 用戶端呼叫 Microsoft 分散式事務協調器 (MS DTC) OLE I交易分配器::開始事務方法以開始 MS DTC 事務並創建表示事務的 MS DTC 事務物件。 然後,應用程式使用SQL_ATTR_ENLIST_IN_DTC選項調用 SQLSetConnectAttr,以將事務物件與 ODBC 連接相關聯。 所有相關的資料庫活動都將在 MS DTC 交易的保護底下進行。 此應用程式會使用 SQL_DTC_DONE 來呼叫 SQLSetConnectAttr，以便結束連接的 DTC 關聯。 如需詳細資訊，請參閱 MS DTC 文件集。|  
|SQL_ATTR_LOGIN_TIMEOUT (ODBC 1.0)|SQLUINTEGER 值對應於等待登錄請求完成才能返回應用程式的秒數。 默認值與驅動程序相關。 如果*ValuePtr*為 0,則超時將禁用,連接嘗試將無限期等待。<br /><br /> 如果指定的超時超過數據源中的最大登錄超時,驅動程式將替換該值並返回 SQLSTATE 01S02(選項值已更改)。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|SQLUINTEGER 值,用於確定如何處理目錄函數的字串參數。<br /><br /> 如果SQL_TRUE,目錄函數的字串參數將被視為標識碼。 情況並不嚴重。 對於非分隔字串,驅動程式刪除任何尾隨空格,並將字串摺疊到大寫。 對於分隔字串,驅動程式刪除任何前導或尾隨空格,並從字面上獲取分隔符之間的任何內容。 如果這些參數之一設置為空指標,則函數將返回SQL_ERROR和 SQLSTATE HY009(無效使用空指標)。<br /><br /> 如果SQL_FALSE,目錄函數的字串參數不被視為標識碼。 案件意義重大。 它們可以包含字串搜索模式,也可以不包含字串搜索模式,具體取決於參數。<br /><br /> 默認值為SQL_FALSE。<br /><br /> **SQLTables**的*表類型*參數 (它採用值清單) 不受此屬性的影響。<br /><br /> 也可以在語句級別設置SQL_ATTR_METADATA_ID。 (它是唯一也是語句屬性的連接屬性。<br /><br /> 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_ODBC_CURSORS (ODBC 2.0)|指定驅動程式管理員如何使用 ODBC 游標庫的 SQLULEN 值:<br /><br /> SQL_CUR_USE_IF_NEEDED = 驅動程式管理員僅在需要時才使用 ODBC 游標庫。 如果驅動程式支援**SQLFetchScroll**中的SQL_FETCH_PRIOR選項,則驅動程式管理器將使用驅動程式的滾動功能。 否則,它使用ODBC游標庫。<br /><br /> SQL_CUR_USE_ODBC = 驅動程式管理員使用 ODBC 游標庫。<br /><br /> SQL_CUR_USE_DRIVER = 驅動程式管理器使用驅動程式的滾動功能。 這是預設值。<br /><br /> 有關 ODBC 游標庫的詳細資訊,請參閱[附錄 F:ODBC 游標庫](../../../odbc/reference/appendixes/appendix-f-odbc-cursor-library.md)。 **警告:** 游標庫將在將來版本的 Windows 中刪除。 避免在新的開發工作中使用此功能,並計劃修改當前使用此功能的應用程式。 Microsoft 建議使用驅動程式的游標功能。|  
|SQL_ATTR_PACKET_SIZE (ODBC 2.0)|指定以位元組為單位的網路數據包大小的 SQLUINTEGER 值。 **註:** 許多數據來源不支援此選項,或者只能返回但不設置網路封包大小。 <br /><br /> 如果指定大小超過最大數據包大小或小於最小數據包大小,驅動程式將替換該值並返回 SQLSTATE 01S02(選項值已更改)。<br /><br /> 如果應用程式在連接後設定數據包大小,驅動程式將返回 SQLSTATE HY011(現在無法設置屬性)。|  
|SQL_ATTR_QUIET_MODE (ODBC 2.0)|視窗句柄 (HWND)。<br /><br /> 如果視窗句柄為空指標,則驅動程式不顯示任何對話框。<br /><br /> 如果視窗句柄不是空指標,則應是應用程式的父視窗句柄。 這是預設值。 驅動程式使用此句柄顯示對話方塊。 **註:** 連接屬性SQL_ATTR_QUIET_MODE不適用於**SQLDriverConnect**顯示的對話方塊。|  
|SQL_ATTR_TRACE (ODBC 1.0)|SQLUINTEGER 值告訴驅動程式管理員是否執行追蹤:<br /><br /> SQL_OPT_TRACE_OFF = 追蹤關閉(預設值)<br /><br /> SQL_OPT_TRACE_ON = 上追蹤<br /><br /> 啟用追蹤時,驅動程式管理器將每個 ODBC 函數調用寫入跟蹤檔。 **註:** 啟用追蹤時,驅動程式管理器可以從任何函數返回 SQLSTATE IM013(跟蹤檔錯誤)。 <br /><br /> 應用程式指定具有SQL_ATTR_TRACEFILE選項的跟蹤檔。 如果檔已存在,驅動程式管理器將追加到該檔。 否則,它將創建該檔。 如果追蹤處於打開,並且未指定跟蹤檔,則驅動程式管理員將寫入檔案 SQL。在根目錄中登錄。<br /><br /> 應用程式可以設置變數**ODBCSharedTraceFlag**以動態啟用跟蹤。 然後,為當前運行的所有 ODBC 應用程式啟用追蹤。 如果應用程式關閉跟蹤,則僅關閉該應用程式。<br /><br /> 如果當應用程式使用*SQL_HANDLE_ENV 的句柄類型*調用**SQLAllocHandle**時,系統資訊中的**Trace**關鍵字設置為 1,則為所有句柄啟用跟蹤。 它僅為稱為**SQLAllocHandle**的應用程式啟用。<br /><br /> 使用SQL_ATTR_TRACE*屬性*調用**SQLSetConnectAttr**並不要求*連接句柄*參數有效,並且如果*連接句柄*為 NULL,則不會返回SQL_ERROR。 此屬性適用於所有連接。|  
|SQL_ATTR_TRACEFILE (ODBC 1.0)|包含追蹤檔名稱的 null 連接端字串。<br /><br /> SQL_ATTR_TRACEFILE屬性的預設值在系統資訊中使用**TraceFile**關鍵字指定。 有關詳細資訊,請參閱[ODBC 子鍵](../../../odbc/reference/install/odbc-subkey.md)。<br /><br /> 使用 SQL_ATTR_ TRACEFILE*的屬性*調用**SQLSetConnect Attr**不需要*連接句柄*參數有效,如果*連接句柄*無效,則不會返回SQL_ERROR。 此屬性適用於所有連接。|  
|SQL_ATTR_TRANSLATE_LIB (ODBC 1.0)|包含包含函數**SQLDriverToDataSource**和**SQLDataSourceToDriver**的庫名稱的 null 連接字串,驅動程式存取該字串以執行字元集轉換等任務。 僅當驅動程式已連接到數據源時,才能指定此選項。 此屬性的設置將在整個連接中保留。 有關翻譯資料的詳細資訊,請參考[DLL](../../../odbc/reference/develop-app/translation-dlls.md)和[翻譯 DLL 函式參考](../../../odbc/reference/syntax/translation-dll-api-reference.md)。|  
|SQL_ATTR_TRANSLATE_OPTION (ODBC 1.0)|傳遞給轉換 DLL 的 32 位標誌值。 僅當驅動程式已連接到數據源時,才能指定此屬性。 有關翻譯資料的資訊,請參考[DLL](../../../odbc/reference/develop-app/translation-dlls.md)。|  
|SQL_ATTR_TXN_ISOLATION (ODBC 1.0)|一個 32 位位元遮罩,用於設定當前連接的事務隔離等級。 應用程式必須調用**SQLEndTran**以提交或回滾連接上的所有打開的事務,然後再使用此選項調用**SQLSetConnectAttr。**<br /><br /> *ValuePtr*的有效值可以透過呼叫**SQLGetInfo**確定,*其資訊類型*等於SQL_TXN_ISOLATION_OPTIONS。<br /><br /> 有關事務隔離等級的說明,請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)和[事務隔離等級](../../../odbc/reference/develop-app/transaction-isolation-levels.md)中SQL_DEFAULT_TXN_ISOLATION資訊類型的說明。|  
  
 [1] 僅當描述符是實現描述符而不是應用程式描述符時,才能非同步調用這些函數。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|傳回連線屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
