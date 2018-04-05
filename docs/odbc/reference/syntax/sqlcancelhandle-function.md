---
title: SQLCancelHandle 函式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQLCancelHandle
helpviewer_keywords:
- SQLCancelHandle function [ODBC]
ms.assetid: 16049b5b-22a7-4640-9897-c25dd0f19d21
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3760400f23b558c27cd70a3ecd288171cbd56534
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlcancelhandle-function"></a>SQLCancelHandle 函式
**一致性**  
 版本引進了： ODBC 3.8  
  
 標準相容性： 無  
  
 預期的是大多數 ODBC 3.8 （含） 以後的驅動程式會實作此函式。 如果驅動程式不存在，呼叫**SQLCancelHandle**的連接，以處理*處理*參數會傳回 sql_error，其中包含 SQLSTATE 的 IM001 和訊息 '驅動程式不支援此函式' 呼叫若要**SQLCancelHandle**與陳述式，當做處理*處理*參數將會對應至呼叫**SQLCancel**由驅動程式管理員，如果可以處理此驅動程式實作**SQLCancel**。 應用程式可以使用**SQLGetFunctions**決定驅動程式是否支援**SQLCancelHandle**。  
  
 **摘要**  
 **SQLCancelHandle**取消連接或陳述上的處理。 驅動程式管理員會將對應的呼叫**SQLCancelHandle**呼叫**SQLCancel**時*HandleType*為 SQL_HANDLE_STMT。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLCancelHandle(  
      SQLSMALLINT  HandleType,  
      SQLHANDLE    Handle);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]Cacel 處理所在的控制代碼類型。 有效值為利用 SQL_HANDLE_DBC 或 SQL_HANDLE_STMT。  
  
 *Handle*  
 [輸入]要取消處理控制代碼。  
  
 如果*處理*不是有效的控制代碼所指定型別的*HandleType*， **SQLCancelHandle**傳回 SQL_INVALID_HANDLE。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancelHandle**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和陳述式處理*處理*或*HandleType*利用 SQL_HANDLE_DBC 和連接控制代碼的*處理*。  
  
 下表列出通常所傳回的 SQLSTATE 值**SQLCancelHandle** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)引數中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|以非同步方式執行的陳述式相關的函式呼叫其中一個相關聯的陳述式控制代碼*處理*，和*HandleType*已設定為 SQL_HANDLE_DBC。 非同步函式仍執行時**SQLCancelHandle**呼叫。<br /><br /> (DM) *HandleType*引數為 SQL_HANDLE_STMT; 相關聯的連接控制代碼; 上呼叫非同步執行的函式和函式還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**呼叫其中一個相關聯的陳述式控制代碼*處理*和*HandleType*已設定為 SQL_HANDLE_DBC，並傳回 SQL_PARAM_DATA_AVAILABLE。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> **SQLBrowseConnect**針對呼叫*ConnectionHandle*，並傳回 SQL_NEED_DATA。 瀏覽的程序完成之前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY092|屬性/選項識別碼無效|*HandleType*已設定為 SQL_HANDLE_ENV 或 SQL_HANDLE_DESC。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*處理*不支援此函式。|  
  
 如果**SQLCancelHandle**呼叫*HandleType*設定為 SQL_HANDLE_STMT，它會傳回任何函式可以傳回的 SQLSTATE **SQLCancel**。  
  
## <a name="comments"></a>註解  
 此函式是類似於**SQLCancel** ，但可能需要連接或陳述式控制代碼為參數，而不是只有陳述式控制代碼。 驅動程式管理員會將對應的呼叫**SQLCancelHandle**呼叫**SQLCancel**時*HandleType*為 SQL_HANDLE_STMT。 這可讓應用程式使用**SQLCancelHandle**來取消陳述式的作業，即使此驅動程式不會實作**SQLCancelHandle**。  
  
 如需取消陳述式作業的詳細資訊，請參閱[SQLCancel 函數](../../../odbc/reference/syntax/sqlcancel-function.md)。  
  
 如果沒有正在進行中的作業上*處理*呼叫**SQLCancelHandle**沒有任何作用。  
  
 **SQLCancelHandle**連接控制代碼可以取消下列處理類型：  
  
-   函式，連接上以非同步方式執行。  
  
-   函式，另一個執行緒上的連接控制代碼上執行。  
  
 當**SQLCancelHandle**取消連接時，所張貼的診斷記錄中以非同步方式執行的函式呼叫**SQLCancelHandle**附加至所傳回的作業正在已取消;**SQLCancelHandle**不會傳回診斷記錄，不過，當取消另一個執行緒上的連接上執行的函式。  
  
 使用**SQLCancelHandle**取消**SQLEndTran**可能連接置於暫停狀態。 如需有關暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。  
  
> [!NOTE]  
>  如需有關如何使用資訊**SQLCancelHandle**中將部署於 Windows 作業系統比 Windows 7 舊的應用程式，請參閱[相容性比較表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
#### <a name="canceling-connection-related-asynchronous-processing"></a>取消連接相關的非同步處理  
 如果函數傳回 SQL_STILL_EXECUTING，應用程式可以呼叫**SQLCancelHandle**取消作業。 如果取消要求成功， **SQLCancelHandle**都會傳回 SQL_SUCCESS。 這不表示，已取消的原始函數。它會指出已處理取消要求。 驅動程式和資料來源決定時，或在作業取消。 應用程式必須繼續呼叫原始函式，直到傳回的程式碼不是 SQL_STILL_EXECUTING。 如果原始函式已取消，傳回碼是 SQL_ERROR 並 SQLSTATE HY008 （取消作業）。 如果原始函式完成其正常處理 （未取消），傳回碼是 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或 SQL_ERROR，而且 HY008 以外的 SQLSTATE （作業已取消），如果原始函式失敗。  
  
#### <a name="canceling-functions-executing-on-another-thread"></a>取消另一個執行緒上執行的函式  
 在多執行緒應用程式中，應用程式可以取消另一個執行緒執行的作業。 若要取消作業，應用程式會呼叫**SQLCancelHandle**與函式，但不同的執行緒上使用的控制代碼。 驅動程式和作業系統會決定如何在作業取消。 **SQLCancelHandle**傳回程式碼表示驅動程式是否處理要求時，傳回 SQL_SUCCESS 或 SQL_ERROR （不傳回任何診斷的資訊）。 如果原始函式的處理取消時，原始的函式會傳回 SQL_ERROR 並 SQLSTATE HY008 （作業已取消）。  
  
 如果函式正在執行時**SQLCancelHandle**稱為取消函式，另一個執行緒上可能會成功，並傳回 SQL_SUCCESS，[取消] 才會生效函式。 呼叫**SQLCancelHandle**沒有任何作用，如果作業完成之前**SQLCancelHandle**可以取消作業。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|正在取消取消上需要的資料，在陳述式的函式，或取消的陳述式，另一個執行緒上執行的函式的陳述式控制代碼上以非同步方式執行的函式。|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
  
## <a name="see-also"></a>請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [非同步執行 (輪詢方法)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
