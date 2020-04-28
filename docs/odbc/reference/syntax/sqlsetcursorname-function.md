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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a3bcd07a39401d49be04d141e50c671179efb16
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287338"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLSetCursorName**會將資料指標名稱與現用語句產生關聯。 如果應用程式未呼叫**SQLSetCursorName**，驅動程式會視需要產生 SQL 語句處理的資料指標名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *CursorName*  
 源資料指標名稱。 若要有效率地處理，資料指標名稱不應包含資料指標名稱中的任何前置或尾端空格，而且如果資料指標名稱包含分隔的識別碼，則分隔符號應定位為游標名稱中的第一個字元。  
  
 *NameLength*  
 源**CursorName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetCursorName**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLSetCursorName**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|資料指標名稱超過上限，因此只會使用允許的最大字元數。|  
|24000|指標狀態無效|對應至*StatementHandle*的語句已是已執行或游標位置的狀態。|  
|34000|指標名稱無效|**CursorName*中指定的資料指標名稱無效，因為它超過驅動程式所定義的最大長度，或是以 "SQLCUR" 或 "SQL_CUR" 開頭。|  
|3C000|重複的資料指標名稱|**CursorName*中指定的資料指標名稱已存在。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY009|Null 指標的使用不正確|（DM）引數*CursorName*是 null 指標。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLSetCursorName**函式時，此 aynchronous 函數仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）引數*NameLength*小於0，但不等於 SQL_NTS。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>評價  
 資料指標名稱只會在定位 update 和 delete 語句中使用（例如，**更新**_資料表名稱_.。。**其中目前的**資料_指標名稱_）。 如需詳細資訊，請參閱[定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式未呼叫**SQLSetCursorName**來定義資料指標名稱，則在執行查詢語句時，驅動程式會產生開頭為字母 SQL_CUR 的名稱，而且長度不超過18個字元。  
  
 連接內的所有資料指標名稱都必須是唯一的。 資料指標名稱的最大長度是由驅動程式所定義。 為了達到最大的互通性，建議應用程式將資料指標名稱限制為不超過18個字元。 在 ODBC 3.x*中，如果*資料指標名稱是加上引號的識別碼，則會以區分大小寫的方式來處理它，而且它可以包含 SQL 語法不允許或特別處理的字元，例如空白或保留的關鍵字。 如果必須以區分大小寫的方式來處理資料指標名稱，則必須以引號識別碼傳遞。  
  
 已明確或隱含設定的資料指標名稱，會在與它關聯的語句卸載之前，使用**SQLFreeHandle**。 只要資料指標處於已配置或備妥的狀態，就可以呼叫**SQLSetCursorName**來重新命名語句上的資料指標。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會使用**SQLSetCursorName**來設定語句的資料指標名稱。 然後，它會使用該語句來抓取 CUSTOMERS 資料表的結果。 最後，它會執行定點更新，以變更 John Smith 的電話號碼。 請注意，應用程式會針對**SELECT**和**UPDATE**語句使用不同的語句控制碼。  
  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回資料指標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|設定資料指標滾動選項|[SQLSetScrollOptions 函式](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
