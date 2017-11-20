---
title: "SQLCancel 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 079a1ac7467348472c501c4dcb055d2cef8e9306
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcancel-function"></a>SQLCancel 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLCancel**取消的陳述式處理。  
  
 若要取消連接或陳述式的處理，請使用[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancel**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLCancel** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)引數中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLCancel**呼叫函式。<br /><br /> (DM) 取消作業失敗，因為非同步作業正在進行連接控制代碼相關聯*StatementHandle*。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY018|伺服器拒絕取消要求|伺服器拒絕取消要求。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 **SQLCancel**可以取消下列類型的陳述式的處理：  
  
-   以非同步方式執行的陳述式上的函式。  
  
-   需要資料的陳述式中的函式。  
  
-   函式，另一個執行緒上的陳述式上執行。  
  
 在 ODBC 2。*x*，如果應用程式呼叫**SQLCancel**當陳述式，不進行任何處理**SQLCancel**具有相同的效果**SQLFreeStmt** SQL_CLOSE 選項。這種行為只為完整性而定義，而且應用程式應該呼叫**SQLFreeStmt**或**SQLCloseCursor**來關閉資料指標。  
  
 當**SQLCancel**呼叫以取消陳述式，已清除的資料需求，正在取消函式所張貼的診斷記錄，以非同步方式執行函式或陳述式中的函式和**SQLCancel**文章它自己的診斷記錄; 當**SQLCancel**稱為取消的陳述式，另一個執行緒上執行的函式，不過，它不會清除診斷記錄的可取消函式，而且不會不張貼它自己的診斷記錄。  
  
## <a name="canceling-asynchronous-processing"></a>取消非同步處理  
 應用程式以非同步方式呼叫的函式之後，它會呼叫不斷地判斷它是否已完成處理函式。 如果函式仍在處理中，它會傳回 SQL_STILL_EXECUTING。 如果函式已完成處理，則會傳回不同的程式碼。  
  
 傳回 SQL_STILL_EXECUTING 的函式呼叫之後，應用程式可以呼叫**SQLCancel**取消函式。 如果取消要求成功，驅動程式傳回 SQL_SUCCESS。 此訊息不表示實際取消函式之;它會指出已處理取消要求。 時，或如果函式會取消實際上是驅動程式而定，資料來源而定。 應用程式必須繼續呼叫原始函式，直到傳回的程式碼不是 SQL_STILL_EXECUTING。 如果已成功取消函式，傳回碼是 SQL_ERROR 並 SQLSTATE HY008 （取消作業）。 如果其正常處理完成的函式，傳回碼是 SQL_SUCCESS 或如果函式成功 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 並 HY008 以外的 SQLSTATE （已取消作業） 如果此函式失敗。  
  
> [!NOTE]  
>  ODBC 3.5，呼叫**SQLCancel**時不會被進行處理的陳述式上不視為**SQLFreeStmt** SQL_CLOSE 選項，但具有根本就無作用。 若要關閉資料指標，應用程式應該呼叫**SQLCloseCursor**，而非**SQLCancel**。  
  
 如需非同步處理的詳細資訊，請參閱[非同步執行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。  
  
## <a name="canceling-functions-that-need-data"></a>取消需要資料的函式  
 之後**SQLExecute**或**SQLExecDirect**傳回 SQL_NEED_DATA，而且已針對所有資料在執行中參數傳送資料之前，應用程式可以呼叫**SQLCancel**取消陳述式執行。 在取消陳述式之後，應用程式可以呼叫**SQLExecute**或**SQLExecDirect**一次。 如需詳細資訊，請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 之後**SQLBulkOperations**或**SQLSetPos**傳回 SQL_NEED_DATA，而且已針對所有資料在執行中資料行傳送資料之前，應用程式可以呼叫**SQLCancel**若要取消作業。 作業已取消之後，應用程式可以呼叫**SQLBulkOperations**或**SQLSetPos**再次; 取消不會影響指標狀態或目前的游標位置。 如需詳細資訊，請參閱[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>取消另一個執行緒上執行的函式  
 在多執行緒應用程式中，應用程式可以取消另一個執行緒執行的函式。 若要取消函式，而應用程式會呼叫**SQLCancel**與當做目標函式，但不同的執行緒上使用相同的陳述式控制代碼。 函式取消的方式取決於驅動程式和作業系統。 如同取消函式，以非同步方式執行的傳回碼**SQLCancel**只會指出是否驅動程式可成功處理要求。 可傳回只有 SQL_SUCCESS 或 SQL_ERROR。沒有傳回任何診斷資訊。 如果原始函式已取消，則會傳回 SQL_ERROR 並 SQLSTATE HY008 （取消作業）。  
  
 如果 SQL 陳述式正在執行時**SQLCancel**取消陳述式執行的另一個執行緒上呼叫，可能會成功地執行，而 [取消] 時傳回 SQL_SUCCESS 也成功。 在此情況下，驅動程式管理員會假設讓應用程式不能使用資料指標，由 [取消]，關閉資料指標開啟的陳述式執行。  
  
 如需執行緒的詳細資訊，請參閱[多執行緒](../../../odbc/reference/develop-app/multithreading.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至參數的緩衝區|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|執行大量插入或更新作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消非同步執行連接控制代碼上另外的功能的函式**SQLCancel**。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放陳述式控制代碼|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|取得診斷記錄的欄位或診斷的標頭中的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|取得多個欄位的診斷資料結構|[SQLGetDiagRec 函式](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|傳回將資料傳送下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|傳送參數資料在執行階段|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|定位資料指標中的資料列集，重新整理此資料列集中，或更新或刪除在結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

