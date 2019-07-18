---
title: SQLSetStmtAttr 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetStmtAttr
helpviewer_keywords:
- SQLSetStmtAttr function [ODBC]
ms.assetid: 7abc5260-733a-48d4-9974-2d1a6a9ea5f6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 583639a5cd4680bf6cfcf03bbaf6ee9eb63adba8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039654"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**設定相關的陳述式的屬性。  
  
> [!NOTE]
>  如需有關什麼驅動程式管理員會對應到此函式時 ODBC *3.x*應用程式使用 ODBC *2.x*驅動程式，請參閱[對應為向後取代函式應用程式的相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 [輸入]選項可用來設定，列在 [註解。]  
  
 *ValuePtr*  
 [輸入]相關聯的值*屬性*。 值而定*屬性*， *ValuePtr*將會是下列其中一項：  
  
-   ODBC 的描述項控制代碼。  
  
-   SQLUINTEGER 值。  
  
-   SQLULEN 值。  
  
-   下列其中一種指標：  
  
    -   以 null 終止的字元字串。  
  
    -   二進位的緩衝區。  
  
    -   值或陣列類型是 SQLLEN、 SQLULEN 或 SQLUSMALLINT。  
  
    -   驅動程式定義的值。  
  
 如果*屬性*引數是驅動程式專屬值*ValuePtr*可能帶正負號的整數。  
  
 *StringLength*  
 [輸入]如果*屬性*ODBC 定義的屬性和*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *ValuePtr*. 如果*屬性*ODBC 定義的屬性和*ValuePtr*是一個整數， *StringLength*會被忽略。  
  
 如果*屬性*是驅動程式定義的屬性，應用程式設定指出屬性給驅動程式管理員性質*StringLength*引數。 *StringLength*可以有下列值：  
  
-   如果*ValuePtr*是字元字串的指標，則*StringLength*是 sql_nts; 之字串的長度。  
  
-   如果*ValuePtr*為二進位的緩衝區的指標，則應用程式會放 SQL_LEN_BINARY_ATTR 的結果 (*長度*) 中的巨集*StringLength*。 這會放在負值*StringLength*。  
  
-   如果*ValuePtr*是字元字串或二進位字串以外的值的指標，則*StringLength*應有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定長度的值，則*StringLength*是 SQL_IS_INTEGER 或 SQL_IS_UINTEGER，視需要。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetStmtAttr**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetStmtAttr** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援指定的值*ValuePtr*，或指定值*ValuePtr*無效，因為實作運作的情況，因此驅動程式取代成類似的值。 (**SQLGetStmtAttr**可以呼叫以判斷暫時替代的值。)取代值是適用於*StatementHandle*直到資料指標已關閉，此時陳述式屬性會還原為先前的值。 您可以變更的陳述式屬性是：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|*屬性*SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR，或 SQL_ATTR_USE_BOOKMARKS，和資料指標為開啟。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY009|使用無效的 null 指標|*屬性*引數識別必要字串屬性，陳述式屬性和*ValuePtr*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLSetStmtAttr**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY011|現在無法設定屬性|*屬性*SQL_ATTR_CONCURRENCY、 SQL_ ATTR_CURSOR_TYPE、 SQL_ ATTR_SIMULATE_CURSOR 或 SQL_ ATTR_USE_BOOKMARKS 和已備妥的陳述式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY017|使用自動配置描述項控制代碼無效|(DM)*屬性*引數為 SQL_ATTR_IMP_ROW_DESC 或 SQL_ATTR_IMP_PARAM_DESC。<br /><br /> (DM)*屬性*引數為 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，並在值*ValuePtr*原本是控制代碼以外的隱含配置描述項控制代碼配置 ARD 或 APD。|  
|HY024|屬性值無效|提供給指定的*屬性*值，指定了無效的值中*ValuePtr*。 （驅動程式管理員會傳回這個僅適用於連接和陳述式屬性接受一組特定的值，例如 SQL_ATTR_ACCESS_MODE 或 SQL_ ATTR_ASYNC_ENABLE 的 SQLSTATE。 對於所有其他連接和陳述式屬性，驅動程式必須確認在指定的值*ValuePtr*。)<br /><br /> *屬性*引數為 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，及*ValuePtr*已不在相同的連線，做為明確配置描述項控制代碼*StatementHandle*引數。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*ValuePtr*是字元字串，而*StringLength*引數為小於 0，但不是 sql_nts;。|  
|HY092|屬性/選項識別碼無效|(DM) 引數指定的值*屬性*ODBC 驅動程式支援的版本無效。<br /><br /> (DM) 引數指定的值*屬性*是唯讀的屬性。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的引數的值*屬性*的驅動程式支援的 ODBC 版本，但不是支援此驅動程式是有效的 ODBC 陳述式屬性。<br /><br /> *屬性*引數為 sql_attr_async_enable 設定，以及呼叫**SQLGetInfo**具有*資訊類型*SQL_ASYNC_MODE 傳回 SQL_AM_CONNECTION。<br /><br /> *屬性*引數為 SQL_ATTR_ENABLE_AUTO_IPD，而 SQL_ATTR_AUTO_IPD 連接屬性的值為 SQL_FALSE。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|S1118|驅動程式不支援非同步通知|如果呼叫**SQLSetStmtAttr**設 SQL_ATTR_ASYNC_STMT_EVENT; 驅動程式不支援非同步通知。|  
  
