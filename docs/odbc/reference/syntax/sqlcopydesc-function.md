---
title: "SQLCopyDesc 函式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8e7383a16b40a966612784e864594588cc37199
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 函式
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLCopyDesc**描述元資訊複製到另一個描述元控制代碼。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>引數  
 *SourceDescHandle*  
 [輸入]來源描述項控制代碼。  
  
 *TargetDescHandle*  
 [輸入]目標描述項控制代碼。 *TargetDescHandle*引數可以是應用程式描述項或 IPD 的控制代碼。 *TargetDescHandle*不能設定為 IRD 的控制代碼或**SQLCopyDesc**會傳回 SQLSTATE HY016 （無法修改實作資料列描述項）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCopyDesc**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_DESC 和*處理*的*TargetDescHandle*。 如果無效*SourceDescHandle*傳遞會在呼叫時，傳回 SQL_INVALID_HANDLE，但會傳回任何的 SQLSTATE。 下表列出通常所傳回的 SQLSTATE 值**SQLCopyDesc** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
 傳回錯誤時，呼叫**SQLCopyDesc**立即中止，及其中的內容中的欄位*TargetDescHandle*是未定義的描述元。  
  
 因為**SQLCopyDesc**可能藉由呼叫實作**SQLGetDescField**和**SQLSetDescField**， **SQLCopyDesc**可能會傳回所傳回的 Sqlstate **SQLGetDescField**或**SQLSetDescField**。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY007|相關的陳述式未準備好|*SourceDescHandle*聯 IRD 和相關聯的陳述式控制代碼不是處於已備妥或已執行狀態。|  
