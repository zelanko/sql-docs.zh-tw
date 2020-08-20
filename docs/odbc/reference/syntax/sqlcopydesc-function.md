---
description: SQLCopyDesc 函式
title: SQLCopyDesc 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ede6d52614c1c35cdc28f6d85e8b3be61235b4ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461190"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLCopyDesc** 會將描述項資訊從一個描述項控制碼複製到另一個。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>引數  
 *SourceDescHandle*  
 輸出來源描述項控制碼。  
  
 *TargetDescHandle*  
 輸出目標描述項控制碼。 *TargetDescHandle*引數可以是應用程式描述項或 IPD 的控制碼。 *TargetDescHandle* 不能設定為 IRD 的控制碼，或 **SQLCOPYDESC** 將傳回 SQLSTATE HY016 (無法修改執行資料列描述項) 。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCopyDesc**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DESC）和*TargetDescHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 如果在呼叫中傳遞了不正確 *SourceDescHandle* ，將會傳回 SQL_INVALID_HANDLE，但不會傳回任何 SQLSTATE。 下表列出 **SQLCopyDesc** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
 傳回錯誤時，會立即中止對 **SQLCopyDesc** 的呼叫，且不會定義 *TargetDescHandle* 描述項中的欄位內容。  
  
 由於 **SQLCopyDesc** 可能會藉由呼叫 **SQLGetDescField** 和 **SQLSetDescField**來執行，因此 **SQLCopyDesc** 可能會傳回 **SQLSTATEs** 或 **SQLGetDescField**所傳回的 SQLSetDescField。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY007|未準備相關聯的語句|*SourceDescHandle* 與 IRD 相關聯，且相關聯的語句控制碼未處於已備妥或已執行的狀態。|  
|HY010|函數順序錯誤| (DM) *SourceDescHandle* 或 *TargetDescHandle* 中的描述項控制碼，與非同步執行函式的 *StatementHandle* 相關聯 (未呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) *SourceDescHandle*或*TargetDescHandle*中的描述項控制碼，與呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**的*StatementHandle*相關聯，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式是針對與 *SourceDescHandle* 或 *TargetDescHandle*關聯的連接控制碼呼叫。 呼叫 **SQLCopyDesc** 函式時，仍在執行此非同步函式。<br /><br />  (DM) **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResults** ，是針對與 *SourceDescHandle* 或 *TargetDescHandle* 相關聯的其中一個語句控制碼呼叫，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY016|無法修改實資料列描述項|*TargetDescHandle* 與 IRD 相關聯。|  
|HY021|不一致的描述項資訊|一致性檢查期間檢查的描述項資訊不一致。 如需詳細資訊，請參閱 **SQLSetDescField**中的「一致性檢查」。|  
|HY092|不正確屬性/選項識別碼|呼叫**SQLCopyDesc**時，會提示呼叫**SQLSetDescField**，但* \* ValuePtr*對*TargetDescHandle*上的*FieldIdentifier*引數是不正確。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *SourceDescHandle* 或 *TargetDescHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 呼叫 **SQLCopyDesc** 會將來源描述項控制碼的欄位複製到目標描述項控制碼。 欄位只能複製到應用程式描述元或 IPD，但不能複製到 IRD。 您可以從應用程式或執行描述項複製欄位。  
  
 只有當語句控制碼處於已備妥或已執行的狀態時，才能從 IRD 複製欄位;否則，函式會傳回 SQLSTATE HY007 (相關聯的語句尚未準備) 。  
  
 無論是否已備妥語句，都可以從 IPD 複製欄位。 如果已備妥具有動態參數的 SQL 語句，並支援並啟用 IPD 的自動填入，則 IPD 會由驅動程式填入。 使用 IPD 作為*SourceDescHandle*來呼叫**SQLCopyDesc**時，會複製已填入的欄位。 如果未由驅動程式擴展 IPD，則會複製原本在 IPD 中的欄位內容。  
  
 描述項的所有欄位（除了 SQL_DESC_ALLOC_TYPE (指定是否自動或) 明確配置描述項控制碼），不論是否為目的地描述項定義了欄位，都會複製該描述項。 複製的欄位會覆寫現有的欄位。  
  
 如果 *SourceDescHandle* 和 *TargetDescHandle* 引數與相同的驅動程式相關聯，驅動程式會複製所有描述項欄位，即使驅動程式是在兩個不同的連接或環境上也一樣。 如果 *SourceDescHandle* 和 *TargetDescHandle* 引數與不同的驅動程式相關聯，驅動程式管理員會複製 odbc 定義的欄位，但不會複製驅動程式定義的欄位或未由 ODBC 定義的欄位，以用於描述項的類型。  
  
 如果發生錯誤，則會立即中止對 **SQLCopyDesc** 的呼叫。  
  
 複製 SQL_DESC_DATA_PTR 欄位時，會在目標描述項上執行一致性檢查。 如果一致性檢查失敗，則會傳回 SQLSTATE HY021 (不一致的描述項資訊) 並立即中止對 **SQLCopyDesc** 的呼叫。 如需一致性檢查的詳細資訊，請參閱 [SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的「一致性檢查」。  
  
 即使連接是在不同的環境下，也可以跨連接複製描述項控制碼。 如果驅動程式管理員偵測到來源和目的地描述項控制碼不屬於相同的連接，而且這兩個連接屬於不同的驅動程式，它就會使用**SQLGetDescField**和**SQLSetDescField**執行逐欄位的複製來執行**SQLCopyDesc** 。  
  
 當呼叫 **SQLCopyDesc** 時，如果某個驅動程式上的 *SourceDescHandle* 與另一個驅動程式上的 *TargetDescHandle* ，則會清除 *SourceDescHandle* 的錯誤佇列。 這是因為在此案例中的 **SQLCopyDesc** 是由呼叫 **SQLGetDescField** 和 **SQLSetDescField**所執行。  
  
> [!NOTE]  
>  應用程式可能會將明確配置的描述項控制碼與 *StatementHandle*建立關聯，而不是呼叫 **SQLCopyDesc** ，將欄位從某個描述項複製到另一個描述項。 明確配置的描述元可以與相同*ConnectionHandle*上的另一個*StatementHandle*建立關聯，方法是將 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 語句屬性設定為明確配置描述項的控制碼。 完成這項操作時，不需要呼叫 **SQLCopyDesc** ，將描述項域值從一個描述項複製到另一個描述項。 不過，描述項控制碼無法與另一個*ConnectionHandle*上的*StatementHandle*相關聯。若要在不同的*ConnectionHandles*上使用*StatementHandles*上相同的描述項欄位值，必須呼叫**SQLCopyDesc** 。  
  
 如需描述項標頭或記錄中之欄位的說明，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)函式。 如需描述項的詳細資訊，請參閱 [描述](../../../odbc/reference/develop-app/descriptors.md)項。  
  
