---
title: SQLColAttribute 函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca10614062a495de2c8f0ee80d7bbd5c0e675ad4
ms.sourcegitcommit: 603d5ef9b45c2f111d36d11864dc032917e4a321
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/08/2019
ms.locfileid: "65449753"
---
# <a name="sqlcolattribute-function"></a>SQLColAttribute 函數
**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLColAttribute**結果集中傳回的資料行的描述項資訊。 描述項資訊會傳回字元字串，描述元相依值或整數值。  
  
> [!NOTE]  
>  如需哪些驅動程式管理員的詳細資訊時 ODBC 3 會對應到此函式。*x*應用程式正在使用的 ODBC 2。*x*驅動程式，請參閱[對應取代函式應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
 [輸入]在 IRD 欄位值是要擷取的記錄數目。 這個引數會對應至結果的資料，以增加資料行順序，從 1 開始循序排序資料行數目。 資料行可以依照任何順序。  
  
 這個引數，可以指定資料行 0 但 SQL_DESC_TYPE 和 SQL_DESC_OCTET_LENGTH 以外的所有值會都傳回未定義的值。  
  
 *FieldIdentifier*  
 [輸入]描述項控制代碼。 這個控制代碼會定義在 IRD 欄位應該查詢 （例如 SQL_COLUMN_TABLE_NAME）。  
  
 *CharacterAttributePtr*  
 [輸出]在其中傳回的值中的緩衝區指標*FieldIdentifier*欄位*ColumnNumber* IRD，如果欄位為字元字串的資料列。 否則，此欄位是未使用。  
  
 如果*CharacterAttributePtr*為 NULL，就*StringLengthPtr*仍會傳回的總位元組數 （不含字元資料之 null 結束字元） 可用來傳回緩衝區中指向*CharacterAttributePtr*。  
  
 *BufferLength*  
 [輸入]如果*FieldIdentifier*是 ODBC 定義欄位並*CharacterAttributePtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *CharacterAttributePtr*。 如果*FieldIdentifier*是 ODBC 定義欄位並\* *CharacterAttribute*Ptr 是一個整數，這個欄位會被忽略。 如果 *\*CharacterAttributePtr*是 Unicode 字串 (呼叫時**SQLColAttributeW**)，則*Columnsize*引數必須是偶數。 如果*FieldIdentifier*驅動程式定義的欄位，應用程式設定指出欄位給驅動程式管理員性質*Columnsize*引數。 *BufferLength*可以有下列值：  
  
-   如果*CharacterAttributePtr*是指標的指標*Columnsize*應有 SQL_IS_POINTER 的值。  
  
-   如果*CharacterAttributePtr*是字元字串的指標*Columnsize*是緩衝區的長度。  
  
-   如果*CharacterAttributePtr* SQL_LEN_BINARY_ATTR 的結果是二進位緩衝區中，應用程式位置的指標 (*長度*) 中的巨集*Columnsize*。 這會放在負值*Columnsize*。  
  
-   如果*CharacterAttributePtr*是固定長度資料類型的指標*Columnsize*必須是下列其中之一：SQL_IS_INTEGER、 SQL_IS_UNINTEGER、 SQL_SMALLINT，還是 SQLUSMALLINT。  
  
 *StringLengthPtr*  
 [輸出]在其中傳回的總位元組數 （不含字元資料的 null 終止位元組） 的緩衝區指標可用來傳回中 **CharacterAttributePtr*。  
  
 若是字元資料，可用來傳回的位元組數目是否大於或等於*Columnsize*中的描述元資訊\* *CharacterAttributePtr*會被截斷成*BufferLength*減去 null 結束字元的長度，是以 null 終止的驅動程式。  
  
 對於所有其他類型的資料，值*Columnsize*會略過驅動程式會假設的大小和 **CharacterAttributePtr*為 32 位元。  
  
 *NumericAttributePtr*  
 [輸出]中要傳回的值，整數的緩衝區指標*FieldIdentifier*欄位*ColumnNumber*如果欄位是數值的描述項類型，例如 SQL_DESC_COLUMN_LENGTH IRD 的資料列。 否則，此欄位是未使用。 請注意，有些驅動程式可能只會寫入較低的 32 位元或 16 位元的緩衝區並保留不變的較高順序位元。 因此，應用程式應該呼叫此函式之前初始化為 0 的值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColAttribute**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，藉由呼叫可取得相關聯的 SQLSTATE 值**SQLGetDiagRec**使用*HandleType*利用 SQL_HANDLE_STMT 的和 a*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLColAttribute** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|緩衝區\* *CharacterAttributePtr*仍不夠大，無法傳回整個字串值，所以已截斷字串值。 中會傳回未截斷的字串值的長度 **StringLengthPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07005|無法準備陳述式*資料指標規格*|與相關聯的陳述式*StatementHandle*未傳回結果集並*FieldIdentifier*未 SQL_DESC_COUNT。 沒有資料行來描述。|  
|07009|描述項索引無效|(DM) 指定的值*ColumnNumber*等於 0，因而 SQL_ATTR_USE_BOOKMARKS 陳述式屬性 SQL_UB_OFF。<br /><br /> 指定的引數的值*ColumnNumber*大於結果集中的資料行數目。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagField**的診斷資料從結構描述的錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 SQLColAttribute 呼叫時，仍執行此 aynchronous 函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 在呼叫之前呼叫的函式**SQLPrepare**， **SQLExecDirect**，或目錄的函式*StatementHandle*。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM)  *\*CharacterAttributePtr*是字元字串，以及*Columnsize*小於 0，但不是等於 SQL_NTS。|  
|HY091|無效的描述項欄位識別碼|指定的引數的值*FieldIdentifier*不是其中一個已定義的值，而並沒有實作定義的值。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|不支援的驅動程式|指定的引數的值*FieldIdentifier*驅動程式不支援。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
 之後呼叫**SQLPrepare**以及之前**SQLExecute**， **SQLColAttribute**可以傳回任何可傳回的 SQLSTATE **SQLPrepare**或是**SQLExecute**，這取決於資料來源時評估相關聯的 SQL 陳述式*StatementHandle*。  
  
 基於效能考量，應用程式不應該呼叫**SQLColAttribute**之前執行的陳述式。  
  