|HY010|函數順序錯誤|(DM) 中的描述項處理*SourceDescHandle*或*TargetDescHandle*與*StatementHandle* ，以非同步方式執行的函式 (not這一個） 已呼叫，而且還在執行時呼叫此函式。<br /><br /> 在中 (DM) 描述項處理*SourceDescHandle*或*TargetDescHandle*與*StatementHandle*其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**已呼叫而傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*SourceDescHandle*或*TargetDescHandle*。 此非同步函式還在執行時**SQLCopyDesc**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**呼叫其中一個相關聯的陳述式控制代碼*SourceDescHandle*或*TargetDescHandle*並傳回 SQL_PARAM_DATA_AVAILABLE。 此函式呼叫之前的所有資料流處理的參數擷取資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY016|無法修改實作資料列描述項|*TargetDescHandle* IRD 與相關聯。|  
|HY021|不一致的描述項資訊|檢查一致性檢查期間的描述項資訊不一致。 如需詳細資訊，請參閱 < 一致性檢查 」，在**SQLSetDescField**。|  
|HY092|屬性/選項識別碼無效|呼叫**SQLCopyDesc**提示呼叫**SQLSetDescField**，但 *\*ValuePtr*對無效*FieldIdentifier*引數上的*TargetDescHandle*。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*SourceDescHandle*或*TargetDescHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 呼叫**SQLCopyDesc**複製的來源描述項欄位控制代碼目標描述項控制代碼。 只有應用程式描述項或 IPD，但不是屬於 IRD 欄位複製。 欄位可以從應用程式或實作描述元複製。  
  
 只有當處於狀態為已備妥或已執行的陳述式控制代碼，可以從 IRD 複製欄位否則，此函數會傳回 SQLSTATE HY007 （相關聯的陳述式未準備好）。  
  
 可以從 IPD 複製欄位，不論是否已備妥的陳述式。 如果已備妥的 SQL 陳述式，由動態參數，而且支援 IPD 的自動擴展且已啟用，則 IPD 填入驅動程式。 當**SQLCopyDesc**稱為為 IPD *SourceDescHandle*，複製擴展的欄位。 如果驅動程式不會填入 IPD，原本在 IPD 欄位的內容會複製。  
  
 所有欄位的描述元，除了 SQL_DESC_ALLOC_TYPE （可指定是否描述項控制代碼已自動或明確地配置），會都複製，不論欄位針對目的地的描述元定義。 複製的欄位覆寫現有的欄位。  
  
 如果驅動程式會複製所有的描述項欄位*SourceDescHandle*和*TargetDescHandle*引數是相同的驅動程式相關聯，即使是在兩個不同的連接上的驅動程式或環境。 如果*SourceDescHandle*和*TargetDescHandle*引數都是不同的驅動程式相關聯、 驅動程式管理員會複製 ODBC 定義的欄位，但不會複製驅動程式定義的欄位或欄位未定義的 ODBC 類型的描述元。  
  
 若要呼叫**SQLCopyDesc**發生錯誤時立即中止。  
  
 複製 SQL_DESC_DATA_PTR 欄位時，會執行一致性檢查目標描述項。 如果一致性檢查失敗，SQLSTATE HY021 就會傳回 （不一致的描述元資訊），並呼叫， **SQLCopyDesc**立即中止。 如需有關一致性檢查的詳細資訊，請參閱 < 一致性檢查 」，在[SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 如果即使連線是在不同環境下，可以透過連線複製描述項控制代碼。 如果驅動程式管理員偵測到來源和目的地描述項控制代碼不屬於相同的連接，而且兩個連線屬於不同的驅動程式時，它會實作**SQLCopyDesc**所執行的欄位欄位使用複製**SQLGetDescField**和**SQLSetDescField**。  
  
 當**SQLCopyDesc**呼叫*SourceDescHandle*上一個驅動程式和*TargetDescHandle*上另一個驅動程式，錯誤佇列的*SourceDescHandle*已清除。 這是因為**SQLCopyDesc**在此情況下藉由呼叫**SQLGetDescField**和**SQLSetDescField**。  
  
> [!NOTE]  
>  應用程式可能可以建立具有明確配置描述項控制代碼關聯*StatementHandle*，而不是呼叫**SQLCopyDesc**至欄位複製到另一個描述元。 明確配置描述元可以是與另一個相關聯*StatementHandle*在同一個*ConnectionHandle*藉由設定 SQL_ATTR_APP_ROW_DESC 或 SQL_ATTR_APP_PARAM_DESC 陳述式此屬性的明確配置的描述項控制代碼。 完成此動作後， **SQLCopyDesc**並沒有呼叫以描述項欄位值複製到另一個描述元。 無法與相關聯的描述項控制代碼*StatementHandle*在另一台*ConnectionHandle*，但是; 上使用相同的描述項欄位值*StatementHandles*不同*ConnectionHandles*， **SQLCopyDesc**已呼叫。  
  
 如需描述項標頭或記錄中欄位的說明，請參閱[SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如需有關描述元的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="copying-rows-between-tables"></a>複製資料表之間的資料列  
 應用程式可能會資料從一個資料表複製到另一個無需先行複製應用程式層級的資料。 若要這樣做，應用程式將繫結相同的資料緩衝區，並且描述項資訊的陳述式會擷取資料，並將資料插入複製的陳述式。 這可達成共用 （繫結的明確配置描述元，做為一個陳述式 ARD 並在另一個 APD） 的應用程式描述元，或使用**SQLCopyDesc**複製 ARD 之間的繫結和兩個陳述式 APD。 如果陳述式位於不同的連線， **SQLCopyDesc**必須使用。 此外， **SQLCopyDesc**已複製 IRD 和 IPD，兩個陳述式之間的繫結呼叫。 驅動程式進行呼叫時透過相同的連接上的陳述式複製，傳回 SQL_ACTIVE_STATEMENTS 資訊類型**SQLGetInfo**必須是大於 1 的這項作業才能成功。 （這不案例複製跨連線時）。  
  
### <a name="code-example"></a>程式碼範例  
 在下列範例中，描述元作業可用來將 PartsSource 資料表的欄位複製到 PartsCopy 資料表。 PartsSource 資料表的內容提取到中的資料列集緩衝區*hstmt0*。 這些值用做為參數的 INSERT 陳述式上*hstmt1*擴展 PartsCopy 資料表的資料行。 若要這樣做的 IRD 欄位*hstmt0*會複製到的 IPD 欄位*hstmt1*，與欄位的 ARD *hstmt0*複製到APD中的欄位*hstmt1*。 使用**SQLSetDescField**至 IPD SQL_DESC_PARAMETER_TYPE 屬性設定為 SQL_PARAM_INPUT，當您從具有輸出參數的陳述式複製 IRD 欄位必須為輸入的參數的 IPD 欄位。  
  
```  
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
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

