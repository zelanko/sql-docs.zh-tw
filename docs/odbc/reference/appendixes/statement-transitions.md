---
title: 語句轉換 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070100"
---
# <a name="statement-transitions"></a>陳述式轉換
ODBC 語句具有下列狀態。  
  
|State|描述|  
|-----------|-----------------|  
|S0|未配置的語句。 （連接狀態必須是 C4、C5 或 C6。 如需詳細資訊，請參閱[連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)）。|  
|S1|已配置的語句。|  
|S2|備妥的語句。 將不會建立任何結果集。|  
|S3|備妥的語句。 將會建立一個（可能是空的）結果集。|  
|S4|已執行語句，但未建立任何結果集。|  
|S5|已執行語句，並已建立（可能是空的）結果集。 資料指標是開啟的，並且位於結果集的第一個資料列之前。|  
|S6|游標位於**SQLFetch**或**SQLFetchScroll**。|  
|S7|游標位於**SQLExtendedFetch**。|  
|S8|函數需要資料。 尚未呼叫**SQLParamData** 。|  
|S9|函數需要資料。 尚未呼叫**SQLPutData** 。|  
|S10|函數需要資料。 已呼叫**SQLPutData** 。|  
|S11|仍在執行中。 在以非同步方式執行的函式傳回 SQL_STILL_EXECUTING 之後，語句會保留在此狀態。 當任何接受語句控制碼的函數正在執行時，語句會暫時處於此狀態。 狀態 S11 中的暫時居住不會顯示在**SQLCancel**的狀態資料表以外的任何狀態資料表中。 當語句暫時處於狀態 S11 時，可以從另一個執行緒呼叫**SQLCancel**來取消該函式。|  
|S12|已取消非同步執行。 在 S12 中，應用程式必須呼叫已取消的函式，直到它傳回 SQL_STILL_EXECUTING 以外的值。 只有在函式傳回 SQL_ERROR 和 SQLSTATE HY008 （作業已取消）時，才會成功取消函式。 如果傳回任何其他值（例如 SQL_SUCCESS），取消作業就會失敗，且函式會正常執行。|  
  
 狀態 S2 和 S3 稱為「備妥」狀態，會以資料指標狀態來指示 S5 至 S7，並將 S8 到 S10 做為「需要」資料狀態，並將 S11 和 S12 狀態視為非同步狀態。 在上述每個群組中，只有當群組中的每個狀態不同時，才會分別顯示轉換;在大部分情況下，每個群組中每個狀態的轉換都相同。  
  
 下表顯示每個 ODBC 函數如何影響語句的狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]，[5]，[6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2]，[5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1 [3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4]，[5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] 當 SQL_HANDLE_ENV *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [3] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [4] 當 SQL_HANDLE_DESC *HandleType*時，此資料列會顯示轉換。  
  
 [5] 以指向有效控制碼的*OutputHandlePtr*呼叫**SQLAllocHandle**時，會覆寫該控制碼，而不考慮先前在該控制碼中的內容，而且可能會造成 ODBC 驅動程式的問題。 不正確的 ODBC 應用程式設計會呼叫**SQLAllocHandle**兩次，並針對* \*OutputHandlePtr*所定義的相同應用程式變數，而不需要呼叫**SQLFreeHandle**來釋放控制碼，然後再重新配置。 以這種方式覆寫 ODBC 控制碼可能會導致 ODBC 驅動程式不一致的行為或錯誤。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowseConnect、SQLConnect 和 SQLDriverConnect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|查看下一個資料表|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulkOperations （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[s] S8 [d] S11 [x]|--[s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|S1 [1] S2 [nr] 和 [2] S3 [r] 和 [2] S5 [3] 和 [5] S6 （[3] 或 [4]）和 [6] S7 [4] 和 [7]|查看下一個資料表|  
  
 [1] **SQLExecDirect**傳回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**傳回 SQL_NEED_DATA。  
  
 [3] **SQLBulkOperations**傳回 SQL_NEED_DATA。  
  
 [4] **SQLSetPos**傳回 SQL_NEED_DATA。  
  
 [5] 尚未呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLExtendedFetch** 。  
  
 已呼叫 [6] **SQLFetch**或**SQLFetchScroll** 。  
  
 [7] 已呼叫**SQLExtendedFetch** 。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQLCancel （非同步狀態）  
  
|S11<br /><br /> 仍在執行|S12<br /><br /> 非同步已取消|  
|-----------------------------|-----------------------------|  
|NS [1] S12 [2]|S12|  
  
 [1] 在執行函式時，語句暫時在狀態 S11 中。 **SQLCancel**是從不同的執行緒呼叫。  
  
 [2] 語句在狀態 S11 中，因為以非同步方式呼叫的函式會 SQL_STILL_EXECUTING 傳回。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|查看下一個資料表|24000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLColAttribute （已備妥的狀態）  
  
|S2<br /><br /> 沒有任何結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1] 07005 [2]|--[s] S11 x|  
  
 [1] *FieldIdentifier*已 SQL_DESC_COUNT。  
  
 [2] *FieldIdentifier*不 SQL_DESC_COUNT。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、SQLPrimaryKeys、SQLProcedureColumns、SQLProcedures、SQLSpecialColumns、SQLStatistics、SQLTablePrivileges 和 SQLTables  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] 和 [1] S5 [s] 和 [1] S11 [x] 和 [1] 24000 [2]|查看下一個資料表|HY010|NS [c] HY010 o|  
  
 [1] 目前的結果是最後一個或唯一的結果，或沒有目前的結果。 如需多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 目前的結果不是最後一個結果。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumnPrivileges、SQLColumns、SQLForeignKeys、SQLGetTypeInfo、SQLPrimaryKeys、SQLProcedureColumns、SQLProcedures、SQLSpecialColumns、SQLStatistics、SQLTablePrivileges 和 SQLTables （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
