---
title: SQLSetDescRec 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescRec
helpviewer_keywords:
- SQLSetDescRec function [ODBC]
ms.assetid: bf55256c-7eb7-4e3f-97ef-b0fee09ba829
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3a733c2b88954c9937e8a170b949535ffa118bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68039730"
---
# <a name="sqlsetdescrec-function"></a>SQLSetDescRec 函式
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLSetDescRec**函式會將多個會影響資料類型的描述項欄位，而且緩衝區的繫結至資料行或參數資料。  
  
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
 [輸入]描述項控制代碼。 這不能 IRD 控制代碼。  
  
 *RecNumber*  
 [輸入]表示描述項記錄，其中包含要設定的欄位。 描述項記錄編號為 0，0 表示書籤記錄的記錄號碼。 這個引數必須是等於或大於 0。 如果*RecNumber* SQL_DESC_COUNT，SQL_DESC_COUNTis 變更為值的值大於*RecNumber*。  
  
 *型別*  
 [輸入]要用來設定描述項記錄的 SQL_DESC_TYPE 欄位的值。  
  
 *SubType*  
 [輸入]型別是 SQL_DATETIME 或 SQL_INTERVAL 的記錄，這是要用來設定 SQL_DESC_DATETIME_INTERVAL_CODE 欄位的值。  
  
 *長度*  
 [輸入]要用來設定描述項記錄的 SQL_DESC_OCTET_LENGTH 欄位的值。  
  
 *有效位數*  
 [輸入]要用來設定描述項記錄的 SQL_DESC_PRECISION 欄位的值。  
  
 *小數位數*  
 [輸入]要用來設定描述項記錄的 SQL_DESC_SCALE 欄位的值。  
  
 *DataPtr*  
 [延後的輸入或輸出]要用來設定 SQL_DESC_DATA_PTR 欄位的描述項記錄的值。 *DataPtr*可設為 null 指標。  
  
 *DataPtr*引數可以設定為 null 指標，若要設定 SQL_DESC_DATA_PTR 欄位為 null 指標。 如果中的控制代碼*DescriptorHandle*引數為 ARD 相關聯，這會解除繫結資料行。  
  
 *StringLengthPtr*  
 [延後的輸入或輸出]要用來設定描述項記錄的 SQL_DESC_OCTET_LENGTH_PTR 欄位的值。 *StringLengthPtr* SQL_DESC_OCTET_LENGTH_PTR 欄位設為 null 指標可以設為 null 指標。  
  
 *IndicatorPtr*  
 [延後的輸入或輸出]要用來設定描述項記錄的 SQL_DESC_INDICATOR_PTR 欄位的值。 *IndicatorPtr* SQL_DESC_INDICATOR_PTR 欄位設為 null 指標可以設為 null 指標。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescRec**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_DESC 並*處理*的*DescriptorHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetDescRec** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|描述項索引無效|*RecNumber*引數設定為 0，而*DescriptorHandle*指 IPD 控點。<br /><br /> *RecNumber*引數為小於 0。<br /><br /> *RecNumber*引數為大於最大數目的資料行或參數可支援資料來源，而*DescriptorHandle*引數為 APD、 IPD 或 ARD。<br /><br /> *RecNumber*引數是等於 0，而*DescriptorHandle*隱含配置 APD 參考引數。 （發生這個錯誤不會不明確配置的應用程式描述項因為不知道應用程式明確配置描述元是否 APD 或 ARD 直到執行階段。）|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) *DescriptorHandle*與建立關聯*StatementHandle*以非同步方式執行的函式 （不這一個） 的呼叫和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*與其*DescriptorHandle*已相關聯，並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*DescriptorHandle*。 此 aynchronous 函式仍在執行時**SQLSetDescRec**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對其中一個相關聯的陳述式控制代碼呼叫*DescriptorHandle*且傳回 SQL_PARAM_DATA_AVAILABLE。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY016|無法修改實作資料列描述項|*DescriptorHandle*引數為 IRD 相關聯。|  
|HY021|不一致的描述元資訊|*型別* 欄位中或任何其他的描述元中的 SQL_DESC_TYPE 欄位相關聯的欄位不是有效或一致。<br /><br /> 描述項一致性檢查期間檢查的資訊不一致。 （請參閱 「 一致性檢查，」 本節稍後的）。|  
|HY090|字串或緩衝區長度無效|(DM) 驅動程式的 ODBC *2.x*驅動程式，描述元是 ARD， *ColumnNumber*引數設定為 0，並指定引數的值*Columnsize*已不等於 4。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*DescriptorHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLSetDescRec**設定的單一資料行或參數的下列欄位：  
  
