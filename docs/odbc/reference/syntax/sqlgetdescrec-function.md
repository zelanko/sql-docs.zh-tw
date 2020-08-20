---
description: SQLGetDescRec 函式
title: SQLGetDescRec 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5237d8b1a1d070752219abd22936615060371a89
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461048"
---
# <a name="sqlgetdescrec-function"></a>SQLGetDescRec 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetDescRec** 會傳回描述項記錄中多個欄位的目前設定或值。 傳回的欄位會描述資料行或參數資料的名稱、資料類型和儲存。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 輸出描述項控制碼。  
  
 *RecNumber*  
 輸出指出應用程式用來搜尋資訊的描述項記錄。 描述項記錄的編號是1，記錄號碼0是書簽記錄。 *RecNumber*引數必須小於或等於 SQL_DESC_COUNT 的值。 如果 *RecNumber* 小於或等於 SQL_DESC_COUNT 但資料列未包含資料行或參數的資料，則對 **SQLGetDescRec** 的呼叫會傳回欄位的預設值。  (需詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「初始化描述項欄位」。 )   
  
 *名稱*  
 出緩衝區的指標，此緩衝區會傳回描述項記錄的 SQL_DESC_NAME 欄位。  
  
 如果 *Name* 為 Null， *StringLengthPtr* 仍會傳回字元總數 (排除字元資料的 Null 終止字元) 可在 *名稱*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出**名稱* 緩衝區的長度（以字元為單位）。  
  
 *StringLengthPtr*  
 出緩衝區的指標，此緩衝區會傳回可在名稱緩衝區中傳回的資料字元數目，不 \* *Name*包括 null 終止字元。 如果字元數大於或等於*BufferLength*，則名稱中的資料 \* *Name*會截斷為*BufferLength*減去 null 終止字元的長度，而且由驅動程式以 null 終止。  
  
 *TypePtr*  
 出緩衝區的指標，此緩衝區會傳回描述項記錄之 SQL_DESC_TYPE 欄位的值。  
  
 *SubTypePtr*  
 出對於類型為 SQL_DATETIME 或 SQL_INTERVAL 的記錄，這是要傳回 SQL_DESC_DATETIME_INTERVAL_CODE 欄位值之緩衝區的指標。  
  
 *LengthPtr*  
 出緩衝區的指標，此緩衝區會傳回描述項記錄之 SQL_DESC_OCTET_LENGTH 欄位的值。  
  
 *PrecisionPtr*  
 出緩衝區的指標，此緩衝區會傳回描述項記錄之 SQL_DESC_PRECISION 欄位的值。  
  
 *ScalePtr*  
 出緩衝區的指標，此緩衝區會傳回描述項記錄之 SQL_DESC_SCALE 欄位的值。  
  
 *NullablePtr*  
 出緩衝區的指標，此緩衝區會傳回描述項記錄之 SQL_DESC_NullABLE 欄位的值。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
 如果 *RecNumber* 大於目前的描述項記錄數目，就會傳回 SQL_NO_DATA。  
  
 如果 *DescriptorHandle* 是 IRD 控制碼，且語句處於已備妥或已執行的狀態，但沒有與其相關聯的開啟資料指標，則會傳回 SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescRec**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DESC）和*DescriptorHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLGetDescRec** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *名稱*不夠大，無法傳回整個描述項欄位。 因此，欄位已被截斷。 Untruncated 描述項欄位的長度會在 **StringLengthPtr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07009|描述元索引無效|*FieldIdentifier*引數是記錄欄位、 *RecNumber*引數設定為0，而*DescriptorHandle*引數是 IPD 控制碼。<br /><br />  (DM) *RecNumber* 引數設定為0，且 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_OFF，且 *DescriptorHandle* 引數為 IRD 控制碼。<br /><br /> *RecNumber*引數小於0。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY007|未準備相關聯的語句|*DescriptorHandle* 與 IRD 相關聯，且相關聯的語句控制碼未處於已備妥或已執行的狀態。|  
|HY010|函數順序錯誤| (DM) *DescriptorHandle* 與非同步執行函式的 *StatementHandle* 相關聯 (未呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) *DescriptorHandle* 與 *StatementHandle* 相關聯，而該會呼叫 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式，是與 *DescriptorHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLGetDescRec** 時，這個非同步函數仍在執行中。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *DescriptorHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫 **SQLGetDescRec** 來取得單一資料行或參數的下列描述項欄位值：  
  
-   SQL_DESC_NAME  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (，其類型為 SQL_DATETIME 或 SQL_INTERVAL 的記錄)   
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_NULLABLE  
  
 **SQLGetDescRec** 不會取出標頭欄位的值。  
  
 應用程式可以將對應至欄位的引數設定為 null 指標，以防止傳回欄位的設定。  
  
 當應用程式呼叫 **SQLGetDescRec** 來抓取特定描述項類型未定義之欄位的值時，此函式會傳回 SQL_SUCCESS 但未定義為欄位傳回的值。 例如，針對 APD 或 ARD 的 SQL_DESC_NAME 或 SQL_DESC_NullABLE 欄位呼叫 **SQLGetDescRec** ，將會傳回 SQL_SUCCESS 但未定義的欄位值。  
  
 當應用程式呼叫 **SQLGetDescRec** 來取得針對特定描述項類型所定義的欄位值，但沒有預設值，而且尚未設定時，此函數會傳回 SQL_SUCCESS 但未定義針對欄位傳回的值。 如需詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「描述項欄位的初始化」。  
  
 欄位的值也可以透過呼叫 **SQLGetDescField**來個別取出。 如需描述項標頭或記錄中欄位的描述，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。 如需描述項的詳細資訊，請參閱 [描述](../../../odbc/reference/develop-app/descriptors.md)項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|系結資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|系結參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