|IH [2]|HY010|查看下一個資料表|24000|--[s] S11 x|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
  
 [1] 當*SourceDescHandle*引數為 ARD、APD 或 IPD 時，此資料列會顯示轉換。  
  
 [2] 當*SourceDescHandle*引數為 IRD 時，此資料列會顯示轉換。  
  
 [3] *SourceDescHandle*和*TargetDescHandle*引數與以非同步方式執行的**SQLCopyDesc**函式中的相同。  
  
 [4] *SourceDescHandle*引數或*TargetDescHandle*引數（或兩者）不同于以非同步方式執行的**SQLCopyDesc**函數。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc （已備妥的狀態）  
  
|S2<br /><br /> 沒有任何結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|24000 [1]|--[s] S11 [x]|  
  
 sha-1當*SourceDescHandle*引數為 IRD 時，此資料列會顯示轉換。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLDataSources 和 SQLDrivers  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|查看下一個資料表|24000|--[s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol （已備妥的狀態）  
  
|S2<br /><br /> 沒有任何結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|07005|--[s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQLDisconnect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0 [1]|S0 [1]|S0 [1]|S0 [1]|HY010|HY010|  
  
 [1] 呼叫**SQLDisconnect**會釋出與連接相關聯的所有語句。 此外，這會將連接狀態傳回 C2。在語句狀態為 S0 之前，連接狀態必須是 C4。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] 或 [3] S1 [1]|--[3] S1 [np] 和（[1] 或 [2]） S1 [p] 和 [1] S2 [p] 和 [2]|--[3] S1 [np] 和（[1] 或 [2]） S1 [p] 和 [1] S3 [p] 和 [2]|HY010|HY010|  
  
 [1] *CompletionType*引數是 SQL_COMMIT， **SQLGetInfo**會傳回 SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型的 SQL_CB_DELETE，或者*CompletionType*引數是 SQL_ROLLBACK，而**SQLGetInfo**會針對 SQL_CB_DELETE 資訊類型傳回 SQL_CURSOR_ROLLBACK_BEHAVIOR。  
  
 [2] *CompletionType*引數是 SQL_COMMIT，而**SQLGetInfo**會傳回 SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型的 SQL_CB_CLOSE，或*CompletionType*引數是 SQL_ROLLBACK，而**SQLGetInfo**會針對 SQL_CB_CLOSE 資訊類型傳回 SQL_CURSOR_ROLLBACK_BEHAVIOR。  
  
 [3] *CompletionType*引數是 SQL_COMMIT，而**SQLGetInfo**會傳回 SQL_CURSOR_COMMIT_BEHAVIOR 資訊類型的 SQL_CB_PRESERVE，或*CompletionType*引數是 SQL_ROLLBACK，而**SQLGetInfo**會針對 SQL_CB_PRESERVE 資訊類型傳回 SQL_CURSOR_ROLLBACK_BEHAVIOR。  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] 和 [nr] S5 [s] 和 [r] S8 [d] S11 [x]|--[e] 和 [1] S1 [e] 和 [2] S4 [s] 和 [nr] S5 [s] 和 [r] S8 [d] S11 [x]|--[e]、[1] 和 [3] S1 [e]、[2] 和 [3] S4 [s]、[nr] 和 [3] S5 [s]、[r] 和 [3] S8 [x] 和 [3] 24000 [4]|查看下一個資料表|HY010|NS [c] HY010 [o]|  
  
 [1] 驅動程式管理員傳回錯誤。  
  
 [2] 驅動程式管理員未傳回此錯誤。  
  
 [3] 目前的結果是最後一個或唯一的結果，或沒有目前的結果。 如需多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 目前的結果不是最後一個結果。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已 SQL_NO_DATA 傳回，驅動程式就會傳回此錯誤。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|HY010|查看下一個資料表|S2 [e]，p，和 [1] S4 [s]、[p]、[nr]、[1] S5 [s]、[p]、[r]、[1] S8 [d]、[p]、[1] S11 [x]、[p] 和 [1] 24000 [p] 和 [2] HY010 [np]|請參閱資料指標狀態資料表|HY010|NS [c] HY010 [o]|  
  
 [1] 目前的結果是最後一個或唯一的結果，或沒有目前的結果。 如需多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 目前的結果不是最後一個結果。  
  
