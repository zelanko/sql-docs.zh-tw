---
title: SQLCopyDesc 功能 |微軟文件
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
ms.openlocfilehash: ef1fa5b319e8d72d5b70e6f2010e493eec6f844a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301225"
---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc 函式
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLCopyDesc**將描述符資訊從一個描述符句柄複製到另一個描述符句柄。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>引數  
 *來源DescHandle*  
 [輸入]源描述符句柄。  
  
 *目標德斯克德爾*  
 [輸入]目標描述符句柄。 *TargetDescHandle*參數可以是應用程式描述符或 IPD 的句柄。 *TargetDescHandle*無法設定為 IRD 的句柄,或者**SQLCopyDesc**將傳回 SQLSTATE HY016(無法修改實現行描述符)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCopyDesc**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_DESC的*句柄類型*和*Handle*目標*DescHandle 的句柄*。 如果在呼叫中傳遞了無效的*SourceDescHandle,* 將返回SQL_INVALID_HANDLE,但不會返回 SQLSTATE。 下表列出了**SQLCopyDesc**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
 返回錯誤后,將立即中止對**SQLCopyDesc**的調用,並且未定義*TargetDescHandle*描述符中欄位的內容。  
  
 由於**SQLCopyDesc**可以透過呼叫**SQLGetDescField**和**SQLSetDescField**實現,因此**SQLCopyDesc**可能會返回**SQLGetDescField**或**SQLSetDescField**傳回的 SQLStatEs。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY007|未準備關聯語句|*SourceDescHandle*與 IRD 相關聯,關聯的語句句柄未處於準備或執行狀態。|  
