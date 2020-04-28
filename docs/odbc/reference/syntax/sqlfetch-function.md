---
title: SQLFetch 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e2da6996d8d6b2ee66befdc90794efec5617b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285968"
---
# <a name="sqlfetch-function"></a>SQLFetch 函式
**標準**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLFetch**會從結果集提取下一個資料列集，並傳回所有系結資料行的資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetch**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)函式，並將*HandleType* SQL_HANDLE_STMT 和*StatementHandle*的*控制碼*，來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLFetch**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。 如果單一資料行發生錯誤，則可以使用 SQL_DIAG_COLUMN_NUMBER 的*以*呼叫[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) ，以判斷發生錯誤的資料行。您可以使用 SQL_DIAG_ROW_NUMBER 的*以*來呼叫和**SQLGetDiagField** ，以判斷包含該資料行的資料列。  
  
 對於可以傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除了 01xxx SQLSTATEs）的所有 SQLSTATEs，如果一或多個多資料列作業的資料列發生錯誤，則會傳回 SQL_SUCCESS_WITH_INFO，而如果單一資料列作業發生錯誤，則會傳回 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|傳回資料行的字串或二進位資料導致截斷非空白字元或非 Null 的二進位資料。 如果它是字串值，則會被右截斷。|  
|01S01|資料列發生錯誤|提取一或多個資料列時發生錯誤。<br /><br /> （如果當 ODBC 3.x 應用程式與 ODBC 2.x*驅動程式搭配*使用時，會傳回此 *.x* SQLSTATE，則可以略過）。|  
|01S07|小數截斷|針對資料行傳回的資料已被截斷。 若為數值資料類型，則會截斷數位的小數部分。 若為包含時間元件的時間、時間戳記和間隔資料類型，則會截斷時間的小數部分。<br /><br /> （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|限制的資料類型屬性違規|在結果集中，資料行的資料值無法轉換成**SQLBindCol**中*TargetType*所指定的資料類型。<br /><br /> 資料行0系結了 SQL_C_BOOKMARK 的資料類型，且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE。<br /><br /> 資料行0系結了 SQL_C_VARBOOKMARK 的資料類型，且 SQL_ATTR_USE_BOOKMARKS 語句屬性未設定為 SQL_UB_VARIABLE。|  
|07009|不正確描述項索引|驅動程式是一個不支援**SQLExtendedFetch**的 ODBC*2.x 驅動程式*，而且資料行的系結中指定的資料行編號是0。<br /><br /> 已系結資料行0，而且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊已截斷|針對資料行傳回的可變長度書簽已截斷。|  
|22002|需要指標變數，但未提供|已將 Null 資料提取到資料行，其*StrLen_or_IndPtr*由**SQLBindCol**設定（或是**SQLSetDescField**或**SQLSetDescRec**所設定的 SQL_DESC_INDICATOR_PTR）為 null 指標。|  
|22003|數值超出範圍|針對一個或多個系結資料行，將數值傳回為數值或字串，可能會導致整個（而不是小數）部分的數位被截斷。<br /><br /> 如需詳細資訊，請參閱附錄 D：資料類型中的[將資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。|  
|22007|不正確日期時間格式|結果集中的字元資料行已系結至日期、時間或時間戳記 C 結構，而且資料行中的值分別為不正確日期、時間或時間戳記。|  
|22012|除數為零|傳回算術運算式的值，導致零除。|  
|22015|間隔欄位溢位|從精確的數值或間隔 SQL 類型指派到間隔 C 類型，會導致前置欄位中的有效位數遺失。<br /><br /> 將資料提取到 interval C 類型時，不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|結果集中的字元資料行已系結至字元 C 緩衝區，而資料行包含的字元在緩衝區的字元集中沒有標記法。<br /><br /> C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;而資料行中的值不是系結 C 類型的有效常值。|  
|24000|指標狀態無效|*StatementHandle*處於執行中狀態，但沒有與*StatementHandle*相關聯的結果集。|  
|40001|序列化失敗|執行提取的交易已終止，以避免發生鎖死。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗，無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 * \* *|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|已啟用*StatementHandle*的非同步處理。 已**呼叫 SQLFetch**函式，在完成執行之前，會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫**SQLFetch**函式。<br /><br /> 或者，已**呼叫 SQLFetch**函式，在完成執行之前，會從多執行緒應用程式中的不同執行緒呼叫*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLFetch**函數時，這個非同步函式仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）指定的*StatementHandle*不是處於執行中狀態。 在未先呼叫**SQLExecDirect**、 **SQLExecute**或目錄函式的情況下呼叫函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式（而非這個函式），而且在呼叫這個函數時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。<br /><br /> （DM）在呼叫**SQLExtendedFetch**之後，以及呼叫具有 SQL_CLOSE 選項的**SQLFreeStmt**之前，會呼叫*StatementHandle*的**SQLFetch** 。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|SQL_ATTR_USE_BOOKMARK 語句屬性已設定為 SQL_UB_VARIABLE，而資料行0已系結至緩衝區，其長度不等於此結果集之書簽的最大長度。 （此長度可在 IRD 的 [SQL_DESC_OCTET_LENGTH] 欄位中使用，而且可以藉由呼叫**SQLDescribeCol**、 **SQLColAttribute**或**SQLGetDescField**來取得）。|  
|HY107|資料列值超出範圍|已 SQL_CURSOR_KEYSET_DRIVEN 使用 SQL_ATTR_CURSOR_TYPE 語句屬性指定的值，但以 SQL_ATTR_KEYSET_SIZE 語句屬性指定的值大於0且小於以 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性指定的值。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*組合和對應資料行的 SQL 資料類型所指定的轉換。|  
|HYT00|已超過逾時的設定|在資料來源傳回要求的結果集之前，查詢超時時間已過期。 超時期間是透過 SQLSetStmtAttr 設定，SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 而且如果啟用通知模式，則必須在控制碼上呼叫**SQLCompleteAsync** ，才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>評價  
 **SQLFetch**會傳回結果集中的下一個資料列集。 只有當結果集存在時，才可以呼叫它：也就是在呼叫之後建立結果集，而且在關閉該結果集的資料指標之前。 如果系結了任何資料行，則會傳回這些資料行中的資料。 如果應用程式已指定資料列狀態陣列的指標，或要傳回提取之資料列數目的緩衝區，則**SQLFetch**也會傳回這項資訊。 呼叫**SQLFetch**可以與**SQLFetchScroll**的呼叫混合，但不能與**SQLExtendedFetch**的呼叫混合使用。 如需詳細資訊，請參閱[提取資料列](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC*3.x 應用程式*與 odbc 2.x 驅動程式搭配運作 *，驅動程式*管理員會將**SQLFetch**呼叫對應至支援**SQLExtendedFetch**之 odbc 2.x*驅動程式的* **SQLExtendedFetch** 。 如果 ODBC 2.x 驅動程式不支援**SQLExtendedFetch**，*驅動程式管理員*會將**SQLFetch**呼叫對應至 ODBC*2.x 驅動程式*中的**SQLFetch** ，這只能提取單一資料列。  
  
 如需詳細資訊，請參閱附錄 G：驅動程式方針中的[區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="positioning-the-cursor"></a>將游標定位  
 建立結果集時，資料指標會位於結果集的開頭之前。 **SQLFetch**會提取下一個資料列集。 這相當於呼叫**SQLFetchScroll** ，並將*FetchOrientation*設為 SQL_FETCH_NEXT。 如需資料指標的詳細資訊，請參閱資料[指標](../../../odbc/reference/develop-app/cursors.md)和[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性會指定資料列集中的資料列數目。 如果**SQLFetch**所提取的資料列集與結果集的結尾重迭， **SQLFetch**會傳回部分資料列集。 也就是說，如果 S + R-1 大於 L，其中 S 是要提取之資料列集的起始資料列，R 是資料列集大小，而 L 是結果集中的最後一個資料列，則只有資料列集的第一個 L-S + 1 資料列才有效。 其餘的資料列是空的，且狀態為 SQL_ROW_NOROW。  
  
 在**SQLFetch**傳回之後，目前的資料列就是資料列集的第一個資料列。  
  
 下表所列的規則會根據本節第二個數據表中所列的條件，說明呼叫**SQLFetch**之後的資料指標定位。  
  
|狀況|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|開始之前|1|  
|*CurrRowsetStart* \<CurrRowsetStart =  *LastResultRow-RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow-RowsetSize*[1]|結束之後|  
|結束之後|結束之後|  
  
 [1] 如果提取之間的資料列集大小有所變更，這就是與先前的 fetch 搭配使用的資料列集大小。  
  
 [2] 如果在提取之間變更了資料列集大小，這就是與新的 fetch 搭配使用的資料列集大小。  
  
|表示法|意義|  
|--------------|-------------|  
|開始之前|區塊資料指標位於結果集開頭之前。 如果新資料列集的第一個資料列是在結果集的開頭之前，則**SQLFetch**會傳回 SQL_NO_DATA。|  
|結束之後|區塊資料指標位於結果集的結尾之後。 如果新資料列集的第一個資料列位於結果集的結尾，則**SQLFetch**會傳回 SQL_NO_DATA。|  
|*CurrRowsetStart*|目前資料列集中第一個資料列的編號。|  
|*LastResultRow*|結果集中最後一個資料列的編號。|  
|*RowsetSize*|資料列集大小。|  
  
 例如，假設結果集有100個數據列，而資料列集大小為5。 下表顯示**SQLFetch**針對不同開始位置所傳回的資料列集和傳回碼。  
  
|目前的資料列集|傳回碼|新增資料列集|已提取的資料列數目|  
|--------------------|-----------------|----------------|------------------------|  
|開始之前|SQL_SUCCESS|1到5|5|  
|1到5|SQL_SUCCESS|6到10|5|  
|52到56|SQL_SUCCESS|57到61|5|  
|91到95|SQL_SUCCESS|96到100|5|  
|93到97|SQL_SUCCESS|98到100。 資料列狀態陣列的資料列4和5會設定為 SQL_ROW_NOROW。|3|  
|96到100|SQL_NO_DATA|無。|0|  
|99到100|SQL_NO_DATA|無。|0|  
|結束之後|SQL_NO_DATA|無。|0|  
  
## <a name="returning-data-in-bound-columns"></a>傳回系結資料行中的資料  
 當**SQLFetch**傳回每個資料列時，它會將每個綁定欄的資料放在系結至該資料行的緩衝區中。 如果未系結任何資料行，則**SQLFetch**不會傳回任何資料，但會將區塊游標向前移動。 您仍然可以使用**SQLGetData**來抓取資料。 如果資料指標是多資料列的資料指標（也就是，SQL_ATTR_ROW_ARRAY_SIZE 大於1），則只有在使用*InfoType*為 SQL_GETDATA_EXTENSIONS 呼叫**SQLGetInfo**時，SQL_GD_BLOCK 才會呼叫**SQLGetData** 。 （如需詳細資訊，請參閱[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)）。  
  
 針對資料列中的每個系結資料行， **SQLFetch**會執行下列動作：  
  
1.  將長度/指標緩衝區設定為 SQL_Null_DATA，並在資料為 Null 時繼續到下一個資料行。 如果資料為 Null，且未系結長度/指標緩衝區， **SQLFetch**會傳回資料列的 SQLSTATE 22002 （需要但不提供指標變數），並繼續進行下一個資料列。 如需如何判斷長度/指標緩衝區位址的詳細資訊，請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
     如果資料行的資料不是 Null， **SQLFetch**會繼續執行步驟2。  
  
2.  如果 SQL_ATTR_MAX_LENGTH 語句屬性設定為非零值，且資料行包含字元或二進位資料，則會將資料截斷為 SQL_ATTR_MAX_LENGTH 個位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 語句屬性的目的是要減少網路流量。 它通常是由資料來源所執行，它會先截斷資料，然後再透過網路傳回。 不需要驅動程式和資料來源來支援它。 因此，為了確保資料會被截斷成特定大小，應用程式應該配置該大小的緩衝區，並在**SQLBindCol**的*cbValueMax*引數中指定大小。  
  
3.  將資料轉換為**SQLBindCol**中的*TargetType*所指定的類型。  
  
4.  如果資料轉換成可變長度的資料類型（例如字元或二進位）， **SQLFetch**會檢查資料長度是否超過資料緩衝區的長度。 如果字元資料的長度（包括 null 終止字元）超過資料緩衝區的長度， **SQLFetch**會將資料截斷為資料緩衝區長度減去 null 終止字元的長度。 然後，它會以 null 結束資料。 如果二進位資料的長度超過資料緩衝區的長度， **SQLFetch**會將它截斷為資料緩衝區的長度。 資料緩衝區的長度是以**SQLBindCol**中的*BufferLength*指定。  
  
     **SQLFetch**絕對不會截斷轉換成固定長度資料類型的資料;它一律會假設資料緩衝區的長度是資料類型的大小。  
  
5.  將轉換的（而且可能已截斷）資料放在資料緩衝區中。 如需如何判斷資料緩衝區位址的詳細資訊，請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
6.  將資料的長度放在長度/指標緩衝區中。 如果指標指標和長度指標都設定為相同的緩衝區（如同呼叫**SQLBindCol** ），則會在緩衝區中寫入有效資料的長度，並在緩衝區中寫入 Null 資料的 SQL_Null_DATA。 如果未系結長度/指標緩衝區， **SQLFetch**就不會傳回長度。  
  
    -   對於字元或二進位資料，這是轉換後的資料長度，而且在截斷之前，因為資料緩衝區太小。 如果在轉換之後，驅動程式無法判斷資料的長度，有時會將長度設定為 SQL_NO_TOTAL。 如果因為 SQL_ATTR_MAX_LENGTH 語句屬性而截斷資料，這個屬性的值會放在長度/指標緩衝區中，而不是實際長度。 這是因為這個屬性是設計用來在轉換之前截斷伺服器上的資料，因此驅動程式無法找出實際長度。  
  
    -   對於所有其他資料類型，這是轉換後的資料長度;也就是說，它是轉換資料的目標型別大小。  
  
     如需如何判斷長度/指標緩衝區位址的詳細資訊，請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
7.  如果在轉換期間截斷資料而不會遺失有效位數（例如，在轉換時，實數1.234 會被截斷為整數1），則**SQLFetch**會傳回 SQLSTATE 01S07 （小數截斷）和 SQL_SUCCESS_WITH_INFO。 如果因為資料緩衝區的長度太小而截斷資料（例如，字串 "abcdef" 放在4位元組的緩衝區中）， **SQLFetch**會傳回 SQLSTATE 01004 （資料已截斷）和 SQL_SUCCESS_WITH_INFO。 如果因為 SQL_ATTR_MAX_LENGTH 語句屬性而截斷資料，則**SQLFetch**會傳回 SQL_SUCCESS 而且不會傳回 SQLSTATE 01S07 （小數截斷）或 SQLSTATE 01004 （資料已截斷）。 如果在轉換期間因遺失有效位數而截斷資料（例如，如果 SQL_INTEGER 值大於100000已轉換成 SQL_C_TINYINT），則**SQLFetch**會傳回 SQLSTATE 22003 （數值超出範圍）和 SQL_ERROR （如果資料列集大小為1）或 SQL_SUCCESS_WITH_INFO （如果資料列集大小大於1）。  
  
 如果**SQLFetch**或**SQLFetchScroll**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則系結資料緩衝區的內容和長度/指標緩衝區不會定義。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 資料列狀態陣列是用來傳回資料列集內每個資料列的狀態。 此陣列的位址是使用 SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定。 陣列是由應用程式佈建，而且必須擁有與 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所指定的數目相同的元素。 其值是由**SQLFetch**、 **SQLFetchScroll**和**SQLBulkOperations**或**SQLSetPos**所設定（但在將資料指標置於**SQLExtendedFetch**的位置之後，才會呼叫它們）。 如果 SQL_ATTR_ROW_STATUS_PTR 語句屬性的值為 null 指標，則這些函式不會傳回資料列狀態。  
  
 如果**SQLFetch**或**SQLFetchScroll**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則不會定義資料列狀態陣列緩衝區的內容。  
  
 下列值會在資料列狀態陣列中傳回。  
  
|資料列狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|已成功提取資料列，而且自上次從這個結果集提取之後，尚未變更。|  
|SQL_ROW_SUCCESS_WITH_INFO|已成功提取資料列，而且自上次從這個結果集提取之後，尚未變更。 不過，傳回關於資料列的警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED [1]、[2] 和 [3]|已成功提取資料列，而且自上次從這個結果集提取之後已經變更。 如果資料列是從這個結果集再次提取，或由**SQLSetPos**重新整理，則狀態會變更為資料列的新狀態。|  
|SQL_ROW_DELETED [3]|上次從這個結果集提取資料列之後，已將其刪除。|  
|SQL_ROW_ADDED [4]|**SQLBulkOperations**插入資料列。 如果從這個結果集再次提取資料列，或由**SQLSetPos**重新整理，其狀態會是 SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|資料列集會重迭結果集的結尾，而且不會傳回雖然該值到資料列狀態陣列之這個元素的任何資料列。|  
  
 [1] 針對索引鍵集、混合和動態資料指標，如果更新索引鍵值，則會將資料列視為已刪除，並加入新的資料列。  
  
 [2] 某些驅動程式無法偵測到資料的更新，因此無法傳回此值。 若要判斷驅動程式是否可以偵測到根據資料列的更新，應用程式會使用 SQL_ROW_UPDATES 選項來呼叫**SQLGetInfo** 。  
  
 [3] **SQLFetch**只有在與**SQLFetchScroll**的呼叫混合時，才會傳回此值。 這是因為**SQLFetch**會在結果集中向前移動，而且當它以獨佔方式使用時，不會重新擷取任何資料列。 因為沒有根據資料列，所以**SQLFetch**不會偵測到對先前提取的資料列所做的變更。 不過，如果**SQLFetchScroll**在先前提取的資料列之前放置資料指標，而使用**SQLFetch**來提取這些資料列，則**SQLFetch**可以偵測到那些資料列的任何變更。  
  
 [4] 僅由 SQLBulkOperations 傳回。 不是由**SQLFetch**或**SQLFetchScroll**所設定。  
  
### <a name="rows-fetched-buffer"></a>讀取的資料列緩衝區  
 提取的緩衝區會用來傳回所提取的資料列數目，包括因為提取時發生錯誤，而未傳回任何資料的資料列。 換句話說，這是資料列狀態陣列中的值不 SQL_ROW_NOROW 的資料列數目。 這個緩衝區的位址是使用 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性所指定。 緩衝區是由應用程式所配置。 它是由**SQLFetch**和**SQLFetchScroll**所設定。 如果 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性的值為 null 指標，則這些函式不會傳回所提取的資料列數目。 若要判斷結果集中目前資料列的數目，應用程式可以使用 SQL_ATTR_ROW_NUMBER 屬性來呼叫**SQLGetStmtAttr** 。  
  
 如果**SQLFetch**或**SQLFetchScroll**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則不會定義已提取之資料列的內容，但當傳回 SQL_NO_DATA 時除外，在此情況下，資料列提取緩衝區中的值會設定為0。  
  
### <a name="error-handling"></a>錯誤處理  
 錯誤和警告可以套用至個別資料列或整個函數。 如需診斷記錄的詳細資訊，請參閱[診斷](../../../odbc/reference/develop-app/diagnostics.md)和[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>整個功能的錯誤和警告  
 如果錯誤適用于整個函式，例如 SQLSTATE HYT00 （超時時間已過期）或 SQLSTATE 24000 （不正確資料指標狀態），則**SQLFetch**會傳回 SQL_ERROR 和適用的 SQLSTATE。 資料列集緩衝區的內容未定義，且資料指標位置不變。  
  
 如果警告適用于整個函式， **SQLFetch**會傳回 SQL_SUCCESS_WITH_INFO 和適用的 SQLSTATE。 適用于整個函式之警告的狀態記錄會在套用至個別資料列的狀態記錄之前傳回。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>個別資料列中的錯誤和警告  
 如果錯誤（例如 SQLSTATE 22012 （除數為零）或警告（例如 SQLSTATE 01004 （資料已截斷））套用至單一資料列， **SQLFetch**會執行下列動作：  
  
-   設定資料列狀態陣列的對應元素，以 SQL_ROW_ERROR 錯誤或警告 SQL_ROW_SUCCESS_WITH_INFO。  
  
-   加入零或多個包含錯誤或警告 SQLSTATEs 的狀態記錄。  
  
-   設定狀態記錄中的資料列和資料行編號欄位。 如果**SQLFetch**無法判斷資料列或資料行編號，會分別將該數位設定為 SQL_ROW_NUMBER_UNKNOWN 或 SQL_COLUMN_NUMBER_UNKNOWN。 如果狀態記錄不適用特定資料行， **SQLFetch**會將資料行編號設定為 SQL_NO_COLUMN_NUMBER。  
  
 **SQLFetch**會繼續提取資料列，直到其提取資料列集中的所有資料列為止。 除非資料列集的每個資料列中發生錯誤（不包括狀態 SQL_ROW_NOROW 的資料列），否則會傳回 SQL_SUCCESS_WITH_INFO，在這種情況下，它會傳回 SQL_ERROR。 特別是，如果資料列集大小為1，且該資料列發生錯誤，則**SQLFetch**會傳回 SQL_ERROR。  
  
 **SQLFetch**會以資料列編號順序傳回狀態記錄。 也就是說，它會傳回未知資料列的所有狀態記錄（如果有的話）;接下來，它會傳回第一個資料列的所有狀態記錄（如果有的話），然後傳回第二個數據列的所有狀態記錄（如果有的話），依此類推。 每個資料列的狀態記錄都會根據排序狀態記錄的一般規則來排序;如需詳細資訊，請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)中的「狀態記錄的順序」。  
  
### <a name="descriptors-and-sqlfetch"></a>描述項和 SQLFetch  
 下列各節說明**SQLFetch**如何與描述項互動。  
  
#### <a name="argument-mappings"></a>引數對應  
 驅動程式不會根據**SQLFetch**的引數設定任何描述項欄位。  
  
#### <a name="other-descriptor-fields"></a>其他描述項欄位  
 **SQLFetch**會使用下列描述項欄位。  
  
|描述項欄位|降冪.|中的欄位|設定|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|頁首|SQL_ATTR_ROW_ARRAY_SIZE 語句屬性|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|頁首|SQL_ATTR_ROW_STATUS_PTR 語句屬性|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|頁首|SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性|  
|SQL_DESC_BIND_TYPE|ARD|頁首|SQL_ATTR_ROW_BIND_TYPE 語句屬性|  
|SQL_DESC_COUNT|ARD|頁首|**SQLBindCol**的*ColumnNumber*引數|  
|SQL_DESC_DATA_PTR|ARD|記錄|**SQLBindCol**的*TargetValuePtr*引數|  
|SQL_DESC_INDICATOR_PTR|ARD|記錄|**SQLBindCol**中的*StrLen_or_IndPtr*引數|  
|SQL_DESC_OCTET_LENGTH|ARD|記錄|**SQLBindCol**中的*BufferLength*引數|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|記錄|**SQLBindCol**中的*StrLen_or_IndPtr*引數|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|頁首|SQL_ATTR_ROWS_FETCHED_PTR 語句屬性|  
|SQL_DESC_TYPE|ARD|記錄|**SQLBindCol**中的*TargetType*引數|  
  
 所有的描述項欄位也可以透過**SQLSetDescField**來設定。  
  
#### <a name="separate-length-and-indicator-buffers"></a>分隔長度和指標緩衝區  
 應用程式可以系結單一緩衝區或兩個可以用來保存長度和指標值的不同緩衝區。 當應用程式呼叫**SQLBindCol**時，驅動程式會將 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 欄位設定為相同的位址，並在*StrLen_or_IndPtr*引數中傳遞。 當應用程式呼叫**SQLSetDescField**或**SQLSetDescRec**時，可以將這兩個欄位設定為不同的位址。  
  
 **SQLFetch**會判斷應用程式是否已指定不同的長度和指標緩衝區。 在此情況下，當資料不是 Null 時， **SQLFetch**會將指標緩衝區設定為0，並傳回長度緩衝區中的長度。 當資料為 Null 時， **SQLFetch**會將指標緩衝區設定為 SQL_Null_DATA，而且不會修改長度緩衝區。  
  
### <a name="code-example"></a>程式碼範例  
 請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)和[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)。  
  
### <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|關閉語句上的資料指標|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|正在提取部分或所有資料行|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備語句以執行|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
