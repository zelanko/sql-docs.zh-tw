---
title: 連接轉換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00ebbe36f8668e83697ff3a0038fbeb38f23ffd2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019195"
---
# <a name="connection-transitions"></a>連線轉換
ODBC 連接具有下列狀態。  
  
|State|描述|  
|-----------|-----------------|  
|C0|未配置的環境，未配置的連接|  
|C1|配置的環境，未配置的連接|  
|C2|配置的環境，配置的連接|  
|C3|連接功能需要資料|  
|C4|連接的連線|  
|C5|連接的連接，配置的語句|  
|C6|連線的連接，進行中的交易。 連接可能會在狀態 C6 中，而不會在連接上配置任何語句。 例如，假設連線處於手動認可模式，且處於狀態 C4。 如果語句已配置、執行（啟動交易），然後釋出，則交易會保持作用中，但不會有任何語句在連接上。|  
  
 下表顯示每個 ODBC 函數如何影響連接狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> 沒有 Env。|C1 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)2|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)第|(IH)|（08003）|（08003）|C5|--[5]|--[5]|  
|(IH)4gb|(IH)|（08003）|（08003）|--[5]|--[5]|--[5]|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType*時，此資料列會顯示轉換。  
  
 [5] 以指向有效控制碼的*OutputHandlePtr*呼叫**SQLAllocHandle**時，會覆寫該控制碼，而不考慮先前的內容 ofthat 控制碼，而且可能會造成 ODBC 驅動程式的問題。 不正確的 ODBC 應用程式設計會呼叫**SQLAllocHandle**兩次，並針對* \*OutputHandlePtr*所定義的相同應用程式變數，而不需要呼叫**SQLFreeHandle**來釋放控制碼，然後再重新配置。 以這種方式覆寫 ODBC 控制碼，可能會導致 ODBC 驅動程式不一致的行為或錯誤。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C3 [d] C4 [s]|--[d] C2 [e] C4 [s]|（08002）|（08002）|（08002）|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5 [2]|  
  
 [1] 連接處於手動認可模式。  
  
 [2] 連接處於自動認可模式。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、SQLPrimaryKeys、SQLProcedureColumns、SQLProcedures、SQLSpecialColumns、SQLStatistics、SQLTablePrivileges 和 SQLTables  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6 [2]|--|  
  
 [1] 連接處於自動認可模式，或資料來源未開始交易。  
  
 [2] 連接在手動認可模式下，且資料來源開始交易。  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|（08002）|（08002）|（08002）|（08002）|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc、SQLGetDescField、SQLGetDescRec、SQLSetDescField 和 SQLSetDescRec  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] 在此狀態中，應用程式可用的唯一描述項是明確配置的描述元。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|（08003）|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s--n [f]|（08002）|（08002）|（08002）|（08002）|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)sha-1|--[3]|--[3]|--[3]|--|--|--[4] 或（[5]，[6]，和 [8]） C4 [5] 和 [7] C5 [5]，[6]，和 [9]|  
|(IH)2|(IH)|（08003）|（08003）|--|--|C5|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 因為連接不是處於已線上狀態，所以不會受到交易的影響。  
  
 [4] 連接上的認可或復原失敗。 在此情況下，函數會傳回 SQL_ERROR。  
  
 [5] 連接上的認可或復原成功。 如果認可或復原在另一個連接上失敗，此函式會傳回 SQL_ERROR; 如果在所有連接上成功認可或復原，此函數會傳回 SQL_SUCCESS。  
  
 [6] 連接上至少有一個已配置的語句。  
  
 [7] 連接上沒有配置任何語句。  
  
 [8] 連接至少有一個語句，其中有一個開啟的資料指標，而資料來源會在認可或回復交易時保留游標，視何者而定（取決於*CompletionType*是否 SQL_COMMIT 或 SQL_ROLLBACK）。 如需詳細資訊，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性。  
  
 [9] 如果連接有任何已開啟資料指標的語句，則在認可或回復交易時，不會保留資料指標。  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect 和 SQLExecute  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6 [2] C6 [3]|--|  
  
 [1] 連接處於自動認可模式，而執行的語句不是資料*指標**規格*（例如 SELECT 語句）;或是連接處於手動認可模式，而執行的語句並未開始交易。  
  
 [2] 連接處於自動認可模式，而執行的語句是資料*指標**規格*（例如 SELECT 語句）。  
  
 [3] 連接在手動認可模式下，且資料來源開始交易。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)sha-1|C0|HY010|HY010|HY010|HY010|HY010|  
