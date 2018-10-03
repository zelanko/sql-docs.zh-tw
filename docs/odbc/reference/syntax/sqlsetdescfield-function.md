---
title: SQLSetDescField 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44a3cfe212fcd452307a6aef0aedd1c22ca4e545
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47717128"
---
# <a name="sqlsetdescfield-function"></a>SQLSetDescField 函式
**合規性**  
 版本導入： ODBC 3.0 版的標準符合性： ISO 92  
  
 **摘要**  
 **SQLSetDescField**設定描述項記錄的單一欄位的值。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>引數  
 *DescriptorHandle*  
 [輸入]描述項控制代碼。  
  
 *RecNumber*  
 [輸入]表示包含應用程式試圖設定之欄位的描述項記錄。 描述項記錄編號為 0，0 表示書籤記錄的記錄號碼。 *RecNumber*標頭欄位會忽略引數。  
  
 *FieldIdentifier*  
 [輸入]表示要設定其值的描述元的欄位。 如需詳細資訊，請參閱 「*FieldIdentifier*引數""註解 」 一節。  
  
 *ValuePtr*  
 [輸入]包含描述元資訊或整數值之緩衝區的指標。 資料類型而定的值*FieldIdentifier*。 如果*ValuePtr*是整數值，它可能會被視為 8 個位元組 (SQLLEN)、 4 個位元組 (SQLINTEGER) 或 2 個位元組 (SQLSMALLINT，) 的值而定*FieldIdentifier*引數。  
  
 *BufferLength*  
 [輸入]如果*FieldIdentifier*是 ODBC 定義欄位並*ValuePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度 **ValuePtr*。 字元字串資料，這個引數應該包含在字串中的位元組數目。  
  
 如果*FieldIdentifier*是 ODBC 定義欄位並*ValuePtr*是一個整數， *Columnsize*會被忽略。  
  
 如果*FieldIdentifier*驅動程式定義的欄位，應用程式設定指出欄位給驅動程式管理員性質*Columnsize*引數。 *BufferLength*可以有下列值：  
  
-   如果*ValuePtr*是字元字串的指標，則*Columnsize*是 sql_nts; 之字串的長度。  
  
-   如果*ValuePtr*為二進位的緩衝區的指標，則應用程式會放 SQL_LEN_BINARY_ATTR 的結果 (*長度*) 中的巨集*Columnsize*。 這會放在負值*Columnsize*。  
  
-   如果*ValuePtr*是字元字串或二進位字串以外的值的指標，則*Columnsize*應有 SQL_IS_POINTER 的值。  
  
