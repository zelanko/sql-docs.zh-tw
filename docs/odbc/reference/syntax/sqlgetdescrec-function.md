---
title: "SQLGetDescRec 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescRec
helpviewer_keywords:
- SQLGetDescRec function [ODBC]
ms.assetid: 325e0907-8e87-44e8-a111-f39e636a9cbc
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c40e0e26ada07854f6772389ed09fc39e092952e
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetDescRec**傳回目前的設定或多個欄位的描述項記錄的值。 傳回的欄位描述的名稱、 資料類型和儲存的資料行或參數的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetDescRec(  
      SQLHDESC        DescriptorHandle,  
      SQLSMALLINT     RecNumber,  
      SQLCHAR *       Name,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLSMALLINT *   TypePtr,  
      SQLSMALLINT *   SubTypePtr,  
      SQLLEN *        LengthPtr,  
      SQLSMALLINT *   PrecisionPtr,  
      SQLSMALLINT *   ScalePtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述項控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的描述項記錄。 描述項記錄編號 1，以記錄編號 0 的書籤記錄。 *RecNumber*引數必須是小於或等於 SQL_DESC_COUNT 的值。 如果*RecNumber*小於或等於 SQL_DESC_COUNT 但資料列不包含資料的資料行或參數，呼叫**SQLGetDescRec**會傳回欄位的預設值。 (如需詳細資訊，請參閱 「 初始設定的描述元的欄位 」 中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
 *名稱*  
 [輸出]這是要傳回 SQL_DESC_NAME 欄位的描述項記錄的緩衝區指標。  
  
 如果*名稱*是 NULL， *StringLengthPtr*仍會傳回的總字元數 （不含字元資料 null 結束字元） 可用來傳回所指向之緩衝區中*名稱*。  
  
 *Columnsize*  
 [輸入]長度 **名稱*緩衝區，以字元為單位。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的資料可用來傳回中的字元數目的緩衝區的指標\**名稱*緩衝區，但不包括 null 結束字元。 字元數目是否大於或等於*Columnsize*中的資料\**名稱*會被截斷成*Columnsize*減的長度null 結束字元，而且是以 null 結束的驅動程式。  
  
 *TypePtr*  
 [輸出]傳回描述項記錄的 SQL_DESC_TYPE 欄位值的緩衝區指標。  
  
 *SubTypePtr*  
 [輸出]型別是 SQL_DATETIME 或 SQL_INTERVAL 記錄，這是傳回 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的值的緩衝區的指標。  
  
 *LengthPtr*  
 [輸出]傳回描述項記錄的 SQL_DESC_OCTET_LENGTH 欄位值的緩衝區指標。  
  
 *PrecisionPtr*  
 [輸出]傳回描述項記錄的 SQL_DESC_PRECISION 欄位值的緩衝區指標。  
  
 *ScalePtr*  
 [輸出]傳回描述項記錄的 SQL_DESC_SCALE 欄位值的緩衝區指標。  
  
 *NullablePtr*  
 [輸出]傳回描述項記錄的 SQL_DESC_NULLABLE 欄位值的緩衝區指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 sql_no_data 為止或 SQL_INVALID_HANDLE。  
  
 如果，則會傳回 SQL_NO_DATA *RecNumber*大於目前的描述項記錄數目。  
  
 如果，則會傳回 SQL_NO_DATA *DescriptorHandle* IRD 的控制代碼和陳述式是在已備妥或已執行狀態但沒有任何與其相關聯的開啟資料指標。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescRec**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_DESC 和*處理*的*DescriptorHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetDescRec** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\**名稱*仍不夠大，無法傳回整個描述項欄位。 因此，此欄位被截斷。 中會傳回未截斷的描述項欄位的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|無效的描述元索引|*FieldIdentifier*引數就是記錄 欄位中， *RecNumber*引數設定為 0，而*DescriptorHandle*引數以前是 IPD 控制代碼。<br /><br /> (DM) *RecNumber*引數設定為 0，並且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF，而*DescriptorHandle*引數以前是 IRD 控制代碼。<br /><br /> *RecNumber*引數為小於 0。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY007|相關的陳述式未準備好|*DescriptorHandle*聯 IRD 和相關聯的陳述式控制代碼不是處於已備妥或已執行狀態。|  
|HY010|函數順序錯誤|(DM) *DescriptorHandle*與*StatementHandle*以非同步方式執行的函式 （不這一個） 的呼叫和還在執行時呼叫此函式。<br /><br /> (DM) *DescriptorHandle*與*StatementHandle*其**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**已呼叫而傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*DescriptorHandle*。 此非同步函式還在執行時**SQLGetDescRec**呼叫。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*DescriptorHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLGetDescRec**來擷取單一資料行或參數的下列描述項欄位的值：  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE （適用於記錄型別是 SQL_DATETIME 或 SQL_INTERVAL）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec**不會擷取標頭欄位的值。  
  
 應用程式可以將對應的引數設定為 null 指標的欄位，以避免傳回欄位的設定值。  
  
 當應用程式呼叫**SQLGetDescRec**若要擷取特定的描述元類型未定義欄位的值，此函數會傳回 SQL_SUCCESS，但是傳回欄位的值為未定義。 例如，呼叫**SQLGetDescRec** APD 或 ARD SQL_DESC_NAME 或 SQL_DESC_NULLABLE 欄位將會傳回 SQL_SUCCESS，但未定義欄位的值。  
  
 當應用程式呼叫**SQLGetDescRec**若要擷取的欄位，為特定的描述元類型定義，但沒有預設值，而且尚未設定值，此函數會傳回 SQL_SUCCESS，但是傳回值此欄位是未定義。 如需詳細資訊，請參閱 「 初始設定的描述元的欄位 」 中[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 欄位的值可以也個別擷取由呼叫**SQLGetDescField**。 如需描述項標頭或記錄中欄位的說明，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如需描述元的詳細資訊，請參閱[描述元](../../../odbc/reference/develop-app/descriptors.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|資料行繫結|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|將參數繫結|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

