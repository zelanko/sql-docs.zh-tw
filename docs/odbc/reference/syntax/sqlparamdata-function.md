---
title: SQLParamData 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 395cf795659b47398639f30fbd863b1f2d385e55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlparamdata-function"></a>SQLParamData 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLParamData**會搭配**SQLPutData**提供參數資料在陳述式執行時，與**SQLGetData**擷取資料流的輸出參數資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLParamData(  
     SQLHSTMT       StatementHandle,  
     SQLPOINTER *   ValuePtrPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *ValuePtrPtr*  
 [輸出]緩衝區中要傳回的位址指標*ParameterValuePtr*中指定的緩衝區**SQLBindParameter** （適用於參數的資料） 或位址*TargetValuePtr*中指定的緩衝區**SQLBindCol** （適用於資料行的資料），如 SQL_DESC_DATA_PTR 描述項記錄欄位中包含。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_INVALID_HANDLE 或 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLParamData**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLParamData** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|所識別的資料值*ValueType*引數中的**SQLBindParameter**繫結的參數無法轉換成資料類型所識別的*ParameterType*引數中的**SQLBindParameter**。<br /><br /> 針對繫結為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 無法轉換成資料類型所識別的參數傳回的資料值*ValueType*引數中的**SQLBindParameter**。<br /><br /> （如果無法轉換一或多個資料列的資料值，但一個或多個資料列已成功地傳回，此函數會傳回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22026|字串資料，長度不符|SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo** "Y"，且於指定較少的資料傳送長參數 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型）與*StrLen_or_IndPtr*引數中的**SQLBindParameter**。<br /><br /> SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo** "Y"，且比中已指定較少的資料傳送長資料行 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型）對應至已加入或更新的資料列中的資料行長度的緩衝區**SQLBulkOperations**或更新與**SQLSetPos**。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|相關聯的連接失敗，此函式，在執行期間，無法決定交易的狀態。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*; 上再呼叫此函式一次*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 先前的函式呼叫不是呼叫**SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**，或**SQLSetPos**位置傳回碼為 SQL_NEED_DATA，或先前的函式呼叫已呼叫**SQLPutData**。<br /><br /> 先前的函式呼叫已呼叫**SQLParamData**。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLParamData**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*和傳回的 SQL_NEED_DATA。 **SQLCancel**呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式對應至*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
 如果**SQLParamData**呼叫時傳送的 SQL 陳述式參數的資料，它會傳回任何可執行陳述式所呼叫的函式所傳回的 SQLSTATE (**SQLExecute**或**SQLExecDirect**)。 如果傳送的資料行的資料時呼叫正在更新或加入**SQLBulkOperations**或更新**SQLSetPos**，它會傳回任何可傳回的 SQLSTATE **SQLBulkOperations**或**SQLSetPos**。  
  
## <a name="comments"></a>註解  
 **SQLParamData**提供兩種用途的資料在執行資料，可以呼叫： 將呼叫中使用的參數資料**SQLExecute**或**SQLExecDirect**，或將資料行資料時使用資料列遭到更新或加入呼叫**SQLBulkOperations**所呼叫或更新**SQLSetPos**。 在執行階段**SQLParamData**傳回的資料指標的驅動程式需要應用程式。  
  
 當應用程式呼叫**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**，驅動程式會傳回 SQL_NEED_如果在需要資料在執行資料的資料。 然後應用程式呼叫**SQLParamData**來決定要傳送的資料。 如果驅動程式需要參數的資料，驅動程式會傳回在 *\*ValuePtrPtr*輸出緩衝處理的應用程式放在資料列集緩衝區中的值。 應用程式可以使用此值來判斷哪一個驅動程式要求的參數資料。 如果驅動程式需要資料行的資料，驅動程式會傳回在 *\*ValuePtrPtr*緩衝區資料行原本繫結，如下所示的位址：  
  
 *繫結位址* + *繫結位移*+ ((*資料列號碼*– 1) x*項目大小*)  
  
 下表所示，其中會定義變數。  
  
|變數|Description|  
|--------------|-----------------|  
|*繫結位址*|使用指定的位址*TargetValuePtr*引數中的**SQLBindCol**。|  
|*繫結位移*|SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性具有指定的位址儲存的值。|  
|*資料列數目*|1 為基底的資料列集中的資料列數目。 單一資料列擷取，也就是預設值，這會是 1。|  
|*項目大小*|資料和長度/指標緩衝區的 SQL_ATTR_ROW_BIND_TYPE 陳述式屬性的值。|  
  
 它也會傳回 SQL_NEED_DATA，這是應用程式，則它應該呼叫的指標**SQLPutData**傳送資料。  
  
 應用程式會呼叫**SQLPutData**視資料行或參數的資料在執行資料傳送的次數。 資料行或參數傳送的所有資料之後，應用程式呼叫**SQLParamData**一次。 如果**SQLParamData**再次傳回 SQL_NEED_DATA，必須將資料傳送另一個參數或資料行。 因此，在應用程式會呼叫**SQLPutData**。 如果所有資料在執行傳送資料的所有參數或資料行，然後**SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 中的值 *\*ValuePtrPtr*未定義，而且可以執行的 SQL 陳述式或**SQLBulkOperations**或**SQLSetPos**可以處理呼叫。  
  
 如果**SQLParamData**搜尋的提供參數資料的 update 或 delete 陳述式，不會影響任何資料來源，呼叫端的資料列**SQLParamData**傳回 sql_no_data 為止。  
  
 在陳述式執行階段傳遞如何資料在執行參數資料的詳細資訊，請參閱 < 傳遞參數值 > 中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。 更新或加入如何資料在執行資料行資料的詳細資訊，請參閱 「 使用 SQLSetPos 」 一節中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)，「 執行大量更新使用中的書籤" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[Long 資料和 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
 **SQLParamData**可以呼叫以擷取資料流的輸出參數。 當**SQLMoreResults**， **SQLExecute**， **SQLGetData**，或**SQLExecDirect**傳回 SQL_PARAM_DATA_AVAILABLE，呼叫**SQLParamData**來判斷哪一個參數可用值。 如需 SQL_PARAM_DATA_AVAILABLE 和資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至參數的緩衝區|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|陳述式中傳回參數的相關資訊|[SQLDescribeParam 函式](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳送參數資料在執行階段|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
