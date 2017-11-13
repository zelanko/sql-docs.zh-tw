---
title: "SQLSetCursorName 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 716170dc027cce47b29a11cc9a650cf4fbb3eb29
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLSetCursorName**關聯現用陳述式中的資料指標名稱。 如果應用程式不會呼叫**SQLSetCursorName**，驅動程式會視需要來處理 SQL 陳述式，會產生資料指標名稱。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Current*  
 [輸入]資料指標名稱。 可有效處理，資料指標名稱不應該在資料指標名稱，包含任何開頭或尾端空格，如果資料指標名稱包含分隔的識別碼，應為資料指標名稱的第一個字元位於分隔符號。  
  
 *NameLength*  
 [輸入]中的字元長度 **Current*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetCursorName**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetCursorName** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|資料指標名稱超過最大的限制，因此使用只允許的字元數上限。|  
|24000|指標狀態無效|對應至的陳述式*StatementHandle*中已存在於未執行或資料指標定位的狀態。|  
|34000|指標名稱無效|中指定的資料指標名稱 **Current*無效，因為它超過最大長度，驅動程式時，所定義，或者啟動 「 SQLCUR"或"SQL_CUR。 」|  
|3C000|重複的資料指標名稱|中指定的資料指標名稱 **Current*已經存在。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY009|無效的 null 指標使用|(DM) 引數*Current*為 null 指標。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此 aynchronous 函式還在執行時**SQLSetCursorName**呼叫函式。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數*NameLength*小於 0，但不是等於 SQL_NTS。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 資料指標名稱只用於定位的 update 和 delete 陳述式 (例如，**更新***資料表名稱*...**WHERE CURRENT OF** *資料指標名稱*)。 如需詳細資訊，請參閱[定位的更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式不會呼叫**SQLSetCursorName**來定義資料指標名稱，在執行查詢陳述式，此驅動程式產生的名稱以字母 SQL_CUR 開頭，而且不會超過 18 個字元的長度。  
  
 在連接中的所有資料指標名稱必須是唯一的。 資料指標名稱的最大長度是驅動程式所定義。 最大的互通性，建議應用程式限制為不超過 18 個字元的資料指標名稱。 在 ODBC 3*.x*，如果資料指標名稱會加上引號識別項視為區分大小寫的方式，它可以包含字元的 SQL 語法會允許或態度特殊，例如空格或保留的關鍵字。 如果資料指標名稱必須區分大小寫的方式來處理，它必須傳遞做為引號識別項。  
  
 會設明確或隱含地維持資料指標名稱設定，直到與相關聯的陳述式卸除，則使用**SQLFreeHandle**。 **SQLSetCursorName**可以呼叫以重新命名的資料指標陳述式，只要游標位於未配置或已備妥狀態。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式使用**SQLSetCursorName**設定陳述式的資料指標名稱。 然後會使用該陳述式從 [客戶] 資料表中擷取結果。 最後，它會執行定位的更新，以變更為 John Smith 的電話號碼。 請注意，應用程式使用不同的陳述式控制代碼的**選取**和**更新**陳述式。  
  
 如需其他程式碼範例，請參閱[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回資料指標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|設定資料指標捲動選項|[SQLSetScrollOptions 函式](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

