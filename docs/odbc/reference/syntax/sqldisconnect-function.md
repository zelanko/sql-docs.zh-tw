---
title: SQL斷開功能 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5ea73919fbe90719d881fb43108ab1934933708
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301148"
---
# <a name="sqldisconnect-function"></a>SQLDisconnect 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLDISCONNECT**將關閉與特定連接句柄關聯的連接。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLDisconnect(  
     SQLHDBC     ConnectionHandle);  
```  
  
## <a name="arguments"></a>引數  
 *連接句柄*  
 [輸入] 連線控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或SQL_STILL_EXECUTING。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDisconnect**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_DBC的*句柄類型*和*連線句柄*。 下表列出了**SQLDISCONNECT**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01002|斷線連線錯誤|斷開連接期間出錯。 但是,斷開連接成功。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08003|連線未開啟|(DM) 參數*ConnectHandle*中指定的連接未打開。|  
|25000|交易狀態無效|在參數*ConnectHandle*指定的連接上存在一個事務。 事務保持活動狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|為*連接句柄*啟用了非同步處理。 調用該函數,並在它fins執行[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)之前在*ConnectHandle*上調用。 然後在*連接處理*上再次調用該函數。<br /><br /> 調用該函數,並在它執行完**SQLCancelHandle**之前從多線程應用程式中的不同線程調用*了 ConnectHandle。*|  
|HY010|函式序列錯誤|(DM) 與*ConnectHandle*關聯的*語句句柄*調用非同步執行函數,並在調用**SQLDISCONNECT**時仍在執行。<br /><br /> (DM) 為*ConnectHandle*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用一個語句句柄,該*語句句柄*與*連接句柄*相關聯並返回SQL_NEED_DATA。 **SQLExecute** **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|連接超時期限在數據源回應請求之前過期,並且連接仍然處於活動狀態。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*連接句柄*關聯的驅動程式不支援該功能。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 如果應用程式在**SQLBrowseConnect**傳回SQL_NEED_DATA後呼叫**SQLDisconnect,** 並在傳回其他返回程式碼之前,驅動程式將取消連接瀏覽過程,並將連接傳回到未連接狀態。  
  
 如果應用程式在與連接句柄關聯的不完整事務時調用**SQLDisconnect,** 驅動程式將返回 SQLSTATE 25000(無效事務狀態),指示事務保持不變,連接處於打開狀態。 不完整的事務是尚未提交或回滾**SQLEndTran**的事務。  
  
 如果應用程式在釋放與連接關聯的所有語句之前調用**SQLDisconnect,** 則驅動程式在成功斷開與數據源的連接後,釋放這些語句和已在連接上顯式分配的所有描述符。 但是,如果與連接關聯的一個或多個語句仍在非同步執行,**則 SQLDisconnect**返回SQL_ERROR SQLSTATE 值為 HY010(函數序列錯誤)。 此外,如果連接處於掛起狀態,或者**SQLCancelHandle**成功取消了**SQLDisconnect,SQLDisconnect**將釋放所有關聯的語句和已在連接上顯式分配**SQLDisconnect**的所有描述符。  
  
 有關應用程式如何使用**SQLDisconnect**的資訊,請參閱[從資料來源或驅動程式斷開連接](../../../odbc/reference/develop-app/disconnecting-from-a-data-source-or-driver.md)。  
  
## <a name="disconnecting-from-a-pooled-connection"></a>斷線與池連線的連線  
 如果為共用環境啟用了連接池,並且應用程式在該環境中的連接上調用**SQLDisconnect,** 則連接將返回到連接池,並且仍然可用於使用相同的共享環境的其他元件。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)[、SQLBrowse 連接函數](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)與[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|配置控點|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|連接到資料來源|[SQLConnect 函數](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|使用連接字串或對話框連接到資料來源|[SQLDriverConnect 函數](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|執行提交或回滾操作|[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|釋放連接句柄|[SQLFreeConnect 函式](../../../odbc/reference/syntax/sqlfreeconnect-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