## <a name="sqlexecute-prepared-states"></a>SQLExecute （已備妥的狀態）  
  
|S2<br /><br /> 沒有任何結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQLExecute （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p]，[1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果**SQLFetch**或**SQLFetchScroll**已 SQL_NO_DATA 傳回，驅動程式就會傳回此錯誤。  
  
## <a name="sqlextendedfetch"></a>SQLExtendedFetch  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|S1010|S1010|24000|查看下一個資料表|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQLExtendedFetch （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 或 [nf-e] S11 [x]|S1010|--[s] 或 [nf-e] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 和 SQLFetchScroll  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|查看下一個資料表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQLFetch 和 SQLFetchScroll （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 或 [nf-e] S11 [x]|--[s] 或 [nf-e] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|--[3]|--|--|--|--|--|--|  
  
 [1] 當 SQL_HANDLE_ENV 或 SQL_HANDLE_DBC *HandleType*時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [3] 此資料列會顯示*HandleType* SQL_HANDLE_DESC 並明確配置描述元時的轉換。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] 當 SQL_CLOSE*選項*時，此資料列會顯示轉換。  
  
 [2] 當*選項*為 SQL_UNBIND 或 SQL_RESET_PARAMS 時，此資料列會顯示轉換。 如果*選項*引數已 SQL_DROP，而基礎*驅動程式是 ODBC 3.x 驅動程式*，則驅動程式管理員會將其對應到**SQLFreeHandle**的呼叫，並將*HandleType*設為 SQL_HANDLE_STMT。 如需詳細資訊，請參閱[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)的轉換資料表。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|查看下一個資料表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGetData （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] 或 [nf-e] S11 [x] 24000 [b] HY109 [i]|--[s] 或 [nf-e] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 或 [2] HY010 [3]|查看下一個資料表|--[1] 或 [2] 24000 [3]|--[1]、[2] 或 [3] S11 [3] 和 [x]|HY010|NS [c] 或 [4] HY010 [o] 和 [5]|  
  
 [1] *DescriptorHandle*引數為 APD 或 ARD。  
  
 [2] *DescriptorHandle*引數是 IPD。  
  
 [3] *DescriptorHandle*引數為 IRD。  
  
 [4] *DescriptorHandle*引數與以非同步方式執行之**SQLGetDescField**或**SQLGetDescRec**函數中的*DescriptorHandle*引數相同。  
  
 [5] *DescriptorHandle*引數與以非同步方式執行之**SQLGetDescField**或**SQLGetDescRec**函數中的*DescriptorHandle*引數不同。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 和 SQLGetDescRec （已備妥的狀態）  
  
