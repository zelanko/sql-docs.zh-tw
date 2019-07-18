---
title: SQLRowCount 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bf24afb193742125fda0d6693274acb98d186c90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018936"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLRowCount**會傳回受影響的資料列數目**更新**，**插入**，或**刪除**陳述式; SQL_ADD，SQL_UPDATE_BY_BOOKMARK 或 SQL_中的 DELETE_BY_BOOKMARK 作業**SQLBulkOperations**; 或在 SQL_UPDATE 或 SQL_DELETE 作業**SQLSetPos**。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *RowCountPtr*  
 [輸出]在其中傳回資料列的緩衝區指標。 針對**更新**，**插入**，並**刪除**陳述式中的 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 作業以及**SQLBulkOperations**，和 SQL_UPDATE 或 SQL_DELETE 運算中**SQLSetPos**，在傳回的值 **RowCountPtr*是所影響的列數要求或不受影響的資料列數目是否為-1。  
  
 當**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**， **SQLSetPos 或 SQLMoreResults**會呼叫 SQL_DIAG_ROW_COUNT診斷資料結構的欄位設定為資料列計數，並視實作而定的方式快取的資料列計數。 **SQLRowCount**傳回快取的資料列計數值。 陳述式控制代碼的已備妥或已配置的狀態設回之前都是有效的快取的資料列計數值，重新執行陳述式，或是**SQLCloseCursor**呼叫。 請注意，是否已呼叫的函式，因為 SQL_DIAG_ROW_COUNT 欄位已設定，所傳回的值**SQLRowCount**可能是不同於 SQL_DIAG_ROW_COUNT 欄位中的值，因為 SQL_DIAG_ROW_COUNT 欄位會重設為0 的任何函式呼叫。  
  
 如需其他陳述式和函式，驅動程式可能會定義中傳回的值\* *RowCountPtr*。 例如，某些資料來源可能無法傳回所傳回的資料列數目**選取**陳述式或類別目錄函式擷取的資料列之前。  
  
> [!NOTE]  
>  許多資料來源無法傳回結果集之前提取它們; 內的資料列數目最大的互通性，不應依賴此行為的應用程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRowCount**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLRowCount** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLRowCount**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 在呼叫之前呼叫的函式**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos** 如*StatementHandle*。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 如果上次執行的陳述式控制代碼上的 SQL 陳述式無法**更新**，**插入**，或**刪除**陳述式或是*作業*先前呼叫中的引數**SQLBulkOperations**不是 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，或如果*作業*先前呼叫中的引數**SQLSetPos** SQL_UPDATE 或 SQL_DELETE 的值不是 **RowCountPtr*是驅動程式定義。 如需詳細資訊，請參閱 <<c0> [ 判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
