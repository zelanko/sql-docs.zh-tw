---
title: 連接轉換 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], connection
- connection transitions [ODBC]
- state transitions [ODBC], connection
ms.assetid: 6b6e1a47-4a52-41c8-bb9e-7ddeae09913e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b59fe86e0fb16dca51d24098c98694e77fa7e82b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32914133"
---
# <a name="connection-transitions"></a>連接轉換
ODBC 連接擁有以下狀態。  
  
|State|Description|  
|-----------|-----------------|  
|C0|未配置的環境中，未配置的連接|  
|C1|配置的環境中，未配置的連接|  
|C2|配置環境中，配置連接|  
|C3|連線函式需要資料|  
|C4|已連線的連線|  
|C5|連接連接，以配置陳述式|  
|C6|已連線的連線，進行中的交易。 很可能在連接上配置的任何陳述式都必須處於 C6 連接。 例如，假設連接是在手動認可模式下，且處於狀態 C4。 如果陳述式會配置，執行 （啟動交易時），並再釋放，交易會維持使用中，但沒有在連接上的任何陳述式。|  
  
 下表顯示每個 ODBC 函數如何影響連接狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> 沒有信封中。|未配置的 C1|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(KARTRIS)[2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
|(KARTRIS)[3]|(KARTRIS)|(08003)|(08003)|C5|--[5]|--[5]|  
|(KARTRIS)[4]|(KARTRIS)|(08003)|(08003)|--[5]|--[5]|--[5]|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 呼叫**SQLAllocHandle**與*OutputHandlePtr*指向有效的控制代碼會覆寫先前內容 ofthat 控制代碼，則不管該控制代碼，可能會造成問題，ODBC 驅動程式。 它是不正確的 ODBC 應用程式開發，呼叫**SQLAllocHandle**兩次以相同的應用程式變數定義 *\*OutputHandlePtr*而不需呼叫**SQLFreeHandle**之前它重新配置釋放控制代碼。 覆寫 ODBC 以此方式的控制代碼可能會導致不一致的行為或內容上的 ODBC 驅動程式的錯誤。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|C4 C3 [d] [s]|-[d] C2 [e] C4 [s]|(08002)|(08002)|(08002)|  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|-[1] C5 [2]|  
  
 [1] 的連接已手動認可模式。  
  
 [2] 的連接處於自動認可模式。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 SQLStatistics、 SQLTablePrivileges 和 SQLTables  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|-[1] C6 [2]|--|  
  
 [1] 的連接處於自動認可模式或資料來源尚未開始交易。  
  
 [2] 的連接在手動認可模式中，而且資料來源開始交易。  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|C4|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc、 SQLGetDescField、 SQLGetDescRec、 SQLSetDescField 和 SQLSetDescRec  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|--[1]|--|--|  
  
 [1] 在此狀態下，可用於應用程式的描述項會明確地配置描述元。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(08003)|C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|C4 s-n [f]|(08002)|(08002)|(08002)|(08002)|  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)[1]|--[3]|--[3]|--[3]|--|--|-[4] 或 ([5]、 [6] 和 [8]) C4 [5] [7] C5 和 [5]、 [6] 和 [9]|  
|(KARTRIS)[2]|(KARTRIS)|(08003)|(08003)|--|--|C5|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 因為連接不是處於連線狀態，所以交易不會受到影響。  
  
 [認可或復原 4]，連線失敗。 函數會在此情況下傳回 SQL_ERROR。  
  
 [認可或復原 5]，已成功在連接上。 如果認可或復原失敗上另一個連接，或如果認可或復原成功的所有連線，則函數會傳回 SQL_SUCCESS，函數會傳回 SQL_ERROR。  
  
 [6] 時，至少一個連接上配置的陳述式。  
  
 [7] 沒有在連接上配置的任何陳述式。  
  
 [8] 的連接至少有一個陳述式，有已開啟的資料指標，和資料來源會保留資料指標時認可或回復交易，較適用於 (取決於是否*CompletionType*已 SQL_認可或 SQL_ROLLBACK）。 如需詳細資訊，請參閱中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 [9] 如果連接已開啟的資料指標是任何陳述式，認可或回復交易時，已不會保留資料指標。  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect 和 SQLExecute  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|-C6 [1] C6 [2] [3]|--|  
  
 [1] 的連接處於自動認可模式，且執行的陳述式不*游標**規格*（例如 SELECT 陳述式）; 或是連接在手動認可模式和陳述式執行尚未開始交易。  
  
 [2] 的連接處於自動認可模式，而執行的陳述式*游標**規格*（例如 SELECT 陳述式）。  
  
 [已在手動認可模式中，3] 的連線和資料來源開始交易。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)[1]|C0|(HY010)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(KARTRIS)[2]|(KARTRIS)|(C1)|(HY010)|(HY010)|(HY010)|(HY010)|  
