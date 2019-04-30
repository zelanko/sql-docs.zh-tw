---
title: SQLDisconnect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61e32c11aafeaf693188a96b48ddd60728ba5bc4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061456"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLDisconnect**關閉與特定的連接控制代碼相關聯的連接。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入]連接控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDisconnect**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_DBC 並*處理*的*ConnectionHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDisconnect** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01002|中斷連線時發生錯誤|中斷連線時發生錯誤。 不過，中斷連線成功。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08003|未開啟連接|(DM) 引數中指定的連接*ConnectionHandle*並未開啟。|  
|25000|交易狀態無效|沒有引數所指定的連接上的處理序中的交易*ConnectionHandle*。 交易會維持使用中。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*ConnectionHandle*。 呼叫函式，並已執行前[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)上呼叫*ConnectionHandle*。 然後在上一次呼叫函式*ConnectionHandle*。<br /><br /> 呼叫函式，並完成執行之前**SQLCancelHandle**上呼叫*ConnectionHandle*從不同的執行緒，多執行緒應用程式中。|  
|HY010|函數順序錯誤|(DM) 的呼叫以非同步方式執行的函式*StatementHandle*聯*ConnectionHandle*仍執行時並**SQLDisconnect**已呼叫。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *ConnectionHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*相關聯*ConnectionHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求，且連線是仍在作用中。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*ConnectionHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 如果應用程式呼叫**SQLDisconnect**之後**SQLBrowseConnect**會傳回 SQL_NEED_DATA，而且它會傳回不同的傳回碼之前，驅動程式取消瀏覽處理序的連接，並傳回未連接狀態連線。  
  
 如果應用程式呼叫**SQLDisconnect**連接控制代碼相關聯的交易未完成時，驅動程式會傳回 SQLSTATE 25000 （無效的交易狀態），指出交易不變和連接已開啟。 不完整的交易是指尚未認可或回復使用**SQLEndTran**。  
  
 如果應用程式呼叫**SQLDisconnect**它已經釋放與連接相關聯的所有陳述式之前，驅動程式，已成功中斷連接資料來源之後會釋出這些陳述式和所有的描述項，已建立明確配置在連接上。 不過，如果一或多個與連接相關聯的陳述式仍在執行非同步**SQLDisconnect** SQLSTATE HY010 值會傳回 SQL_ERROR （函數順序錯誤）。 此外， **SQLDisconnect**會釋放所有相關聯的陳述式和所有的描述項，已明確配置的連接上，如果連接處於暫停狀態或者**SQLDisconnect**已已成功取消**SQLCancelHandle**。  
  
 如需有關如何使用應用程式資訊**SQLDisconnect**，請參閱[中斷資料來源或驅動程式](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>共用的連接與中斷連線  
 如果連接共用已啟用共用的環境，而且應用程式呼叫**SQLDisconnect**在該環境中連接之後，連接傳回連接集區並仍可使用其他元件相同的共用的環境中。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)， [SQLBrowseConnect 函式](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)，並[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|連接到資料來源使用的連接字串或對話方塊方塊|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|執行認可或復原作業|[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|釋放連接控制代碼|[SQLFreeConnect 函式](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