|HY010|函式序列錯誤|(DM) *SourceDescHandle*或*TargetDescHandle*中的描述符句柄與*語句句柄相關聯,* 其中調用了異步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) *SourceDescHandle*或*TargetDescHandle*中的描述符句柄與*一個語句句柄*相關聯,SQL_NEED_DATA調用 SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos。** **SQLExecute** **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 對於與*SourceDescHandle*或*TargetDescHandle*關聯的連接句柄,調用了異步執行函數。 調用**SQLCopyDesc**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用為與*SourceDescHandle 或 TargetDescHandle*關聯的語句**SQLExecute***TargetDescHandle*句柄之一,並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY016|無法變更行描述子|*TargetDescHandle*與 IRD 相關聯。|  
|HY021|描述符資訊不一致|在一致性檢查期間檢查的描述符資訊不一致。 有關詳細資訊,請參閱**SQLSetDescField**中的「一致性檢查」。|  
|HY092|不合法屬性/選項識別碼|對**SQLCopyDesc 的**呼叫提示呼叫**SQLSetDescField,** 但*\*ValuePtr*對*TargetDescHandle*上的*字段識別元*參數無效。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*源DescHandle*或*TargetDescHandle*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 對**SQLCopyDesc 的**呼叫將源描述符句柄的欄位複製到目標描述符句柄。 欄位只能複製到應用程式描述器或 IPD,但無法複製到 IRD。 可以從應用程式或實現描述符複製欄位。  
  
 僅當語句句柄處於準備或執行狀態時,才能從 IRD 複製欄位;否則,函數將返回 SQLSTATE HY007(未準備關聯語句)。  
  
 無論是否已準備語句,都可以從 IPD 複製欄位。 如果已準備具有動態參數的 SQL 語句,並且支援並啟用 IPD 的自動填充,則驅動程式將填充 IPD。 當**SQLCopyDesc**調用 IPD 作為*源DescHandle時*,將複製填充的欄位。 如果驅動程式未填充 IPD,則複製最初在 IPD 中使用的欄位的內容。  
  
 描述符的所有欄位(SQL_DESC_ALLOC_TYPE(指定描述符句柄是自動分配還是顯式分配)除外,無論是否為目標描述符定義該欄位,都將複製該欄位。 複製的欄位覆蓋現有欄位。  
  
 如果*SourceDescHandle*和*TargetDescHandle*參數與同一驅動程式關聯,即使驅動程式位於兩個不同的連接或環境中,驅動程式也會複製所有描述符位。 如果*SourceDescHandle*和*TargetDescHandle*參數與不同的驅動程式相關聯,則驅動程式管理員將複製 ODBC 定義的欄位,但不會複製由 ODBC 為描述符類型定義的驅動程式定義的欄位。  
  
 如果發生錯誤,將立即中止對**SQLCopyDesc 的**調用。  
  
 複製SQL_DESC_DATA_PTR欄位時,對目標描述符執行一致性檢查。 如果一致性檢查失敗,將返回 SQLSTATE HY021(不一致的描述符資訊),並立即中止對**SQLCopyDesc 的**調用。 有關一致性檢查的詳細資訊,請參閱[SQLSetDescRec 函數](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的「一致性檢查」。  
  
 描述符句柄可以跨連接複製,即使連接位於不同的環境中也是如此。 如果驅動程式管理器檢測到源和目標描述符句柄不屬於同一連接,並且兩個連接屬於單獨的驅動程式,則它透過使用**SQLGetDescField**和**SQLSetDescField**執行逐字段複製來實現**SQLCopyDesc。**  
  
 當**SQLCopyDesc**調用一個驅動程式上的*SourceDescHandle*和另一個驅動程式上的*TargetDescHandle*時,*將清除 SourceDescHandle*的錯誤佇列。 這是因為在這種情況下 **,SQLCopyDesc**是通過對**SQLGetDescField**和**SQLSetDescField**的調用實現的。  
  
> [!NOTE]  
>  應用程式也許能夠將顯式分配的描述符句柄與*語句句柄*相關聯,而不是調用**SQLCopyDesc**將欄位從一個描述符複製到另一個描述符。 通過將SQL_ATTR_APP_ROW_DESC或SQL_ATTR_APP_PARAM_DESC語句屬性設置為顯式分配的描述符的句柄,可以與同一*連接句柄*上的另一個*語句句柄*關聯顯式分配的描述符。 完成此操作後,不必呼叫**SQLCopyDesc**即可將描述符位值從一個描述符複製到另一個描述符。 但是,描述符句柄不能與另一個*ConnectHandle*上的*語句句柄*關聯;要在不同的*連接句柄*上的*語句句柄*上使用相同的描述符位值,必須調用**SQLCopyDesc。**  
  
 有關描述符標題或記錄中的欄位的說明,請參閱[SQLSetDescField 函數](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 有關描述符的詳細資訊,請參閱[描述子](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="copying-rows-between-tables"></a>在表格之間複製列  
 應用程式可以將數據從一個表複製到另一個表,而無需在應用程式級別複製數據。 為此,應用程式將相同的數據緩衝區和描述符資訊綁定到獲取數據的語句以及將數據插入到副本中的語句。 這可以通過共用應用程式描述符(將顯式分配的描述符綁定為 ARD 到另一個語句中的 APD)或使用**SQLCopyDesc**複製兩個語句的 ARD 和 APD 之間的綁定來實現。 如果語句位於不同的連接上,則必須使用**SQLCopyDesc。** 此外,必須調用**SQLCopyDesc**來複製 IRD 和兩個語句的 IPD 之間的綁定。 在同一連接上跨語句複製時 SQL_ACTIVE_STATEMENTS,驅動程式返回的調用**SQLGetInfo**的資訊類型必須大於 1 才能成功。 (跨連接複製時不是這樣。  
  
### <a name="code-example"></a>程式碼範例  
 在下面的範例中,描述符操作用於將零件源表的欄位複製到「零件複製」表中。 零件源表的內容被提取到*hstmt0*中的排集緩衝區中。 這些值用作*hstmt1*上的 INSERT 語句的參數,以填充零件複製表的列。 為此 *,hstmt0*的 IRD 欄位被複製到*hstmt1*的 IPD 欄位,並將*hstmt0*的 ARD 欄位複製到*hstmt1*的 APD 欄位。 當您將 IRD 欄位從具有輸出參數的語句複製到需要輸入參數的 IPD 欄位時,使用**SQLSetDescField**將 IPD 的SQL_DESC_PARAMETER_TYPE屬性設定為SQL_PARAM_INPUT。  
  
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
|取得多個描述符位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述符欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述符位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
