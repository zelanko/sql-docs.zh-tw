---
description: SQLFreeStmt 函數
title: SQLFreeStmt 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFreeStmt
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFreeStmt
helpviewer_keywords:
- SQLFreeStmt function [ODBC]
ms.assetid: 03408162-8b63-4470-90c4-e6c7d8d33892
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9cd85a3ae9098c7258d8934015ef39316a33748
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491258"
---
# <a name="sqlfreestmt-function"></a>SQLFreeStmt 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLFreeStmt** 會停止與特定語句相關聯的處理、關閉與語句相關聯的任何開啟的資料指標、捨棄暫止的結果，或選擇性地釋出所有與語句控制碼相關聯的資源。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFreeStmt(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Option);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼  
  
 *選項*  
 輸出下列其中一個選項：  
  
 SQL_ 關閉：關閉與 *StatementHandle* 相關聯的資料指標 (如果有定義) 並捨棄所有暫止的結果。 應用程式稍後可以使用相同或不同的參數值再次執行 **SELECT** 語句，以重新開啟此資料指標。 如果沒有開啟任何資料指標，此選項就不會影響應用程式。 您也可以呼叫**SQLCloseCursor**來關閉資料指標。 如需詳細資訊，請參閱 [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
 SQL_DROP：此選項已被取代。 使用 SQL_DROP 的*選項*呼叫**SQLFreeStmt**時，會在驅動程式管理員中對應至[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
 SQL_UNBIND：將 ARD 的 SQL_DESC_COUNT 欄位設定為0，釋放 **SQLBindCol** 針對指定 *StatementHandle*所系結的所有資料行緩衝區。 這不會解除書簽資料行的系結;若要這樣做，書簽資料行之 ARD 的 SQL_DESC_DATA_PTR 欄位會設定為 Null。 請注意，如果這項作業是在由多個語句共用的明確配置描述項上執行，此作業將會影響共用描述項之所有語句的系結。 如需詳細資訊，請參閱 [ (基本) 取得結果的總覽 ](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 SQL_RESET_PARAMS：將 APD 的 SQL_DESC_COUNT 欄位設定為0，釋放 **SQLBindParameter** 針對指定 *StatementHandle*所設定的所有參數緩衝區。 如果這項作業是在一個以上的語句所共用的明確配置描述項上執行，此作業將會影響共用描述項之所有語句的系結。 如需詳細資訊，請參閱系結 [參數](../../../odbc/reference/develop-app/binding-parameters-odbc.md)。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFreeStmt**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLFreeStmt** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLFreeStmt** 時，這個非同步函數仍在執行中。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在針對所有資料流程參數抓取資料之前，會使用設定為 SQL_RESET_PARAMS 的 *選項* 來呼叫此函數。<br /><br />  (DM) 針對 *StatementHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY092|選項類型超出範圍| (DM) 為引數 *選項* 指定的值不是：<br /><br /> SQL_CLOSE SQL_DROP SQL_UNBIND SQL_RESET_PARAMS|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 使用 SQL_CLOSE 選項來呼叫 **SQLFreeStmt** 相當於呼叫 **SQLCloseCursor**，不同之處在于如果語句沒有開啟任何資料指標，則具有 SQL_CLOSE 的 **SQLFreeStmt** 不會影響應用程式。 如果沒有開啟任何資料指標，呼叫 **SQLCloseCursor** 會傳回 SQLSTATE 24000 (不正確資料指標狀態) 。  
  
 應用程式在釋放語句控制碼之後，不應該使用該控制碼;驅動程式管理員不會檢查函式呼叫中控制碼的有效性。  
  
## <a name="example"></a>範例  
 這是免費控制碼的良好程式設計作法。 不過，為了簡單起見，下列範例不包含可釋放已配置之控制碼的程式碼。 如需如何釋放控制碼的範例，請參閱 [SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|關閉資料指標|[SQLCloseCursor 函式](../../../odbc/reference/syntax/sqlclosecursor-function.md)|  
|釋放控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
