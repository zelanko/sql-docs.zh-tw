---
title: SQLGetCursorName 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285546"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLGetCursorName**會傳回與指定的語句相關聯的資料指標名稱。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *CursorName*  
 輸出要在其中傳回資料指標名稱之緩衝區的指標。  
  
 如果*CursorName*為 Null， *NameLengthPtr*仍會傳回*CursorName*所指向的緩衝區中可傳回的字元總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源\* *CursorName*的長度（以字元為單位）。 如果* \*CursorName*中的值是 Unicode 字串（在呼叫**SQLGetCursorNameW**時），則*BufferLength*引數必須是偶數。  
  
 *NameLengthPtr*  
 輸出記憶體的指標，要在其中傳回\* *CursorName*中可傳回的字元總數（不包括 null 終止字元）。 如果可傳回的字元數大於或等於*BufferLength*， \* *CursorName*中的資料指標名稱會截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetCursorName**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLGetCursorName**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *CursorName*不夠大，無法傳回整個資料指標名稱，所以資料指標名稱已截斷。 Untruncated 資料指標名稱的長度會在 **NameLengthPtr*中傳回。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLGetCursorName**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY015|沒有可用的資料指標名稱|（DM）*驅動程式是 ODBC 2.x 驅動程式*，語句上沒有開啟的資料指標，而且沒有使用**SQLSetCursorName**設定的資料指標名稱。|  
|HY090|不正確字串或緩衝區長度|（DM）引數*BufferLength*中指定的值小於0。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>評價  
 資料指標名稱只會在定位 update 和 delete 語句中使用（例如，**更新**_資料表名稱_.。。**其中目前的**資料_指標名稱_）。 如需詳細資訊，請參閱[定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式未呼叫**SQLSetCursorName**來定義資料指標名稱，則驅動程式會產生名稱。 這個名稱的開頭是字母 SQL_CUR。  
  
> [!NOTE]
>  在 ODBC 2.x*中，如果*沒有開啟的資料指標，而且呼叫**SQLSetCursorName**未設定任何名稱，則呼叫**SQLGetCursorName**會傳回 SQLSTATE HY015 （沒有可用的資料指標名稱）。 在 ODBC 3.x*中，這*已不再是 true;無論何時呼叫**SQLGetCursorName** ，驅動程式都會傳回資料指標名稱。  
  
 **SQLGetCursorName**會傳回資料指標的名稱，不論該名稱是以明確或隱含方式建立。 如果未呼叫**SQLSetCursorName** ，則會隱含產生資料指標名稱。 只要資料指標處於已配置或備妥的狀態，就可以呼叫**SQLSetCursorName**來重新命名語句上的資料指標。  
  
 已明確或隱含設定的資料指標名稱，會在與它相關聯的*StatementHandle*中斷時，使用**SQLFreeHandle**搭配 SQL_HANDLE_STMT 的*HandleType* 。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備語句以執行|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