-   如果*ValuePtr*包含固定長度的值，則*Columnsize*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT，還是 SQL_IS_USMALLINT，適當地。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetDescField**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的SQL_HANDLE_DESC 並*處理*的*DescriptorHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetDescField** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|驅動程式不支援指定的值 *\*ValuePtr* (如果*ValuePtr*是指標) 或中的值*ValuePtr* (如果*ValuePtr*是整數值)，或是 *\*ValuePtr*無效，因為實作運作的情況，因此驅動程式取代成類似的值。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|描述項索引無效|*FieldIdentifier*引數就是 [記錄] 欄位中， *RecNumber*引數為 0，而*DescriptorHandle* IPD 的控制代碼的參考引數。<br /><br /> *RecNumber*引數為小於 0，而*DescriptorHandle* ARD 或 APD 指引數。<br /><br /> *RecNumber*引數為大於最大數目的資料行或參數可支援資料來源，而*DescriptorHandle* APD 或 ARD 參考的引數。<br /><br /> (DM) *FieldIdentifier*引數為 SQL_DESC_COUNT，及 *\*ValuePtr*引數為小於 0。<br /><br /> *RecNumber*引數是等於 0，而*DescriptorHandle*隱含配置 APD 參考引數。 （這個錯誤就不需要明確配置的應用程式描述項，因為不知道應用程式明確配置描述元是 APD 或 ARD 直到執行時間。）|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊已截斷|*FieldIdentifier*引數是與 SQL_DESC_NAME，而*Columnsize*引數為大於 SQL_MAX_IDENTIFIER_LEN 的值。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY010|函數順序錯誤|(DM) *DescriptorHandle*與建立關聯*StatementHandle*以非同步方式執行的函式 （不這一個） 的呼叫和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*與其*DescriptorHandle*已相關聯，並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*DescriptorHandle*。 此非同步函式仍在執行時**SQLSetDescField**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對其中一個相關聯的陳述式控制代碼呼叫*DescriptorHandle*且傳回 SQL_PARAM_DATA_AVAILABLE。 資料已擷取所有的資料流參數前呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY016|無法修改實作資料列描述項|*DescriptorHandle*引數為相關聯的 IRD，而*FieldIdentifier*引數不是 SQL_DESC_ARRAY_STATUS_PTR 或 SQL_DESC_ROWS_PROCESSED_PTR。|  
|HY021|不一致的描述元資訊|電子郵件地址 和 SQL_DESC_DATETIME_INTERVAL_CODE SQL_DESC_TYPE 欄位並非來自有效的 ODBC SQL 類型的有效驅動程式專屬 SQL 型別 （Ipd) 或有效的 ODBC C 類型 （適用於 Apd 或 ARDs）。<br /><br /> 描述項一致性檢查期間檢查的資訊不一致。 (請參閱 「 一致性檢查 」 中的**SQLSetDescRec**。)|  
|HY090|字串或緩衝區長度無效|(DM)  *\*ValuePtr*是字元字串，以及*Columnsize*小於零，但不是等於 SQL_NTS。<br /><br /> (DM) 驅動程式的 ODBC 2 *.x*驅動程式，描述元是 ARD， *ColumnNumber*引數設定為 0，並指定引數的值*Columnsize*已不等於 4。|  
|HY091|無效的描述項欄位識別碼|指定的值*FieldIdentifier*引數不是 ODBC 定義的欄位，而並沒有實作定義的值。<br /><br /> *FieldIdentifier*引數無效*DescriptorHandle*引數。<br /><br /> *FieldIdentifier*引數為唯讀、 ODBC 定義的欄位。|  
|HY092|屬性/選項識別碼無效|中的值 *\*ValuePtr*不是適用於*FieldIdentifier*引數。<br /><br /> *FieldIdentifier*引數是將 SQL_DESC_UNNAMED，及*ValuePtr*已 SQL_NAMED。|  
|包含 SQLSTATE=HY105|無效的參數類型|(DM) 指定 SQL_DESC_PARAMETER_TYPE 欄位的值無效。 (如需詳細資訊，請參閱 「*了*引數 」 一節**SQLBindParameter**。)|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[What's New in ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*DescriptorHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式可以呼叫**SQLSetDescField**一次設定其中任何描述項欄位。 若要一次呼叫**SQLSetDescField**單一的描述項中設定的單一欄位。 此函式可以呼叫以設定任何欄位中任何描述項類型，提供可設定的欄位。 （請參閱本節稍後的表格）。  
  
> [!NOTE]  
>  如果呼叫**SQLSetDescField**失敗時，所識別的描述項記錄的內容*RecNumber*引數是未定義。  
  
 若要設定透過單一呼叫的函式的多個描述項欄位，可以呼叫其他函式。 **SQLSetDescRec**函式會設定各種不同的欄位資料型別和緩衝區繫結至資料行或參數 （SQL_DESC_TYPE、 SQL_DESC_DATETIME_INTERVAL_CODE、 SQL_DESC_OCTET_LENGTH、 SQL_DESC_PRECISION、 SQL_ 影響DESC_SCALE、 SQL_DESC_DATA_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 欄位）。 **SQLBindCol**或是**SQLBindParameter**可用來進行繫結的資料行或參數的完整規格。 這些函式會將特定群組的一個函式呼叫的描述項欄位。  
  
 **SQLSetDescField**可以呼叫以將位移新增至繫結指標 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 或 SQL_DESC_OCTET_LENGTH_PTR） 來變更繫結緩衝區。 這會變更繫結緩衝區，而不會呼叫**SQLBindCol**或是**SQLBindParameter**，可讓應用程式而不需要變更其他欄位，例如 SQL_DESC_DATA_ 變更 SQL_DESC_DATA_PTR型別。  
  
 如果應用程式呼叫**SQLSetDescField**為設定 SQL_DESC_COUNT 以外的任何欄位或延後的欄位 SQL_DESC_DATA_PTR、 SQL_DESC_OCTET_LENGTH_PTR 或 SQL_DESC_INDICATOR_PTR，記錄就會變成未繫結。  
  
 描述項標頭欄位會設定藉由呼叫**SQLSetDescField**適當*FieldIdentifier*。 許多標頭欄位也是陳述式屬性，因此也可以設定由呼叫**SQLSetStmtAttr**。 這可讓應用程式設定不含第一個取得描述項控制代碼的描述項欄位。 當**SQLSetDescField**來設定標頭欄位中，會呼叫*RecNumber*引數會被忽略。  
  
 A *RecNumber*為 0 用來設定書籤的欄位。  
  
> [!NOTE]  
>  陳述式屬性 SQL_ATTR_USE_BOOKMARKS 應一律設定之前先呼叫**SQLSetDescField**設定書籤欄位。 雖然這不是必要項目，強烈建議。  
  
## <a name="sequence-of-setting-descriptor-fields"></a>設定描述項欄位的順序  
 當設定描述項欄位，藉由呼叫**SQLSetDescField**，應用程式必須遵循特定的順序：  
  
1.  應用程式必須先設定的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 或 SQL_DESC_DATETIME_INTERVAL_CODE 欄位。  
  
2.  設定其中一個欄位之後，應用程式可設定的資料類型，屬性和驅動程式設定資料類型的屬性欄位的資料類型的適當的預設值。 自動將預設型別屬性欄位，可確保的描述元一律可供使用後具有指定的資料類型的應用程式。 如果應用程式明確地設定資料型別屬性，它會覆寫預設的屬性。  
  
3.  已設定其中一個步驟 1 中所列的欄位，並已設定資料型別屬性之後，應用程式可以設定 SQL_DESC_DATA_PTR。 這會提示描述項欄位的一致性檢查。 如果應用程式變更的資料型別或屬性，設定 SQL_DESC_DATA_PTR 欄位之後，驅動程式會設定為 null 指標，解除繫結資料錄的 SQL_DESC_DATA_PTR。 這會強制應用程式，依序完成適當的步驟，可描述項記錄之前。  
  
## <a name="initialization-of-descriptor-fields"></a>描述項欄位的初始設定  
 當配置描述元時，描述元中的欄位可以初始化為預設值，沒有預設值，初始化或是未定義類型的描述元。 下表指出每種類型的描述元，使用"D"表示該欄位預設值，初始化和"ND"表示該欄位沒有預設值初始化的每個欄位的初始化。 如果會顯示數字，該欄位的預設值是該數字。 資料表也會指出欄位是否為讀取/寫入 (R/W) 或唯讀狀態 (R)。  
  
 IRD 欄位的預設值之後才有尚未準備或執行陳述式和 IRD 填入之後，不會在已配置的陳述式控制代碼或描述元。 直到 IRD 填入之後，任何嘗試存取的 IRD 欄位會傳回錯誤。  
  
 某些描述項欄位會定義一個或多個，但不是全部的描述項類型 （ARDs 和 IRDs，和 Apd 和 Ipd）。 未定義類型的描述項欄位時，它就不需要任何使用該描述元的函式。  
  
 可以存取的欄位**SQLGetDescField**一定無法由設定**SQLSetDescField**。 可藉由設定欄位**SQLSetDescField**詳列於下表。  
  
 下表概述標頭欄位的初始化。  
  
|標頭欄位名稱|類型|R/W|預設|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: 針對 SQL_DESC_ALLOC_AUTO 隱含或 SQL_DESC_ALLOC_USER 的明確<br /><br /> APD: SQL_DESC_ALLOC_AUTO 的隱含或 SQL_DESC_ALLOC_USER 的明確<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: [1] APD: [1] 的 IRD： 未使用的 IPD： 未使用|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|ARD: R/W APD: R/W IRD: IPD R/W: R/W|ARD: Null ptr APD: Null ptr IRD: Null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD： 未使用<br /><br /> IPD： 未使用|  
SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: 0 APD: IRD 0: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|ARD： 未使用的 APD： 未使用的 IRD: R/W IPD: R/W|ARD： 未使用的 APD： 未使用的 IRD: Null ptr IPD: Null ptr|  
  
 [只有當驅動程式會自動填入 IPD 時，會定義 1] 這些欄位。 如果沒有，也就是未定義。 如果應用程式嘗試設定這些欄位，SQLSTATE HY091 （無效的描述項欄位識別碼） 將會傳回。  
  
 記錄欄位的初始化是下表所示。  
  
|記錄欄位名稱|類型|R/W|預設|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: SQL_C_ 預設 APD: SQL_C_ 預設 IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用的 [2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用|  
|SQL_DESC_LABEL|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_LENGTH|SQLULEN|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD： 未使用的 IPD： 未使用|ARD: Null ptr APD: Null ptr IRD： 未使用 IPD： 未使用|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD： 未使用的 IPD: R/W|ARD： 未使用的 APD： 未使用的 IRD： 未使用的 IPD: D = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD： 未使用<br /><br /> APD： 未使用<br /><br /> IRD: R<br /><br /> IPD: R|ARD： 未使用<br /><br /> APD： 未使用<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: IRD R/W: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
SQL_DESC_TYPE_NAME|SQLCHAR *|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD: R|ARD： 未使用的 APD： 未使用的 IRD: D IPD: D [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD： 未使用的 APD： 未使用的 IRD: R IPD： 未使用|ARD： 未使用的 APD： 未使用的 IRD: D IPD： 未使用|  
  
 [只有當驅動程式會自動填入 IPD 時，會定義 1] 這些欄位。 如果沒有，也就是未定義。 如果應用程式嘗試設定這些欄位，SQLSTATE HY091 （無效的描述項欄位識別碼） 將會傳回。  
  
 [IPD 中的 2] 的 SQL_DESC_DATA_PTR 欄位可以設定來強制執行一致性檢查。 在後續呼叫**SQLGetDescField**或是**SQLGetDescRec**，驅動程式不需要傳回 SQL_DESC_DATA_PTR 已設為值。  
  
## <a name="fieldidentifier-argument"></a>FieldIdentifier 引數  
 *FieldIdentifier*引數表示要設定描述項欄位。 描述元包含*描述項標頭*下一節中，「 標頭欄位 」，以及零或多個描述的標頭欄位所組成*描述項記錄*記錄欄位所組成一節下 「 標頭欄位 」 一節所述。  
  
## <a name="header-fields"></a>標頭欄位  
 每個描述項有標頭包含下列欄位：  
  
 **[All] SQL_DESC_ALLOC_TYPE**  
 這個唯讀 SQLSMALLINT 標頭欄位會指定是否描述項配置會自動由驅動程式或明確的應用程式。 應用程式可以取得，但不是能修改此欄位。 欄位是設為 SQL_DESC_ALLOC_AUTO 驅動程式所驅動程式會自動配置描述元。 它是如果設定為 SQL_DESC_ALLOC_USER 驅動程式應用程式所明確配置描述元。  
  
 **SQL_DESC_ARRAY_SIZE [應用程式描述項]**  
 ARDs，在此 SQLULEN 標頭欄位會指定資料列集中的資料列數目。 這是藉由呼叫傳回資料列數目**SQLFetch**或是**SQLFetchScroll** ，或藉由呼叫來操作**SQLBulkOperations**或**SQLSetPos**.  
  
 Apd，在此 SQLULEN 標頭欄位會指定每個參數的值數目。  
  
 此欄位的預設值為 1。 如果 SQL_DESC_ARRAY_SIZE 大於 1，SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR APD 或 ARD 指向陣列。 每個陣列的基數等於這個欄位的值。  
  
 也可以藉由呼叫設定此欄位中 ARD **SQLSetStmtAttr**使用 SQL_ATTR_ROW_ARRAY_SIZE 屬性。 APD 中的這個欄位也可以藉由呼叫設定**SQLSetStmtAttr** SQL_ATTR_PARAMSET_SIZE 屬性。  
  
 **[All] SQL_DESC_ARRAY_STATUS_PTR**  
 針對每個描述項類型，而此 SQLUSMALLINT * 標頭欄位會指向陣列的 SQLUSMALLINT 值。 這些陣列的命名方式如下： 資料列狀態陣列 (IRD) 中，參數狀態陣列 (IPD) 中，資料列作業陣列 (ARD) 和參數作業陣列 (APD)。  
  
 在 IRD 此標頭欄位會指向資料列狀態陣列，包含在呼叫之後的狀態值**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 陣列的資料列集內有資料列的項目數。 應用程式必須配置 SQLUSMALLINTs 的陣列，並設定為指向陣列的這個欄位。 根據預設，欄位是設為 null 指標。 驅動程式將會填入陣列 — 除非 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為 null 指標，在此情況下產生沒有狀態值，而且不會填入陣列。  
  
> [!CAUTION]  
>  如果應用程式設定的資料列狀態陣列 IRD SQL_DESC_ARRAY_STATUS_PTR 欄位所指的項目，則驅動程式行為是未定義。  
  
 在一開始填入陣列的呼叫所**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 如果呼叫未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，此欄位所指陣列的內容為未定義。 陣列中的項目可以包含下列值：  
  
-   SQL_ROW_SUCCESS: 資料列已成功擷取，而且尚未變更，因為它一次擷取。  
  
-   SQL_ROW_SUCCESS_WITH_INFO: 資料列已成功擷取，而且尚未變更，因為它一次擷取。 不過，資料列相關的已傳回警告。  
  
-   SQL_ROW_ERROR： 提取資料列時發生錯誤。  
  
-   SQL_ROW_UPDATED： 已成功擷取的資料列，以及自上次擷取後已經更新。 如果再次擷取資料列，其狀態會是 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_DELETED： 已經刪除的資料列，因為它一次擷取。  
  
-   SQL_ROW_ADDED： 已插入資料列**SQLBulkOperations**。 如果再次擷取資料列，其狀態會是 SQL_ROW_SUCCESS。  
  
-   SQL_ROW_NOROW： 重疊的資料列集結果集的結尾，並傳回任何資料列，對應至資料列狀態陣列的這個項目。  
  
 也可以藉由呼叫設定此欄位在 IRD **SQLSetStmtAttr** sql_attr_row_status_ptr 設定屬性。  
  
 只有在傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 之後，才有效 IRD 的 SQL_DESC_ARRAY_STATUS_PTR 欄位。 如果傳回的程式碼不是其中一種，SQL_DESC_ROWS_PROCESSED_PTR 所指向的位置會是未定義。  
  
 在 IPD，此標頭欄位會指向包含每一組參數值之後呼叫的狀態資訊的參數狀態陣列**SQLExecute**或是**SQLExecDirect**。 如果在呼叫**SQLExecute**或是**SQLExecDirect**未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，此欄位所指陣列的內容為未定義。 應用程式必須配置 SQLUSMALLINTs 的陣列，並設定為指向陣列的這個欄位。 驅動程式將會填入陣列 — 除非 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為 null 指標，在此情況下產生沒有狀態值，而且不會填入陣列。 陣列中的項目可以包含下列值：  
  
-   SQL_PARAM_SUCCESS： 這一集的參數成功執行的 SQL 陳述式。  
  
-   SQL_PARAM_SUCCESS_WITH_INFO： 這一集的參數，成功地執行 SQL 陳述式不過，警告資訊可在診斷資料結構。  
  
-   SQL_PARAM_ERROR： 處理這組參數時發生錯誤。 使用診斷資料結構中的其他錯誤資訊。  
  
-   SQL_PARAM_UNUSED： 這個參數集為未使用，可能是因為，一些先前的參數集而造成錯誤中止進一步處理，或因為 SQL_PARAM_IGNORE 設定該 SQL_DESC_ARRAY_ 所指定之陣列中的參數集APD STATUS_PTR 欄位。  
  
-   SQL_PARAM_DIAG_UNAVAILABLE： 未提供診斷資訊。 這個範例是資訊的當驅動程式會將參數陣列視為單一單位，因此不會產生此層級時發生錯誤。  
  
 也可以藉由呼叫設定此欄位在 IPD **SQLSetStmtAttr** SQL_ATTR_PARAM_STATUS_PTR 屬性。  
  
 在 ARD，此標頭欄位會指向一個值，可以設定應用程式，以指出此資料列是否要忽略的資料列作業陣列**SQLSetPos**作業。 陣列中的項目可以包含下列值：  
  
-   SQL_ROW_PROCEED： 該資料列包含在大量作業中使用**SQLSetPos**。 （此設定並不保證此作業會在資料列上進行。 如果資料列狀態 SQL_ROW_ERROR IRD 資料列狀態陣列中的，驅動程式可能無法執行作業的資料列中。）  
  
-   SQL_ROW_IGNORE： 從大量作業使用排除的資料列**SQLSetPos**。  
  
 如果不設定陣列的任何項目，在大量作業中包含的所有資料列。 如果 ARD SQL_DESC_ARRAY_STATUS_PTR 欄位中的值是 null 指標，所有資料列會包含在大量作業。指標指向有效的陣列且陣列的所有項目已 SQL_ROW_PROCEED 解譯都是相同的。 如果陣列中的項目設定為 SQL_ROW_IGNORE，已忽略的資料列的資料列狀態陣列中的值不會變更。  
  
 也可以藉由呼叫設定此欄位中 ARD **SQLSetStmtAttr** SQL_ATTR_ROW_OPERATION_PTR 屬性。  
  
 APD 中，在此標頭欄位會指向參數作業陣列的值可以設定應用程式，以表示這組參數是否要忽略的時機**SQLExecute**或**SQLExecDirect**呼叫。 陣列中的項目可以包含下列值：  
  
-   SQL_PARAM_PROCEED： 一組參數納入**SQLExecute**或是**SQLExecDirect**呼叫。  
  
-   SQL_PARAM_IGNORE： 一組參數會從排除**SQLExecute**或是**SQLExecDirect**呼叫。  
  
 如果不設定陣列的任何項目，在中使用的參數陣列中的所有組**SQLExecute**或是**SQLExecDirect**呼叫。 如果 APD 中的 [SQL_DESC_ARRAY_STATUS_PTR] 欄位中的值是 null 指標，則會使用所有的參數集;指標指向有效的陣列且陣列的所有項目已 SQL_PARAM_PROCEED 解譯都是相同的。  
  
 APD 中的這個欄位也可以藉由呼叫設定**SQLSetStmtAttr** SQL_ATTR_PARAM_OPERATION_PTR 屬性。  
  
 **SQL_DESC_BIND_OFFSET_PTR [應用程式描述項]**  
 這是 SQLLEN * 標頭欄位會指向繫結位移。 根據預設，它會設定為 null 指標。 如果此欄位不是 null 指標，驅動程式會取值指標，並將已取值的值加入至每個延遲欄位 （SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR） 描述項記錄中具有非 null 值在擷取的時間，並使用新的指標值繫結時。  
  
 繫結位移是一律直接新增至 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位中的值。 如果位移變更為不同的值，新的值是仍然直接新增至每個描述項欄位中的值。 新的位移不會加入至欄位值，加上任何先前的位移。  
  
 這個欄位是*延後的欄位*： 它不會在其設定，但可在稍後由驅動程式需要判斷資料緩衝區的位址時的時間。  
  
 也可以藉由呼叫設定此欄位中 ARD **SQLSetStmtAttr** SQL_ATTR_ROW_BIND_OFFSET_PTR 屬性。 也可以藉由呼叫設定此欄位中 ARD **SQLSetStmtAttr** SQL_ATTR_PARAM_BIND_OFFSET_PTR 屬性。  
  
 如需詳細資訊，請參閱中的資料列取向繫結的描述[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)並[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)。  
  
 **SQL_DESC_BIND_TYPE [應用程式描述項]**  
 此 SQLUINTEGER 標頭欄位會設定要用於繫結資料行或參數的繫結方向。  
  
 ARDs，在此欄位會指定繫結方向時**SQLFetchScroll**或是**SQLFetch**相關聯的陳述式控制代碼上呼叫。  
  
 若要選取資料行的資料行取向繫結，此欄位設為 SQL_BIND_BY_COLUMN （預設值）。  
  
 也可以藉由呼叫設定此欄位中 ARD **SQLSetStmtAttr**使用 SQL_ATTR_ROW_BIND_TYPE*屬性*。  
  
 Apd 中，在此欄位會指定要用於動態參數的繫結方向。  
  
 若要選取資料行取向的繫結參數，此欄位設為 SQL_BIND_BY_COLUMN （預設值）。  
  
 APD 中的這個欄位也可以藉由呼叫設定**SQLSetStmtAttr**與 SQL_ATTR_PARAM_BIND_TYPE*屬性*。  
  
 **[All] SQL_DESC_COUNT**  
 此 SQLSMALLINT 標頭欄位會指定包含資料的最高編號記錄 1 為基底的索引。 當驅動程式設定的描述元的資料結構時，它也必須設定 SQL_DESC_COUNT 欄位，以顯示多少筆記錄都很重要。 當應用程式配置此資料結構的執行個體時，它並沒有指定要保留的空間的多少筆記錄。 如應用程式指定記錄的內容，驅動程式會接受任何必要的動作，以確保描述項控制代碼會參考適當大小的資料結構。  
  
 SQL_DESC_COUNT 不是計數 （如果欄位是 ARD） 繫結的所有資料行或所有的參數會繫結 （如果欄位是 APD 中），但最高編號的記錄數目。 如果最高編號的資料行或參數未繫結時，則會變更 SQL_DESC_COUNT 的下一個最高編號的資料行或參數數目。 如果資料行或參數，以數字小於最高編號的資料行數目是未繫結 (藉由呼叫**SQLBindCol**具有*TargetValuePtr*引數設定為 null 指標或**SQLBindParameter**具有*ParameterValuePtr*引數設定為 null 指標)，則不會變更 SQL_DESC_COUNT。 如果其他資料行或參數數字大於最高編號的記錄，其中包含資料繫結，驅動程式會自動增加 SQL_DESC_COUNT 欄位中的值。 如果所有資料行藉由呼叫未繫結**SQLFreeStmt**使用 SQL_UNBIND 選項時，在 IRD 中 ARD SQL_DESC_COUNT 欄位會設定為 0。 如果**SQLFreeStmt**稱為 SQL_RESET_PARAMS 選項時，在 APD 和 IPD SQL_DESC_COUNT 欄位會設定為 0。  
  
 SQL_DESC_COUNT 中的值可以明確設定的應用程式藉由呼叫**SQLSetDescField**。 如果明確地減少 SQL_DESC_COUNT 中的值，有效地移除大於 SQL_DESC_COUNT 中的新值的數字的所有記錄。 如果 SQL_DESC_COUNT 中的值明確設定為 0，且欄位處於 ARD，會釋放繫結的書籤資料行除外的所有資料緩衝區。  
  
 在此欄位的 ARD 中的記錄計數不包含繫結的書籤資料行。 書籤資料行解除繫結的唯一方法是設定 SQL_DESC_DATA_PTR 欄位為 null 指標。  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [實作描述元]**  
 在 IRD 此 SQLULEN\*標頭欄位會指向包含在呼叫之後擷取的資料列數目的緩衝區**SQLFetch**或是**SQLFetchScroll**，或大量作業中受影響的資料列數目由呼叫**SQLBulkOperations**或是**SQLSetPos**，包括錯誤資料列。  
  
 在 IPD，此 SQLUINTEGER * 標頭欄位會指向包含集合的已處理，包括錯誤集的參數數目的緩衝區。 如果這是 null 指標，則會不傳回任何數字。  
  
 只有在已呼叫後傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 之後，才是有效 SQL_DESC_ROWS_PROCESSED_PTR **SQLFetch**或**SQLFetchScroll** （適用於一個 IRD 欄位中） 或**SQLExecute**， **SQLExecDirect**，或**SQLParamData** （適用於 IPD 欄位）。 如果呼叫，以填滿緩衝區中所指的這個欄位不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容會未定義，除非它傳回 sql_no_data 為止，案例在緩衝區中的值設定為 0。  
  
 也可以藉由呼叫設定此欄位中 ARD **SQLSetStmtAttr** SQL_ATTR_ROWS_FETCHED_PTR 屬性。 APD 中的這個欄位也可以藉由呼叫設定**SQLSetStmtAttr** SQL_ATTR_PARAMS_PROCESSED_PTR 屬性。  
  
 此欄位所指向的緩衝區會配置應用程式。 它是驅動程式所設定的延後的輸出緩衝區。 根據預設，它會設定為 null 指標。  
  
## <a name="record-fields"></a>記錄欄位  
 每個描述元會包含資料行的資料或動態參數，根據描述元的類型定義的欄位所組成的一或多個記錄。 每一筆記錄是單一資料行或參數的完整定義。  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 此唯讀 SQLINTEGER 記錄欄位包含 SQL_TRUE，資料行是否自動遞增資料行或 SQL_FALSE 如果資料行不是自動遞增資料行。 此欄位是唯讀的但基礎的自動遞增資料行不是一定是唯讀的。  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含基底資料行名稱，結果集資料行。 如果基底的資料行名稱不存在 （如所示的是運算式的資料行的情況下），此變數包含空字串。  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含基底資料表名稱，結果集資料行。 如果基底資料表名稱不能定義，或不適用，則此變數包含空字串。  
  
 **SQL_DESC_CASE_SENSITIVE [實作描述元]**  
 這個唯讀 SQLINTEGER 記錄欄位包含 SQL_TRUE，如果資料行或參數來處理為區分大小寫的定序和比較或 SQL_FALSE 如果資料行也不會處理定序和比較為區分大小寫，或就非字元資料行。  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含基底資料表包含資料行的目錄。 如果資料行是運算式或資料行是否屬於檢視，傳回的值會是驅動程式相關。 如果資料來源不支援目錄，或無法判斷目錄，此變數包含空字串。  
  
 **[All] SQL_DESC_CONCISE_TYPE**  
 這個 SQLSMALLINT 標頭欄位會指定所有的資料類型，包括 datetime 和間隔資料類型的精確資料類型。  
  
 橫條、 的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE，SQL_DESC_DATETIME_INTERVAL_CODE 欄位中的值都相互依賴。 設定每次一個欄位，另也必須設定。 可以藉由呼叫設定 SQL_DESC_CONCISE_TYPE **SQLBindCol**或是**SQLBindParameter**，或**SQLSetDescField**。 可以藉由呼叫設定 SQL_DESC_TYPE **SQLSetDescField**或是**SQLSetDescRec**。  
  
 如果 SQL_DESC_CONCISE_TYPE 設定為精簡的資料類型的間隔或 datetime 資料類型以外的 SQL_DESC_TYPE 欄位設定為相同的值和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為 0。  
  
 SQL_DESC_CONCISE_TYPE 設定為精簡的日期時間或間隔資料類型，如果 SQL_DESC_TYPE 欄位設定為對應的詳細資訊型別 （如果是 SQL_DATETIME 或 SQL_INTERVAL） 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為適當的次要代碼。  
  
 **[應用程式描述項和 Ipd] 的 SQL_DESC_DATA_PTR**  
 此 SQLPOINTER 資料錄的欄位會指向將包含的參數值 （Apd) 或 （適用於 ARDs) 的資料行值的變數。 這個欄位是*延後的欄位*。 它不會在其設定，但在稍後由驅動程式用來擷取資料的時間。  
  
 ARD 的 SQL_DESC_DATA_PTR 欄位所指定的資料行是未繫結，如果*TargetValuePtr*呼叫中的引數**SQLBindCol**為 null 指標，或如果 SQL_DESC_DATA_PTR 欄位中設定 ARD若要呼叫**SQLSetDescField**或是**SQLSetDescRec**為 null 指標。 如果設定 SQL_DESC_DATA_PTR 欄位為 null 指標，不會影響其他欄位。  
  
 如果在呼叫**SQLFetch**或是**SQLFetchScroll** ，在此欄位所指向緩衝區的填滿未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容為未定義。  
  
 每當設定 APD、 ARD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時，驅動程式會檢查中的 SQL_DESC_TYPE 欄位的值包含其中一個有效的 ODBC C 資料類型或驅動程式特定資料類型，以及其他會影響的資料類型的所有欄位都一致。 IPD 的 SQL_DESC_DATA_PTR 欄位只能使用會提示一致性檢查。 具體來說，如果應用程式在設定 SQL_DESC_DATA_PTR 欄位 IPD 和更新版本呼叫**SQLGetDescField**此欄位中，它不一定會傳回設定一樣的值。 如需詳細資訊，請參閱 「 一致性檢查 」，在[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [全部]**  
 如果是 SQL_DATETIME 或 SQL_INTERVAL 的 SQL_DESC_TYPE 欄位時，此 SQLSMALLINT 記錄欄位就會包含特定的日期時間或間隔資料類型的子代碼。 這是針對 SQL 和 C 資料類型，則為 true。 程式碼所組成的資料類型名稱"CODE"（針對 datetime 類型），取代 「 類型 」 或 「 C_TYPE 」 或 「 程式碼 」 取代 「 間隔 」 或 「 C_INTERVAL"（針對間隔類型）。  
  
 如果 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 中的應用程式描述元會設定為 SQL_C_DEFAULT，描述項不是陳述式控制代碼相關聯的 SQL_DESC_DATETIME_INTERVAL_CODE 內容為未定義。  
  
 下表所列的日期時間資料類型時，可以設定此欄位。  
  
|日期時間類型|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP / SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 下表所列的間隔資料類型，可以設定此欄位。  
  
|間隔類型|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR / SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE / SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND / SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
QL_INTERVAL_HOUR_TO_MINUTE / SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE / SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND / SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
QL_INTERVAL_SECOND / SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 如需有關資料間隔，而此欄位的詳細資訊，請參閱[資料類型識別碼和描述元](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)。  
  
 **[All] SQL_DESC_DATETIME_INTERVAL_PRECISION**  
 此 SQLINTEGER 記錄欄位包含間隔開頭有效位數，如果 SQL_DESC_TYPE 欄位為 SQL_INTERVAL。 當 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為間隔資料類型時，此欄位設為預設間隔開頭有效位數。  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 此唯讀 SQLINTEGER 記錄欄位包含顯示資料行的資料所需的字元的數上限。  
  
 **SQL_DESC_FIXED_PREC_SCALE [實作描述元]**  
 此唯讀 SQLSMALLINT 記錄欄位設為 SQL_TRUE，如果資料行是精確數值資料行，且具有固定有效位數和非零值的小數位數或 SQL_FALSE 如果資料行不是確切的數值資料行具有固定有效位數和小數位數。  
  
 **SQL_DESC_INDICATOR_PTR [應用程式描述項]**  
 在 ARDs，這是 SQLLEN * 記錄欄位會指向指標變數。 如果資料行的值是 NULL，此變數會包含 SQL_NULL_DATA。 Apd，如這個指標變數來指定 NULL 的動態引數將設定為 SQL_NULL_DATA。 否則，變數會是零 （除非 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 中的值都是相同的指標）。  
  
 如果 ARD SQL_DESC_INDICATOR_PTR 欄位會是 null 指標，驅動程式無法傳回資料行是否為 NULL 的相關資訊。 如果資料行為 NULL 和 SQL_DESC_INDICATOR_PTR 為 null 指標，SQLSTATE 22002 （指標變數所需但未提供） 時，會傳回驅動程式會嘗試在呼叫之後填入緩衝區**SQLFetch**或**SQLFetchScroll**。 如果在呼叫**SQLFetch**或是**SQLFetchScroll**未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容為未定義。  
  
 SQL_DESC_INDICATOR_PTR 欄位會決定是否要設定 SQL_DESC_OCTET_LENGTH_PTR 所指的欄位。 如果資料行的資料值為 NULL，驅動程式會將指標變數設定為 SQL_NULL_DATA。 然後不設定 SQL_DESC_OCTET_LENGTH_PTR 所指的欄位。 如果 NULL 值就不會發生在擷取期間，SQL_DESC_INDICATOR_PTR 所指向緩衝區設定為零和 SQL_DESC_OCTET_LENGTH_PTR 所指向緩衝區設為資料的長度。  
  
 APD 中的 [SQL_DESC_INDICATOR_PTR] 欄位為 null 指標，如果應用程式無法使用此描述項記錄，來指定 NULL 引數。  
  
 這個欄位是*延後的欄位*： 它不會在其設定，但會在稍後驅動程式用來表示 null 屬性 （適用於 ARDs)，或決定 null 屬性 （Apd) 的時間。  
  
 **與 SQL_DESC_LABEL [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含資料行標籤或標題。 如果資料行沒有標籤，此變數會包含資料行名稱。 如果是未命名的資料行，而且沒有標籤，此變數包含空字串。  
  
 **SQL_DESC_LENGTH [全部]**  
 此 SQLULEN 記錄欄位會是最大頁數或實際長度字元字串中字元或二進位資料類型，以位元組為單位。 這是固定長度資料類型的最大長度或可變長度資料類型的實際長度。 其值一律不包括結束的字元字串的 null 終止字元。 類型為 SQL_TYPE_DATE、 SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP，或其中一個 SQL 間隔資料類型的值，此欄位會有以字元為單位的日期時間或間隔值代表的字元字串的長度。  
  
 此欄位中的值可能不同於 「 長度 」 做為 ODBC 2 中所定義的值 *.x*。 如需詳細資訊，請參閱 <<c0> [ 附錄 d： 資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含驅動程式會辨識為此資料類型的常值的前置詞的字元。 此變數包含空字串資料類型不適用的常值的前置詞。  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含驅動程式會辨識為此資料類型的常值後置詞的字元。 此變數包含空字串資料類型不適用的文字尾碼。  
  
 **SQL_DESC_LOCAL_TYPE_NAME [實作描述元]**  
 這個唯讀 SQLCHAR * 記錄欄位包含任何當地語系化 （原生語言） 的名稱可能不同於一般的資料型別名稱的資料類型。 如果沒有當地語系化的名稱，則會傳回空字串。 這個欄位是僅供顯示。  
  
 **與 SQL_DESC_NAME [實作描述元]**  
 此 SQLCHAR * 資料列描述項記錄欄位包含的資料行別名，如果它適用於。 如果不適用資料行別名，則會傳回資料行名稱。 在任一情況下，驅動程式會將 SQL_DESC_UNNAMED 欄位設定為 SQL_NAMED 時它會設定與 SQL_DESC_NAME 欄位。 如果沒有任何資料行名稱或資料行別名，驅動程式中與 SQL_DESC_NAME 欄位會傳回空字串，並將 SQL_DESC_UNNAMED 欄位設定為 sql_unnamed 時。  
  
 應用程式可以設定與 SQL_DESC_NAME 欄位 IPD 的參數名稱或別名，以依名稱指定預存程序參數。 (如需詳細資訊，請參閱 <<c0> [ 依名稱 （具名參數） 的繫結參數](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md)。)IRD 的與 SQL_DESC_NAME 欄位是唯讀的欄位;SQLSTATE HY091 如果應用程式嘗試將它設定，則會傳回 （無效的描述項欄位識別碼）。  
  
 在 Ipd，這個欄位是未定義的如果驅動程式不支援具名的參數。 如果驅動程式支援具名的參數，而且能夠描述參數，參數名稱會傳回此欄位中。  
  
 **SQL_DESC_NULLABLE [實作描述元]**  
 IRDs，在此唯讀 SQLSMALLINT 記錄欄位會是 SQL_NULLABLE，如果資料行可以有 NULL 值，SQL_NO_NULLS 如果資料行不具有 NULL 值或 SQL_NULLABLE_UNKNOWN，如果不知道資料行是否接受 NULL 值。 此欄位屬於結果集資料行，不是基底的資料行。  
  
 在 Ipd，這個欄位是一律設定為 SQL_NULLABLE 因為動態參數都可為 null，而且無法設定應用程式。  
  
 **[All] SQL_DESC_NUM_PREC_RADIX**  
 SQLINTEGER 當這個欄位包含值為 2 中的 SQL_DESC_TYPE 欄位的資料類型是近似的數值資料類型，因為 SQL_DESC_PRECISION 欄位包含的位元數。 當這個欄位包含值為 10 中的 SQL_DESC_TYPE 欄位的資料類型是精確數值資料類型，因為 SQL_DESC_PRECISION 欄位包含的小數位數。 此欄位設為 0 表示所有非數值資料類型。  
  
 **[所有] 的 SQL_DESC_OCTET_LENGTH**  
 這是 SQLLEN 記錄欄位包含的長度，以位元組為單位的字元字串或二進位資料類型。 固定長度的字元或二進位類型，這是以位元組為單位的實際長度。 可變長度的字元或二進位類型，這是以位元組為單位的最大長度。 這個值一律會排除實作描述項之 null 結束字元的空間，而且永遠會包含應用程式描述項之 null 結束字元的空間。 應用程式資料，此欄位會包含緩衝區的大小。 Apd，這個欄位被定義僅適用於輸出或輸入/輸出參數。  
  
 **SQL_DESC_OCTET_LENGTH_PTR [應用程式描述項]**  
 這是 SQLLEN * 記錄欄位，將包含的總長度以位元組為單位的動態引數 （參數描述項） 或 （適用於資料列描述項） 的繫結的資料行值的變數會指向。  
  
 APD 中，是會忽略這個值的字元字串和二進位檔; 以外的所有引數如果此欄位會指向 SQL_NTS，動態引數必須以 null 結束。 若要表示繫結的參數是資料在執行中參數，應用程式設定此欄位中適當的記錄 APD 中的變數，，請在執行階段，將會包含值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果. 如果有多個這類欄位，可以用來唯一識別參數的值設定 SQL_DESC_DATA_PTR，以協助判斷哪一個參數所要求的應用程式。  
  
 如果 ARD OCTET_LENGTH_PTR 欄位為 null 指標，驅動程式不會傳回資料行長度資訊。 APD 中的 SQL_DESC_OCTET_LENGTH_PTR 欄位為 null 指標，如果驅動程式會假設字元字串和二進位的值都是 null 結束。 （二進位值不得以 null 結尾的但應有的長度，以避免截斷）。  
  
 如果在呼叫**SQLFetch**或是**SQLFetchScroll** ，在此欄位所指向緩衝區的填滿未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，緩衝區的內容為未定義。 這個欄位是*延後的欄位*。 它不會在其設定，但在稍後由驅動程式用來判斷或表示八位元長度的資料的時間。  
  
 **SQL_DESC_PARAMETER_TYPE [Ipd]**  
 此 SQLSMALLINT 記錄欄位設定為 SQL_PARAM_INPUT 的輸入參數，輸入/輸出參數，輸出參數，針對輸入/輸出資料流處理的參數，SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_ SQL_PARAM_OUTPUT SQL_PARAM_INPUT_OUTPUTPARAM_OUTPUT_STREAM 做為輸出資料流處理參數。 根據預設，它會設定為 SQL_PARAM_INPUT。  
  
 IPD 中，為欄位設定為 SQL_PARAM_INPUT 預設如果 （SQL_ATTR_ENABLE_AUTO_IPD 陳述式屬性是 SQL_FALSE） 驅動程式不會自動填入 IPD。 應用程式應該不是輸入的參數的參數 IPD 中設定此欄位。  
  
 **SQL_DESC_PRECISION [全部]**  
 此 SQLSMALLINT 記錄欄位包含是精確數值類型，在 （二進位精確度） 的近似數值類型，則表示尾數的位元數或 SQL_TYPE_TIME SQL_TYPE 的小數秒數元件中的數字的數字的數字的數目_TIMESTAMP 或 SQL_INTERVAL_SECOND 資料型別。 這個欄位是未定義的所有其他資料類型。  
  
 此欄位中的值可能不同於 「 精確度 」 做為 ODBC 2 中所定義的值 *.x*。 如需詳細資訊，請參閱 <<c0> [ 附錄 d： 資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_ROWVER [實作描述元]**  
 這個 SQLSMALLINTrecord 欄位會指示是否修改資料行是自動和 dbms 的資料列更新 （例如，類型為"timestamp"SQL Server 中的資料行） 時。 此記錄欄位的值是設定為 SQL_TRUE，如果資料行是資料列版本設定資料行，以及 SQL_FALSE 否則。 此資料行屬性是類似於呼叫**SQLSpecialColumns** IdentifierType 的 SQL_ROWVER 來判斷是否會自動更新的資料行使用。  
  
 **[All] SQL_DESC_SCALE**  
 此 SQLSMALLINT 記錄欄位包含 decimal 與 numeric 資料類型的定義小數位數。 對於所有其他資料類型未定義的欄位。  
  
 此欄位中的值可能不同於 「 調整 」 ODBC 2 中所定義的值 *.x*。 如需詳細資訊，請參閱 <<c0> [ 附錄 d： 資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含基底資料表包含資料行的結構描述名稱。 如果資料行是運算式或資料行是否屬於檢視，傳回的值會是驅動程式相關。 如果資料來源不支援結構描述，或無法判斷結構描述名稱，此變數包含空字串。  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 這個唯讀 SQLSMALLINT 記錄欄位會設定為下列值之一：  
  
-   如果資料行不能在 SQL_PRED_NONE**其中**子句。 (這是 ODBC 2 SQL_UNSEARCHABLE 值相同 *.x*。)  
  
-   SQL_PRED_CHAR 如果資料行可以用於**何處**子句，但僅限於有**像**述詞。 (這是 ODBC 2 SQL_LIKE_ONLY 值相同 *.x*。)  
  
-   SQL_PRED_BASIC 如果資料行可以用於**何處**子句以外的所有比較運算子搭配**像**。 (這是 ODBC 2 SQL_EXCEPT_LIKE 值相同 *.x*。)  
  
-   如果資料行可以用於 SQL_PRED_SEARCHABLE**其中**搭配任何比較運算子的子句。  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 這個唯讀 SQLCHAR * 記錄欄位包含基底資料表包含此資料行的名稱。 如果資料行是運算式或資料行是否屬於檢視，傳回的值會是驅動程式相關。  
  
 **[所有] 的 SQL_DESC_TYPE**  
 此 SQLSMALLINT 記錄欄位指定的精簡 SQL 或 C 資料類型以外的日期時間和間隔資料類型的所有資料類型。 日期時間和間隔資料類型，此欄位會指定是 SQL_DATETIME 或 SQL_INTERVAL 的詳細資訊的資料類型。  
  
 此欄位包含如果是 SQL_DATETIME 或 SQL_INTERVAL，每當 SQL_DESC_DATETIME_INTERVAL_CODE 欄位必須包含精簡類型的適當子代碼。 Datetime 資料類型的 SQL_DESC_TYPE 包含 SQL_DATETIME，而 SQL_DESC_DATETIME_INTERVAL_CODE 欄位包含特定的日期時間資料型別的子代碼。 間隔資料類型的 SQL_DESC_TYPE 包含 SQL_INTERVAL 而 SQL_DESC_DATETIME_INTERVAL_CODE 欄位包含特定間隔資料類型的次要代碼。  
  
 中的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 欄位的值都相互依賴。 設定每次一個欄位，另也必須設定。 可以藉由呼叫設定 SQL_DESC_TYPE **SQLSetDescField**或是**SQLSetDescRec**。 可以藉由呼叫設定 SQL_DESC_CONCISE_TYPE **SQLBindCol**或是**SQLBindParameter**，或**SQLSetDescField**。  
  
 如果 SQL_DESC_TYPE 設定為精簡的資料類型的間隔或 datetime 資料類型以外，SQL_DESC_CONCISE_TYPE 欄位設定為相同的值和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為 0。  
  
 如果 SQL_DESC_TYPE 設定的詳細資訊的日期時間或間隔資料類型 （如果是 SQL_DATETIME 或 SQL_INTERVAL） 為 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為適當的子代碼，SQL_DESC_CONCISE 類型 欄位設為相對應的精簡型別。 嘗試將 SQL_DESC_TYPE 設定為其中一種簡潔的日期時間或是間隔類型，則會傳回 SQLSTATE HY021 （不一致的描述元資訊）。  
  
 當呼叫所設定的 SQL_DESC_TYPE 欄位**SQLBindCol**， **SQLBindParameter**，或**SQLSetDescField**，下列欄位會設定為下列的預設值，下表所示。 相同的資料錄的其餘欄位的值是未定義。  
  
|SQL_DESC_TYPE 值|隱含地設定其他欄位|  
|------------------------------|---------------------------------|  
|SQL_CHAR、 SQL_VARCHAR、 SQL_C_CHAR SQL_C_VARCHAR|SQL_DESC_LENGTH 設為 1。 SQL_DESC_PRECISION 設為 0。|  
|SQL_DATETIME|SQL_DESC_DATETIME_INTERVAL_CODE 設 SQL_CODE_DATE 或 SQL_CODE_TIME，SQL_DESC_PRECISION 設為 0。 當它設定為 SQL_DESC_TIMESTAMP 時，SQL_DESC_PRECISION 設為 6。|  
|SQL_DECIMAL，SQL_NUMERIC，SQL_C_NUMERIC|SQL_DESC_SCALE 設為 0。 SQL_DESC_PRECISION 會設定為個別的資料類型的實作定義的有效位數。<br /><br /> 請參閱[SQL 到 c： 數值](../../../odbc/reference/appendixes/sql-to-c-numeric.md)如需有關如何以手動方式將繫結 SQL_C_NUMERIC 值資訊。|  
|SQL_FLOAT、 SQL_C_FLOAT|SQL_DESC_PRECISION SQL_FLOAT 是設定為實作定義的預設有效位數。|  
|SQL_INTERVAL|當 SQL_DESC_DATETIME_INTERVAL_CODE 設定間隔資料類型時，會將 SQL_DESC_DATETIME_INTERVAL_PRECISION 設定為 2 （預設間隔開頭有效位數）。 時的間隔秒數元件，則會將 SQL_DESC_PRECISION 設定為 6 （預設間隔秒數有效位數）。|  
  
 當應用程式呼叫**SQLSetDescField**來設定欄位的描述元，而不是呼叫**SQLSetDescRec**，應用程式必須先宣告的資料類型。 載入時，會隱含地設定，如上表所示的其他欄位。 值的隱含集是否有任何無法接受，應用程式接著可以呼叫**SQLSetDescField**或是**SQLSetDescRec**明確地設定無法接受的值。  
  
 **SQL_DESC_TYPE_NAME [實作描述元]**  
 這個唯讀 SQLCHAR * 記錄欄位包含資料來源而定的型別名稱 （例如，"CHAR"、"VARCHAR"，等等）。 如果資料類型名稱未知時，此變數包含空字串。  
  
 **將 SQL_DESC_UNNAMED [實作描述元]**  
 此 SQLSMALLINT 記錄中欄位的資料列描述項是由 SQL_NAMED 或 sql_unnamed 時驅動程式時設定其設定與 SQL_DESC_NAME 欄位。 如果與 SQL_DESC_NAME 欄位包含資料行別名或不適用資料行別名，驅動程式將 SQL_DESC_UNNAMED 將欄位設定為 SQL_NAMED。 如果應用程式會將 IPD 與 SQL_DESC_NAME 欄位設定的參數名稱或別名，驅動程式會設定為 SQL_NAMED IPD SQL_DESC_UNNAMED 欄位。 如果沒有任何資料行名稱或資料行別名，則驅動程式會將 SQL_DESC_UNNAMED 欄位設 sql_unnamed 時。  
  
 應用程式可以設定 IPD SQL_DESC_UNNAMED 欄位為 sql_unnamed 時。 驅動程式會傳回 SQLSTATE HY091 （無效的描述項欄位識別碼），如果應用程式嘗試 IPD SQL_DESC_UNNAMED 欄位設為 SQL_NAMED。 IRD SQL_DESC_UNNAMED 欄位是唯讀的;SQLSTATE HY091 如果應用程式嘗試將它設定，則會傳回 （無效的描述項欄位識別碼）。  
  
 **SQL_DESC_UNSIGNED [實作描述元]**  
 如果資料行類型簽章時，這個唯讀 SQLSMALLINT 記錄欄位設為 SQL_TRUE，如果資料行類型是不帶正負號或非數值或 SQL_FALSE。  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 這個唯讀 SQLSMALLINT 記錄欄位會設定為下列值之一：  
  
-   如果結果集資料行的 SQL_ATTR_READ_ONLY 處於唯讀狀態。  
  
-   如果結果集資料行的 SQL_ATTR_WRITE 是讀寫。  
  
-   SQL_ATTR_READWRITE_UNKNOWN 如果不知道是否在結果集資料行可更新。  
  
 SQL_DESC_UPDATABLE 描述結果集中資料行中，不是基底資料表中的資料行的可更新性。 此結果集資料行所依據的基底資料表中的資料行的可更新性可能會不同於此欄位中的值。 資料行是否可更新可以根據資料類型、 使用者權限，以及結果集本身的定義。 如果是不明確的資料行是否可更新，應該會傳回 SQL_ATTR_READWRITE_UNKNOWN。  
  
## <a name="consistency-checks"></a>一致性檢查  
 一致性檢查是由驅動程式自動執行應用程式傳遞值 ARD、 APD 或 IPD 的 SQL_DESC_DATA_PTR 欄位時。 任何欄位是否具有其他欄位中，不一致**SQLSetDescField**會傳回 SQLSTATE HY021 （不一致的描述元資訊）。 如需詳細資訊，請參閱 「 一致性檢查 」，在[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|資料行繫結|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|將參數繫結|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取得描述項欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得多個描述項欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定多個描述項欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)
