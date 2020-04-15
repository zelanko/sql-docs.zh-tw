---
title: 語句轉換 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55f82e275bfd5bff12544b35a1370cdb31495320
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302849"
---
# <a name="statement-transitions"></a>陳述式轉換
ODBC 語句具有以下狀態。  
  
|State|描述|  
|-----------|-----------------|  
|S0|未分配的語句。 (連接狀態必須為 C4、C5 或 C6。 有關詳細資訊,請參閱[連接轉換](../../../odbc/reference/appendixes/connection-transitions.md)。|  
|S1|已分配的語句。|  
|S2|準備的聲明。 不會創建任何結果集。|  
|S3|準備的聲明。 將創建(可能為空)結果集。|  
|S4|已執行語句,未創建結果集。|  
|S5|已執行語句並創建(可能為空)結果集。 游標處於打開位置,位於結果集的第一行之前。|  
|S6|使用**SQLFetch**或**SQLFetchScroll**定位的游標。|  
|S7|使用 SQL**擴充取得**定位的游標。|  
|S8|函數需要數據。 尚未調用**SQLParamData。**|  
|S9|函數需要數據。 尚未調用**SQLPutData。**|  
|S10|函數需要數據。 **SQLPutData**已調用。|  
|S11|仍在執行。 非同步執行的函數返回SQL_STILL_EXECUTING後,語句將處於此狀態。 語句暫時處於此狀態,而接受語句句柄的任何函數正在執行。 狀態 S11 中的暫住位置不顯示在除**SQLCancel**的狀態表以外的任何狀態表中。 當語句暫時處於狀態 S11 時,可以通過從另一個線程調用**SQLCancel**來取消該函數。|  
|S12|非同步執行已取消。 在 S12 中,應用程式必須調用已取消的函數,直到它返回SQL_STILL_EXECUTING以外的值。 僅當函數返回SQL_ERROR和 SQLSTATE HY008(操作已取消)時,該函數才成功取消。 如果它返回任何其他值(如SQL_SUCCESS,則取消操作失敗,並且函數正常執行。|  
  
 狀態 S2 和 S3 稱為準備狀態,狀態 S5 到 S7 作為游標狀態,將 S8 到 S10 作為需求數據狀態,並將 S11 和 S12 作為非同步狀態。 在每個組中,僅當轉換在組中的每個狀態不同時才會單獨顯示;在大多數情況下,每個組中的每個狀態的轉換都相同。  
  
 下表顯示了每個 ODBC 函數如何影響語句狀態。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1], [5], [6]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[2], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|S1[3]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
|--[4], [5]|--[5]|--[5]|--[5]|--[5]|--[5]|--[5]|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV時的過渡。  
  
 [2] 此行顯示*HandleType* SQL_HANDLE_DBC時的過渡。  
  
 [3] 此行顯示*HandleType* SQL_HANDLE_STMT時的過渡。  
  
 [4] 此行顯示*handleType* SQL_HANDLE_DESC時的過渡。  
  
 [5] 使用*OutputHandlePtr*調用**SQLAllocHandle,** 指向一個有效的句柄,該句柄處理時不考慮該句柄的先前內容,並且可能會給 ODBC 驅動程式帶來問題。 使用為*\*OutputHandlePtr*定義的相同應用程式變數調用**SQLAllocHandle**兩次,而不調用**SQLFreeHandle**以釋放句柄,然後再重新分配該句柄,這是不正確的 ODBC 應用程式程式設計。 以這種方式覆蓋 ODBC 句柄可能會導致 ODBC 驅動程式的行為不一致或錯誤。  
  
## <a name="sqlbindcol"></a>SQLBindCol  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbindparameter"></a>SQLBindParameter  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlbrowseconnect-sqlconnect-and-sqldriverconnect"></a>SQLBrowse 連接、SQL 連線和 SQLDriver 連線  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|08002|08002|08002|08002|08002|08002|08002|  
  
## <a name="sqlbulkoperations"></a>SQLBulk 操作  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|請參考表格|HY010|NS [c] HY010 o|  
  
## <a name="sqlbulkoperations-cursor-states"></a>SQLBulk 動作(遊標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|-- [s] S8 [d] S11 [x]|-- [s] S8 [d] S11 [x]|HY010|  
  
## <a name="sqlcancel"></a>SQLCancel  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|S1[1] S2 [nr] 和 [2] S3 [r] 和 [2] S5[3] 和 [5] S6([3] 或 [4])和 [6] S7[4] 和 [7]|請參考表格|  
  
 [1] **SQLExecDirect**返回SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回SQL_NEED_DATA。  
  
 [3] **SQLBulk 操作**返回SQL_NEED_DATA。  
  
 [4] **SQLSetPos**返回SQL_NEED_DATA。  
  
 [5] **SQLFetch、SQLFetchScroll**或 SQL**擴展獲取**尚未調用。 **SQLFetchScroll**  
  
 [6] **SQLFetch**或**SQLFetchScroll**已調用。  
  
 [7] **SQL 擴展提取**已調用。  
  
## <a name="sqlcancel-asynchronous-states"></a>SQL取消(非同步狀態)  
  
|S11<br /><br /> 仍在執行|S12<br /><br /> 非同步取消|  
|-----------------------------|-----------------------------|  
|NS[1] S12[2]|S12|  
  
 [1] 語句在執行函數時暫時處於狀態 S11。 **SQLCancel**是從不同的線程調用的。  
  
 [2] 語句處於狀態 S11,因為稱為異步返回的函數SQL_STILL_EXECUTING。  
  
## <a name="sqlclosecursor"></a>SQLCloseCursor  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|24000|24000|24000|S1 [np] S3 [p]|HY010|HY010|  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|請參考表格|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqlcolattribute-prepared-states"></a>SQLCol屬性(準備狀態)  
  
|S2<br /><br /> 無結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1] 07005[2]|-- S11 x|  
  
 [1]*字段標識符*SQL_DESC_COUNT。  
  
 [2]*字段標識碼*未SQL_DESC_COUNT。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables"></a>SQLColumn 特權、SQLColumn、SQL 外鍵、SQLGetTypeInfo、SQL 主鍵、SQL過程列、SQL 過程程式、SQL 特殊列、SQLStatistics、SQLTable 特權和 SQLTables  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S5 [s] S11 [x]|S1 [e] S5 [s] S11 [x]|S1 [e] 和 [1] S5 [s] 和 [1] S11 [x] 和 [1] 24000 [2]|請參考表格|HY010|NS [c] HY010 o|  
  
 [1] 當前結果是最後或唯一的結果,或者沒有當前結果。 有關多個結果的詳細資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 當前結果不是最後的結果。  
  