|S2<br /><br /> 沒有任何結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1]、[2] 或 [3] S11 [2] 和 [x]|--[1]、[2] 或 [3] S11 [x]|  
  
 [1] *DescriptorHandle*引數為 APD 或 ARD。  
  
 [2] *DescriptorHandle*引數是 IPD。  
  
 [3] *DescriptorHandle*引數為 IRD。 請注意，當*DescriptorHandle*為 IRD 時，這些函式一律會傳回狀態 S2 中 SQL_NO_DATA。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 和 SQLGetDiagRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH [2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] 當*HandleType*是 SQL_HANDLE_ENV、SQL_HANDLE_DBC 或 SQL_HANDLE_DESC 時，此資料列會顯示轉換。  
  
 [2] 當 SQL_HANDLE_STMT *HandleType*時，此資料列會顯示轉換。  
  
 [3] 當*以*為 SQL_DIAG_ROW_COUNT 時， **SQLGetDiagField**一律會傳回此狀態中的錯誤。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--[1] 24000 [2]|--[1] 24000 [2]|--[1] 24000 [2]|查看下一個資料表|HY010|HY010|  
  
 [1] 未 SQL_ATTR_ROW_NUMBER 語句屬性。  
  
 [2] 語句屬性已 SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000 [2]|--[1] 或（[v] 和 [2]） 24000 [b] 和 [2] HY109 [i] 和 [2]|--[i] 或（[v] 和 [2]） 24000 [b] 和 [2] HY109 [1] 和 [2]|  
  
 [1] 未 SQL_ATTR_ROW_NUMBER*屬性*引數。  
  
 [2]*屬性*引數已 SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|--[s] 和 [2] S1 [nf-e]，[np]，和 [4] S2 [nf-e]，[p]，以及 [4] S5 [s] 和 [3] S11 [x]|S1 [nf-e]、[np] 和 [4] S3 [nf-e]、[p] 和 [4] S4 [s] 和 [2] S5 [s] 和 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 此函式一律會傳回處於此狀態 SQL_NO_DATA。  
  
 [2] 下一個結果是資料列計數。  
  
 [3] 下一個結果是結果集。  
  
 [4] 目前的結果是最後一個結果。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|--[s] S11 [x]|--[s] S11 [x]|--[s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|查看下一個資料表|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData （需要資料狀態）  
  
|S8<br /><br /> 需要資料|S9<br /><br /> 必須 Put|S10<br /><br /> 可以 Put|  
|----------------------|---------------------|---------------------|  
|S1 [e] 和 [1] S2 [e]，[nr]，和 [2] S3 [e]，[r]，以及 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S9 [d] S11 [x]|HY010|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S4 [s]、[nr]，以及（[1] 或 [2]） S5 [s]，[r]、和（[1] 或 [2]） S5 （[s] 或 [e]）和 [4] S6 （[s] 或 [e]）和 [5] S7 （[s] 或 [e]）和 [3] S9 [d] S11 [x]|  
  
 [1] **SQLExecDirect**傳回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**傳回 SQL_NEED_DATA。  
  
 [3] 已從狀態 S7 呼叫**SQLSetPos** ，並傳回 SQL_NEED_DATA。  
  
 [4] 已從狀態 S5 呼叫**SQLBulkOperations** ，並傳回 SQL_NEED_DATA。  
  
 [5] 已從狀態 S6 呼叫**SQLSetPos**或**SQLBulkOperations** ，並傳回 SQL_NEED_DATA。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] 和 [nr] S3 [s] 和 [r] S11 [x]|--[s] 或（[e] 和 [1]） S1 [e] 和 [2] S11 [x]|S1 [e] 和 [3] S2 [s]、[nr] 和 [3] S3 [s]、[r] 和 [3] S11 [x] 和 [3] 24000 [4]|查看下一個資料表|HY010|NS [c] HY010 [o]|  
  
 [1] 除了驗證語句（SQLSTATE was HY009 [不正確引數值] 或 HY090 [不正確字串或緩衝區長度]）之外，此準備作業會失敗。  
  
 [2] 驗證語句時，準備失敗（SQLSTATE 不是 HY009 [不正確引數值] 或 HY090 [不正確字串或緩衝區長度]）。  
  
 [3] 目前的結果是最後一個或唯一的結果，或沒有目前的結果。 如需多個結果的詳細資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 目前的結果不是最後一個結果。  
  