|(IH)2|(IH)|C1|HY010|HY010|HY010|HY010|  
|(IH)第|(IH)|(IH)|(IH)|(IH)|C4 [5]--[6]|--[7] C4 [5] 和 [8] C5 [6] 和 [8]|  
|(IH)4gb|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType*時，此資料列會顯示轉換。  
  
 [5] 連接上只有一個已配置的語句。  
  
 [6] 連接上已配置多個語句。  
  
 [7] 連接處於手動認可模式。  
  
 [8] 連接處於自動認可模式。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)sha-1|(IH)|(IH)|(IH)|(IH)|--|C5 [3]--[4]|  
|(IH)2|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] 當 SQL_CLOSE*選項*引數時，此資料列會顯示交易。  
  
 [2] 當*Option*引數 SQL_UNBIND 或 SQL_RESET_PARAMS 時，此資料列會顯示交易。  
  
 [3] 連接處於自動認可模式，而且沒有任何資料指標在此例外的語句中開啟。  
  
 [4] 連接處於手動認可模式，或處於自動認可模式，而且至少有一個其他語句已開啟資料指標。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003 [2]|HY010|--|--|--|  
  
 [1]*屬性*引數已 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，或已設定連接屬性的值。  
  
 [2]*屬性*引數不是 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，而且尚未設定連接屬性的值。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)sha-1|--|--|--|--|--|--|  
|(IH)2|(IH)|--|--|--|--|--|  
|(IH)第|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)4gb|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType*時，此資料列會顯示轉換。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003 [2]|08003|--|--|--|  
  
 [1] *InfoType*引數已 SQL_ODBC_VER。  
  
 [2] 未 SQL_ODBC_VER *InfoType*引數。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6 [2]|--[3] C5 [1]|  
  
 [1] 連接處於自動認可模式，而且對**SQLMoreResults**的呼叫尚未初始化資料指標規格結果集的處理。  
  
 [2] 連接處於自動認可模式，而且對**SQLMoreResults**的呼叫已初始化資料指標規格結果集的處理。  
  
 [3] 連接處於手動認可模式。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|（08003）|（08003）|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6 [2]|--|  
  
 [1] 連接處於自動認可模式，或資料來源未開始交易。  
  
 [2] 連接在手動認可模式下，且資料來源開始交易。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003 [2]|HY010|--[3] 08002 [4] HY011 [5]|--[3] 08002 [4] HY011 [5]|--[3] 和 [6] C5 [8] 08002 [4] HY011 [5] 或 [7]|  
  
 [1]*屬性*引數不 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [2]*屬性*引數已 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [3]*屬性*引數不 SQL_ATTR_ODBC_CURSORS 或 SQL_ATTR_PACKET_SIZE。  
  
 [4]*屬性*引數已 SQL_ATTR_ODBC_CURSORS。  
  
 [5]*屬性*引數已 SQL_ATTR_PACKET_SIZE。  
  
 [6] 未 SQL_ATTR_AUTOCOMMIT*屬性*引數，或*屬性*引數已 SQL_ATTR_AUTOCOMMIT，而且設定此屬性未認可交易。  
  
 [7]*屬性*引數已 SQL_ATTR_TXN_ISOLATION。  
  
 [8]*屬性*引數已 SQL_ATTR_AUTOCOMMIT，且設定此屬性已認可交易。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|HY010|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函數  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