## <a name="sqlcolumnprivileges-sqlcolumns-sqlforeignkeys-sqlgettypeinfo-sqlprimarykeys-sqlprocedurecolumns-sqlprocedures-sqlspecialcolumns-sqlstatistics-sqltableprivileges-and-sqltables-cursor-states"></a>SQLColumn 特權、SQLColumn、SQL 外鍵、SQLGetTypeInfo、SQL 主鍵、SQL過程列、SQL 過程程式、SQL 特殊列、SQLStatistics、SQLTable 特權和 SQLTables(游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000[1]|24000|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理員將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
|IH[2]|HY010|請參考表格|24000|-- S11 x|HY010|NS [c] 和 [3] HY010 [o] 或 [4]|  
  
 [1] 當*SourceDescHandle*參數為 ARD、APD 或 IPD 時,此行顯示過渡。  
  
 [2] 當*SourceDescHandle*參數是 IRD 時,此行顯示過渡。  
  
 [3] *SourceDescHandle*和*TargetDescHandle*參數與以非同步方式執行的**SQLCopyDesc**函數中相同。  
  
 [4] *SourceDescHandle*參數或*TargetDescHandle*參數(或兩者)都與以異步方式運行的**SQLCopyDesc**函數不同。  
  
## <a name="sqlcopydesc-prepared-states"></a>SQLCopyDesc(準備狀態)  
  
|S2<br /><br /> 無結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|24000[1]|-- [s] S11 [x]|  
  
 [1]此行顯示 *「源DescHandle」* 參數為 IRD 時的過渡。  
  
## <a name="sqldatasources-and-sqldrivers"></a>SQLData 源及 SQL 驅動程式  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqldescribecol"></a>SQLDescribeCol  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|請參考表格|24000|-- [s] S11 [x]|HY010|NS [c] HY010 o|  
  
## <a name="sqldescribecol-prepared-states"></a>SQLDescribeCol(準備狀態)  
  
