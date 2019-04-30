---
title: SQLFreeStmt 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f3cca214aeb63720e193f57f06a22481ae7d369f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259323"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLFreeStmt**停止特定的陳述式相關聯的處理、 關閉任何開啟的資料指標相關聯的陳述式，會捨棄暫止的結果，或選擇性地釋放陳述式控制代碼相關聯的所有資源。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼  
  
 *選項*  
 [輸入]下列選項之一：  
  
 SQL_ 關閉：關閉資料指標相關聯*StatementHandle* （如果已定義），並捨棄所有暫止的結果。 應用程式可以稍後重新開啟這個資料指標執行**選取**再次以相同或不同的參數值的陳述式。 如果任何資料指標開啟時，此選項會有不會影響應用程式。 **SQLCloseCursor**也可以呼叫來關閉資料指標。 如需詳細資訊，請參閱 <<c0> [ 關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 SQL_DROP:這個選項已被取代。 呼叫**SQLFreeStmt**具有*選項*SQL_DROP 的會對應至在驅動程式管理員[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
 SQL_UNBIND:設定為 0，釋放所有的資料行緩衝區 ARD SQL_DESC_COUNT 欄位繫結**SQLBindCol**的給定*StatementHandle*。 這不會不解除繫結的書籤資料行中;若要這樣做，請 ARD 書籤資料行的 SQL_DESC_DATA_PTR 欄位是設為 NULL。 請注意，是否共用的多個陳述式的明確配置描述元上執行這項作業，則作業會影響共用描述元的所有陳述式的繫結。 如需詳細資訊，請參閱 <<c0> [ 概觀的擷取結果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 SQL_RESET_PARAMS:APD 中的 [SQL_DESC_COUNT] 欄位設定為 0，釋放所有所設定的參數緩衝區**SQLBindParameter**的給定*StatementHandle*。 如果共用的多個陳述式的明確配置描述元上執行這項作業，則這項作業會影響共用描述元的所有陳述式的繫結。 如需詳細資訊，請參閱 <<c0> [ 繫結參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeStmt**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLFreeStmt** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLFreeStmt**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 使用呼叫此函式*選項*設定為 SQL_RESET_PARAMS，資料擷取的資料流處理的所有參數。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY092|選項類型超出範圍|(DM) 引數指定的值*選項*不是：<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 呼叫**SQLFreeStmt** SQL_CLOSE 與選項相當於呼叫**SQLCloseCursor**，不同之處在於**SQLFreeStmt** SQL_CLOSE 與不會影響應用程式如果任何資料指標不是，開啟的陳述式上。 如果任何資料指標不為開啟，請呼叫**SQLCloseCursor**傳回 SQLSTATE 24000 （無效的資料指標狀態）。  
  
 釋出; 之後，應用程式不應使用的陳述式控制代碼驅動程式管理員不會檢查函式呼叫中的控制代碼的有效性。  
  
## <a name="example"></a>範例  
 它是良好的程式設計作法，以釋放控制代碼。 不過，為了簡單起見，下列範例不包含程式碼，可釋放已配置控制代碼。 如需如何釋放控制代碼的範例，請參閱 < [SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
```  
// SQLFreeStmt.cpp  
// compile with: user32.lib odbc32.lib  
#include <windows.h>  
#include <sqlext.h>  
  
int main() {  
   // declare and initialize the environment, connection, statement handles  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   SQLRETURN retCode;  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen;  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, (SQLCHAR *)"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1024 + 1, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
   retCode = SQLFreeStmt(hstmt, SQL_UNBIND);  
   retCode = SQLFreeStmt(hstmt, SQL_RESET_PARAMS);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|關閉資料指標|[SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|釋放控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
