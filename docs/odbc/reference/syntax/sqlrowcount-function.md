---
title: SQLRowCount 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRowCount
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLRowCount
helpviewer_keywords:
- SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65683174ee5b48a8f7b861f3ba838334d70025ae
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345442"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 函數
**標準**  
 引進的版本:ODBC 1.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLRowCount**會傳回受**UPDATE**、 **INSERT**或**DELETE**語句影響的資料列數;**SQLBulkOperations**中的 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK 運算;或**SQLSetPos**中的 SQL_UPDATE 或 SQL_DELETE 作業。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *RowCountPtr*  
 輸出指向要傳回資料列計數的緩衝區。 適用于**UPDATE**、 **INSERT**和**DELETE**語句、 **SQLBULKOPERATIONS**中的 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 作業, 以及 SQL_UPDATE 中的 SQL_DELETE 或 SQLSetPos 作業  , 在 **RowCountPtr*中傳回的值是受要求影響的資料列數, 如果無法使用受影響的資料列數目, 則為-1。  
  
 當呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、 **SQLSetPos 或 SQLMORERESULTS**時, 診斷資料結構的 SQL_DIAG_ROW_COUNT 欄位會設定為數據列計數, 而資料列計數會在與執行相依的方式。 **SQLRowCount**會傳回快取的資料列計數值。 快取的資料列計數值在語句控制碼設回已備妥或已配置的狀態之前有效, 會重新叫用語句, 或呼叫**SQLCloseCursor** 。 請注意, 如果在設定 SQL_DIAG_ROW_COUNT 欄位之後呼叫了函數, **SQLRowCount**所傳回的值可能會與 SQL_DIAG_ROW_COUNT 欄位中的值不同, 因為 SQL_DIAG_ROW_COUNT 欄位會由任何函式呼叫重設為0。  
  
 對於其他語句和函數, 驅動程式可能會定義在*RowCountPtr*中\*傳回的值。 例如, 某些資料來源可能可以在提取資料列之前, 傳回**SELECT**語句或目錄函數所傳回的資料列數目。  
  
> [!NOTE]  
>  許多資料來源在提取結果集之前, 都無法傳回結果集中的資料列數;為了達到最大的互通性, 應用程式不應該依賴此行為。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRowCount**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec HandleType Handletype 來和  *StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。  下表列出**SQLRowCount**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLRowCount**函數時, 這個非同步函式仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** , 並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。<br /><br /> (DM) 在呼叫*StatementHandle*的**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**之前, 已呼叫過函數。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式, 且在呼叫此函式時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 如果在語句控制碼上執行的最後一個 SQL 語句不是**UPDATE**、 **INSERT**或**DELETE**語句, 或是先前對**SQLBulkOperations**的呼叫中的*Operation*引數不是 SQL_ADD, SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK, 或如果先前對**SQLSetPos**的呼叫中的*Operation*引數不是 SQL_UPDATE 或 SQL_DELETE, 則 **RowCountPtr*的值是驅動程式定義的。 如需詳細資訊, 請參閱[判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