-   SQL_DESC_TYPE  
  
-   SQL_DESC_DATETIME_INTERVAL_CODE （適用於記錄型別是 SQL_DATETIME 或 SQL_INTERVAL）  
  
-   SQL_DESC_OCTET_LENGTH  
  
-   SQL_DESC_PRECISION  
  
-   SQL_DESC_SCALE  
  
-   SQL_DESC_DATA_PTR  
  
-   SQL_DESC_OCTET_LENGTH_PTR  
  
-   SQL_DESC_INDICATOR_PTR  
  
> [!NOTE]  
>  如果呼叫**SQLSetDescRec**失敗時，所識別的描述項記錄的內容*RecNumber*引數是未定義。  
  
 繫結資料行或參數時**SQLSetDescRec**可讓您變更會影響繫結，而不需呼叫的多個欄位**SQLBindCol**或是**SQLBindParameter**或進行多次呼叫**SQLSetDescField**。 **SQLSetDescRec**可以設定目前未使用陳述式相關聯的描述項欄位。 請注意， **SQLBindParameter**設定更多的欄位，比**SQLSetDescRec**、 可以設定欄位 APD 和 IPD，在一個呼叫中，而且不需要描述項控制代碼。  
  
> [!NOTE]  
>  陳述式屬性 SQL_ATTR_USE_BOOKMARKS 應一律設定之前先呼叫**SQLSetDescRec**具有*RecNumber*引數為 0 時可設定書籤 欄位。 雖然這不是必要項目，強烈建議。  
  
## <a name="consistency-checks"></a>一致性檢查  
 一致性檢查會驅動程式自動執行應用程式在設定 SQL_DESC_DATA_PTR 欄位 APD、 ARD，或 IPD 時。 任何欄位是否具有其他欄位中，不一致**SQLSetDescRec**會傳回 SQLSTATE HY021 （不一致的描述元資訊）。  
  
 每當應用程式在設定 SQL_DESC_DATA_PTR 欄位 APD、 ARD，或 IPD，驅動程式會檢查的 SQL_DESC_TYPE 欄位的值，而且適用於該 SQL_DESC_TYPE 欄位的值有效且一致。 這項檢查是一律執行時**SQLBindParameter**或**SQLBindCol**稱為或當**SQLSetDescRec**稱為 APD、 ARD，或 IPD。 這項一致性檢查包含描述項欄位上的下列檢查：  
  
-   SQL_DESC_TYPE 欄位必須是其中一個有效的 ODBC C SQL 型別或驅動程式專屬的 SQL 型別。 SQL_DESC_CONCISE_TYPE 欄位必須是其中一個有效的 ODBC C 或 SQL 類型或驅動程式專屬 C 或 SQL 類型，包括精簡的日期時間和間隔類型。  
  
-   如果 SQL_DESC_TYPE 記錄欄位是 SQL_DATETIME 或 SQL_INTERVAL，SQL_DESC_DATETIME_INTERVAL_CODE 欄位必須是其中一個有效的日期時間或間隔代碼。 (請參閱 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位中的說明[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。)  
  
-   如果 SQL_DESC_TYPE 欄位指出數值類型，[SQL_DESC_PRECISION 和 SQL_DESC_SCALE] 欄位會驗證為有效。  
  
-   如果 SQL_DESC_CONCISE_TYPE 欄位是時間戳記資料類型，間隔輸入秒數元件，或其中一個間隔資料類型與時間元件，SQL_DESC_PRECISION 欄位會驗證為有效的秒數有效位數。  
  
-   如果 SQL_DESC_CONCISE_TYPE 是間隔資料類型，SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位會驗證必須是有效的間隔開頭有效位數值。  
  
 通常未設定 SQL_DESC_DATA_PTR 欄位的 IPD;不過，應用程式可以先註冊才能強制執行一致性檢查的 IPD 欄位。 無法在 IRD 上執行一致性檢查。 IPD 的 SQL_DESC_DATA_PTR 欄位設定為值並非實際儲存，而且無法擷取由呼叫**SQLGetDescField**或是**SQLGetDescRec**; 此設定只對強制一致性檢查。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|資料行繫結|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|將參數繫結|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得單一的描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定單一的描述項欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
