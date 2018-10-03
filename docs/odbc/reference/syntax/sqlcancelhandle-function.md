---
title: SQLCancelHandle 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a814b15255a485bf6fbc28ad31d4e789f8482447
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47662116"
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式
**合規性**  
 版本導入： ODBC 3.8  
  
 標準相容性： 無  
  
 我們預期大部分 ODBC 3.8 （和更新版本） 驅動程式會實作此函式。 否則驅動程式，呼叫**SQLCancelHandle**連線，以處理*處理*參數會傳回 sql_error，其中包含 SQLSTATE 的 IM001 和訊息 '驅動程式不支援此函式' 呼叫若要**SQLCancelHandle**陳述式，當做處理*處理*參數將會對應到呼叫**SQLCancel**透過驅動程式管理員，並且如果可以處理此驅動程式會實作**SQLCancel**。 應用程式可以使用**SQLGetFunctions**決定了驅動程式是否支援**SQLCancelHandle**。  
  
 **摘要**  
 **SQLCancelHandle**取消連接或陳述上的處理。 驅動程式管理員會將對應的呼叫**SQLCancelHandle**的呼叫**SQLCancel**時*HandleType*是利用 SQL_HANDLE_STMT。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]Cacel 處理所在的控制代碼型別。 有效值為利用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 [輸入]要取消處理控制代碼。  
  
 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCancelHandle**傳回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancelHandle**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 和陳述式會處理*處理*或是*HandleType*利用 SQL_HANDLE_DBC 和連接控制代碼*處理*。  
  
 下表列出通常所傳回的 SQLSTATE 值**SQLCancelHandle** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)引數中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|以非同步方式執行的陳述式相關函式呼叫的其中一個相關聯的陳述式控制代碼*處理*，並*HandleType*已設定為 SQL_HANDLE_DBC。 非同步函式仍執行時**SQLCancelHandle**呼叫。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT; 上的相關聯的連接控制代碼; 呼叫的非同步執行的函式和函式仍執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對其中一個相關聯的陳述式控制代碼呼叫*處理*並*HandleType*已設定為 SQL_HANDLE_DBC，並傳回 SQL_PARAM_DATA_AVAILABLE。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> **SQLBrowseConnect**針對呼叫*ConnectionHandle*，並傳回 SQL_NEED_DATA。 瀏覽程序完成之前呼叫這個函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY092|屬性/選項識別碼無效|*HandleType*已設定為 SQL_HANDLE_ENV 或 SQL_HANDLE_DESC。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*處理*不支援此函式。|  
  
 如果**SQLCancelHandle**呼叫*HandleType*設定為 SQL_HANDLE_STMT，它會傳回任何函式可以傳回的 SQLSTATE **SQLCancel**。  
  
## <a name="comments"></a>註解  
 此函數很相似**SQLCancel** ，但可能需要為參數，而不是只有陳述式控制代碼的連線或陳述式控制代碼。 驅動程式管理員會將對應的呼叫**SQLCancelHandle**的呼叫**SQLCancel**時*HandleType*是利用 SQL_HANDLE_STMT。 這可讓應用程式以使用**SQLCancelHandle**來取消陳述式的作業，即使此驅動程式不會實作**SQLCancelHandle**。  
  
 如需有關如何取消陳述式作業的詳細資訊，請參閱[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)。  
  
 如果在沒有任何進行中的作業*處理*呼叫**SQLCancelHandle**沒有任何作用。  
  
 **SQLCancelHandle**連接控制代碼可以取消下列類型的處理：  
  
-   函式，連接上以非同步方式執行。  
  
-   連接控制代碼，另一個執行緒上執行的函式。  
  
 當**SQLCancelHandle**若要取消連接時，所張貼的診斷記錄中以非同步方式執行的函式會呼叫**SQLCancelHandle**會附加至所傳回的作業正在已取消;**SQLCancelHandle**不會傳回診斷記錄，不過，當取消另一個執行緒上的連接上執行的函式。  
  
 使用**SQLCancelHandle**取消**SQLEndTran**可能連接置於暫停狀態。 如需有關暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  如需有關如何使用資訊**SQLCancelHandle**中將 Windows 7 比舊版 Windows 作業系統部署的應用程式，請參閱[相容性比較表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>取消連接相關的非同步處理  
 如果函式傳回 SQL_STILL_EXECUTING 時，應用程式可以呼叫**SQLCancelHandle**取消作業。 如果取消要求成功， **SQLCancelHandle**都會傳回 SQL_SUCCESS。 這不表示，已取消原始函式;表示已處理取消要求。 驅動程式和資料來源決定時，或在作業取消。 應用程式必須繼續呼叫原始函式，直到傳回的程式碼不是 SQL_STILL_EXECUTING。 如果原始函式已取消，傳回碼是 SQL_ERROR 並 SQLSTATE HY008 （已取消的作業）。 如果原始函式完成其一般處理 （未取消），傳回碼是 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或 SQL_ERROR，而且以外 HY008 SQLSTATE （作業已取消），如果原始函式失敗。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>取消另一個執行緒上執行的函式  
 在多執行緒應用程式中，應用程式可以取消另一個執行緒執行的作業。 若要取消作業，應用程式會呼叫**SQLCancelHandle**與用於函式，但在不同的執行緒控制代碼。 驅動程式和作業系統判斷取消作業的方式。 **SQLCancelHandle**傳回程式碼會指示驅動程式是否處理要求，然後傳回 SQL_SUCCESS 或 SQL_ERROR （未傳回任何診斷的資訊）。 如果原始函式的處理已取消，原始的函式會傳回 SQL_ERROR，而且 SQLSTATE HY008 （已取消的作業）。  
  
 如果函式正在執行時**SQLCancelHandle**稱為取消函式的另一個執行緒，可能會失敗，傳回 SQL_SUCCESS，取消生效之前的函式。 呼叫**SQLCancelHandle**沒有任何作用，如果作業完成之前**SQLCancelHandle**能夠取消作業。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|正在取消取消需要資料的陳述式中的函式，或取消的陳述式，另一個執行緒上執行的函式的陳述式控制代碼上以非同步方式執行的函式。|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
