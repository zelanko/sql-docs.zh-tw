---
title: SQLSetCursor 名稱函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287338"
---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLSetCursorName**將游標名稱與活動語句關聯起來。 如果應用程式不呼叫**SQLSetCursorName,** 驅動程式將根據需要生成 SQL 語句處理所需的遊標名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *游標名稱*  
 [輸入]游標名稱。 為了進行有效的處理,游標名稱不應在游標名稱中包括任何前導空格或尾隨空格,如果游標名稱包含分隔標識符,則分隔符應定位為游標名稱中的第一個字元。  
  
 *NameLength*  
 [輸入]長度以 =*游標名稱*的字元為 。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetCursorName**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLSetCursorName**通常傳回的 SQLSTATE 值,並解釋了此函式中內容中的每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|游標名稱超過最大限制,因此只使用允許的最大字元數。|  
|24000|指標狀態無效|與*語句句柄*對應的語句已處於已執行或游標定位狀態。|  
|34000|指標名稱無效|在[*CursorName 中*指定的游標名稱無效,因為它超過了驅動程式定義的最大長度,或者以"SQLCUR"或"SQL_CUR"開始。|  
|3C000|重覆的游標名稱|在游*標名稱 中*指定的游標名稱已存在。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY009|不合法的空白指標|(DM) 參數*CursorName*是一個空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 呼叫**SQLSetCursorName**函數時,此 aynchronous 函數仍在執行。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 參數*NameLength*小於 0,但不等於SQL_NTS。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 游標名稱只有定位的更新與移除語句(例如,**更新**_表名_...**其中游**_標名稱_的目前 。 有關詳細資訊,請參閱[位置更新與刪除語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式不呼叫**SQLSetCursorName**來定義游標名稱,則在執行查詢語句時,驅動程式將生成以字母SQL_CUR開頭且長度不超過 18 個字元的名稱。  
  
 連接中的所有遊標名稱都必須是唯一的。 游標名稱的最大長度由驅動程式定義。 為了達到最大互操作性,建議應用程式將游標名稱限制為不超過 18 個字元。 在 ODBC 3 *.x*中,如果游標名稱是參考標識符,則以區分大小寫的方式處理它,並且它可以包含 SQL 語法不允許或將特殊處理的字元,例如空白或保留關鍵字。 如果必須以區分大小寫的方式處理游標名稱,則必須將其作為引號標識符傳遞。  
  
 顯式設定或隱式設置的游標名稱將保持設置,直到使用**SQLFreeHandle**刪除與其關聯的語句。 只要游標處於已分配或準備狀態,就可以調用**SQLSetCursorName**在語句上重新命名游標。  
  
## <a name="code-example"></a>程式碼範例  
 在下面的範例中,應用程式使用**SQLSetCursorName**為語句設置游標名稱。 然後,它使用該語句從 CUSTOMERS 表檢索結果。 最後,它執行定位更新以更改約翰·史密斯的電話號碼。 請注意,應用程式對**SELECT**和**UPDATE**語句使用不同的語句句柄。  
  
 有關另一個代碼範例,請參閱[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
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
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|返回游標名稱|[SQLGetCursorName 函式](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|設定游標滾動選項|[SQLSetScrollOptions 函式](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