|S2<br /><br /> 無結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|07005|-- [s] S11 [x]|  
  
## <a name="sqldescribeparam"></a>SQLDescribeParam  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|HY010|HY010|HY010|NS [c] HY010 [o]|  
  
## <a name="sqldisconnect"></a>SQL 斷線  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|S0[1]|S0[1]|S0[1]|S0[1]|(HY010)|(HY010)|  
  
 {1} 調用**SQLDisconnect**釋放與連接關聯的所有語句。 此外,這將連接狀態返回到 C2;在語句狀態為 S0 之前,連接狀態必須為 C4。  
  
## <a name="sqlendtran"></a>SQLEndTran  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--[2] 或[3] S1[1]|--[3] S1 [np] 和 ([1] 或 [2]) S1 [p] 和 [1] S2 [p] 和 [2]|--[3] S1 [np] 和 ([1] 或 [2]) S1 [p] 和 [1] S3 [p] 和 [2]|(HY010)|(HY010)|  
  
 {1}*完成類型*參數**SQL_COMMIT,SQLGetInfo**傳回SQL_CURSOR_COMMIT_BEHAVIOR資訊類型的SQL_CB_DELETE,或者 *"完成類型"* 參數SQL_ROLLBACK,SQLGetInfo**SQLGetInfo**返回SQL_CURSOR_ROLLBACK_BEHAVIOR資訊類型的SQL_CB_DELETE。  
  
 [2]*完成類型*參數**SQL_COMMIT,SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR資訊類型的SQL_CB_CLOSE,或者 *"完成類型"* 參數SQL_ROLLBACK,SQLGetInfo**SQLGetInfo**返回SQL_CURSOR_ROLLBACK_BEHAVIOR資訊類型的SQL_CB_CLOSE。  
  
 [3]*完成類型*參數**SQL_COMMIT,SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR資訊類型的SQL_CB_PRESERVE,或者 *"完成類型"* 參數SQL_ROLLBACK,SQLGetInfo**SQLGetInfo**返回SQL_CURSOR_ROLLBACK_BEHAVIOR資訊類型的SQL_CB_PRESERVE。  
  
## <a name="sqlexecdirect"></a>SQLExecDirect  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S4 [s] 和 [nr] S5 [s] 和 [r] S8 [d] S11 [x]|-- [e] 和 [1] S1 [e] 和 [2] S4 [s] 和 [nr] S5 [s] 和 [r] S8 [d] S11 [x]|-- [e]、[1]和[3]S1 [e]、[2]和[3]S4 [s]、[nr]和[3] S5 [s]、[r]和[3]S8 [d] 和 [3] S11 [x] 和 [3] 24000 [4]|請參考表格|HY010|NS [c] HY010 [o]|  
  
 [1] 驅動程式管理員傳回錯誤。  
  
 [2] 驅動程式管理員未返回錯誤。  
  
 [3] 當前結果是最後一個或唯一的結果,或者沒有當前結果。 有關多個結果的詳細資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 當前結果不是最後的結果。  
  
## <a name="sqlexecdirect-cursor-states"></a>SQLExecDirect(游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000 [1]|24000|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理員將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**返回SQL_NO_DATA,則驅動程式將返回此錯誤。  
  
## <a name="sqlexecute"></a>SQLExecute  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|請參考表格|S2 [e]、p 和 [1] S4 [s]、[p]、[nr] 和 [1] S5 [s]、[p]、[r] 和 [1] S8 [d]、[p] 和 [1] S11 [x]、[p] 和 [1] 24000 [p] 和 [2] HY010 [np]|請參考游標狀態表|HY010|NS [c] HY010 [o]|  
  
 [1] 當前結果是最後或唯一的結果,或者沒有當前結果。 有關多個結果的詳細資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [2] 當前結果不是最後的結果。  
  
## <a name="sqlexecute-prepared-states"></a>SQL 執行(就緒狀態)  
  
|S2<br /><br /> 無結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|S4 [s] S8 [d] S11 [x]|S5 [s] S8 [d] S11 [x]|  
  
## <a name="sqlexecute-cursor-states"></a>SQL 執行 (游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|24000 [p] HY010 [np]|24000 [p], [1] HY010 [np]|24000 [p] HY010 [np]|  
  
 [1] 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理員將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**返回SQL_NO_DATA,則驅動程式將返回此錯誤。  
  
