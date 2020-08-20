---
description: SQLGetCursorName 函數
title: SQLGetCursorName 函式 |Microsoft Docs
ms.custom: ''
ms.date: 06/12/2020
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
ms.openlocfilehash: 454a6630afb565381b8dfc457c5c34a1194ccf63
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461100"
---
# <a name="sqlgetcursorname-function"></a>SQLGetCursorName 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetCursorName** 會傳回與指定的語句相關聯的資料指標名稱。  
  
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
 輸出語句控制碼。  
  
 *CursorName*  
 出要傳回資料指標名稱之緩衝區的指標。  
  
 如果 *CursorName* 是 Null， *NameLengthPtr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *CursorName*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出\* *CursorName*的長度（以字元為單位）。 
  
 *NameLengthPtr*  
 出記憶體的指標，要在其中傳回字元總數 (不包括 null 終止字元) 可在 \* *CursorName*中傳回。 如果可傳回的字元數大於或等於*BufferLength*，CursorName 中的資料指標名稱 \* *CursorName*就會被截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetCursorName**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLGetCursorName** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *CursorName*不夠大，無法傳回整個資料指標名稱，因此資料指標名稱已被截斷。 Untruncated 資料指標名稱的長度會在 **NameLengthPtr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLGetCursorName** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 針對 *StatementHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY015|沒有可使用的資料指標名稱| (DM) *驅動程式是 ODBC 2.x 驅動程式* ，語句上沒有任何開啟的資料指標，且沒有使用 **SQLSetCursorName**設定資料指標名稱。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *BufferLength* 中指定的值小於0。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 資料指標名稱只在定位 update 和 delete 語句中使用 (例如，**更新**_資料表名稱_.。。) **的目前的**資料_指標名稱_。 如需詳細資訊，請參閱 [定點更新和刪除語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)。 如果應用程式未呼叫 **SQLSetCursorName** 來定義資料指標名稱，驅動程式會產生名稱。 這個名稱是以字母 SQL_CUR 開頭。  
  
> [!NOTE]
>  在 ODBC 2.x*中，如果*沒有開啟的資料指標，且呼叫 **SQLSetCursorName**未設定任何名稱，則對 **SQLGETCURSORNAME** 的呼叫會傳回 SQLSTATE HY015， (沒有可) 的資料指標名稱。 在 ODBC 3.x*中，這*已不再成立;無論何時呼叫 **SQLGetCursorName** ，驅動程式都會傳回資料指標名稱。  
  
 無論名稱是以明確或隱含方式建立， **SQLGetCursorName**都會傳回資料指標的名稱。 如果未呼叫 **SQLSetCursorName** ，就會隱含地產生資料指標名稱。 只要資料指標處於已配置或已準備的狀態，即可呼叫**SQLSetCursorName**來重新命名語句上的資料指標。  
  
 以明確或隱含方式設定的資料指標名稱會保持設定，直到卸載與其相關聯的 *StatementHandle* 為止，並使用 **SQLFreeHandle** 搭配 SQL_HANDLE_STMT 的 *HandleType* 。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備要執行的語句|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
