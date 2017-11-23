---
title: "SQLSetStmtAttr 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetStmtAttr
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetStmtAttr
helpviewer_keywords: SQLSetStmtAttr function [ODBC]
ms.assetid: 7abc5260-733a-48d4-9974-2d1a6a9ea5f6
caps.latest.revision: "32"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 6fb9cd848463d0315d42b49f42e690f1bd7e47b0
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**設定相關的陳述式的屬性。  
  
> [!NOTE]  
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC 3*.x*應用程式使用 ODBC 2*.x*驅動程式，請參閱[向後的對應取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Attribute*  
 [輸入]選項可用來設定，列在 [意見]。  
  
 *ValuePtr*  
 [輸入]相關聯的值*屬性*。 值而定*屬性*， *ValuePtr*將會是下列其中一項：  
  
-   ODBC 描述項控制代碼。  
  
-   SQLUINTEGER 值。  
  
-   SQLULEN 值。  
  
-   下列其中一種指標：  
  
    -   以 null 結束的字元字串。  
  
    -   二進位的緩衝區。  
  
    -   值或陣列類型是 SQLLEN、 SQLULEN 或 SQLUSMALLINT。  
  
    -   驅動程式所定義的值。  
  
 如果*屬性*引數是驅動程式專屬值*ValuePtr*可能是帶正負號的整數。  
  
 *StringLength*  
 [輸入]如果*屬性*是 ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*屬性*是 ODBC 定義的屬性和*ValuePtr*是整數， *StringLength*會被忽略。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*StringLength*引數。 *StringLength*可以是下列值：  
  
-   如果*ValuePtr*是字元字串的指標，則*StringLength*是 SQL_NTS 之字串的長度。  
  
-   如果*ValuePtr*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR 結果 (*長度*) 中的巨集*StringLength*。 這樣做會放在負值*StringLength*。  
  
-   如果*ValuePtr*是字元字串或二進位字串以外的值的指標，則*StringLength*應該有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定長度的值，則*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetStmtAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**與*HandleType*的 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetStmtAttr** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02 的警告|選項值已變更|驅動程式不支援指定的值*ValuePtr*，或是在指定的值*ValuePtr*不實作的工作狀況，造成無效，因此驅動程式取代相似的值。 (**SQLGetStmtAttr**可以呼叫以判斷暫時替代的值。)取代值無效， *StatementHandle*直到資料指標已關閉，此時陳述式屬性會還原為先前的值。 陳述式屬性可以變更為：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|*屬性*SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR 或 SQL_ATTR_USE_BOOKMARKS，且資料指標為開啟。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY009|無效的 null 指標使用|*屬性*引數識別必要的字串屬性，為陳述式屬性和*ValuePtr*引數為 null 指標。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLSetStmtAttr**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY011|現在無法設定屬性|*屬性*SQL_ATTR_CONCURRENCY、 SQL_ ATTR_CURSOR_TYPE、 SQL_ ATTR_SIMULATE_CURSOR 或 SQL_ ATTR_USE_BOOKMARKS 和已備妥的陳述式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY017|使用自動配置描述項控制代碼無效|(DM)*屬性*引數是 SQL_ATTR_IMP_ROW_DESC 或 SQL_ATTR_IMP_PARAM_DESC。<br /><br /> (DM)*屬性*引數以前是 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，並在值*ValuePtr*原本以外的控制代碼執行隱含配置描述項控制代碼配置給 ARD 或 APD。|  
|HY024|屬性值無效|提供給指定*屬性*值，指定了無效的值中*ValuePtr*。 （驅動程式管理員會傳回這個僅適用於連接和陳述式屬性接受一組離散值，例如 SQL_ATTR_ACCESS_MODE 或 SQL_ ATTR_ASYNC_ENABLE 的 SQLSTATE。 對於所有其他連接和陳述式屬性，驅動程式必須確認中指定的值*ValuePtr*。)<br /><br /> *屬性*引數是 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，和*ValuePtr*已明確配置描述項控制代碼會做為相同的連接*StatementHandle*引數。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*ValuePtr*是字元字串，而*StringLength*引數為小於 0，但不是 SQL_NTS。|  
|HY092|屬性/選項識別碼無效|(DM) 指定的引數的值*屬性*對 ODBC 驅動程式支援的版本無效。<br /><br /> (DM) 指定的引數的值*屬性*唯讀屬性。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*驅動程式支援 ODBC 的版本，但不支援此驅動程式是有效的 ODBC 陳述式屬性。<br /><br /> *屬性*引數以前是 SQL_ATTR_ASYNC_ENABLE，而呼叫**SQLGetInfo**與*資訊類型*SQL_ASYNC_MODE 傳回 SQL_AM_CONNECTION。<br /><br /> *屬性*引數是 SQL_ATTR_ENABLE_AUTO_IPD，而 SQL_ATTR_AUTO_IPD 連接屬性的值是 SQL_FALSE。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|S1118|驅動程式不支援非同步通知|如果呼叫**SQLSetStmtAttr**設定 SQL_ATTR_ASYNC_STMT_EVENT; 驅動程式不支援非同步通知。|  
  
