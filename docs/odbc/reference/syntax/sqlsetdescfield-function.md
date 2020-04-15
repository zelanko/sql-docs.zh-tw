---
title: SQLSetDescfield 函數 |微軟文件
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 122d4b26d1d75811d4a8e252378ce8f81ca2c66b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299548"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 函式

**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLSetDescField**設定描述符記錄的單個字段的值。  
  
## <a name="syntax"></a>語法  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述符句柄。  
  
 *RecNumber*  
 [輸入]指示包含應用程式要設置的欄位的描述符記錄。 描述符記錄從 0 編號,記錄編號 0 是書籤記錄。 對於標頭欄位,將忽略*RecNumber*參數。  
  
 *FieldIdentifier*  
 [輸入]指示要設置其值的描述符的欄位。 有關詳細資訊,請參閱"註釋"部分中的"*欄位識別符*參數"。  
  
 *ValuePtr*  
 [輸入]指向包含描述符資訊的緩衝區或整數值的指標。 資料類型取決於*字段標識碼*的值。 如果*ValuePtr*是整數值,則根據*字段標識符*參數的值,它可以被視為 8 個字節 (SQLLEN)、4 個字節 (SQLINTEGER) 或 2 個字節 (SQLSMALLINT)。  
  
 *緩衝區長度*  
 [輸入]如果*Field 識別碼*是 ODBC 定義的欄位 *,ValuePtr*指向字串或二進位緩衝區,則此參數應為 **ValuePtr*的長度。 對於字串資料,此參數應包含字串中的位元組數。  
  
 如果*欄位識別碼*是 ODBC 定義的欄位 *,ValuePtr*是整數,則忽略*緩衝區長度*。  
  
 如果*Field 識別碼*是驅動程式定義的欄位,則應用程式透過設定*BufferLength*參數向驅動程式管理員指示該欄位的性質。 *緩衝區長度*可以具有以下值:  
  
-   如果*ValuePtr*是指向字串的指標,則*緩衝區長度*是字串的長度或SQL_NTS。  
  
-   如果*ValuePtr*是指向二進位緩衝區的指標,則應用程式將SQL_LEN_BINARY_ATTR(*長度*)宏的結果放在*緩衝區長度*中。 這將在*緩衝區長度*中放置負值。  
  
-   如果*ValuePtr*是指向字串或二進位元字串以外的值的指標,則*BufferLength*應具有該值SQL_IS_POINTER。  
  
