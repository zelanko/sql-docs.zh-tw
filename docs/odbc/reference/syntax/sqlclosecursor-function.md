---
description: SQLCloseCursor 函式
title: SQLCloseCursor 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6b4abc6076d976640325475594b80d6d503b50fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448826"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLCloseCursor** 會關閉已在語句上開啟的資料指標，並捨棄暫止的結果。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCloseCursor**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLCloseCursor** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|24000|指標狀態無效|在 *StatementHandle*上未開啟任何資料指標。  (只有 ODBC 3 才會傳回此方法。*x* 驅動程式。 ) |  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式是針對與 *StatementHandle* 相關聯的連接控制碼呼叫，而且在呼叫此函式時仍在執行中。<br /><br />  (DM) 針對 *StatementHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 如果沒有開啟任何資料指標， **SQLCloseCursor**會傳回 SQLSTATE 24000 (不正確資料指標狀態) 。 呼叫 **SQLCloseCursor** 相當於使用 SQL_CLOSE 選項來呼叫 **SQLFreeStmt** ，但如果語句上沒有開啟任何資料指標，則 **SQLFreeStmt** with SQL_CLOSE 不會影響應用程式，而 **SQLCloseCursor** 會傳回 SQLSTATE 24000 (不正確資料指標狀態) 。  
  
> [!NOTE]  
>  如果是 ODBC 3。使用 ODBC 2 的*x* 應用程式。*x* 驅動程式會在沒有任何資料指標開啟時呼叫 **SQLCloseCursor** ，SQLSTATE 24000 (不會傳回不正確資料指標狀態) ，因為驅動程式管理員會將 **SQLCloseCursor** 對應至具有 SQL_CLOSE 的 **SQLFreeStmt** 。  
  
 如需詳細資訊，請參閱 [關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱 [SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md) 函式和 [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)函式。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|釋放控制碼|[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|處理多個結果集|[SQLMoreResults 函數](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
