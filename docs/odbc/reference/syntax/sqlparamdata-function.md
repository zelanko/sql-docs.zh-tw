---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ffba9afd0609bab57cdaa182b650f7bd5a0fb34
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47606813"
---
# <a name="sqlparamdata-function"></a>SQLParamData 函式
**合規性**  
 版本導入： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLParamData**可搭配使用**SQLPutData**來提供參數資料在陳述式執行時，與**SQLGetData**來擷取資料流的輸出參數資料。  
  
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
 [輸出]緩衝區中要傳回的位址指標*ParameterValuePtr*中所指定的緩衝區**SQLBindParameter** （適用於參數的資料） 或位址*TargetValuePtr*中指定的緩衝區**SQLBindCol** （適用於資料行的資料），人事 SQL_DESC_DATA_PTR 描述項記錄欄位。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR、 SQL_INVALID_HANDLE，還是 SQL_PARAM_DATA_AVAILABLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLParamData**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLParamData** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|所識別的資料值*ValueType*中的引數**SQLBindParameter**繫結的參數無法轉換成資料類型所識別的*ParameterType*中的引數**SQLBindParameter**。<br /><br /> 資料傳回的值繫結為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT 無法轉換成所識別的資料型別參數*ValueType*中的引數**SQLBindParameter**。<br /><br /> （如果無法轉換一或多個資料列的資料值，但一或多個資料列已成功地傳回，此函式會傳回 SQL_SUCCESS_WITH_INFO。）|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22026|字串資料，長度不符|SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo** "Y"，並於指定長度的參數 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型） 傳送較少的資料具有*StrLen_or_IndPtr*中的引數**SQLBindParameter**。<br /><br /> SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo**是"Y"，以及比中已指定，將已傳送長資料行 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型） 的較少的資料對應到已加入或更新的資料列中的資料行長度的緩衝區**SQLBulkOperations**或更新的**SQLSetPos**。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*; 呼叫的函式已再一次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 先前的函式呼叫不是呼叫**SQLExecDirect**， **SQLExecute**， **SQLBulkOperations**，或**SQLSetPos**位置程式碼在 SQL_NEED_DATA，或是先前的函式呼叫的呼叫會傳回**SQLPutData**。<br /><br /> 先前的函式呼叫已呼叫**SQLParamData**。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLParamData**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*和傳回的 SQL_NEED_DATA。 **SQLCancel**呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 至對應的磁碟機*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
 如果**SQLParamData**稱為時傳送的 SQL 陳述式參數的資料，它會傳回任何可執行陳述式所呼叫的函式所傳回的 SQLSTATE (**SQLExecute** 或**SQLExecDirect**)。 如果呼叫傳送的資料行的資料時正在更新或加上**SQLBulkOperations**或更新**SQLSetPos**，它會傳回任何可傳回的 SQLSTATE **SQLBulkOperations**或是**SQLSetPos**。  
  
## <a name="comments"></a>註解  
 **SQLParamData**可以呼叫以提供兩種用途的資料在執行資料： 將用於呼叫的參數資料**SQLExecute**或**SQLExecDirect**，或資料行的資料將會使用的時機資料列更新或新增藉由呼叫**SQLBulkOperations**或更新的呼叫所**SQLSetPos**。 在執行階段**SQLParamData**傳回的資料指標的驅動程式需要應用程式。  
  
 當應用程式呼叫**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**，驅動程式會傳回 SQL_NEED_如果在需要資料在執行資料的資料。 應用程式，然後呼叫**SQLParamData**來決定要傳送的資料。 如果驅動程式需要參數的資料，驅動程式會傳回在 *\*ValuePtrPtr*輸出緩衝處理的應用程式放在資料列集的緩衝區中的值。 應用程式可以使用此值來判斷哪一個驅動程式要求的參數資料。 如果驅動程式需要的資料行資料，驅動程式會傳回在 *\*ValuePtrPtr*緩衝區資料行原本繫結，如下所示的位址：  
  
 *繫結位址* + *繫結位移*+ ((*資料列編號*– 1) x*項目大小*)  
  
 下表所示，其中會定義變數。  
  
|變數|描述|  
|--------------|-----------------|  
|*繫結位址*|使用指定的地址*TargetValuePtr*中的引數**SQLBindCol**。|  
|*繫結位移*|SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性與指定的位址儲存的值。|  
|*資料列數目*|1 為基底的資料列集中的資料列數目。 針對單一資料列擷取，也就是預設值，這會是 1。|  
|*項目大小*|資料和長度/指標緩衝區的 SQL_ATTR_ROW_BIND_TYPE 陳述式屬性的值。|  
  
 它也會傳回 SQL_NEED_DATA，這是應用程式，它應該呼叫指示器**SQLPutData**來傳送資料。  
  
 應用程式會呼叫**SQLPutData**所需的資料在執行資料的資料行或參數傳送的次數。 資料行或參數傳送的所有資料之後，應用程式會呼叫**SQLParamData**一次。 如果**SQLParamData**一次會傳回 SQL_NEED_DATA，必須將資料傳送另一個參數或資料行。 因此，應用程式會再次呼叫**SQLPutData**。 如果所有資料在執行資料已都傳送的所有參數或資料行，然後**SQLParamData** SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 中的值會傳回 *\*ValuePtrPtr*是未定義，而且可以執行的 SQL 陳述式或**SQLBulkOperations**或是**SQLSetPos**可以處理呼叫。  
  
 如果**SQLParamData**提供的參數資料搜尋的 update 或 delete 陳述式，並不會影響任何資料來源，呼叫端的資料列**SQLParamData**傳回 sql_no_data 為止。  
  
 陳述式執行階段會傳遞如何資料在執行參數資料的詳細資訊，請參閱 「 傳遞參數值 」 中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)並[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。 更新或新增如何資料在執行資料行資料的詳細資訊，請參閱 「 使用 SQLSetPos 」 一節中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)、 「 執行大量更新使用中的書籤 」 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，並[長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
 **SQLParamData**可以呼叫以擷取資料流的輸出參數。 當**SQLMoreResults**， **SQLExecute**， **SQLGetData**，或**SQLExecDirect**傳回 SQL_PARAM_DATA_AVAILABLE，呼叫**SQLParamData**來判斷哪一個參數提供的值。 如需有關 SQL_PARAM_DATA_AVAILABLE 和資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
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
|在執行階段傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
