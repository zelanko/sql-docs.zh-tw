---
title: SQLDisconnect 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDisconnect
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDisconnect
helpviewer_keywords:
- SQLDisconnect function [ODBC]
ms.assetid: 9e84a58e-db48-4821-a0cd-5c711fcbe36b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 788ca2eb7cf37314eb7d5386a23f17123f9ccaff
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343005"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函式
**標準**  
 引進的版本:ODBC 1.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLDisconnect**會關閉與特定連接控制碼相關聯的連接。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>引數  
 *ConnectionHandle*  
 [輸入] 連線控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDisconnect**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec 和 HandleType 的  SQL_HANDLE_DBC 和*ConnectionHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。  下表列出**SQLDisconnect**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|說明|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01002|中斷連線錯誤|中斷連線期間發生錯誤。 不過, 中斷連線成功。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|08003|連接未開啟|(DM) 引數*ConnectionHandle*中指定的連接未開啟。|  
|25000|交易狀態無效|引數*ConnectionHandle*所指定的連接上有交易在處理中。 交易會維持使用中狀態。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*ConnectionHandle*的非同步處理。 已呼叫函式, 且在完成執行[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)之前, 已在*ConnectionHandle*上呼叫該函數。 然後在*ConnectionHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 且在完成執行**SQLCancelHandle**之前, 已從多執行緒應用程式中的不同執行緒在*ConnectionHandle*上呼叫該函數。|  
|HY010|函數順序錯誤|(DM) 針對與*ConnectionHandle*相關聯的*StatementHandle*呼叫非同步執行的函式, 且在呼叫**SQLDisconnect**時仍在執行中。<br /><br /> (DM) 已針對*ConnectionHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對與*StatementHandle*相關聯的*ConnectionHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|連接逾時期間已于資料來源回應要求之前過期, 而且連接仍在使用中。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*ConnectionHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時, 就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING, 而且如果啟用通知模式, 則必須在控制碼上呼叫**SQLCompleteAsync** , 才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 如果應用程式在**SQLBrowseConnect**傳回 SQL_NEED_DATA 之後和傳回不同的傳回碼之前呼叫**SQLDisconnect** , 驅動程式會取消連線流覽進程, 並將連接傳回未連線的狀態。  
  
 如果應用程式在有與連接控制碼相關聯的未完成交易時呼叫**SQLDisconnect** , 則驅動程式會傳回 SQLSTATE 25000 (不正確交易狀態), 表示交易未變更, 且連接為斷開. 未完成的交易是指尚未使用**SQLEndTran**認可或回復的交易。  
  
 如果應用程式在釋放與連接相關聯的所有語句之前呼叫**SQLDisconnect** , 驅動程式從資料來源成功中斷連接之後, 會釋出這些語句和所有已明確配置的描述元。在連接上。 不過, 如果與連接相關聯的一或多個語句仍以非同步方式執行, 則**SQLDisconnect**會傳回 SQL_ERROR, 其 SQLSTATE 值為 HY010 (函數序列錯誤)。 此外,  如果連接處於已暫停狀態或已成功取消  **SQLDisconnect, 則 SQLDisconnect 會釋放所有相關聯的語句, 以及已在連接上明確配置的所有描述元。SQLCancelHandle**。  
  
 如需有關應用程式如何使用**SQLDisconnect**的詳細資訊, 請參閱[從資料來源或驅動程式中斷連接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>從共用連線中斷連接  
 如果已針對共用環境啟用連接共用, 且應用程式在該環境的連接上呼叫**SQLDisconnect** , 則會將連接傳回連接集區, 而且仍然可以使用相同共用的其他元件環境.  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)、 [SQLBrowseConnect 函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)和[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置控制碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函式](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用連接字串或對話方塊連接到資料來源|[SQLDriverConnect 函式](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|執行認可或復原作業|[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|釋放連接控制碼|[SQLFreeConnect 函式](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