## <a name="comments"></a>註解  
 陳述式的陳述式屬性都有效，除非有另一個呼叫來變更**SQLSetStmtAttr** ，或者藉由呼叫的陳述式會卸除為止**SQLFreeHandle**。 呼叫**SQLFreeStmt** SQL_CLOSE、 SQL_UNBIND，或 SQL_RESET_PARAMS 選項不會重設的陳述式屬性。  
  
 如果資料來源不支援指定的值，某些陳述式屬性支援類似的值替換*ValuePtr*。 在此情況下，驅動程式會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。 例如，如果*屬性*是 SQL_ATTR_CONCURRENCY 並*ValuePtr* SQL_CONCUR_ROWVER，且資料來源不支援這，如果驅動程式取代 SQL_CONCUR_VALUES，並傳回 SQL_SUCCESS_WITH_INFO。 若要判斷已取代的值，應用程式會呼叫**SQLGetStmtAttr**。  
  
 使用設定資訊的格式*ValuePtr*取決於指定*屬性*。 **SQLSetStmtAttr**接受兩個不同的格式之一的屬性資訊： 字元字串或整數值。 屬性的描述中註明的每個格式。 此格式適用於每個屬性中傳回的資訊**SQLGetStmtAttr**。 字元字串所指向*ValuePtr*引數**SQLSetStmtAttr**具有長度*StringLength*。  
  