-   如果*ValuePtr*包含固定長度值,則*緩衝區長度*為SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT或SQL_IS_USMALLINT(視適用)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescField**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_DESC的*句柄類型*和*描述符句柄*。 下表列出了**SQLSetDescField**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|驅動程式不支援*\*ValuePtr*中指定的值(如果*ValuePtr*是指針)或*ValuePtr*中的值(如果*ValuePtr*是整數值),或者*\*ValuePtr*由於實現工作條件而無效,因此驅動程式替換了類似的值。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07009|不合法的描述符索引|*欄位識別符*參數是記錄欄位 *,RecNumber*參數為 0,*描述符句柄*參數引用 IPD 句柄。<br /><br /> *RecNumber*參數小於 0,*描述符處理*參數引用 ARD 或 APD。<br /><br /> *RecNumber*參數大於資料來源可以支援的最大欄或參數數,*描述符處理*參數引用 APD 或 ARD。<br /><br /> (DM)*字段識別符*參數*\*SQL_DESC_COUNT,ValuePtr*參數小於 0。<br /><br /> *RecNumber*參數等於 0,*描述符句柄*參數引用隱式分配的 APD。 (顯式分配的應用程式描述符不會發生此錯誤,因為在執行時間之前,不知道顯式分配的應用程式描述符是 APD 還是 ARD。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22001|字串資料,右截斷|*字段識別符*參數SQL_DESC_NAME,*緩衝區長度*參數的值大於SQL_MAX_IDENTIFIER_LEN。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY010|函式序列錯誤|(DM)*描述符處理*與*語句句柄*相關聯,在調用此函數時,調用了非同步執行函數(不是此函數),並且仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*,其中*描述符句柄*SQL_NEED_DATA關聯並返回。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 對於與*描述符句柄*關聯的連接句柄,調用了非同步執行函數。 呼叫**SQLSetDescField**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被呼叫為與*描述符句柄*關聯的語句句柄**SQLExecute**之一,並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY016|無法變更行描述子|*描述符句柄*參數與 IRD 相關聯,*並且欄位識別符*參數未SQL_DESC_ARRAY_STATUS_PTR或SQL_DESC_ROWS_PROCESSED_PTR。|  
|HY021|描述符資訊不一致|SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE欄位不形成有效的 ODBC SQL 類型或有效的特定於驅動程式的 SQL 類型(對於 IPD)或有效的 ODBC C 類型(對於 AD 或 AD)。<br /><br /> 在一致性檢查期間檢查的描述符資訊不一致。 (請參閱**SQLSetDescRec**中的"一致性檢查"|  
|HY090|不合法的字串或緩衝區長度|(DM) * \*ValuePtr*是一個字串,*緩衝區長度*小於零,但不等於SQL_NTS。<br /><br /> (DM) 驅動程式是 ODBC 2 *.x*驅動程式,描述符是 ARD,*列號*參數設置為 0,為參數*BufferLength*指定的值不等於 4。|  
|HY091|不合法的字段識別碼|為*FieldIdentifier 參數*指定的值不是 ODBC 定義的欄位,不是實現定義的值。<br /><br /> 對於*描述符處理*參數,*字段識別符*參數無效。<br /><br /> *欄位識別符*參數是一個唯讀的 ODBC 定義的欄位。|  
|HY092|不合法屬性/選項識別碼|ValuePtr 中的值對*字段識別符*參數無效。 * \**<br /><br /> *字段標識符*參數SQL_DESC_UNNAMED,ValuePtr *ValuePtr* SQL_NAMED。|  
|HY105|不合法參數型態|(DM) 為SQL_DESC_PARAMETER_TYPE欄位指定的值無效。 (有關詳細資訊,請參閱**SQLBind 參數**中的「*輸入輸出類型*參數」 部分。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[ODBC 3.8 中的新增功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*描述符處理*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 應用程式可以調用**SQLSetDescField**來一次設置一個描述符欄位。 對**SQLSetDescField 的**一次調用在單個描述符中設置單個字段。 可以調用此函數來設置任何描述符類型中的任何欄位,前提是可以設置該欄位。 (請參閱本節後面的表。  
  
> [!NOTE]  
>  如果對**SQLSetDescField**的調用失敗,則*RecNumber*參數標識的描述符記錄的內容將未定義。  
  
 可以調用其他函數來設置具有函數單個調用的多個描述符欄位。 **SQLSetDescRec**函數設置各種欄位,這些欄位會影響綁定到列或參數的數據類型和緩衝區(SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_INDICATOR_PTR欄位)。 **SQLBindCol**或**SQLBind參數**可用於為列或參數的綁定制定完整的規範。 這些函數設置具有一個函數調用的特定描述符欄位組。  
  
 可以調用**SQLSetDescField**來透過綁定指標(SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR或SQL_DESC_OCTET_LENGTH_PTR)添加偏移量來更改綁定緩衝區。 這將更改綁定緩衝區而不調用**SQLBindCol**或**SQLBindparameter**,這允許應用程式更改SQL_DESC_DATA_PTR而不更改其他欄位,如SQL_DESC_DATA_TYPE。  
  
 如果應用程式調用**SQLSetDescField**來設置SQL_DESC_COUNT以外的任何欄位,或者SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR或SQL_DESC_INDICATOR_PTR的延遲欄位,則記錄將變為未綁定。  
  
 描述符標頭欄位是透過使用相應的*字段識別碼*調用**SQLSetDescField**來設定的。 許多標頭欄位也是語句屬性,因此也可以通過調用**SQLSetStmtAttr**來設置它們。 這允許應用程式在不首先獲取描述符句柄的情況下設置描述符欄位。 當調用**SQLSetDescField**來設置標頭欄位時,將忽略*RecNumber*參數。  
  
 *RecNumber* 0 用於設置書籤欄位。  
  
> [!NOTE]  
>  在調用**SQLSetDescField**來設置書籤欄位之前,應始終設置語句屬性SQL_ATTR_USE_BOOKMARKS。 雖然這不是強制性的,但強烈建議這樣做。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>設定描述符位的順序  
 使用**SQLSetDescField**設定描述符位時,應用程式必須遵循特定順序:  
  
1.  應用程式必須首先設置SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE或SQL_DESC_DATETIME_INTERVAL_CODE欄位。  
  
2.  設置這些欄位之一後,應用程式可以設置數據類型的屬性,並且驅動程式將數據類型屬性欄位設置為數據類型的相應預設值。 類型屬性欄位的自動預設可確保描述符始終準備好在應用程式指定數據類型後使用。 如果應用程式顯示式設定資料類型屬性,則它將重寫預設屬性。  
  
3.  在步驟 1 中列出的一個字段被設置並設置了數據類型屬性後,應用程式可以SQL_DESC_DATA_PTR設置。 這提示對描述符欄位進行一致性檢查。 如果應用程式在設置SQL_DESC_DATA_PTR欄位後更改數據類型或屬性,則驅動程式將SQL_DESC_DATA_PTR設置為空指標,取消綁定記錄。 這將強制應用程式在描述符記錄可用之前按順序完成正確的步驟。  
  
## <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定  
 分配描述符時,描述符中的欄位可以初始化為預設值,在沒有預設值的情況下初始化,或者未定義描述符的類型。 下表指示每種描述符類型每個欄位的初始化,其中"D"指示該欄位用預設值初始化,而"ND"表示該欄位在沒有預設值的情況下初始化。 如果顯示數位,則欄位的預設值為該數位。 這些表還指示欄位是讀/寫 (R/W) 還是唯讀 (R)。  
  
 IRD 的欄位僅在準備或執行語句並填充 IRD 之後才具有預設值,而不是在分配語句句柄或描述符後。 在填充 IRD 之前,任何嘗試存取 IRD 欄位的嘗試都將傳回錯誤。  
  
 某些描述符位是為描述符類型的一個或多個(但不是全部)定義的(AD 和 IRD 以及 AD 和 IPD)。 當一個字段未為描述符類型定義時,使用該描述符的任何函數都不需要該欄位。  
  
 **SQLGetDescField**可以造訪的欄位不一定由**SQLSetDescField**設置。 下表列出了**SQLSetDescField**可以設置的欄位。  
  
 標題欄位的初始化在下表中概述。  
  
|標題欄位名稱|類型|R/W|預設|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD:SQL_DESC_ALLOC_AUTO隱式或SQL_DESC_ALLOC_USER為顯式<br /><br /> APD:SQL_DESC_ALLOC_AUTO隱式或SQL_DESC_ALLOC_USER為顯式<br /><br /> 國際復興開發銀行:SQL_DESC_ALLOC_AUTO<br /><br /> IPD:SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD:[1] APD:[1] IRD:未使用的 IPD:未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD:R/W APD:R/W IRD:R/W IPD:R/W|ARD: 空點子 APD: 空點 ptr IRD: 空點 IPD: 空點子|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD: 空點子 APD: 空點子 IRD: 未使用的 IPD: 未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD:SQL_BIND_BY_COLUMN<br /><br /> IRD:未使用<br /><br /> IPD:未使用|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|ARD:未使用的 APD:未使用的 IRD:R/W IPD:R/W|ARD:未使用的 APD:未使用的 IRD:空點 IPD:空點子|  
  
 [1] 僅當驅動程式自動填充 IPD 時,才會定義這些欄位。 如果沒有,它們未定義。 如果應用程式嘗試設置這些欄位,將返回 SQLSTATE HY091(無效描述符欄位識別碼)。  
  
 記錄欄位的初始化如下表所示。  
  
|記錄欄位名稱|類型|R/W|預設|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: SQL_C_ DEFAULT APD: SQL_C_ DEFAULT IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPointer|ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD: 空點子 APD: 空點子 IRD: 未使用的 IPD: 未使用 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN ||ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD: 空點子 APD: 空點子 IRD: 未使用的 IPD: 未使用|  
|SQL_DESC_LABEL|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_LENGTH|SQLULEN|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN ||ARD:R/W APD:R/W IRD:未使用的 IPD:未使用|ARD: 空點子 APD: 空點子 IRD: 未使用的 IPD: 未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:未使用的 IPD:R/W|ARD:未使用的 APD:未使用的 IRD:未使用的 IPD:D=SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD:未使用<br /><br /> APD:未使用<br /><br /> IRD: R<br /><br /> IPD: R|ARD:未使用<br /><br /> APD:未使用<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD:R/W APD:R/W IRD:R IPD:R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR ||ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:R|ARD:未使用的 APD:未使用的 IRD:D IPD:D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD:未使用的 APD:未使用的 IRD:R IPD:未使用|ARD:未使用的 APD:未使用的 IRD:D IPD:未使用|  
  
 [1] 僅當驅動程式自動填充 IPD 時,才會定義這些欄位。 如果沒有,它們未定義。 如果應用程式嘗試設置這些欄位,將返回 SQLSTATE HY091(無效描述符欄位識別碼)。  
  
 [2] IPD 中的SQL_DESC_DATA_PTR欄位可以設置為強制一致性檢查。 在隨後調用**SQLGetDescField**或**SQLGetDescRec 時**,不需要驅動程式返回SQL_DESC_DATA_PTR設置為的值。  
  
## <a name="fieldidentifier-argument"></a>欄位識別子參數  
 *欄位識別符*參數指示要設置的描述符位。 描述符包含*描述符標頭,* 由下一節中描述的標題欄位「標題欄位」和零個或多個*描述元記錄組成,* 由「標題欄位」部分後部分中描述的記錄欄位組成。  
  
## <a name="header-fields"></a>標題欄位  
 每個描述符都有一個標頭,其中包含以下欄位:  
  
 **SQL_DESC_ALLOC_TYPE [全部]**  
 此唯讀 SQLSMALLINT 標頭欄位指定描述碼是由驅動程式自動分配還是由應用程式顯式分配。 應用程式可以獲取而不是修改此欄位。 如果描述符由驅動程式自動分配,則該欄位設置為由驅動程式SQL_DESC_ALLOC_AUTO。 如果描述符由應用程式顯式分配,則驅動程式將其設置為SQL_DESC_ALLOC_USER。  
  
 **SQL_DESC_ARRAY_SIZE [應用程式描述符]**  
 在ARD中,此 SQLULEN 標頭欄位指定行集中的行數。 這是調用**SQLFetch**或**SQLFetchScroll**或透過呼叫**SQLBulk 操作**或**SQLSetPos**返回的行數。  
  
 在 AD 中,此 SQLULEN 標頭欄位指定每個參數的值數。  
  
 此欄位的預設值為 1。 如果SQL_DESC_ARRAY_SIZE大於 APD 或 ARD 指向陣列的 1、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR。 每個陣列的基數等於此欄位的值。  
  
 ARD 中的此欄位也可以通過使用SQL_ATTR_ROW_ARRAY_SIZE屬性調用**SQLSetStmtAttr**來設置。 APD 中的此欄位也可以通過使用SQL_ATTR_PARAMSET_SIZE屬性調用**SQLSetStmtAttr**來設置。  
  
 **SQL_DESC_ARRAY_STATUS_PTR [全部]**  
 對於每種描述符類型,此 SQLUSMALLINT = 標頭欄位指向 SQLUSMALLINT 值陣列。 這些陣列的命名方式如下:行狀態陣列 (IRD)、參數狀態陣列 (IPD)、行操作陣列 (ARD) 和參數操作陣列 (APD)。  
  
 在 IRD 中,此標頭欄位指向在調用**SQLBulk 操作**、SQLFetch、SQLFetchScroll**SQLFetch**或**SQLFetchScroll****SQLSetPos**後包含狀態值的行狀態陣列。 陣列具有與行集中的行一樣多的元素。 應用程式必須分配 SQLUSMALLINT 陣列,並將此欄位設置為指向陣列。 默認情況下,該欄位設置為空指標。 驅動程式將填充陣列 ─ 除非SQL_DESC_ARRAY_STATUS_PTR欄位設定為空指標,在這種情況下不會生成狀態值,並且陣列未填充。  
  
> [!CAUTION]  
>  如果應用程式設定 IRD SQL_DESC_ARRAY_STATUS_PTR 欄位指向的行狀態陣列的元素,則驅動程式行為未定義。  
  
 陣列最初由對**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos****SQLFetchScroll**的調用填充。 如果調用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則此欄位指向的陣列的內容將未定義。 陣列的元素可以包含以下值:  
  
-   SQL_ROW_SUCCESS:該行已成功提取,自上次提取以來未更改。  
  
-   SQL_ROW_SUCCESS_WITH_INFO:該行已成功提取,自上次提取以來未更改。 但是,返回了有關該行的警告。  
  
-   SQL_ROW_ERROR:獲取行時出錯。  
  
-   SQL_ROW_UPDATED:該行已成功提取,自上次提取以來已更新。 如果再次提取該行,則其狀態為SQL_ROW_SUCCESS。  
  
-   SQL_ROW_DELETED:自上次提取行以來,該行已被刪除。  
  
-   SQL_ROW_ADDED:該行由**SQLBulk 操作**插入。 如果再次提取該行,則其狀態為SQL_ROW_SUCCESS。  
  
-   SQL_ROW_NOROW:行集與結果集的末尾重疊,並且不會返回對應於行狀態陣列的此元素的行。  
  
 IRD 中的此欄位也可以通過使用SQL_ATTR_ROW_STATUS_PTR屬性調用**SQLSetStmtAttr**來設置。  
  
 IRD 的SQL_DESC_ARRAY_STATUS_PTR欄位僅在返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO後才有效。 如果返回代碼不是其中之一,則SQL_DESC_ROWS_PROCESSED_PTR指向的位置未定義。  
  
 在 IPD 中,此標頭欄位指向一個參數狀態陣列,其中包含對 SQLExecute 或**SQLExecDirect**調用**SQLExecDirect**後每組參數值的狀態資訊。 如果對 SQLExecute 或**SQLExecDirect**的呼叫未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則此欄位指向的陣列**SQLExecDirect**的內容未定義。 應用程式必須分配 SQLUSMALLINT 陣列,並將此欄位設置為指向陣列。 驅動程式將填充陣列 ─ 除非SQL_DESC_ARRAY_STATUS_PTR欄位設定為空指標,在這種情況下不會生成狀態值,並且陣列未填充。 陣列的元素可以包含以下值:  
  
-   SQL_PARAM_SUCCESS:已成功為這組參數執行 SQL 語句。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO:已成功為這組參數執行 SQL 語句;但是,診斷數據結構中提供了警告資訊。  
  
-   SQL_PARAM_ERROR:在處理這組參數時出錯。 診斷數據結構中提供了其他錯誤資訊。  
  
-   SQL_PARAM_UNUSED:此參數集未使用,可能是因為以前的一些參數集導致錯誤中止進一步處理,或者因為 aPD 的SQL_DESC_ARRAY_STATUS_PTR欄位指定的陣列中為該參數集設置了SQL_PARAM_IGNORE。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE:診斷資訊不可用。 例如,當驅動程式將參數陣列視為單片單元,因此不會生成此級別的錯誤資訊。  
  
 IPD 中的此欄位也可以通過使用SQL_ATTR_PARAM_STATUS_PTR屬性調用**SQLSetStmtAttr**來設置。  
  
 在 ARD 中,此標頭欄位指向一個行操作陣列,該陣列的值可以由應用程式設置,以指示是否為**SQLSetPos**操作忽略此行。 陣列的元素可以包含以下值:  
  
-   SQL_ROW_PROCEED:該行包含在使用**SQLSetPos**的批量操作中。 (此設置不保證該操作將在行上發生。 如果該行的狀態SQL_ROW_ERROR IRD 行狀態陣列中,則驅動程式可能無法在行中執行操作。  
  
-   SQL_ROW_IGNORE: 使用**SQLSetPos**將該行從批量操作中排除。  
  
 如果未設置陣列的元素,則所有行都包含在批量操作中。 如果 ARD SQL_DESC_ARRAY_STATUS_PTR 欄位中的值為空指標,則所有行都包含在批量操作中;如果 ARD 欄位中的值為空指標,則所有行都包含在批量操作中。"解釋與指標指向有效陣列和陣列的所有元素都SQL_ROW_PROCEED相同。 如果陣列中的元素設置為SQL_ROW_IGNORE,則忽略行的行狀態陣列中的值不會更改。  
  
 ARD 中的此欄位也可以通過使用SQL_ATTR_ROW_OPERATION_PTR屬性調用**SQLSetStmtAttr**來設置。  
  
 在 APD 中,此標頭欄位指向應用程式可以設置的值的參數操作陣列,以指示在調用 SQLExecute 或**SQLExecDirect**時是否忽略這組**SQLExecDirect**參數。 陣列的元素可以包含以下值:  
  
-   SQL_PARAM_PROCEED:SQLExecute 或**SQLExecDirect**呼**SQLExecDirect**叫中包含 一組參數。  
  
-   SQL_PARAM_IGNORE:從 SQLExecute 或**SQLExecDirect**調用**SQLExecDirect**中排除參數集。  
  
 如果未設置陣列的元素,則 SQLExecute 或**SQLExecDirect**調用中將使用陣列中**SQLExecDirect**的所有參數集。 如果 APD SQL_DESC_ARRAY_STATUS_PTR欄位中的值為空指標,則使用所有參數集;如果使用 aPD 欄位中的值,則使用所有參數集。解釋與指標指向有效陣列和陣列的所有元素SQL_PARAM_PROCEED相同。  
  
 APD 中的此欄位也可以通過使用SQL_ATTR_PARAM_OPERATION_PTR屬性調用**SQLSetStmtAttr**來設置。  
  
 **SQL_DESC_BIND_OFFSET_PTR [應用程式描述符]**  
 此 SQLLEN = 標頭欄位指向綁定偏移量。 默認情況下,它設置為空指標。 如果此欄位不是空指標,則驅動程式將引用指標,並將已引用的值添加到在提取時描述符記錄中具有非空值(SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和SQL_DESC_OCTET_LENGTH_PTR)的每個延遲欄位,並在綁定時使用新的指標值。  
  
 綁定偏移量始終直接添加到SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR欄位中的值。 如果偏移更改為其他值,則新值仍直接添加到每個描述符欄位中的值。 新偏移量不會添加到欄位值加上任何較早的偏移量中。  
  
 此欄位是*延遲欄位*:在設置時不使用它,但在需要確定數據緩衝區的位址時,驅動程式稍後會使用它。  
  
 ARD 中的此欄位也可以通過使用SQL_ATTR_ROW_BIND_OFFSET_PTR屬性調用**SQLSetStmtAttr**來設置。 ARD 中的此欄位也可以通過使用SQL_ATTR_PARAM_BIND_OFFSET_PTR屬性調用**SQLSetStmtAttr**來設置。  
  
 有關詳細資訊,請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)和[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md)中行綁定的說明。  
  
 **SQL_DESC_BIND_TYPE [應用程式描述符]**  
 此 SQLUINTEGER 標頭欄位設置綁定方向,用於綁定列或參數。  
  
 在 AD 中,此欄位指定在關聯語句句柄上調用**SQLFetchScroll**或**SQLFetch**時綁定方向。  
  
 要為列選擇按列方向的綁定,此欄位設置為SQL_BIND_BY_COLUMN(預設值)。  
  
 ARD 中的此欄位也可以通過使用 SQL_ATTR_ROW_BIND_TYPE*屬性*調用**SQLSetStmtAttr**來設置。  
  
 在 AD 中,此欄位指定用於動態參數的綁定方向。  
  
 要為參數選擇按列綁定,此欄位設置為SQL_BIND_BY_COLUMN(預設值)。  
  
 APD 中的此欄位也可以通過使用 SQL_ATTR_PARAM_BIND_TYPE*屬性*呼叫**SQLSetStmtAttr**來設置。  
  
 **SQL_DESC_COUNT [全部]**  
 此 SQLSMALLINT 標頭欄位指定包含數據的最高編號記錄的基於 1 的索引。 當驅動程式為描述符設定數據結構時,它還必須設置SQL_DESC_COUNT欄位以顯示有多少記錄很重要。 當應用程式分配此數據結構的實例時,它不必指定要為其保留多少記錄。 當應用程式指定記錄的內容時,驅動程式會執行任何必需的操作,以確保描述符句柄引用大小適當的數據結構。  
  
 SQL_DESC_COUNT不是綁定的所有數據列(如果欄位位於ARD中)或綁定的所有參數(如果欄位位於APD中)的計數,而是編號最高的記錄數。 如果最高編號的列或參數未綁定,則SQL_DESC_COUNT更改為下一個編號最高的列或參數的編號。 如果數位小於最高編號列數的列或參數未綁定(透過呼叫**SQLBindCol,** 將*TargetValuePtr*參數設定為空指標,或將*參數ValuePtr*參數設定為空指針的**SQLBindparameter),** 則不會更改SQL_DESC_COUNT。 如果附加列或參數的編號大於包含數據的最高編號記錄,則驅動程式會自動增加SQL_DESC_COUNT欄位中的值。 如果使用"SQL_UNBIND"選項調用**SQLFreeStmt**取消綁定所有列,則 ARD 和 IRD 中的SQL_DESC_COUNT欄位設置為 0。 如果使用SQL_RESET_PARAMS選項調用**SQLFreeStmt,** 則 APD 和 IPD 中的SQL_DESC_COUNT欄位設置為 0。  
  
 SQL_DESC_COUNT中的值可以通過調用**SQLSetDescField**由應用程式顯式設置。 如果顯式減小SQL_DESC_COUNT中的值,則有效刪除SQL_DESC_COUNT中數位大於新值的所有記錄。 如果SQL_DESC_COUNT中的值顯式設置為 0,並且該欄位位於 ARD 中,則釋放除綁定書簽列之外的所有數據緩衝區。  
  
 ARD 此欄位中的記錄計數不包括綁定書簽列。 取消綁定書籤列的唯一方法是將SQL_DESC_DATA_PTR欄位設置為空指標。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [實作描述符]**  
 在 IRD 中\*,此 SQLULEN 標頭欄位指向一個緩衝區,其中包含調用**SQLFetch**或**SQLFetchScroll**後獲取的行數,或調用**SQLBulk 操作**或**SQLSetPos(** 包括錯誤行)在批量操作中受影響的行數。  
  
 在 IPD 中,此 SQLUINTEGER = 標頭欄位指向一個緩衝區,其中包含已處理的參數集數,包括錯誤集。 如果這是空指標,則不會返回任何數位。  
  
 SQL_DESC_ROWS_PROCESSED_PTR僅在調用**SQLFetch**或**SQLFetchScroll(** 對於 IRD 欄位)或 SQLExecute、SQLExecDirect**SQLExecute**或**SQLParamData(** 對於 IPD**SQLExecDirect**欄位)後返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO後才有效。 如果填充此字段指向的緩衝區的調用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則緩衝區的內容將未定義,除非返回SQL_NO_DATA,在這種情況下緩衝區中的值設置為 0。  
  
 ARD 中的此欄位也可以通過使用SQL_ATTR_ROWS_FETCHED_PTR屬性調用**SQLSetStmtAttr**來設置。 APD 中的此欄位也可以通過使用SQL_ATTR_PARAMS_PROCESSED_PTR屬性調用**SQLSetStmtAttr**來設置。  
  
 此欄位指向的緩衝區由應用程式分配。 它是驅動程式設置的延遲輸出緩衝區。 默認情況下,它設置為空指標。  
  
## <a name="record-fields"></a>記錄欄位  
 每個描述符包含一個或多個記錄,這些記錄由定義列數據或動態參數的欄位組成,具體取決於描述符的類型。 每個記錄都是單個列或參數的完整定義。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [紅外點]**  
 此唯讀 SQLINTEGER 記錄欄位包含SQL_TRUE如果列是自動遞增列,則SQL_FALSE列不是自動遞增列。 此欄位是唯讀的,但基礎自動遞增列不一定是唯讀的。  
  
 **SQL_DESC_BASE_COLUMN_NAME [紅外點]**  
 此唯讀 SQLCHAR = 記錄欄位包含結果集列的基本列名稱。 如果基本列名稱不存在(如表達式的列),此變數包含一個空字串。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRD]**  
 此唯讀 SQLCHAR = 記錄欄位包含結果集列的基表名稱。 如果無法定義基表名稱或不適用,則此變數包含一個空字串。  
  
 **SQL_DESC_CASE_SENSITIVE [實作描述符]**  
 此唯讀 SQLINTEGER 記錄欄位包含SQL_TRUE如果列或參數被視爲區分大小寫(用於排序規則和比較);如果該列不被視爲區分大小寫(用於排序規則和比較)或該列是否被視為非字元列,則SQL_FALSE。  
  
 **SQL_DESC_CATALOG_NAME [紅外指示]**  
 此唯讀 SQLCHAR = 記錄欄位包含包含欄位的基表的目錄。 如果列是表達式或列是視圖的一部分,則返回值與驅動程序相關。 如果數據來源不支援目錄或無法確定目錄,則此變數包含一個空字串。  
  
 **SQL_DESC_CONCISE_TYPE [全部]**  
 此 SQLSMALLINT 標頭欄位指定所有資料類型(包括日期時間和間隔數據類型)的簡明數據類型。  
  
 SQL_DESC_CONCISE_TYPE、SQL_DESC_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE欄位中的值是相互依賴的。 每次設置其中一個字段時,還必須設置另一個字段。 SQL_DESC_CONCISE_TYPE可以通過調用**SQLBindCol**或**SQLBind 參數**(或**SQLSetDescField)** 來設置。 SQL_DESC_TYPE可以通過調用**SQLSetDescField**或**SQLSetDescRec**來設置。  
  
 如果SQL_DESC_CONCISE_TYPE設置為間隔或日期時間數據類型以外的簡明數據類型,則SQL_DESC_TYPE欄位設置為相同的值,SQL_DESC_DATETIME_INTERVAL_CODE欄位設置為 0。  
  
 如果SQL_DESC_CONCISE_TYPE設置為簡明日期時間或間隔數據類型,則SQL_DESC_TYPE欄位設置為相應的詳細類型(SQL_DATETIME或SQL_INTERVAL),並將SQL_DESC_DATETIME_INTERVAL_CODE欄位設置為相應的子代碼。  
  
 **SQL_DESC_DATA_PTR [應用程式描述符與 IPD]**  
 此 SQLPOINTER 記錄欄位指向將包含參數值(對於 AD)或列值(用於 AD)的變數。 此欄位是*遞延欄位*。 它在設置時不使用,但驅動程式稍後使用它來檢索數據。  
  
 如果調用**SQLBindCol**中的*TargetValuePtr*參數為空指標,或者 ARD 中的SQL_DESC_DATA_PTR欄位由對**SQLSetDescField**或**SQLSetDescRec**的調用設置為空指標,則 ARD SQL_DESC_DATA_PTR欄位指定的列將取消綁定。 如果SQL_DESC_DATA_PTR欄位設置為空指標,則其他欄位不受影響。  
  
 如果對**SQLFetch**或**SQLFetchScroll**的調用填充此欄位指向的緩衝區未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則緩衝區的內容未定義。  
  
 每當設定 APD、ARD 或 IPD 的SQL_DESC_DATA_PTR欄位時,驅動程式都會檢查SQL_DESC_TYPE欄位中的值是否包含有效的 ODBC C 資料類型或特定於驅動程式的數據類型,並且影響數據類型的所有其他欄位是否一致。 提示一致性檢查是 IPD SQL_DESC_DATA_PTR欄位的唯一用途。 具體而言,如果應用程式設置 IPD 的SQL_DESC_DATA_PTR欄位,並在此欄位上調用**SQLGetDescField,** 則不一定返回它設置的值。 有關詳細資訊,請參閱[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的「一致性檢查」。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [全部]**  
 當SQL_DESC_TYPE欄位SQL_DATETIME或SQL_INTERVAL時,此 SQLSMALLINT 記錄欄位包含特定日期時間或間隔數據類型的子代碼。 SQL 和 C 數據類型都是如此。 代碼由資料類型名稱組成,其中"CODE"代替了"TYPE"或"C_TYPE"(用於日期時間類型),或"CODE"代替"INTERVAL"或"C_INTERVAL"(對於間隔類型)。  
  
 如果應用程式描述符中的SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE設置為SQL_C_DEFAULT,並且描述符不與語句句柄關聯,則SQL_DESC_DATETIME_INTERVAL_CODE的內容未定義。  
  
 此欄位可用於下表中列出的日期時間數據類型。  
  
|日期時間類型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 此欄位可用於下表中列出的間隔數據類型。  
  
|間隔類型|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/ SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/ SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 關於資料間隔與此欄位的詳細資訊,請參考[資料類型識別碼與描述符](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)號 。  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [全部]**  
 如果SQL_DESC_TYPE字段SQL_INTERVAL,則此 SQLINTEGER 記錄欄位包含間隔前導精度。 當SQL_DESC_DATETIME_INTERVAL_CODE欄位設置為間隔數據類型時,此欄位設置為預設間隔前導精度。  
  
 **SQL_DESC_DISPLAY_SIZE [IRD]**  
 此唯讀 SQLINTEGER 記錄欄位包含顯示列中資料所需的最大字元數。  
  
 **SQL_DESC_FIXED_PREC_SCALE [實作描述符]**  
 如果列是精確數值列且具有固定精度和非零比例,則此唯讀 SQLSMALLINT 記錄欄位設定為SQL_TRUE,如果列不是具有固定精度和刻度的精確數位列,則SQL_FALSE。  
  
 **SQL_DESC_INDICATOR_PTR [應用程式描述符]**  
 在 ARD 中,此 SQLLEN = 記錄欄位指向指標變數。 如果列值為 NULL,則此變數包含SQL_NULL_DATA。 對於 AD,指標變數設定為SQL_NULL_DATA指定 NULL 動態參數。 否則,變數為零(除非SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR中的值是相同的指標)。  
  
 如果ARD中的SQL_DESC_INDICATOR_PTR欄位為空指標,則阻止驅動程式返回有關列是否為NULL的資訊。 如果列為 NULL 且SQL_DESC_INDICATOR_PTR為空指標,則當驅動程式嘗試在調用**SQLFetch**或**SQLFetchScroll**後填充緩衝區時,將返回 SQLSTATE 22002(需要但未提供指標變數)。 如果對**SQLFetch**或**SQLFetchScroll**的調用未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則緩衝區的內容未定義。  
  
 SQL_DESC_INDICATOR_PTR欄位確定是否設置了SQL_DESC_OCTET_LENGTH_PTR指向的欄位。 如果列的資料值為 NULL,則驅動程式將指示器變數設定為SQL_NULL_DATA。 然後不設置SQL_DESC_OCTET_LENGTH_PTR指向的欄位。 如果在提取過程中未遇到 NULL 值,則SQL_DESC_INDICATOR_PTR指向的緩衝區設置為零,SQL_DESC_OCTET_LENGTH_PTR指向的緩衝區設置為數據的長度。  
  
 如果 APD 中的SQL_DESC_INDICATOR_PTR欄位是空指標,則應用程式不能使用此描述符記錄指定 NULL 參數。  
  
 此欄位是*遞延欄位*:在設定時不使用它,但驅動程式稍後使用它來指示 null(對於 AD)或確定 null(對於 AD)。  
  
 **SQL_DESC_LABEL [紅外指示]**  
 此唯讀 SQLCHAR = 記錄欄位包含列標籤或標題。 如果列沒有標籤,則此變數包含列名稱。 如果列未命名且未標記,則此變數包含一個空字串。  
  
 **SQL_DESC_LENGTH [全部]**  
 此 SQLULEN 記錄欄位是字元字串的最大長度或實際長度,或以位元組為單位的二進位資料類型。 它是固定長度數據類型的最大長度,或可變長度數據類型的實際長度。 其值始終排除結束字元字串的 null 終止字元。 對於類型為SQL_TYPE_DATE、SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP或 SQL 間隔數據類型之一的值,此欄位具有日期時間或間隔值的字串表示的字元長度。  
  
 此欄位中的值可能與 ODBC 2 *.x*中定義的「長度」值不同。 關於詳細資訊,請參閱附錄[D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_LITERAL_PREFIX [紅外點]**  
 此唯讀 SQLCHAR = 記錄欄位包含驅動程式識別為此資料類型文本的前置字元或字元。 此變數包含不適用於文本前置資料類型的空字串。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRD]**  
 此唯讀 SQLCHAR = 記錄欄位包含驅動程式識別為此資料類型文本的後綴的字元或字元。 此變數包含不適用於文本後綴的資料類型的空字串。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [實作描述符]**  
 此唯讀 SQLCHAR = 記錄欄位包含資料類型可能與資料類型的常規名稱不同的任何當地語系化(母語)名稱。 如果沒有當地語系化名稱,則返回一個空字串。 此欄位僅用於顯示目的。  
  
 **SQL_DESC_NAME [實作描述符]**  
 此 SQLCHAR = 行描述符中的記錄欄位包含列別名(如果適用)。 如果列別名不適用,則返回列名稱。 在這兩種情況下,驅動程式在設置SQL_DESC_NAME欄位時將SQL_DESC_UNNAMED欄位設置為SQL_NAMED。 如果沒有列名或列別名,驅動程式將返回SQL_DESC_NAME欄位中的空字串,並將SQL_DESC_UNNAMED欄位設置為SQL_UNNAMED。  
  
 應用程式可以將 IPD 的SQL_DESC_NAME欄位設定為參數名稱或別名,以便按名稱指定儲存的過程參數。 ( 關於詳細資訊,請參考[此名稱(命名參數)綁定參數](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。IRD 的SQL_DESC_NAME欄位是唯讀字段;如果應用程式嘗試設定 SQLSTATE HY091(無效描述符位元號),將返回它。  
  
 在 ID 中,如果驅動程式不支援命名參數,則此欄位未定義。 如果驅動程式支援命名參數並能夠描述參數,則參數名稱將在此欄位中返回。  
  
 **SQL_DESC_NULLABLE [實作描述符]**  
 在 IRD 中,如果列可以具有 NULL 值,則此唯讀 SQLSMALLINT 記錄欄位SQL_NULLABLE,如果列沒有 NULL 值,則SQL_NO_NULLS列是否具有 NULL 值,或者如果不知道列是否接受 NULL 值,則SQL_NULLABLE_UNKNOWN。 此欄位與結果集列相關,而不是與基本列相關。  
  
 在 IID 中,此欄位始終設置為SQL_NULLABLE,因為動態參數始終為空,並且不能由應用程式設置。  
  
 **SQL_DESC_NUM_PREC_RADIX [全部]**  
 如果SQL_DESC_TYPE欄位中的數據類型是近似數值數據類型,則此 SQLINTEGER 欄位包含值 2,因為SQL_DESC_PRECISION欄位包含位數。 如果SQL_DESC_TYPE欄位中的數據類型是精確數位資料類型,則此欄位包含值10,因為SQL_DESC_PRECISION欄位包含小數位數。 此欄位設置為 0,用於所有非數位數據類型。  
  
 **SQL_DESC_OCTET_LENGTH [全部]**  
 此 SQLLEN 記錄欄位包含字串或二進位資料類型的長度(以位元組為單位)。 對於固定長度字元或二進位類型,這是以位元組為單位的實際長度。 對於可變長度字元或二進位類型,這是以位元組為單位的最大長度。 此值始終排除實現描述符的 null 終止字元的空間,並且始終包含應用程式描述符的 null 終止字元的空間。 對於應用程式數據,此欄位包含緩衝區的大小。 對於 AD,此欄位僅為輸出或輸入/輸出參數定義。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [應用程式描述符]**  
 此 SQLLEN = 記錄欄位指向一個變數,該變數將包含動態參數(對於參數描述符)或綁定列值(對於行描述符)的總長度。  
  
 對於 APD,除字串和二進位之外的所有參數,此值都將被忽略;如果此欄位指向SQL_NTS,則動態參數必須為 null 終止。 為了指示綁定參數將是執行時的數據參數,應用程式將 APD 的適當記錄中的此欄位設置為變數,在執行時,該變數將包含值SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的結果。 如果有多個此類欄位,則可以將SQL_DESC_DATA_PTR設置為唯一標識參數的值,以説明應用程式確定請求的參數。  
  
 如果ARD的OCTET_LENGTH_PTR欄位為空指標,則驅動程式不會返回列的長度資訊。 如果 APD 的SQL_DESC_OCTET_LENGTH_PTR欄位為空指標,則驅動程式假定字串和二進位值為 null 終止。 (二進位值不應為null終止,而應為長度指定以避免截斷。  
  
 如果對**SQLFetch**或**SQLFetchScroll**的調用填充此欄位指向的緩衝區未返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則緩衝區的內容未定義。 此欄位是*遞延欄位*。 它在設置時不使用,但驅動程式稍後使用它來確定或指示數據的八進位長度。  
  
 **SQL_DESC_PARAMETER_TYPE [IPD]**  
 此 SQLSMALLINT 記錄欄位設定為輸入參數SQL_PARAM_INPUT、輸入/輸出參數SQL_PARAM_INPUT_OUTPUT、輸出參數SQL_PARAM_OUTPUT、輸入/輸出流參數SQL_PARAM_INPUT_OUTPUT_STREAM或輸出流參數的SQL_PARAM_OUTPUT_STREAM。 默認情況下,它設置為SQL_PARAM_INPUT。  
  
 對於 IPD,如果驅動程式未自動填充 IPD(SQL_ATTR_ENABLE_AUTO_IPD語句屬性SQL_FALSE),則默認情況下,該欄位設置為SQL_PARAM_INPUT。 應用程式應在 IPD 中為不是輸入參數的參數設置此欄位。  
  
 **SQL_DESC_PRECISION [全部]**  
 此 SQLSMALLINT 記錄欄位包含精確數值類型的位數、近似數值類型的 mantissa 中的位數(二進位元),或SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP或SQL_INTERVAL_SECOND數據類型的小數秒分量中的位數。 此欄位對於所有其他數據類型未定義。  
  
 此欄位中的值可能與 ODBC 2 *.x*中定義的「精度」值不同。 關於詳細資訊,請參閱附錄[D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_ROWVER [實作描述符]**  
 此 SQLSMALLINTrecord 欄位指示在更新行時 DBMS 是否自動修改列(例如,SQL Server 中類型"時間戳"類型的列)。 如果列是行版本控制列,則此記錄欄位的值設置為SQL_TRUE,否則SQL_FALSE。 此列屬性類似於使用SQL_ROWVER識別碼類型呼叫**SQL 特別列**,以確定列是否自動更新。  
  
 **SQL_DESC_SCALE [全部]**  
 此 SQLSMALLINT 記錄欄位包含小數點和數位數據類型的已定義比例。 對於所有其他數據類型,該欄位未定義。  
  
 此欄位中的值可能與 ODBC 2 *.x*中定義的「縮放」值不同。 關於詳細資訊,請參閱附錄[D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_SCHEMA_NAME [紅外指示]**  
 此唯讀 SQLCHAR = 記錄欄位包含包含欄位的基表的架構名稱。 如果列是表達式或列是視圖的一部分,則返回值與驅動程序相關。 如果數據源不支援架構或無法確定架構名稱,則此變數包含一個空字串。  
  
 **SQL_DESC_SEARCHABLE [紅外點]**  
 此唯讀 SQLSMALLINT 記錄欄位設定為以下值之一:  
  
-   如果列不能在**WHERE**子句中使用,則SQL_PRED_NONE。 (這與 ODBC 2 *.x 中的*SQL_UNSEARCHABLE值相同。  
  
-   SQL_PRED_CHAR該列是否可以在**WHERE**子句中使用,但只能與**LIKE**謂詞一起使用。 (這與 ODBC 2 *.x 中的*SQL_LIKE_ONLY值相同。  
  
-   SQL_PRED_BASIC該列是否可以在**WHERE**子句中使用,與除**LIKE**之外的所有比較運算符。 (這與 ODBC 2 *.x 中的*SQL_EXCEPT_LIKE值相同。  
  
-   SQL_PRED_SEARCHABLE該列是否可以在任何比較運算符的**WHERE**子句中使用。  
  
 **SQL_DESC_TABLE_NAME [IRD]**  
 此唯讀 SQLCHAR = 記錄欄位包含包含此列的基表的名稱。 如果列是表達式或列是視圖的一部分,則返回值與驅動程序相關。  
  
 **SQL_DESC_TYPE [全部]**  
 此 SQLSMALLINT 記錄欄位指定除日期時間和間隔數據類型之外的所有數據類型的簡明 SQL 或 C 資料類型。 對於日期時間和間隔數據類型,此欄位指定SQL_DATETIME或SQL_INTERVAL的詳細數據類型。  
  
 每當此欄位包含SQL_DATETIME或SQL_INTERVAL時,SQL_DESC_DATETIME_INTERVAL_CODE欄位必須包含簡潔類型的相應子代碼。 對於日期時間數據類型,SQL_DESC_TYPE包含SQL_DATETIME,並且SQL_DESC_DATETIME_INTERVAL_CODE欄位包含特定日期時間數據類型的子代碼。 對於間隔數據類型,SQL_DESC_TYPE包含SQL_INTERVAL,並且SQL_DESC_DATETIME_INTERVAL_CODE欄位包含特定間隔數據類型的子代碼。  
  
 SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE欄位中的值是相互依賴的。 每次設置其中一個字段時,還必須設置另一個字段。 SQL_DESC_TYPE可以通過調用**SQLSetDescField**或**SQLSetDescRec**來設置。 SQL_DESC_CONCISE_TYPE可以通過調用**SQLBindCol**或**SQLBind 參數**(或**SQLSetDescField)** 來設置。  
  
 如果SQL_DESC_TYPE設置為間隔或日期時間數據類型以外的簡明數據類型,則SQL_DESC_CONCISE_TYPE欄位設置為相同的值,SQL_DESC_DATETIME_INTERVAL_CODE欄位設置為 0。  
  
 如果SQL_DESC_TYPE設置為詳細日期時間或間隔數據類型(SQL_DATETIME 或SQL_INTERVAL),並且SQL_DESC_DATETIME_INTERVAL_CODE欄位設置為相應的子代碼,則SQL_DESC_CONCISE TYPE 欄位設置為相應的簡潔類型。 嘗試將SQL_DESC_TYPE設置為其中一個簡潔的日期時間或間隔類型將返回 SQLSTATE HY021(描述符資訊不一致)。  
  
 當SQL_DESC_TYPE欄位由對**SQLBindCol、SQLBind****參數**或**SQLSetDescField**的調用設置時,以下欄位將設置為以下預設值,如下表所示。 未定義同一記錄的剩餘欄位的值。  
  
|SQL_DESC_TYPE值|其他欄位隱式設定|  
|------------------------------|---------------------------------|  
|SQL_CHAR、SQL_VARCHAR、SQL_C_CHAR、SQL_C_VARCHAR|SQL_DESC_LENGTH設置為 1。 SQL_DESC_PRECISION設置為 0。|  
|SQL_DATETIME|當SQL_DESC_DATETIME_INTERVAL_CODE設置為SQL_CODE_DATE或SQL_CODE_TIME時,SQL_DESC_PRECISION設置為 0。 當它設置為SQL_DESC_TIMESTAMP時,SQL_DESC_PRECISION設置為 6。|  
|SQL_DECIMAL,SQL_NUMERIC,SQL_C_NUMERIC|SQL_DESC_SCALE設置為 0。 SQL_DESC_PRECISION設置為相應數據類型的實現定義的精度。<br /><br /> 有關如何手動綁定SQL_C_NUMERIC值的資訊,請參閱[SQL 到 C:數位](../../../odbc/reference/appendixes/sql-to-c-numeric.md)。|  
|SQL_FLOAT,SQL_C_FLOAT|SQL_DESC_PRECISION設置為SQL_FLOAT的實現定義的預設精度。|  
|SQL_INTERVAL|當SQL_DESC_DATETIME_INTERVAL_CODE設置為間隔數據類型時,SQL_DESC_DATETIME_INTERVAL_PRECISION設置為 2(預設間隔前導精度)。 當間隔具有秒分量時,SQL_DESC_PRECISION設置為 6(預設間隔秒精度)。|  
  
 當應用程式呼叫**SQLSetDescField**來設定描述符的欄位,而不是調用**SQLSetDescRec**時,應用程式必須首先聲明數據類型。 當它這樣做時,上一個表中指示的其他欄位將隱式設置。 如果隱式設置的任何值是不可接受的,則應用程式可以調用**SQLSetDescField**或**SQLSetDescRec**顯式設定不可接受的值。  
  
 **SQL_DESC_TYPE_NAME [實作描述符]**  
 此唯讀 SQLCHAR = 記錄欄位包含與資料源相關的類型名稱(例如,"CHAR"、"VARCHAR"等)。 如果資料類型名稱未知,則此變數包含一個空字串。  
  
 **SQL_DESC_UNNAMED [實作描述符]**  
 行描述符中的此 SQLSMALLINT 記錄欄位由驅動程式設定為SQL_NAMED或SQL_UNNAMED設定SQL_DESC_NAME欄位時。 如果SQL_DESC_NAME欄位包含列別名,或者列別名不適用,則驅動程式將SQL_DESC_UNNAMED欄位設置為SQL_NAMED。 如果應用程式將 IPD 的SQL_DESC_NAME欄位設置為參數名稱或別名,則驅動程式將 IPD 的SQL_DESC_UNNAMED欄位設置為SQL_NAMED。 如果沒有列名稱或列別名,驅動程式將SQL_DESC_UNNAMED欄位設置為SQL_UNNAMED。  
  
 應用程式可以將 IPD 的SQL_DESC_UNNAMED欄位設置為SQL_UNNAMED。 如果應用程式嘗試將 IPD 的SQL_DESC_UNNAMED欄位設定為SQL_NAMED,則驅動程式將返回 SQLSTATE HY091(無效描述符位元識別碼)。 IRD 的SQL_DESC_UNNAMED欄位是唯讀的;如果應用程式嘗試設定 SQLSTATE HY091(無效描述符位元號),將返回它。  
  
 **SQL_DESC_UNSIGNED [實作描述符]**  
 如果列類型未簽名或非數位,則此唯讀 SQLSMALLINT 記錄欄位設置為SQL_TRUE,如果列類型已簽名,則SQL_FALSE。  
  
 **SQL_DESC_UPDATABLE [紅外點]**  
 此唯讀 SQLSMALLINT 記錄欄位設定為以下值之一:  
  
-   如果結果集列是唯讀的,SQL_ATTR_READ_ONLY。  
  
-   如果結果集列是讀寫列,SQL_ATTR_WRITE。  
  
-   如果不知道結果集列是否可更新,SQL_ATTR_READWRITE_UNKNOWN。  
  
 SQL_DESC_UPDATABLE描述結果集中列的升數據度,而不是基表中的列。 此結果集列所基於的基表中列的升數據度可能與此欄位中的值不同。 列是否可更新可以基於數據類型、使用者許可權和結果集本身的定義。 如果不清楚列是否可更新,則應返回SQL_ATTR_READWRITE_UNKNOWN。  
  
## <a name="consistency-checks"></a>一致性檢查  
 每當應用程式通過ARD、APD或IPDSQL_DESC_DATA_PTR欄位的值時,驅動程式會自動執行一致性檢查。 如果任何欄位與其他欄位不一致 **,SQLSetDescField**將返回 SQLSTATE HY021(描述符資訊不一致)。 有關詳細資訊,請參閱[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的「一致性檢查」。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|繫結欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|繫結參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述字列|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得多個描述符位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定多個描述符位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)