## <a name="copying-rows-between-tables"></a>在資料表之間複製資料列  
 應用程式可以將資料從一個資料表複製到另一個資料表，而不需要在應用層級複製資料。 若要這樣做，應用程式會將相同的資料緩衝區和描述元資訊系結至提取資料的語句，以及將資料插入複本的語句。 您可以藉由共用應用程式描述項來完成這項作業， (將明確配置的描述元系結至另一個) 中的 ARD 和 APD，或使用 **SQLCopyDesc** 來複製這兩個語句的 ARD 與 APD 之間的系結。 如果語句位於不同的連接上，則必須使用 **SQLCopyDesc** 。 此外，您必須呼叫 **SQLCopyDesc** ，以複製兩個語句的 IRD 和 IPD 之間的系結。 當在相同連接上跨語句複製時，驅動程式針對 **SQLGetInfo** 呼叫所傳回的 SQL_ACTIVE_STATEMENTS 資訊類型必須大於1，這項作業才會成功。  (在跨連接複製時就不會發生這種情況。 )   
  
### <a name="code-example"></a>程式碼範例  
 在下列範例中，描述項作業會用來將 PartsSource 資料表的欄位複製到 PartsCopy 資料表中。 PartsSource 資料表的內容會提取到 *hstmt0*中的資料列集緩衝區。 在 *hstmt1* 上，這些值會用來做為 INSERT 語句的參數，以填入 PartsCopy 資料表的資料行。 若要這樣做， *HSTMT0* IRD 的欄位會複製到*hstmt1*IPD 的欄位，而*hstmt0* ARD 的欄位則會複製到 APD hstmt1 的欄位*中。* 使用 **SQLSetDescField** 將 IPD 的 SQL_DESC_PARAMETER_TYPE 屬性設定為，當您將具有輸出參數的語句中的 IRD 欄位複製到需要作為輸入參數的 IPD 欄位時，SQL_PARAM_INPUT。  
  
```cpp  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
