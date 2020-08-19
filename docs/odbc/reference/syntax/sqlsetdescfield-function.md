---
description: SQLSetDescField 函式
title: SQLSetDescField 函式 |Microsoft Docs
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
ms.openlocfilehash: 2c21d3a21e863d62a3cc8d685e81c6e3265c1551
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421132"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 函式

**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLSetDescField** 會設定描述項記錄的單一欄位值。  
  
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
 輸出描述項控制碼。  
  
 *RecNumber*  
 輸出表示描述項記錄，其中包含應用程式要設定的欄位。 描述項記錄是從0開始編號，記錄號碼0是書簽記錄。 標頭欄位會忽略 *RecNumber* 引數。  
  
 *FieldIdentifier*  
 輸出指出要設定其值的描述項欄位。 如需詳細資訊，請參閱「批註」一節中的「*FieldIdentifier* 引數」。  
  
 *ValuePtr*  
 輸出包含描述項資訊之緩衝區的指標，或整數值。 資料類型取決於 *FieldIdentifier*的值。 如果 *ValuePtr* 是整數值，則可能會被視為8個位元組 (SQLLEN) ，4個位元組 (SQLINTEGER) 或2個位元組 (SQLSMALLINT) ，視 *FieldIdentifier* 引數的值而定。  
  
 *BufferLength*  
 輸出如果 *FieldIdentifier* 是 ODBC 定義的欄位，而 *ValuePtr* 指向字元字串或二進位緩衝區，則這個引數應該是 **ValuePtr*的長度。 若為字元字串資料，這個引數應該包含字串中的位元組數目。  
  
 如果 *FieldIdentifier* 是 ODBC 定義的欄位，而 *ValuePtr* 是整數，則會忽略 *BufferLength* 。  
  
 如果 *FieldIdentifier* 是驅動程式定義的欄位，則應用程式會藉由設定 *BufferLength* 引數，將欄位的本質指出至驅動程式管理員。 *BufferLength* 可以有下列值：  
  
-   如果 *ValuePtr* 是字元字串的指標，則 *BufferLength* 是字串或 SQL_NTS 的長度。  
  
-   如果 *ValuePtr* 是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR (*長度*) 宏的結果放在 *BufferLength*中。 這會在 *BufferLength*中放置負數值。  
  
-   如果 *ValuePtr* 是字元字串或二進位字串以外的值指標，則 *BufferLength* 應該具有 SQL_IS_POINTER 的值。  
  