## <a name="sqlextendedfetch"></a>SQL 延伸  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|S1010|S1010|24000|請參考表格|S1010|NS [c] S1010 [o]|  
  
## <a name="sqlextendedfetch-cursor-states"></a>SQL 延伸取得(遊標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|S7 [s] 或 [nf] S11 [x]|S1010|-- [s] 或 [nf] S11 [x]|  
  
## <a name="sqlfetch-and-sqlfetchscroll"></a>SQLFetch 與 SQLFetchScroll  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|請參考表格|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlfetch-and-sqlfetchscroll-cursor-states"></a>SQL 擷取與 SQLFetchScroll(游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|S6 [s] 或 [nf] S11 [x]|-- [s] 或 [nf] S11 [x]|HY010|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|-- [1]|HY010|HY010|HY010|HY010|HY010|HY010|  
|IH [2]|S0|S0|S0|S0|HY010|HY010|  
|-- [3]|--|--|--|--|--|--|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV或SQL_HANDLE_DBC時的過渡。  
  
 [2] 此行顯示*handleType* SQL_HANDLE_STMT時的過渡。  
  
 [3] 此行顯示*HandleType* SQL_HANDLE_DESC並顯式分配描述符時的過渡。  
  
## <a name="sqlfreestmt"></a>SQLFreeStmt  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH [1]|--|--|S1 [np] S2 [p]|S1 [np] S3 [p]|HY010|HY010|  
|IH [2]|--|--|--|--|HY010|HY010|  
  
 [1] 此行顯示*選項*SQL_CLOSE時的過渡。  
  
 [2] 此行顯示*選項*SQL_UNBIND或SQL_RESET_PARAMS時的過渡。 如果*Option*參數SQL_DROP並且基礎驅動程式是 ODBC 3 *.x*驅動程式,則驅動程式管理器將此參數映射到**SQLFreeHandle**的呼叫,*其中句柄類型*設定為SQL_HANDLE_STMT。 有關詳細資訊,請參閱[SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)的過渡表。  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetcursorname"></a>SQLGetCursorName  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|--|--|HY010|HY010|  
  
## <a name="sqlgetdata"></a>SQLGetData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|請參考表格|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlgetdata-cursor-states"></a>SQLGet 資料(游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] 或 [nf] S11 [x] 24000 [b] HY109 [i]|-- [s] 或 [nf] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField 和 SQLGetDescRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|-- [1] 或 [2] HY010 [3]|請參考表格|-- [1] 或 [2] 24000 [3]|-- [1]、[2]或[3] S11 [3] 和 [x]|HY010|NS [c] 或 [4] HY010 [o] 和 [5]|  
  
 [1]*描述符句柄*參數是 APD 或 ARD。  
  
 [2]*描述符句柄*參數是 IPD。  
  
 [3]*描述符處理*參數是 IRD。  
  
 [4]*描述符處理*參數與**SQLGetDescfield**或**SQLGetDescrec**函數中以非同步方式執行的描述*符處理*參數相同。  
  
 [5]*描述符處理*參數不同於**SQLGetDescfield**或**SQLGetDescrec**函數中非同步執行的描述*符處理*參數。  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec-prepared-states"></a>SQLGetDescField 和 SQLGetDescRec(準備狀態)  
  
|S2<br /><br /> 無結果|S3<br /><br /> 結果|  
|-----------------------|--------------------|  
|--[1]、[2]或[3]S11[2]和[x]|--[1]、[2]或[3] S11 [x]|  
  
 [1]*描述符句柄*參數是 APD 或 ARD。  
  
 [2]*描述符句柄*參數是 IPD。  
  
 [3]*描述符處理*參數是 IRD。 請注意,當*描述符句柄*是 IRD 時,這些函數始終在狀態 S2 中返回SQL_NO_DATA。  
  
## <a name="sqlgetdiagfield-and-sqlgetdiagrec"></a>SQLGetDiagField 與 SQLGetDiagRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--|--|--|  
|IH[2]|--[3]|--[3]|--|--|--[3]|--[3]|  
  
 [1] 此行顯示*HandleType* SQL_HANDLE_ENV、SQL_HANDLE_DBC 或SQL_HANDLE_DESC時的過渡。  
  
 [2] 此行顯示*handleType* SQL_HANDLE_STMT時的過渡。  
  
 [3] 當*Diag標識符*SQL_DIAG_ROW_COUNT時 **,SQLGetDiagField**總是返回此狀態下的錯誤。  
  
