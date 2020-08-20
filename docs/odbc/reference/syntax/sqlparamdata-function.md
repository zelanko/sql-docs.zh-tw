---
description: SQLParamData 函式
title: SQLParamData 函式 |Microsoft Docs
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
ms.openlocfilehash: d44b3bd5017e5ef5cebb40c9bbbaccdde7368bbf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487251"
---
# <a name="sqlparamdata-function"></a>SQLParamData 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLParamData** 會與 **SQLPutData** 一起使用，以便在語句執行時間提供參數資料，並使用 **SQLGetData** 來取出資料流程輸出參數資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *ValuePtrPtr*  
 出緩衝區的指標，此緩衝區會傳回**SQLBindParameter** (中針對參數資料) 指定的*ParameterValuePtr*緩衝區位址，或是資料行資料) 之**SQLBindCol** (中所指定*TargetValuePtr*緩衝區的位址，如 SQL_DESC_DATA_PTR 描述項記錄欄位所包含。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLParamData**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLParamData** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|在**SQLBindParameter**中，針對系結參數所識別的*ValueType*引數所識別的資料值，無法轉換為**SQLBindParameter**中*ParameterType*引數所識別的資料類型。<br /><br /> 針對系結為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 的參數傳回的資料值無法轉換成**SQLBindParameter**中的*ValueType*引數所識別的資料類型。<br /><br />  (如果無法轉換一個或多個資料列的資料值，但成功傳回一或多個資料列，則此函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22026|字串資料，長度不符|**SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型為 "Y"，且較少的資料已傳送給長參數 (資料類型 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定資料類型，) 于**SQLBindParameter**中的*StrLen_or_IndPtr*引數所指定的資料類型。<br /><br /> **SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型為 "Y"，且較少的資料行已傳送較少的資料 (資料類型 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定的資料類型 **) 與資料**列中的資料行相對應的資料列中的資料行所指定的資料列中所指定的資料行所對應的資料列中所指定的資料**行。**|  
|40001|序列化失敗|交易已復原，因為另一個交易發生資源鎖死。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 已呼叫函式，且在完成執行之前，在*StatementHandle*上呼叫了**SQLCancel**或**SQLCancelHandle** ;接著會在*StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 先前的函式呼叫不是呼叫 **SQLExecDirect**、 **SQLExecute**、 **SQLBulkOperations**或 **SQLSetPos** ，其中傳回碼是 SQL_NEED_DATA 的，或是之前的函式呼叫是對 **SQLPutData**的呼叫。<br /><br /> 先前的函式呼叫是對 **SQLParamData**的呼叫。<br /><br />  (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLParamData** 函式時，仍在執行此非同步函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，會呼叫**SQLCancel** 。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 對應至 *StatementHandle* 的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
 如果在 SQL 語句中傳送參數的資料時呼叫 **SQLParamData** ，它可能會傳回呼叫的函式所傳回的任何 SQLSTATE，以執行語句 (**SQLExecute** 或 **SQLExecDirect**) 。 如果在傳送要更新或新增的資料行資料 **，或使用** **SQLSetPos**來更新資料行時呼叫它，它可能會傳回 **SQLBulkOperations** 或 **SQLSetPos**可以傳回的任何 SQLSTATE。  
  
## <a name="comments"></a>註解  
 您可以呼叫**SQLParamData**來提供兩個使用的資料執行中資料：用於呼叫**SQLExecute**或**SQLExecDirect**的參數資料，或是當呼叫**SQLBulkOperations**或透過呼叫來更新或加入資料列時，所要使用的資料行**資料。** 在執行時間， **SQLParamData** 會將驅動程式所需的資料指標返回應用程式。  
  
 當應用程式呼叫 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos**時，驅動程式會在需要資料執行中資料時傳回 SQL_NEED_DATA。 然後，應用程式會呼叫 **SQLParamData** 來判斷要傳送的資料。 如果驅動程式需要參數資料，驅動程式會在* \* ValuePtrPtr*輸出緩衝區中傳回應用程式放入資料列集緩衝區的值。 應用程式可以使用此值來判斷驅動程式所要求的參數資料。 如果驅動程式需要資料行資料，驅動程式會在* \* ValuePtrPtr*緩衝區中傳回資料行原先系結的位址，如下所示：  
  
 系結*位址*  + *Binding Offset* + ( # B1 *Row Number* -1) x*元素大小*)   
  
 變數的定義方式如下表所示。  
  
|變數|描述|  
|--------------|-----------------|  
|*系結位址*|在**SQLBindCol**中使用*TargetValuePtr*引數指定的位址。|  
|*系結位移*|儲存在使用 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性指定之位址的值。|  
|*Row Number*|資料列集中的資料列編號，以1為基點數。 若為單一資料列提取（預設值），則為1。|  
|*元素大小*|資料和長度/指標緩衝區的 SQL_ATTR_ROW_BIND_TYPE 語句屬性值。|  
  
 它也會傳回 SQL_NEED_DATA，也就是應用程式應該呼叫 **SQLPutData** 來傳送資料的指標。  
  
 應用程式會視需要多次呼叫 **SQLPutData** ，以傳送資料行或參數的資料執行資料。 傳送資料行或參數的所有資料之後，應用程式會再次呼叫 **SQLParamData** 。 如果 **SQLParamData** 再次傳回 SQL_NEED_DATA，就必須傳送另一個參數或資料行的資料。 因此，應用程式會再次呼叫 **SQLPutData**。 如果所有參數或資料行都已傳送所有資料執行中資料，則**SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO、未定義* \* ValuePtrPtr*中的值，而且可以執行 SQL 語句，或是可以處理**SQLBulkOperations**或**SQLSetPos**呼叫。  
  
 如果 **SQLParamData** 為搜尋的 update 或 delete 語句提供的參數資料不會影響資料來源中的任何資料列，則對 **SQLParamData** 的呼叫會傳回 SQL_NO_DATA。  
  
 如需如何在語句執行時間傳遞資料執行中參數資料的詳細資訊，請參閱 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 中的「傳遞參數值」和傳送 [較長的資料](../../../odbc/reference/develop-app/sending-long-data.md)。 如需有關如何更新或加入資料執行中資料行資料的詳細資訊，請參閱 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)中的「使用 SQLSetPos」一節， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)中的「使用書簽執行大量更新」以及 [Long data 和 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
 您可以呼叫**SQLParamData**來取出資料流程輸出參數。 當 **SQLMoreResults**、 **SQLExecute**、 **SQLGetData**或 **SQLExecDirect** 傳回 SQL_PARAM_DATA_AVAILABLE 時，請呼叫 **SQLParamData** 來判斷哪個參數有可用的值。 如需 SQL_PARAM_DATA_AVAILABLE 和資料流程輸出參數的詳細資訊，請參閱 [使用 SQLGetData 來抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回語句中參數的相關資訊|[SQLDescribeParam 函數](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|在執行時間傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
