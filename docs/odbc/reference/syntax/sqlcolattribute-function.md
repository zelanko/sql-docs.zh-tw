---
title: "SQLColAttribute 函數 |Microsoft 文件"
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
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4248444c3b8908266a587ce3cb208a1d492fe1d9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLColAttribute**結果集中傳回的資料行的描述項資訊。 描述項資訊是以字元字串，描述元而定的值或整數值傳回。  
  
> [!NOTE]  
>  如需有關哪些驅動程式管理員將此函式可對應時 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式，請參閱[對應取代函式的應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *ColumnNumber*  
 [輸入]在 IRD 欄位值是要擷取的記錄數目。 這個引數會對應至結果的資料，以遞增的資料行順序，從 1 開始依序排序的資料行數目。 資料行可以依照任何順序。  
  
 資料行 0 可指定這個引數，但 SQL_DESC_TYPE 和 SQL_DESC_OCTET_LENGTH 以外的所有值會都傳回未定義的值。  
  
 *FieldIdentifier*  
 [輸入]描述項控制代碼。 這個控制代碼會定義在 IRD 中的哪一個欄位應該查詢 （例如 SQL_COLUMN_TABLE_NAME）。  
  
 *CharacterAttributePtr*  
 [輸出]這是要傳回的值中的緩衝區指標*FieldIdentifier*欄位*ColumnNumber* IRD，如果欄位是字元字串的資料列。 否則，此欄位是未使用。  
  
 如果*CharacterAttributePtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回緩衝區中所指*CharacterAttributePtr*。  
  
 *Columnsize*  
 [輸入]如果*FieldIdentifier*是 ODBC 定義的欄位和*CharacterAttributePtr*指向的字元字串或二進位的緩衝區，這個引數應該是長度\* *CharacterAttributePtr*。 如果*FieldIdentifier*是 ODBC 定義的欄位和\* *CharacterAttribute*Ptr 是一個整數，這個欄位會被忽略。 如果 *\*CharacterAttributePtr*是 Unicode 字串 (當呼叫**SQLColAttributeW**)、 *Columnsize*引數必須是偶數。 如果*FieldIdentifier*是驅動程式定義的欄位，應用程式設定指出欄位驅動程式管理員性質*Columnsize*引數。 *Columnsize*可以是下列值：  
  
-   如果*CharacterAttributePtr*是指標的指標， *Columnsize*應該有 SQL_IS_POINTER 的值。  
  
-   如果*CharacterAttributePtr*是字元字串的指標*Columnsize*緩衝區的長度。  
  
-   如果*CharacterAttributePtr* SQL_LEN_BINARY_ATTR 的結果是二進位的緩衝區，應用程式位置的指標 (*長度*) 中的巨集*Columnsize*。 這樣做會放在負值*Columnsize*。  
  
-   如果*CharacterAttributePtr*是固定長度的資料類型的指標*Columnsize*必須是下列其中之一： SQL_IS_INTEGER、 SQL_IS_UNINTEGER、 SQL_SMALLINT 或 SQLUSMALLINT。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不含字元資料的 null 結束位元組） 的緩衝區指標可用來傳回中 **CharacterAttributePtr*。  
  
 若是字元資料，可用來傳回的位元組數目是否大於或等於*Columnsize*中的描述元資訊\* *CharacterAttributePtr*會被截斷成*Columnsize* null 結束字元的長度減而且是以 null 結束的驅動程式。  
  
 對於所有其他類型的資料，值*Columnsize*會忽略和驅動程式會假設大小 **CharacterAttributePtr*為 32 位元。  
  
 *NumericAttributePtr*  
 [輸出]這是要傳回的值中的整數緩衝區指標*FieldIdentifier*欄位*ColumnNumber*如果欄位是數值的描述元類型，例如 SQL_DESC_COLUMN_LENGTH IRD 的資料列。 否則，此欄位是未使用。 請注意，有些驅動程式可能只會寫入較低的 32 位元或 16 位元的緩衝區並保留不變的更高序位位元。 因此，應用程式應該呼叫此函式之前初始化為 0 的值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColAttribute**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**與*HandleType*利用 SQL_HANDLE_STMT 的和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLColAttribute** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|緩衝區\* *CharacterAttributePtr*仍不夠大，無法傳回整個字串值，所以已截斷字串值。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07005|無法準備陳述式*資料指標規格*|與相關聯的陳述式*StatementHandle*未傳回結果集和*FieldIdentifier*未 SQL_DESC_COUNT。 沒有資料行來描述。|  
|07009|無效的描述元索引|(DM) 指定的值*ColumnNumber*等於 0，且驗證了 SQL_UB_OFF SQL_ATTR_USE_BOOKMARKS 陳述式屬性。<br /><br /> 指定的引數的值*ColumnNumber*大於結果集中的資料行數目。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagField**結構描述的錯誤，並且其原因的診斷資料。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 仍在 SQLColAttribute 呼叫時執行此 aynchronous 函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> (DM) 函式呼叫之前呼叫**SQLPrepare**， **SQLExecDirect**，或為目錄函數*StatementHandle*。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*CharacterAttributePtr*是字元字串，並*Columnsize*小於 0，但不是等於 SQL_NTS。|  
|HY091|無效的描述項欄位識別碼|指定的引數的值*FieldIdentifier*未定義值的其中一個，且不實作定義的值。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|不支援的驅動程式|指定的引數的值*FieldIdentifier*驅動程式不支援。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
 之後呼叫**SQLPrepare**之前**SQLExecute**， **SQLColAttribute**可以傳回任何可傳回的 SQLSTATE **SQLPrepare**或**SQLExecute**，端視資料來源時評估相關聯的 SQL 陳述式*StatementHandle*。  
  
 基於效能考量，應用程式不應該呼叫**SQLColAttribute**之前執行的陳述式。  
  
## <a name="comments"></a>註解  
 如需有關應用程式如何使用所傳回的資訊資訊**SQLColAttribute**，請參閱[結果集的中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLColAttribute**傳回資訊，請在\* *NumericAttributePtr*或\* *CharacterAttributePtr*。 整數資訊傳回\* *NumericAttributePtr* SQLLEN 值; 中傳回資訊的其他所有格式\* *CharacterAttributePtr*。 當資訊傳回\* *NumericAttributePtr*，驅動程式會忽略*CharacterAttributePtr*， *Columnsize*，和*StringLengthPtr*。 當資訊傳回\* *CharacterAttributePtr*，驅動程式會忽略*NumericAttributePtr*。  
  
 **SQLColAttribute**從 IRD 的描述項欄位會傳回值。 函式被呼叫陳述式控制代碼，而不是描述項控制代碼。 所傳回的值**SQLColAttribute**如*FieldIdentifier*本章節稍後所列的值也可以藉由呼叫擷取**SQLGetDescField**與適當的 IRD 控制代碼。  
  
 目前已定義的描述項欄位，它們所導入，而它們會傳回資訊的引數稍後顯示在本章節內容; ODBC 的版本更多的描述元類型可由驅動程式來利用不同的資料來源的定義。  
  
 ODBC 3。*x*驅動程式必須傳回每個描述項欄位的值。 如果描述項欄位不會套用到驅動程式或資料來源，且除非另有指明，驅動程式會傳回在 0 \* *StringLengthPtr*或空字串中的 **CharacterAttributePtr*。  
  
## <a name="backward-compatibility"></a>回溯相容性  
 ODBC 3。*x*函式**SQLColAttribute**取代已被取代的 ODBC 2。*x*函式**SQLColAttributes**。 當對應**SQLColAttributes**至**SQLColAttribute** (當 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式)，或對應**SQLColAttribute**至**SQLColAttributes** (當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式)，驅動程式管理員可以將值傳遞*FieldIdentifier* ，透過將其對應至新的值，或將傳回錯誤，如下所示：  
  
> [!NOTE]  
>  使用中的前置詞*FieldIdentifier* ODBC 3 中的值。*x*從該使用中的 ODBC 2 已變更。*x*。 新的前置詞為"SQL_DESC";舊的前置詞為"SQL_COLUMN"。  
  
-   如果**#define** ODBC 2 的值。*x* *FieldIdentifier*相同**#define** ODBC 3 的值。*x* *FieldIdentifier*，函式呼叫中的值就只會傳遞。  
  
-   **#Define** ODBC 2 的值。*x* *FieldIdentifiers* SQL_COLUMN_LENGTH、 SQL_COLUMN_PRECISION 和 SQL_COLUMN_SCALE 會與不同**#define** ODBC 3 的值。*x* *FieldIdentifiers* SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_LENGTH。 ODBC 2。*x*驅動程式只需要支援 ODBC 2。*x*值。 ODBC 3。*x*驅動程式必須支援 「 SQL_COLUMN"和"SQL_DESC"值的這三個*FieldIdentifiers*。 因為有效位數、 小數位數和長度會定義以不同的方式在 ODBC 3，這些值會不同。*x*比 ODBC 2。*x*。 如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
-   如果**#define** ODBC 2 的值。*x* *FieldIdentifier*不同**#define** ODBC 3 的值。*x* *FieldIdentifier*，做為與計數，名稱，並可為 NULL 值，函式呼叫中的值會對應到對應的值。 例如，SQL_COLUMN_COUNT 會對應至 SQL_DESC_COUNT，和 SQL_DESC_COUNT 對應到 SQL_COLUMN_COUNT，根據對應的方向。  
  
-   如果*FieldIdentifier*是在 ODBC 3 的新值。*x*，如這沒有對應的值在 ODBC 2。*x*，它將不會對應時 ODBC 3。*x*應用程式所使用的是它的呼叫中**SQLColAttribute** ODBC 2。*x*驅動程式，並呼叫會傳回 SQLSTATE HY091 （無效的描述項欄位識別碼）。  
  
 下表列出所傳回的描述元類型**SQLColAttribute**。 型別*NumericAttributePtr*值是**SQLLEN \*** 。  
  
|*FieldIdentifier*|資訊<br /><br /> 傳回|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 的資料行是否自動遞增資料行。<br /><br /> 如果資料行不是自動遞增資料行，或不是數值，SQL_FALSE。<br /><br /> 此欄位僅適用於數值資料類型資料行。 應用程式可以將值插入含有自動遞增資料行的資料列，但是通常無法更新資料行中的值。<br /><br /> 插入至 autoincrement 資料行中進行時，唯一的值被插入資料行在插入時。 未定義時，遞增，但資料來源專用。 應用程式不應該假設任何特定值的 autoincrement 資料行開始在任何特定點或增量。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|基底的資料行名稱的結果集資料行。 如果基底的資料行名稱不存在 （如同在資料行是運算式的案例），此變數包含空字串。<br /><br /> 此資訊會從 IRD 是唯讀欄位的 SQL_DESC_BASE_COLUMN_NAME 記錄欄位傳回。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|包含資料行的基底資料表的名稱。 如果基底資料表名稱不能定義，或不適用，此變數包含空字串。<br /><br /> 此資訊會從 IRD 是唯讀欄位的 SQL_DESC_BASE_TABLE_NAME 記錄欄位傳回。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|如果資料行來處理，以區分大小寫的定序與比較，SQL_TRUE。<br /><br /> 如果資料行也不會處理為區分大小寫定序和比較，或是非字元，SQL_FALSE。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含資料行的資料表的目錄。 傳回的值是由實作定義的資料行是運算式或資料行是檢視的一部分。 如果資料來源不支援目錄，或無法判斷目錄名稱，則會傳回空字串。 此 VARCHAR 記錄欄位不是限制為 128 個字元。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|精簡的資料類型。<br /><br /> 日期時間和間隔資料類型，這個欄位會傳回精確的資料類型。例如，SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR。 (如需詳細資訊，請參閱[資料類型識別碼和描述元](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)附錄 d： 資料型別中。)<br /><br /> 此資訊會從 IRD 的 SQL_DESC_CONCISE_TYPE 記錄欄位傳回。|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|在結果集中可用的資料行數目。 如果結果集中沒有資料行，這會傳回 0。 中的值*ColumnNumber*會忽略引數。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_COUNT 標頭欄位中傳回。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|若要顯示的資料行的資料所需的字元數目上限。 如需顯示大小的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|如果資料行具有固定有效位數和非零，小數位數的資料來源專用的 SQL_TRUE。<br /><br /> 如果資料行並沒有固定有效位數和非零，小數位數的資料來源專用的 SQL_FALSE。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|資料行標籤或標題。 比方說，EmpName 的資料行可能會標示為員工名稱，或可能會加上別名。<br /><br /> 如果資料行沒有標籤，會傳回資料行名稱。 如果未標記，資料行，且未命名的則會傳回空字串。|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|可能是一個數字值類型字元字串或二進位資料的最大或實際的字元長度。 它是固定長度的資料類型的最大字元長度或可變長度資料類型的實際字元長度。 其值永遠不包括結束的字元字串的 null 結束位元組。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_LENGTH 記錄欄位傳回。<br /><br /> 如需長度的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|這個 varchar （128） 記錄欄位包含驅動程式會辨識為此資料類型的常值的前置詞的字元。 此欄位包含不適用常值前置詞的資料類型為空字串。 如需詳細資訊，請參閱[常值前置詞和尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|這個 varchar （128） 記錄欄位包含驅動程式會辨識為此資料類型的常值後置字元。 此欄位會包含空字串資料類型不適用的文字尾碼。 如需詳細資訊，請參閱[常值前置詞和尾碼](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|此 varchar （128） 記錄欄位包含任何當地語系化 （原生語言） 的名稱可能不同於一般的資料型別名稱的資料類型。 如果沒有當地語系化的名稱，則會傳回空字串。 這個欄位是僅供顯示。 字串的字元集是地區設定相關，通常在伺服器的預設字元集。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|如果它適用於資料行別名。 如果不適用資料行別名，則會傳回資料行名稱。 在任一情況下，SQL_DESC_UNNAMED 設 SQL_NAMED。 如果沒有任何資料行名稱或資料行別名，則傳回空的字串，且 SQL_DESC_UNNAMED 設 sql_unnamed 時。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_NAME 記錄欄位傳回。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ 可為 NULL 的資料行可以有 NULL 值; 如果如果資料行不具有 NULL 值;，SQL_NO_NULLS或 SQL_NULLABLE_UNKNOWN 如果不知道資料行是否接受 NULL 值。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_NULLABLE 記錄欄位傳回。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|如果 SQL_DESC_TYPE 欄位中的資料類型是近似數值資料類型，此 SQLINTEGER 欄位會包含值為 2，因為 SQL_DESC_PRECISION 欄位包含的位元數。 如果 SQL_DESC_TYPE 欄位中的資料類型是精確數值資料類型，此欄位會包含值為 10，因為 SQL_DESC_PRECISION 欄位包含的小數位數。 此欄位設定為 0，所有非數值資料類型。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|字元字串或二進位資料類型的長度，以位元組為單位。 固定長度的字元或二進位類型，這是以位元組為單位的實際長度。 可變長度的字元或二進位類型，這是以位元組為單位的最大長度。 此値不包含 null 結束字元。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_OCTET_LENGTH 記錄欄位傳回。<br /><br /> 如需長度的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料型別中。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|值的數值表示適用的有效位數的數值資料類型。 對於資料型別 SQL_TYPE_TIME SQL_TYPE_TIMESTAMP，而且代表時間間隔，其值的所有間隔資料類型的小數秒數元件適用的有效位數。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_PRECISION 記錄欄位傳回。|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|適用於數值資料類型小數位數值。 DECIMAL 和 NUMERIC 資料類型，這是已定義的小數位數。 它是未定義的所有其他資料類型。<br /><br /> 此資訊會從 IRD 的小數位數記錄欄位傳回。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含資料行的資料表結構描述。 傳回的值是由實作定義的資料行是運算式或資料行是檢視的一部分。 如果資料來源不支援結構描述，或無法判斷結構描述名稱，則會傳回空字串。 此 VARCHAR 記錄欄位不是限制為 128 個字元。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|如果資料行不能在 WHERE 子句，SQL_PRED_NONE。 （這是 ODBC 2 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> 如果資料行可以用於 WHERE 子句中，但是只能搭配 LIKE 述詞，SQL_PRED_CHAR。 （這是 ODBC 2 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> 如果資料行可以用於 WHERE 子句類似以外的所有比較運算子與，SQL_PRED_BASIC。 （這是 ODBC 2 SQL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果資料行可以用於 WHERE 子句搭配任何比較運算子，SQL_PRED_SEARCHABLE。<br /><br /> 資料行的輸入 SQL_LONGVARCHAR 及 SQL_LONGVARBINARY 通常傳回 SQL_PRED_CHAR。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含資料行之資料表的名稱。 傳回的值是由實作定義的資料行是運算式或資料行是檢視的一部分。<br /><br /> 如果無法判別資料表名稱，則會傳回空字串。|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|數值，指定 SQL 資料類型。<br /><br /> 當*ColumnNumber*等於 SQL_BINARY 傳回可變長度的書籤為 0，而且 SQL_INTEGER 會傳回固定長度的書籤。<br /><br /> 日期時間和間隔資料類型，這個欄位會傳回的詳細資訊的資料類型： 如果是 SQL_DATETIME 或 SQL_INTERVAL。 (如需詳細資訊，請參閱[資料類型識別碼和描述元](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)附錄 d： 資料型別中。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_TYPE 記錄欄位傳回。 **注意：**才能對 ODBC 2。*x*驅動程式，請改用 SQL_DESC_CONCISE_TYPE。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|資料來源而定的資料型別名稱。例如，"CHAR"、"VARCHAR"、"MONEY"、"長 VARBINARY"或者 「 CHAR （） FOR BIT DATA 中的 」。<br /><br /> 如果此類型為 unknown，則會傳回空字串。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED 或 sql_unnamed 時。 如果 SQL_DESC_NAME 欄位 IRD 的包含資料行別名或資料行名稱，則會傳回 SQL_NAMED。 如果沒有任何資料行名稱或資料行別名，則會傳回 sql_unnamed 時。<br /><br /> 此資訊會從 IRD 的 SQL_DESC_UNNAMED 記錄欄位傳回。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 如果資料行是不帶正負號 （或不是數字）。<br /><br /> 如果資料行已簽署，SQL_FALSE。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|資料行會描述所定義的常數的值：<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE 描述結果集的資料行，不是基底資料表中的資料行的可更新性。 基底結果集資料行所依據的資料行的可更新性可能會與此欄位中的值不同。 資料行是否可更新可以根據的資料類型、 使用者權限，以及結果集本身的定義。 如果是不明確的資料行是否可更新，則應該傳回 SQL_ATTR_READWRITE_UNKNOWN。|  
  
 **SQLColAttribute**是可延伸的替代**SQLDescribeCol**。 **SQLDescribeCol**傳回一組固定的 ANSI 89 SQL 為基礎的描述項資訊。 **SQLColAttribute**可讓您更詳盡的 ANSI SQL 92 和 DBMS 廠商延伸模組中可用的描述元資訊的存取。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集內的資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>範例  
 下列範例程式碼不會釋放控制代碼和連線。 請參閱[SQLFreeHandle 函數](../../../odbc/reference/syntax/sqlfreehandle-function.md)，[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)，和[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)釋放控制代碼和陳述式的程式碼範例。  
  
```  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;  
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   retCode = SQLNumResultCols(hstmt, &numColumn);  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)