-   如果 *ValuePtr* 包含固定長度的值，則 *BufferLength* 會視需要 SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或 SQL_IS_USMALLINT。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescField**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_DESC）和*DescriptorHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLSetDescField** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01S02|選項值已變更|此驅動程式不支援在* \* ValuePtr*中指定的值 (如果*ValuePtr*是指標) 或*ValuePtr*中的值 (如果*ValuePtr*是整數值) ，或* \* ValuePtr*因為實值的使用狀況而無效，則驅動程式會取代類似的值。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07009|描述元索引無效|*FieldIdentifier*引數是記錄欄位、 *RecNumber*引數為0，而*DESCRIPTORHANDLE*引數則參考 IPD 把手。<br /><br /> *RecNumber*引數小於0，而*DescriptorHandle*引數則參考 ARD 或 APD。<br /><br /> *RecNumber*引數大於資料來源可支援的資料行或參數的最大數目，以及參考 APD 或 ARD 的*DescriptorHandle*引數。<br /><br />  (DM) *FieldIdentifier*引數是 SQL_DESC_COUNT 的，而且* \* ValuePtr*引數小於0。<br /><br /> *RecNumber*引數等於0，而*DescriptorHandle*引數則參考隱含配置的 APD。 因為明確配置的應用程式描述項不知道明確配置的應用程式描述項是否為 APD 或 ARD，所以不會發生此錯誤。 )  (|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊已截斷|*FieldIdentifier*引數 SQL_DESC_NAME，而且*BufferLength*引數的值大於 SQL_MAX_IDENTIFIER_LEN。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY010|函數順序錯誤| (DM) *DescriptorHandle* 與非同步執行函式的 *StatementHandle* 相關聯 (未呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br />  (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**是針對與*StatementHandle*相關聯並傳回 SQL_NEED_DATA 的*DescriptorHandle*所呼叫。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式，是與 *DescriptorHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLSetDescField** 函式時，仍在執行此非同步函式。<br /><br /> 針對與*DescriptorHandle*相關聯的其中一個語句控制碼呼叫 (DM) **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY016|無法修改實資料列描述項|*DescriptorHandle*引數與 IRD 相關聯，且*FieldIdentifier*引數未 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。|  
|HY021|不一致的描述項資訊|[SQL_DESC_TYPE] 和 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位不會形成有效的 ODBC SQL 類型或有效的驅動程式特定 SQL 類型 (用於 Ipd) 或適用于 Apd 或 ARDs (的有效 ODBC C 類型) 。<br /><br /> 一致性檢查期間檢查的描述項資訊不一致。  (請參閱 **SQLSetDescRec**中的「一致性檢查」。 ) |  
|HY090|不正確字串或緩衝區長度| (DM) * \* ValuePtr*是一個字元字串，而*BufferLength*小於零但不等於 SQL_NTS。<br /><br />  (DM) *驅動程式是 ODBC 2.x 驅動程式* 、描述元為 ARD、 *ColumnNumber* 引數設定為0，且為引數 *BufferLength* 指定的值不等於4。|  
|HY091|不正確描述項欄位識別碼|為 *FieldIdentifier* 引數指定的值不是 ODBC 定義的欄位，而且不是實值定義的值。<br /><br /> *DescriptorHandle*引數的*FieldIdentifier*引數無效。<br /><br /> *FieldIdentifier*引數是唯讀的 ODBC 定義欄位。|  
|HY092|不正確屬性/選項識別碼|* \* ValuePtr*中的值對*FieldIdentifier*引數無效。<br /><br /> *FieldIdentifier*引數已 SQL_DESC_UNNAMED， *ValuePtr*是 SQL_NAMED。|  
|HY105|不正確參數類型| (DM) 為 SQL_DESC_PARAMETER_TYPE 欄位指定的值無效。  (需詳細資訊，請參閱**SQLBindParameter**中的「*InputOutputType*引數」一節。 ) |  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [ODBC 3.8 中的新功能](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *DescriptorHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫 **SQLSetDescField** 來一次設定一個描述項欄位。 **SQLSetDescField**的一個呼叫會在單一描述項中設定單一欄位。 您可以呼叫這個函式，以設定任何描述元類型中的任何欄位，前提是可以設定欄位。  (請參閱本節稍後的表格。 )   
  
> [!NOTE]  
>  如果呼叫 **SQLSetDescField** 失敗，則由 *RecNumber* 引數所識別之描述項記錄的內容未定義。  
  
 您可以呼叫其他函式，使用函式的單一呼叫來設定多個描述項欄位。 **SQLSetDescRec**函數會設定各種欄位，這些欄位會影響系結至資料行或參數的資料類型和緩衝區， (SQL_DESC_TYPE、SQL_DESC_DATETIME_INTERVAL_CODE、SQL_DESC_OCTET_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 欄位) 。 您可以使用**SQLBindCol**或**SQLBindParameter**來建立資料行或參數系結的完整規格。 這些函式會使用一個函式呼叫來設定特定的描述項欄位群組。  
  
 您可以藉由將位移新增至系結指標 (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 或 SQL_DESC_OCTET_LENGTH_PTR) ，來呼叫**SQLSetDescField**來變更系結緩衝區。 這會變更系結緩衝區，而不會呼叫 **SQLBindCol** 或 **SQLBindParameter**，這可讓應用程式 SQL_DESC_DATA_PTR 變更，而不需要變更其他欄位，例如 SQL_DESC_DATA_TYPE。  
  
 如果應用程式呼叫 **SQLSetDescField** 來設定 SQL_DESC_COUNT 或延遲欄位 SQL_DESC_DATA_PTR、SQL_DESC_OCTET_LENGTH_PTR 或 SQL_DESC_INDICATOR_PTR 以外的任何欄位，記錄就會變成未系結。  
  
 描述元標頭欄位的設定方式是使用適當的*FieldIdentifier*呼叫**SQLSetDescField** 。 許多標頭欄位也是語句屬性，因此也可以透過呼叫 **SQLSetStmtAttr**來設定。 這可讓應用程式在不先取得描述項控制碼的情況下設定描述項欄位。 當呼叫 **SQLSetDescField** 來設定標頭欄位時，會忽略 *RecNumber* 引數。  
  
 *RecNumber* 0 用來設定書簽欄位。  
  
> [!NOTE]  
>  在呼叫 **SQLSetDescField** 來設定書簽欄位之前，應該一律先設定語句屬性 SQL_ATTR_USE_BOOKMARKS。 雖然這不是強制性的，但強烈建議您這樣做。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>設定描述項欄位的順序  
 藉由呼叫 **SQLSetDescField**來設定描述項欄位時，應用程式必須遵循特定的順序：  
  
1.  應用程式必須先設定 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE 或 SQL_DESC_DATETIME_INTERVAL_CODE 欄位。  
  
2.  設定這些欄位的其中一個之後，應用程式就可以設定資料類型的屬性，而驅動程式會將資料類型屬性欄位設定為資料類型的適當預設值。 自動預設的類型屬性欄位可確保描述項在應用程式指定資料類型之後，一律可供使用。 如果應用程式明確設定資料類型屬性，它會覆寫預設屬性。  
  
3.  在步驟1中所列的其中一個欄位已設定，而且已設定資料類型屬性之後，應用程式就可以設定 SQL_DESC_DATA_PTR。 這會提示描述項欄位的一致性檢查。 如果應用程式在設定 SQL_DESC_DATA_PTR 欄位之後變更資料類型或屬性，則驅動程式會將 SQL_DESC_DATA_PTR 設定為 null 指標、將記錄解除系結。 這會強制應用程式依序完成適當的步驟，然後才能使用描述項記錄。  
  
## <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定  
 配置描述項時，描述項中的欄位可以初始化為預設值、不使用預設值進行初始化，或針對描述項類型未定義。 下表指出每個類型之描述項的每個欄位初始化，並以 "D" 表示欄位是以預設值初始化，而 "ND" 表示該欄位在沒有預設值的情況下初始化。 如果顯示數位，則欄位的預設值為該數位。 這些表格也會指出欄位是否為讀取/寫入 (R/W) 或唯讀 (R) 。  
  
 IRD 的欄位只有在語句已備妥或執行，而且已填入 IRD，而不是在配置語句控制碼或描述項時，才會有預設值。 在 IRD 填入之前，嘗試存取 IRD 的欄位將會傳回錯誤。  
  
 某些描述項欄位是針對一或多個（但不是全部）描述項類型所定義 (ARDs 和 IRDs，以及 Apd 和 Ipd) 。 當某個描述項類型的欄位未定義時，任何使用該描述項的函式都不需要。  
  
 **SQLGetDescField**可以存取的欄位不一定是由**SQLSetDescField**設定。 下表列出可由 **SQLSetDescField** 設定的欄位。  
  
 標頭欄位的初始化會在接下來的表格中列出。  
  
|標頭功能變數名稱|類型|R/W|預設|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD： R APD： R IRD： R IPD： R|ARD：明確的隱含或 SQL_DESC_ALLOC_USER SQL_DESC_ALLOC_AUTO<br /><br /> APD：明確的隱含或 SQL_DESC_ALLOC_USER SQL_DESC_ALLOC_AUTO<br /><br /> IRD： SQL_DESC_ALLOC_AUTO<br /><br /> IPD： SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD： R/W APD： R/W IRD：未使用的 IPD：未使用|ARD： [1] APD： [1] IRD：未使用的 IPD：未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD： R/W APD： R/W IRD： R/W IPD： R/W|ARD： Null ptr APD： Null ptr IRD： Null ptr IPD： Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN|ARD： R/W APD： R/W IRD：未使用的 IPD：未使用|ARD： Null ptr APD： Null ptr IRD：未使用的 IPD：未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD： R/W APD： R/W IRD：未使用的 IPD：未使用|ARD： SQL_BIND_BY_COLUMN<br /><br /> APD： SQL_BIND_BY_COLUMN<br /><br /> IRD：未使用<br /><br /> IPD：未使用|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： 0 APD： 0 IRD： D IPD：0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN|ARD：未使用的 APD：未使用的 IRD： R/W IPD： R/W|ARD：未使用的 APD：未使用的 IRD： Null ptr IPD： Null ptr|  
  
 [1] 只有當驅動程式自動填入 IPD 時，才會定義這些欄位。 如果沒有，則未定義。 如果應用程式嘗試設定這些欄位，則會傳回 SQLSTATE HY091 (不正確描述項欄位識別碼) 。  
  
 記錄欄位的初始化如下表所示。  
  
|記錄欄位名稱|類型|R/W|預設|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD：未使用的 APD：未使用的 IRD： R IPD： R|ARD：未使用的 APD：未使用的 IRD： D IPD： D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： SQL_C_ 預設 APD： SQL_C_ 預設 IRD： D IPD： ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD： R/W APD： R/W IRD：未使用的 IPD：未使用|ARD： Null ptr APD： Null ptr IRD：未使用的 IPD：未使用 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD： R IPD： R|ARD：未使用的 APD：未使用的 IRD： D IPD： D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN|ARD： R/W APD： R/W IRD：未使用的 IPD：未使用|ARD： Null ptr APD： Null ptr IRD：未使用的 IPD：未使用|  
|SQL_DESC_LABEL|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_LENGTH|SQLULEN|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD： R|ARD：未使用的 APD：未使用的 IRD： D IPD： D [1]|  
|SQL_DESC_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD： R IPD： R|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN|ARD： R/W APD： R/W IRD：未使用的 IPD：未使用|ARD： Null ptr APD： Null ptr IRD：未使用的 IPD：未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD：未使用的 IPD： R/W|ARD：未使用的 APD：未使用的 IRD：未使用的 IPD： D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD：未使用<br /><br /> APD：未使用<br /><br /> IRD： R<br /><br /> IPD： R|ARD：未使用<br /><br /> APD：未使用<br /><br /> IRD： ND<br /><br /> IPD： ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD： R/W APD： R/W IRD： R IPD： R/W|ARD： SQL_C_DEFAULT APD： SQL_C_DEFAULT IRD： D IPD： ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR|ARD：未使用的 APD：未使用的 IRD： R IPD： R|ARD：未使用的 APD：未使用的 IRD： D IPD： D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD： R IPD： R/W|ARD： ND APD： ND IRD： D IPD： ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD： R IPD： R|ARD：未使用的 APD：未使用的 IRD： D IPD： D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD：未使用的 APD：未使用的 IRD： R IPD：未使用|ARD：未使用的 APD：未使用的 IRD： D IPD：未使用|  
  
 [1] 只有當驅動程式自動填入 IPD 時，才會定義這些欄位。 如果沒有，則未定義。 如果應用程式嘗試設定這些欄位，則會傳回 SQLSTATE HY091 (不正確描述項欄位識別碼) 。  
  
 [2] 您可以設定 IPD 中的 SQL_DESC_DATA_PTR 欄位來強制執行一致性檢查。 在後續呼叫 **SQLGetDescField** 或 **SQLGetDescRec**時，驅動程式不需要傳回 SQL_DESC_DATA_PTR 設定為的值。  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 引數  
 *FieldIdentifier*引數表示要設定的描述項欄位。 描述項包含描述項 *標頭，* 其中包含下一節中所述的標頭欄位、「標頭欄位」和零或多個描述項 *記錄，* 其中包含 [標頭欄位] 一節中所述的記錄欄位。  
  
## <a name="header-fields"></a>標頭欄位  
 每個描述項都有由下欄欄位組成的標頭：  
  
 **SQL_DESC_ALLOC_TYPE [全部]**  
 這個唯讀的 SQLSMALLINT 標頭欄位會指定驅動程式是由驅動程式自動設定，或由應用程式明確配置描述項。 應用程式可以取得（但不能修改）此欄位。 如果驅動程式已自動設定描述元，則此欄位會設定為由驅動程式 SQL_DESC_ALLOC_AUTO。 如果應用程式已明確配置描述項，則會將它設定為由驅動程式 SQL_DESC_ALLOC_USER。  
  
 **SQL_DESC_ARRAY_SIZE [應用程式描述項]**  
 在 ARDs 中，這個 SQLULEN 標頭欄位會指定資料列集中的資料列數目。 這是呼叫 **SQLFetch** 或 **SQLFetchScroll** ，或藉由呼叫 **SQLBulkOperations** 或 **SQLSetPos**來操作時，所要傳回的資料列數目。  
  
 在 Apd 中，這個 SQLULEN 標頭欄位會指定每個參數的值數目。  
  
 此欄位的預設值為1。 如果 SQL_DESC_ARRAY_SIZE 大於1、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR，以及陣列的 APD 或 ARD 點 SQL_DESC_OCTET_LENGTH_PTR。 每個陣列的基數都等於這個欄位的值。  
  
 您也可以呼叫具有 SQL_ATTR_ROW_ARRAY_SIZE 屬性的 **SQLSetStmtAttr** ，來設定 ARD 中的這個欄位。 您也可以呼叫具有 SQL_ATTR_PARAMSET_SIZE 屬性的 **SQLSetStmtAttr** ，來設定 APD 中的這個欄位。  
  
 **SQL_DESC_ARRAY_STATUS_PTR [全部]**  
 針對每個描述項類型，這個 SQLUSMALLINT * 標頭欄位會指向 SQLUSMALLINT 值的陣列。 這些陣列的命名如下：資料列狀態陣列 (IRD) 、參數狀態陣列 (IPD) 、資料列作業陣列 (ARD) 和參數運算元組 (APD) 。  
  
 在 IRD 中，此標頭欄位會指向 **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或 **SQLSetPos**的呼叫之後的資料列狀態陣列，其中包含狀態值。 陣列的元素數目與資料列集中的資料列數目相同。 應用程式必須配置 SQLUSMALLINTs 的陣列，並將此欄位設定為指向陣列。 依預設，此欄位會設為 null 指標。 此驅動程式將會填入陣列-除非 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為 null 指標，在這種情況下不會產生狀態值，也不會填入陣列。  
  
> [!CAUTION]  
>  如果應用程式設定 IRD 的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指向之資料列狀態陣列的元素，則驅動程式行為是未定義的。  
  
 陣列最初是透過呼叫 **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或 **SQLSetPos**來填入。 如果呼叫未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，此欄位所指向的陣列內容會是未定義的。 陣列中的元素可以包含下列值：  
  
-   SQL_ROW_SUCCESS：資料列已成功提取，且自上次提取以來尚未變更。  
  
-   SQL_ROW_SUCCESS_WITH_INFO：資料列已成功提取，且自上次提取以來尚未變更。 但是，傳回有關資料列的警告。  
  
-   SQL_ROW_ERROR：提取資料列時發生錯誤。  
  
-   SQL_ROW_UPDATED：資料列已成功提取，且自上次提取之後已更新。 如果再次提取資料列，它的狀態會是 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_DELETED：資料列自上次提取之後已刪除。  
  
-   SQL_ROW_ADDED： **SQLBulkOperations**插入資料列。 如果再次提取資料列，它的狀態會是 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_NOROW：資料列集重迭了結果集的結尾，而且沒有傳回任何資料列，對應至資料列狀態陣列的這個元素。  
  
 您也可以呼叫具有 SQL_ATTR_ROW_STATUS_PTR 屬性的 **SQLSetStmtAttr** ，來設定 IRD 中的這個欄位。  
  
 IRD 的 SQL_DESC_ARRAY_STATUS_PTR 欄位只有在 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 傳回之後才有效。 如果傳回碼不是其中一種，則 SQL_DESC_ROWS_PROCESSED_PTR 指向的位置會是未定義的。  
  
 在 IPD 中，此標頭欄位會指向參數狀態陣列，其中包含呼叫 **SQLExecute** 或 **SQLExecDirect**之後每組參數值的狀態資訊。 如果對 **SQLExecute** 或 **SQLExecDirect** 的呼叫未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，此欄位所指向的陣列內容會是未定義的。 應用程式必須配置 SQLUSMALLINTs 的陣列，並將此欄位設定為指向陣列。 此驅動程式將會填入陣列-除非 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為 null 指標，在這種情況下不會產生狀態值，也不會填入陣列。 陣列中的元素可以包含下列值：  
  
-   SQL_PARAM_SUCCESS：已成功針對這組參數執行 SQL 語句。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO：已成功針對這組參數執行 SQL 語句;不過，診斷資料結構中有提供警告資訊。  
  
-   SQL_PARAM_ERROR：處理這組參數時發生錯誤。 診斷資料結構提供其他錯誤資訊。  
  
-   SQL_PARAM_UNUSED：未使用此參數集，可能是因為某些先前的參數集造成中止進一步處理的錯誤，或因為已針對 APD 的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指定的陣列中的一組參數設定 SQL_PARAM_IGNORE。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE：無法使用診斷資訊。 其中一個範例就是當驅動程式將參數陣列視為整合式單位時，不會產生此層級的錯誤資訊。  
  
 您也可以使用 SQL_ATTR_PARAM_STATUS_PTR 屬性來呼叫 **SQLSetStmtAttr** ，以設定 IPD 中的這個欄位。  
  
 在 ARD 中，這個標頭欄位會指向一個值的資料列作業陣列，這些值可以由應用程式設定，以指出是否要針對 **SQLSetPos** 作業忽略此資料列。 陣列中的元素可以包含下列值：  
  
-   SQL_ROW_PROCEED：使用 **SQLSetPos**的大量作業中包含資料列。  (這種設定並不保證會在資料列上進行操作。 如果資料列的狀態 SQL_ROW_ERROR 在 IRD 資料列狀態陣列中，驅動程式可能無法在資料列中執行此作業。 )   
  
-   SQL_ROW_IGNORE：使用 **SQLSetPos**從大量作業中排除資料列。  
  
 如果未設定陣列的元素，則大量作業中會包含所有資料列。 如果 ARD 的 [SQL_DESC_ARRAY_STATUS_PTR] 欄位中的值為 null 指標，則所有資料列都會包含在大量作業中;轉譯與指向有效陣列的指標，以及陣列的所有元素都 SQL_ROW_PROCEED 一樣。 如果陣列中的元素設定為 SQL_ROW_IGNORE，則不會變更已忽略之資料列的資料列狀態陣列中的值。  
  
 您也可以呼叫具有 SQL_ATTR_ROW_OPERATION_PTR 屬性的 **SQLSetStmtAttr** ，來設定 ARD 中的這個欄位。  
  
 在 APD 中，此標頭欄位會指向可由應用程式設定之值的參數作業陣列，以指出呼叫 **SQLExecute** 或 **SQLExecDirect** 時，是否要忽略這組參數。 陣列中的元素可以包含下列值：  
  
-   SQL_PARAM_PROCEED：參數集包含在 **SQLExecute** 或 **SQLExecDirect** 呼叫中。  
  
-   SQL_PARAM_IGNORE：從 **SQLExecute** 或 **SQLExecDirect** 呼叫中排除參數集。  
  
 如果未設定陣列的元素，則會在 **SQLExecute** 或 **SQLExecDirect** 呼叫中使用陣列中的所有參數集合。 如果 APD 的 [SQL_DESC_ARRAY_STATUS_PTR] 欄位中的值為 null 指標，則會使用所有的參數集;轉譯與指向有效陣列的指標，以及陣列的所有元素都 SQL_PARAM_PROCEED 一樣。  
  
 您也可以呼叫具有 SQL_ATTR_PARAM_OPERATION_PTR 屬性的 **SQLSetStmtAttr** ，來設定 APD 中的這個欄位。  
  
 **SQL_DESC_BIND_OFFSET_PTR [應用程式描述項]**  
 這個 SQLLEN * 標頭欄位會指向系結位移。 預設會將它設定為 null 指標。 如果這個欄位不是 null 指標，驅動程式會對指標進行取值，並將取值值加入至描述項記錄中具有非 null 值的每個延後欄位， (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR) SQL_DESC_OCTET_LENGTH_PTR 和在系結時使用新的指標值。  
  
 系結位移一律會直接加入至 [SQL_DESC_DATA_PTR]、[SQL_DESC_INDICATOR_PTR] 和 [SQL_DESC_OCTET_LENGTH_PTR] 欄位中的值。 如果位移變更為不同的值，則新值仍會直接加入至每個描述項欄位中的值。 新的位移不會加入域值加上任何先前的位移。  
  
 此欄位是 *延後欄位*：在設定時不會使用此欄位，而且當驅動程式稍後需要判斷資料緩衝區的位址時，就會使用此欄位。  
  
 您也可以呼叫具有 SQL_ATTR_ROW_BIND_OFFSET_PTR 屬性的 **SQLSetStmtAttr** ，來設定 ARD 中的這個欄位。 您也可以呼叫具有 SQL_ATTR_PARAM_BIND_OFFSET_PTR 屬性的 **SQLSetStmtAttr** ，來設定 ARD 中的這個欄位。  
  
 如需詳細資訊，請參閱 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 和 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)中的資料列取向系結描述。  
  
 **SQL_DESC_BIND_TYPE [應用程式描述項]**  
 這個 SQLUINTEGER 標頭欄位會設定要用於系結資料行或參數的系結方向。  
  
 在 ARDs 中，這個欄位會指定在相關聯的語句控制碼上呼叫 **SQLFetchScroll** 或 **SQLFetch** 時的系結方向。  
  
 若要選取資料行的資料行取向系結，這個欄位會設定為 SQL_BIND_BY_COLUMN (預設) 。  
  
 您也可以呼叫具有 SQL_ATTR_ROW_BIND_TYPE*屬性*的**SQLSetStmtAttr** ，來設定 ARD 中的這個欄位。  
  
 在 Apd 中，這個欄位會指定要用於動態參數的系結方向。  
  
 若要選取參數的資料行取向系結，這個欄位會設定為 SQL_BIND_BY_COLUMN (預設) 。  
  
 您也可以呼叫具有 SQL_ATTR_PARAM_BIND_TYPE*屬性*的**SQLSetStmtAttr** ，來設定 APD 中的這個欄位。  
  
 **SQL_DESC_COUNT [全部]**  
 這個 SQLSMALLINT 標頭欄位會指定包含資料之最高編號記錄的以1為起始的索引。 當驅動程式設定描述項的資料結構時，它也必須設定 SQL_DESC_COUNT 欄位來顯示有多少筆記錄。 當應用程式佈建此資料結構的實例時，不需要指定保留空間的記錄數目。 當應用程式指定記錄的內容時，驅動程式會採取任何必要的動作，以確保描述項控制碼參考適當大小的資料結構。  
  
 SQL_DESC_COUNT 不是系結 (的所有資料行計數（如果欄位是在 ARD) 中），或者如果欄位是在 APD) 中，則是所有系結 (的參數，但最高編號記錄的編號。 如果最高編號的資料行或參數未系結，則 SQL_DESC_COUNT 會變更為下一個最高編號的資料行或參數的編號。 如果資料行或參數的數位小於最高編號的資料行數目， (則會呼叫**SQLBindCol** ，並將*TargetValuePtr*引數設定為 null 指標，或使用*ParameterValuePtr*引數設定為) null 指標的**SQLBindParameter** ，而不會變更 SQL_DESC_COUNT。 如果其他資料行或參數系結的數位大於包含資料的最高編號記錄，驅動程式會自動增加 [SQL_DESC_COUNT] 欄位中的值。 如果使用 SQL_UNBIND 選項呼叫 **SQLFreeStmt** 來解除系結所有資料行，則 ARD 和 IRD 中的 SQL_DESC_COUNT 欄位會設定為0。 如果使用 SQL_RESET_PARAMS 選項來呼叫 **SQLFreeStmt** ，APD 和 IPD 中的 SQL_DESC_COUNT 欄位會設定為0。  
  
 藉由呼叫 **SQLSetDescField**，應用程式可以明確設定 SQL_DESC_COUNT 中的值。 如果 SQL_DESC_COUNT 中的值已明確減少，則會有效地移除數位大於 SQL_DESC_COUNT 中新值的所有記錄。 如果 SQL_DESC_COUNT 中的值明確設定為0，而且欄位位於 ARD 中，則會釋放系結書簽資料行以外的所有資料緩衝區。  
  
 ARD 的這個欄位中的記錄計數不包含系結的書簽資料行。 解除書簽資料行的唯一方法，是將 SQL_DESC_DATA_PTR 欄位設定為 null 指標。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [實描述項]**  
 在 IRD 中，這個 SQLULEN \* 標頭欄位會指向一個緩衝區，其中包含呼叫 **SQLFetch** 或 **SQLFetchScroll**之後所提取的資料列數目，或對 **SQLBulkOperations** 或 **SQLSetPos**的呼叫所執行之大量作業所影響的資料列數目，包括錯誤資料列。  
  
 在 IPD 中，此 SQLUINTEGER * 標頭欄位會指向包含已處理之參數集數目的緩衝區，包括錯誤集。 如果這是 null 指標，則不會傳回任何數位。  
  
 SQL_SUCCESS_WITH_INFO SQL_SUCCESS 只有在呼叫 SQLFetch 或 SQLFetchScroll (以進行 IRD 欄位) 或**SQLExecute**、 **SQLExecDirect**或**SQLPARAMDATA** (（適用于 IPD 欄位) ）的**SQLFetch**或**SQLFetchScroll**之後，SQL_DESC_ROWS_PROCESSED_PTR 才有效。 如果填入此欄位所指向之緩衝區的呼叫不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則不會定義緩衝區的內容，除非它傳回 SQL_NO_DATA，在此情況下，緩衝區中的值會設定為0。  
  
 您也可以呼叫具有 SQL_ATTR_ROWS_FETCHED_PTR 屬性的 **SQLSetStmtAttr** ，來設定 ARD 中的這個欄位。 您也可以呼叫具有 SQL_ATTR_PARAMS_PROCESSED_PTR 屬性的 **SQLSetStmtAttr** ，來設定 APD 中的這個欄位。  
  
 此欄位所指向的緩衝區是由應用程式所配置。 它是驅動程式所設定的延遲輸出緩衝區。 預設會將它設定為 null 指標。  
  
## <a name="record-fields"></a>記錄欄位  
 每個描述項都包含一個或多個記錄，這些記錄是由定義資料行資料或動態參數的欄位所組成，視描述項的類型而定。 每一筆記錄都是單一資料行或參數的完整定義。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 如果資料行是自動遞增資料行，這個唯讀的 SQLINTEGER 記錄欄位包含 SQL_TRUE，或者，如果資料行不是自動遞增資料行，則為 SQL_FALSE。 此欄位是唯讀的，但基礎自動遞增資料行不一定是唯讀的。  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含結果集資料行的基底資料行名稱。 如果基底資料行名稱不存在 (如運算式) 的資料行案例中，此變數包含空字串。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含結果集資料行的基表名稱。 如果無法定義基表名稱或其不適用，則此變數包含空字串。  
  
 **SQL_DESC_CASE_SENSITIVE [實描述項]**  
 如果資料行或參數視為區分大小寫的定序和比較，則這個唯讀的 SQLINTEGER 記錄欄位包含 SQL_TRUE; 如果資料行的定序和比較不區分大小寫，則為 SQL_FALSE，或者，如果它是非字元資料行，則為。  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含包含資料行之基表的目錄。 如果資料行是運算式，或者資料行是視圖的一部分，則傳回值為驅動程式相依。 如果資料來源不支援目錄或無法判斷目錄，則此變數包含空字串。  
  
 **SQL_DESC_CONCISE_TYPE [全部]**  
 這個 SQLSMALLINT 標頭欄位會為所有資料類型（包括 datetime 和 interval 資料類型）指定簡潔的資料類型。  
  
 [SQL_DESC_CONCISE_TYPE]、[SQL_DESC_TYPE] 和 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位中的值是相互依存的。 每次設定其中一個欄位時，也必須設定另一個欄位。 SQL_DESC_CONCISE_TYPE 可以透過呼叫 **SQLBindCol** 或 **SQLBindParameter**或 **SQLSetDescField**來設定。 SQL_DESC_TYPE 可以透過呼叫 **SQLSetDescField** 或 **SQLSetDescRec**來設定。  
  
 如果 SQL_DESC_CONCISE_TYPE 設定為資料類型，而不是間隔或日期時間資料類型，則 SQL_DESC_TYPE 欄位會設定為相同的值，而且 SQL_DESC_DATETIME_INTERVAL_CODE 欄位會設定為0。  
  
 如果 SQL_DESC_CONCISE_TYPE 設定為 [簡潔 datetime] 或 [interval] 資料類型，則 SQL_DESC_TYPE 欄位會設定為對應的 [詳細資訊類型] (SQL_DATETIME 或 SQL_INTERVAL) ，而且 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位會設定為適當的子代碼。  
  
 **SQL_DESC_DATA_PTR [應用程式描述元和 Ipd]**  
 這個 SQLPOINTER 記錄欄位指向的變數將包含 Apd) 的參數值 (，或 ARDs) 的資料行值 (。 此欄位是 *延後欄位*。 它在設定時不會使用，但稍後會由驅動程式用來取出資料。  
  
 如果對**SQLBindCol**的呼叫中的*TargetValuePtr*引數為 null 指標，或如果 ARD 中的 SQL_DESC_DATA_PTR 欄位是由對**SQLSetDescField**或**SQLSetDescRec**的呼叫設定為 null 指標，則 ARD 的 SQL_DESC_DATA_PTR 欄位所指定的資料行就會解除系結。 如果 SQL_DESC_DATA_PTR 欄位設定為 null 指標，則不會影響其他欄位。  
  
 如果 **SQLFetch** 或 **SQLFetchScroll** 的呼叫填入此欄位所指向的緩衝區時，不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則不會定義緩衝區的內容。  
  
 每當設定 APD、ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式就會檢查 [SQL_DESC_TYPE] 欄位中的值是否包含其中一個有效的 ODBC C 資料類型或驅動程式特定的資料類型，而且影響資料類型的其他所有欄位都是一致的。 提示一致性檢查是唯一使用 IPD 的 SQL_DESC_DATA_PTR 欄位。 尤其是，如果應用程式設定 IPD 的 SQL_DESC_DATA_PTR 欄位，而稍後呼叫此欄位上的 **SQLGetDescField** ，則不一定會傳回已設定的值。 如需詳細資訊，請參閱 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的「一致性檢查」。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [全部]**  
 當 SQL_DESC_TYPE 欄位 SQL_DATETIME 或 SQL_INTERVAL 時，此 SQLSMALLINT 記錄欄位包含特定 datetime 或 interval 資料類型的子代碼。 這對 SQL 和 C 資料類型都是如此。 此程式碼包含使用 "CODE" 來取代 "TYPE" 或 "C_TYPE" (適用于 datetime 類型) 的資料類型名稱，或 "CODE" 取代間隔類型 (的 "C_INTERVAL") 。  
  
 如果應用程式描述項的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定為 SQL_C_DEFAULT，且描述項未與語句控制碼相關聯，則 SQL_DESC_DATETIME_INTERVAL_CODE 的內容為未定義。  
  
 您可以針對下表所列的日期時間資料類型設定此欄位。  
  
|日期時間類型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 您可以針對下表所列的間隔資料類型設定此欄位。  
  
|間隔類型|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
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
|SQL_INTERVAL_YEAR/SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 如需有關資料間隔和這個欄位的詳細資訊，請參閱 [資料類型識別碼和描述](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)元。  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [全部]**  
 如果 SQL_INTERVAL SQL_DESC_TYPE 欄位，此 SQLINTEGER 記錄欄位包含間隔前置精確度。 當 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為 interval 資料類型時，此欄位會設定為預設的間隔有效位數。  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 這個唯讀 SQLINTEGER 記錄欄位包含顯示資料行資料所需的最大字元數。  
  
 **SQL_DESC_FIXED_PREC_SCALE [實描述項]**  
 如果資料行是精確的數值資料行，而且具有固定的有效位數和非零值，SQL_FALSE 或如果資料行不是具有固定有效位數和小數位數的精確數值資料行，就會將這個唯讀 SQLSMALLINT 記錄欄位設定為 SQL_TRUE。  
  
 **SQL_DESC_INDICATOR_PTR [應用程式描述項]**  
 在 ARDs 中，此 SQLLEN * 記錄欄位指向指標變數。 如果資料行值為 Null，則此變數包含 SQL_Null_DATA。 若為 Apd，則會將指標變數設定為 SQL_Null_DATA，以指定 Null 動態引數。 否則，除非 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 中的值) 相同的指標，否則變數為零 (。  
  
 如果 ARD 中的 SQL_DESC_INDICATOR_PTR 欄位為 null 指標，驅動程式就無法傳回有關資料行是否為 Null 的資訊。 如果資料行是 Null，且 SQL_DESC_INDICATOR_PTR 為 null 指標，則當驅動程式在呼叫 **SQLFetch** 或 **SQLFetchScroll**之後嘗試填入緩衝區時，就會傳回 SQLSTATE 22002 (指標變數，但未提供) 。 如果對 **SQLFetch** 或 **SQLFetchScroll** 的呼叫未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則不會定義緩衝區的內容。  
  
 SQL_DESC_INDICATOR_PTR 欄位會決定是否已設定 SQL_DESC_OCTET_LENGTH_PTR 所指向的欄位。 如果資料行的資料值為 Null，驅動程式會將指標變數設定為 SQL_Null_DATA。 然後，SQL_DESC_OCTET_LENGTH_PTR 所指向的欄位就不會設定。 如果提取期間未發生 Null 值，SQL_DESC_INDICATOR_PTR 所指向的緩衝區會設定為零，而且 SQL_DESC_OCTET_LENGTH_PTR 所指向的緩衝區會設定為數據的長度。  
  
 如果 APD 中的 SQL_DESC_INDICATOR_PTR 欄位為 null 指標，則應用程式無法使用此描述項記錄來指定 Null 引數。  
  
 此欄位是 *延後欄位*：在設定時不會使用它，但稍後會由驅動程式用來指出 ARDs) 的 null 屬性 (或判斷 apd) 的可 null 性 (。  
  
 **SQL_DESC_LABEL [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含資料行標籤或標題。 如果資料行沒有標籤，此變數就會包含資料行名稱。 如果資料行未命名且未標記，則此變數包含空字串。  
  
 **SQL_DESC_LENGTH [全部]**  
 這個 SQLULEN 記錄欄位是字元字串的最大長度或實際長度（以位元組為單位）或二進位資料類型（以位元組為單位）。 這是固定長度資料類型的最大長度，或是可變長度資料類型的實際長度。 它的值一律會排除結束字元字串的 null 終止字元。 對於類型為 SQL_TYPE_DATE、SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP 或其中一個 SQL interval 資料類型的值，此欄位的長度（以字元表示的日期時間或間隔值的字元字串表示）。  
  
 此欄位中的值可能與 ODBC 2.x 中定義的 "length" 的值*不同。* 如需詳細資訊，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含驅動程式辨識為此資料類型之常值前置詞的字元。 此變數包含不適用常值前置詞之資料類型的空字串。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含驅動程式辨識為此資料類型之常值尾碼的字元。 此變數包含不適用常值尾碼之資料類型的空字串。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [實描述項]**  
 這個唯讀的 SQLCHAR * 記錄欄位包含資料類型的任何當地語系化 (原生語言) 名稱，該資料類型可能與資料類型的一般名稱不同。 如果沒有當地語系化的名稱，則會傳回空字串。 此欄位僅供顯示之用。  
  
 **SQL_DESC_NAME [實描述項]**  
 資料列描述項中的這個 SQLCHAR * 記錄欄位包含資料行別名（如果有的話）。 如果資料行別名不適用，就會傳回資料行名稱。 無論是哪一種情況，驅動程式都會將 SQL_DESC_UNNAMED 欄位設定為在設定 SQL_DESC_NAME 欄位時 SQL_NAMED。 如果沒有資料行名稱或資料行別名，驅動程式會在 SQL_DESC_NAME 欄位中傳回空字串，並將 SQL_DESC_UNNAMED 欄位設定為 SQL_UNNAMED。  
  
 應用程式可以將 IPD 的 SQL_DESC_NAME 欄位設定為參數名稱或別名，以依名稱指定預存程式參數。  (如需詳細資訊，請參閱 [ (具名引數的名稱系結參數) ](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。 ) IRD 的 [SQL_DESC_NAME] 欄位是唯讀欄位;SQLSTATE HY091 (不正確描述項欄位識別碼) 將會在應用程式嘗試設定時傳回。  
  
 在 Ipd 中，如果驅動程式不支援具名引數，則這個欄位是未定義的。 如果驅動程式支援具名引數，而且能夠描述參數，則會在此欄位中傳回參數名稱。  
  
 **SQL_DESC_NullABLE [實描述項]**  
 在 IRDs 中，如果資料行可以有 Null 值，則會 SQL_NullABLE 此唯讀 SQLSMALLINT 記錄欄位，SQL_NO_NullS 如果資料行沒有 Null 值，則為，如果資料行不知道資料行是否接受 Null 值，則為 SQL_NullABLE_UNKNOWN。 此欄位與結果集資料行有關，而不是基底資料行。  
  
 在 Ipd 中，此欄位一律設定為 SQL_NullABLE，因為動態參數永遠可為 null，而且不能由應用程式設定。  
  
 **SQL_DESC_NUM_PREC_RADIX [全部]**  
 如果 [SQL_DESC_TYPE] 欄位中的資料類型是近似的數值資料類型，這個 SQLINTEGER 欄位就會包含2的值，因為 SQL_DESC_PRECISION 欄位包含的位數。 如果 [SQL_DESC_TYPE] 欄位中的資料類型是精確數值資料類型，此欄位就會包含10值，因為 SQL_DESC_PRECISION 欄位包含十進位數。 所有非數值資料類型的這個欄位都設定為0。  
  
 **SQL_DESC_OCTET_LENGTH [全部]**  
 這個 SQLLEN 記錄欄位包含字元字串或二進位資料類型的長度（以位元組為單位）。 若為固定長度的字元或二進位類型，這是實際的長度（以位元組為單位）。 若為可變長度的字元或二進位類型，這是最大長度（以位元組為單位）。 此值一律會排除實值的 null 終止字元空格，而且一律會包含應用程式描述項的 null 終止字元空間。 針對應用程式資料，此欄位包含緩衝區的大小。 若為 Apd，則只會針對輸出或輸入/輸出參數定義此欄位。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [應用程式描述項]**  
 這個 SQLLEN * 記錄欄位指向的變數將包含參數描述項的動態引數 (的總長度（以位元組為單位）) 或資料列描述項)  (的系結資料行值。  
  
 若為 APD，除了字元字串和二進位字元以外，所有引數都會忽略此值;如果這個欄位指向 SQL_NTS，動態引數必須以 null 結束。 為了指出系結的參數將是資料執行中的參數，應用程式會將適當 APD 記錄中的這個欄位設定為變數，而在執行時間會包含 SQL_LEN_DATA_AT_EXEC 宏的值 SQL_DATA_AT_EXEC 或結果。 如果有多個這類欄位，則可以將 SQL_DESC_DATA_PTR 設定為可唯一識別參數的值，以協助應用程式判斷所要求的參數。  
  
 如果 ARD 的 OCTET_LENGTH_PTR 欄位為 null 指標，驅動程式就不會傳回資料行的長度資訊。 如果 APD 的 SQL_DESC_OCTET_LENGTH_PTR 欄位為 null 指標，驅動程式會假設字元字串和二進位值以 null 終止。  (二進位值不應以 null 終止，但應獲得長度以避免截斷。 )   
  
 如果 **SQLFetch** 或 **SQLFetchScroll** 的呼叫填入此欄位所指向的緩衝區時，不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則不會定義緩衝區的內容。 此欄位是 *延後欄位*。 它在設定時不會使用，但稍後會由驅動程式用來判斷或指出資料的八位長度。  
  
 **SQL_DESC_PARAMETER_TYPE [Ipd]**  
 這個 SQLSMALLINT 記錄欄位設定為輸入參數的 SQL_PARAM_INPUT、輸入/輸出參數的 SQL_PARAM_INPUT_OUTPUT、輸出參數的 SQL_PARAM_OUTPUT、輸入/輸出資料流程參數的 SQL_PARAM_INPUT_OUTPUT_STREAM，或輸出資料流程參數的 SQL_PARAM_OUTPUT_STREAM。 預設會將它設定為 SQL_PARAM_INPUT。  
  
 如果是 IPD，則在預設情況下，如果 IPD 未由驅動程式自動填入，則此欄位會設定為 SQL_PARAM_INPUT (SQL_ATTR_ENABLE_AUTO_IPD 語句屬性 SQL_FALSE) 。 應用程式應該在 IPD 中為非輸入參數的參數設定此欄位。  
  
 **SQL_DESC_PRECISION [全部]**  
 這個 SQLSMALLINT 記錄欄位包含精確數數值型別的位數、尾數中的位數 (二進位精確度) 的近似數數值型別，或 SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP 或 SQL_INTERVAL_SECOND 資料類型的小數秒陣列件中的位數數位。 所有其他資料類型的這個欄位都是未定義的。  
  
 此欄位中的值可能與 ODBC 2.x 中定義的「精確度」值*不同。* 如需詳細資訊，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_ROWVER [實描述項]**  
 這個 SQLSMALLINTrecord 欄位指出當資料列更新時，DBMS 是否會自動修改資料行 (例如，SQL Server) 中類型 "timestamp" 的資料行。 如果資料行是資料列版本設定資料行，此 [記錄] 欄位的值會設為 SQL_TRUE，否則為 SQL_FALSE。 此資料行屬性類似于使用 IdentifierType 的 SQL_ROWVER 來呼叫 **SQLSpecialColumns** ，以判斷是否會自動更新資料行。  
  
 **SQL_DESC_SCALE [全部]**  
 這個 SQLSMALLINT 記錄欄位包含小數和數值資料類型的定義小數位數。 所有其他資料類型的欄位都是未定義的。  
  
 此欄位中的值可能與 ODBC 2.x 中定義的 "scale" 值*不同。* 如需詳細資訊，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含包含資料行之基表的架構名稱。 如果資料行是運算式，或者資料行是視圖的一部分，則傳回值為驅動程式相依。 如果資料來源不支援架構，或無法判斷架構名稱，則此變數包含空字串。  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 這個唯讀的 SQLSMALLINT 記錄欄位設定為下列其中一個值：  
  
-   如果資料行不能用在 **WHERE** 子句中，則為 SQL_PRED_NONE。  (這與 ODBC 2.x 中的 SQL_UNSEARCHABLE 值*相同。 ) *  
  
-   SQL_PRED_CHAR 如果資料行可以在 **WHERE** 子句中使用，但只用于 **LIKE** 述詞。  (這與 ODBC 2.x 中的 SQL_LIKE_ONLY 值*相同。 ) *  
  
-   SQL_PRED_BASIC 如果資料行可以在 **WHERE** 子句中搭配所有比較運算子（ **如 LIKE**）使用。  (這與 ODBC 2.x 中的 SQL_EXCEPT_LIKE 值*相同。 ) *  
  
-   如果資料行可以在 **WHERE** 子句中搭配任何比較運算子使用，則為 SQL_PRED_SEARCHABLE。  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含包含此資料行之基表的名稱。 如果資料行是運算式，或者資料行是視圖的一部分，則傳回值為驅動程式相依。  
  
 **SQL_DESC_TYPE [全部]**  
 這個 SQLSMALLINT 記錄欄位會為所有資料類型指定簡潔的 SQL 或 C 資料類型，但 datetime 和 interval 資料類型除外。 若為 datetime 和 interval 資料類型，這個欄位會指定詳細資料類型，也就是 SQL_DATETIME 或 SQL_INTERVAL。  
  
 每當此欄位包含 SQL_DATETIME 或 SQL_INTERVAL 時，SQL_DESC_DATETIME_INTERVAL_CODE 欄位必須包含適用于精簡型別的適當子代碼。 若為 datetime 資料類型，SQL_DESC_TYPE 包含 SQL_DATETIME，而 SQL_DESC_DATETIME_INTERVAL_CODE 欄位包含特定 datetime 資料類型的子代碼。 對於間隔資料類型，SQL_DESC_TYPE 包含 SQL_INTERVAL，而 SQL_DESC_DATETIME_INTERVAL_CODE 欄位包含特定間隔資料類型的子代碼。  
  
 [SQL_DESC_TYPE] 和 [SQL_DESC_CONCISE_TYPE] 欄位中的值是相互依存的。 每次設定其中一個欄位時，也必須設定另一個欄位。 SQL_DESC_TYPE 可以透過呼叫 **SQLSetDescField** 或 **SQLSetDescRec**來設定。 SQL_DESC_CONCISE_TYPE 可以透過呼叫 **SQLBindCol** 或 **SQLBindParameter**或 **SQLSetDescField**來設定。  
  
 如果 SQL_DESC_TYPE 設定為資料類型，而不是間隔或日期時間資料類型，則 SQL_DESC_CONCISE_TYPE 欄位會設定為相同的值，而且 SQL_DESC_DATETIME_INTERVAL_CODE 欄位會設定為0。  
  
 如果 SQL_DESC_TYPE 設定為 verbose datetime 或 interval 資料類型 (SQL_DATETIME 或 SQL_INTERVAL) 而且 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為適當的子代碼，則 [SQL_DESC_CONCISE 型別] 欄位會設定為對應的精確類型。 嘗試將 SQL_DESC_TYPE 設定為其中一個精確的 datetime 或 interval 類型，將會傳回 SQLSTATE HY021 (不一致的描述項資訊) 。  
  
 當 SQL_DESC_TYPE 欄位設定為 **SQLBindCol**、 **SQLBindParameter**或 **SQLSetDescField**的呼叫時，會將下欄欄位設定為下列預設值，如下表所示。 相同記錄的其餘欄位值未定義。  
  
|SQL_DESC_TYPE 的值|隱含設定的其他欄位|  
|------------------------------|---------------------------------|  
|SQL_CHAR、SQL_VARCHAR、SQL_C_CHAR、SQL_C_VARCHAR|SQL_DESC_LENGTH 設定為1。 SQL_DESC_PRECISION 設定為0。|  
|SQL_DATETIME|當 SQL_DESC_DATETIME_INTERVAL_CODE 設定為 SQL_CODE_DATE 或 SQL_CODE_TIME 時，SQL_DESC_PRECISION 會設定為0。 當它設定為 SQL_DESC_TIMESTAMP 時，SQL_DESC_PRECISION 會設定為6。|  
|SQL_DECIMAL、SQL_NUMERIC SQL_C_NUMERIC|SQL_DESC_SCALE 設定為0。 針對個別資料類型，SQL_DESC_PRECISION 設定為執行定義的有效位數。<br /><br /> 如需有關如何手動系結 SQL_C_NUMERIC 值的詳細資訊，請參閱 [SQL 至 C：數位](../../../odbc/reference/appendixes/sql-to-c-numeric.md) 。|  
|SQL_FLOAT，SQL_C_FLOAT|SQL_DESC_PRECISION 設定為 SQL_FLOAT 的執行定義預設精確度。|  
|SQL_INTERVAL|當 SQL_DESC_DATETIME_INTERVAL_CODE 設定為 INTERVAL 資料類型時，SQL_DESC_DATETIME_INTERVAL_PRECISION 會設定為 2 (預設的間隔) 有效位數。 當間隔有 seconds 的元件時，SQL_DESC_PRECISION 設定為 6 (預設間隔秒精確度) 。|  
  
 當應用程式呼叫 **SQLSetDescField** 來設定描述項的欄位，而不是呼叫 **SQLSetDescRec**時，應用程式必須先宣告資料類型。 當它執行時，會隱含地設定上表中指出的其他欄位。 如果有任何隱含設定的值無法接受，則應用程式可以呼叫 **SQLSetDescField** 或 **SQLSetDescRec** ，以明確地設定無法接受的值。  
  
 **SQL_DESC_TYPE_NAME [實描述項]**  
 這個唯讀 SQLCHAR * 記錄欄位包含資料來源相依的型別名稱 (例如 "CHAR"、"VARCHAR" 等等) 。 如果資料類型名稱未知，則此變數包含空字串。  
  
 **SQL_DESC_UNNAMED [實描述項]**  
 在設定 SQL_DESC_NAME 欄位時，驅動程式會將資料列描述項中的這個 SQLSMALLINT 記錄欄位設定為 SQL_NAMED 或 SQL_UNNAMED。 如果 SQL_DESC_NAME 欄位包含資料行別名，或是資料行別名不適用，驅動程式會將 SQL_DESC_UNNAMED 欄位設定為 SQL_NAMED。 如果應用程式將 IPD 的 SQL_DESC_NAME 欄位設定為參數名稱或別名，驅動程式會將 IPD 的 SQL_DESC_UNNAMED 欄位設定為 SQL_NAMED。 如果沒有資料行名稱或資料行別名，驅動程式會將 SQL_DESC_UNNAMED 欄位設定為 SQL_UNNAMED。  
  
 應用程式可以將 IPD 的 SQL_DESC_UNNAMED 欄位設定為 SQL_UNNAMED。 如果應用程式嘗試將 IPD 的 SQL_DESC_UNNAMED 欄位設定為 SQL_NAMED，驅動程式會傳回 SQLSTATE HY091 (不正確描述項欄位識別碼) 。 IRD 的 SQL_DESC_UNNAMED 欄位是唯讀的;SQLSTATE HY091 (不正確描述項欄位識別碼) 將會在應用程式嘗試設定時傳回。  
  
 **SQL_DESC_UNSIGNED [實描述項]**  
 如果資料行類型不帶正負號或非數位，則這個唯讀的 SQLSMALLINT 記錄欄位會設定為 SQL_TRUE，或者，如果資料行類型已簽署，則會 SQL_FALSE。  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 這個唯讀的 SQLSMALLINT 記錄欄位設定為下列其中一個值：  
  
-   如果結果集資料行是唯讀的，則為 SQL_ATTR_READ_ONLY。  
  
-   如果結果集資料行是讀寫，則為 SQL_ATTR_WRITE。  
  
-   如果不知道結果集資料行是否可更新，請 SQL_ATTR_READWRITE_UNKNOWN。  
  
 SQL_DESC_UPDATABLE 描述結果集中資料行的更新，而不是基表中的資料行。 此結果集資料行所依據之基表中的資料行可更新性，可能會與此欄位中的值不同。 資料行是否可更新是以資料類型、使用者權限和結果集本身的定義為基礎。 如果不清楚資料行是否可更新，則應該傳回 SQL_ATTR_READWRITE_UNKNOWN。  
  
## <a name="consistency-checks"></a>一致性檢查  
 當應用程式傳入 ARD、APD 或 IPD 的 SQL_DESC_DATA_PTR 欄位值時，驅動程式會自動執行一致性檢查。 如果有任何欄位與其他欄位不一致， **SQLSetDescField** 會傳回 SQLSTATE HY021 (不一致的描述項資訊) 。 如需詳細資訊，請參閱 [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)中的「一致性檢查」。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|系結資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|系結參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)
