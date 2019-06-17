---
title: SQLCancel 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ad701efe914780a74bba3b8f0530b4881d7709
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537623"
---
# <a name="sqlcancel-function"></a>SQLCancel 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLCancel**取消的陳述式處理。  
  
 若要取消連接或陳述式的處理，請使用[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancel**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLCancel** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)引數中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLCancel**呼叫函式。<br /><br /> (DM) 取消作業失敗，因為非同步作業是在連接控制代碼相關聯的進度*StatementHandle*。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY018|伺服器拒絕取消要求|伺服器拒絕取消要求。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 **SQLCancel**可以取消下列類型的陳述式上的處理：  
  
-   函式，以非同步方式執行的陳述式上。  
  
-   需要資料的陳述式中的函式。  
  
-   在另一個執行緒上的陳述式上執行的函式。  
  
 在 ODBC 2。*x*，如果應用程式會呼叫**SQLCancel**當陳述式上不進行任何處理**SQLCancel**具有相同的效果**SQLFreeStmt** SQL_CLOSE 選項;這種行為只為完整性而定義，而且應用程式應該呼叫**SQLFreeStmt**或是**SQLCloseCursor**來關閉資料指標。  
  
 當**SQLCancel**呼叫來取消陳述式，會清除的需求資料，所取消函式所張貼的診斷記錄，以非同步方式執行函式或陳述式中的函式和**SQLCancel**張貼自己的診斷記錄; 當**SQLCancel**稱為取消另一個執行緒上的陳述式上執行的函式，不過，它不會清除此診斷記錄的可取消函式，並不會不張貼自己的診斷記錄。  
  
## <a name="canceling-asynchronous-processing"></a>取消非同步處理  
 應用程式以非同步方式呼叫的函式之後，它會呼叫重複以判斷是否結束處理函式。 如果函式仍在處理中，它會傳回 SQL_STILL_EXECUTING。 如果函式已完成處理，它會傳回不同的程式碼。  
  
 傳回 SQL_STILL_EXECUTING 的函式呼叫之後，應用程式可以呼叫**SQLCancel**取消函式。 如果取消要求成功，驅動程式傳回 SQL_SUCCESS。 此訊息不會指出實際取消函式之;表示已處理取消要求。 時，或如果函式會取消實際上是驅動程式相依性和資料來源而定。 應用程式必須繼續呼叫原始函式，直到傳回的程式碼不是 SQL_STILL_EXECUTING。 如果已成功取消函式，傳回碼是 SQL_ERROR 並 SQLSTATE HY008 （已取消的作業）。 如果其正常的處理完成的函式，傳回碼是 SQL_SUCCESS 或如果函數成功 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 並 HY008 以外的 SQLSTATE （已取消的作業） 如果失敗的函式。  
  
> [!NOTE]  
>  在 ODBC 3.5 中，呼叫**SQLCancel**時不處理是在陳述式不會當做**SQLFreeStmt** SQL_CLOSE 選項，但已完全就無作用。 若要關閉資料指標，應用程式應該呼叫**SQLCloseCursor**，而非**SQLCancel**。  
  
 如需有關非同步處理的詳細資訊，請參閱 <<c0> [ 非同步執行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。  
  
## <a name="canceling-functions-that-need-data"></a>取消需要資料的函式  
 在後**SQLExecute**或是**SQLExecDirect**會傳回 SQL_NEED_DATA，而且資料已傳送的所有資料在執行中參數之前，應用程式可以呼叫**SQLCancel**若要取消陳述式執行。 已取消的陳述式之後，應用程式可以呼叫**SQLExecute**或是**SQLExecDirect**一次。 如需詳細資訊，請參閱 < [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 在後**SQLBulkOperations**或是**SQLSetPos**會傳回 SQL_NEED_DATA，而且資料已傳送的所有資料在執行資料行之前，應用程式可以呼叫**SQLCancel**若要取消作業。 已取消作業後，應用程式可以呼叫**SQLBulkOperations**或是**SQLSetPos**再次; 取消不會影響資料指標狀態或目前的游標位置。 如需詳細資訊，請參閱 < [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或是[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>取消另一個執行緒上執行的函式  
 在多執行緒應用程式中，應用程式可以取消另一個執行緒執行的函式。 若要取消的函式應用程式會呼叫**SQLCancel**與目標函式，但不同的執行緒上使用相同的陳述式控制代碼。 此函式的取消方式，取決於驅動程式和作業系統。 如同取消以非同步方式執行的傳回碼的函式**SQLCancel**僅會指示是否驅動程式可成功處理要求。 可以傳回只有 SQL_SUCCESS 或 SQL_ERROR;未不傳回任何診斷的資訊。 如果原始函式已取消，則會傳回 SQL_ERROR，而且 SQLSTATE HY008 （已取消的作業）。  
  
 如果 SQL 陳述式正在執行的時機**SQLCancel**取消陳述式執行的另一個執行緒上呼叫，就能成功地執行，並在取消時傳回 SQL_SUCCESS 也會成功。 在此情況下，驅動程式管理員會假設執行陳述式開啟資料指標已關閉的 [取消]，因此應用程式將無法使用資料指標。  
  
 如需有關執行緒的詳細資訊，請參閱[進行多執行緒處理](../../../odbc/reference/develop-app/multithreading.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至參數的緩衝區|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|執行大量插入或更新作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|以非同步方式執行連接控制代碼上另外功能的函式會取消**SQLCancel**。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放陳述式控制代碼|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|取得的診斷記錄的欄位或診斷的標頭的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|取得多個欄位的診斷資料結構|[SQLGetDiagRec 函式](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|傳回的資料傳送至下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|在執行階段傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|遊標定位在資料列集、 重新整理此資料列集中，或更新或刪除在結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