|(KARTRIS)[3]|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|C4 [5]-[6]|-[7] C4 [5]，[8] C5 [6] 和 [8]|  
|(KARTRIS)[4]|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|--|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 時，在此連接上配置的單獨一個陳述式。  
  
 [6] 沒有在連接上配置的多個陳述式。  
  
 [7] 的連接已手動認可模式。  
  
 [8] 的連接處於自動認可模式。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)[1]|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|C5 [3]-[4]|  
|(KARTRIS)[2]|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|--|  
  
 [1] 這個資料列會顯示交易時*選項*引數是 SQL_CLOSE。  
  
 [2] 這個資料列會顯示交易時*選項*引數是 SQL_UNBIND 或 SQL_RESET_PARAMS。  
  
 [3] 的連接處於自動認可模式下，而沒有資料指標已開啟此以外的任何陳述式。  
  
 [4] 的連接已在手動認可模式中，或在自動認可模式和至少一個其他陳述式上開啟游標的。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|KARTRIS|KARTRIS|--[1] 08003[2]|HY010|--|--|--|  
  
 [1]*屬性*引數是 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，或值已設定連接屬性。  
  
 [2]*屬性*引數不是 SQL_ATTR_ACCESS_MODE、 SQL_ATTR_AUTOCOMMIT、 SQL_ATTR_LOGIN_TIMEOUT、 SQL_ATTR_ODBC_CURSORS、 SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，且值具有未設定連線屬性。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)[1]|--|--|--|--|--|--|  
|(KARTRIS)[2]|(KARTRIS)|--|--|--|--|--|  
|(KARTRIS)[3]|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|--|  
|(KARTRIS)[4]|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|--|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|KARTRIS|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|KARTRIS|KARTRIS|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|KARTRIS|KARTRIS|--[1] 08003[2]|08003|--|--|--|  
  
 [1]*資訊類型*引數以前是 SQL_ODBC_VER。  
  
 [2]*資訊類型*引數不是 SQL_ODBC_VER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|-[1] C6 [2]|-[3] 的 C5 [1]|  
  
 [1] 的連接處於自動認可模式，且呼叫**SQLMoreResults**未初始化的處理結果集的資料指標規格。  
  
 [2] 的連接處於自動認可模式，且呼叫**SQLMoreResults**已初始化處理的結果集的資料指標規格。  
  
 [3] 的連接已手動認可模式。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(08003)|(08003)|--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|-[1] C6 [2]|--|  
  
 [1] 的連接處於自動認可模式或資料來源尚未開始交易。  
  
 [2] 的連接處於手動-認可模式下，且資料來源開始交易。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|KARTRIS|KARTRIS|--[1] 08003[2]|HY010|-[3] 08002 [4] HY011 [5]|-[3] 08002 [4] HY011 [5]|-[3] 和 [6] C5 [8] [4] HY011 08002 [5] 或 [7]|  
  
 [1]*屬性*引數不是 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [2]*屬性*引數是 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [3]*屬性*引數不是 SQL_ATTR_ODBC_CURSORS 或 SQL_ATTR_PACKET_SIZE。  
  
 [4]*屬性*引數以前是 SQL_ATTR_ODBC_CURSORS。  
  
 [5]*屬性*引數以前是 SQL_ATTR_PACKET_SIZE。  
  
 [6]*屬性*引數不是 SQL_ATTR_AUTOCOMMIT，或*屬性*引數為 SQL_ATTR_AUTOCOMMIT，以及設定這個屬性未認可的交易。  
  
 [7]*屬性*引數為 SQL_ATTR_TXN_ISOLATION。  
  
 [8]*屬性*引數為 SQL_ATTR_AUTOCOMMIT，以及將此屬性設定認可的交易。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|--|--|(HY010)|--|--|--|  
  
## <a name="all-other-odbc-functions"></a>其他所有 ODBC 函數  
  
|C0<br /><br /> 沒有信封中。|C1<br /><br /> 未配置|C2<br /><br /> 配置|C3<br /><br /> 需要的資料|C4<br /><br /> 已連接|C5<br /><br /> 引數|C6<br /><br /> Transaction|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|(KARTRIS)|--|--|
