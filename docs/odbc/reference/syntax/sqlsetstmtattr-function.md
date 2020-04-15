---
title: SQLSetStmtAttr 函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfbd2144e677d053f6154dfb3a1df1f6c25d9da5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287259"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**設置與語句相關的屬性。  
  
> [!NOTE]
>  有關驅動程式管理員將此功能映射到 ODBC *3.x*應用程式使用 ODBC *2.x*驅動程式時的詳細資訊,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetStmtAttr(  
     SQLHSTMT      StatementHandle,  
     SQLINTEGER    Attribute,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    StringLength);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *屬性*  
 [輸入]選項設置,列在「註釋」 中。  
  
 *ValuePtr*  
 [輸入]要與*屬性*關聯的值。 根據*屬性*的值 *,ValuePtr*將是以下之一:  
  
-   ODBC 描述符句柄。  
  
-   SQLUINTEGER 值。  
  
-   SQLULEN 值。  
  
-   指向下列之一的指標:  
  
    -   null 終止字串。  
  
    -   二進位緩衝區。  
  
    -   SQLLEN、SQLULEN 或 SQLUSMALLINT 類型的值或陣列。  
  
    -   驅動程式定義的值。  
  
 如果*屬性*參數是特定於驅動程式的值 *,ValuePtr*可能是一個簽名整數。  
  
 *字串長度*  
 [輸入]如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*指向字串或二進位緩衝區,\*則此參數應為*ValuePtr*的長度。 如果*屬性*是 ODBC 定義的屬性 *,ValuePtr*是整數,則忽略*字串長度*。  
  
 如果*屬性*是驅動程式定義的屬性,則應用程式通過設置*StringLength*參數指示該屬性對驅動程式管理員的性質。 *字串長度*可以具有以下值:  
  
-   如果*ValuePtr*是指向字串的指標,則*StringLength*是字串的長度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*StringLength 中*。 這將在*字串長度*中放置負值。  
  
