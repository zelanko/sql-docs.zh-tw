---
title: SQLSetDescRec 功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299528"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 函式
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLSetDescRec**函數設置多個描述符欄位,這些描述符欄位會影響綁定到列或參數資料的數據類型和緩衝區。  
  
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
 [輸入]描述符句柄。 這不能是 IRD 句柄。  
  
 *RecNumber*  
 [輸入]指示包含要設置的欄位的描述符記錄。 描述符記錄從 0 編號,記錄編號 0 是書籤記錄。 此參數必須等於或大於 0。 如果*RecNumber*大於SQL_DESC_COUNT的值,SQL_DESC_COUNTis變更為*RecNumber*的值 。  
  
 *型別*  
 [輸入]要為描述符記錄設置SQL_DESC_TYPE欄位的值。  
  
 *亞*  
 [輸入]對於類型為SQL_DATETIME或SQL_INTERVAL的記錄,這是要設置SQL_DESC_DATETIME_INTERVAL_CODE欄位的值。  
  
 *長度*  
 [輸入]要為描述符記錄設置SQL_DESC_OCTET_LENGTH欄位的值。  
  
 *精度*  
 [輸入]要為描述符記錄設置SQL_DESC_PRECISION欄位的值。  
  
 *調整*  
 [輸入]要為描述符記錄設置SQL_DESC_SCALE欄位的值。  
  
 *資料Ptr*  
 【 延遲輸入或輸出 】要為描述符記錄設置SQL_DESC_DATA_PTR欄位的值。 *DataPtr*可以設置為空指標。  
  
 *DataPtr*參數可以設置為空指標,以將SQL_DESC_DATA_PTR欄位設置為空指標。 如果*描述符處理*參數中的句柄與 ARD 關聯,則取消綁定列。  
  
 *字串長度 Ptr*  
 【 延遲輸入或輸出 】要為描述符記錄設置SQL_DESC_OCTET_LENGTH_PTR欄位的值。 *可以將 StringLengthPtr*設置為空指標,以將SQL_DESC_OCTET_LENGTH_PTR欄位設置為空指標。  
  
 *指標Ptr*  
 【 延遲輸入或輸出 】要為描述符記錄設置SQL_DESC_INDICATOR_PTR欄位的值。 *指標Ptr*可以設置為空指標,以將SQL_DESC_INDICATOR_PTR欄位設置為空指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescRec**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_DESC的*句柄類型*和*描述符句柄*。 下表列出了**SQLSetDescRec**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07009|不合法的描述符索引|*RecNumber*參數設定為 0,*描述符句柄*引用 IPD 句柄。<br /><br /> *RecNumber*參數小於 0。<br /><br /> *RecNumber*參數大於資料來源可以支援的最大欄或參數數,並且*描述符句柄*參數是 APD、IPD 或 ARD。<br /><br /> *RecNumber*參數等於 0,*描述符句柄*參數引用隱式分配的 APD。 (顯式分配的應用程式描述符不會發生此錯誤,因為在執行時間之前,不知道顯式分配的應用程式描述符是 APD 還是 ARD。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM)*描述符處理*與*語句句柄*相關聯,在調用此函數時,調用了非同步執行函數(不是此函數),並且仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*,其中*描述符句柄*SQL_NEED_DATA關聯並返回。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 對於與*描述符句柄*關聯的連接句柄,調用了非同步執行函數。 調用**SQLSetDescRec**函數時,此 aynchronous 函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被呼叫為與*描述符句柄*關聯的語句句柄**SQLExecute**之一,並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY016|無法變更行描述子|*描述符處理*參數與 IRD 相關聯。|  
