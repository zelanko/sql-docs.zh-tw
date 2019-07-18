---
title: 陳述式轉換 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transitioning states [ODBC], statement
- state transitions [ODBC], statement
- statement transitions [ODBC]
ms.assetid: 3d70e0e3-fe83-4b4d-beac-42c82495a05b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b0d46bad2e0b37c5e6751a4895cdf1899aee4b01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070100"
---
# <a name="statement-transitions"></a>陳述式轉換
ODBC 陳述式具有下列狀態。  
  
|State|描述|  
|-----------|-----------------|  
|S0|未配置陳述式。 （C4、 C5 或 C6，必須是連線狀態。 如需詳細資訊，請參閱 <<c0> [ 連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)。)|  
|S1|配置陳述式。|  
|S2|備妥的陳述式。 將會不建立任何結果集。|  
|S3|備妥的陳述式。 將建立 （可能是空的） 的結果集。|  
|S4|建立執行陳述式和任何結果集。|  
|S5|建立執行陳述式和 （可能是空的） 的結果集。 資料指標會開啟並定位在結果集的第一個資料列之前。|  
|S6|游標與放**SQLFetch**或是**SQLFetchScroll**。|  
|S7|游標與放**SQLExtendedFetch**。|  
|S8|函式需要資料。 **SQLParamData**尚未呼叫。|  
|S9|函式需要資料。 **SQLPutData**尚未呼叫。|  
|S10|函式需要資料。 **SQLPutData**已呼叫。|  
|S11|仍在執行中。 陳述式會將數字處於此狀態之後以非同步方式執行的函式會傳回 SQL_STILL_EXECUTING。 陳述式暫時處於此狀態時執行的陳述式控制代碼會接受任何函式。 暫存的居住地處於的狀態資料表以外的任何狀態資料表中不會顯示 S11 **SQLCancel**。 當陳述式暫時處於狀態 S11 時，可以藉由呼叫取消函式**SQLCancel**從另一個執行緒。|  
|S12|取消非同步執行。 S12，在應用程式必須呼叫已取消的函式，直到傳回 SQL_STILL_EXECUTING 以外的值。 只有當函式會傳回 SQL_ERROR SQLSTATE HY008 函式已成功取消 （已取消的作業）。 如果傳回其他值，例如 SQL_SUCCESS，取消作業失敗，並正常執行的函式。|  
  
 狀態 S2 和 S3 稱為備妥狀態，表示透過 S7 S5，資料指標狀態，為需要的資料狀態，表示透過 S10 S8，並指出 S11 和 S12 為非同步狀態。 在每個這些群組中，轉換時，會顯示個別只他們有不同的群組; 中的每個狀態在大部分情況下，每個轉換狀態在每個群組都相同。  
  
 下表顯示每個 ODBC 函數的陳述式狀態影響。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_ENV。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_DBC。  
  
 [3] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_STMT。  
  
 [4] 這個資料列會顯示轉換時*HandleType*已 SQL_HANDLE_DESC。  
  
 [5] 呼叫**SQLAllocHandle**具有*OutputHandlePtr*指向有效的控制代碼會覆寫該控制代碼，而不必考慮先前的內容所處理，而且可能會造成問題，ODBC 驅動程式。 它會呼叫不正確的 ODBC 應用程式開發**SQLAllocHandle**兩次使用相同的應用程式變數定義 *\*OutputHandlePtr*而不需呼叫**SQLFreeHandle**之前它重新配置釋放控制代碼。 覆寫 ODBC 控制代碼的方式可能會導致不一致的行為或部分的 ODBC 驅動程式的錯誤。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect、 SQLConnect 和 SQLDriverConnect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|請參閱下一步 的資料表|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|-[s] S8 [d] S11 [x]|-[s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 [1] S2 [nr] 和 [2] S3 [r] 和 [2] 的 S5 [3] 和 [5] S6 ([3] 或 [4]) 和 [6] S7 [4] 和 [7]|請參閱下一步 的資料表|  
  
 [1] **SQLExecDirect**傳回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**傳回 SQL_NEED_DATA。  
  
 [3] **SQLBulkOperations**傳回 SQL_NEED_DATA。  
  
 [4] **SQLSetPos**傳回 SQL_NEED_DATA。  
  
 [5] **SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**尚未呼叫。  
  
 [6] **SQLFetch**或是**SQLFetchScroll**呼叫。  
  
 [7] **SQLExtendedFetch**呼叫。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel （非同步狀態）  
  
|S11<br /><br /> 仍在執行|S12<br /><br /> 非同步取消|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] 的陳述式是暫時狀態 S11 中，當函式正在執行。 **SQLCancel**已從不同的執行緒呼叫。  
  
 [2] 的陳述式因為處於 S11 非同步呼叫的函式傳回 SQL_STILL_EXECUTING。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|請參閱下一步 的資料表|24000|-[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute （備妥狀態）  
  
|S2<br /><br /> 沒有結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-[s] S11 x|  
  
 [1] *FieldIdentifier*已 SQL_DESC_COUNT。  
  
 [2] *FieldIdentifier*未 SQL_DESC_COUNT。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 q、 SQLTablePrivileges 和 SQLTables  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(KARTRIS)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] [1] S5 [s] 和 [1] S11 [x] 和 [1] 24000 [2]|請參閱下一步 的資料表|HY010|NS [c] HY010 o|  
  
 [1] 目前結果的最後一個或只有結果，或沒有任何目前的結果。 如需有關多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 目前的結果不是最後一個結果。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges、 SQLColumns、 SQLForeignKeys、 SQLGetTypeInfo、 SQLPrimaryKeys、 SQLProcedureColumns、 SQLProcedures、 SQLSpecialColumns、 q、 SQLTablePrivileges 和 SQLTables （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] 這項錯誤會傳回由驅動程式管理員，如果**SQLFetch**或是**SQLFetchScroll**尚未傳回 sql_no_data 之後，如果驅動程式傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] 和 [3] 的 HY010 [o] 或 [4]|  
