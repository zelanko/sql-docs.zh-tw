---
description: 連線轉換
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5f7fecf0ad25311e9d96f4db8554c1cdbf24e91
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339444"
---
# <a name="connection-transitions"></a>連線轉換
ODBC 連接具有下列狀態。  
  
|State|描述|  
|-----------|-----------------|  
|C0|未配置的環境，未配置的連接|  
|C1|配置的環境，未配置的連接|  
|C2|配置的環境，配置的連接|  
|C3|連接函數需要資料|  
|C4|連接的連接|  
|C5|連接的連接，已配置的語句|  
|C6|連接的連接，進行中的交易。 連接可能會處於狀態 C6，而不會在連接上配置任何語句。 例如，假設連接是在手動認可模式下，且處於狀態 C4。 如果已配置語句、執行 (啟動交易) ，然後釋出，則交易會維持作用中，但連接上沒有任何語句。|  
  
 下表顯示每個 ODBC 函數如何影響連接狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|C0<br /><br /> 沒有 Env。|C1 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|--------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|C1 [1]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
| (IH) [2]|C2|--[5]|--[5]|--[5]|--[5]|--[5]|  
| (IH) [3]| (IH) | (08003) | (08003) |C5|--[5]|--[5]|  
| (IH) [4]| (IH) | (08003) | (08003) |--[5]|--[5]|--[5]|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType* 時，這個資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
 [5] 呼叫 **SQLAllocHandle** 時， *OutputHandlePtr* 指向有效的控制碼會覆寫該控制碼，而不考慮先前的內容 ofthat 控制碼，而且可能會導致 ODBC 驅動程式發生問題。 這是不正確的 ODBC 應用程式設計，可使用針對* \* OutputHandlePtr*定義的相同應用程式變數來呼叫**SQLAllocHandle**兩次，而不需要呼叫**SQLFreeHandle**來釋放控制碼，然後再重新配置。 以這種方式覆寫 ODBC 控制碼可能會導致 ODBC 驅動程式部分的行為不一致或發生錯誤。  
  
## <a name="sqlbrowseconnect"></a>SQLBrowseConnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) |C3 [d] C4 [s]|--[d] C2 [e] C4 [s]| (08002) | (08002) | (08002) |  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) | (IH) |--|--[1] C5 [2]|  
  
 [1] 連接處於手動認可模式。  
  
 [2] 連接處於自動認可模式。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、SQLPrimaryKeys、SQLProcedureColumns、SQLProcedures、SQLSpecialColumns、SQLStatistics、SQLTablePrivileges 和 SQLTables  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) | (IH) |--[1] C6 [2]|--|  
  
 [1] 連接處於自動認可模式，或資料來源未開始交易。  
  
 [2] 連接處於手動認可模式，且資料來源已開始交易。  
  
## <a name="sqlconnect"></a>SQLConnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) |C4| (08002) | (08002) | (08002) | (08002) |  
  
## <a name="sqlcopydesc-sqlgetdescfield-sqlgetdescrec-sqlsetdescfield-and-sqlsetdescrec"></a>SQLCopyDesc、SQLGetDescField、SQLGetDescRec、SQLSetDescField 和 SQLSetDescRec  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) |--[1]|--|--|  
  
 [1] 在此狀態下，應用程式唯一可用的描述項是明確配置的描述項。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) |--|--|--|--|--|--|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (08003) |C2|C2|C2|25000|  
  
## <a name="sqldriverconnect"></a>SQLDriverConnect  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) |C4 s--n [f]| (08002) | (08002) | (08002) | (08002) |  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) [1]|--[3]|--[3]|--[3]|--|--|--[4] 或 ( [5]、[6] 和 [8] ) C4 [5] 和 [7] C5 [5]、[6] 和 [9]|  
| (IH) [2]| (IH) | (08003) | (08003) |--|--|C5|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 因為連接未處於連接狀態，所以不會受到交易的影響。  
  
 [4] 連接上的認可或復原失敗。 在此情況下，函數會傳回 SQL_ERROR。  
  
 [5] 連接成功認可或回復。 如果另一個連接上的 commit 或 rollback 失敗，函數會傳回 SQL_ERROR，否則如果在所有連接上成功認可或回復，則函式會傳回 SQL_SUCCESS。  
  
 [6] 連接上至少配置了一個語句。  
  
 [7] 連接上沒有配置任何語句。  
  
 [8] 連接至少有一個語句，其中有一個開啟的資料指標，而資料來源會在認可或回復交易時保留資料指標，視何者套用 (取決於 *CompletionType* 是否 SQL_COMMIT 或 SQL_ROLLBACK) 。 如需詳細資訊，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)中的 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 屬性。  
  
 [9] 如果連接的任何語句都有開啟的資料指標，則在認可或回復交易時，不會保留資料指標。  
  
## <a name="sqlexecdirect-and-sqlexecute"></a>SQLExecDirect 和 SQLExecute  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) | (IH) |--[1] C6 [2] C6 [3]|--|  
  
 [1] 連接處於自動認可模式，而執行的語句不是資料*指標**規格* (例如 SELECT 語句) ;或連接處於手動認可模式，而執行的語句並未開始交易。  
  
 [2] 連接處於自動認可模式，而執行的語句是資料*指標**規格* (例如 SELECT 語句) 。  
  
 [3] 連接處於手動認可模式，且資料來源已開始交易。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) [1]|C0| (HY010) | (HY010) | (HY010) | (HY010) | (HY010) |  
