---
title: "SQLRowCount 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRowCount
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRowCount
helpviewer_keywords: SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04a4e5061a80fec51361e82c57102df8e3fa34c8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="sqlrowcount-function"></a>SQLRowCount 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLRowCount**傳回受影響的資料列數目**更新**，**插入**，或**刪除**陳述式; SQL_ADD，SQL_UPDATE_BY_BOOKMARK 或 SQL_中的 DELETE_BY_BOOKMARK 作業**SQLBulkOperations**; 或在 SQL_UPDATE 或 SQL_DELETE 作業**SQLSetPos**。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *RowCountPtr*  
 [輸出]指出緩衝區中要傳回的資料列數。 如**更新**，**插入**，和**刪除**陳述式中的 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 作業以及**SQLBulkOperations**，和在 SQL_UPDATE 或 SQL_DELETE 作業**SQLSetPos**中, 傳回的值 **RowCountPtr*是影響之資料列數目要求或不受影響的資料列數目是否為-1。  
  
 當**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**， **SQLSetPos 或 SQLMoreResults**會呼叫 SQL_DIAG_ROW_COUNT診斷資料結構中的欄位設定為資料列計數，並視實作而定的方式快取的資料列計數。 **SQLRowCount**傳回快取的資料列計數值。 快取的資料列計數值是否有效，直到陳述式控制代碼設定回備妥或已配置的狀態，重新執行陳述式，或**SQLCloseCursor**呼叫。 請注意，是否已經呼叫函式，因為 SQL_DIAG_ROW_COUNT 欄位已設定，所傳回的值**SQLRowCount**可能是 SQL_DIAG_ROW_COUNT 欄位中的值不同，因為 SQL_DIAG_ROW_COUNT 欄位會重設為0 的任何函式呼叫。  
  
 針對其他陳述式和函式，此驅動程式可能定義中傳回的值\* *RowCountPtr*。 例如，某些資料來源可能是能夠傳回的資料列數目傳回**選取**陳述式或類別目錄函式擷取的資料列之前。  
  
> [!NOTE]  
>  許多資料來源不能傳回資料列的數目的結果集之前提取。最大的互通性，不應依賴此行為的應用程式。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRowCount**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLRowCount** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLRowCount**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> (DM) 函式呼叫之前呼叫**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos** 的*StatementHandle*。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 如果上次執行陳述式控制代碼上的 SQL 陳述式無法**更新**，**插入**，或**刪除**陳述式或*作業*上次呼叫中的引數**SQLBulkOperations**未 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，或如果*作業*先前呼叫中的引數**SQLSetPos** SQL_UPDATE 或 SQL_DELETE 的值不是 **RowCountPtr*是驅動程式定義。 如需詳細資訊，請參閱[判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