-   如果*ValuePtr*是指向字串或二進位元字串以外的值的指標,則*StringLength*應具有該值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定長度值,則*StringLength*會根據需要SQL_IS_INTEGER或SQL_IS_UINTEGER。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetStmtAttr**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*語句句柄*的*句柄*。 下表列出了**SQLSetStmtAttr**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|驅動程式不支援*ValuePtr*中指定的值,或者*ValuePtr*中指定的值由於實現工作條件而無效,因此驅動程式替換了類似的值。 (可以調用**SQLGetStmtAttr**以確定臨時替換的值。替換值對*語句處理*有效,直到游標關閉,此時語句屬性將還原到其上一個值。 可以變更的語片屬性包括:<br /><br /> SQL_ATTR_ROW_ARRAY_SIZE ATTR_MAX_ROWS SQL_ SQL_ ATTR_KEYSET_SIZE ATTR_CURSOR_TYPE ATTR_CONCURRENCY SQL_ SQL_SQL_ATTR_QUERY_TIMEOUTSQL_SQL_SQL_SQL_SQL_SQL_SQL_ATTR_MAX_LENGTHSQL_SQL_SQL_SQL_SQL_SQL_SQL_ATTR_SIMULATE_CURSOR<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|*屬性*SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 或SQL_ATTR_USE_BOOKMARKS,並且游標已打開。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY009|不合法的空白指標|*屬性*參數標識了需要字串屬性的語句屬性 *,ValuePtr*參數為空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLSetStmtAttr**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY011|無法立即設定屬性|*屬性*SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR或SQL_ATTR_USE_BOOKMARKS,並編寫了該聲明。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY017|自動配置的描述符句柄的不合法的使用|(DM)*屬性*參數SQL_ATTR_IMP_ROW_DESC或SQL_ATTR_IMP_PARAM_DESC。<br /><br /> (DM)*屬性*參數SQL_ATTR_APP_ROW_DESC或*SQL_ATTR_APP_PARAM_DESC,ValuePtr*中的值是隱式分配的描述符句柄,而不是最初為 ARD 或 APD 分配的句柄。|  
|HY024|不合法屬性值|給定指定的*屬性*值,在*ValuePtr*中指定了無效值。 (驅動程式管理員僅對接受一組離散值(如SQL_ATTR_ACCESS_MODE或SQL_ATTR_ASYNC_ENABLE)的連接和語句屬性返回此 SQLSTATE。 對所有其他連線與敘述屬性,驅動程式必須驗證*ValuePtr*中指定的值 。<br /><br /> *屬性*參數SQL_ATTR_APP_ROW_DESC或*SQL_ATTR_APP_PARAM_DESC,ValuePtr*是顯式分配的描述符句柄,與*語句句柄*參數的連接不相同。|  
|HY090|不合法的字串或緩衝區長度|(DM) * \*ValuePtr*是一個字串,*字串長度*參數小於 0,但不是SQL_NTS。|  
|HY092|不合法屬性/選項識別碼|(DM) 為參數*屬性*指定的值對驅動程式支援的 ODBC 版本無效。<br /><br /> (DM) 為參數*屬性*指定的值是唯讀屬性。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|為參數*屬性*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC 語句屬性,但驅動程式不支援該屬性。<br /><br /> *屬性*參數SQL_ATTR_ASYNC_ENABLE,並且對**SQLGetInfo**的呼叫(帶有SQL_ASYNC_MODE*的資訊類型*返回SQL_AM_CONNECTION。<br /><br /> *屬性*參數SQL_ATTR_ENABLE_AUTO_IPD,連接屬性SQL_ATTR_AUTO_IPD的值SQL_FALSE。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|S1118|驅動程式不支援非同步通知|如果呼叫 SQLSetStmtAttr 設定為設定SQL_ATTR_ASYNC_STMT_EVENT;如果呼叫**SQLSetStmtAttr**以設定SQL_ATTR_ASYNC_STMT_EVENT驅動程式不支援非同步通知。|  
  
## <a name="comments"></a>註解  
 語句的語句屬性保持有效,直到它們被另一個調用**SQLSetStmtAttr**更改,或者直到通過調用**SQLFreeHandle**刪除語句。 使用SQL_CLOSE、SQL_UNBIND或SQL_RESET_PARAMS選項調用**SQLFreeStmt**不會重置語句屬性。  
  
 如果數據來源不支援*ValuePtr*中指定的值,則某些語句屬性支援替換類似的值。 在這種情況下,驅動程式返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02(選項值已更改)。 例如,如果*屬性*為*SQL_ATTR_CONCURRENCY,ValuePtr*是SQL_CONCUR_ROWVER,並且數據源不支援此功能,則驅動程式將替換SQL_CONCUR_VALUES並返回SQL_SUCCESS_WITH_INFO。 要確定取代值,應用程式呼叫**SQLGetStmtAttr**。  
  
 使用*ValuePtr*設定的資訊集的格式來取決於指定的*屬性*。 **SQLSetStmtAttr**以兩種不同格式之一接受屬性資訊:字串或整數值。 每個格式在屬性的說明中註明。 此格式適用於**SQLGetStmtAttr**中每個屬性返回的資訊。 **SQLSetStmtAttr**的*ValuePtr*參數指向的字串的長度為*字串長度*。  
  
> [!NOTE]
>  通過調用**SQLSetConnect Attr**在連接級別設置語句屬性的能力已在 ODBC *3.x*中被棄用。 ODBC *3.x*應用程式絕不應在連接級別設置語句屬性。 ODBC *3.x*語句屬性無法在連接級別設置,SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE屬性除外,這些屬性既是連接屬性,也是語句屬性,可以在連接級別或語句級別進行設置。  
> 
> [!NOTE]
>  ODBC *3.x*驅動程式僅需要支援此功能,如果它們應與在連接級別設置 ODBC *2.x*語句選項的 ODBC *2.x*應用程式配合使用。 有關詳細資訊,請參閱附錄 G 中的[SQLSetConnectOption 映射](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)下的「在連接層級設定語句選項」:向後相容性的驅動程式指南。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>設定描述字列的敘述屬性  
 許多語句屬性對應於描述符的標頭欄位。 設置這些屬性實際上會導致設置描述符欄位。 通過調用**SQLSetStmtAttr**而不是**SQLSetDescField**設置欄位的優點是,不需要為函數調用獲取描述符句柄。  
  
> [!CAUTION]  
>  為一個語句調用**SQLSetStmtAttr**可能會影響其他語句。 當顯式分配與語句關聯的 APD 或 ARD 並與其他語句關聯時,將發生這種情況。 由於**SQLSetStmtAttr**修改 APD 或 ARD,因此修改將應用於與此描述符關聯的所有語句。 如果這不是必需的行為,應用程式應在再次調用**SQLStmtAttr**之前將此描述符與其他語句(通過呼叫**SQLSetStmtAttr**將SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC欄位設置為其他描述符句柄)分離。  
  
 當描述符欄位設置為正在設置的相應語句屬性的結果時,該欄位僅針對當前與*語句句柄*參數標識的語句關聯的適用描述符設定,並且屬性設置不會影響將來可能與該語句關聯的任何描述符。 當一個也是語句屬性的描述符位元元元由對**SQLSetDescField**的調用設置時,將設置相應的語句屬性。 如果顯式分配的描述符與語句分離,則對應於標頭欄位的語句屬性將恢復為隱式分配的描述符中的欄位的值。  
  
 分配語句時(請參閱[SQLAllocHandle),](../../../odbc/reference/syntax/sqlallochandle-function.md)四個描述符句柄將自動分配並與語句關聯。 顯式分配的描述符句柄可以通過調用**SQLAllocHandle**與*SQL_HANDLE_DESCfHandleType*進行關聯,以分配描述符句柄,然後調用**SQLSetStmtAttr**將描述符句柄與語句相關聯。  
  
 下表中的語句屬性對應於描述符標頭欄位。  
  
|語句屬性|標題欄位|德克|  
|-------------------------|------------------|-----------|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|APD|  
|SQL_ATTR_PARAM_BIND_TYPE|SQL_DESC_BIND_TYPE|APD|  
|SQL_ATTR_PARAM_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|APD|  
|SQL_ATTR_PARAM_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|IPD|  
|SQL_ATTR_PARAMS_PROCESSED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|IPD|  
|SQL_ATTR_PARAMSET_SIZE|SQL_DESC_ARRAY_SIZE|APD|  
|SQL_ATTR_ROW_ARRAY_SIZE|SQL_DESC_ARRAY_SIZE|阿爾德|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR|SQL_DESC_BIND_OFFSET_PTR|阿爾德|  
|SQL_ATTR_ROW_BIND_TYPE|SQL_DESC_BIND_TYPE|阿爾德|  
|SQL_ATTR_ROW_OPERATION_PTR|SQL_DESC_ARRAY_STATUS_PTR|阿爾德|  
|SQL_ATTR_ROW_STATUS_PTR|SQL_DESC_ARRAY_STATUS_PTR|稅務局|  
|SQL_ATTR_ROWS_FETCHED_PTR|SQL_DESC_ROWS_PROCESSED_PTR|稅務局|  
  
## <a name="statement-attributes"></a>陳述式屬性  
 當前定義的屬性及其引入的 ODBC 版本顯示在下表中;預計驅動程式將定義更多屬性,以利用不同的數據源。 ODBC 保留一系列屬性;驅動程式開發人員必須從 Open Group 為其特定於驅動程式使用保留值。 有關詳細資訊,請參閱[特定於驅動程式的資料類型、描述符類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|屬性|*價值 Ptr*內容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC (ODBC 3.0)|APD 的句柄,用於後續調用語句句柄上的**SQLExecute**和**SQLExecDirect。** 此屬性的初始值是最初分配語句時隱式分配的描述符。 如果此屬性的值設置為SQL_NULL_DESC或最初為描述符分配的句柄,則以前與語句句柄關聯的顯式分配的 APD 句柄將與其分離,並且語句句柄將還原到隱式分配的 APD 句柄。<br /><br /> 此屬性不能設置為隱式分配給另一個語句或在同一語句上隱式設置的另一個描述符句柄;隱含式配置的描述符句柄不能與多個語句或描述符句柄關聯。|  
|SQL_ATTR_APP_ROW_DESC (ODBC 3.0)|語句句柄上的 ARD 句柄,用於後續提取。 此屬性的初始值是最初分配語句時隱式分配的描述符。 如果此屬性的值設置為SQL_NULL_DESC或最初為描述符分配的句柄,則以前與語句句柄關聯的顯式分配的 ARD 句柄將與其分離,並且語句句柄將還原到隱式分配的 ARD 句柄。<br /><br /> 此屬性不能設置為隱式分配給另一個語句或在同一語句上隱式設置的另一個描述符句柄;隱含式配置的描述符句柄不能與多個語句或描述符句柄關聯。|  
|SQL_ATTR_ASYNC_ENABLE (ODBC 1.0)|SQLULEN 值,用於指定呼叫的函數是否非同步執行:<br /><br /> SQL_ASYNC_ENABLE_OFF = 禁用語句級別的非同步執行支援(預設值)。<br /><br /> SQL_ASYNC_ENABLE_ON = 啟用語句級非同步執行支援。<br /><br /> 有關詳細資訊,請參閱[非同步執行(輪詢方法)。](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)<br /><br /> 對於具有語句級非同步執行支援的驅動程式,語句屬性SQL_ATTR_ASYNC_ENABLE唯讀取。 其值與分配語句句柄時具有相同名稱的連接級別屬性的值相同。<br /><br /> 呼叫**SQLSetStmtAttr**以在SQL_ASYNC_MODE*資訊類型*傳回SQL_AM_CONNECTION傳回 SQLSTATE HYC00(未實現可選功能)時設置SQL_ATTR_ASYNC_ENABLE。 有關詳細資訊,請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)瞭解更多資訊。|  
|SQL_ATTR_ASYNC_STMT_EVENT (ODBC 3.8)|作為事件句柄的 SQLPOINTER 值。<br /><br /> 通過調用**SQLSetStmtAttr**來設置**SQL_ATTR_ASYNC_STMT_EVENT**屬性並指定事件句柄,從而啟用非同步函數的完成通知。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK (ODBC 3.8)|非同步回檔函數的 SQLPOINTER。<br /><br /> 只有驅動程式管理器可以使用此屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT (ODBC 3.8)|內容結構的 SQLPOINTER<br /><br /> 只有驅動程式管理器可以使用此屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_CONCURRENCY (ODBC 2.0)|指定游標並發的 SQLULEN 值:<br /><br /> SQL_CONCUR_READ_ONLY = 游標是唯讀的。 不允許更新。<br /><br /> SQL_CONCUR_LOCK = Cursor 使用盡可能低的鎖定級別來確保可以更新行。<br /><br /> SQL_CONCUR_ROWVER = 游標使用樂觀併發控制,比較行版本,如 SQLBase ROWID 或 Sybase TIMESTAMP。<br /><br /> SQL_CONCUR_VALUES = 游標使用樂觀併發控制,比較值。<br /><br /> SQL_ATTR_CONCURRENCY的預設值為SQL_CONCUR_READ_ONLY。<br /><br /> 無法為打開的游標指定此屬性。 有關詳細資訊,請參閱[並發類型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果SQL_ATTR_CURSOR_TYPE*屬性*更改為不支援當前值SQL_ATTR_CONCURRENCY的類型,則在執行時將更改SQL_ATTR_CONCURRENCY值,並在調用**SQLExecDirect**或**SQLPrepare**時發出警告。<br /><br /> 如果驅動程式支援**選擇更新**語句,並且在將SQL_ATTR_CONCURRENCY的值設置為SQL_CONCUR_READ_ONLY時執行此類語句,則將返回錯誤。 如果SQL_ATTR_CONCURRENCY的值更改為驅動程式支援的值,該值為 SQL_ATTR_CURSOR_TYPE,而不是當前值 SQL_ATTR_CURSOR_TYPE,則在執行時將更改SQL_ATTR_CURSOR_TYPE值,並在調用**SQLExecDirect**或**SQLPrepare**時發出 SQLSTATE 01S02(選項值已更改)的值。<br /><br /> 如果數據源不支援指定的併發,驅動程式將替換不同的併發併發並返回 SQLSTATE 01S02(選項值已更改)。 對於SQL_CONCUR_VALUES,驅動程式替換SQL_CONCUR_ROWVER,反之亦然。 對於SQL_CONCUR_LOCK,駕駛員按順序替換SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES。 直到執行時間,才會檢查替換值的有效性。<br /><br /> 有關SQL_ATTR_CONCURRENCY與其他游標屬性之間的關係的詳細資訊,請參閱[游標特徵和游標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE (ODBC 3.0)|指定應用程式所需的支援級別的 SQLULEN 值。 設置此屬性會影響對**SQLExecDirect**和**SQLExecute 的**後續調用。<br /><br /> SQL_NONSCROLLABLE = 語句句柄不需要可滾動遊標。 如果應用程式在此句柄上調用**SQLFetchScroll,** 則*提取方向*的唯一有效值SQL_FETCH_NEXT。 這是預設值。<br /><br /> SQL_SCROLLABLE = 語句句柄上需要可滾動的遊標。 調用**SQLFetchScroll**時,應用程式可以指定任何有效的*Fetch 方向*值,從而在順序模式以外的模式中實現游標定位。<br /><br /> 有關可滾動遊標的詳細資訊,請參閱[可滾動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 有關SQL_ATTR_CURSOR_SCROLLABLE與其他游標屬性之間的關係的詳細資訊,請參閱[游標特徵和游標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY (ODBC 3.0)|SQLULEN 值,用於指定語句句柄上的游標是否使另一個游標對結果集所做的更改可見。 設置此屬性會影響對**SQLExecDirect**和**SQLExecute 的**後續調用。 應用程式可以讀取此屬性的值,以獲取應用程式最近設置的初始狀態或其狀態。<br /><br /> SQL_UNSPECIFIED = 未指定游標類型,以及語句句柄上的游標是否使另一個游標對結果集所做的更改可見。 語句句柄上的游標可能使任何、某些或所有此類更改都變得可見。 這是預設值。<br /><br /> SQL_INSENSITIVE = 語句句柄上的所有遊標都顯示結果集,而不反映任何其他游標對它所做的任何更改。 不敏感的游標是唯讀的。 這對應於靜態游標,該靜態游標具有唯讀的併發。<br /><br /> SQL_SENSITIVE = 語句句柄上的所有遊標都使另一個游標對結果集所做的所有更改都可見。<br /><br /> 有關SQL_ATTR_CURSOR_SENSITIVITY與其他游標屬性之間的關係的詳細資訊,請參閱[游標特徵和游標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE (ODBC 2.0)|指定游標型態的 SQLULEN 值:<br /><br /> SQL_CURSOR_FORWARD_ONLY = 游標僅向前滾動。<br /><br /> SQL_CURSOR_STATIC = 結果集中的數據是靜態的。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 驅動程式保存並使用鍵SQL_ATTR_KEYSET_SIZE語句屬性中指定的行數。<br /><br /> SQL_CURSOR_DYNAMIC = 驅動程式僅保存和使用行集中行的鍵。<br /><br /> 默認值為SQL_CURSOR_FORWARD_ONLY。 在準備 SQL 語句後,無法指定此屬性。<br /><br /> 如果數據源不支援指定的游標類型,驅動程式將替換不同的游標類型並返回 SQLSTATE 01S02(選項值已更改)。 對於混合或動態游標,驅動程式按順序替換按鍵集驅動的或靜態游標。 對於鍵集驅動的游標,驅動程式將替換靜態游標。<br /><br /> 有關可滾動游標類型的詳細資訊,請參閱[可滾動游標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 有關SQL_ATTR_CURSOR_TYPE與其他游標屬性之間的關係的詳細資訊,請參閱[游標特徵和游標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD (ODBC 3.0)|指定是否執行 IPD 的自動填滿的 SQLULEN 值:<br /><br /> SQL_TRUE = 呼叫**SQLPrepare**後打開 IPD 的自動填充。 SQL_FALSE = 呼叫**SQLPrepare**後關閉 IPD 的自動填充。 (如果支援,應用程式仍可以通過呼叫**SQLDescribeParam**來獲取 IPD 欄位資訊。語句屬性SQL_ATTR_ENABLE_AUTO_IPD的預設值為SQL_FALSE。 關於詳細資訊,請參考[IPD 的自動填滿](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR (ODBC 3.0)|指向二進位\*書籤值的 SQLLEN。 當**SQLFetchScroll**呼叫*fFetch 方向*等於SQL_FETCH_BOOKMARK時,驅動程式將從此字段拾取書籤值。 此欄位預設為空指標。 有關詳細資訊,請參閱[按書籤滾動](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 此欄位指向的值不用於按書籤刪除、按書籤更新或按**SQLBulk 操作**中的書籤操作提取,該操作使用在行集緩衝區中緩存的書籤。|  
|SQL_ATTR_IMP_PARAM_DESC (ODBC 3.0)|IPD 的句柄。 此屬性的值是最初分配語句時分配的描述符。 應用程式無法設置此屬性。<br /><br /> 此屬性可以通過對**SQLGetStmtAttr**的調用檢索,但不能通過調用**SQLSetStmtAttr**來設置。|  
|SQL_ATTR_IMP_ROW_DESC (ODBC 3.0)|IRD 的句柄。 此屬性的值是最初分配語句時分配的描述符。 應用程式無法設置此屬性。<br /><br /> 此屬性可以通過對**SQLGetStmtAttr**的調用檢索,但不能通過調用**SQLSetStmtAttr**來設置。|  
|SQL_ATTR_KEYSET_SIZE (ODBC 2.0)|一個 SQLULEN,用於指定鍵集驅動的游標的鍵集中的行數。 如果鍵集大小為 0(預設值),則游標為完全鍵集驅動。 如果鍵集大小大於 0,則游標是混合的(鍵集中內鍵集驅動,鍵集外部的動態)。 默認鍵集大小為 0。 有關鍵集驅動的游標的詳細資訊,請參閱[鍵集驅動的遊標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定大小超過最大鍵集大小,驅動程式將替換該大小並返回 SQLSTATE 01S02(選項值已更改)。<br /><br /> 如果鍵集大小大於 0 且小於行集大小 **,SQLFetch** **或 SQLFetchScroll**將返回錯誤。|  
|SQL_ATTR_MAX_LENGTH (ODBC 1.0)|SQLULEN 值,用於指定驅動程式從字元或二進位列返回的最大資料量。 如果*ValuePtr*小於可用數據的長度 **,SQLFetch**或**SQLGetData**會截取數據並返回SQL_SUCCESS。 如果*ValuePtr*為 0(預設值),驅動程式將嘗試返回所有可用數據。<br /><br /> 如果指定的長度小於數據源可以返回的最小資料量或大於數據源可以返回的最大資料量,驅動程式將替換該值並返回 SQLSTATE 01S02(選項值已更改)。<br /><br /> 此屬性的值可以在打開的游標上設置;也可以在打開的游標上設置此屬性的值。但是,該設置可能不會立即生效,在這種情況下,驅動程式將返回 SQLSTATE 01S02(選項值已更改)並將屬性重置為其原始值。<br /><br /> 此屬性旨在減少網路流量,並且僅當多層驅動程式中的數據源(而不是驅動程式)可以實現時,才應支援此屬性。 應用程式不應使用此機制來截截數據;因此,應用程式不應使用此機制來截截數據。為了截斷接收的數據,應用程式應在**SQLBindCol**或**SQLGetData**中的*緩衝區長度*參數中指定最大緩衝區長度。|  
|SQL_ATTR_MAX_ROWS (ODBC 1.0)|與要返回到**SELECT**語句的應用程式的最大行數對應的 SQLULEN 值。 如果\* *ValuePtr*等於 0(預設值),則驅動程式將返回所有行。<br /><br /> 此屬性旨在減少網路流量。 從概念上講,在創建結果集時應用它,並將結果集限制為第一個*ValuePtr*行。 如果結果集中的行數大於*ValuePtr,* 則結果集將被截斷。<br /><br /> SQL_ATTR_MAX_ROWS應用於*語句*上的所有結果集,包括目錄函數返回的結果集。 SQL_ATTR_MAX_ROWS為游標行計數的值建立最大值。<br /><br /> 如果驅動程式不能保證SQL_ATTR_MAX_ROWS將正確實現,則驅動程式不應類比**SQLFetch**或**SQLFetchScroll** SQL_ATTR_MAX_ROWS行為(如果無法在數據源中實現結果集大小限制)。<br /><br /> 它是驅動程式定義的SQL_ATTR_MAX_ROWS是否適用於 SELECT 語句以外的語句(如目錄函數)。<br /><br /> 此屬性的值可以在打開的游標上設置;也可以在打開的游標上設置此屬性的值。但是,該設置可能不會立即生效,在這種情況下,驅動程式將返回 SQLSTATE 01S02(選項值已更改)並將屬性重置為其原始值。|  
|SQL_ATTR_METADATA_ID (ODBC 3.0)|SQLULEN 值,用於確定如何處理目錄函數的字串參數。<br /><br /> 如果SQL_TRUE,目錄函數的字串參數將被視為標識碼。 情況並不嚴重。 對於非分隔字串,驅動程式刪除任何尾隨空格,並將字串摺疊到大寫。 對於分隔字串,驅動程式刪除任何前導或尾隨空格,並從字面上獲取分隔符之間的任何內容。 如果這些參數之一設置為空指標,則函數將返回SQL_ERROR和 SQLSTATE HY009(無效使用空指標)。<br /><br /> 如果SQL_FALSE,目錄函數的字串參數不被視為標識碼。 案件意義重大。 它們可以包含字串搜索模式,也可以不包含字串搜索模式,具體取決於參數。<br /><br /> 默認值為SQL_FALSE。<br /><br /> **SQLTables**的*表類型*參數 (它採用值清單) 不受此屬性的影響。<br /><br /> 也可以在連接級別設置SQL_ATTR_METADATA_ID。 (它和SQL_ATTR_ASYNC_ENABLE是唯一也是連接屬性的語句屬性。<br /><br /> 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN (ODBC 1.0)|SQLULEN 值,指示驅動程式是否應掃描 SQL 字串的逸出序列:<br /><br /> SQL_NOSCAN_OFF = 驅動程式掃描 SQL 字串以搜尋轉義序列(預設值)。<br /><br /> SQL_NOSCAN_ON = 驅動程式不掃描 SQL 字串的逸出序列。 相反,驅動程式將語句直接發送到數據源。<br /><br /> 有關詳細資訊,請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN = 值,指向添加到用於更改動態參數綁定的指標的偏移量。 如果此欄位為非空,則驅動程式將引用指標,將已引用的值添加到描述符記錄中的每個延遲欄位(SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR),並在綁定時使用新的指標值。 預設情況下,它設置為 null。<br /><br /> 綁定偏移量始終直接添加到SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR欄位。 如果偏移更改為其他值,則新值仍直接添加到描述符欄位中的值。 新偏移量不會添加到欄位值加上任何較早的偏移量中。<br /><br /> 有關詳細資訊,請參閱[參數綁定偏移量](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 設定語句屬性將設置 APD 標頭中的SQL_DESC_BIND_OFFSET_PTR欄位。|  
|SQL_ATTR_PARAM_BIND_TYPE (ODBC 3.0)|一個 SQLULEN 值,指示要用於動態參數的綁定方向。<br /><br /> 此欄位設定為SQL_PARAM_BIND_BY_COLUMN(預設值)以選擇按列方向綁定。<br /><br /> 要選擇按行綁定,此欄位設置為將綁定到一組動態參數的結構或緩衝區實例的長度。 此長度必須包括所有綁定參數的空間以及結構或緩衝區的任何填充,以確保當綁定參數的位址以指定長度遞增時,結果將指向下一組參數中同一參數的開頭。 在 ANSI C 中使用*大小*運算符時,此行為得到保證。<br /><br /> 有關詳細資訊,請參閱[參數的綁定陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 設置此語句屬性將設置 aPD 標頭中SQL_DESC_BIND_TYPE欄位。|  
|SQL_ATTR_PARAM_OPERATION_PTR (ODBC 3.0)|指向 SQLUSMALLINT 值的 SQLUSMALLINT\*值,用於在執行 SQL 語句期間忽略參數的 SQLUSMALLINT 值陣組。 每個值設置為SQL_PARAM_PROCEED(要執行的參數)或SQL_PARAM_IGNORE(要忽略的參數)。<br /><br /> 在處理過程中,通過將 APD 中的SQL_DESC_ARRAY_STATUS_PTR指向的陣列中的狀態值設置為SQL_PARAM_IGNORE,可以忽略一組參數。 如果一組參數的狀態值設置為SQL_PARAM_PROCEED或陣列中未設置任何元素,則處理其狀態值。<br /><br /> 此語句屬性可以設置為空指標,在這種情況下,驅動程式不返回參數狀態值。 可以隨時設置此屬性,但直到下次調用**SQLExecDirect**或**SQLExecute**時才會使用新值。<br /><br /> 如果沒有綁定參數,將忽略此屬性。<br /><br /> 有關詳細資訊,請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定語句屬性將設置 APD 標頭中SQL_DESC_ARRAY_STATUS_PTR欄位。|  
|SQL_ATTR_PARAM_STATUS_PTR (ODBC 3.0)|SQLUSMALLINT\*值,該值指向 SQLUSMALLINT 值陣列,該值包含對 SQLExecute 或**SQLExecDirect****SQLExecDirect**調用後每行參數值的狀態資訊。 僅當PARAMSET_SIZE大於 1 時,才需要此欄位。<br /><br /> 狀態值可以包含以下值:<br /><br /> SQL_PARAM_SUCCESS:已成功為這組參數執行 SQL 語句。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO:已成功為這組參數執行 SQL 語句;但是,診斷數據結構中提供了警告資訊。<br /><br /> SQL_PARAM_ERROR:處理這組參數時出錯。 診斷數據結構中提供了其他錯誤資訊。<br /><br /> SQL_PARAM_UNUSED:此參數集未使用,可能是因為以前的一些參數集導致錯誤中止了進一步處理,或者因為SQL_PARAM_IGNORE為SQL_ATTR_PARAM_OPERATION_PTR指定的陣列中該參數集設置了。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE:驅動程式將參數陣列視為單片單元,因此不會生成此級別的錯誤資訊。<br /><br /> 此語句屬性可以設置為空指標,在這種情況下,驅動程式不返回參數狀態值。 可以隨時設置此屬性,但直到下次調用**SQLExecute**或**SQLExecDirect**時才會使用新值。 請注意,設置此屬性可能會影響驅動程式實現的輸出參數行為。<br /><br /> 有關詳細資訊,請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定此語句屬性將設置 IPD 標頭中SQL_DESC_ARRAY_STATUS_PTR欄位。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR (ODBC 3.0)|指向緩衝區的\*SQLULEN 記錄欄位,用於返回已處理的參數集數,包括錯誤集。 如果這是空指標,則不會返回任何數位。<br /><br /> 設定此語句屬性將設置 IPD 標頭中的SQL_DESC_ROWS_PROCESSED_PTR欄位。<br /><br /> 如果對**SQLExecDirect**或**SQLExecute**的調用填充此屬性指向的緩衝區未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則緩衝區的內容未定義。<br /><br /> 有關詳細資訊,請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|SQL_ATTR_PARAMSET_SIZE (ODBC 3.0)|指定每個參數的值數的 SQLULEN 值。 如果SQL_ATTR_PARAMSET_SIZE大於 APD 指向陣列的 1、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR。 每個陣列的基數等於此欄位的值。<br /><br /> 如果沒有綁定參數,將忽略此屬性。<br /><br /> 有關詳細資訊,請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定語句屬性將設置 APD 標頭中的SQL_DESC_ARRAY_SIZE欄位。|  
|SQL_ATTR_QUERY_TIMEOUT (ODBC 1.0)|SQLULEN 值對應於等待 SQL 語句執行後返回到應用程式的秒數。 如果*ValuePtr*等於 0(預設值),則沒有超時。<br /><br /> 如果指定的超時超過數據源中的最大超時或小於最小超時 **,SQLSetStmtAttr**將替換該值並返回 SQLSTATE 01S02(選項值已更改)。<br /><br /> 請注意,如果**SELECT**語句超時,應用程式無需調用**SQLCloseCursor**來重用該語句。<br /><br /> 此語句屬性中的查詢超時設置在同步和非同步模式下都有效。|  
|SQL_ATTR_RETRIEVE_DATA (ODBC 2.0)|SQLULEN 值:<br /><br /> SQL_RD_ON = **SQLFetchScroll,** 在 ODBC *3.x*中 **,SQLFetch**在將游標定位到指定位置后檢索數據。 這是預設值。<br /><br /> SQL_RD_OFF = **SQLFetchScroll,** 在 ODBC *3.x*中 **,SQLFetch**在定位游標後不會檢索數據。<br /><br /> 通過將SQL_RETRIEVE_DATA設置為SQL_RD_OFF,應用程式可以驗證行是否存在或檢索行的書籤,而不會產生檢索行的開銷。 有關詳細資訊,請參閱[捲動和提取行](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 此屬性的值可以在打開的游標上設置;也可以在打開的游標上設置此屬性的值。但是,該設置可能不會立即生效,在這種情況下,驅動程式將返回 SQLSTATE 01S02(選項值已更改)並將屬性重置為其原始值。|  
|SQL_ATTR_ROW_ARRAY_SIZE (ODBC 3.0)|SQLULEN 值,用於指定每次調用**SQLFetch**或**SQLFetchScroll**返回的行數。 這也是**SQLBulk 操作**中批量書籤操作中使用的書籤陣列中的行數。 預設值為 1。<br /><br /> 如果指定的行集大小超過數據來源支援的最大列集大小,驅動程式將替換該值並返回 SQLSTATE 01S02(選項值已更改)。<br /><br /> 有關詳細資訊,請參閱[行集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 設置語句屬性將設置ARD標頭中SQL_DESC_ARRAY_SIZE欄位。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR (ODBC 3.0)|SQLULEN = 值,指向添加到指標以更改列數據綁定的偏移量。 如果此欄位為非空,則驅動程式將引用指標,將已引用的值添加到描述符記錄中的每個延遲欄位(SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR),並在綁定時使用新的指標值。 預設情況下,它設置為 null。<br /><br /> 設置語句屬性將設置ARD標頭中SQL_DESC_BIND_OFFSET_PTR欄位。|  
|SQL_ATTR_ROW_BIND_TYPE (ODBC 1.0)|SQLULEN 值,用於設定在關聯語句上調用**SQLFetch**或**SQLFetchScroll**時要使用的綁定方向。 通過將值設置為SQL_BIND_BY_COLUMN來選擇按列綁定。 通過將值設置為將結果列綁定到的緩衝區或緩衝區實例的長度來選擇行綁定。<br /><br /> 如果指定了長度,它必須包含所有綁定列的空間以及結構或緩衝區的任何填充,以確保當綁定列的位址以指定長度遞增時,結果將指向下一行中同一列的開頭。 在 ANSI C 中使用具有結構或聯合**的大小**運算符時,此行為得到保證。<br /><br /> 列綁定是**SQLFetch**和**SQLFetchScroll**的預設綁定方向。<br /><br /> 有關詳細資訊,請參閱[綁定列以與區塊游標一起使用](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 設置語句屬性將設置 SQL_DESC_BIND_TYPE 欄位在 ARD 標頭中。|  
|SQL_ATTR_ROW_NUMBER (ODBC 2.0)|SQLULEN 值,它是整個結果集中的當前行的編號。 如果無法確定當前行的數量或沒有當前行,則驅動程式返回 0。<br /><br /> 此屬性可以通過對**SQLGetStmtAttr**的調用檢索,但不能通過調用**SQLSetStmtAttr**來設置。|  
|SQL_ATTR_ROW_OPERATION_PTR (ODBC 3.0)|指向 SQLUSMALLINT\*值的值,用於使用**SQLSetPos**在批量操作期間忽略行的 SQLUSMALLINT 值陣列。 每個值設置為SQL_ROW_PROCEED(用於在批量操作中包含行)或SQL_ROW_IGNORE(將行從批量操作中排除)。 (在調用**SQLBulk 操作**期間使用此陣列不能忽略行。<br /><br /> 此語句屬性可以設置為空指標,在這種情況下,驅動程式不會返回行狀態值。 可以隨時設置此屬性,但直到下次調用**SQLSetPos**時才會使用新值。<br /><br /> 有關詳細資訊,請參閱使用[SQLSetPos 更新行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md),以及[使用 SQLSetPos 在行集中刪除行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 設置此語句屬性將設置ARD中SQL_DESC_ARRAY_STATUS_PTR欄位。|  
|SQL_ATTR_ROW_STATUS_PTR (ODBC 3.0)|指向 SQLFetch\*或**SQLFetchScroll**呼叫後包含行狀態值的 SQLUSMALLINT 值陣列的 SQLUSMALLINT 值的值。 **SQLFetch** 陣列具有與行集中的行一樣多的元素。<br /><br /> 此語句屬性可以設置為空指標,在這種情況下,驅動程式不會返回行狀態值。 此屬性可以隨時設置,但新值在下次調用**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos**之前不會使用。 **SQLFetchScroll**<br /><br /> 有關詳細資訊,請參閱[已提取的行數和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 設定語句屬性將設置 IRD 標頭中SQL_DESC_ARRAY_STATUS_PTR欄位。<br /><br /> 此屬性由 ODBC *2.x*驅動程式映射到對**SQL 擴展獲取**調用中的*rgbRowStatus*陣列。|  
|SQL_ATTR_ROWS_FETCHED_PTR (ODBC 3.0)|指向一個緩衝區\*的 SQLULEN 值,該緩衝區用於返回調用**SQLFetch**或**SQLFetchScroll**後獲取的行數;受調用**SQLSetPos**執行的大量操作影響的行數,*操作*參數為 SQL_REFRESH;或受**SQLBulk 操作**執行的批量操作影響的行數。 此數位包括錯誤行。<br /><br /> 有關詳細資訊,請參閱[已提取的行數和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 設定語句屬性將設置 IRD 標頭中SQL_DESC_ROWS_PROCESSED_PTR欄位。<br /><br /> 如果對**SQLFetch**或**SQLFetchScroll**的調用填充此屬性指向的緩衝區未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則緩衝區的內容未定義。|  
|SQL_ATTR_SIMULATE_CURSOR (ODBC 2.0)|SQLULEN 值,用於指定類比定位更新和刪除語句的驅動程式是否保證此類語句僅影響一行。<br /><br /> 要類比定位的更新和刪除語句,大多數驅動程式都會構造搜索**的更新**或**DELETE**語句,其中包含一個**WHERE**子句,該子句指定當前行中每列的值。 除非這些列構成唯一的鍵,否則此類語句可能會影響多個行。<br /><br /> 為了保證此類語句僅影響一行,驅動程式確定唯一鍵中的列並將這些列添加到結果集中。 如果應用程式保證結果集中的列構成唯一的鍵,則不需要驅動程式這樣做。 這可能會縮短執行時間。<br /><br /> SQL_SC_NON_UNIQUE = 驅動程式不保證類比定位更新或刪除語句僅影響一行;因此,驅動程式不保證將只影響一行。這是應用程式的責任這樣做。 如果語句影響多個行 **,SQLExecute、SQLExecDirect**或**SQLSetPos**將返回 SQLSTATE 01001(**SQLExecDirect**遊標操作衝突)。<br /><br /> SQL_SC_TRY_UNIQUE = 驅動程式嘗試保證模擬定位更新或刪除語句僅影響一行。 驅動程序始終執行此類語句,即使它們可能會影響多個行,例如沒有唯一鍵時。 如果語句影響多個行 **,SQLExecute、SQLExecDirect**或**SQLSetPos**將返回 SQLSTATE 01001(**SQLExecDirect**遊標操作衝突)。<br /><br /> SQL_SC_UNIQUE = 驅動程式保證模擬定位更新或刪除語句僅影響一行。 如果驅動程式無法保證給定語句的此參數 **,SQLExecDirect**或**SQLPrepare**將返回錯誤。<br /><br /> 如果數據來源為定位更新和刪除語句提供本機 SQL 支援,並且驅動程式不模擬游標,則當請求SQL_SIMULATE_CURSORSQL_SC_UNIQUE時,將返回SQL_SUCCESS。 如果請求SQL_SC_TRY_UNIQUE或SQL_SC_NON_UNIQUE,則返回SQL_SUCCESS_WITH_INFO。 如果數據源提供SQL_SC_TRY_UNIQUE級別的支援,而驅動程式不提供,則返回SQL_SUCCESSSQL_SC_TRY_UNIQUE,併為SQL_SC_NON_UNIQUE返回SQL_SUCCESS_WITH_INFO。<br /><br /> 如果數據源不支援指定的游標類比類型,驅動程式將替換不同的類比類型並返回 SQLSTATE 01S02(選項值已更改)。 對於SQL_SC_UNIQUE,駕駛員按順序替換SQL_SC_TRY_UNIQUE或SQL_SC_NON_UNIQUE。 對於SQL_SC_TRY_UNIQUE,駕駛員將替換SQL_SC_NON_UNIQUE。<br /><br /> 默認值為SQL_SC_UNIQUE。<br /><br /> 關於詳細資訊,請參閱[模擬定位更新與移除語句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS (ODBC 2.0)|SQLULEN 值,用於指定應用程式是否使用帶有游標的書籤:<br /><br /> SQL_UB_OFF = 關閉(預設值)<br /><br /> SQL_UB_VARIABLE = 應用程式將使用帶有游標的書籤,如果支援,驅動程式將提供可變長度書籤。 SQL_UB_FIXED在 ODBC *3.x*中棄用。 ODBC *3.x*應用程式應始終使用可變長度書籤,即使使用 ODBC *2.x*驅動程式(僅支援 4 位元組、固定長度書籤)。 這是因為固定長度書籤只是可變長度書籤的特殊情況。 使用 ODBC *2.x*驅動程式時,驅動程式管理器將SQL_UB_VARIABLE映射到SQL_UB_FIXED。<br /><br /> 要將書籤與游標一起使用,應用程式必須在打開游標之前使用SQL_UB_VARIABLE值指定此屬性。<br /><br /> 有關詳細資訊,請參閱[檢索書籤](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [1] 僅當描述符是實現描述符而不是應用程式描述符時,才能非同步調用這些函數。  
  
 請參考[列-Wise 繫結](../../../odbc/reference/develop-app/column-wise-binding.md)與[行-Wise 的結合 。](../../../odbc/reference/develop-app/row-wise-binding.md)  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回連線屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回敘述屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連線屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定描述符的單欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
