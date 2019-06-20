---
title: SQLSetCursorName 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a976d7caad790c80b15c17d65686ee1f6308f415
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536751"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLSetCursorName**關聯現用陳述式中的資料指標名稱。 如果應用程式不會呼叫**SQLSetCursorName**，驅動程式會視需要來處理 SQL 陳述式，會產生資料指標名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *CursorName*  
 [輸入]資料指標名稱。 有效的處理，資料指標名稱不得包含任何開頭或尾端空格的資料指標名稱，以及如果資料指標名稱包含分隔的識別碼，應為資料指標名稱的第一個字元位於分隔符號。  
  
 *NameLength*  
 [輸入]中的字元長度 **Current*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetCursorName**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetCursorName** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|資料指標名稱超過最大的限制，因此使用只允許的字元數上限。|  
|24000|指標狀態無效|對應至的陳述式*StatementHandle*已存在於執行，或按一下 資料指標定位的狀態。|  
|34000|指標名稱無效|中指定的資料指標名稱 **Current*無效，因為它超過最大長度，驅動程式時，所定義，或者啟動 「 SQLCUR"或"SQL_CUR。 」|  
|3C000|重複的資料指標名稱|中指定的資料指標名稱 **Current*已經存在。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY009|使用無效的 null 指標|(DM) 引數*Current*是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此 aynchronous 函式仍在執行時**SQLSetCursorName**呼叫函式。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數*NameLength*小於 0，但不是等於 SQL_NTS。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 資料指標名稱僅用於定位的 update 和 delete 陳述式 (例如**更新**_資料表名稱_...**WHERE CURRENT OF** _資料指標名稱_)。 如需詳細資訊，請參閱 <<c0> [ 定位更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式不會呼叫**SQLSetCursorName**來定義資料指標名稱，在驅動程式會產生的名稱開頭為字母 SQL_CUR，而且未超過 18 個字元的長度是查詢陳述式的執行。  
  
 在連接中的所有資料指標名稱必須是唯一的。 資料指標名稱的最大長度是由驅動程式定義。 最大的互通性，建議應用程式限制為不超過 18 個字元的資料指標名稱。 在 ODBC 3 *.x*，如果資料指標名稱是加上引號的識別項視為區分大小寫的方式，它可以包含字元的 SQL 語法不會允許或態度，例如空白或保留的關鍵字。 如果資料指標名稱都必須被視為區分大小寫的方式，則必須傳遞做為加上引號的識別碼。  
  
 資料指標名稱，設定明確或隱含地將會保持設定直到除與相關聯的陳述式時，使用**SQLFreeHandle**。 **SQLSetCursorName**可以呼叫來重新命名的資料指標陳述式，只要游標處於已配置或已備妥狀態。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會使用**SQLSetCursorName**設定陳述式的資料指標名稱。 然後，它會使用該陳述式來擷取 CUSTOMERS 資料表中的結果。 最後，它會執行定位的更新，以變更為 John Smith 的電話號碼。 請注意，應用程式使用不同的陳述式控制代碼，以便**選取** 並**更新**陳述式。  
  
 如需其他程式碼範例，請參閱[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```cpp  
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
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