## <a name="comments"></a>註解  
 如需應用程式如何使用傳回的資訊**SQLColAttribute**，請參閱[結果集的中繼資料](../../../odbc/reference/develop-app/result-set-metadata.md)。  
  
 **SQLColAttribute**傳回的資訊，請在\* *NumericAttributePtr*或在\* *CharacterAttributePtr*。 整數資訊都會傳入\* *NumericAttributePtr*視為 SQLLEN 值; 中傳回的資訊的其他所有格式\* *CharacterAttributePtr*。 中傳回資訊時\* *NumericAttributePtr*，此驅動程式會忽略*CharacterAttributePtr*， *Columnsize*，和*StringLengthPtr*。 在傳回的資訊時\* *CharacterAttributePtr*，此驅動程式會忽略*NumericAttributePtr*。  
  
 **SQLColAttribute**會從 IRD 的描述項欄位的傳回值。 函式會呼叫的陳述式控制代碼，而不是描述項控制代碼。 所傳回的值**SQLColAttribute** for *FieldIdentifier*本節稍後所列的值也可以藉由呼叫來擷取**SQLGetDescField**與適當的 IRD 控制代碼。  
  
 目前定義的描述項欄位引進，而它們會傳回資訊的引數稍後顯示在這一節; 的 ODBC 的版本更多的描述元類型可由驅動程式，以利用不同的資料來源定義。  
  
 ODBC 3。*x*驅動程式必須傳回每個描述項欄位的值。 如果描述項欄位不會套用到驅動程式或資料來源，而且除非另有指明，驅動程式會傳回在 0 \* *StringLengthPtr*中的空字串或 **CharacterAttributePtr*。  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 ODBC 3。*x*函式**SQLColAttribute**取代已被取代的 ODBC 2。*x*函式**SQLColAttributes**。 當對應**SQLColAttributes**要**SQLColAttribute** (當 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式)，或對應**SQLColAttribute**要**SQLColAttributes** (當 ODBC 3。*x*應用程式正在使用的 ODBC 2。*x*驅動程式)，驅動程式管理員可以將值傳遞*FieldIdentifier*透過，將它對應至新的值，或發生錯誤時，會傳回，如下所示：  
  