|HY021|描述符資訊不一致|*"類型'* 欄位或與描述符中SQL_DESC_TYPE欄位關聯的任何其他欄位無效或一致。<br /><br /> 在一致性檢查期間檢查的描述符資訊不一致。 (請參閱本節後面的"一致性檢查"。|  
|HY090|不合法的字串或緩衝區長度|(DM) 驅動程式是 ODBC *2.x*驅動程式,描述符是 ARD,*列號*參數設置為 0,為參數*BufferLength*指定的值不等於 4。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*描述符處理*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLSetDescRec**為單列或參數設定以下欄位:  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE(對於其類型為SQL_DATETIME或SQL_INTERVAL的記錄)  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  如果對**SQLSetDescRec**的呼叫失敗,則*RecNumber*參數標識的描述符記錄的內容將未定義。  
  
 綁定列或參數時 **,SQLSetDescCRec**允許您更改影響綁定的多個字段,而無需調用**SQLBindCol**或**SQLBind 參數**或對**SQLSetDescField**進行多次調用。 **SQLSetDescRec**可以在描述符上設置當前未與語句關聯的欄位。 請注意 **,SQLBind參數**設置的欄位比**SQLSetDescRec**多,可以在一個調用中同時設置 APD 和 IPD 上的欄位,並且不需要描述符句柄。  
  
> [!NOTE]  
>  在調用使用*RecNumber*參數為 0 的**SQLSetDescRec**來設置書籤欄位之前,應始終設置語句屬性SQL_ATTR_USE_BOOKMARKS。 雖然這不是強制性的,但強烈建議這樣做。  
  
## <a name="consistency-checks"></a>一致性檢查  
 每當應用程式設定 APD、ARD 或 IPD 的SQL_DESC_DATA_PTR欄位時,驅動程式會自動執行一致性檢查。 如果任何欄位與其他欄位不一致 **,SQLSetDescRec**將返回 SQLSTATE HY021(描述符資訊不一致)。  
  
 每當應用程式設定 APD、ARD 或 IPD SQL_DESC_DATA_PTR欄位時,驅動程式都會檢查SQL_DESC_TYPE欄位的值以及適用於該SQL_DESC_TYPE欄位的值是否有效且一致。 當調用**SQLBind 參數**或**SQLBindCol**或調用**SQLSetDescRec**進行 APD、ARD 或 IPD 時,始終執行此檢查。 此一致性檢查包括以下對描述符位的檢查:  
  
-   SQL_DESC_TYPE欄位必須是有效的 ODBC C 或 SQL 類型之一,或者特定於驅動程式的 SQL 類型。 SQL_DESC_CONCISE_TYPE欄位必須是有效的 ODBC C 或 SQL 類型之一,或特定於驅動程式的 C 或 SQL 類型,包括簡潔的日期時間和間隔類型。  
  
-   如果SQL_DESC_TYPE記錄欄位是SQL_DATETIME或SQL_INTERVAL,則SQL_DESC_DATETIME_INTERVAL_CODE欄位必須是有效的日期時間或間隔代碼之一。 (請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中SQL_DESC_DATETIME_INTERVAL_CODE欄位的說明。  
  
-   如果SQL_DESC_TYPE欄位指示數值類型,則SQL_DESC_PRECISION和SQL_DESC_SCALE欄位將驗證為有效。  
  
-   如果SQL_DESC_CONCISE_TYPE欄位是時間戳資料類型、具有秒分量的間隔類型或具有時間分量的間隔數據類型之一,則SQL_DESC_PRECISION欄位將驗證為有效的秒精度。  
  
-   如果SQL_DESC_CONCISE_TYPE是間隔數據類型,則SQL_DESC_DATETIME_INTERVAL_PRECISION欄位將驗證為有效的間隔前導精度值。  
  
 通常不設置 IPD 的SQL_DESC_DATA_PTR欄位;但是,應用程式可以這樣做來強制對 IPD 欄位進行一致性檢查。 無法對 IRD 執行一致性檢查。 IPD 的SQL_DESC_DATA_PTR欄位的值實際上未儲存,並且無法透過呼叫**SQLGetDescField**或**SQLGetDescRec**檢索該值。設置僅用於強制一致性檢查。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|繫結欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|繫結參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得單一描述符欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得多個描述符位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一描述符欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