## <a name="sqlprepare-cursor-states"></a>SQLPrepare （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|HY010|HY010|查看下一個資料表|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData （需要資料狀態）  
  
|S8<br /><br /> 需要資料|S9<br /><br /> 必須 Put|S10<br /><br /> 可以 Put|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 和 [1] S2 [e]，[nr]，和 [2] S3 [e]，[r]，以及 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] and [3] S10 [s] S11 [x]|--[s] S1 [e] 和 [1] S2 [e]，[nr]，和 [2] S3 [e]，[r]，以及 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] and [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect**傳回 SQL_NEED_DATA。  
  
 [2] **SQLExecute**傳回 SQL_NEED_DATA。  
  
 [3] 已從狀態 S7 呼叫**SQLSetPos** ，並傳回 SQL_NEED_DATA。  
  
 [4] 已從狀態 S5 呼叫**SQLBulkOperations** ，並傳回 SQL_NEED_DATA。  
  
 [5] 已從狀態 S6 呼叫**SQLSetPos**或**SQLBulkOperations** ，並傳回 SQL_NEED_DATA。  
  
 [6] 一個或多個對**SQLPutData**的呼叫會傳回 SQL_SUCCESS，然後*StrLen_or_Ind*設定為 SQL_Null_DATA，對相同的參數進行呼叫**SQLPutData** 。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|HY010|HY010|--|--|HY010|HY010|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000 [3]|HY010|HY010|  
  
 [1] 當*屬性*為連接屬性時，此資料列會顯示轉換。 如需*屬性*為語句屬性的轉換，請參閱**SQLSetStmtAttr**的語句轉換表。  
  
 [2]*屬性*引數不 SQL_ATTR_CURRENT_CATALOG。  
  
 [3]*屬性*引數已 SQL_ATTR_CURRENT_CATALOG。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursorName  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|--|--|HY010|HY010|  
  
 [1] 此資料列會顯示轉換，其中*DescriptorHandle*引數為 ARD、APD、IPD，或（適用于**SQLSetDescField**） IRD*引數*為 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR 時的 FieldIdentifier。 當*FieldIdentifier*為任何其他值時，呼叫 IRD 的**SQLSetDescField**是錯誤的。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|HY010|HY010|24000|查看下一個資料表|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos （資料指標狀態）  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQLExtendedFetch|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|--[s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH|--|--[1] HY011 [2]|--[1] 24000 [2]|--[1] 24000 [2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|  
  
 [1]*屬性*引數不是 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE 或 SQL_ATTR_CURSOR_SENSITIVITY。  
  
 [2]*屬性*引數已 SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE 或 SQL_ATTR_CURSOR_SENSITIVITY。
