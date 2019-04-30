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
manager: craigg
ms.openlocfilehash: f808460a1421a9ab4cb3a76c2810d810b9636b11
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224509"
---
# <a name="connection-transitions"></a>連線轉換
ODBC 連接擁有以下狀態。  
  
|State|描述|  
|-----------|-----------------|  
|C0|未配置的環境，未配置的連接|  
|C1|配置的環境中，未配置的連接|  
|C2|配置環境中，配置連接|  
|C3|連線的函式需要資料|  
|C4|已連線的連線|  
|C5|連線連接，以配置陳述式|  
|C6|已連線的連線，進行中的交易。 可以連接到處於 C6 配置在連接上沒有陳述式。 例如，假設連接是在手動認可模式下，且處於狀態 C4。 如果陳述式會配置，執行 （啟動交易時），並再釋放，交易會維持使用中，但沒有在連接上的任何陳述式。|  
  
 下表顯示每個 ODBC 函數如何影響連接狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> 沒有環境中。|未配置的 C1|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1[1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(IH)[3]|(IH)|(08003)|(08003)|C5|--[5]|--[5]|  
|(IH)[4]|(IH)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 呼叫**SQLAllocHandle**具有*OutputHandlePtr*指向有效的控制代碼會覆寫先前的內容 ofthat 控點，不論該控制代碼和可能會造成問題，ODBC 驅動程式。 它會呼叫不正確的 ODBC 應用程式開發**SQLAllocHandle**兩次使用相同的應用程式變數定義 *\*OutputHandlePtr*而不需呼叫**SQLFreeHandle**之前它重新配置釋放控制代碼。 覆寫 ODBC 控制代碼的方式可能會導致不一致的行為或部分的 ODBC 驅動程式的錯誤。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 C3 [d] [s]|-[d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--[1] C5[2]|  
  
 [1] 的連接已在手動認可模式。  
  
 [2] 的連接處於自動認可模式。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 q、 SQLTablePrivileges 和 SQLTables  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] 的連接已在自動認可模式中，或資料來源未開始交易。  
  
 [2] 的連接在手動認可模式，且資料來源開始交易。  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc、 SQLGetDescField、 SQLGetDescRec、 SQLSetDescField 和 SQLSetDescRec  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|--[1]|--|--|  
  
 [1] 在此狀態下，可供應用程式的描述項會明確配置描述元。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|C4 s -- n[f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--[3]|--[3]|--[3]|--|--|-[4] 或 ([5]、 [6] 和 [8]) C4 [5] 和 [7] C5 [5]、 [6] 和 [9]|  
|(IH)[2]|(IH)|(08003)|(08003)|--|--|C5|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 因為連接不是處於連線狀態，它會受到交易。  
  
 [4] 的 commit 或 rollback 連線失敗。 此函式會在此情況下傳回 SQL_ERROR。  
  
 [5] 的 commit 或 rollback 成功連線。 如果認可或復原，無法在另一個連線，或如果 commit 或 rollback 成功的所有連線，則函數會傳回 SQL_SUCCESS，函數會傳回 SQL_ERROR。  
  
 [6] 時，至少一個連接上配置的陳述式。  
  
 [7] 沒有在連接上配置的任何陳述式。  
  
 [8] 上，連接至少有一個陳述式，有已開啟的資料指標，以及資料來源會保留資料指標，當交易認可或回復時，無論套用哪一個 (取決於是否*CompletionType*已 SQL_認可或 SQL_ROLLBACK）。 如需詳細資訊，請參閱中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 [9] 如果連接已開啟的資料指標所的任何陳述式，認可或回復交易時，已不會保留資料指標。  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect 和 SQLExecute  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2] C6[3]|--|  
  
 [1] 連接處於自動認可模式，並執行的陳述式不是*游標**規格*（例如 SELECT 陳述式），或是在手動認可模式和陳述式連接執行未開始交易。  
  
 [2] 的連接處於自動認可模式，並執行的陳述式已*游標**規格*（例如 SELECT 陳述式）。  
  
 [3] 連線在手動認可模式，且資料來源開始交易。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[2]|(IH)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|C4[5] --[6]|-[7] C4 [5] 和 [8] C5 [6] 和 [8]|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 發生在連接上配置的單獨一個陳述式。  
  
 [6] 沒有在連接上配置的多個陳述式。  
  
 [7] 的連接已在手動認可模式。  
  
 [8] 的連接處於自動認可模式。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|(IH)|(IH)|(IH)|(IH)|--|C5[3] --[4]|  
|(IH)[2]|(IH)|(IH)|(IH)|(IH)|--|--|  
  
 [1] 這個資料列顯示的交易時*選項*引數是 SQL_CLOSE。  
  
 [2] 這個資料列顯示的交易時*選項*引數為 SQL_UNBIND 或 SQL_RESET_PARAMS。  
  
 [3] 的連接已在自動認可模式中，而且沒有資料指標開啟這一個以外的任何陳述式。  
  
 [4] 的連接已在手動認可模式中，或在自動認可模式和至少一個其他陳述式上開啟游標的。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--|--|--|  
  
 [1]*屬性*引數為 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT，SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，或連接屬性已設定的值。  
  
 [2]*屬性*引數已不 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT，SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，，值沒有已設定連線屬性。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)[1]|--|--|--|--|--|--|  
|(IH)[2]|(IH)|--|--|--|--|--|  
|(IH)[3]|(IH)|(IH)|(IH)|(IH)|--|--|  
|(IH)[4]|(IH)|(IH)|(IH)|--|--|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|08003|--|--|--|  
  
 [1]*資訊類型*引數為 SQL_ODBC_VER。  
  
 [2]*資訊類型*引數不是 SQL_ODBC_VER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--[3] C5[1]|  
  
 [1] 連接處於自動認可模式，並呼叫**SQLMoreResults**未初始化的處理結果集的資料指標規格。  
  
 [2] 的連接處於自動認可模式，並呼叫**SQLMoreResults**已初始化處理的結果集的資料指標規格。  
  
 [3] 的連接已在手動認可模式。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--[1] C6[2]|--|  
  
 [1] 的連接已在自動認可模式中，或資料來源未開始交易。  
  
 [2] 的連接在手動認可模式，且資料來源開始交易。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|IH|IH|--[1] 08003[2]|HY010|--[3] 08002[4] HY011[5]|--[3] 08002[4] HY011[5]|-[3] 和 [6] C5 [8] [4] HY011 08002 [5] 或 [7]|  
  
 [1]*屬性*引數不是 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [2]*屬性*引數為 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [3]*屬性*引數不是 SQL_ATTR_ODBC_CURSORS 或 SQL_ATTR_PACKET_SIZE。  
  
 [4]*屬性*引數為 SQL_ATTR_ODBC_CURSORS。  
  
 [5]*屬性*引數為 SQL_ATTR_PACKET_SIZE。  
  
 [6]*屬性*引數不是 SQL_ATTR_AUTOCOMMIT，或有*屬性*引數為 SQL_ATTR_AUTOCOMMIT，以及設定這個屬性未認可的交易。  
  
 [7]*屬性*引數為 SQL_ATTR_TXN_ISOLATION。  
  
 [8]*屬性*引數為 SQL_ATTR_AUTOCOMMIT，以及將此屬性設定認可交易。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>所有其他的 ODBC 函數  
  
|C0<br /><br /> 沒有環境中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(IH)|(IH)|(IH)|(IH)|(IH)|--|--|