## <a name="comments"></a>註解  
 陳述式的陳述式屬性都有效，除非有變更的另一個呼叫**SQLSetStmtAttr**或直到陳述式會卸除呼叫**SQLFreeHandle**。 呼叫**SQLFreeStmt** SQL_CLOSE、 SQL_UNBIND，或 SQL_RESET_PARAMS 選項不會重陳述式屬性。  
  
 如果資料來源不支援指定的值，某些陳述式屬性支援值相似的替代*ValuePtr*。 在這種情況下，驅動程式會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。 例如，如果*屬性*是 SQL_ATTR_CONCURRENCY 和*ValuePtr*就 SQL_CONCUR_ROWVER，且如果資料來源不支援這，驅動程式取代 SQL_CONCUR_VALUES 傳回 SQL_SUCCESS_WITH_INFO。 若要判斷替代的值，應用程式呼叫**SQLGetStmtAttr**。  
  
 資訊的格式設定與*ValuePtr*取決於指定*屬性*。 **SQLSetStmtAttr**接受屬性中有兩種不同格式的資訊： 字元字串或整數值。 每個格式註屬性的描述中。 此格式適用於每個屬性中傳回的資訊**SQLGetStmtAttr**。 字元字串所指向*ValuePtr*引數的**SQLSetStmtAttr**長度為*StringLength*。  
  
> [!NOTE]  
>  能夠在連接層級設定陳述式屬性，藉由呼叫**SQLSetConnectAttr**已被取代，在 ODBC 3*.x*。 ODBC 3*.x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC 3*.x*陳述式屬性不能在連接層級，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 」 屬性，這些連接屬性和陳述式屬性，同時也可以設定在連接層級或陳述式層級設定。  
  