## <a name="sqlgetenvattr"></a>SQLGetEnvAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetfunctions"></a>SQLGetFunctions  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetinfo"></a>SQLGetInfo  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--[1] 24000[2]|--[1] 24000[2]|--[1] 24000[2]|請參考表格|HY010|HY010|  
  
 [1] 語句屬性未SQL_ATTR_ROW_NUMBER。  
  
 [2] 語句屬性SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlgetstmtattr-cursor-states"></a>SQLGetStmtAttr(游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|--[1] 24000[2]|--[1] 或 ([v] 和 [2] 24000 [b] 和 [2] HY109 [i] 和 [2]|-- [i] 或 ([v] 和 [2] 2] 24000 [b] 和 [2] HY109 [1] 和 [2]|  
  
 [1]*屬性*參數未SQL_ATTR_ROW_NUMBER。  
  
 [2]*屬性*參數SQL_ATTR_ROW_NUMBER。  
  
## <a name="sqlmoreresults"></a>SQLMoreResults  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|--[1]|--[1]|-- [s] 和 [2] S1 [nf]、[np]和 [4] S2 [nf]、[p]和 [4] S5 [s] 和 [3] S11 [x]|S1 [nf]、[np]和 [4] S3 [nf]、[p] 和 [4] S4 [s] 和 [2] S5 [s] 和 [3] S11 [x]|HY010|NS [c] HY010 [o]|  
  
 [1] 函數始終返回SQL_NO_DATA處於此狀態。  
  
 [2] 下一個結果是行計數。  
  
 [3] 下一個結果是結果集。  
  
 [4] 當前結果是最後的結果。  
  
## <a name="sqlnativesql"></a>SQLNativeSql  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--|--|--|--|--|--|--|  
  
## <a name="sqlnumparams"></a>SQLNumParams  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlnumresultcols"></a>SQLNumResultCols  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|-- [s] S11 [x]|-- [s] S11 [x]|-- [s] S11 [x]|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata"></a>SQLParamData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|請參考表格|NS [c] HY010 [o]|  
  
## <a name="sqlparamdata-need-data-states"></a>SQLParamData(需要資料狀態)  
  
|S8<br /><br /> 需要資料|S9<br /><br /> 必須把|S10<br /><br /> 可以放|  
|----------------------|---------------------|---------------------|  
|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S9 [d] S11 [x]|HY010|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e], [r]和[2] S4 [s]、[nr]和([1]或[2])S5 [s]、[r]和([1]或[2])S5([s] 或[e])和[4]S6([s]或[e])和[5]S7([s]或[e])和[3]S9[s]|  
  
 [1] **SQLExecDirect**返回SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回SQL_NEED_DATA。  
  
 [3] **SQLSetPos**是從狀態 S7 調用並返回SQL_NEED_DATA。  
  
 [4] **SQLBulk操作**從狀態 S5 調用並返回SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或**SQLBulk 操作**從狀態 S6 調用並返回SQL_NEED_DATA。  
  
## <a name="sqlprepare"></a>SQLPrepare  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|S2 [s] 和 [nr] S3 [s] 和 [r] S11 [x]|-- [s] 或 ([e] 和 [1]) S1 [e] 和 [2] S11 [x]|S1 [e] 和 [3] S2 [s]、[nr] 和 [3] S3 [s] 、[r] 和 [3] S11 [x] 和 [3] 24000 [4]|請參考表格|HY010|NS [c] HY010 [o]|  
  
 [1] 準備失敗的原因除驗證語句(SQLSTATE 是 HY009 [無效參數值] 或 HY090 [無效字串或緩衝區長度])。  
  
 [2] 驗證語句時準備失敗(SQLSTATE 不是 HY009 [無效參數值]或 HY090 [無效字串或緩衝區長度])。  
  
 [3] 當前結果是最後一個或唯一的結果,或者沒有當前結果。 有關多個結果的詳細資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 [4] 當前結果不是最後的結果。  
  
## <a name="sqlprepare-cursor-states"></a>SQL 準備 (游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|24000|24000|  
  
