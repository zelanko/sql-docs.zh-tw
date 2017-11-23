---
title: "SQLDisconnect 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLDisconnect
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDisconnect
helpviewer_keywords: SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
caps.latest.revision: "31"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ad106e27956217ba2afa0960d094a7bb7243d07
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLDisconnect**關閉與特定連接控制代碼相關聯的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDisconnect**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_DBC 和*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDisconnect** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01002|中斷連線錯誤|中斷連接時發生錯誤。 不過，已成功中斷連接。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連線。|(DM) 引數中指定的連接*ConnectionHandle*未開啟。|  
|25000|交易狀態無效|發生在引數所指定的連接上的處理序中的交易*ConnectionHandle*。 交易會維持使用中。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*ConnectionHandle*。 呼叫此函式，以及它之前已經執行[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*。 上一次呼叫函式則*ConnectionHandle*。<br /><br /> 呼叫此函式，以及前完成執行**SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒在多執行緒應用程式。|  
|HY010|函數順序錯誤|以非同步方式執行的函式的呼叫 (DM) *StatementHandle*與相關聯*ConnectionHandle*還在執行時和**SQLDisconnect**已呼叫。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *ConnectionHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*聯*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求，且仍在作用中連接。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 如果應用程式呼叫**SQLDisconnect**之後**SQLBrowseConnect**傳回 SQL_NEED_DATA，它會傳回不同的傳回程式碼之前，驅動程式會取消瀏覽處理序的連接，並傳回未連接狀態連線。  
  
 如果應用程式呼叫**SQLDisconnect**不完整的交易與連接控制代碼相關聯時，驅動程式會傳回 SQLSTATE 25000 （無效的交易狀態），指出交易不變和連接為開啟。 不完整的交易是指尚未認可或回復與**SQLEndTran**。  
  
 如果應用程式呼叫**SQLDisconnect**它已經釋放與連接相關聯的所有陳述式之前，驅動程式，已成功中斷連接資料來源之後會釋出這些陳述式和所有已的描述元明確配置在連接上。 不過，如果一或多個與連接相關聯的陳述式會仍然以非同步方式執行， **SQLDisconnect** SQLSTATE HY010 的值會傳回 SQL_ERROR （函數順序錯誤）。 此外， **SQLDisconnect**會釋放所有相關聯的陳述式和所有已明確配置連接，如果連接處於暫停狀態或者的描述元**SQLDisconnect**已已成功取消**SQLCancelHandle**。  
  
 如需有關如何使用應用程式資訊**SQLDisconnect**，請參閱[中斷資料來源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>從共用的連接中斷連接  
 如果連接共用已啟用共用的環境，而且應用程式呼叫**SQLDisconnect**該環境中的連接，連接傳回連接集區且上仍可使用其他元件共用相同的環境。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)，和[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|執行認可或復原作業|[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|釋放連接控制代碼|[SQLFreeConnect 函式](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>請參閱＜  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