> [!NOTE]  
>  使用中的前置詞*FieldIdentifier* ODBC 3 中的值。*x*已從該使用中的 ODBC 2 變更。*x*。 新的前置詞是"SQL_DESC";舊的前置詞是"SQL_COLUMN 」。  
  
-   如果 **#define**值為 ODBC 2。*x* *FieldIdentifier*等同於 **#define** ODBC 3 的值。*x* *FieldIdentifier*，只傳遞函式呼叫中的值。  
  
-   **#Define** ODBC 2 的值。*x* *FieldIdentifiers* SQL_COLUMN_LENGTH、 SQL_COLUMN_PRECISION 和 SQL_COLUMN_SCALE 互異 **#define** ODBC 3 的值。*x* *FieldIdentifiers* SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_LENGTH。 ODBC 2。*x*驅動程式只需要支援 ODBC 2。*x*值。 ODBC 3。*x*驅動程式必須支援 「 SQL_COLUMN"和"SQL_DESC"值的這三種*FieldIdentifiers*。 因為有效位數、 小數位數和長度會定義以不同的方式在 ODBC 3，這些值會不同。*x*比起在 ODBC 2。*x*。 如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
-   如果 **#define**值為 ODBC 2。*x* *FieldIdentifier*不同 **#define** ODBC 3 的值。*x* *FieldIdentifier*，做為與計數，也就是名稱，並可為 NULL 的值，這個函式呼叫中的值會對應到對應的值。 比方說，SQL_COLUMN_COUNT 會對應至 SQL_DESC_COUNT，而且 SQL_DESC_COUNT 對應至 SQL_COLUMN_COUNT，根據對應的方向。  
  
-   如果*FieldIdentifier*是在 ODBC 3 的新值。*x*，如這有 ODBC 2 中已沒有對應的值。*x*，它將不會對應時 ODBC 3。*x*應用程式所使用的是它在呼叫**SQLColAttribute** ODBC 2。*x*驅動程式，並呼叫會傳回 SQLSTATE HY091 （無效的描述項欄位識別碼）。  
  
 下表列出所傳回的描述元類型**SQLColAttribute**。 型別*NumericAttributePtr*的值是**SQLLEN \*** 。  
  
