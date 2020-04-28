---
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
ms.openlocfilehash: b29879ff7635d6eb7d5a0f7489ff3994758d4a35
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299528"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 函式
**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLSetDescRec**函數會設定多個描述項欄位，以影響系結至資料行或參數資料的資料類型和緩衝區。  
  
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
 源描述項控制碼。 這不一定是 IRD 控制碼。  
  
 *RecNumber*  
 源指出包含要設定之欄位的描述項記錄。 描述項記錄是從0開始編號，記錄號碼為0，表示書簽記錄。 這個引數必須等於或大於0。 如果*RecNumber*大於 SQL_DESC_COUNT 的值，SQL_DESC_COUNTis 變更為*RecNumber*的值。  
  
 *類型*  
 源要為描述項記錄設定 SQL_DESC_TYPE 欄位的值。  
  
 *類型*  
 源對於其類型為 SQL_DATETIME 或 SQL_INTERVAL 的記錄，這就是要設定 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的值。  
  
 *長度*  
 源要為描述項記錄設定 SQL_DESC_OCTET_LENGTH 欄位的值。  
  
 *有效位數*  
 源要為描述項記錄設定 SQL_DESC_PRECISION 欄位的值。  
  
 *調整*  
 源要為描述項記錄設定 SQL_DESC_SCALE 欄位的值。  
  
 *DataPtr*  
 [延遲輸入或輸出]要為描述項記錄設定 SQL_DESC_DATA_PTR 欄位的值。 *DataPtr*可以設定為 null 指標。  
  
 *DataPtr*引數可以設定為 null 指標，將 SQL_DESC_DATA_PTR 欄位設定為 null 指標。 如果*DescriptorHandle*引數中的控制碼與 ARD 相關聯，就會將該資料行解除系結。  
  
 *StringLengthPtr*  
 [延遲輸入或輸出]要為描述項記錄設定 SQL_DESC_OCTET_LENGTH_PTR 欄位的值。 *StringLengthPtr*可以設定為 null 指標，將 SQL_DESC_OCTET_LENGTH_PTR 欄位設定為 null 指標。  
  
 *IndicatorPtr*  
 [延遲輸入或輸出]要為描述項記錄設定 SQL_DESC_INDICATOR_PTR 欄位的值。 *IndicatorPtr*可以設定為 null 指標，將 SQL_DESC_INDICATOR_PTR 欄位設定為 null 指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescRec**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_DESC *HandleType*和*DescriptorHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出**SQLSetDescRec**常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|不正確描述項索引|*RecNumber*引數已設定為0，而*DescriptorHandle*參考 IPD 控制碼。<br /><br /> *RecNumber*引數小於0。<br /><br /> *RecNumber*引數大於資料來源可以支援的資料行或參數數目上限，而*DescriptorHandle*引數為 APD、IPD 或 ARD。<br /><br /> *RecNumber*引數等於0，而*DescriptorHandle*引數參考了隱含配置的 APD。 （此錯誤不會發生在明確配置的應用程式描述項中，因為不知道明確配置的應用程式描述元是否為 APD 或 ARD 直到執行時間）。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY010|函數順序錯誤|（DM） *DescriptorHandle*已與*StatementHandle*相關聯，其已呼叫非同步執行的函式（而不是這個），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM） **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**已*針對 StatementHandle 相關*聯並傳回 SQL_NEED_DATA 的*DescriptorHandle*呼叫。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。<br /><br /> （DM）已針對與*DescriptorHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLSetDescRec**函式時，此 aynchronous 函數仍在執行中。<br /><br /> 已針對與*DescriptorHandle*相關聯的其中一個語句控制碼呼叫（DM） **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY016|無法修改執行資料列描述項|*DescriptorHandle*引數與 IRD 相關聯。|  
