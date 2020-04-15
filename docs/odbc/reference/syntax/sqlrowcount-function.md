---
title: SQLRowCount 函數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81293368"
---
# <a name="sqlrowcount-function"></a>SQLRowCount 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLRowCount**傳回受**更新**、**插入**或**刪除**語句影響的行數;**SQLBulk 操作**中的SQL_ADD、SQL_UPDATE_BY_BOOKMARK或SQL_DELETE_BY_BOOKMARK操作;或**SQLSetPos**中的SQL_UPDATE或SQL_DELETE操作。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *羅( 羅) CountPtr*  
 【輸出]指向要返回行計數的緩衝區。 對於**SQLBulk 操作**中的SQL_ADD、SQL_UPDATE_BY_BOOKMARK和SQL_DELETE_BY_BOOKMARK操作的**UPDATE、INSERT**和**DELETE**語句,以及**SQLSetPos**中SQL_UPDATE或SQL_DELETE操作,在 「*RowCountPtr」* 中傳回的值是受請求影響的行數,**INSERT**如果受影響的行數不可用,則為 -1。  
  
 當調用**SQLExecute、SQLExecDirect、SQLBulk****操作****、SQLSetPos 或 SQLMore 結果**時,診斷數據結構的SQL_DIAG_ROW_COUNT欄位設置為行計數,行計數以**SQLExecute**與實現相關的方式緩存。 **SQLRowCount**傳回緩存的行計數值。 緩存的行計數值有效,直到語句句柄設置回準備或分配狀態,重新執行語句或調用**SQLCloseCursor。** 請注意,如果自設置SQL_DIAG_ROW_COUNT欄位以來已調用函數,**則 SQLRowCount**返回的值可能與SQL_DIAG_ROW_COUNT欄位中的值不同,因為 SQL_DIAG_ROW_COUNT欄位被任何函數調用重置為 0。  
  
 對於其他語句和函數,驅動程式可以定義在\**RowCountPtr*中返回的值。 例如,某些數據源在獲取行之前,可能能夠返回**SELECT**語句或目錄函數返回的行數。  
  
> [!NOTE]  
>  許多數據源無法在獲取結果集中的行數之前返回它們;為了達到最大的互操作性,應用程式不應依賴此行為。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLRowCount**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLRowCount**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLRowCount**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 在呼叫**SQLExecute、SQLExecDirect、SQLBulk****操作**或**SQLSetPos**之前呼叫*的敘述 。* **SQLExecute**<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 如果在語句句柄上執行的最後一個 SQL 語句不是**更新**、**插入**或**DELETE**語句,或者對**SQLBulk 操作**的上一個調用中的*操作*參數不是SQL_ADD、SQL_UPDATE_BY_BOOKMARK或SQL_DELETE_BY_BOOKMARK,或者如果上一個調用**SQLSetPos**中的*操作*參數未SQL_UPDATE或SQL_DELETE,則 =*RowCountPtr*的值是驅動程式定義的。 有關詳細資訊,請參閱[確定受影響的行數](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
