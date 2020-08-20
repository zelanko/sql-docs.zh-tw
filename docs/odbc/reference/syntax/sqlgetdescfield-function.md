---
description: SQLGetDescField 函數
title: SQLGetDescField 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31618ca5283ae6875cb4243cc88e643452cef4d1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461064"
---
# <a name="sqlgetdescfield-function"></a>SQLGetDescField 函數
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetDescField** 會傳回描述項記錄中單一欄位的目前設定或值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 輸出描述項控制碼。  
  
 *RecNumber*  
 輸出指出應用程式用來搜尋資訊的描述項記錄。 描述項記錄是從0開始編號，記錄號碼0是書簽記錄。 如果 *FieldIdentifier* 引數指出標頭欄位，則會忽略 *RecNumber* 。 如果 *RecNumber* 小於或等於 SQL_DESC_COUNT 但資料列未包含資料行或參數的資料，則對 **SQLGetDescField** 的呼叫會傳回欄位的預設值。  (需詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「初始化描述項欄位」。 )   
  
 *FieldIdentifier*  
 輸出表示要傳回其值的描述項欄位。 如需詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「*FieldIdentifier*引數」一節。  
  
 *ValuePtr*  
 出要傳回描述項資訊的緩衝區指標。 資料類型取決於 *FieldIdentifier*的值。  
  
 如果 *ValuePtr* 是整數型別，應用程式應該使用 SQLULEN 的緩衝區，並在呼叫此函式之前將值初始化為0，因為某些驅動程式可能只會寫入較低的32位或16位的緩衝區，而不會讓較高的順序位保持不變。  
  
 如果 *ValuePtr* 為 Null， *StringLengthPtr* 仍會傳回位元組總數 (排除字元資料的 Null 終止字元) 可在 *ValuePtr*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出如果*FieldIdentifier*是 ODBC 定義的欄位，而*ValuePtr*指向字元字串或二進位緩衝區，則這個引數應該是 \* *ValuePtr*的長度。 如果*FieldIdentifier*是 ODBC 定義的欄位，而 \* *ValuePtr*是整數，則會忽略*BufferLength* 。 如果* \* ValuePtr*中的值是 Unicode 資料類型 (在呼叫**SQLGetDescFieldW**) 時， *BufferLength*引數必須是偶數。  
  
 如果 *FieldIdentifier* 是驅動程式定義的欄位，則應用程式會藉由設定 *BufferLength* 引數，將欄位的本質指出至驅動程式管理員。 *BufferLength* 可以有下列值：  
  
-   如果* \* ValuePtr*是字元字串的指標，則*BufferLength*是字串或 SQL_NTS 的長度。  
  
-   如果* \* ValuePtr*是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR (*長度*) 宏的結果放在*BufferLength*中。 這會在 *BufferLength*中放置負數值。  
  
-   如果* \* ValuePtr*是字元字串或二進位字串以外的值指標，則*BufferLength*應該具有 SQL_IS_POINTER 的值。  
  
-   如果* \* ValuePtr*包含固定長度的資料類型，則*BufferLength*會視需要 SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或 SQL_IS_USMALLINT。  
  
 *StringLengthPtr*  
 出要在其中傳回位元組總數的緩衝區指標 (不包括 null 終止字元所需的位元組數目) 可在 **ValuePtr*中傳回。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_NO_DATA 或 SQL_INVALID_HANDLE。  
  
 如果 *RecNumber* 大於目前的描述項記錄數目，就會傳回 SQL_NO_DATA。  
  
 如果 *DescriptorHandle* 是 IRD 控制碼，且語句處於已備妥或已執行的狀態，但沒有與其相關聯的開啟資料指標，則會傳回 SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetDescField**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLGetDescField** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|緩衝區 \* *ValuePtr*不夠大，無法傳回整個描述項欄位，所以欄位已被截斷。 Untruncated 描述項欄位的長度會在 **StringLengthPtr*中傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07009|描述元索引無效| (DM) *RecNumber* 引數等於0、SQL_ATTR_USE_BOOKMARK 語句屬性 SQL_UB_OFF，而且 *DescriptorHandle* 引數是 IRD 控制碼。 只有當描述項與語句控制碼相關聯時，才可以為明確配置的描述項傳回 (此錯誤。 ) <br /><br /> *FieldIdentifier*引數是記錄欄位， *RecNumber*引數為0，而*DescriptorHandle*引數是 IPD 控制碼。<br /><br /> *RecNumber*引數小於0。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY007|未準備相關聯的語句|*DescriptorHandle* 已與 *StatementHandle* 建立關聯，以做為 IRD，且相關聯的語句控制碼尚未準備或執行。|  
|HY010|函數順序錯誤| (DM) *DescriptorHandle* 與非同步執行函式的 *StatementHandle* 相關聯 (未呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) *DescriptorHandle* 與 *StatementHandle* 相關聯，而該會呼叫 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式，是與 *DescriptorHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLGetDescField** 函式時，仍在執行此非同步函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY021|不一致的描述項資訊|[SQL_DESC_TYPE] 和 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位不會形成有效的 ODBC SQL 類型、適用于 Ipd) 的有效驅動程式專屬 SQL (類型，或適用于 Apd 或 ARDs (的有效 ODBC C 類型) 。|  
|HY090|不正確字串或緩衝區長度| (DM) * \* ValuePtr*是一個字元字串，而*BufferLength*小於零。|  
|HY091|不正確描述項欄位識別碼|*FieldIdentifier* 不是 ODBC 定義的欄位，而且不是實值定義的值。<br /><br /> 未定義*DescriptorHandle*的*FieldIdentifier* 。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *DescriptorHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫 **SQLGetDescField** 來傳回描述項記錄的單一欄位值。 對 **SQLGetDescField** 的呼叫可以傳回任何描述元類型中任何欄位的設定，包括標頭欄位、記錄欄位和書簽欄位。 應用程式可以對 **SQLGetDescField**進行重複呼叫，以任意順序取得相同或不同描述項中多個欄位的設定。 您也可以呼叫**SQLGetDescField** ，以傳回驅動程式定義的描述項欄位。  
  
 基於效能考慮，在執行語句之前，應用程式不應該呼叫 IRD 的 **SQLGetDescField** 。  
  
 在 **SQLGetDescRec**的單一呼叫中，也可以取出多個欄位的設定，以描述資料行或參數資料的名稱、資料類型和儲存。 您可以呼叫**SQLGetStmtAttr** ，以傳回描述項標頭中也是語句屬性之單一欄位的設定。 **SQLColAttribute**、 **SQLDescribeCol**和 **SQLDescribeParam** 會傳回記錄或書簽欄位。  
  
 當應用程式呼叫 **SQLGetDescField** 來抓取特定描述項類型未定義之欄位的值時，此函式會傳回 SQL_SUCCESS 但未定義為欄位傳回的值。 例如，針對 APD 或 ARD 的 SQL_DESC_NAME 或 SQL_DESC_NullABLE 欄位呼叫 **SQLGetDescField** ，將會傳回 SQL_SUCCESS 但未定義的欄位值。  
  
 當應用程式呼叫 **SQLGetDescField** 來取得針對特定描述項類型所定義的欄位值，但沒有預設值，而且尚未設定時，此函數會傳回 SQL_SUCCESS 但未定義針對欄位傳回的值。 如需初始化描述項欄位和欄位描述的詳細資訊，請參閱 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的「描述項欄位的初始化」。 如需描述項的詳細資訊，請參閱 [描述](../../../odbc/reference/develop-app/descriptors.md)項。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
