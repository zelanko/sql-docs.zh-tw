---
title: SQL取消功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCancel
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCancel
helpviewer_keywords:
- SQLCancel function [ODBC]
ms.assetid: ac0b5972-627f-4440-8c5a-0e8da728726d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcc2afce495a1481692ba1f20162a2df5d9a9458
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301308"
---
# <a name="sqlcancel-function"></a>SQLCancel 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLCancel**取消語句的處理。  
  
 要取消連接或語句的處理,請使用[SQLCancelHandle 函數](../../../odbc/reference/syntax/sqlcancelhandle-function.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLCancel(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLCancel**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_STMT的*句柄類型*和*敘述句柄*。 下表列出了**SQLCancel**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)在參數*\*MessageText*緩衝區中返回的錯誤消息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLCancel**函數時,此異步函數仍在執行。<br /><br /> (DM) 取消操作失敗,因為與*語句句柄*關聯的連接句柄正在進行非同步操作。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY018|伺服器拒絕取消要求|伺服器拒絕了取消請求。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 **SQLCancel**可以取消敘述上的以下類型處理:  
  
-   在語句上異步運行的函數。  
  
-   需要數據的語句上的函數。  
  
-   在另一個線程上的語句上運行的函數。  
  
 在 ODBC 2 中。*x,* 如果應用程式在未對語句執行處理時調用**SQLCancel,** 則**SQLCancel**具有與**SQLFreeStmt**與 SQL_CLOSE 選項相同的效果;此行為僅針對完整性而定義,應用程式應調用**SQLFreeStmt**或**SQLCloseCursor**來關閉游標。  
  
 當調用**SQLCancel**以取消在語句或需要數據的語句上異步運行的函數時,將清除被取消的函數發佈的診斷記錄,並且**SQLCancel**發佈自己的診斷記錄;但是,當**SQLCancel**調用以取消在另一個線程上的語句上運行的函數時,它不會清除正在取消的函數的診斷記錄,也不會發佈自己的診斷記錄。  
  
## <a name="canceling-asynchronous-processing"></a>取消非同步處理  
 應用程式同步調用函數後,它會重複調用該函數以確定它是否已完成處理。 如果函數仍在處理中,它將返回SQL_STILL_EXECUTING。 如果函數已完成處理,它將返回其他代碼。  
  
 對返回SQL_STILL_EXECUTING的函數進行任何調用後,應用程式可以調用**SQLCancel**來取消該函數。 如果取消請求成功,驅動程式將返回SQL_SUCCESS。 此消息不指示該函數實際上已取消;因此,該功能未表示該函數已取消。它表示已處理取消請求。 當或如果實際取消該函數時,則與驅動程序相關且與數據源相關。 應用程式必須繼續調用原始函數,直到返回代碼不SQL_STILL_EXECUTING。 如果已成功取消該功能,則返回代碼SQL_ERROR SQLSTATE HY008(操作已取消)。 如果函數完成正常處理,則返回代碼將SQL_SUCCESS或SQL_SUCCESS_WITH_INFO如果函數成功或SQL_ERROR,並且如果函數失敗,則為 HY008 以外的 SQLSTATE(操作已取消)。  
  
> [!NOTE]  
>  在 ODBC 3.5 中,對**SQLCancel**的調用,當語句未執行任何處理時,不會被視為使用 SQL_CLOSE選項的**SQLFreeStmt,** 但根本沒有效果。 要關閉游標,應用程式應呼叫**SQLCloseCursor**,而不是**SQLCancel**。  
  
 有關同步處理的詳細資訊,請參閱[非同步執行](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)。  
  
## <a name="canceling-functions-that-need-data"></a>取消需要資料的函數  
 **在 SQLExecute**或**SQLExecDirect**傳回SQL_NEED_DATA並在為所有資料執行參數發送數據之前,應用程式可以調用**SQLCancel**取消語句執行。 取消語句後,應用程式可以再次調用**SQLExecute**或**SQLExecDirect。** 有關詳細資訊,請參閱[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 **在 SQLBulk 操作**或**SQLSetPos**返回SQL_NEED_DATA後,在為執行時的所有數據發送數據之前,應用程式可以調用**SQLCancel**來取消該操作。 操作取消後,應用程式可以再次調用**SQLBulk 操作**或**SQLSetPos;** 取消不會影響游標狀態或當前游標位置。 有關詳細資訊,請參閱[SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="canceling-functions-executing-on-another-thread"></a>取消在另一個緒執行的函數  
 在多線程應用程式中,應用程式可以取消在另一個線程上運行的函數。 要取消該函數,應用程式調用**SQLCancel**時,使用與目標函數使用的相同語句句柄,但調用不同的線程。 如何取消功能取決於驅動程式和作業系統。 與取消非同步運行的函數一樣 **,SQLCancel**的返回代碼僅指示驅動程式是否成功處理了請求。 只能返回SQL_SUCCESS或SQL_ERROR;未返回任何診斷資訊。 如果原始函數被取消,它將返回SQL_ERROR和 SQLSTATE HY008(操作已取消)。  
  
 如果在調用另一個線程上的**SQLCancel**取消語句執行時正在執行 SQL 語句,則在執行成功並返回SQL_SUCCESS,而取消也成功。 在這種情況下,驅動程式管理器假定語句執行打開的游標被取消關閉,因此應用程式將無法使用游標。  
  
 有關執行緒的詳細資訊,請參閱[多線程](../../../odbc/reference/develop-app/multithreading.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|執行批次插入或更新操作|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|除了**SQLCancel**的功能外,取消在連接句柄上異步運行的函數。|[SQLCancelHandle 函式](../../../odbc/reference/syntax/sqlcancelhandle-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放敘述|[SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|取得診斷記錄的欄位或診斷標頭的欄位|[SQLGetDiagField 函式](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
|取得診斷資料結構的多個字段|[SQLGetDiagRec 函式](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
|傳回下一個參數以送出資料|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|在執行時傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|將游標定位在列集中、刷新列集中中的資料或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
