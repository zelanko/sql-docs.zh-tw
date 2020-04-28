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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dfbd2144e677d053f6154dfb3a1df1f6c25d9da5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287259"
---
# <a name="sqlsetstmtattr-function"></a>SQLSetStmtAttr 函數
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLSetStmtAttr**會設定與語句相關的屬性。  
  
> [!NOTE]
>  如需 ODBC *3.x 應用程式**與 odbc 2.x*驅動程式搭配使用時，驅動程式管理員將此函式對應至哪個功能的詳細資訊，請參閱對應取代函式[以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 源語句控制碼。  
  
 *特性*  
 源要設定的選項，列在 [批註] 中。  
  
 *ValuePtr*  
 源要與*屬性*相關聯的值。 視*屬性*的值而定， *valueptr 是*將會是下列其中一項：  
  
-   ODBC 描述項控制碼。  
  
-   SQLUINTEGER 值。  
  
-   SQLULEN 值。  
  
-   下列其中一項的指標：  
  
    -   以 null 結束的字元字串。  
  
    -   二進位緩衝區。  
  
    -   SQLLEN、SQLULEN 或 SQLUSMALLINT 類型的值或陣列。  
  
    -   驅動程式定義的值。  
  
 如果*屬性*引數是驅動程式特定的值，則*valueptr 是*可能是帶正負號的整數。  
  
 *StringLength*  
 源如果*attribute*是 ODBC 定義的屬性，而且*valueptr 是*指向字元字串或二進位緩衝區，則這個引數應該是\* *valueptr 是*的長度。 如果*attribute*是 ODBC 定義的屬性，而*valueptr 是*是整數，則會忽略*StringLength* 。  
  
 如果*屬性*是驅動程式定義的屬性，則應用程式會藉由設定*StringLength*引數，來指出該屬性對驅動程式管理員的本質。 *StringLength*可以有下列值：  
  
-   如果*valueptr 是*是字元字串的指標，則*StringLength*是字串或 SQL_NTS 的長度。  
  
-   如果*valueptr 是*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR （*長度*）宏的結果放在*StringLength*中。 這會將負數值放在*StringLength*中。  
  
-   如果*valueptr 是*是字元字串或二進位字串以外的值指標，則*StringLength*應具有 SQL_IS_POINTER 的值。  
  
-   如果*valueptr 是*包含固定長度的值，則*StringLength*會適當地 SQL_IS_INTEGER 或 SQL_IS_UINTEGER。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetStmtAttr**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLSetStmtAttr**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援在*valueptr 是*中指定的值，或在*valueptr 是*中指定的值因為執行中的工作狀況而無效，因此驅動程式會取代類似的值。 （您可以呼叫**SQLGetStmtAttr**來判斷暫時取代的值）。替代值對*StatementHandle*有效，直到資料指標關閉為止，此時語句屬性會還原為先前的值。 可以變更的語句屬性包括：<br /><br /> SQL_ ATTR_CONCURRENCY SQL_ ATTR_CURSOR_TYPE SQL_ ATTR_KEYSET_SIZE SQL_ ATTR_MAX_LENGTH SQL_ ATTR_MAX_ROWS SQL_ ATTR_QUERY_TIMEOUT SQL_ATTR_ROW_ARRAY_SIZE SQL_ ATTR_SIMULATE_CURSOR<br /><br /> （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|*屬性*已 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR 或 SQL_ATTR_USE_BOOKMARKS，而且資料指標已開啟。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY009|Null 指標的使用不正確|*屬性*引數已識別出需要字串屬性的語句屬性，而且*valueptr 是*引數為 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLSetStmtAttr**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY011|無法立即設定屬性|*屬性*已 SQL_ATTR_CONCURRENCY、SQL_ ATTR_CURSOR_TYPE、SQL_ ATTR_SIMULATE_CURSOR 或 SQL_ ATTR_USE_BOOKMARKS，而且已準備語句。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY017|使用自動設定的描述項控制碼無效|（DM）*屬性*引數已 SQL_ATTR_IMP_ROW_DESC 或 SQL_ATTR_IMP_PARAM_DESC。<br /><br /> （DM）*屬性*引數已 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，而*valueptr 是*中的值是隱含配置的描述項控制碼，而非原先配置給 ARD 或 APD 的控制碼。|  
|HY024|不正確屬性值|給定指定的*屬性*值，在*valueptr 是*中指定了不正確值。 （驅動程式管理員只會針對接受一組離散值的連接和語句屬性傳回此 SQLSTATE，例如 SQL_ATTR_ACCESS_MODE 或 SQL_ ATTR_ASYNC_ENABLE。 對於所有其他連接和語句屬性，驅動程式必須確認*valueptr 是*中指定的值）。<br /><br /> *屬性*引數已 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC，而*valueptr 是*是明確配置的描述項控制碼，與*StatementHandle*引數不在相同的連接上。|  
|HY090|不正確字串或緩衝區長度|（DM） * \*valueptr 是*是字元字串，而*StringLength*引數小於0，但不 SQL_NTS。|  
|HY092|不正確屬性/選項識別碼|（DM）為引數*屬性*指定的值，對於驅動程式所支援的 ODBC 版本而言是不正確。<br /><br /> （DM）為引數*屬性*指定的值為唯讀屬性。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|為引數*屬性*指定的值，對驅動程式支援的 odbc 版本而言是有效的 odbc 語句屬性，但驅動程式並不支援。<br /><br /> *屬性*引數已 SQL_ATTR_ASYNC_ENABLE，且*InfoType* SQL_ASYNC_MODE 為的**SQLGetInfo**呼叫會傳回 SQL_AM_CONNECTION。<br /><br /> *屬性*引數已 SQL_ATTR_ENABLE_AUTO_IPD，且連接屬性 SQL_ATTR_AUTO_IPD 的值為 SQL_FALSE。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|S1118|驅動程式不支援非同步通知|如果呼叫**SQLSetStmtAttr**以設定 SQL_ATTR_ASYNC_STMT_EVENT，則為，驅動程式不支援非同步通知。|  
  
## <a name="comments"></a>評價  
 語句的語句屬性會一直有效，直到另一個呼叫**SQLSetStmtAttr** ，或直到呼叫**SQLFreeHandle**來卸載語句為止。 使用 SQL_CLOSE、SQL_UNBIND 或 SQL_RESET_PARAMS 選項呼叫**SQLFreeStmt**時，不會重設語句屬性。  
  
 如果資料來源不支援*valueptr 是*中指定的值，某些語句屬性支援替代的值。 在這種情況下，驅動程式會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （選項值已變更）。 例如，如果*屬性*是 SQL_ATTR_CONCURRENCY 而且*valueptr 是*是 SQL_CONCUR_ROWVER 的，而且如果資料來源不支援這種情況，驅動程式會替代 SQL_CONCUR_VALUES 並傳回 SQL_SUCCESS_WITH_INFO。 為了判斷替代值，應用程式會呼叫**SQLGetStmtAttr**。  
  
 使用*valueptr 是*設定的資訊格式取決於指定的*屬性*。 **SQLSetStmtAttr**可接受兩種不同格式之一的屬性資訊：字元字串或整數值。 屬性的描述中會注明每個的格式。 此格式適用于針對**SQLGetStmtAttr**中的每個屬性所傳回的資訊。 **SQLSetStmtAttr**的*valueptr 是*引數所指向的字元字串長度為*StringLength*。  
  
> [!NOTE]
>  藉由呼叫**SQLSetConnectAttr**在連接層級設定語句屬性的功能，已*在 ODBC 3.x*中被取代。 ODBC *3.x*應用程式絕對不應在連接層級設定語句屬性。 ODBC *3.x*語句屬性無法在連接層級設定，但 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 屬性（兩者都是連接屬性和語句屬性），而且可以在連接層級或語句層級設定。  
> 
> [!NOTE]
>  如果 ODBC *3.x 驅動程式*應該與在連接層級設定 odbc *2.x 語句選項的 odbc* *2.x 應用程式*搭配使用，則只需要支援這種功能。 如需詳細資訊，請參閱附錄 G：驅動程式指導方針中的[SQLSetConnectOption 對應](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)中的「在連接層級設定語句選項」，以提供回溯相容性。  
  
## <a name="statement-attributes-that-set-descriptor-fields"></a>設定描述項欄位的語句屬性  
 許多語句屬性會對應至描述項的標頭欄位。 設定這些屬性實際上會產生描述項欄位的設定。 藉由呼叫**SQLSetStmtAttr**而非**SQLSetDescField**來設定欄位，其優點是不需要為函式呼叫取得描述項控制碼。  
  
> [!CAUTION]  
>  呼叫一個語句的**SQLSetStmtAttr**可能會影響其他語句。 當明確配置與語句相關聯的 APD 或 ARD，而且也與其他語句相關聯時，就會發生這種情況。 由於**SQLSetStmtAttr**會修改 APD 或 ARD，因此修改會套用到與此描述項相關聯的所有語句。 如果這不是必要的行為，應用程式應該將此描述項與其他語句中斷關聯（藉由呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 欄位設定為不同的描述項控制碼），然後再次呼叫**SQLSetStmtAttr** 。  
  
 當描述項欄位設定為要設定之對應語句屬性的結果時，只會針對目前與*StatementHandle*引數所識別的語句相關聯的適用描述元設定欄位，而屬性設定不會影響未來可能與該語句相關聯的任何描述元。 當**SQLSetDescField**的呼叫設定了同時為語句屬性的描述項欄位時，就會設定對應的語句屬性。 如果明確配置的描述元與語句解除關聯，則對應至標頭欄位的語句屬性會還原為隱含配置描述項中的欄位值。  
  
 配置語句時（請參閱[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)），系統會自動設定四個描述元控制碼，並與語句相關聯。 明確配置的描述項控制碼可以與語句相關聯，方法是呼叫**SQLAllocHandle**與*fHandleType*的 SQL_HANDLE_DESC 來配置描述項控制碼，然後呼叫**SQLSetStmtAttr** ，使描述項控制碼與語句產生關聯。  
  
 下表中的語句屬性會對應到描述項標頭欄位。  
  
|語句屬性|標頭欄位|降冪.|  
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
 下表顯示目前定義的屬性和其引進所在的 ODBC 版本：預期驅動程式會定義更多屬性，以利用不同的資料來源。 屬性的範圍是由 ODBC 所保留。驅動程式開發人員必須從開啟的群組中，保留自己的驅動程式特有的值。 如需詳細資訊，請參閱[驅動程式特有的資料類型、描述項類型、資訊類型、診斷類型和屬性](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md)。  
  
|屬性|*Valueptr 是*內容|  
|---------------|-------------------------|  
|SQL_ATTR_APP_PARAM_DESC （ODBC 3.0）|在語句控制碼上，後續呼叫**SQLExecute**和**SQLExecDirect**的 APD 控制碼。 這個屬性的初始值是一開始配置語句時，隱含配置的描述元。 如果這個屬性的值設定為 SQL_Null_DESC 或原先配置給描述項的控制碼，則先前與語句控制碼相關聯的明確配置 APD 控制碼會與其中斷關聯，而且語句控制碼會還原為隱含配置的 APD 控制碼。<br /><br /> 這個屬性不能設定為隱含配置給另一個語句的描述元控制碼，或是在相同的語句上隱含設定的另一個描述項控制碼。隱含配置的描述元控制碼無法與一個以上的語句或描述項控制碼建立關聯。|  
|SQL_ATTR_APP_ROW_DESC （ODBC 3.0）|語句控制碼上後續提取的 ARD 控制碼。 這個屬性的初始值是一開始配置語句時，隱含配置的描述元。 如果這個屬性的值設定為 SQL_Null_DESC 或原先配置給描述項的控制碼，則先前與語句控制碼相關聯的明確配置 ARD 控制碼會與其中斷關聯，而且語句控制碼會還原為隱含配置的 ARD 控制碼。<br /><br /> 這個屬性不能設定為隱含配置給另一個語句的描述元控制碼，或是在相同的語句上隱含設定的另一個描述項控制碼。隱含配置的描述元控制碼無法與一個以上的語句或描述項控制碼建立關聯。|  
|SQL_ATTR_ASYNC_ENABLE （ODBC 1.0）|SQLULEN 值，指定使用指定的語句所呼叫的函數是否以非同步方式執行：<br /><br /> SQL_ASYNC_ENABLE_OFF = Disable 語句層級非同步執行支援（預設值）。<br /><br /> SQL_ASYNC_ENABLE_ON = 啟用語句層級非同步執行支援。<br /><br /> 如需詳細資訊，請參閱[非同步執行（輪詢方法）](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。<br /><br /> 對於語句層級非同步執行支援的驅動程式，語句屬性 SQL_ATTR_ASYNC_ENABLE 為唯讀。 其值與配置語句控制碼時相同名稱的連接層級屬性值相同。<br /><br /> 呼叫**SQLSetStmtAttr**以設定 SQL_ASYNC_MODE *InfoType*傳回時的 SQL_ATTR_ASYNC_ENABLE SQL_AM_CONNECTION 傳回 SQLSTATE HYC00 （未執行的選擇性功能）。 如需詳細資訊，請參閱[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。|  
|SQL_ATTR_ASYNC_STMT_EVENT （ODBC 3.8）|屬於事件控制碼的 SQLPOINTER 值。<br /><br /> 藉由呼叫**SQLSetStmtAttr**來設定**SQL_ATTR_ASYNC_STMT_EVENT**屬性並指定事件控制碼，即可啟用非同步函式完成的通知。|  
|SQL_ATTR_ASYNC_STMT_PCALLBACK （ODBC 3.8）|非同步回呼函數的 SQLPOINTER。<br /><br /> 只有驅動程式管理員可以使用這個屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_ASYNC_STMT_PCONTEXT （ODBC 3.8）|SQLPOINTER 至內容結構<br /><br /> 只有驅動程式管理員可以使用這個屬性呼叫驅動程式的**SQLSetStmtAttr**函數。|  
|SQL_ATTR_CONCURRENCY （ODBC 2.0）|指定資料指標並行的 SQLULEN 值：<br /><br /> SQL_CONCUR_READ_ONLY = 資料指標是唯讀的。 不允許任何更新。<br /><br /> SQL_CONCUR_LOCK = 資料指標使用的最低層級鎖定足以確保資料列可以更新。<br /><br /> SQL_CONCUR_ROWVER = 資料指標使用開放式並行存取控制，比較資料列版本，例如 SQLBase ROWID 或 Sybase 時間戳記。<br /><br /> SQL_CONCUR_VALUES = 資料指標使用開放式並行存取控制，比較值。<br /><br /> SQL_ATTR_CONCURRENCY 的預設值為 SQL_CONCUR_READ_ONLY。<br /><br /> 無法為開啟的資料指標指定此屬性。 如需詳細資訊，請參閱[並行類型](../../../odbc/reference/develop-app/concurrency-types.md)。<br /><br /> 如果 SQL_ATTR_CURSOR_TYPE*屬性*變更為不支援目前 SQL_ATTR_CONCURRENCY 值的類型，則會在執行時間變更 SQL_ATTR_CONCURRENCY 的值，並在呼叫**SQLExecDirect**或**SQLPrepare**時發出警告。<br /><br /> 如果驅動程式支援**SELECT FOR UPDATE**語句，而這類語句是在 SQL_ATTR_CONCURRENCY 的值設定為 SQL_CONCUR_READ_ONLY 時執行，則會傳回錯誤。 如果 SQL_ATTR_CONCURRENCY 的值變更為某個值，而驅動程式支援 SQL_ATTR_CURSOR_TYPE 的某個值，但不是針對目前的 SQL_ATTR_CURSOR_TYPE 值，則 SQL_ATTR_CURSOR_TYPE 的值將會在執行時變更，而且在呼叫**SQLExecDirect**或**SQLPrepare**時，就會發出 SQLSTATE 01S02 （已變更的選項值）。<br /><br /> 如果資料來源不支援指定的平行存取，驅動程式會替代不同的並行，並傳回 SQLSTATE 01S02 （已變更的選項值）。 針對 SQL_CONCUR_VALUES，驅動程式會替代 SQL_CONCUR_ROWVER，反之亦然。 針對 SQL_CONCUR_LOCK，驅動程式會依序替代，SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES。 在執行時間之前，不會檢查替代值的有效性。<br /><br /> 如需 SQL_ATTR_CONCURRENCY 與其他資料指標屬性之間關聯性的詳細資訊，請參閱資料[指標特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_SCROLLABLE （ODBC 3.0）|SQLULEN 值，指定應用程式所需的支援層級。 設定此屬性會影響後續對**SQLExecDirect**和**SQLExecute**的呼叫。<br /><br /> SQL_NONSCROLLABLE = 語句控制碼上不需要可滾動的資料指標。 如果應用程式在此控制碼上呼叫**SQLFetchScroll** ，則唯一有效的*FetchOrientation*值為 SQL_FETCH_NEXT。 這是預設值。<br /><br /> SQL_SCROLLABLE = 語句控制碼上必須有可滾動的資料指標。 呼叫**SQLFetchScroll**時，應用程式可以指定任何有效的*FetchOrientation*值，以在連續模式以外的模式中達到資料指標定位。<br /><br /> 如需可滾動資料指標的詳細資訊，請參閱可滾動的資料[指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。 如需 SQL_ATTR_CURSOR_SCROLLABLE 與其他資料指標屬性之間關聯性的詳細資訊，請參閱資料[指標特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)|  
|SQL_ATTR_CURSOR_SENSITIVITY （ODBC 3.0）|SQLULEN 值，指定語句控制碼上的資料指標是否可以顯示另一個資料指標對結果集所做的變更。 設定此屬性會影響後續對**SQLExecDirect**和**SQLExecute**的呼叫。 應用程式可以讀回這個屬性的值，以取得其初始狀態或應用程式最近設定的狀態。<br /><br /> SQL_UNSPECIFIED = 未指定資料指標類型是什麼，以及語句控制碼上的資料指標是否會使另一個資料指標對結果集所做的變更變成可見。 語句控制碼上的資料指標可能會使無、部分或所有這類變更變成可見。 這是預設值。<br /><br /> SQL_INSENSITIVE = 語句控制碼上的所有資料指標都會顯示結果集，而不會反映任何其他資料指標對它所做的任何變更。 不區分資料指標是唯讀的。 這會對應到靜態資料指標，其具有唯讀的平行存取。<br /><br /> SQL_SENSITIVE = 語句控制碼上的所有資料指標都會使另一個資料指標對結果集所做的所有變更變成可見。<br /><br /> 如需 SQL_ATTR_CURSOR_SENSITIVITY 與其他資料指標屬性之間關聯性的詳細資訊，請參閱資料[指標特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_CURSOR_TYPE （ODBC 2.0）|指定資料指標類型的 SQLULEN 值：<br /><br /> SQL_CURSOR_FORWARD_ONLY = 資料指標只向前滾動。<br /><br /> SQL_CURSOR_STATIC = 結果集中的資料是靜態的。<br /><br /> SQL_CURSOR_KEYSET_DRIVEN = 驅動程式會儲存並使用索引鍵，以取得 SQL_ATTR_KEYSET_SIZE 語句屬性中所指定的資料列數目。<br /><br /> SQL_CURSOR_DYNAMIC = 驅動程式只會儲存並使用資料列集中資料列的索引鍵。<br /><br /> 預設值為 SQL_CURSOR_FORWARD_ONLY。 準備好 SQL 語句之後，就無法指定這個屬性。<br /><br /> 如果資料來源不支援指定的資料指標類型，則驅動程式會替代不同的資料指標類型，並傳回 SQLSTATE 01S02 （已變更的選項值）。 若是混合或動態資料指標，驅動程式會以索引鍵集驅動或靜態資料指標的順序替代。 針對索引鍵集驅動資料指標，驅動程式會替代靜態資料指標。<br /><br /> 如需可滾動資料指標類型的詳細資訊，請參閱可[滾動資料指標類型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)。 如需 SQL_ATTR_CURSOR_TYPE 與其他資料指標屬性之間關聯性的詳細資訊，請參閱資料[指標特性和資料指標類型](../../../odbc/reference/develop-app/cursor-characteristics-and-cursor-type.md)。|  
|SQL_ATTR_ENABLE_AUTO_IPD （ODBC 3.0）|SQLULEN 值，指定是否執行自動填入 IPD：<br /><br /> SQL_TRUE = 在呼叫**SQLPrepare**之後開啟 IPD 的自動填入。 SQL_FALSE = 在呼叫**SQLPrepare**之後關閉 IPD 的自動填入。 （如果支援，應用程式仍然可以藉由呼叫**SQLDescribeParam**來取得 IPD 欄位資訊）。SQL_FALSE SQL_ATTR_ENABLE_AUTO_IPD 語句屬性的預設值。 如需詳細資訊，請參閱[IPD 的自動填入](../../../odbc/reference/develop-app/automatic-population-of-the-ipd.md)。|  
|SQL_ATTR_FETCH_BOOKMARK_PTR （ODBC 3.0）|指向二進位\*書簽值的 SQLLEN。 當使用*fFetchOrientation*等於 SQL_FETCH_BOOKMARK 來呼叫**SQLFetchScroll**時，驅動程式會從這個欄位拾取書簽值。 此欄位的預設值為 null 指標。 如需詳細資訊，請參閱[依書簽滾動](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)。<br /><br /> 這個欄位所指向的值不會在書簽中用於刪除、以書簽更新，或在**SQLBulkOperations**中以書簽作業提取，這會使用在資料列集緩衝區中快取的書簽。|  
|SQL_ATTR_IMP_PARAM_DESC （ODBC 3.0）|IPD 的控制碼。 這個屬性的值是一開始配置語句時所配置的描述元。 應用程式無法設定此屬性。<br /><br /> 這個屬性可以透過呼叫**SQLGetStmtAttr**來抓取，而不是由呼叫**SQLSetStmtAttr**所設定。|  
|SQL_ATTR_IMP_ROW_DESC （ODBC 3.0）|IRD 的控制碼。 這個屬性的值是一開始配置語句時所配置的描述元。 應用程式無法設定此屬性。<br /><br /> 這個屬性可以透過呼叫**SQLGetStmtAttr**來抓取，而不是由呼叫**SQLSetStmtAttr**所設定。|  
|SQL_ATTR_KEYSET_SIZE （ODBC 2.0）|SQLULEN，指定索引鍵集驅動資料指標的索引鍵集中的資料列數目。 如果索引鍵集大小為0（預設值），則資料指標會是完整的索引鍵集驅動。 如果索引鍵集大小大於0，則資料指標會混合（索引鍵集內的索引鍵集驅動，並在索引鍵集外部動態）。 預設的索引鍵集大小為0。 如需索引鍵集驅動資料指標的詳細資訊，請參閱索引[鍵集驅動資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)。<br /><br /> 如果指定的大小超過最大的索引鍵集大小，則驅動程式會取代該大小，並傳回 SQLSTATE 01S02 （已變更的選項值）。<br /><br /> 如果索引鍵集大小大於0且小於資料列集大小， **SQLFetch**或**SQLFetchScroll**會傳回錯誤。|  
|SQL_ATTR_MAX_LENGTH （ODBC 1.0）|SQLULEN 值，指定驅動程式從字元或二進位資料行傳回的最大資料量。 如果*valueptr 是*小於可用資料的長度， **SQLFetch**或**SQLGetData**會截斷資料並傳回 SQL_SUCCESS。 如果*valueptr 是*為0（預設值），則驅動程式會嘗試傳回所有可用的資料。<br /><br /> 如果指定的長度小於資料來源可傳回的最小資料量，或大於資料來源可以傳回的最大資料量，則驅動程式會替代該值並傳回 SQLSTATE 01S02 （已變更的選項值）。<br /><br /> 可以在開啟的資料指標上設定這個屬性的值;不過，此設定可能不會立即生效，在此情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更），並將屬性重設為其原始值。<br /><br /> 這個屬性的目的是要減少網路流量，而且只有在多層式驅動程式中的資料來源（相對於驅動程式）可以執行它時才支援。 應用程式不應該使用這項機制來截斷資料;若要截斷收到的資料，應用程式應該在**SQLBindCol**或**SQLGetData**的*BufferLength*引數中指定最大緩衝區長度。|  
|SQL_ATTR_MAX_ROWS （ODBC 1.0）|對應至**SELECT**語句之應用程式的最大資料列數目的 SQLULEN 值。 如果\* *valueptr 是*等於0（預設值），則驅動程式會傳回所有資料列。<br /><br /> 這個屬性的目的是要減少網路流量。 在概念上，它會在建立結果集時套用，並將結果集限制為第一個*valueptr 是*的資料列。 如果結果集中的資料列數目大於*valueptr 是*，則會截斷結果集。<br /><br /> SQL_ATTR_MAX_ROWS 適用于*語句*上的所有結果集，包括目錄函式所傳回的結果集。 SQL_ATTR_MAX_ROWS 建立資料指標資料列計數的最大值。<br /><br /> 驅動程式不應該模擬**SQLFetch**或**SQLFetchScroll**的 SQL_ATTR_MAX_ROWS 行為（如果結果集大小限制無法在資料來源上執行的話），如果它無法保證 SQL_ATTR_MAX_ROWS 會正確執行。<br /><br /> 無論 SQL_ATTR_MAX_ROWS 是否適用于 SELECT 語句以外的語句（例如目錄函式），都是由驅動程式定義的。<br /><br /> 可以在開啟的資料指標上設定這個屬性的值;不過，此設定可能不會立即生效，在此情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更），並將屬性重設為其原始值。|  
|SQL_ATTR_METADATA_ID （ODBC 3.0）|決定如何處理目錄函數之字串引數的 SQLULEN 值。<br /><br /> 如果 SQL_TRUE，則會將目錄函數的字串引數視為識別碼。 這種情況並不重要。 若為 nondelimited 字串，驅動程式會移除任何尾端空格，而字串會折迭為大寫。 對於分隔的字串，驅動程式會移除任何開頭或尾端空格，並以字面形式接受兩者之間的任何字元。 如果其中一個引數設定為 null 指標，此函式會傳回 SQL_ERROR 並 SQLSTATE HY009 （null 指標的用法無效）。<br /><br /> 如果 SQL_FALSE，則不會將目錄函式的字串引數視為識別碼。 這種情況很重要。 視引數而定，它們可以包含字串搜尋模式。<br /><br /> 預設值為 SQL_FALSE。<br /><br /> **SQLTables**的*TableType*引數（接受值清單）不會受到此屬性的影響。<br /><br /> 您也可以在連接層級上設定 SQL_ATTR_METADATA_ID。 （它和 SQL_ATTR_ASYNC_ENABLE 是唯一也是連接屬性的語句屬性）。<br /><br /> 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。|  
|SQL_ATTR_NOSCAN （ODBC 1.0）|SQLULEN 值，指出驅動程式是否應該掃描 SQL 字串是否有逸出序列：<br /><br /> SQL_NOSCAN_OFF = 驅動程式會掃描 SQL 字串中的逸出序列（預設值）。<br /><br /> SQL_NOSCAN_ON = 驅動程式不會掃描 SQL 字串是否有逸出序列。 相反地，驅動程式會將語句直接傳送至資料來源。<br /><br /> 如需詳細資訊，請參閱[ODBC 中的 Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR （ODBC 3.0）|SQLULEN * 值，指向新增至指標的位移，以變更動態參數的系結。 如果此欄位為非 null，則驅動程式會取值指標、將解除引用的值新增至描述項記錄中的每個延後欄位（SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR），並在系結時使用新的指標值。 根據預設，它會設為 null。<br /><br /> 系結位移一律會直接新增至 [SQL_DESC_DATA_PTR]、[SQL_DESC_INDICATOR_PTR] 和 [SQL_DESC_OCTET_LENGTH_PTR] 欄位。 如果位移變更為不同的值，則新的值仍會直接加入至 [描述項] 欄位中的值。 新的位移不會加入至域值加上任何先前的位移。<br /><br /> 如需詳細資訊，請參閱參數系結[位移](../../../odbc/reference/develop-app/parameter-binding-offsets.md)。<br /><br /> 設定這個語句屬性會設定 APD 標頭中的 SQL_DESC_BIND_OFFSET_PTR 欄位。|  
|SQL_ATTR_PARAM_BIND_TYPE （ODBC 3.0）|SQLULEN 值，表示要用於動態參數的系結方向。<br /><br /> 此欄位設定為 SQL_PARAM_BIND_BY_COLUMN （預設值），以選取資料行取向的系結。<br /><br /> 若要選取資料列取向的系結，此欄位會設定為結構的長度，或將系結至一組動態參數的緩衝區實例。 這個長度必須包含所有系結參數的空間，以及結構或緩衝區的任何填補，以確保當系結參數的位址以指定的長度遞增時，結果會指向下一組參數中相同參數的開頭。 在 ANSI C 中使用*sizeof*運算子時，會保證此行為。<br /><br /> 如需詳細資訊，請參閱系結[參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。<br /><br /> 設定這個語句屬性會設定 APD 標頭中的 SQL_DESC_ BIND_TYPE 欄位。|  
|SQL_ATTR_PARAM_OPERATION_PTR （ODBC 3.0）|SQLUSMALLINT \*值，指向用來在 SQL 語句執行期間忽略參數的 SQLUSMALLINT 值陣列。 每個值都會設定為 SQL_PARAM_PROCEED （用於要執行的參數）或 SQL_PARAM_IGNORE （以忽略參數）。<br /><br /> 在處理期間可以忽略一組參數，方法是在 APD 中的 SQL_DESC_ARRAY_STATUS_PTR 所指向的陣列中設定狀態值，以 SQL_PARAM_IGNORE。 如果其狀態值設定為 SQL_PARAM_PROCEED，或如果未設定陣列中的任何元素，則會處理一組參數。<br /><br /> 這個語句屬性可以設定為 null 指標，在此情況下，驅動程式不會傳回參數狀態值。 您可以隨時設定這個屬性，但必須等到下次呼叫**SQLExecDirect**或**SQLExecute**時，才會使用新的值。<br /><br /> 沒有系結參數時，會忽略這個屬性。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定這個語句屬性會設定 APD 標頭中的 SQL_DESC_ARRAY_STATUS_PTR 欄位。|  
|SQL_ATTR_PARAM_STATUS_PTR （ODBC 3.0）|SQLUSMALLINT \*值，指向 SQLUSMALLINT 值的陣列，其中包含在呼叫**SQLExecute**或**SQLExecDirect**之後的每個參數值資料列的狀態資訊。 只有當 PARAMSET_SIZE 大於1時，才需要此欄位。<br /><br /> 狀態值可以包含下列值：<br /><br /> SQL_PARAM_SUCCESS：已成功執行此參數集的 SQL 語句。<br /><br /> SQL_PARAM_SUCCESS_WITH_INFO：已成功執行此參數集的 SQL 語句;不過，診斷資料結構中有提供警告資訊。<br /><br /> SQL_PARAM_ERROR：處理這組參數時發生錯誤。 診斷資料結構中有其他錯誤資訊。<br /><br /> SQL_PARAM_UNUSED：這個參數集未使用，可能是因為某個先前的參數集造成了中止進一步處理的錯誤，或因為 SQL_ATTR_PARAM_OPERATION_PTR 指定之陣列中的參數集 SQL_PARAM_IGNORE 已設定。<br /><br /> SQL_PARAM_DIAG_UNAVAILABLE：驅動程式會將參數陣列視為整合式單位，因此不會產生此層級的錯誤資訊。<br /><br /> 這個語句屬性可以設定為 null 指標，在此情況下，驅動程式不會傳回參數狀態值。 您可以隨時設定這個屬性，但必須等到下次呼叫**SQLExecute**或**SQLExecDirect**時，才會使用新的值。 請注意，設定此屬性可能會影響驅動程式所實作為輸出參數的行為。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定此語句屬性會設定 IPD 標頭中的 SQL_DESC_ARRAY_STATUS_PTR 欄位。|  
|SQL_ATTR_PARAMS_PROCESSED_PTR （ODBC 3.0）|SQLULEN \*記錄欄位，指向要在其中傳回已處理之參數集數目的緩衝區，包括錯誤集合。 如果這是 null 指標，則不會傳回任何數位。<br /><br /> 設定此語句屬性會設定 IPD 標頭中的 SQL_DESC_ROWS_PROCESSED_PTR 欄位。<br /><br /> 如果**SQLExecDirect**或**SQLExecute**的呼叫在這個屬性所指向的緩衝區中，不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則會定義緩衝區的內容。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。|  
|SQL_ATTR_PARAMSET_SIZE （ODBC 3.0）|SQLULEN 值，指定每個參數的值數目。 如果 SQL_ATTR_PARAMSET_SIZE 大於1，SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR APD 點到陣列。 每個陣列的基數等於此欄位的值。<br /><br /> 沒有系結參數時，會忽略這個屬性。<br /><br /> 如需詳細資訊，請參閱[使用參數陣列](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)。<br /><br /> 設定這個語句屬性會設定 APD 標頭中的 SQL_DESC_ARRAY_SIZE 欄位。|  
|SQL_ATTR_QUERY_TIMEOUT （ODBC 1.0）|SQLULEN 值，對應至等候 SQL 語句執行的秒數，然後再返回應用程式。 如果*valueptr 是*等於0（預設值），則不會有任何 timeout。<br /><br /> 如果指定的超時時間超過資料來源中的最大等待時間，或小於最小的 timeout，則**SQLSetStmtAttr**會替代該值並傳回 SQLSTATE 01S02 （選項值已變更）。<br /><br /> 請注意，如果**SELECT**語句超時，應用程式就不需要呼叫**SQLCloseCursor**來重複使用語句。<br /><br /> 在此語句屬性中設定的查詢超時，在同步與非同步模式中都是有效的。|  
|SQL_ATTR_RETRIEVE_DATA （ODBC 2.0）|SQLULEN 值：<br /><br /> SQL_RD_ON = **SQLFetchScroll** *，而在 ODBC 3.X*中， **SQLFetch**會在將資料指標放到指定的位置之後，抓取它。 這是預設值。<br /><br /> SQL_RD_OFF = **SQLFetchScroll** *，而在 ODBC 3.X*中， **SQLFetch**不會在定位資料指標之後，抓取資料。<br /><br /> 藉由將 SQL_RETRIEVE_DATA 設定為 SQL_RD_OFF，應用程式可以驗證資料列是否存在，或抓取資料列的書簽，而不會造成抓取資料列的額外負荷。 如需詳細資訊，請參閱[滾動和提取資料列](../../../odbc/reference/develop-app/scrolling-and-fetching-rows-odbc.md)。<br /><br /> 可以在開啟的資料指標上設定這個屬性的值;不過，此設定可能不會立即生效，在此情況下，驅動程式會傳回 SQLSTATE 01S02 （選項值已變更），並將屬性重設為其原始值。|  
|SQL_ATTR_ROW_ARRAY_SIZE （ODBC 3.0）|SQLULEN 值，指定每次呼叫**SQLFetch**或**SQLFetchScroll**時所傳回的資料列數目。 它也是書簽陣列中用於**SQLBulkOperations**中大量書簽作業的資料列數目。 預設值為 1。<br /><br /> 如果指定的資料列集大小超過資料來源所支援的最大資料列集大小，則驅動程式會替代該值，並傳回 SQLSTATE 01S02 （已變更的選項值）。<br /><br /> 如需詳細資訊，請參閱資料列[集大小](../../../odbc/reference/develop-app/rowset-size.md)。<br /><br /> 設定這個語句屬性會設定 ARD 標頭中的 SQL_DESC_ARRAY_SIZE 欄位。|  
|SQL_ATTR_ROW_BIND_OFFSET_PTR （ODBC 3.0）|SQLULEN * 值，指向新增至指標的位移，以變更資料行資料的系結。 如果此欄位為非 null，則驅動程式會取值指標、將解除引用的值新增至描述項記錄中的每個延後欄位（SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR），並在系結時使用新的指標值。 根據預設，它會設為 null。<br /><br /> 設定這個語句屬性會設定 ARD 標頭中的 SQL_DESC_BIND_OFFSET_PTR 欄位。|  
|SQL_ATTR_ROW_BIND_TYPE （ODBC 1.0）|SQLULEN 值，設定在相關聯的語句上呼叫**SQLFetch**或**SQLFetchScroll**時所使用的系結方向。 藉由將值設定為 SQL_BIND_BY_COLUMN 來選取資料行取向的系結。 藉由將值設定為結構的長度，或將結果資料行系結至的緩衝區實例，來選取資料列取向的系結。<br /><br /> 如果指定長度，它必須包含所有系結資料行的空間，以及結構或緩衝區的任何填補，以確保當系結資料行的位址以指定的長度遞增時，結果會指向下一個資料列中相同資料行的開頭。 在 ANSI C 中搭配結構或等位使用**sizeof**運算子時，會保證此行為。<br /><br /> 資料行取向系結是**SQLFetch**和**SQLFetchScroll**的預設系結方向。<br /><br /> 如需詳細資訊，請參閱系結[資料行以搭配使用區塊資料指標](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)。<br /><br /> 設定這個語句屬性會設定 ARD 標頭中的 SQL_DESC_BIND_TYPE 欄位。|  
|SQL_ATTR_ROW_NUMBER （ODBC 2.0）|SQLULEN 值，這是整個結果集中目前資料列的數目。 如果無法判斷目前資料列的數目，或目前沒有資料列，則驅動程式會傳回0。<br /><br /> 這個屬性可以透過呼叫**SQLGetStmtAttr**來抓取，而不是由呼叫**SQLSetStmtAttr**所設定。|  
|SQL_ATTR_ROW_OPERATION_PTR （ODBC 3.0）|SQLUSMALLINT \*值，指向用來在大量作業期間使用**SQLSetPos**忽略資料列的 SQLUSMALLINT 值陣列。 每個值都會設定為 SQL_ROW_PROCEED （針對要包含在大量作業中的資料列）或 SQL_ROW_IGNORE （用於要從大量作業中排除的資料列）。 （呼叫**SQLBulkOperations**時，無法使用這個陣列忽略資料列）。<br /><br /> 這個語句屬性可以設定為 null 指標，在此情況下，驅動程式不會傳回資料列狀態值。 您可以隨時設定這個屬性，但在下一次呼叫**SQLSetPos**之前，不會使用新的值。<br /><br /> 如需詳細資訊，請參閱[使用 SQLSetPos 更新資料列集中](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)的資料列和[使用 SQLSetPos 刪除資料列集中的資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)。<br /><br /> 設定這個語句屬性會設定 ARD 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位。|  
|SQL_ATTR_ROW_STATUS_PTR （ODBC 3.0）|SQLUSMALLINT \*值，指向**SQLFetch**或**SQLFetchScroll**呼叫之後的 SQLUSMALLINT 值陣列，其中包含資料列狀態值。 陣列的元素數目與資料列集中的資料列數相同。<br /><br /> 這個語句屬性可以設定為 null 指標，在此情況下，驅動程式不會傳回資料列狀態值。 您可以隨時設定這個屬性，但在下一次呼叫**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**之前，不會使用新的值。<br /><br /> 如需詳細資訊，請參閱[提取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 設定這個語句屬性會設定 IRD 標頭中的 SQL_DESC_ARRAY_STATUS_PTR 欄位。<br /><br /> 這個屬性是*由 ODBC 2.x*驅動程式對應至**SQLExtendedFetch**呼叫中的*rgbRowStatus*陣列。|  
|SQL_ATTR_ROWS_FETCHED_PTR （ODBC 3.0）|SQLULEN \*值，指向要在其中傳回**SQLFetch**或**SQLFetchScroll**呼叫之後提取之資料列數目的緩衝區。使用*SQL_REFRESH 的作業引數*呼叫**SQLSetPos**所執行的大量作業所影響的資料列數目。或由**SQLBulkOperations**所執行之大量作業所影響的資料列數目。 此數目包含錯誤資料列。<br /><br /> 如需詳細資訊，請參閱[提取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)。<br /><br /> 設定這個語句屬性會設定 IRD 標頭中的 SQL_DESC_ROWS_PROCESSED_PTR 欄位。<br /><br /> 如果**SQLFetch**或**SQLFetchScroll**的呼叫在這個屬性所指向的緩衝區中，不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則會定義緩衝區的內容。|  
|SQL_ATTR_SIMULATE_CURSOR （ODBC 2.0）|SQLULEN 值，指定模擬定位 update 和 delete 語句的驅動程式是否保證這類語句只會影響一個單一資料列。<br /><br /> 為了模擬定位的 update 和 delete 語句，大部分的驅動程式會建立一個搜尋的**update**或**delete**語句，其中包含指定目前資料列中每個資料行值的**WHERE**子句。 除非這些資料行構成唯一索引鍵，否則這類語句可能會影響一個以上的資料列。<br /><br /> 為保證這類語句只會影響一個資料列，驅動程式會判斷唯一索引鍵中的資料行，並將這些資料行加入至結果集。 如果應用程式保證結果集中的資料行構成唯一索引鍵，則不需要驅動程式來執行這項操作。 這可能會減少執行時間。<br /><br /> SQL_SC_NON_UNIQUE = 驅動程式不保證模擬的定點更新或刪除語句只會影響一個資料列;應用程式必須負責這麼做。 如果語句影響一個以上的資料列， **SQLExecute**、 **SQLExecDirect**或**SQLSetPos**會傳回 SQLSTATE 01001 （資料指標作業衝突）。<br /><br /> SQL_SC_TRY_UNIQUE = 驅動程式會嘗試保證模擬的定位 update 或 delete 語句只會影響一個資料列。 驅動程式一律會執行這類語句，即使它們可能會影響一個以上的資料列，例如沒有唯一索引鍵時。 如果語句影響一個以上的資料列， **SQLExecute**、 **SQLExecDirect**或**SQLSetPos**會傳回 SQLSTATE 01001 （資料指標作業衝突）。<br /><br /> SQL_SC_UNIQUE = 驅動程式保證模擬的定位 update 或 delete 語句只會影響一個資料列。 如果驅動程式無法保證指定語句的這個， **SQLExecDirect**或**SQLPrepare**會傳回錯誤。<br /><br /> 如果資料來源為定位的 update 和 delete 語句提供原生 SQL 支援，而驅動程式未模擬資料指標，則在要求 SQL_SIMULATE_CURSOR SQL_SC_UNIQUE 時，會傳回 SQL_SUCCESS。 如果要求 SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE，則會傳回 SQL_SUCCESS_WITH_INFO。 如果資料來源提供 SQL_SC_TRY_UNIQUE 層級的支援，而驅動程式不存在，則會傳回 SQL_SC_TRY_UNIQUE 的 SQL_SUCCESS，並傳回 SQL_SC_NON_UNIQUE 的 SQL_SUCCESS_WITH_INFO。<br /><br /> 如果資料來源不支援指定的資料指標模擬類型，則驅動程式會替代不同的模擬類型，並傳回 SQLSTATE 01S02 （已變更的選項值）。 針對 SQL_SC_UNIQUE，驅動程式會依序替代，SQL_SC_TRY_UNIQUE 或 SQL_SC_NON_UNIQUE。 針對 SQL_SC_TRY_UNIQUE，驅動程式會替代 SQL_SC_NON_UNIQUE。<br /><br /> 預設值為 SQL_SC_UNIQUE。<br /><br /> 如需詳細資訊，請參閱[模擬定位的 Update 和 Delete 語句](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)。|  
|SQL_ATTR_USE_BOOKMARKS （ODBC 2.0）|SQLULEN 值，指定應用程式是否會搭配使用書簽與資料指標：<br /><br /> SQL_UB_OFF = 關閉（預設值）<br /><br /> SQL_UB_VARIABLE = 應用程式會使用書簽搭配游標，而驅動程式會提供可變長度的書簽（如果支援的話）。 *ODBC 3.x 中的 SQL_UB_FIXED*已被取代。 ODBC *3.x 應用程式*應該一律使用可變長度的書簽，即使使用的*是 odbc 2.x*驅動程式（僅支援4個位元組的固定長度書簽）。 這是因為固定長度的書簽只是可變長度書簽的特殊案例。 使用 ODBC 2.x 驅動程式時，*驅動程式管理員*會將 SQL_UB_VARIABLE 對應到 SQL_UB_FIXED。<br /><br /> 若要搭配使用書簽和游標，應用程式必須在開啟資料指標之前，使用 SQL_UB_VARIABLE 值來指定此屬性。<br /><br /> 如需詳細資訊，請參閱抓取[書簽](../../../odbc/reference/develop-app/retrieving-bookmarks.md)。|  
  
 [1] 只有當描述項是一個執行描述項，而不是應用程式描述項時，才能以非同步方式呼叫這些函數。  
  
 請參閱資料行取向的系結和資料[列](../../../odbc/reference/develop-app/column-wise-binding.md)取向[的](../../../odbc/reference/develop-app/row-wise-binding.md)系結。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回連接屬性的設定|[SQLGetConnectAttr 函數](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|傳回語句屬性的設定|[SQLGetStmtAttr 函式](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|設定連接屬性|[SQLSetConnectAttr 函數](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|設定描述項的單一欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
