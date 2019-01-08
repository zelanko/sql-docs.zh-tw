---
title: SQLCloseCursor 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCloseCursor
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCloseCursor
helpviewer_keywords:
- SQLCloseCursor function [ODBC]
ms.assetid: 05b0a054-e28d-4e16-b5b0-07418486b372
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 912e4d109a9e769442c65d292ff190d79705eb21
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53201537"
---
# <a name="sqlclosecursor-function"></a>SQLCloseCursor 函式
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLCloseCursor**關閉資料指標已經開啟的陳述式，並捨棄暫止的結果。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLCloseCursor(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCloseCursor**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLCloseCursor** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|24000|指標狀態無效|沒有資料指標是開啟*StatementHandle*。 （這會傳回只 ODBC 3。*x*驅動程式。)|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫相關聯的連接控制代碼*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 **SQLCloseCursor**傳回 SQLSTATE 24000 （無效的資料指標狀態），如果不是開啟的任何資料指標。 呼叫**SQLCloseCursor**相當於呼叫**SQLFreeStmt** SQL_CLOSE 選項時，發生例外狀況， **SQLFreeStmt**與 SQL_CLOSE 會有任何影響應用程式如果任何資料指標不是開啟的陳述式上，雖然**SQLCloseCursor**傳回 SQLSTATE 24000 （無效的資料指標狀態）。  
  
> [!NOTE]  
>  如果 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLCloseCursor**當沒有資料指標開啟時，不傳回 SQLSTATE 24000 （無效的資料指標狀態），因為驅動程式管理員會將對應**SQLCloseCursor**來**SQLFreeStmt**與 SQL_CLOSE。  
  
 如需詳細資訊，請參閱 <<c0> [ 關閉資料指標](../../../odbc/reference/develop-app/closing-the-cursor.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)並[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|釋放控制代碼|[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)|  
|處理多個結果集|[SQLMoreResults 函式](../../../odbc/reference/syntax/sqlmoreresults-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
