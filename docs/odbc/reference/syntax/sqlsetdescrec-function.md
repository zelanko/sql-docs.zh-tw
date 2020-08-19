---
description: SQLSetDescRec 函式
title: SQLSetDescRec 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8f0e423de06acf82e6c883531514c57c29d9407
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421122"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 函式
**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLSetDescRec**函數會設定多個描述元欄位，這些欄位會影響系結至資料行或參數資料的資料類型和緩衝區。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetDescRec(  
      SQLHDESC      DescriptorHandle,  
      SQLSMALLINT   RecNumber,  
      SQLSMALLINT   Type,  
      SQLSMALLINT   SubType,  
      SQLLEN        Length,  
      SQLSMALLINT   Precision,  
      SQLSMALLINT   Scale,  
      SQLPOINTER    DataPtr,  
      SQLLEN *      StringLengthPtr,  
      SQLLEN *      IndicatorPtr);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 輸出描述項控制碼。 這不得為 IRD 控制碼。  
  
 *RecNumber*  
 輸出指出包含要設定之欄位的描述項記錄。 描述項記錄是從0開始編號，記錄號碼0是書簽記錄。 此引數必須等於或大於0。 如果 *RecNumber* 大於 SQL_DESC_COUNT 的值，SQL_DESC_COUNTis 變更為 *RecNumber*的值。  
  
 *型別*  
 輸出要將描述項記錄的 SQL_DESC_TYPE 欄位設定成的值。  
  
 *亞*  
 輸出對於類型為 SQL_DATETIME 或 SQL_INTERVAL 的記錄，這是要設定 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的值。  
  
 *長度*  
 輸出要將描述項記錄的 SQL_DESC_OCTET_LENGTH 欄位設定成的值。  
  
 *有效位數*  
 輸出要將描述項記錄的 SQL_DESC_PRECISION 欄位設定成的值。  
  
 *縮放比例*  
 輸出要將描述項記錄的 SQL_DESC_SCALE 欄位設定成的值。  
  
 *DataPtr*  
 [延遲的輸入或輸出]要將描述項記錄的 SQL_DESC_DATA_PTR 欄位設定成的值。 *DataPtr* 可以設定為 null 指標。  
  
 *DataPtr*引數可以設定為 null 指標，將 SQL_DESC_DATA_PTR 欄位設定為 null 指標。 如果 *DescriptorHandle* 引數中的控制碼與 ARD 相關聯，這會將資料行解除系結。  
  
 *StringLengthPtr*  
 [延遲的輸入或輸出]要將描述項記錄的 SQL_DESC_OCTET_LENGTH_PTR 欄位設定成的值。 *StringLengthPtr* 可以設定為 null 指標，將 SQL_DESC_OCTET_LENGTH_PTR 欄位設定為 null 指標。  
  
 *IndicatorPtr*  
 [延遲的輸入或輸出]要將描述項記錄的 SQL_DESC_INDICATOR_PTR 欄位設定成的值。 *IndicatorPtr* 可以設定為 null 指標，將 SQL_DESC_INDICATOR_PTR 欄位設定為 null 指標。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescRec**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DESC）和*DescriptorHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLSetDescRec** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07009|描述元索引無效|*RecNumber*引數設定為0，而*DESCRIPTORHANDLE*則參考 IPD 把手。<br /><br /> *RecNumber*引數小於0。<br /><br /> *RecNumber*引數大於資料來源可支援的資料行或參數的最大數目，而*DescriptorHandle*引數為 APD、IPD 或 ARD。<br /><br /> *RecNumber*引數等於0，而*DescriptorHandle*引數則參考隱含配置的 APD。  (不知道明確配置的應用程式描述項，就不會發生此錯誤，因為在執行時間之前，明確配置的應用程式描述項是否為 APD 或 ARD。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) *DescriptorHandle* 與非同步執行函式的 *StatementHandle* 相關聯 (未呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**是針對與*StatementHandle*相關聯並傳回 SQL_NEED_DATA 的*DescriptorHandle*所呼叫。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式，是與 *DescriptorHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLSetDescRec** 函式時，此 aynchronous 函數仍在執行中。<br /><br /> 針對與*DescriptorHandle*相關聯的其中一個語句控制碼呼叫 (DM) **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY016|無法修改實資料列描述項|*DescriptorHandle*引數與 IRD 相關聯。|  
|HY021|不一致的描述項資訊|*類型*欄位或與描述項中的 SQL_DESC_TYPE 欄位相關聯的任何其他欄位無效或一致。<br /><br /> 一致性檢查期間檢查的描述項資訊不一致。  (請參閱本節後面的「一致性檢查」。 ) |  
|HY090|不正確字串或緩衝區長度| (DM) *驅動程式是 ODBC 2.x* 驅動程式、描述元為 ARD、 *ColumnNumber* 引數設定為0，且為引數 *BufferLength* 指定的值不等於4。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *DescriptorHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫 **SQLSetDescRec** 來設定單一資料行或參數的下欄欄位：  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE (，其類型為 SQL_DATETIME 或 SQL_INTERVAL 的記錄)   
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  如果呼叫 **SQLSetDescRec** 失敗，則由 *RecNumber* 引數所識別之描述項記錄的內容未定義。  
  
 系結資料行或參數時， **SQLSetDescRec** 可讓您變更多個影響系結的欄位，而不需要呼叫 **SQLBindCol** 或 **SQLBindParameter** ，或對 **SQLSetDescField**進行多次呼叫。 **SQLSetDescRec** 可以在目前未與語句相關聯的描述項上設定欄位。 請注意， **SQLBindParameter** 會設定比 **SQLSetDescRec**更多的欄位，可以在一個呼叫中同時設定 APD 和 IPD 的欄位，而不需要描述項控制碼。  
  
> [!NOTE]  
>  您應該一律先設定語句屬性 SQL_ATTR_USE_BOOKMARKS，然後再呼叫*RecNumber*引數為0的**SQLSetDescRec** ，以設定書簽欄位。 雖然這不是強制性的，但強烈建議您這樣做。  
  
## <a name="consistency-checks"></a>一致性檢查  
 當應用程式設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式會自動執行一致性檢查。 如果有任何欄位與其他欄位不一致， **SQLSetDescRec** 會傳回 SQLSTATE HY021 (不一致的描述項資訊) 。  
  
 每當應用程式設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式都會檢查 SQL_DESC_TYPE 欄位的值以及適用于該 SQL_DESC_TYPE 欄位的值是否有效且一致。 當呼叫 **SQLBindParameter** 或 **SQLBindCol** 時，或針對 APD、ARD 或 IPD 呼叫 **SQLSetDescRec** 時，一律會執行這項檢查。 這項一致性檢查包含下列對描述項欄位的檢查：  
  
-   SQL_DESC_TYPE 欄位必須是其中一個有效的 ODBC C 或 SQL 類型，或是驅動程式特定的 SQL 類型。 SQL_DESC_CONCISE_TYPE 欄位必須是其中一個有效的 ODBC C 或 SQL 類型，或是驅動程式專屬的 C 或 SQL 類型，包括簡潔的日期時間和間隔類型。  
  
-   如果 SQL_DESC_TYPE 記錄欄位是 SQL_DATETIME 或 SQL_INTERVAL，則 SQL_DESC_DATETIME_INTERVAL_CODE 欄位必須是有效的日期時間或間隔碼之一。  (在 [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中查看 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的描述。 )   
  
-   如果 SQL_DESC_TYPE 欄位指出數數值型別，則 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位會驗證為有效。  
  
-   如果 SQL_DESC_CONCISE_TYPE 欄位是時間或時間戳記資料類型、具有秒元件的間隔類型，或是具有時間元件的間隔資料類型之一，則會將 SQL_DESC_PRECISION 欄位驗證為有效的秒數有效位數。  
  
-   如果 SQL_DESC_CONCISE_TYPE 是間隔資料類型，則會將 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位驗證為有效的間隔前置精確度值。  
  
 IPD 的 SQL_DESC_DATA_PTR 欄位通常不會設定;不過，應用程式可以這樣做，以強制執行 IPD 欄位的一致性檢查。 無法在 IRD 上執行一致性檢查。 **SQLGetDescField**或**SQLGetDescRec**的呼叫不會實際儲存 IPD 的 SQL_DESC_DATA_PTR 欄位，而且無法透過呼叫來抓取此值;這項設定只會強制執行一致性檢查。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|系結資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|系結參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得單一描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