> [!NOTE]
>  能夠在連接層級設定陳述式屬性，藉由呼叫**SQLSetConnectAttr** ODBC 中的過時*3.x*。 ODBC *3.x*應用程式應該永遠不會設定在連接層級的陳述式屬性。 ODBC *3.x*陳述式屬性無法設定在連接層級，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性，這是連接屬性和陳述式屬性，而且可以是在連接層級或陳述式層級設定。  
> 
> [!NOTE]
>  ODBC *3.x*驅動程式只需要支援這項功能，如果應該使用 ODBC *2.x*應用程式，設定 ODBC *2.x*連接層級的陳述式選項。 如需詳細資訊，請參閱 「 設定陳述式選項在連接層級 」 底下[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>設定描述項欄位的陳述式屬性  
 許多陳述式屬性對應到描述項標頭欄位。 描述項欄位的設定中設定這些屬性實際結果。 藉由呼叫設定欄位**SQLSetStmtAttr**而**SQLSetDescField**描述項控制代碼不需要取得函式呼叫的優點。  
  
> [!CAUTION]  
>  呼叫**SQLSetStmtAttr**的一個陳述式可能會影響其他陳述式。 會發生這種情況是當 APD 或陳述式相關聯的 ARD 明確配置，而且也與其他陳述式相關聯。 因為**SQLSetStmtAttr**修改 APD 或 ARD，所做的修改套用至與這個描述元相關聯的所有陳述式。 如果這不是所需的行為，應用程式應該中斷關聯的其他陳述式的這個描述元 (藉由呼叫**SQLSetStmtAttr**設為不同的 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 欄位描述項控制代碼） 然後再呼叫**SQLSetStmtAttr**一次。  
  
 當描述項欄位設定所設定的對應陳述式屬性的結果時，只會針對適用的描述項所識別的陳述式使用目前相關聯的設定欄位*StatementHandle*引數和屬性設定不會影響任何可能在未來在該陳述式相關聯的描述元。 當呼叫設定也是陳述式屬性描述項欄位**SQLSetDescField**，相對應的陳述式屬性設定。 如果明確配置描述項會中斷與的關聯從陳述式，會對應到標頭欄位的陳述式屬性將會還原為隱含配置描述項欄位的值。  
  
 當配置陳述式 (請參閱[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md))，四個描述項控制代碼會自動配置和陳述式相關聯。 明確配置描述項控制代碼可以藉由呼叫陳述式相關聯**SQLAllocHandle**具有*fHandleType*的配置描述項控制代碼，然後呼叫SQL_HANDLE_DESC**SQLSetStmtAttr**陳述式相關聯的描述項控制代碼。  
  
 下表中的陳述式屬性對應到描述項標頭欄位。  
  
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
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IRD|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IRD|  
  
## <a name="statement-attributes"></a>陳述式屬性  
 下列表格中，顯示目前定義的屬性，並在其中引進的 ODBC 版本我們預期更多的屬性將會定義驅動程式，以善用不同的資料來源。 ODBC; 保留範圍的屬性驅動程式開發人員必須保留供自己從 Open Group 的驅動程式專屬使用的值。 如需詳細資訊，請參閱 <<c0> [ 驅動程式專屬資料型別、 描述項類型、 資訊類型、 診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|屬性|*ValuePtr*內容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|APD 中的後續呼叫的控制代碼**SQLExecute**並**SQLExecDirect**陳述式控制代碼。 這個屬性的初始值是一開始配置陳述式時，隱含配置描述項。 如果此屬性的值設定為 SQL_NULL_DESC 或原先配置描述項控制代碼，先前的陳述式控制代碼關聯的明確配置的 APD 控制代碼從它中斷與的關聯，且陳述式控制代碼會還原為隱含配置 APD 控制代碼。<br /><br /> 無法將設定這個屬性，另一個陳述式已隱含配置描述項控制代碼或隱含地設定相同的陳述式; 的另一個描述項控制代碼隱含配置描述項控制代碼不能與多個陳述式或描述項控制代碼相關聯。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|針對後續陳述式控制代碼上的提取 ARD 控制代碼。 這個屬性的初始值是一開始配置陳述式時，隱含配置描述項。 如果此屬性的值設定為 SQL_NULL_DESC 或原先配置描述項控制代碼，先前的陳述式控制代碼關聯的明確配置的 ARD 控制代碼從它中斷與的關聯，且陳述式控制代碼會還原為隱含配置 ARD 控制代碼。<br /><br /> 無法將設定這個屬性，另一個陳述式已隱含配置描述項控制代碼或隱含地設定相同的陳述式; 的另一個描述項控制代碼隱含配置描述項控制代碼不能與多個陳述式或描述項控制代碼相關聯。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|SQLULEN 值，這個值指定是否要以非同步方式執行指定的陳述式呼叫的函式：<br /><br /> SQL_ASYNC_ENABLE_OFF = 停用陳述式的支援層級的非同步執行 （預設值）。<br /><br /> Sql_async_enable_on，然後 = 啟用陳述式層級的非同步執行的支援。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 非同步執行 （輪詢的方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> 陳述式層級的非同步執行支援的驅動程式，陳述式屬性 sql_attr_async_enable 設定為唯讀。 其值會位於具有相同名稱的連接層級屬性的值相同的陳述式控制代碼已配置的時間。<br /><br /> 呼叫**SQLSetStmtAttr** ，將 sql_attr_async_enable 設定時 SQL_ASYNC_MODE*資訊類型*傳回 SQL_AM_CONNECTION 傳回 SQLSTATE HYC00 （未實作選擇性功能）。 如需詳細資訊，請參閱 < [SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)如需詳細資訊。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|為事件處理常式的 SQLPOINTER 值。<br /><br /> 藉由呼叫已完成的非同步函式的通知**SQLSetStmtAttr**來設定**SQL_ATTR_ASYNC_STMT_EVENT**屬性，指定事件處理常式。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|SQLPOINTER 非同步的回呼函式。<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**具有此屬性的函式。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|Context 結構的 SQLPOINTER<br /><br /> 驅動程式管理員可以呼叫的驅動程式僅**SQLSetStmtAttr**具有此屬性的函式。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|指定資料指標並行 SQLULEN 值：<br /><br /> SQL_CONCUR_READ_ONLY = 資料指標是唯讀的。 不允許任何更新。<br /><br /> SQL_CONCUR_LOCK = 資料指標會使用鎖定不足以確保可以更新資料列的最低層級。<br /><br /> SQL_CONCUR_ROWVER = 資料指標使用開放式並行存取控制，比較資料列版本，例如 SQLBase ROWID 或 Sybase 時間戳記。<br /><br /> SQL_CONCUR_VALUES = 資料指標使用開放式並行存取控制，比較值。<br /><br /> 預設值為 sql_attr_concurrency 設定為 SQL_CONCUR_READ_ONLY。<br /><br /> 開啟的資料指標時，不指定這個屬性。 如需詳細資訊，請參閱 <<c0> [ 並行類型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果 SQL_ATTR_CURSOR_TYPE*屬性*變更為不支援目前的 SQL_ATTR_CONCURRENCY 值型別，sql_attr_concurrency 設定的值將會變更在執行時間以及時發出警告**SQLExecDirect**或是**SQLPrepare**呼叫。<br /><br /> 如果此驅動程式支援**SELECT FOR UPDATE**陳述式，這類陳述式執行時，值的 SQL_ATTR_CONCURRENCY 設定為 SQL_CONCUR_READ_ONLY，將會傳回錯誤。 如果 sql_attr_concurrency 設定的值變更為值，此驅動程式支援的 SQL_ATTR_CURSOR_TYPE 中某些值，但不適用於 SQL_ATTR_CURSOR_TYPE 的目前值，將變更的 SQL_ATTR_CURSOR_TYPE 值在執行階段和 SQLSTATE 01s02 的警告（選項值已變更） 時發出**SQLExecDirect**或是**SQLPrepare**呼叫。<br /><br /> 如果資料來源不支援指定的並行，驅動程式替代不同的並行處理，並傳回 SQLSTATE 01S02 （選項值已變更）。 對於 SQL_CONCUR_VALUES，驅動程式會取代 SQL_CONCUR_ROWVER，反之亦然。 對於 SQL_CONCUR_LOCK，驅動程式取代，在 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES 的順序。 替代值之有效性不會等到執行階段檢查。<br /><br /> 如需有關 SQL_ATTR_CONCURRENCY 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|指定的應用程式所需的支援層級的 SQLULEN 值。 設定這個屬性會影響後續呼叫**SQLExecDirect**並**SQLExecute**。<br /><br /> SQL_NONSCROLLABLE = 可捲動資料指標不需要的陳述式控制代碼。 如果應用程式會呼叫**SQLFetchScroll**此控制代碼的唯一有效的值上*Sqlfetchscroll*是 SQL_FETCH_NEXT。 這是預設值。<br /><br /> SQL_SCROLLABLE = 可捲動資料指標為所需的陳述式控制代碼。 呼叫時**SQLFetchScroll**，應用程式可以指定任何有效值*Sqlfetchscroll*，達到資料指標定位在循序模式以外的模式。<br /><br /> 如需有關可捲動資料指標的詳細資訊，請參閱[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需有關 SQL_ATTR_CURSOR_SCROLLABLE 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|SQLULEN 值，指定是否在陳述式控制代碼上的資料指標顯示另一個資料指標設定至結果所做的變更。 設定這個屬性會影響後續呼叫**SQLExecDirect**並**SQLExecute**。 應用程式可以讀回應用程式設定這個屬性，以取得其初始狀態或其狀態為最近期的值。<br /><br /> SQL_UNSPECIFIED = 並未指定資料指標類型的功能和是否資料指標陳述式控制代碼上的顯示結果集，另一個資料指標所做的變更。 資料指標陳述式控制代碼上的可能會顯示無、 部分或全部這類變更。 這是預設值。<br /><br /> SQL_INSENSITIVE = 所有的資料指標的結果集而不會反映任何變更陳述式控制代碼顯示的任何其他資料指標。 非感應式資料指標是唯讀的。 這會對應至靜態資料指標，其為唯讀並行存取。<br /><br /> SQL_SENSITIVE = 陳述式控制代碼進行顯示由另一個資料指標的結果所做的變更設定的所有資料指標。<br /><br /> 如需有關 SQL_ATTR_CURSOR_SENSITIVITY 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|指定資料指標類型的 SQLULEN 值：<br /><br /> SQL_CURSOR_FORWARD_ONLY = 資料指標唯一捲動轉寄。<br /><br /> SQL_CURSOR_STATIC = 資料在結果集是靜態的。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 驅動程式儲存和使用該索引鍵之 SQL_ATTR_KEYSET_SIZE 陳述式屬性中指定的資料列數目。<br /><br /> SQL_CURSOR_DYNAMIC = 驅動程式儲存和使用資料列集中的資料列的索引鍵。<br /><br /> 預設值是 SQL_CURSOR_FORWARD_ONLY。 已備妥的 SQL 陳述式之後，就無法指定這個屬性。<br /><br /> 如果資料來源不支援指定的資料指標類型，驅動程式取代的不同資料指標類型，並傳回 SQLSTATE 01S02 （選項值已變更）。 對於混合式或動態資料指標，驅動程式替代，依序索引鍵集驅動或靜態資料指標。 對於索引鍵集驅動資料指標時，驅動程式會取代靜態資料指標。<br /><br /> 如需可捲動資料指標類型的詳細資訊，請參閱[可捲動資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 如需有關 SQL_ATTR_CURSOR_TYPE 和其他資料指標屬性之間的關聯性的詳細資訊，請參閱[資料指標的特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|指定是否要執行自動填入 IPD SQLULEN 值：<br /><br /> SQL_TRUE = 開啟呼叫之後，自動填入 IPD **SQLPrepare**。 SQL_FALSE = 關閉呼叫之後，自動填入 IPD **SQLPrepare**。 (應用程式仍然可以藉由呼叫取得 IPD 欄位資訊**SQLDescribeParam**，如果支援。)預設值的陳述式屬性 SQL_ATTR_ENABLE_AUTO_IPD 為 SQL_FALSE。 如需詳細資訊，請參閱 <<c0> [ 自動填入 IPD](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|SQLLEN \* ，它會指向二進位的書籤值。 當**SQLFetchScroll**呼叫*fFetchOrientation*等於 SQL_FETCH_BOOKMARK，驅動程式會挑選此欄位中的書籤值。 此欄位預設為 null 指標。 如需詳細資訊，請參閱 <<c0> [ 依書籤捲動](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 此欄位所指向的值不是 delete 依書籤、 書籤，來更新或擷取中的書籤作業所**SQLBulkOperations**，這會使用快取資料列集的緩衝區中的書籤。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD 控制代碼。 此屬性的值是一開始配置陳述式時配置描述項。 應用程式無法設定這個屬性。<br /><br /> 這個屬性可以擷取由呼叫**SQLGetStmtAttr**但未設定的呼叫所**SQLSetStmtAttr**。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD 控制代碼。 此屬性的值是一開始配置陳述式時配置描述項。 應用程式無法設定這個屬性。<br /><br /> 這個屬性可以擷取由呼叫**SQLGetStmtAttr**但未設定的呼叫所**SQLSetStmtAttr**。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|指定在索引鍵集驅動資料指標的索引鍵集中的資料列數目 SQLULEN。 如果索引鍵集大小為 0 （預設值），資料指標會是完整的索引鍵集驅動。 如果索引鍵集大小大於 0，資料指標被混合 （索引鍵集內索引鍵集驅動和動態外部索引鍵集）。 預設索引鍵集大小為 0。 如需有關索引鍵集驅動資料指標的詳細資訊，請參閱 <<c0> [ 索引鍵集衍生資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定的大小超過最大索引鍵集大小，此驅動程式取代該大小，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> **SQLFetch**或是**SQLFetchScroll**會傳回錯誤，如果索引鍵集大小大於 0 且小於資料列集大小。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|指定驅動程式會傳回從字元或二進位資料行的資料的最大數量的 SQLULEN 值。 如果*ValuePtr*可用的資料，長度少於**SQLFetch**或是**SQLGetData**截斷的資料，並傳回 SQL_SUCCESS。 如果*ValuePtr*是 0 （預設值），則驅動程式會嘗試傳回所有可用的資料。<br /><br /> 如果指定的長度，則可以傳回的資料來源的資料的最小數量小於或大於最大的資料量，可以傳回的資料來源，驅動程式替代作業的值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 此屬性的值可以設定上開啟的資料指標;不過，此設定可能不會立即生效，在這種情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更） 和重設為其原始值的屬性。<br /><br /> 這個屬性要減少網路流量，而且應該在資料來源 （而不是驅動程式） 中的多層式驅動程式可以實作它時，才支援。 這項機制不應由應用程式来截斷的資料;若要截斷收到的資料，應用程式應該指定最大的緩衝區長度，以*Columnsize*中的引數**SQLBindCol**或**SQLGetData**。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|對應至應用程式所傳回的資料列數目上限 SQLULEN 值**選取**陳述式。 如果\* *ValuePtr*等於 0 （預設值），驅動程式會傳回所有資料列。<br /><br /> 此屬性被用來減少網路流量。 就概念而言，它會在其中套用時的結果集建立，並限制結果集的第一個*ValuePtr*資料列。 如果結果集中的資料列數目大於*ValuePtr*，會截斷結果集。<br /><br /> SQL_ATTR_MAX_ROWS 適用於所有結果集上*陳述式*，包括所傳回的目錄函數。 SQL_ATTR_MAX_ROWS 會建立資料指標資料列計數值最大值。<br /><br /> 驅動程式應該不會模擬 SQL_ATTR_MAX_ROWS 行為**SQLFetch**或是**SQLFetchScroll** （如果結果集大小限制不能實作在資料來源） 如果它無法保證該 SQL_ATTR_MAX_ROWS 會正確地實作。<br /><br /> 它是驅動程式定義是否 SQL_ATTR_MAX_ROWS 套用至陳述式 （例如目錄函式） 的 SELECT 陳述式以外。<br /><br /> 此屬性的值可以設定上開啟的資料指標;不過，此設定可能不會立即生效，在這種情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更） 和重設為其原始值的屬性。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|決定如何處理目錄函數的字串引數的 SQLULEN 值。<br /><br /> 如果 SQL_TRUE，目錄函數的字串引數會被視為識別碼。 如此並不重要。 針對了非分隔的字串，驅動程式會移除任何尾端的空格，並為大寫的字串摺疊。 針對分隔的字串，驅動程式會移除任何開頭或尾端空格，並採用任何實際上是分隔符號之間。 如果這些引數的其中一個設定為 null 指標，函式會傳回 SQL_ERROR 並 SQLSTATE HY009 （使用無效的 null 指標）。<br /><br /> 如果 SQL_FALSE，目錄函數的字串引數不會被視為識別碼。 案例很重要。 它們可以包含字串的搜尋模式，根據引數。<br /><br /> 預設值為 SQL_FALSE。<br /><br /> *TableType*引數**SQLTables**，後者會採用值的清單，不會影響這個屬性。<br /><br /> SQL_ATTR_METADATA_ID 也可以設定在連接層級上。 （它和 sql_attr_async_enable 設定是唯一的陳述式屬性，還有連接屬性）。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|SQLULEN 值，指出此驅動程式是否應該掃描逸出序列 (sequence) 的 SQL 字串：<br /><br /> SQL_NOSCAN_OFF = 驅動程式掃描 SQL 字串的逸出序列 （預設值）。<br /><br /> SQL_NOSCAN_ON = 驅動程式不會掃描 SQL 字串的逸出序列 (sequence)。 相反地，驅動程式陳述式將直接傳送至資料來源。<br /><br /> 如需詳細資訊，請參閱 < [ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 位移新增至變更繫結的動態參數的指標所指向的值。 如果此欄位為非 null，驅動程式會取值指標加入至每個延遲欄位 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR），描述項記錄中，會使用新的指標值繫結時。 它會設定預設為 null。<br /><br /> 繫結位移是一律直接新增至 [SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR] 欄位。 如果位移變更為不同的值，新的值是仍然直接新增至描述項欄位中的值。 新的位移不會加入至欄位值，加上任何先前的位移。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 參數繫結位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 將此陳述式屬性設定 SQL_DESC_BIND_OFFSET_PTR 欄位 APD 標頭中設定。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|SQLULEN 值，指出要用於動態參數的繫結方向。<br /><br /> 此欄位設 SQL_PARAM_BIND_BY_COLUMN （預設值） 中，選取資料行取向的繫結。<br /><br /> 若要選取資料列取向的繫結，此欄位設為結構或緩衝區一組動態參數繫結的執行個體的長度。 這個長度會包含所有繫結的參數以及結構或緩衝區，確保，當繫結參數的位址會隨著指定的長度，結果會指向相同的參數，在下一個開頭的任何填補的空間參數集。 使用時*sizeof* ANSI C 中的運算子，保證此行為。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 繫結參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 將此陳述式屬性設定 SQL_DESC_ BIND_TYPE 欄位 APD 標頭中設定。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*值指向 SQLUSMALLINT 值的陣列，用來在執行 SQL 陳述式的期間略過參數。 每個值設為 SQL_PARAM_PROCEED （適用於執行參數） 或 SQL_PARAM_IGNORE （適用於要忽略參數）。<br /><br /> 一組參數可以在處理期間忽略 SQL_DESC_ARRAY_STATUS_PTR 至 SQL_PARAM_IGNORE APD 中所指陣列中設定的值。 如果其狀態的值設定為 SQL_PARAM_PROCEED，或設定陣列中的任何項目，則會處理一組參數。<br /><br /> 此陳述式屬性可以設定為 null 指標，在其中案例驅動程式不會傳回參數的狀態值。 可以隨時設定這個屬性，但新的值不是等到下次**SQLExecDirect**或是**SQLExecute**呼叫。<br /><br /> 沒有任何繫結的參數時，會忽略此屬性。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 將此陳述式屬性設定 SQL_DESC_ARRAY_STATUS_PTR 欄位 APD 標頭中設定。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*值指向 SQLUSMALLINT 陣列值的參數值的每個資料列包含的狀態資訊，在呼叫之後**SQLExecute**或是**SQLExecDirect**。 只有當 PARAMSET_SIZE 大於 1 時，才需要此欄位。<br /><br /> [狀態] 值可以包含下列值：<br /><br /> SQL_PARAM_SUCCESS:SQL 陳述式成功執行這一集的參數。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO:這一集的參數，成功執行的 SQL 陳述式不過，警告資訊可在診斷資料結構。<br /><br /> SQL_PARAM_ERROR:處理這組參數時發生錯誤。 使用診斷資料結構中的其他錯誤資訊。<br /><br /> SQL_PARAM_UNUSED:此參數集為未使用，可能是因為，一些先前的參數集而造成錯誤中止進一步處理，或因為 SQL_PARAM_IGNORE 設定該 SQL_ATTR_PARAM_OPERATION_PTR 所指定之陣列中的參數集。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE:驅動程式的參數陣列視為單一單位，因此不會產生此層級的資訊時發生錯誤。<br /><br /> 此陳述式屬性可以設定為 null 指標，在其中案例驅動程式不會傳回參數的狀態值。 可以隨時設定這個屬性，但新的值不是等到下次**SQLExecute**或是**SQLExecDirect**呼叫。 請注意，將此屬性設定可能會影響的驅動程式實作 output 參數行為。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定此陳述式屬性在 IPD 標頭中設定 SQL_DESC_ARRAY_STATUS_PTR 欄位。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|SQLULEN\*資料錄的欄位所指向的緩衝區中要傳回的已處理，包括錯誤集的參數集的數目。 如果這是 null 指標，則會不傳回任何數字。<br /><br /> 設定此陳述式屬性在 IPD 標頭中設定 SQL_DESC_ROWS_PROCESSED_PTR 欄位。<br /><br /> 如果在呼叫**SQLExecDirect**或是**SQLExecute** ，填入這個屬性所指向的緩衝區不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容為未定義。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|指定的每個參數的值數目的 SQLULEN 值。 如果則 sql_attr_paramset_size 會大於 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 的 APD 指向陣列。 每個陣列的基數等於這個欄位的值。<br /><br /> 沒有任何繫結的參數時，會忽略此屬性。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定此陳述式屬性設定 APD 標頭中的 SQL_DESC_ARRAY_SIZE 欄位。|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|SQLULEN 值，對應至 SQL 陳述式執行傳回給應用程式之前所等待的秒數。 如果*ValuePtr*會等於 0 （預設值），沒有任何逾時。<br /><br /> 如果指定的逾時超過資料來源中的最大逾時或小於最小的逾時， **SQLSetStmtAttr**取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 請注意，應用程式不需要呼叫**SQLCloseCursor**重複使用陳述式，如果**選取**陳述式已逾時。<br /><br /> 設定在這個陳述式屬性中的查詢逾時是在同步與非同步模式中無效。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 值：<br /><br /> SQL_RD_ON = **SQLFetchScroll** ，然後在 ODBC *3.x*， **SQLFetch**擷取資料之後將游標置於指定的位置。 這是預設值。<br /><br /> SQL_RD_OFF = **SQLFetchScroll** ，然後在 ODBC *3.x*， **SQLFetch**之後將游標置於不擷取資料。<br /><br /> SQL_RETRIEVE_DATA 設 SQL_RD_OFF，一個資料列存在，或擷取的資料列的書籤，而不會造成擷取資料列的負擔，可以確認應用程式。 如需詳細資訊，請參閱 <<c0> [ 捲動和提取的資料列](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 此屬性的值可以設定上開啟的資料指標;不過，此設定可能不會立即生效，在這種情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更） 和重設為其原始值的屬性。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|SQLULEN 值，指定每個呼叫所傳回的資料列數目**SQLFetch**或是**SQLFetchScroll**。 它也是陣列中的書籤中有大量的書籤作業中使用的資料列數**SQLBulkOperations**。 預設值為 1。<br /><br /> 如果指定的資料列集大小超過資料來源所支援的最大資料列集大小，此驅動程式取代該值，並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 設定此陳述式屬性設定 ARD 標頭中的 SQL_DESC_ARRAY_SIZE 欄位。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN * 位移新增至變更繫結的資料行的資料指標所指向的值。 如果此欄位為非 null，驅動程式會取值指標加入至每個延遲欄位 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR），描述項記錄中，會使用新的指標值繫結時。 它會設定預設為 null。<br /><br /> 將此陳述式屬性設定 SQL_DESC_BIND_OFFSET_PTR 欄位 ARD 標頭中設定。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|SQLULEN 值，這個設定的繫結方向的值時使用**SQLFetch**或是**SQLFetchScroll**相關的陳述式上呼叫。 資料行取向繫結會選取將值設為 SQL_BIND_BY_COLUMN。 選取資料列取向繫結的值結構或緩衝區，其中將會繫結結果資料行的執行個體的長度。<br /><br /> 如果指定的長度，則它必須包含所有繫結的資料行以及結構或緩衝區，確保，當繫結的資料行的位址會隨著指定的長度，結果會指向相同的資料行中開頭的任何填補的空間e 的下一個資料列。 使用時**sizeof**結構或等位在 ANSI C 中使用的運算子，保證此行為。<br /><br /> 資料行取向繫結則是預設繫結方向**SQLFetch**並**SQLFetchScroll**。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 繫結區塊資料指標搭配使用的資料行](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 將此陳述式屬性設定 SQL_DESC_BIND_TYPE 欄位 ARD 標頭中設定。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|是整個結果中目前資料列數目 SQLULEN 值設定。 如果無法判斷目前的資料列數目，或者沒有目前的資料列，則驅動程式會傳回 0。<br /><br /> 這個屬性可以擷取由呼叫**SQLGetStmtAttr**但未設定的呼叫所**SQLSetStmtAttr**。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|SQLUSMALLINT\*值指向 SQLUSMALLINT 值的陣列，用來在大量作業，使用忽略的資料列**SQLSetPos**。 每個值設為 SQL_ROW_PROCEED （適用於大量作業中要包含的資料列） 或 SQL_ROW_IGNORE （適用於大量作業要排除的資料列）。 (不能忽略資料列，在呼叫期間使用這個陣列**SQLBulkOperations**。)<br /><br /> 此陳述式屬性可以設定為 null 指標，案例驅動程式不會傳回資料列狀態值。 可以隨時設定這個屬性，但新的值不是等到下次**SQLSetPos**呼叫。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 的資料列集使用 SQLSetPos 更新資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)並[刪除的資料列中的資料列集使用 SQLSetPos](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 設定此陳述式屬性集中 ARD SQL_DESC_ARRAY_STATUS_PTR 欄位。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT \* SQLUSMALLINT 陣列所指向的值之後呼叫值包含資料列狀態值**SQLFetch**或是**SQLFetchScroll**。 陣列的資料列集內有資料列的項目數。<br /><br /> 此陳述式屬性可以設定為 null 指標，案例驅動程式不會傳回資料列狀態值。 可以隨時設定這個屬性，但新的值不是等到下次**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**呼叫。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 編號的擷取資料列和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 將此陳述式屬性設定 SQL_DESC_ARRAY_STATUS_PTR 欄位 IRD 標頭中設定。<br /><br /> 這個屬性會對應由 ODBC *2.x*驅動程式新增至*rgbRowStatus*的呼叫中的陣列**SQLExtendedFetch**。|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|SQLULEN\*指向的緩衝區中要傳回的呼叫之後擷取的資料列數目的值**SQLFetch**或是**SQLFetchScroll**; 執行大量作業所影響的資料列數目藉由呼叫**SQLSetPos**具有*作業*SQL_REFRESH; 或藉由執行大量作業所影響的資料列數目的引數**SQLBulkOperations**. 此數目包含錯誤資料列。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 編號的擷取資料列和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 將此陳述式屬性設定 SQL_DESC_ROWS_PROCESSED_PTR 欄位 IRD 標頭中設定。<br /><br /> 如果在呼叫**SQLFetch**或是**SQLFetchScroll** ，填入這個屬性所指向的緩衝區不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容為未定義。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|指定驅動程式，模擬定位的 update 和 delete 陳述式是否保證，這類陳述式會影響只有一個單一資料列的 SQLULEN 值。<br /><br /> 若要模擬定位的 update 及 delete 陳述式，大部分的驅動程式建構搜尋**更新**或**刪除**包含陳述式**其中**指定子句目前的資料列中的每個資料行的值。 這些資料行是由唯一的索引鍵所組成，除非這類陳述式可能會影響多個資料列。<br /><br /> 若要保證，這類陳述式會影響只有一個資料列，驅動程式會判斷唯一索引鍵中的資料行，並將這些資料行加入至結果集。 如果應用程式保證結果集中的資料行構成的唯一索引鍵，驅動程式不會需要進行此作業。 這可能會減少執行時間。<br /><br /> SQL_SC_NON_UNIQUE = 驅動程式不保證模擬是否位於 update 或 delete 陳述式會影響只有一個資料列;是應用程式的責任，若要這樣做。 如果陳述式會影響多個資料列**SQLExecute**， **SQLExecDirect**，或**SQLSetPos**傳回 SQLSTATE 01001 （資料指標作業衝突）。<br /><br /> SQL_SC_TRY_UNIQUE = 驅動程式嘗試以保證的模擬定位更新或刪除陳述式影響的只有一個資料列。 驅動程式一律會執行這類陳述式，即使它們可能會影響多個資料列，例如當沒有唯一的索引鍵。 如果陳述式會影響多個資料列**SQLExecute**， **SQLExecDirect**，或**SQLSetPos**傳回 SQLSTATE 01001 （資料指標作業衝突）。<br /><br /> SQL_SC_UNIQUE = 驅動程式可確保模擬定位的 update 或 delete 陳述式影響的只有一個資料列。 如果驅動程式指定的陳述式中，無法保證這**SQLExecDirect**或是**SQLPrepare**會傳回錯誤。<br /><br /> 如果資料來源會提供原生 SQL 支援定位的 update 和 delete 陳述式和驅動程式不會模擬資料指標，SQL_SC_UNIQUE SQL_SIMULATE_CURSOR 的要求時，會傳回 SQL_SUCCESS。 如果要求 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE，則會傳回 SQL_SUCCESS_WITH_INFO。 如果資料來源提供 SQL_SC_TRY_UNIQUE 層級的支援，而且驅動程式不會 SQL_SC_TRY_UNIQUE 和 SQL_SUCCESS_WITH_INFO 會傳回如 SQL_SC_NON_UNIQUE 時，會傳回 SQL_SUCCESS。<br /><br /> 如果資料來源不支援指定的資料指標模擬類型，驅動程式取代為不同的模擬類型，並傳回 SQLSTATE 01S02 （選項值已變更）。 對於 SQL_SC_UNIQUE，驅動程式取代，在 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE 的順序。 對於 SQL_SC_TRY_UNIQUE，驅動程式會取代 SQL_SC_NON_UNIQUE。<br /><br /> 預設為 SQL_SC_UNIQUE。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 模擬定位的 Update 和刪除陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|指定應用程式與資料指標是否使用書籤 SQLULEN 值：<br /><br /> SQL_UB_OFF = Off （預設值）<br /><br /> SQL_UB_VARIABLE = 應用程式會使用資料指標的書籤和驅動程式會提供可變長度的書籤，並支援。 ODBC 中已被取代 SQL_UB_FIXED *3.x*。 ODBC *3.x*應用程式應該一律使用可變長度的書籤，甚至是在使用 ODBC 時，才*2.x* （其支援只有 4 個位元組，固定長度書籤） 的驅動程式。 這是因為固定長度書籤只是特殊案例的可變長度書籤。 使用 ODBC 時*2.x*驅動程式，則驅動程式管理員就會將 SQL_UB_VARIABLE 對應至 SQL_UB_FIXED。<br /><br /> 若要使用資料指標中的書籤，應用程式必須指定此屬性 SQL_UB_VARIABLE 值才能開啟資料指標。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 擷取書籤](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [1] 這些函式可以非同步呼叫，只有當描述項是實作描述項，不應用程式描述項。  
  
 請參閱[資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)並[資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函式](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回陳述式屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函式](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定的單一欄位的描述元|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