|IH[2]|HY010|請參閱下一步 的資料表|24000|-[s] S11 x|HY010|NS [c] 和 [3] 的 HY010 [o] 或 [4]|  
  
 [1] 這個資料列會顯示轉換時*SourceDescHandle*引數為 ARD、 APD 或 IPD。  
  
 [2] 這個資料列會顯示轉換時*SourceDescHandle*引數為 IRD。  
  
 [3] *SourceDescHandle*並*TargetDescHandle*引數不在相同**SQLCopyDesc**函式以非同步方式執行。  
  
 [4] 可能*SourceDescHandle*引數或有*TargetDescHandle*引數 （或兩者） 已在不同於**SQLCopyDesc**正在執行的函式以非同步的方式。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc （備妥狀態）  
  
|S2<br /><br /> 沒有結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|24000[1]|-[s] S11 [x]|  
  
 [1]此資料列會顯示轉換時*SourceDescHandle*引數為 IRD。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|請參閱下一步 的資料表|24000|-[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol （備妥狀態）  
  
|S2<br /><br /> 沒有結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|07005|-[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 [1] 呼叫**SQLDisconnect**釋放與連接相關聯的所有陳述式。 此外，這會回到連線狀態 C2;連線狀態必須是 C4 之前的陳述式狀態為 S0。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|-[2] 或 [3] S1 [1]|-[3] S1 [np] 和 （[1] 或 [2]） S1 [p] 和 [1] S2 [p] 和 [2]|-[3] S1 [np] 和 （[1] 或 [2]） S1 [p] 和 [1] S3 [p] 和 [2]|(HY010)|(HY010)|  
  
 [1] *CompletionType*引數是 SQL_COMMIT 並**SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型，傳回 SQL_CB_DELETE 或*CompletionType*引數是 SQL_ROLLBACK 並**SQLGetInfo**傳回 SQL_CB_DELETE SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型。  
  
 [2] *CompletionType*引數是 SQL_COMMIT 並**SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型，傳回 SQL_CB_CLOSE 或*CompletionType*引數是 SQL_ROLLBACK 並**SQLGetInfo**傳回 SQL_CB_CLOSE SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型。  
  
 [3] *CompletionType*引數是 SQL_COMMIT 並**SQLGetInfo** SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型，傳回 SQL_CB_PRESERVE 或*CompletionType*引數是 SQL_ROLLBACK 並**SQLGetInfo**傳回 SQL_CB_PRESERVE SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型。  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(KARTRIS)|S4 [s] 和 [nr] S5 [s] 和 [r] [d] S8 S11 [x]|-[e] [1] S1 [e] 和 [2] S4 [s] 和 [nr] S5 [s] 和 [r] [d] S8 S11 [x]|-[e]，[1]，和 [3] S1 [e]、 [2] 和 [3] S4 [s]，[nr]，和 [3] S5 [s]、 [r]，S8 [3] [d] 和 [3] 的 S11 [x] 和 [3] 24000 [4]|請參閱下一步 的資料表|HY010|NS [c] HY010 [o]|  
  
 [傳回由驅動程式管理員 1] 的錯誤。  
  
 [2] 的錯誤未傳回由驅動程式管理員。  
  
 [3] 目前結果的最後一個或只有結果，或沒有任何目前的結果。 如需有關多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 目前的結果不是最後一個結果。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] 這項錯誤會傳回由驅動程式管理員，如果**SQLFetch**或是**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(KARTRIS)|(HY010)|請參閱下一步 的資料表|S2 [e]，p 及 [1] S4 [s]、 [p]，[nr]，和 [1] S5 [s]、 [p]，[r]，和 [1] S8 [d] [p]，和 [1] S11 [x]，[p]，並為 [1] 24000 [p] 和 [2] HY010 [np]|請參閱 < 資料指標狀態 」 表格|HY010|NS [c] HY010 [o]|  
  
 [1] 目前結果的最後一個或只有結果，或沒有任何目前的結果。 如需有關多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 目前的結果不是最後一個結果。  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute （備妥狀態）  
  
|S2<br /><br /> 沒有結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|S4 [s] [d] S8 S11 [x]|S5 [s] [d] S8 S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p]、 [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] 這項錯誤會傳回由驅動程式管理員，如果**SQLFetch**或是**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|請參閱下一步 的資料表|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 或 [nf] S11 [x]|S1010|-[s] 或 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 和 SQLFetchScroll  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|請參閱下一步 的資料表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch 和 SQLFetchScroll （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 或 [nf] S11 [x]|-[s] 或 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|KARTRIS [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] 這個資料列會顯示轉換時*HandleType* SQL_HANDLE_ENV 或利用 SQL_HANDLE_DBC。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_STMT。  
  
 [3] 這個資料列會顯示轉換時*HandleType* SQL_HANDLE_DESC 並明確配置描述元。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|KARTRIS [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|KARTRIS [2]|--|--|--|--|HY010|HY010|  
  
 [1] 這個資料列會顯示轉換時*選項*已 SQL_CLOSE。  
  
 [2] 這個資料列會顯示轉換時*選項*SQL_UNBIND 或 SQL_RESET_PARAMS。 如果 *選項*引數為 SQL_DROP 與基礎驅動程式的 ODBC 3 *.x*驅動程式，則驅動程式管理員將其對應至呼叫**SQLFreeHandle**具有*HandleType*設定為 SQL_HANDLE_STMT。 如需詳細資訊，請參閱轉換表[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|請參閱下一步 的資料表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] 或 [nf] [x] 24000 [b] HY109 S11 [i]|-[s] 或 [nf] [x] 24000 [b] HY109 S11 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|-[1] 或 [2] HY010 [3]|請參閱下一步 的資料表|-[1] 或 [2] 24000 [3]|-[1]、 [2] 或 [3] S11 [3] 和 [x]|HY010|NS [c] 或 [4] HY010 [o] 和 [5]|  
  
 [1] *DescriptorHandle*引數為 APD 或 ARD。  
  
 [2] *DescriptorHandle*引數為 IPD。  
  
 [3] *DescriptorHandle*引數為 IRD。  
  
 [4] *DescriptorHandle*引數為相同*DescriptorHandle*中的引數**SQLGetDescField**或是**SQLGetDescRec**以非同步方式執行的函式。  
  
 [5] *DescriptorHandle*引數並非*DescriptorHandle*中的引數**SQLGetDescField**或**SQLGetDescRec**正在以非同步方式執行的函式。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 和 SQLGetDescRec （備妥狀態）  
  
|S2<br /><br /> 沒有結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|-[1]、 [2] 或 [3] S11 [2] 和 [x]|-[1]、 [2] 或 [3] S11 [x]|  
  
 [1] *DescriptorHandle*引數為 APD 或 ARD。  
  
 [2] *DescriptorHandle*引數為 IPD。  
  
 [3] *DescriptorHandle*引數為 IRD。 請注意，這些函式一律會傳回 SQL_NO_DATA 處於 S2 時*DescriptorHandle*已 IRD。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] 這個資料列會顯示轉換時*HandleType*為 SQL_HANDLE_ENV、 利用 SQL_HANDLE_DBC 或 SQL_HANDLE_DESC。  
  
 [2] 這個資料列會顯示轉換時*HandleType*已利用 SQL_HANDLE_STMT。  
  
 [3] **SQLGetDiagField**一律會傳回此錯誤時狀態*Sqlgetdiagfield*是 SQL_DIAG_ROW_COUNT。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|請參閱下一步 的資料表|HY010|HY010|  
  
 [1] 的陳述式屬性不是 SQL_ATTR_ROW_NUMBER。  
  
 [2] 的陳述式屬性是 SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|-[1] 或 ([v] 和 [2]) 24000 [b] 和 [2] HY109 [i] 和 [2]|-[i] 或 ([v] 和 [2]) 24000 [b] 和 [2] HY109 [1] 和 [2]|  
  
 [1]*屬性*引數不是 SQL_ATTR_ROW_NUMBER。  
  
 [2]*屬性*引數為 SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(KARTRIS)|--[1]|--[1]|-[s] 和 [2] S1 [nf]，[np]，[4] S2 和 [nf]，[p]，和 [4] S5 [s] 和 [3] S11 [x]|S1 [nf]，[np]，[4] S3 和 [nf]，[p] 和 [4] S4 [s] 和 [2] S5 [s] 和 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 函式一律會傳回 sql_no_data 為止處於此狀態。  
  
 [2] 的下一個結果是使用資料列計數。  
  
 [3] 的下一個結果是結果集。  
  
 [4] 目前的結果會是最後一個結果。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|-[s] S11 [x]|-[s] S11 [x]|-[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|請參閱下一步 的資料表|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData （需要資料狀態）  
  
|S8<br /><br /> 需要的資料|S9<br /><br /> 必須將|S10<br /><br /> 可以將|  
|----------------------|---------------------|---------------------|  
|S1 [e] 和 [1] S2 [e]、 [nr]，和 [2] S3 [e]、 [r]，和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 S9 [3] [d] S11 [x]|HY010|S1 [e] 和 [1] S2 [e]，[nr]，和 [2] S3 [e]、 [r]，和 [2] S4 [s]、 [nr]，和 ([1] 或 [2]) S5 [s]、 [r]，和 ([1] 或 [2]) S5 ([s] 或 [e]) 和 [4] S6 ([s] 或 [e]) 和 [5] S7 ([s] 或 [e]) 和 S9 [3] [d] S11 [x]|  
  
 [1] **SQLExecDirect**傳回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**傳回 SQL_NEED_DATA。  
  
 [3] **SQLSetPos**必須已從狀態 S7 呼叫而傳回 SQL_NEED_DATA。  
  
 [4] **SQLBulkOperations**必須已從狀態 S5 呼叫而傳回 SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或是**SQLBulkOperations**必須已從狀態 S6 呼叫而傳回 SQL_NEED_DATA。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(KARTRIS)|S2 [s] 和 [nr] S3 [s] 和 [r] S11 [x]|-[s] 或 ([e] 和 [1]) S1 [e] 和 [2] S11 [x]|S1 [e] [3] S2 和 [s]、 [nr]，和 [3] S3 [s]、 [r]，和 [3] S11 [x] 和 [3] 24000 [4]|請參閱下一步 的資料表|HY010|NS [c] HY010 [o]|  
  
 [1] 準備失敗以外的原因而驗證陳述式 (SQLSTATE 是 HY009 [無效的引數的值] 或 [HY090 無效的字串或緩衝區長度])。  
  
 [2] 的準備工作失敗時驗證該陳述式 (SQLSTATE 未 HY009 [無效的引數的值] 或 HY090 [無效的字串或緩衝區長度])。  
  
 [3] 目前結果的最後一個或只有結果，或沒有任何目前的結果。 如需有關多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 目前的結果不是最後一個結果。  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|請參閱下一步 的資料表|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData （需要資料狀態）  
  
|S8<br /><br /> 需要的資料|S9<br /><br /> 必須將|S10<br /><br /> 可以將|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 和 [1] S2 [e]、 [nr]，和 [2] S3 [e]、 [r]，和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S10 [s] S11 [x]|-[s] S1 [e] 和 [1] S2 [e]、 [nr]，和 [2] S3 [e]、 [r]，和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] [3] S11 [x] HY011 和 [6]|  
  
 [1] **SQLExecDirect**傳回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**傳回 SQL_NEED_DATA。  
  
 [3] **SQLSetPos**必須已從狀態 S7 呼叫而傳回 SQL_NEED_DATA。  
  
 [4] **SQLBulkOperations**必須已從狀態 S5 呼叫而傳回 SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或是**SQLBulkOperations**必須已從狀態 S6 呼叫而傳回 SQL_NEED_DATA。  
  
 [6] 一或多個呼叫**SQLPutData**的單一參數傳回 SQL_SUCCESS，然後再呼叫**SQLPutData**嘗試，以使用相同的參數*Strlen_or_ind&lt*設定為 SQL_NULL_DATA。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(KARTRIS)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] 這個資料列會顯示轉換時*屬性*連接屬性。 用於轉換的時機*屬性*是陳述式屬性，請參閱陳述式轉換資料表中的**SQLSetStmtAttr**。  
  
 [2]*屬性*引數不是 SQL_ATTR_CURRENT_CATALOG。  
  
 [3]*屬性*引數為 SQL_ATTR_CURRENT_CATALOG。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] 這個資料列會顯示轉換所在*DescriptorHandle*引數是 ARD APD、 IPD，或 (如**SQLSetDescField**) IRD 時*FieldIdentifier*引數是 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。 它會呼叫錯誤**SQLSetDescField** IRD 如時*FieldIdentifier*是任何其他值。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|請參閱下一步 的資料表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos （資料指標狀態）  
  
|S5<br /><br /> 開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-[s] [d] S8 S11 [24000 [b] HY109 x] [i]|-[s] [d] S8 S11 [24000 [b] HY109 x] [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要的資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|  
  
 [1]*屬性*引數不是 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR、 SQL_ATTR_USE_BOOKMARKS、 SQL_ATTR_CURSOR_SCROLLABLE 或 SQL_ATTR_CURSOR_SENSITIVITY。  
  
 [2]*屬性*引數為 SQL_ATTR_CONCURRENCY、 SQL_ATTR_CURSOR_TYPE、 SQL_ATTR_SIMULATE_CURSOR、 SQL_ATTR_USE_BOOKMARKS、 SQL_ATTR_CURSOR_SCROLLABLE，還是 SQL_ATTR_CURSOR_SENSITIVITY。