|HY021|不一致的描述項資訊|*類型*欄位，或與描述元中的 SQL_DESC_TYPE 欄位相關聯的任何其他欄位無效或不一致。<br /><br /> 在一致性檢查期間檢查的描述項資訊不一致。 （請參閱本節稍後的「一致性檢查」）。|  
|HY090|不正確字串或緩衝區長度|（DM）*驅動程式是 ODBC 2.x*驅動程式、描述項是 ARD、 *ColumnNumber*引數設定為0，而針對引數*BufferLength*所指定的值不等於4。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*DescriptorHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>評價  
 應用程式可以呼叫**SQLSetDescRec**來設定單一資料行或參數的下欄欄位：  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE （適用于其類型為 SQL_DATETIME 或 SQL_INTERVAL 的記錄）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  如果對**SQLSetDescRec**的呼叫失敗，則*RecNumber*引數所識別之描述項記錄的內容會是未定義的。  
  
 當系結資料行或參數時， **SQLSetDescRec**可讓您變更會影響系結的多個欄位，而不需要呼叫**SQLBindCol**或**SQLBindParameter** ，或對**SQLSetDescField**進行多次呼叫。 **SQLSetDescRec**可以在目前未與語句相關聯的描述項上設定欄位。 請注意， **SQLBindParameter**會設定比**SQLSetDescRec**更多的欄位，可以在單一呼叫中設定 APD 和 IPD 上的欄位，而不需要描述項控制碼。  
  
> [!NOTE]  
>  在呼叫具有0的*RecNumber*引數的**SQLSetDescRec**之前，一定要先設定語句屬性 SQL_ATTR_USE_BOOKMARKS 來設定書簽欄位。 雖然這不是強制性的，但強烈建議您這麼做。  
  
## <a name="consistency-checks"></a>一致性檢查  
 每當應用程式設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式就會自動執行一致性檢查。 如果任何欄位與其他欄位不一致，則**SQLSetDescRec**會傳回 SQLSTATE HY021 （不一致的描述項資訊）。  
  
 每當應用程式設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式會檢查 SQL_DESC_TYPE 欄位的值和適用于該 SQL_DESC_TYPE 欄位的值是否有效且一致。 呼叫**SQLBindParameter**或**SQLBindCol**時，或是針對 APD、ARD 或 IPD 呼叫**SQLSetDescRec**時，一律會執行這種檢查。 此一致性檢查包含下列描述項欄位的檢查：  
  
-   SQL_DESC_TYPE 欄位必須是其中一個有效的 ODBC C 或 SQL 類型，或驅動程式特定的 SQL 類型。 SQL_DESC_CONCISE_TYPE 欄位必須是其中一個有效的 ODBC C 或 SQL 類型，或是驅動程式特定的 C 或 SQL 類型，包括簡潔的 datetime 和 interval 類型。  
  
-   如果 [SQL_DESC_TYPE 記錄] 欄位 SQL_DATETIME 或 SQL_INTERVAL，則 SQL_DESC_DATETIME_INTERVAL_CODE 欄位必須是其中一個有效的日期時間或間隔代碼。 （請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位的描述）。  
  
-   如果 [SQL_DESC_TYPE] 欄位指出數數值型別，則 [SQL_DESC_PRECISION] 和 [SQL_DESC_SCALE] 欄位會驗證為有效。  
  
-   如果 [SQL_DESC_CONCISE_TYPE] 欄位是時間或時間戳記資料類型、具有秒陣列件的間隔類型，或包含時間元件的其中一個間隔資料類型，則 SQL_DESC_PRECISION 欄位會驗證為有效的秒數有效位數。  
  
-   如果 SQL_DESC_CONCISE_TYPE 是間隔資料類型，則 SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位會驗證為有效的間隔前置精確度值。  
  
 IPD 的 SQL_DESC_DATA_PTR 欄位通常不會設定;不過，應用程式可以這樣做，以強制執行 IPD 欄位的一致性檢查。 無法在 IRD 上執行一致性檢查。 IPD 的 SQL_DESC_DATA_PTR 欄位設定為的值實際上並不會儲存，而且無法藉由呼叫**SQLGetDescField**或**SQLGetDescRec**來抓取;此設定只會用來強制執行一致性檢查。  
  
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
