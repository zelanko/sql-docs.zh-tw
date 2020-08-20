---
description: SQLRowCount 函數
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
ms.openlocfilehash: 666351fcd4758170baaf62fbd80cd45a554ab92a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499591"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLRowCount** 會傳回受 **UPDATE**、 **INSERT**或 **DELETE** 語句影響的資料列數目; **SQLBulkOperations**中的 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK 操作;或 **SQLSetPos**中的 SQL_UPDATE 或 SQL_DELETE 作業。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *RowCountPtr*  
 出指向要傳回資料列計數的緩衝區。 針對 **UPDATE**、 **INSERT**和 **DELETE** 語句，對於 **SQLBulkOperations**中的 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 和 SQL_DELETE_BY_BOOKMARK 作業，以及 **SQLSetPos**中的 SQL_UPDATE 或 SQL_DELETE 作業，**RowCountPtr* 中傳回的值為受要求影響的資料列數目，如果無法使用受影響的資料列數目，則為-1。  
  
 當呼叫 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**、 **SQLSetPos 或 SQLMoreResults** 時，診斷資料結構的 SQL_DIAG_ROW_COUNT 欄位會設定為數據列計數，並以與執行相依的方式快取資料列計數。 **SQLRowCount** 會傳回快取的資料列計數值。 快取的資料列計數值會在語句控制碼設回已備妥或已配置的狀態之前有效，會重新叫用語句，或呼叫 **SQLCloseCursor** 。 請注意，如果在設定 SQL_DIAG_ROW_COUNT 欄位之後呼叫函數， **SQLRowCount** 所傳回的值可能會與 SQL_DIAG_ROW_COUNT 欄位中的值不同，因為任何函式呼叫都會將 SQL_DIAG_ROW_COUNT 欄位重設為0。  
  
 針對其他語句和函式，驅動程式可能會定義在 RowCountPtr 中傳回的值 \* * *。 例如，某些資料來源可能會在提取資料列之前，傳回 **SELECT** 語句或目錄函數所傳回的資料列數目。  
  
> [!NOTE]  
>  許多資料來源在提取結果集之前無法傳回資料列的數目;基於最大的互通性，應用程式不應該依賴此行為。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRowCount**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLRowCount** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLRowCount** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 在呼叫 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos** for *StatementHandle*之前，會呼叫此函數。<br /><br />  (DM) 針對 *StatementHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 如果在語句控制碼上執行的最後一個 SQL 語句不是**UPDATE**、 **INSERT**或**DELETE**語句，或是先前呼叫**SQLBulkOperations** *的作業引數不*是 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，或者先前呼叫**SQLSetPos** *的作業引數*不是 SQL_UPDATE 或 SQL_DELETE，則 **RowCountPtr*的值為驅動程式定義。 如需詳細資訊，請參閱 [決定受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