## <a name="sqlputdata"></a>SQLPutData  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|HY010|HY010|請參考表格|NS [c] HY010 [o]|  
  
## <a name="sqlputdata-need-data-states"></a>SQLPutData(需要資料狀態)  
  
|S8<br /><br /> 需要資料|S9<br /><br /> 必須把|S10<br /><br /> 可以放|  
|----------------------|---------------------|---------------------|  
|HY010|S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S10 [s] S11 [x]|-- [s] S1 [e] 和 [1] S2 [e]、[nr] 和 [2] S3 [e]、[r] 和 [2] S5 [e] 和 [4] S6 [e] 和 [5] S7 [e] 和 [3] S11 [x] HY011 [6]|  
  
 [1] **SQLExecDirect**返回SQL_NEED_DATA。  
  
 [2] **SQLExecute**返回SQL_NEED_DATA。  
  
 [3] **SQLSetPos**是從狀態 S7 調用並返回SQL_NEED_DATA。  
  
 [4] **SQLBulk操作**從狀態 S5 調用並返回SQL_NEED_DATA。  
  
 [5] **SQLSetPos**或**SQLBulk 操作**從狀態 S6 調用並返回SQL_NEED_DATA。  
  
 [6] 對**SQLPutData**的單個參數傳回的一個或多個調用SQL_SUCCESS,**然後對同**一參數進行了調用 *,StrLen_or_Ind*設置為SQL_NULL_DATA。  
  
## <a name="sqlrowcount"></a>SQLRowCount  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|(IH)|(HY010)|(HY010)|--|--|(HY010)|(HY010)|  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|--[1]|--|--|--|--[2] 24000[3]|HY010|HY010|  
  
 [1] 此行顯示*屬性*為連接屬性時的過渡。 有關*屬性*為語句屬性時的過渡,請參閱**SQLSetStmtAttr 的**語句轉換表。  
  
 [2]*屬性*參數未SQL_ATTR_CURRENT_CATALOG。  
  
 [3]*屬性*參數SQL_ATTR_CURRENT_CATALOG。  
  
## <a name="sqlsetcursorname"></a>SQLSetCursor 名稱  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--|24000|24000|HY010|HY010|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField 和 SQLSetDescRec  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|IH[1]|--|--|--|--|HY010|HY010|  
  
 [1] 當*字段標識符*參數SQL_DESC_ARRAY_STATUS_PTR或SQL_DESC_ROWS_PROCESSED_PTR時,此行顯示*描述符處理*參數為 ARD、APD、IPD 或 (對於**SQLSetDescField)** IRD 的過渡。 當*字段標識碼*是任何其他值時,為 IRD 調用**SQLSetDescField**是錯誤的。  
  
## <a name="sqlsetenvattr"></a>SQLSetEnvAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|HY011|HY011|HY011|HY011|Y011|HY01|HY011|  
  
## <a name="sqlsetpos"></a>SQLSetPos  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|HY010|HY010|24000|請參考表格|HY010|NS [c] HY010 [o]|  
  
## <a name="sqlsetpos-cursor-states"></a>SQLSetPos(游標狀態)  
  
|S5<br /><br /> 已開啟|S6<br /><br /> SQLFetch 或 SQLFetchScroll|S7<br /><br /> SQL 延伸|  
|-------------------|---------------------------------------|-----------------------------|  
|24000|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|-- [s] S8 [d] S11 [x] 24000 [b] HY109 [i]|  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
  
|S0<br /><br /> 未配置|S1<br /><br /> 已配置|S2-S3<br /><br /> Prepared|S4<br /><br /> 執行|S5-S7<br /><br /> 資料指標|S8-S10<br /><br /> 需要資料|S11-S12<br /><br /> 非同步處理|  
|------------------------|----------------------|------------------------|---------------------|----------------------|--------------------------|-----------------------|  
|Ih|--|--[1] HY011[2]|--[1] 24000[2]|--[1] 24000[2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|HY010 [np] 或 [1] HY011 [p] 和 [2]|  
  
 [1]*屬性*參數不SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE或SQL_ATTR_CURSOR_SENSITIVITY。  
  
 [2]*屬性*參數是SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_SIMULATE_CURSOR、SQL_ATTR_USE_BOOKMARKS、SQL_ATTR_CURSOR_SCROLLABLE或SQL_ATTR_CURSOR_SENSITIVITY。
