---
description: SQLSetCursorName 函式
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
ms.openlocfilehash: 1a7deee4ecb37225260f011d4944e992f16d94e1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499487"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLSetCursorName** 會將資料指標名稱與現用語句產生關聯。 如果應用程式未呼叫 **SQLSetCursorName**，驅動程式會視需要產生 SQL 語句處理所需的資料指標名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *CursorName*  
 輸出資料指標名稱。 為了有效率地處理，資料指標名稱不應該在資料指標名稱中包含任何前置或尾端空格，而且如果資料指標名稱包含分隔的識別碼，則分隔符號應該定位為數據指標名稱中的第一個字元。  
  
 *NameLength*  
 輸出**CursorName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetCursorName**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLSetCursorName** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|資料指標名稱超過上限，因此只會使用允許的最大字元數。|  
|24000|指標狀態無效|對應至 *StatementHandle* 的語句已在執行或資料指標位置的狀態。|  
|34000|指標名稱無效|**CursorName* 中指定的資料指標名稱無效，因為它超過驅動程式所定義的最大長度，或以 "SQLCUR" 或 "SQL_CUR" 開頭。|  
|3C000|重複的資料指標名稱|**CursorName* 中指定的資料指標名稱已存在。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY009|Null 指標的用法無效| (DM) 引數 *CursorName* 為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLSetCursorName** 函式時，此 aynchronous 函數仍在執行中。<br /><br />  (DM) 針對 *StatementHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *NameLength* 小於0但不等於 SQL_NTS。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 資料指標名稱只在定位 update 和 delete 語句中使用 (例如，**更新**_資料表名稱_.。。) **的目前的**資料_指標名稱_。 如需詳細資訊，請參閱 [定點更新和刪除語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式未呼叫 **SQLSetCursorName** 來定義資料指標名稱，則在執行查詢語句時，驅動程式會產生以字母 SQL_CUR 開頭且長度不超過18個字元的名稱。  
  
 連接中的所有資料指標名稱都必須是唯一的。 資料指標名稱的最大長度是由驅動程式所定義。 為了達到最大的互通性，建議應用程式將資料指標名稱限制為不超過18個字元。 在 ODBC 3.x*中，如果*資料指標名稱是加上引號的識別碼，則會以區分大小寫的方式來處理它，而且它可以包含 SQL 的語法不允許或特別處理的字元，例如空白或保留的關鍵字。 如果必須以區分大小寫的方式來處理資料指標名稱，則必須以引號識別碼形式傳遞。  
  
 明確或隱含設定的資料指標名稱，在使用 **SQLFreeHandle**卸載與其相關聯的語句之前，會保持設定狀態。 只要資料指標處於已配置或已準備的狀態，即可呼叫**SQLSetCursorName**來重新命名語句上的資料指標。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會使用 **SQLSetCursorName** 來設定語句的資料指標名稱。 然後，它會使用該語句來取出 CUSTOMERS 資料表的結果。 最後，它會執行定點更新來變更 John Smith 的電話號碼。 請注意，此應用程式會針對 **SELECT** 和 **UPDATE** 語句使用不同的語句控制碼。  
  
 如需其他程式碼範例，請參閱 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
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
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回資料指標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|設定資料指標滾動選項|[SQLSetScrollOptions 函式](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
