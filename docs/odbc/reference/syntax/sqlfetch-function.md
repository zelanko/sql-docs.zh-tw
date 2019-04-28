---
title: SQLFetch 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetch
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetch
helpviewer_keywords:
- SQLFetch function [ODBC]
ms.assetid: 6c6611d2-bc6a-4390-87c9-1c5dd9cfe07c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 001238b4e5d47b22ca991efcd8b4ee28971d7af7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "62982302"
---
# <a name="sqlfetch-function"></a>SQLFetch 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLFetch**提取從結果集中的下一個資料列集的資料，並傳回所有繫結的資料行的資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetch**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫[SQLGetDiagRec 函式](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)使用*HandleType*利用 SQL_HANDLE_STMT 的和 a*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLFetch** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。 如果在單一資料行，就會發生錯誤[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)也可以呼叫*Sqlgetdiagfield* SQL_DIAG_COLUMN_NUMBER 來判斷發生錯誤; 資料行的和**SQLGetDiagField**也可以呼叫*Sqlgetdiagfield*的 SQL_DIAG_ROW_NUMBER 來決定包含該資料行的資料列。  
  
 針對所有這些 Sqlstate 可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除了 01xxx Sqlstate)，如果一個或多個，而非全部的資料列的多資料列的作業，發生錯誤，而且如果發生錯誤時，會傳回 SQL_ERROR，則會傳回 SQL_SUCCESS_WITH_INFO單一資料列作業。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|字串或二進位資料傳回的資料行導致的非空白的字元或非 NULL 的二進位資料截斷。 如果是字串值，則向右截斷。|  