| (IH) [2]| (IH) | (C1) | (HY010) | (HY010) | (HY010) | (HY010) |  
| (IH) [3]| (IH) | (IH) | (IH) | (IH) |C4 [5]--[6]|--[7] C4 [5] 和 [8] C5 [6] 和 [8]|  
| (IH) [4]| (IH) | (IH) | (IH) |--|--|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType* 時，這個資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
 [5] 連接上只配置了一個語句。  
  
 [6] 在連接上配置了多個語句。  
  
 [7] 連接處於手動認可模式。  
  
 [8] 連接處於自動認可模式。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) [1]| (IH) | (IH) | (IH) | (IH) |--|C5 [3]--[4]|  
| (IH) [2]| (IH) | (IH) | (IH) | (IH) |--|--|  
  
 [1] 當 *選項* 引數 SQL_CLOSE 時，此資料列會顯示交易。  
  
 [2] 當 *Option* 引數 SQL_UNBIND 或 SQL_RESET_PARAMS 時，此資料列會顯示交易。  
  
 [3] 連線處於自動認可模式，且除了此資料指標以外的任何語句都未開啟任何資料指標。  
  
 [4] 連接處於手動認可模式，或處於自動認可模式，且至少有一個其他語句開啟了資料指標。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003 [2]|HY010|--|--|--|  
  
 [1] *屬性* 引數已 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE，或已設定連接屬性的值。  
  
 [2] 未 SQL_ATTR_ACCESS_MODE、SQL_ATTR_AUTOCOMMIT、SQL_ATTR_LOGIN_TIMEOUT、SQL_ATTR_ODBC_CURSORS、SQL_ATTR_TRACE 或 SQL_ATTR_TRACEFILE 的 *屬性* 引數，而且尚未設定連接屬性的值。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) [1]|--|--|--|--|--|--|  
| (IH) [2]| (IH) |--|--|--|--|--|  
| (IH) [3]| (IH) | (IH) | (IH) | (IH) |--|--|  
| (IH) [4]| (IH) | (IH) | (IH) |--|--|--|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType* 時，這個資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType* 時，這個資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType* 時，這個資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType* 時，這個資料列會顯示轉換。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|HY010|HY010|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003 [2]|08003|--|--|--|  
  
 [1] *InfoType* 引數已 SQL_ODBC_VER。  
  
 [2] 未 SQL_ODBC_VER *InfoType* 引數。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) | (IH) |--[1] C6 [2]|--[3] C5 [1]|  
  
 [1] 連接處於自動認可模式，而 **SQLMoreResults** 的呼叫尚未初始化資料指標規格之結果集的處理。  
  
 [2] 連接處於自動認可模式，而 **SQLMoreResults** 的呼叫已初始化資料指標規格的結果集處理。  
  
 [3] 連接處於手動認可模式。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (08003) | (08003) |--|--|--|  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) | (IH) |--[1] C6 [2]|--|  
  
 [1] 連接處於自動認可模式，或資料來源未開始交易。  
  
 [2] 連接處於手動認可模式，且資料來源已開始交易。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
|Ih|Ih|--[1] 08003 [2]|HY010|--[3] 08002 [4] HY011 [5]|--[3] 08002 [4] HY011 [5]|--[3] 和 [6] C5 [8] 08002 [4] HY011 [5] 或 [7]|  
  
 [1] 未 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION *屬性* 引數。  
  
 [2] *屬性* 引數是 SQL_ATTR_TRANSLATE_LIB 或 SQL_ATTR_TRANSLATE_OPTION。  
  
 [3] 未 SQL_ATTR_ODBC_CURSORS 或 SQL_ATTR_PACKET_SIZE *屬性* 引數。  
  
 [4] *屬性* 引數已 SQL_ATTR_ODBC_CURSORS。  
  
 [5] *屬性* 引數已 SQL_ATTR_PACKET_SIZE。  
  
 [6] 未 SQL_ATTR_AUTOCOMMIT *屬性* 引數，或已 SQL_ATTR_AUTOCOMMIT *屬性* 引數，且設定這個屬性未認可交易。  
  
 [7] *屬性* 引數已 SQL_ATTR_TXN_ISOLATION。  
  
 [8] *屬性* 引數已 SQL_ATTR_AUTOCOMMIT，並設定此屬性認可交易。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) |--|--| (HY010) |--|--|--|  
  
## <a name="all-other-odbc-functions"></a>所有其他 ODBC 函數  
  
|C0<br /><br /> 沒有 Env。|C1<br /><br /> 未配置|C2<br /><br /> 已配置|C3<br /><br /> 需要資料|C4<br /><br /> 連線|C5<br /><br /> 引數|C6<br /><br /> 交易|  
|--------------------|------------------------|----------------------|----------------------|----------------------|----------------------|------------------------|  
| (IH) | (IH) | (IH) | (IH) | (IH) |--|--|
