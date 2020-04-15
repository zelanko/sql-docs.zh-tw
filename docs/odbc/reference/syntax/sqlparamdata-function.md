---
title: SQLParamData 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLParamData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLParamData
helpviewer_keywords:
- SQLParamData function [ODBC]
ms.assetid: 68fe010d-9539-4e5b-a260-c8d32423b1db
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ed149e125e3231d670c6ddbd4569ff5ccee5c15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306919"
---
# <a name="sqlparamdata-function"></a>SQLParamData 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLParamData**與**SQLPutData**一起使用,在語句執行時提供參數數據,並與**SQLGetData**一起檢索流式輸出參數數據。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *價值PtrPtr*  
 【輸出]指向用於返回**SQLBind 參數**中指定的*參數 ValuePtr*緩衝區的位址(用於參數數據)或**SQLBindCol**中指定的*TargetValuePtr*緩衝區的位址(對於列資料)的緩衝區的指標,SQL_DESC_DATA_PTR描述符記錄欄位中所包含。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_INVALID_HANDLE或SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLParamData**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLParamData**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|綁定參數的**SQLBind 參數**中*的值類型*參數識別的資料值無法轉換為**SQLBind 參數**中的*參數類型*參數識別的資料類型。<br /><br /> 返回為SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT綁定的參數的數據值無法轉換為**SQLBind 參數**中*ValueType*參數標識的數據類型。<br /><br /> (如果無法轉換一個或多個行的數據值,但成功返回一個或多個行,則此函數將返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22026|字串資料，長度不符|**SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN資訊類型為"Y",對於長參數(資料類型為SQL_LONGVARCHAR、SQL_LONGVARBINARY或長資料來源特定資料類型)發送的數據少於**SQLBind 參數**中*StrLen_or_IndPtr*參數中指定的數據。<br /><br /> **SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN資訊類型為"Y",對於長列(數據類型SQL_LONGVARCHAR、SQL_LONGVARBINARY或長數據來源特定資料類型)發送的數據比在與使用**SQLBulk 操作**添加或更新或使用**SQLSetPos**更新的數據列中的列對應的長度緩衝區中指定的數據較少。|  
|40001|序列化失敗|由於資源與另一個事務死鎖,事務被回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**調用了*語句句柄*;然後,在*語句句柄*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 以前的函數調用不是對 SQLExecDirect、SQLExecute、SQLBulk**操作**或**SQLSetPos**的呼叫,其中返回代碼SQL_NEED_DATA,或者以前的**SQLExecDirect**函數調用是對**SQLPutData**的調用。 **SQLExecute**<br /><br /> 前面的函數調用是對**SQLParamData**的調用。<br /><br /> (DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLParamData**函數時,此異步函數仍在執行。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> ** **SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於*語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** **SQLCancel**是在為執行時的所有數據參數或列發送數據之前調用的。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 對應於*語句句柄*的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
 如果在 SQL 語句中為參數傳送資料時呼叫**SQLParamData,** 它可以傳回執行敘述 **(SQLExecute**或**SQLExecDirect)** 的函數可以傳回的任何 SQLSTATE。 如果在發送使用**SQLBulk 操作**更新或添加的列的數據或使用**SQLSetPos**更新時調用它,則可以返回**SQLBulk 操作**或**SQLSetPos**可以傳回的任何 SQLSTATE。  
  
## <a name="comments"></a>註解  
 **SQLParamData**可以調用提供執行時的數據,用於兩個用途:參數數據,用於 SQLExecute 或**SQLExecDirect**的**SQLExecDirect**呼叫,或者列數據,這些資料將在調用**SQLBulk 操作**或透過呼叫**SQLSetPos**更新或更新行時使用。 在執行時 **,SQLParamData**會向應用程式返回驅動程式所需的數據的指示器。  
  
 當應用程式呼叫**SQLExecute**SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**時,驅動程式在需要執行資料的數據**SQLExecDirect**時返回SQL_NEED_DATA。 然後,應用程式調用**SQLParamData**以確定要發送的數據。 如果驅動程式需要參數數據,驅動程式在*\*ValuePtrPtr*輸出緩衝區中返回應用程式在行集緩衝區中放置的值。 應用程式可以使用此值來確定驅動程式請求的參數數據。 如果驅動程式需要列資料,驅動程式將返回*\*ValuePtrPtr*緩衝區中該列最初綁定到的位址,如下所示:  
  
 *繫結位址* + *繫結位位移*量 = ((*行號*- 1) x*元素大小*)  
  
 其中變數定義如下表所示。  
  
|變數|描述|  
|--------------|-----------------|  
|*繫結位址*|在**SQLBindCol**中使用*TargetValuePtr*參數指定的位址。|  
|*繫結位移*|儲存在使用SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性指定的位址的值。|  
|*Row Number*|行集中的行的 1 個基於的編號。 對於預設的單行提取,這是 1。|  
|*元素大小*|數據和長度/指標緩衝區SQL_ATTR_ROW_BIND_TYPE語句屬性的值。|  
  
 它還返回SQL_NEED_DATA,這是應用程式應呼叫**SQLPutData**發送數據的指示器。  
  
 應用程式根據需要多次調用**SQLPutData**以發送列或參數的執行數據。 為列或參數發送所有數據后,應用程式將再次調用**SQLParamData。** 如果**SQLParamData**再次返回SQL_NEED_DATA,則必須為另一個參數或列發送數據。 因此,應用程式再次呼叫**SQLPutData**。 如果已為所有參數或列發送了所有執行數據數據,則**SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,*\*則 ValuePtrPtr*中的值未定義,可以執行 SQL 語句或處理**SQLBulk 操作**或**SQLSetPos**呼叫。  
  
 如果**SQLParamData**為搜尋的更新或刪除語句提供參數數據,而該語句不會影響數據來源上的任何行,則對**SQLParamData**的調用將返回SQL_NO_DATA。  
  
 有關如何在語句執行時傳遞數據執行時參數資料的詳細資訊,請參閱[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md)中的"傳遞參數值"和["發送長數據](../../../odbc/reference/develop-app/sending-long-data.md)"。 有關如何更新或添加數據執行列資料的詳細資訊,請參閱 SQLSetPos 中的「使用[SQLSetPos」](../../../odbc/reference/syntax/sqlsetpos-function.md)部分[、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)中的「使用書籤執行批量更新」以及[長數據和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)節。  
  
 可以調用**SQLParamData**來檢索流式輸出參數。 當**SQLMore 結果****、SQLExecute、SQLGetData**或**SQLExecDirect**返回SQL_PARAM_DATA_AVAILABLE時,調用**SQLParamData**以**SQLGetData**確定哪個參數具有可用的值。 有關SQL_PARAM_DATA_AVAILABLE和串流式輸出參數的詳細資訊,請參閱使用[SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回敘述中有關參數的資訊|[SQLDescribeParam 函數](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|在執行時傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
