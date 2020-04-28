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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2cbca03e7c3e381b803196a1bf7bb227ebeea03b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293368"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 函數
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLRowCount**會傳回受**UPDATE**、 **INSERT**或**DELETE**語句影響的資料列數;**SQLBulkOperations**中的 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK 作業;或是**SQLSetPos**中的 SQL_UPDATE 或 SQL_DELETE 作業。  
  
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
 輸出指向要傳回資料列計數的緩衝區。 針對**UPDATE**、 **INSERT**和**DELETE**語句，針對**SQLBulkOperations**中的 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 作業，以及針對**SQLSetPos**中的 SQL_UPDATE 或 SQL_DELETE 作業，在 **RowCountPtr*中傳回的值就是要求所影響的資料列數，如果無法使用受影響的資料列數目，則為-1。  
  
 呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、 **SQLSetPos 或 SQLMoreResults**時，診斷資料結構的 [SQL_DIAG_ROW_COUNT] 欄位會設定為數據列計數，而資料列計數會以與執行相依的方式進行快取。 **SQLRowCount**會傳回快取的資料列計數值。 快取的資料列計數值在語句控制碼設回已備妥或已配置的狀態之前有效，會重新叫用語句，或呼叫**SQLCloseCursor** 。 請注意，如果在設定 [SQL_DIAG_ROW_COUNT] 欄位之後呼叫了函式， **SQLRowCount**傳回的值可能會與 [SQL_DIAG_ROW_COUNT] 欄位中的值不同，因為任何函式呼叫都會將 SQL_DIAG_ROW_COUNT 欄位重設為0。  
  
 對於其他語句和函數，驅動程式可能會定義在\* *RowCountPtr*中傳回的值。 例如，某些資料來源可能可以在提取資料列之前，傳回**SELECT**語句或目錄函數所傳回的資料列數目。  
  
> [!NOTE]  
>  許多資料來源在提取結果集之前，都無法傳回結果集中的資料列數;為了達到最大的互通性，應用程式不應該依賴此行為。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRowCount**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLRowCount**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLRowCount**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）在呼叫*StatementHandle*的**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**之前，已呼叫過函數。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>評價  
 如果在語句控制碼上執行的最後一個 SQL 語句不是**UPDATE**、 **INSERT**或**DELETE**語句，或是先前呼叫**SQLBulkOperations**的作業引數不是 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，或先前呼叫**SQLSetPos** *的作業*引數未 SQL_UPDATE 或 SQL_DELETE，則 **RowCountPtr*的值會定義為驅動程式。 *Operation* 如需詳細資訊，請參閱[判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