|01S01|資料列中的錯誤|擷取一或多個資料列時發生錯誤。<br /><br /> (如果 ODBC 3 時，會傳回此 SQLSTATE *.x*應用程式正在使用的 ODBC 2 *.x*驅動程式，可以忽略它。)|  
|01S07|小數位數截斷|傳回資料行的資料已遭截斷。 數值資料類型已遭截斷數字的小數部分。 時間、 時間戳記，和包含時間元件的 interval 資料類型，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|在結果集中的資料行的資料值無法轉換成所指定的資料類型*TargetType*中**SQLBindCol**。<br /><br /> 資料類型為 SQL_C_BOOKMARK，繫結資料行 0 且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_VARIABLE。<br /><br /> 資料類型為 SQL_C_VARBOOKMARK，繫結資料行 0 和 SQL_ATTR_USE_BOOKMARKS 陳述式屬性未設定為 SQL_UB_VARIABLE。|  
|07009|描述項索引無效|驅動程式的 ODBC 2 *.x*不支援的驅動程式**SQLExtendedFetch**，和資料行繫結中指定資料行編號為 0。<br /><br /> 繫結資料行 0，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊已截斷|傳回資料行的可變長度書籤已遭截斷。|  
|22002|指標變數但未提供|NULL 的資料擷取成資料行其*StrLen_or_IndPtr*來設定**SQLBindCol** (或所設定的 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 為 null 指標。|  
|22003|數值超出範圍|傳回數字的值視為數值或字串的一或多個繫結的資料行可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附錄 d:資料類型。|  
|22007|無效的日期時間格式|在結果集中的字元資料行已繫結至日期、 時間或時間戳記 C 結構，但資料行的值，分別無效的日期、 時間戳記。|  
|22012|除數為零|算術運算式的值傳回，因而導致除數為零。|  
|22015|間隔欄位溢位|將指派從精確數值或時間間隔 SQL 型別，給 C 間隔類型造成有效位數的遺失開頭的欄位中。<br /><br /> 當 C 間隔類型以提取資料時，發生 C 間隔類型中的 SQL 類型的值不表示。|  
|22018|轉換規格的字元值無效|在結果集中的字元資料行已繫結至字元 C 的緩衝區，和資料行包含緩衝區的字元集中未表示的字元。<br /><br /> C 類型為精確或近似數值、 日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;和資料行中的值不是有效的常值的繫結的 C 類型。|  
|24000|指標狀態無效|*StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。|  
|40001|序列化失敗|擷取已執行所在的交易已終止避免死結。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 **SQLFetch**呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*. 然後**SQLFetch**在上一次呼叫函式*StatementHandle*。<br /><br /> 或者， **SQLFetch**呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒，多執行緒應用程式中。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLFetch**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 已呼叫的函式，但是未先呼叫**SQLExecDirect**， **SQLExecute**或目錄函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLFetch**針對呼叫*StatementHandle*之後**SQLExtendedFetch**呼叫之前**SQLFreeStmt** SQL_ 與已呼叫關閉選項。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|SQL_ATTR_USE_BOOKMARK 陳述式屬性已設定為 SQL_UB_VARIABLE，而且資料行 0 已繫結至其長度不等於此結果集的書籤的最大長度的緩衝區。 (這個長度的 SQL_DESC_OCTET_LENGTH IRD 欄位中而且可由呼叫**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY107|資料列值超出範圍|SQL_ATTR_CURSOR_TYPE 陳述式屬性所指定的值是 SQL_CURSOR_KEYSET_DRIVEN，但使用 SQL_ATTR_KEYSET_SIZE 陳述式屬性所指定的值是大於 0 且小於 SQL_ATTR_ROW_ARRAY_ 與指定的值大小陳述式屬性。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援指定的組合來轉換*TargetType*中**SQLBindCol**和對應的資料行的 SQL 資料類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 透過 SQLSetStmtAttr，sql_attr_query_timeout 時設定的逾時期限。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLFetch**結果集中傳回的下一個資料列集。 只有當結果集存在時，才可以呼叫它： 也就是說，在呼叫之後，建立結果集，而且游標之前關閉結果集的移轉。 如果任何資料行已繫結，它會傳回這些資料行中的資料。 如果應用程式具有指定資料列狀態陣列或在其中傳回擷取的資料列數目的緩衝區的指標**SQLFetch**也會傳回這項資訊。 呼叫**SQLFetch**可以透過呼叫混合**SQLFetchScroll**但不能呼叫的方式來混合**SQLExtendedFetch**。 如需詳細資訊，請參閱 <<c0> [ 擷取資料的資料列](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC 3 *.x*應用程式會使用 ODBC 2 *.x*驅動程式，則驅動程式管理員會對應**SQLFetch**呼叫**SQLExtendedFetch**的ODBC 2 *.x*支援的驅動程式**SQLExtendedFetch**。 如果 ODBC 2 *.x*驅動程式不支援**SQLExtendedFetch**，則驅動程式管理員會將對應**SQLFetch**呼叫**SQLFetch** ODBC 2 *.x*驅動程式，可以擷取單一資料列。  
  
 如需詳細資訊，請參閱 <<c0> [ 區塊資料指標、 可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
## <a name="positioning-the-cursor"></a>遊標定位在  
 建立結果集時，資料指標位於結果集的開頭之前。 **SQLFetch**提取下一個資料列集。 它相當於呼叫**SQLFetchScroll**具有*Sqlfetchscroll*設 SQL_FETCH_NEXT。 如需有關資料指標的詳細資訊，請參閱 <<c0> [ 資料指標](../../../odbc/reference/develop-app/cursors.md)並[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性會指定資料列集中的資料列數目。 如果所要提取的資料列集**SQLFetch**重疊的結果集結尾**SQLFetch**傳回部分的資料列集。 也就是說，如果 S + R，-1 大於 L，其中 S 資料列集擷取，R 的起始資料列是資料列集大小，而 L 最後一個資料列結果集中，則只有第一個 L-S + 1 個資料列集的資料列都有效。 剩餘的資料列是空的且狀態為 SQL_ROW_NOROW。  
  
 在後**SQLFetch**傳回時，目前的資料列是資料列集的第一個資料列。  
  
 下表所列的規則說明資料指標定位呼叫後**SQLFetch**，這取決於第二個資料表，這一節中所列的條件。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|開始之前|1|  
|*CurrRowsetStart* \<= *LastResultRow - RowsetSize*[1]|*CurrRowsetStart* + *RowsetSize*[2]|  
|*CurrRowsetStart* > *LastResultRow - RowsetSize*[1]|後端|  
|後端|後端|  
  
 [1] 如果之間擷取變更資料列集大小，這是曾經與前一個擷取的資料列集大小。  
  
 [2] 如果之間擷取變更資料列集大小，這會是所使用的新擷取的資料列集大小。  
  
|表示法|意義|  
|--------------|-------------|  
|開始之前|區塊資料指標位於結果集的開頭之前。 如果新的資料列集的第一個資料列的結果集中，開始之前**SQLFetch**傳回 sql_no_data 為止。|  
|後端|區塊資料指標位於結果結尾設定之後。 如果新的資料列集的第一個資料列之後的結果集結尾**SQLFetch**傳回 sql_no_data 為止。|  
|*CurrRowsetStart*|中目前資料列集的第一個資料列數目。|  
|*LastResultRow*|在結果集中的最後一個資料列數目。|  
|*RowsetSize*|資料列集大小。|  
  
 例如，假設結果集有 100 個資料列和資料列集大小為 5。 下表顯示所傳回的資料列集和傳回碼**SQLFetch**不同的起始位置。  
  
|目前資料列集|傳回碼|新的資料列集|擷取的資料列數目|  
|--------------------|-----------------|----------------|------------------------|  
|開始之前|SQL_SUCCESS|1 到 5|5|  
|1 到 5|SQL_SUCCESS|6 到 10|5|  
|52 到 56|SQL_SUCCESS|57 到 61|5|  
|91 到 95|SQL_SUCCESS|96 至 100|5|  
|93 到 97|SQL_SUCCESS|98 到 100。 4 和 5 的資料列狀態陣列的資料列會設為 SQL_ROW_NOROW。|3|  
|96 至 100|SQL_NO_DATA|無。|0|  
|99 到 100 之間|SQL_NO_DATA|無。|0|  
|後端|SQL_NO_DATA|無。|0|  
  
## <a name="returning-data-in-bound-columns"></a>繫結的資料行中傳回的資料  
 作為**SQLFetch**傳回每個資料列中，它會將每個繫結的資料行的資料放在繫結至該資料行緩衝區中。 如果沒有資料行已繫結， **SQLFetch**會傳回任何資料，但未向前移動區塊資料指標。 仍然可以使用擷取的資料**SQLGetData**。 如果資料指標的多資料列的資料指標 （也就是 SQL_ATTR_ROW_ARRAY_SIZE 大於 1）， **SQLGetData** SQL_GD_BLOCK 時，會傳回時，才可以呼叫**SQLGetInfo**呼叫*資訊類型*SQL_GETDATA_EXTENSIONS。 (如需詳細資訊，請參閱 < [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。)  
  
 每個繫結資料行中的資料列**SQLFetch**會進行下列作業：  
  
1.  設定為 SQL_NULL_DATA 的長度/指標緩衝區，並繼續進行下一個資料行，如果資料為 NULL。 如果資料為 NULL，而且沒有長度/指標緩衝區已繫結時， **SQLFetch**資料列會傳回 SQLSTATE 22002 （指標變數所需但未提供），然後繼續進行下一個資料列。 如何判斷長度/指標緩衝區的位址的相關資訊，請參閱 「 緩衝區位址 」，在[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
     如果資料行的資料不是 NULL， **SQLFetch**繼續進行步驟 2。  
  
2.  如果 SQL_ATTR_MAX_LENGTH 陳述式屬性設定為非零值，且資料行包含字元或二進位資料，就會將資料截斷為 SQL_ATTR_MAX_LENGTH 個位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 陳述式屬性被要減少網路流量。 它通常被藉由資料來源，再透過網路進行截斷的資料。 驅動程式和資料來源不需要支援它。 因此，若要確保資料會截斷成特定的大小，應用程式應該配置該大小的緩衝區和指定的大小以*cbValueMax*中的引數**SQLBindCol**。  
  
3.  將資料轉換成指定的型別*TargetType*中**SQLBindCol**。  
  
4.  如果資料已轉換成可變長度資料類型，例如字元或二進位**SQLFetch**會檢查資料的長度是否超過資料緩衝區的長度。 如果字元資料 （包括 null 結束字元） 的長度超過資料緩衝區的長度**SQLFetch**截斷的資料為 null 結束字元的長度小於資料緩衝區的長度。 它接著 null 終止的資料。 如果二進位資料的長度超過資料緩衝區的長度**SQLFetch**截斷的資料緩衝區的長度。 指定資料緩衝區的長度*Columnsize*中**SQLBindCol**。  
  
     **SQLFetch**永遠不會截斷轉換為固定長度資料類型的資料，它一律會假設資料緩衝區的長度是資料類型的大小。  
  
5.  將資料緩衝區中的轉換 （和可能已截斷） 資料。 如何判斷資料緩衝區的位址的相關資訊，請參閱 「 緩衝區位址 」，在[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
6.  置於長度/指標緩衝區中資料的長度。 如果指標的指標和長度指標兩者都設定為相同的緩衝區 (為呼叫**SQLBindCol**沒有)，長度會寫入有效的資料緩衝區中，而 SQL_NULL_DATA 以 NULL 資料的緩衝區。 如果沒有長度/指標緩衝區已繫結， **SQLFetch**不會傳回長度。  
  
    -   針對字元或二進位資料，這是資料的長度轉換之後，以及之前截斷因為太小的資料緩衝區。 如果驅動程式無法在轉換之後，判斷資料的長度，因為有時候是 long 資料的情況，它會將長度設定為 SQL_NO_TOTAL 中。 資料已截斷因為 SQL_ATTR_MAX_LENGTH 陳述式屬性，此屬性的值會放入長度/指標緩衝區，而不是實際的長度。 這是因為這個屬性是會截斷轉換之前, 在伺服器上的資料，讓驅動程式有沒有辦法找出實際的長度為何。  
  
    -   對於所有其他資料類型，這是在轉換後資料的長度也就是說，它是已轉換的目標資料類型的大小。  
  
     如何判斷長度/指標緩衝區的位址的相關資訊，請參閱 「 緩衝區位址 」，在[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
7.  如果資料在轉換時截斷而不會遺失有效位數 （比方說，實數 1.234 會截斷為整數 1 轉換時，） **SQLFetch**傳回 SQLSTATE 01S07 （小數位數截斷） 和 SQL_SUCCESS_WITH_INFO。 如果資料遭到截斷，因為資料緩衝區的長度太小 （例如，字串"abcdef"會放在 4 個位元組的緩衝區，） **SQLFetch**傳回 SQLSTATE 01004 （資料已截斷） 和 SQL_SUCCESS_WITH_INFO。 如果資料遭到截斷 SQL_ATTR_MAX_LENGTH 陳述式屬性，因為**SQLFetch**都會傳回 SQL_SUCCESS，且沒有傳回 SQLSTATE 01S07 （小數位數截斷） 或 SQLSTATE 01004 （資料已截斷）。 如果資料在轉換時截斷遺失 （例如，如果大於 100000 的 SQL_INTEGER 已轉換成 SQL_C_TINYINT），有效位數**SQLFetch**傳回 SQLSTATE 22003 （數值超出範圍）和 （如果資料列集大小為 1） 的 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO （如果資料列集大小大於 1 時）。  
  
 如果未定義的繫結的資料緩衝區和長度/指標緩衝區的內容，則**SQLFetch**或是**SQLFetchScroll**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 資料列狀態陣列用來傳回資料列集中的每個資料列的狀態。 這個陣列的位址會指定 sql_attr_row_status_ptr 設定陳述式屬性。 陣列由應用程式所配置，而且必須具有 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性所指定的項目數。 會設定其值**SQLFetch**， **SQLFetchScroll**，並**SQLBulkOperations**或是**SQLSetPos** （除外，它們已被呼叫時資料指標具有已依定位後**SQLExtendedFetch**)。 如果 sql_attr_row_status_ptr 設定陳述式屬性的值是 null 指標，則這些函式將不會傳回資料列狀態。  
  
 如果未定義的資料列狀態陣列緩衝區的內容，則**SQLFetch**或是**SQLFetchScroll**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 在 資料列狀態陣列，會傳回下列的值。  
  
|資料列狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|資料列已成功擷取，而且尚未變更，因為它一次擷取此結果集。|  
|SQL_ROW_SUCCESS_WITH_INFO|資料列已成功擷取，而且尚未變更，因為它一次擷取此結果集。 不過，資料列相關的已傳回警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED [1]，[2]，和 [3]|資料列已順利擷取和已變更，因為它一次擷取此結果集。 如果從這個結果集一次提取或重新整理的資料列**SQLSetPos**，狀態會變更為資料列的新狀態。|  
|SQL_ROW_DELETED[3]|資料列已經刪除，因為它一次擷取此結果集。|  
|SQL_ROW_ADDED[4]|已插入資料列**SQLBulkOperations**。 如果從這個結果集一次提取或重新整理的資料列**SQLSetPos**，其狀態會是 SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|重疊的資料列集結果集的結尾，並傳回任何資料列，對應至資料列狀態陣列的這個項目。|  
  
 [1] 的索引鍵集，混合式和動態資料指標，如果更新金鑰的值時，資料的資料列會被視為已被刪除，並加入新的資料列。  
  
 [2] 有些驅動程式無法偵測更新的資料，且無法傳回此值。 若要判斷驅動程式是否可以偵測 refetched 的資料列更新，應用程式會呼叫**SQLGetInfo** SQL_ROW_UPDATES 選項。  
  
 [3] **SQLFetch**可以傳回此值，只有當它是混合使用呼叫**SQLFetchScroll**。 這是因為**SQLFetch**通過結果集，並以獨佔方式使用，不會不重新擷取任何資料列。 沒有任何資料列 refetched，因為**SQLFetch**不會偵測先前擷取的資料列所做的變更。 不過，如果**SQLFetchScroll**任何先前擷取的資料列之前，將游標置於並**SQLFetch**用來擷取這些資料列**SQLFetch**可以偵測到的任何變更這些資料列。  
  
 [4] 所傳回 SQLBulkOperations 只。 未設定**SQLFetch**或是**SQLFetchScroll**。  
  
### <a name="rows-fetched-buffer"></a>擷取緩衝區資料列。  
 擷取緩衝區的資料列用來傳回的資料列的提取，包括任何資料，傳回因為發生錯誤時所要擷取的資料列數目。 換句話說，它是其中的資料列狀態陣列中的值不是 SQL_ROW_NOROW 的資料列數目。 這個緩衝區的位址會指定 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性。 應用程式所配置的緩衝區。 它由設定**SQLFetch**並**SQLFetchScroll**。 如果 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性的值是 null 指標，則這些函式將不會傳回擷取的資料列數目。 若要判斷目前在結果集中的資料列數目，應用程式可以呼叫**SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 屬性。  
  
 如果擷取的資料列緩衝區的內容為未定義**SQLFetch**或是**SQLFetchScroll**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA 傳回時，在此情況下除外在提取緩衝區資料列中的值設定為 0。  
  
### <a name="error-handling"></a>錯誤處理  
 錯誤和警告可以套用至個別資料列或整個函式。 如需診斷記錄的詳細資訊，請參閱[診斷](../../../odbc/reference/develop-app/diagnostics.md)並[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>錯誤和警告，在整個函式  
 如果錯誤會套用至整個函式，例如 SQLSTATE HYT00 （過期的逾時） 或 SQLSTATE 24000 （無效的資料指標狀態）， **SQLFetch**傳回 SQL_ERROR，而且適用的 SQLSTATE。 是未定義的資料列集緩衝區的內容和資料指標位置會變更。  
  
 如果整個函式，適用於警告**SQLFetch**傳回 SQL_SUCCESS_WITH_INFO 和適用的 SQLSTATE。 適用於個別的資料列的狀態記錄之前，會傳回狀態記錄套用至整個函式的警告。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>錯誤和警告中個別資料列  
 如果發生錯誤 （例如 SQLSTATE 22012 （以零進行除法）) 或警告 （例如 SQLSTATE 01004 （資料已截斷）) 會套用至單一的資料列中， **SQLFetch**會進行下列作業：  
  
-   設定資料列狀態陣列的對應項目至 SQL_ROW_ERROR 錯誤或 SQL_ROW_SUCCESS_WITH_INFO 的警告。  
  
-   新增包含 Sqlstate 錯誤或警告的零或多個狀態記錄。  
  
-   狀態記錄中設定的資料列和資料行的數字欄位。 如果**SQLFetch**無法判斷資料列或資料行的數目，將該數字設 SQL_ROW_NUMBER_UNKNOWN 或 SQL_COLUMN_NUMBER_UNKNOWN，分別。 狀態記錄不會套用到特定的資料行中，如果**SQLFetch** SQL_NO_COLUMN_NUMBER 設定資料行數目。  
  
 **SQLFetch**繼續提取資料列，直到它提取資料列集中的所有資料列。 它會傳回 SQL_SUCCESS_WITH_INFO，除非發生錯誤時 （不含資料列狀態 SQL_ROW_NOROW） 資料列集，每個資料列在此情況下會傳回 SQL_ERROR。 特別是，如果資料列集大小為 1，而且該資料列中發生錯誤**SQLFetch**會傳回 SQL_ERROR。  
  
 **SQLFetch**狀態記錄的順序傳回資料列數目。 也就是說，它會傳回未知的資料列 （如果有的話）; 的所有狀態記錄接下來它會傳回第一個資料列 （如果有的話），所有的狀態記錄，然後它會傳回所有的狀態記錄，第二個資料列 （如果有的話），依此類推。 根據一般的規則來排序狀態記錄; 排序每個資料列的狀態記錄如需詳細資訊，請參閱 「 順序的狀態的記錄 」 中[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
### <a name="descriptors-and-sqlfetch"></a>描述項和 SQLFetch  
 下列各節說明如何**SQLFetch**描述項進行互動。  
  
#### <a name="argument-mappings"></a>引數對應  
 驅動程式不會設定任何基礎的引數的描述項欄位**SQLFetch**。  
  
#### <a name="other-descriptor-fields"></a>其他描述項欄位  
 下列的描述項欄位由**SQLFetch**。  
  
|描述項欄位|Desc。|中的欄位|透過設定|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|標頭|SQL_ATTR_ROW_ARRAY_SIZE statement attribute|  
|SQL_DESC_ARRAY_STATUS_PTR|IRD|標頭|Sql_attr_row_status_ptr 設定陳述式屬性|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|標頭|SQL_ATTR_ROW_BIND_OFFSET_PTR statement attribute|  
|SQL_DESC_BIND_TYPE|ARD|標頭|SQL_ATTR_ROW_BIND_TYPE statement attribute|  
|SQL_DESC_COUNT|ARD|標頭|*ColumnNumber*引數**SQLBindCol**|  
|SQL_DESC_DATA_PTR|ARD|記錄|*TargetValuePtr*引數**SQLBindCol**|  
|SQL_DESC_INDICATOR_PTR|ARD|記錄|*StrLen_or_IndPtr*中的引數**SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH|ARD|記錄|*BufferLength*中的引數**SQLBindCol**|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|記錄|*StrLen_or_IndPtr*中的引數**SQLBindCol**|  
|SQL_DESC_ROWS_PROCESSED_PTR|IRD|標頭|SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性|  
|SQL_DESC_TYPE|ARD|記錄|*TargetType*中的引數**SQLBindCol**|  
  
 您也可以透過設定所有的描述項欄位**SQLSetDescField**。  
  
#### <a name="separate-length-and-indicator-buffers"></a>個別的長度和指標緩衝區  
 應用程式可以繫結，單一緩衝區或兩個個別的緩衝區可保留長度與指標值。 當應用程式呼叫**SQLBindCol**，驅動程式設定的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 欄位 ARD 到相同的位址會傳入*StrLen_or_IndPtr*引數。 當應用程式呼叫**SQLSetDescField**或是**SQLSetDescRec**，它可以將這兩個欄位設定為不同的位址。  
  
 **SQLFetch**判斷應用程式是否已指定個別的長度和指標緩衝區。 在此情況下，當資料不是 NULL， **SQLFetch**將設為 0 的指標緩衝區和長度的緩衝區中傳回的長度。 當資料為 NULL， **SQLFetch**指標緩衝區設定為 SQL_NULL_DATA，並不會修改長度的緩衝區。  
  
### <a name="code-example"></a>程式碼範例  
 請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)， [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)， [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)，以及[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)。  
  
### <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在結果集中傳回資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|關閉資料指標陳述式上|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|正在擷取部分或全部的資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集資料行|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