|*FieldIdentifier*|[資訊]<br /><br /> 傳回|描述|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 資料行是否自動遞增資料行。<br /><br /> 如果資料行不是自動遞增資料行，或不是數字，SQL_FALSE。<br /><br /> 這個欄位是適用於數值資料類型資料行。 應用程式可以將值插入含有自動遞增資料行的資料列，但通常不能更新資料行中的值。<br /><br /> 自動遞增資料行進行插入時，唯一的值會插入資料行在插入時。 增量未定義，但資料來源特有。 應用程式不應該假設任何特定值的自動遞增資料行開始在任何特定點或遞增。|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|基底的資料行名稱的結果集資料行。 如果基底的資料行名稱不存在 （如所示的是運算式的資料行的情況下），則此變數包含空字串。<br /><br /> 這項資訊是從 SQL_DESC_BASE_COLUMN_NAME 記錄欄位傳回的 IRD，也就是唯讀的欄位。|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|基底資料表包含資料行名稱。 如果基底資料表名稱不能定義，或不適用，則此變數包含空字串。<br /><br /> 這項資訊是從 SQL_DESC_BASE_TABLE_NAME 記錄欄位傳回的 IRD，也就是唯讀的欄位。|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|如果資料行來處理為區分大小寫定序和比較，SQL_TRUE。<br /><br /> 如果資料行也不會處理定序和比較為區分大小寫，或是非字元，SQL_FALSE。|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|資料表包含資料行的目錄。 傳回的值是由實作定義的資料行是運算式或資料行是檢視的一部分。 如果資料來源不支援目錄，或無法判斷目錄名稱，則會傳回空字串。 此 VARCHAR 記錄欄位不是限制為 128 個字元。|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|精簡的資料類型。<br /><br /> 日期時間和間隔資料類型，這個欄位會傳回精確的資料類型;比方說，SQL_TYPE_TIME 或 SQL_INTERVAL_YEAR。 (如需詳細資訊，請參閱 <<c0> [ 資料類型識別碼和描述元](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)附錄 d:資料型別。）<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_CONCISE_TYPE 記錄欄位傳回。|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|在結果集中可用的資料行數目。 如果結果集中沒有資料行，這會傳回 0。 中的值*ColumnNumber*引數會被忽略。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_COUNT 標頭欄位中傳回。|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|若要顯示的資料行的資料所需的字元數目上限。 如需有關顯示大小的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|如果資料行具有固定有效位數和非零值的小數位數的資料來源特有的 SQL_TRUE。<br /><br /> 如果資料行沒有資料來源特有的固定有效位數和非零值的小數位數，SQL_FALSE。|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|資料行標籤或標題。 比方說，名為 EmpName 的資料行可能會標示為 員工名稱，或可能會加上別名。<br /><br /> 如果資料行沒有標籤，則會傳回資料行名稱。 如果是沒有標籤資料行，且未命名的則會傳回空字串。|  
|SQL_DESC_LENGTH  (ODBC 3.0)|*NumericAttributePtr*|是一個數字值的最大頁數或實際字元長度的字元字串或二進位資料類型。 這是固定長度資料類型的最大字元長度或可變長度資料類型的實際字元長度。 其值一律不包括結束的字元字串的 null 終止位元組。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_LENGTH 記錄欄位傳回。<br /><br /> 如需長度的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|此 VARCHAR(128) 記錄欄位包含驅動程式會辨識為此資料類型的常值的前置詞的字元。 此欄位包含不適用的常值的前置詞的資料類型的空字串。 如需詳細資訊，請參閱 <<c0> [ 常值前置詞和後置詞](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|此 VARCHAR(128) 記錄欄位包含驅動程式會辨識為此資料類型的常值後置詞的字元。 此欄位包含不適用常值後置詞的資料類型的空字串。 如需詳細資訊，請參閱 <<c0> [ 常值前置詞和後置詞](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md)。|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|此 VARCHAR(128) 記錄欄位會包含任何當地語系化 （原生語言） 的名稱可能不同於一般的資料型別名稱的資料類型。 如果沒有當地語系化的名稱，則會傳回空字串。 這個欄位是僅供顯示。 字串的字元集是地區設定相關，而通常是伺服器的預設字元集。|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|如果它適用於資料行別名。 如果不適用資料行別名，則會傳回資料行名稱。 在任一情況下，將 SQL_DESC_UNNAMED 設為 SQL_NAMED。 如果沒有任何資料行名稱或資料行別名，則傳回空的字串，並將 SQL_DESC_UNNAMED 設 sql_unnamed 時。<br /><br /> 這項資訊會從 IRD 的與 SQL_DESC_NAME 記錄欄位傳回。|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ 可為 NULL 的資料行可以有 NULL 值; 如果如果資料行不具有 NULL 值;，SQL_NO_NULLS或 SQL_NULLABLE_UNKNOWN 如果不知道資料行是否接受 NULL 值。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_NULLABLE 記錄欄位傳回。|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|如果 SQL_DESC_TYPE 欄位中的資料類型是近似的數值資料類型，此 SQLINTEGER 欄位會包含值為 2，因為 SQL_DESC_PRECISION 欄位包含的位元數。 如果 SQL_DESC_TYPE 欄位中的資料類型是精確數值資料類型，此欄位會包含值為 10，因為 SQL_DESC_PRECISION 欄位包含的小數位數。 此欄位設為 0 表示所有非數值資料類型。|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|字元字串或二進位資料類型的長度，以位元組為單位。 固定長度的字元或二進位類型，這是以位元組為單位的實際長度。 可變長度的字元或二進位類型，這是以位元組為單位的最大長度。 此值不包括 null 結束字元。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_OCTET_LENGTH 記錄欄位傳回。<br /><br /> 如需長度的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d:資料類型。|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|表示數值資料類型的適用的有效位數數值的值。 資料類型 SQL_TYPE_TIME SQL_TYPE_TIMESTAMP，並代表時間間隔，其值的所有間隔資料類型都是適用於元件的有效位數小數秒數。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_PRECISION 記錄欄位傳回。|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|適用於數值資料類型的小數位數值。 DECIMAL 和 NUMERIC 資料類型，這是定義標尺。 其為未定義的所有其他資料類型。<br /><br /> 這項資訊會從 IRD 的小數位數筆記錄欄位傳回。|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含資料行的資料表結構描述。 傳回的值是由實作定義的資料行是運算式或資料行是檢視的一部分。 如果資料來源不支援結構描述，或無法判斷結構描述名稱，則會傳回空字串。 此 VARCHAR 記錄欄位不是限制為 128 個字元。|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|如果資料行不能在 WHERE 子句，SQL_PRED_NONE。 （這是 ODBC 2 SQL_UNSEARCHABLE 值相同。*x*。)<br /><br /> 如果資料行可以用於 WHERE 子句中，但是只能搭配 LIKE 述詞，SQL_PRED_CHAR。 （這是 ODBC 2 SQL_LIKE_ONLY 值相同。*x*。)<br /><br /> 如果資料行可以用於 WHERE 子句類似以外的所有比較運算子與，SQL_PRED_BASIC。 （這是 ODBC 2 SQL_EXCEPT_LIKE 值相同。*x*。)<br /><br /> 如果資料行可以用於 WHERE 子句搭配任何比較運算子，SQL_PRED_SEARCHABLE。<br /><br /> 資料行的輸入 SQL_LONGVARCHAR 和 SQL_LONGVARBINARY 通常傳回 SQL_PRED_CHAR。|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|包含資料行之資料表的名稱。 傳回的值是由實作定義的資料行是運算式或資料行是檢視的一部分。<br /><br /> 如果無法判斷資料表名稱，則會傳回空字串。|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|數值，指定 SQL 資料類型。<br /><br /> 當*ColumnNumber*等於 0，SQL_BINARY 會傳回可變長度的書籤並 SQL_INTEGER 會傳回固定長度書籤。<br /><br /> 日期時間和間隔資料類型，此欄位會傳回的詳細資訊的資料類型：如果是 SQL_DATETIME 或 SQL_INTERVAL。 (如需詳細資訊，請參閱 <<c0> [ 資料類型識別碼和描述元](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)附錄 d:資料類型。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_TYPE 記錄欄位傳回。 **注意：** 處理 ODBC 2。*x*驅動程式，改為使用 SQL_DESC_CONCISE_TYPE。|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|資料來源相關的資料型別名稱;比方說，"CHAR"、"VARCHAR"、"MONEY"、"長 VARBINARY"或者"CHAR （） FOR BIT DATA"。<br /><br /> 如果類型是未知，則會傳回空字串。|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED 或 sql_unnamed 時。 如果與 SQL_DESC_NAME 欄位 IRD 的包含資料行別名或資料行名稱，則會傳回 SQL_NAMED。 如果沒有任何資料行名稱或資料行別名，則會傳回 sql_unnamed 時。<br /><br /> 這項資訊會從 IRD 的 SQL_DESC_UNNAMED 記錄欄位傳回。|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE 如果資料行是不帶正負號 （或不是數字）。<br /><br /> 如果資料行簽章，SQL_FALSE。|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|資料行會描述所定義的常數的值：<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE 描述結果集中資料行中，不是基底資料表中的資料行的可更新性。 基底結果集資料行所依據的資料行的可更新性可能不同於此欄位中的值。 資料行是否可更新可以根據資料類型、 使用者權限，以及結果集本身的定義。 如果是不明確的資料行是否可更新，應該會傳回 SQL_ATTR_READWRITE_UNKNOWN。|  
  
 **SQLColAttribute**是可延伸替代**SQLDescribeCol**。 **SQLDescribeCol**傳回一組固定的 ANSI 89 SQL 為基礎的描述元資訊。 **SQLColAttribute**可讓您存取更詳盡的 ANSI SQL-92 和 DBMS 廠商延伸模組中可用的描述元資訊。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在結果集中傳回資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>範例  
 下列範例程式碼不會釋放控制代碼和連線。 請參閱[SQLFreeHandle 函式](../../../odbc/reference/syntax/sqlfreehandle-function.md)， [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)，並[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)來釋放控制代碼和陳述式的程式碼範例。  
  
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
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
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
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)