> [!NOTE]  
>  ODBC 3*.x*驅動程式只需要支援這項功能，如果應使用 ODBC 2*.x*應用程式，設定 ODBC 2*.x*連接層級的陳述式選項。 如需詳細資訊，請參閱 「 設定陳述式選項在連接層級 」 下[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中附錄 g： 驅動程式的指導方針回溯相容性。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>設定描述項欄位的陳述式屬性  
 許多陳述式屬性會對應至描述元的標頭欄位。 設定這些屬性實際上結果的描述項欄位的設定。 藉由呼叫設定欄位**SQLSetStmtAttr**而不是為**SQLSetDescField**描述項控制代碼並沒有取得函式呼叫的優點。  
  
> [!CAUTION]  
>  呼叫**SQLSetStmtAttr**為一個陳述式可能會影響其他陳述式。 會發生這種情況是當 APD 或陳述式相關聯的 ARD 明確配置，而且也與其他陳述式相關聯。 因為**SQLSetStmtAttr**修改 APD 或 ARD，所做的修改套用至與此描述元相關聯的所有陳述式。 如果這不是必要的行為，應用程式應該中斷關聯此描述元的陳述式 (藉由呼叫**SQLSetStmtAttr**設為不同的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 欄位描述項控制代碼） 然後再呼叫**SQLSetStmtAttr**一次。  
  
 當描述項欄位設定對應的陳述式屬性所設定的結果時，只會針對適用的描述項所識別的陳述式目前相關聯的設定欄位*StatementHandle*引數，以及屬性設定不會影響任何可能在未來該陳述式相關聯的描述元。 當呼叫所設定，同時也是陳述式屬性描述項欄位**SQLSetDescField**，對應的陳述式屬性設定。 如果明確配置描述項分開的陳述式，陳述式屬性對應至標頭欄位將還原為隱含地配置描述項欄位的值。  
  
 當配置陳述式 (請參閱[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md))，四個描述項控制代碼會自動配置和陳述式相關聯。 明確配置描述項控制代碼可以透過呼叫陳述式相關聯**SQLAllocHandle**與*fHandleType*的配置描述項控制代碼，然後呼叫SQL_HANDLE_DESC**SQLSetStmtAttr**與陳述式的描述項控制代碼。  
  
 下表中的陳述式屬性對應至描述項標頭欄位。  
  
|陳述式屬性|標頭欄位|Desc。|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|ARD|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|ARD|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|ARD|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|ARD|  
|SQL_ATTR_ROW_STATUS_PTR 設定|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>陳述式屬性  
 下列表格中會顯示目前定義的屬性和這些功能的 ODBC 版本預期更多屬性將會定義驅動程式，以善用不同的資料來源。 ODBC; 保留範圍的屬性驅動程式開發人員必須保留自己從開啟 群組的特定驅動程式使用的值。 如需詳細資訊，請參閱[驅動程式特定資料類型，描述元類型、 資訊類型、 診斷的型別，以及屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|Attribute|*ValuePtr*內容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|APD 中的後續呼叫的控制代碼**SQLExecute**和**SQLExecDirect**陳述式控制代碼上。 這個屬性的初始值會是一開始會配置陳述式時，隱含地配置描述項。 如果這個屬性的值設為 SQL_NULL_DESC 或原先配置描述元的控制代碼，先前的陳述式控制代碼關聯的明確配置的 APD 控制代碼分開，而且陳述式控制代碼會還原成隱含地配置 APD 控制代碼。<br /><br /> 無法將設定這個屬性，隱含地配置給另一個陳述式的描述項控制代碼或隱含地設定相同的陳述式; 的另一個描述元控制代碼隱含地配置描述項控制代碼無法與多個陳述式或描述項控制代碼相關聯。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|針對後續的提取陳述式控制代碼上 ARD 控制代碼。 這個屬性的初始值會是一開始會配置陳述式時，隱含地配置描述項。 如果這個屬性的值設為 SQL_NULL_DESC 或原先配置描述元的控制代碼，先前的陳述式控制代碼關聯的明確配置的 ARD 控制代碼分開，而且陳述式控制代碼會還原成隱含地配置 ARD 控制代碼。<br /><br /> 無法將設定這個屬性，隱含地配置給另一個陳述式的描述項控制代碼或隱含地設定相同的陳述式; 的另一個描述元控制代碼隱含地配置描述項控制代碼無法與多個陳述式或描述項控制代碼相關聯。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|SQLULEN 值，指定是否要以非同步方式執行指定的陳述式以呼叫的函式：<br /><br /> SQL_ASYNC_ENABLE_OFF = 停用陳述式的支援層級的非同步執行 （預設值）。<br /><br /> 請 = 啟用陳述式層級的非同步執行的支援。<br /><br /> 如需詳細資訊，請參閱[非同步執行 （輪詢方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> 陳述式層級的非同步執行支援的驅動程式，陳述式屬性 SQL_ATTR_ASYNC_ENABLE 為唯讀。 其值為具有相同名稱的連接層級屬性的值相同時，會配置陳述式控制代碼。<br /><br /> 呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_ASYNC_ENABLE 設定時 SQL_ASYNC_MODE*資訊類型*傳回 SQL_AM_CONNECTION 傳回 SQLSTATE HYC00 （未實作的選擇性功能）。 如需詳細資訊，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)如需詳細資訊。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|為事件處理常式的 SQLPOINTER 值。<br /><br /> 完成的非同步函式的通知已啟用藉由呼叫**SQLSetStmtAttr**設定**SQL_ATTR_ASYNC_STMT_EVENT**屬性，指定事件處理常式。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|SQLPOINTER 非同步回呼函式。<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**以這個屬性的函式。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|SQLPOINTER 內容結構<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**以這個屬性的函式。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|指定資料指標並行 SQLULEN 值：<br /><br /> SQL_CONCUR_READ_ONLY = 資料指標是唯讀的。 不允許的任何更新。<br /><br /> SQL_CONCUR_LOCK = 資料指標會使用鎖定不足以確保可以更新資料列的最低層級。<br /><br /> SQL_CONCUR_ROWVER = 資料指標使用開放式並行存取控制，比較資料列版本，例如 SQLBase ROWID 或 Sybase 時間戳記。<br /><br /> SQL_CONCUR_VALUES = 資料指標使用開放式並行存取控制，比較值。<br /><br /> 預設值為 sql_attr_concurrency 設定為 SQL_CONCUR_READ_ONLY。<br /><br /> 這個屬性不能指定為開啟的資料指標。 如需詳細資訊，請參閱[並行類型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果 SQL_ATTR_CURSOR_TYPE*屬性*變更成不支援 SQL_ATTR_CONCURRENCY 的目前值的類型，sql_attr_concurrency 設定的值將會變更在執行時間，以及當發出警告**SQLExecDirect**或**SQLPrepare**呼叫。<br /><br /> 如果驅動程式支援**SELECT FOR UPDATE**陳述式，這類陳述式執行時，值的 SQL_ATTR_CONCURRENCY 設定為 SQL_CONCUR_READ_ONLY，將會傳回錯誤。 如果 sql_attr_concurrency 設定的值變更為 的 SQL_ATTR_CURSOR_TYPE 某些值，但不適用於 SQL_ATTR_CURSOR_TYPE 的目前值，此驅動程式支援的值，將變更的 SQL_ATTR_CURSOR_TYPE 值在執行階段和 SQLSTATE 01s02 的警告（選項值已變更） 時發出**SQLExecDirect**或**SQLPrepare**呼叫。<br /><br /> 如果資料來源不支援指定的並行，驅動程式會替代不同的並行存取，並傳回 SQLSTATE 01S02 （選項值已變更）。 對於 SQL_CONCUR_VALUES 驅動程式會取代 SQL_CONCUR_ROWVER，反之亦然。 對於 SQL_CONCUR_LOCK，驅動程式取代，在 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES 的順序。 直到執行時間，不會檢查替代值的有效性。<br /><br /> 如需 SQL_ATTR_CONCURRENCY 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性以及資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|指定應用程式需要的支援層級的 SQLULEN 值。 設定這個屬性會影響後續呼叫**SQLExecDirect**和**SQLExecute**。<br /><br /> SQL_NONSCROLLABLE = Scrollable 資料指標並不需要陳述式控制代碼。 如果應用程式呼叫**SQLFetchScroll**此控制代碼的唯一有效的值上*Sqlfetchscroll*是 SQL_FETCH_NEXT。 這是預設值。<br /><br /> SQL_SCROLLABLE = Scrollable 資料指標所需的陳述式控制代碼。 當呼叫**SQLFetchScroll**，應用程式可能指定的任何有效的值*Sqlfetchscroll*，達到資料指標定位在非循序模式的模式。<br /><br /> 如需可捲動資料指標的詳細資訊，請參閱[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需 SQL_ATTR_CURSOR_SCROLLABLE 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性以及資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|SQLULEN 值，指定資料指標陳述式控制代碼上的是否顯示另一個資料指標設定至結果所做的變更。 設定這個屬性會影響後續呼叫**SQLExecDirect**和**SQLExecute**。 應用程式可以讀取傳回的值，這個屬性，以取得其初始狀態或其狀態為最最近的應用程式設定。<br /><br /> SQL_UNSPECIFIED = 未指定資料指標類型為何，而是否資料指標陳述式控制代碼上的顯示結果集，另一個資料指標所做的變更。 資料指標陳述式控制代碼上的進行可能會看見無、 某些或所有這類變更。 這是預設值。<br /><br /> SQL_INSENSITIVE = 任何其他資料指標所所有資料指標陳述式控制代碼顯示結果集而不會反映對其進行任何變更。 非感應式資料指標是唯讀的。 這會對應至靜態資料指標，具有僅供唯讀並行存取。<br /><br /> SQL_SENSITIVE = 陳述式控制代碼進行顯示另一個資料指標所設定的所有變更結果的所有資料指標。<br /><br /> 如需 SQL_ATTR_CURSOR_SENSITIVITY 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性以及資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|指定資料指標類型的 SQLULEN 值：<br /><br /> SQL_CURSOR_FORWARD_ONLY = 資料指標唯一捲動向前復原。<br /><br /> SQL_CURSOR_STATIC = 資料的結果集是靜態。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 此驅動程式會儲存和使用該索引鍵之 SQL_ATTR_KEYSET_SIZE 陳述式屬性中指定的資料列數目。<br /><br /> SQL_CURSOR_DYNAMIC = 此驅動程式會儲存，並使用資料列集中的資料列的索引鍵。<br /><br /> 預設值是 SQL_CURSOR_FORWARD_ONLY。 已備妥的 SQL 陳述式之後，不能指定這個屬性。<br /><br /> 如果資料來源不支援指定的資料指標類型，驅動程式會替代不同的資料指標類型，並傳回 SQLSTATE 01S02 （選項值已變更）。 對於混合或動態資料指標，此驅動程式替代，順序的索引鍵集衍生或靜態資料指標。 對於索引鍵集驅動資料指標時，驅動程式會取代靜態資料指標。<br /><br /> 如需可捲動資料指標類型的詳細資訊，請參閱[可捲動資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 如需 SQL_ATTR_CURSOR_TYPE 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性以及資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|指定是否要執行自動母體擴展的 IPD SQLULEN 值：<br /><br /> SQL_TRUE = 呼叫之後自動母體擴展 IPD 開啟**SQLPrepare**。 SQL_FALSE = 關閉呼叫之後自動母體擴展 IPD **SQLPrepare**。 (應用程式仍然可以藉由呼叫取得 IPD 欄位資訊**SQLDescribeParam**，如果支援。)預設值的陳述式屬性 SQL_ATTR_ENABLE_AUTO_IPD 為 SQL_FALSE。 如需詳細資訊，請參閱[IPD 的自動擴展](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|SQLLEN \* ，它會指向二進位的書籤值。 當**SQLFetchScroll**呼叫*fFetchOrientation*等於 SQL_FETCH_BOOKMARK，驅動程式收取書籤值，此欄位中。 此欄位預設為 null 指標。 如需詳細資訊，請參閱[捲動書籤](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 此欄位所指向的值不供刪除書籤、 書籤，來更新或擷取書籤中被作業**SQLBulkOperations**，會使用快取資料列集的緩衝區中的書籤。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD 控制代碼。 這個屬性的值是一開始會配置陳述式時，配置描述項。 應用程式無法將此屬性。<br /><br /> 這個屬性可以擷取由呼叫**SQLGetStmtAttr**但未設定呼叫**SQLSetStmtAttr**。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD 控制代碼。 這個屬性的值是一開始會配置陳述式時，配置描述項。 應用程式無法將此屬性。<br /><br /> 這個屬性可以擷取由呼叫**SQLGetStmtAttr**但未設定呼叫**SQLSetStmtAttr**。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|指定索引鍵集驅動資料指標索引鍵中的資料列數目 SQLULEN。 如果索引鍵集大小為 0 （預設值），游標會是完整的索引鍵集驅動。 如果索引鍵集大小大於 0，資料指標被混合 （索引鍵集內索引鍵集驅動和動態外部索引鍵集）。 預設索引鍵集大小為 0。 如需索引鍵集驅動資料指標的詳細資訊，請參閱[索引鍵集衍生資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定的大小超過最大索引鍵集大小，驅動程式會取代該大小，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> **SQLFetch**或**SQLFetchScroll**索引鍵集大小大於 0 且小於資料列集大小，才會傳回錯誤。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|指定驅動程式會傳回字元或二進位資料行中的資料的最大數量的 SQLULEN 值。 如果*ValuePtr*小於可用的資料長度**SQLFetch**或**SQLGetData**截斷的資料，並傳回 SQL_SUCCESS。 如果*ValuePtr*是 0 （預設值），驅動程式會嘗試傳回所有可用的資料。<br /><br /> 如果指定的長度小於最小的資料來源可以傳回的資料量或大於最大資料量，可以傳回的資料來源，驅動程式取代的值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 這個屬性的值可以設定上開啟的資料指標。不過，設定可能不會立即生效，在這種情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更） 和重設為其原始值的屬性。<br /><br /> 此屬性為了降低網路流量，並應該在資料來源 （而不是驅動程式） 中的多層式驅動程式可以實作它時，才支援。 這項機制不應由應用程式截斷資料。若要截斷接收資料，應用程式應該指定最大緩衝區長度，以*Columnsize*引數中的**SQLBindCol**或**SQLGetData**。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|對應至要傳回的應用程式進行的資料列數目上限 SQLULEN 值**選取**陳述式。 如果\* *ValuePtr*等於 0 （預設值），驅動程式會傳回所有資料列。<br /><br /> 這個屬性被用來減少網路流量。 就概念而言，它會套用時建立結果集，並限制結果集第一個*ValuePtr*資料列。 如果結果集中的資料列數目大於*ValuePtr*，會截斷結果集。<br /><br /> SQL_ATTR_MAX_ROWS 適用於所有結果集上*陳述式*，包括所傳回的目錄函數。 SQL_ATTR_MAX_ROWS 會建立最大值的資料指標資料列計數。<br /><br /> 驅動程式應該不會模擬 SQL_ATTR_MAX_ROWS 行為**SQLFetch**或**SQLFetchScroll** （如果結果集大小的限制不能實作在資料來源） 如果不能保證該 SQL_ATTR_MAX_ROWS 會正確地實作。<br /><br /> 它是由驅動程式定義 SQL_ATTR_MAX_ROWS 是否適用於 SELECT 陳述式 （例如目錄函數） 以外的陳述式。<br /><br /> 這個屬性的值可以設定上開啟的資料指標。不過，設定可能不會立即生效，在這種情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更） 和重設為其原始值的屬性。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|判斷目錄函數的字串引數的處理方式 SQLULEN 值。<br /><br /> 如果 SQL_TRUE，目錄函數的字串引數會被視為識別項。 大小寫並不重要。 了非分隔的字串，請移除任何尾端的空格，驅動程式和字串會摺成大寫。 分隔的字串，請移除任何開頭或尾端空格，驅動程式，並只採用任何常值是與分隔符號之間。 如果其中一個這些引數設定為 null 指標，此函數會傳回 SQL_ERROR 並 SQLSTATE HY009 （使用無效的 null 指標）。<br /><br /> 如果 SQL_FALSE，目錄函數的字串引數不會視為識別項。 案例很重要。 它們可以包含字串的搜尋模式，根據的引數。<br /><br /> 預設值為 SQL_FALSE。<br /><br /> *TableType*引數的**SQLTables**，其可接受的值，清單不會受到這個屬性。<br /><br /> SQL_ATTR_METADATA_ID 也可以設定在連接層級上。 （它並 SQL_ATTR_ASYNC_ENABLE 是同時為連接屬性的唯一陳述式屬性）。<br /><br /> 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|SQLULEN 值，指出驅動程式是否應該掃描 SQL 字串的逸出序列：<br /><br /> SQL_NOSCAN_OFF = 驅動程式掃描 SQL 字串的逸出序列 （預設值）。<br /><br /> SQL_NOSCAN_ON = 驅動程式不會掃描 SQL 字串的逸出序列。 相反地，驅動程式陳述式將直接傳送至資料來源。<br /><br /> 如需詳細資訊，請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 位移新增至變更繫結的動態參數的指標所指向的值。 如果此欄位為非 null，此驅動程式會取值指標、 將已取值的值加入至每個延遲欄位 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 描述項記錄中並使用新的指標值繫結時。 它會設定預設為 null。<br /><br /> 繫結位移是一律直接加入 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位。 如果位移變更為不同的值，新的值仍然會加入直接到描述項欄位中的值。 新的位移不會加入至欄位值加上任何先前的位移。<br /><br /> 如需詳細資訊，請參閱[參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_BIND_OFFSET_PTR 欄位 APD 標頭中。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|指出要用於動態參數繫結方向 SQLULEN 值。<br /><br /> 此欄位設為 SQL_PARAM_BIND_BY_COLUMN （預設值），來選取資料行取向的繫結。<br /><br /> 若要選取資料列取向的繫結，此欄位設定為結構或緩衝區一組動態參數繫結的執行個體的長度。 這個長度會包含所有繫結的參數以及結構或緩衝區，確保當繫結參數的位址會隨著指定的長度，結果將會為相同的參數在接下來的開頭的任何填補的空間一組參數。 當使用*sizeof* ANSI C 中的運算子，保證此行為。<br /><br /> 如需詳細資訊，請參閱[繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_ BIND_TYPE 欄位 APD 標頭中。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*值指向 SQLUSMALLINT 值的陣列，用來在執行 SQL 陳述式的期間略過參數。 每個值設定為 SQL_PARAM_PROCEED （適用於執行參數） 或 SQL_PARAM_IGNORE （適用於的參數被忽略）。<br /><br /> 一組參數可以在處理期間略過 SQL_DESC_ARRAY_STATUS_PTR 至 SQL_PARAM_IGNORE APD 中所指陣列中設定狀態的值。 如果其狀態的值設定為 SQL_PARAM_PROCEED，或設定陣列中的任何項目，則會處理一組參數。<br /><br /> 此陳述式屬性可以設為 null 指標，在其中案例驅動程式不會傳回參數的狀態值。 這個屬性可以設定在任何時間，但不是會使用新的值必須等到下次**SQLExecDirect**或**SQLExecute**呼叫。<br /><br /> 沒有任何繫結的參數時，會忽略此屬性。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_ARRAY_STATUS_PTR 欄位 APD 標頭中。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 陣列所指向的值包含值的狀態資訊每個資料列的參數值呼叫後**SQLExecute**或**SQLExecDirect**。 只有當 PARAMSET_SIZE 大於 1 時，才需要此欄位。<br /><br /> Status 值可以包含下列值：<br /><br /> SQL_PARAM_SUCCESS： 這組參數成功執行的 SQL 陳述式。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO: SQL 陳述式已成功執行這組參數。不過，警告資訊是可用於診斷資料結構。<br /><br /> SQL_PARAM_ERROR： 有錯誤發生在處理這個參數的集合。 使用診斷資料結構中的其他錯誤資訊。<br /><br /> SQL_PARAM_UNUSED： 這個參數集是未使用，可能是因為，某些先前的參數集造成錯誤中止進一步處理，或因為 SQL_PARAM_IGNORE 已設定該 SQL_ATTR_PARAM_ 所指定之陣列中的參數集OPERATION_PTR。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE： 驅動程式的參數陣列視為一個龐大的單位，因此不會產生此層級的資訊時發生錯誤。<br /><br /> 此陳述式屬性可以設為 null 指標，在其中案例驅動程式不會傳回參數的狀態值。 這個屬性可以設定在任何時間，但不是會使用新的值必須等到下次**SQLExecute**或**SQLExecDirect**呼叫。 請注意，將此屬性設定可能會影響驅動程式所實作的輸出參數行為。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_ARRAY_STATUS_PTR 欄位 IPD 標頭中。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|SQLULEN\*資料錄欄位指向之緩衝區中要傳回的已處理，包括錯誤集的參數集的數目。 如果這是 null 指標，將會傳回沒有數字。<br /><br /> 此陳述式屬性設定 SQL_DESC_ROWS_PROCESSED_PTR 欄位 IPD 標頭中。<br /><br /> 如果呼叫**SQLExecDirect**或**SQLExecute** ，在這個屬性所指向之緩衝區的填滿不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容是未定義。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|指定每個參數的值數目的 SQLULEN 值。 如果則 sql_attr_paramset_size 會大於 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR APD 要的點陣列。 每個陣列之基數等於這個欄位的值。<br /><br /> 沒有任何繫結的參數時，會忽略此屬性。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定此陳述式屬性設定的 SQL_DESC_ARRAY_SIZE 欄位 APD 標頭中。|  
|SQL_ATTR_QUERY_TIMEOUT 時 (ODBC 1.0)|對應的 SQL 陳述式執行傳回至應用程式之前等待的秒數 SQLULEN 值。 如果*ValuePtr*是等於 0 （預設值），還有不會逾時。<br /><br /> 如果指定的逾時超過資料來源中的最大逾時或小於最小的逾時， **SQLSetStmtAttr**用取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 請注意，應用程式不需要呼叫**SQLCloseCursor**重複使用陳述式，如果**選取**陳述式已逾時。<br /><br /> 此陳述式屬性中設定的查詢逾時是在同步與非同步模式中有效。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 值：<br /><br /> SQL_RD_ON = **SQLFetchScroll**和在 ODBC 3*.x*， **SQLFetch**擷取資料之後，它會將游標放到指定的位置。 這是預設值。<br /><br /> SQL_RD_OFF = **SQLFetchScroll**和在 ODBC 3*.x*， **SQLFetch**之後將游標置於不擷取資料。<br /><br /> 設定 SQL_RD_OFF SQL_RETRIEVE_DATA，應用程式可以驗證的資料列存在，或擷取的資料列的書籤，而不會造成擷取資料列的負擔。 如需詳細資訊，請參閱[捲動和提取資料列](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 這個屬性的值可以設定上開啟的資料指標。不過，設定可能不會立即生效，在這種情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更） 和重設為其原始值的屬性。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|指定每次呼叫所傳回的資料列數目的 SQLULEN 值**SQLFetch**或**SQLFetchScroll**。 它也是陣列中的書籤中用於大量書籤作業使用的資料列數目**SQLBulkOperations**。 預設值是 1。<br /><br /> 如果指定的資料列集大小超過資料來源所支援的最大資料列集大小，此驅動程式用取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 如需詳細資訊，請參閱[資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 設定此陳述式屬性設定的 SQL_DESC_ARRAY_SIZE 欄位 ARD 標頭中。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 位移新增至變更繫結的資料行的資料指標所指向的值。 如果此欄位為非 null，此驅動程式會取值指標、 將已取值的值加入至每個延遲欄位 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 描述項記錄中並使用新的指標值繫結時。 它會設定預設為 null。<br /><br /> 此陳述式屬性設定 SQL_DESC_BIND_OFFSET_PTR 欄位 ARD 標頭中。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|SQLULEN 值，這個繫結方向設定的值時使用**SQLFetch**或**SQLFetchScroll**相關的陳述式上呼叫。 資料行取向繫結會選取此值設定為 SQL_BIND_BY_COLUMN。 資料列取向繫結會選取此值設定為結構或緩衝區，其中會繫結結果資料行的執行個體的長度。<br /><br /> 如果指定的長度，則它必須包含所有繫結的資料行以及結構或緩衝區，確保當繫結的資料行的位址會隨著指定的長度，結果將會為第的相同資料行的開頭的任何填補的空間e 的下一個資料列。 當使用**sizeof**保證具有結構或等位在 ANSI C 中的運算子，這種行為。<br /><br /> 資料行取向繫結則是預設值繫結方向**SQLFetch**和**SQLFetchScroll**。<br /><br /> 如需詳細資訊，請參閱[繫結區塊資料指標搭配使用的資料行](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_BIND_TYPE 欄位 ARD 標頭中。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|是整個結果中的目前資料列數目 SQLULEN 值設定。 如果無法判斷目前的資料列數目，或目前沒有資料列，則驅動程式會傳回 0。<br /><br /> 這個屬性可以擷取由呼叫**SQLGetStmtAttr**但未設定呼叫**SQLSetStmtAttr**。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*值指向 SQLUSMALLINT 值的陣列，用來使用大量作業期間忽略的資料列**SQLSetPos**。 每個值設定為 SQL_ROW_PROCEED （適用於大量作業中包含的資料列） 或 SQL_ROW_IGNORE （適用於大量作業要排除的資料列）。 (不忽略資料列，藉由呼叫期間使用這個陣列**SQLBulkOperations**。)<br /><br /> 此陳述式屬性可以將 null 指標，驅動程式的情況下不會傳回資料列狀態的值。 這個屬性可以設定在任何時間，但不是會使用新的值必須等到下次**SQLSetPos**呼叫。<br /><br /> 如需詳細資訊，請參閱[更新 SQLSetPos 與資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)和[SQLSetPos 與資料列集刪除資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_ARRAY_STATUS_PTR 欄位中 ARD。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 陣列所指向的值之後呼叫值包含資料列狀態值**SQLFetch**或**SQLFetchScroll**。 陣列中有資料列集內有資料列的元素。<br /><br /> 此陳述式屬性可以將 null 指標，驅動程式的情況下不會傳回資料列狀態的值。 這個屬性可以設定在任何時間，但不是會使用新的值必須等到下次**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**呼叫。<br /><br /> 如需詳細資訊，請參閱[編號的擷取資料列和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_ARRAY_STATUS_PTR 欄位 IRD 標頭中。<br /><br /> 這個屬性由 ODBC 2 對應*.x*驅動程式新增至*rgbRowStatus*的呼叫中的陣列**SQLExtendedFetch**。|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|SQLULEN\*值指向的緩衝區中要傳回其呼叫之後擷取的資料列數目， **SQLFetch**或**SQLFetchScroll**; 執行的大量作業所影響的資料列數目藉由呼叫**SQLSetPos**與*作業*SQL_REFRESH; 或由執行大量作業所影響的資料列數目的引數**SQLBulkOperations**. 這個數目包括錯誤資料列。<br /><br /> 如需詳細資訊，請參閱[編號的擷取資料列和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 此陳述式屬性設定 SQL_DESC_ROWS_PROCESSED_PTR 欄位 IRD 標頭中。<br /><br /> 如果呼叫**SQLFetch**或**SQLFetchScroll** ，在這個屬性所指向之緩衝區的填滿不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容是未定義。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|指定驅動程式的模擬定位的 update 和 delete 陳述式是否保證，這類陳述式會影響只有一個單一資料列的 SQLULEN 值。<br /><br /> 若要模擬定位的 update 和 delete 陳述式，大多數的驅動程式建構搜尋**更新**或**刪除**陳述式包含**其中**指定子句目前的資料列中每個資料行的值。 這些資料行組成的唯一索引鍵，除非這類陳述式可能會影響多個資料列。<br /><br /> 若要保證，這類陳述式會影響只有一個資料列，驅動程式會判斷唯一索引鍵中的資料行，並將這些資料行加入至結果集。 如果應用程式可保證結果集中的資料行組成的唯一索引鍵時，若要這樣做不需要的驅動程式。 這可能會降低執行時間。<br /><br /> SQL_SC_NON_UNIQUE = 驅動程式並不保證模擬定位更新或 delete 陳述式將會影響只有一個資料列。是應用程式的責任，若要這樣做。 如果陳述式會影響多個資料列， **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**傳回 SQLSTATE 01001 （資料指標作業衝突）。<br /><br /> SQL_SC_TRY_UNIQUE = 則驅動程式會嘗試保證，模擬定位更新或刪除陳述式會影響只有一個資料列。 驅動程式一律會執行這類陳述式，即使它們可能會影響多個資料列，例如當沒有唯一索引鍵。 如果陳述式會影響多個資料列， **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**傳回 SQLSTATE 01001 （資料指標作業衝突）。<br /><br /> SQL_SC_UNIQUE = 驅動程式可確保模擬定位的更新或刪除陳述式會影響只有一個資料列。 如果驅動程式指定的陳述式中，無法保證此**SQLExecDirect**或**SQLPrepare**會傳回錯誤。<br /><br /> 如果資料來源提供原生 SQL 支援定位的 update 和 delete 陳述式和驅動程式不會模擬資料指標，SQL_SC_UNIQUE 為 SQL_SIMULATE_CURSOR 要求時，會傳回 SQL_SUCCESS。 如果要求 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE 時，會傳回 SQL_SUCCESS_WITH_INFO。 如果資料來源提供的支援 SQL_SC_TRY_UNIQUE 層級，並在驅動程式不會傳回 SQL_SUCCESS，SQL_SC_TRY_UNIQUE 和 SQL_SUCCESS_WITH_INFO 會傳回如 SQL_SC_NON_UNIQUE。<br /><br /> 如果資料來源不支援指定的資料指標模擬類型，驅動程式會替代不同的模擬類型，並傳回 SQLSTATE 01S02 （選項值已變更）。 對於 SQL_SC_UNIQUE，驅動程式取代，在 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE 的順序。 對於 SQL_SC_TRY_UNIQUE，驅動程式會取代 SQL_SC_NON_UNIQUE。<br /><br /> 預設為 SQL_SC_UNIQUE。<br /><br /> 如需詳細資訊，請參閱[模擬定位的更新和刪除陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|指定應用程式是否會使用與資料指標的書籤 SQLULEN 值：<br /><br /> SQL_UB_OFF = Off （預設值）<br /><br /> SQL_UB_VARIABLE = 應用程式將會與資料指標中，使用書籤和驅動程式會提供可變長度的書籤，並支援。 在 ODBC 3 已被取代 SQL_UB_FIXED*.x*。 ODBC 3*.x*應用程式應該一律使用可變長度的書籤，即使在使用 ODBC 2*.x*驅動程式 （可支援只有 4 個位元組，固定長度的書籤）。 這是因為固定長度的書籤是只可變長度的書籤的特殊案例。 使用 ODBC 2 時*.x*驅動程式，驅動程式管理員就會將 SQL_UB_VARIABLE 對應至 SQL_UB_FIXED。<br /><br /> 若要使用與資料指標的書籤，應用程式必須 SQL_UB_VARIABLE 值指定此屬性之前開啟資料指標。<br /><br /> 如需詳細資訊，請參閱[擷取書籤](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [1] 這些函式可以非同步方式呼叫，只有當描述元是實作描述項，不應用程式的描述項。  
  
 請參閱[資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)和[資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定的單一欄位的描述元|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
