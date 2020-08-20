---
description: SQLFetch 函式
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
ms.openlocfilehash: f13aabcf19968873683bf12bcde5bb006422e260
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476096"
---
# <a name="sqlfetch-function"></a>SQLFetch 函式
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLFetch** 會從結果集中提取下一個資料列集，並傳回所有系結資料行的資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetch**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫[SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)函式（ *HandleType*為 SQL_HANDLE_STMT 和*StatementHandle*的*控制碼*）來取得相關聯的 SQLSTATE 值。 下表列出 **SQLFetch** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。 如果在單一資料行上發生錯誤，則可以使用 SQL_DIAG_COLUMN_NUMBER 的*以*來呼叫[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md) ，以判斷發生錯誤的資料行;您可以使用 SQL_DIAG_ROW_NUMBER 的*以*來呼叫和**SQLGetDiagField** ，以判斷包含該資料行的資料列。  
  
 對於可以傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR (（除了 01xxx SQLSTATEs) 以外）的所有 SQLSTATEs，如果一或多個（但不是全部）多資料列作業的資料列發生錯誤，則會傳回 SQL_SUCCESS_WITH_INFO，如果單一資料列作業發生錯誤，則會傳回 SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|針對資料行傳回的字串或二進位資料會截斷非空白字元或非 Null 的二進位資料。 如果是字串值，就會以正確的方式截斷。|  
|01S01|資料列發生錯誤|提取一或多個資料列時發生錯誤。<br /><br />  (如果 ODBC 3.x 應用程式正在使用 ODBC 2.x*驅動程式時*傳回這個 SQLSTATE，則可以 *.x*忽略它。 ) |  
|01S07|小數截斷|為數據行傳回的資料已截斷。 若為數值資料類型，則會截斷數位的小數部分。 針對包含時間元件的時間、時間戳記和間隔資料類型，時間的小數部分會被截斷。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|在結果集中，資料行的資料值無法轉換成**SQLBindCol**中*TargetType*所指定的資料類型。<br /><br /> 資料行0系結了 SQL_C_BOOKMARK 的資料類型，且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE。<br /><br /> 資料行0系結了 SQL_C_VARBOOKMARK 的資料類型，且 SQL_ATTR_USE_BOOKMARKS 語句屬性未設定為 SQL_UB_VARIABLE。|  
|07009|描述元索引無效|驅動*程式是 ODBC 2.x 驅動程式* ，不支援 **SQLExtendedFetch**，而且資料行的系結中指定的資料行編號為0。<br /><br /> 已系結資料行0，且 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊已截斷|為數據行傳回的可變長度書簽已被截斷。|  
|22002|需要指標變數，但未提供|Null 資料已提取至資料**行，而**該資料行的*StrLen_or_IndPtr* SQL_DESC_INDICATOR_PTR (由**SQLSetDescField**或**SQLSetDescRec**) 設定的資料行（null 指標）。|  
|22003|數值超出範圍|將數值或字串傳回為一個或多個系結資料行的數值或字串，可能會導致整個 (，而不是小數) 部分要截斷的數位。<br /><br /> 如需詳細資訊，請參閱附錄 D：資料類型中的 [將資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) 。|  
|22007|不正確日期時間格式|結果集中的字元資料行系結至日期、時間或時間戳記 C 結構，而資料行中的值分別是不正確日期、時間或時間戳記。|  
|22012|零除|傳回算術運算式的值，導致零除。|  
|22015|間隔欄位溢位|從確切數值或間隔 SQL 類型指派至間隔 C 類型，會導致在前置欄位中遺失有效位數。<br /><br /> 將資料提取到間隔 C 類型時，間隔 C 類型中沒有 SQL 類型的值表示。|  
|22018|轉換規格的字元值無效|結果集中的字元資料行已系結至字元 C 緩衝區，而資料行包含的字元沒有在緩衝區的字元集中表示。<br /><br /> C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;且資料行中的值不是系結 C 類型的有效常值。|  
|24000|指標狀態無效|*StatementHandle*處於執行中狀態，但沒有與*StatementHandle*相關聯的結果集。|  
|40001|序列化失敗|執行提取的交易已終止，以防止鎖死。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫**SQLFetch**函式，並在它完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後，在*StatementHandle*上再次呼叫**SQLFetch**函數。<br /><br /> 或者，呼叫**SQLFetch**函式，並在它完成執行之前，從多執行緒應用程式中的不同執行緒呼叫*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLFetch** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 指定的 *StatementHandle* 未處於執行中狀態。 在未先呼叫 **SQLExecDirect**、 **SQLExecute** 或 catalog 函數的情況下呼叫函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br /> 在呼叫**SQLExtendedFetch**之後，以及呼叫 SQL_CLOSE 選項**SQLFreeStmt**之前，會呼叫*StatementHandle*的 (DM) **SQLFetch** 。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度|SQL_ATTR_USE_BOOKMARK 語句屬性已設定為 SQL_UB_VARIABLE，而且資料行0系結至長度不等於此結果集之書簽長度上限的緩衝區。  (此長度可在 IRD 的 [SQL_DESC_OCTET_LENGTH] 欄位中取得，而且可以藉由呼叫 **SQLDescribeCol**、 **SQLColAttribute**或 **SQLGetDescField**來取得。 ) |  
|HY107|資料列值超出範圍|已 SQL_CURSOR_KEYSET_DRIVEN 使用 SQL_ATTR_CURSOR_TYPE 語句屬性指定的值，但以 SQL_ATTR_KEYSET_SIZE 語句屬性指定的值大於0，且小於 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性指定的值。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*組合所指定的轉換，以及對應資料行的 SQL 資料類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回要求的結果集之前過期。 Timeout 期限是透過 SQLSetStmtAttr、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 **SQLFetch** 會傳回結果集中的下一個資料列集。 只有在結果集存在時，才可以呼叫它：亦即，在建立結果集的呼叫之後，以及在該結果集上的資料指標結束之前。 如果有系結的資料行，則會傳回這些資料行中的資料。 如果應用程式已指定資料列狀態陣列的指標，或是要傳回所提取資料列數的緩衝區，則 **SQLFetch** 也會傳回這項資訊。 對 **SQLFetch** 的呼叫可以與 **SQLFetchScroll** 的呼叫混合，但無法與 **SQLExtendedFetch**的呼叫混合。 如需詳細資訊，請參閱 [提取資料列](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC 3.x 應用程式搭配 ODBC 2.x 驅動程式使用，驅動程式管理員 *.x*會將**SQLFetch**呼叫對應至支援**SQLExtendedFetch**的 odbc*2.x 驅動程式* **SQLExtendedFetch** 。* * 如果 ODBC 2.x 驅動程式不支援**SQLExtendedFetch**，驅動程式管理員會將**SQLFetch**呼叫對應到 ODBC*2.X 驅動程式*中的**SQLFetch** ，*此驅動程式*只能提取單一資料列。  
  
 如需詳細資訊，請參閱附錄 G：提供回溯相容性之驅動程式指導方針中的 [區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 。  
  
## <a name="positioning-the-cursor"></a>定位游標  
 當建立結果集時，資料指標會位於結果集的開頭之前。 **SQLFetch** 會提取下一個資料列集。 這相當於呼叫 **SQLFetchScroll** ，並將 *FetchOrientation* 設定為 SQL_FETCH_NEXT。 如需資料指標的詳細資訊，請參閱資料[指標和](../../../odbc/reference/develop-app/cursors.md)[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性指定資料列集中的資料列數目。 如果 **SQLFetch** 所提取的資料列集與結果集的結尾重迭，則 **SQLFetch** 會傳回部分資料列集。 也就是說，如果 S + R-1 大於 L，其中 S 是要提取之資料列集的起始資料列，R 是資料列集大小，而 L 是結果集中的最後一個資料列，則只有資料列集的第一個 L-S + 1 個數據列是有效的。 其餘的資料列是空的，且狀態為 SQL_ROW_NOROW。  
  
 **SQLFetch**傳回之後，目前的資料列是資料列集的第一個資料列。  
  
 下表所列的規則會根據本節第二個表格中所列的條件，說明在呼叫 **SQLFetch**之後的資料指標定位。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|開始之前|1|  
|*CurrRowsetStart* \< CurrRowsetStart = *LastResultRow-RowsetSize*[1]|*CurrRowsetStart*  + *RowsetSize*[2]|  
|*CurrRowsetStart*  > *LastResultRow-RowsetSize*[1]|結束後|  
|結束後|結束後|  
  
 [1] 如果在提取之間變更資料列集大小，這就是與先前的提取搭配使用的資料列集大小。  
  
 [2] 如果在提取之間變更資料列集大小，這就是與新提取搭配使用的資料列集大小。  
  
|表示法|意義|  
|--------------|-------------|  
|開始之前|區塊資料指標位於結果集的開頭之前。 如果新資料列集的第一個資料列在結果集的開頭之前， **SQLFetch** 會傳回 SQL_NO_DATA。|  
|結束後|區塊資料指標位於結果集的結尾之後。 如果新資料列集的第一個資料列位於結果集的結尾， **SQLFetch** 會傳回 SQL_NO_DATA。|  
|*CurrRowsetStart*|目前資料列集中第一個資料列的編號。|  
|*LastResultRow*|結果集中最後一個資料列的編號。|  
|*RowsetSize*|資料列集大小。|  
  
 例如，假設結果集的資料列是100，且資料列集大小為5。 下表顯示 **SQLFetch** 針對不同開始位置所傳回的資料列集和傳回碼。  
  
|目前的資料列集|傳回碼|新的資料列集|提取的資料列數目|  
|--------------------|-----------------|----------------|------------------------|  
|開始之前|SQL_SUCCESS|1至5|5|  
|1至5|SQL_SUCCESS|6到10|5|  
|52至56|SQL_SUCCESS|57至61|5|  
|91至95|SQL_SUCCESS|96至100|5|  
|93至97|SQL_SUCCESS|98到100。 資料列狀態陣列的資料列4和5會設定為 SQL_ROW_NOROW。|3|  
|96至100|SQL_NO_DATA|無。|0|  
|99至100|SQL_NO_DATA|無。|0|  
|結束後|SQL_NO_DATA|無。|0|  
  
## <a name="returning-data-in-bound-columns"></a>傳回系結資料行中的資料  
 當 **SQLFetch** 傳回每個資料列時，它會將緩衝區中每個系結資料行的資料放入該資料行。 如果沒有系結的資料行， **SQLFetch** 就不會傳回任何資料，而是會將區塊資料指標往前移動。 您仍可使用 **SQLGetData**來取出資料。 如果資料指標是多資料列的資料指標 (也就是，SQL_ATTR_ROW_ARRAY_SIZE 大於 1) ，則只有當以 SQL_GETDATA_EXTENSIONS *InfoType*呼叫**SQLGetInfo**時，SQL_GD_BLOCK 才會呼叫**SQLGetData** 。  (需詳細資訊，請參閱 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。 )   
  
 針對資料列中的每個系結資料行， **SQLFetch** 會執行下列動作：  
  
1.  設定要 SQL_Null_DATA 的長度/指標緩衝區，並在資料為 Null 時繼續進行下一個資料行。 如果資料為 Null，而且未系結任何長度/指標緩衝區， **SQLFetch** 會傳回所需的 SQLSTATE 22002 (指標變數，但不會為數據列提供) ，然後繼續進行下一個資料列。 如需如何判斷長度/指標緩衝區位址的詳細資訊，請參閱 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
     如果資料行的資料不是 Null，則 **SQLFetch** 會繼續進行步驟2。  
  
2.  如果 SQL_ATTR_MAX_LENGTH 語句屬性設定為非零值，且資料行包含字元或二進位資料，則資料會被截斷為 SQL_ATTR_MAX_LENGTH 個位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 語句屬性的目的是要減少網路流量。 它通常是由資料來源所執行，這會在透過網路傳回資料之前截斷資料。 驅動程式和資料來源不需要支援。 因此，為了確保資料會被截斷為特定大小，應用程式應配置該大小的緩衝區，並在**SQLBindCol**中指定*cbValueMax*引數的大小。  
  
3.  將資料轉換為**SQLBindCol**中*TargetType*所指定的型別。  
  
4.  如果資料轉換成可變長度的資料類型（例如字元或二進位）， **SQLFetch** 會檢查資料的長度是否超過資料緩衝區的長度。 如果字元資料的長度 (包括 null 終止字元) 超過資料緩衝區的長度， **SQLFetch** 就會將資料截斷為資料緩衝區的長度，而不是 null 終止字元的長度。 然後，它會以 null 結束資料。 如果二進位資料的長度超過資料緩衝區的長度， **SQLFetch** 會將它截斷為資料緩衝區的長度。 資料緩衝區的長度是以**SQLBindCol**中的*BufferLength*指定。  
  
     **SQLFetch** 絕對不會截斷轉換成固定長度資料類型的資料;它一律會假設資料緩衝區的長度是資料類型的大小。  
  
5.  將已轉換的 (以及可能截斷的) 資料放入資料緩衝區。 如需有關如何判斷資料緩衝區位址的詳細資訊，請參閱 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
6.  將資料的長度放在長度/指標緩衝區中。 如果指標指標和長度指標都設為相同的緩衝區 (當呼叫 **SQLBindCol** 確實) 時，長度會寫入緩衝區中以取得有效的資料，並將 SQL_Null_DATA 寫入緩衝區以取得 Null 資料。 如果未系結任何長度/指標緩衝區， **SQLFetch** 就不會傳回長度。  
  
    -   若為字元或二進位資料，這是轉換後以及截斷之前的資料長度，因為資料緩衝區太小。 如果驅動程式無法在轉換後判斷資料的長度，有時會有 long 資料的情況，它會將長度設定為 SQL_NO_TOTAL。 如果因為 SQL_ATTR_MAX_LENGTH 語句屬性而截斷資料，這個屬性的值會放在長度/指標緩衝區，而不是實際的長度。 這是因為這個屬性是設計用來在轉換之前截斷伺服器上的資料，因此驅動程式無法找出實際的長度。  
  
    -   對於所有其他資料類型，這是轉換後的資料長度;也就是說，它是轉換資料的類型大小。  
  
     如需如何判斷長度/指標緩衝區位址的詳細資訊，請參閱 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
7.  如果在轉換期間截斷資料，而不會遺失有效位數 (例如，在轉換) 時，會將實數1.234 截斷為整數1， **SQLFetch** 會傳回 SQLSTATE 01S07 (小數截斷) 和 SQL_SUCCESS_WITH_INFO。 如果因為資料緩衝區的長度太小而截斷資料 (例如，字串 "abcdef" 會放在4位元組的緩衝區) 中， **SQLFetch** 會傳回 SQLSTATE 01004 (資料截斷) 和 SQL_SUCCESS_WITH_INFO。 如果因為 SQL_ATTR_MAX_LENGTH 語句屬性而截斷資料， **SQLFetch** 會傳回 SQL_SUCCESS，而不會傳回 SQLSTATE 01S07 (小數截斷) 或 SQLSTATE 01004 (資料被截斷) 。 如果資料在轉換期間因為遺失有效位數而被截斷 (例如，如果大於100000的 SQL_INTEGER 值已轉換成 SQL_C_TINYINT) ， **SQLFetch** 會傳回 SQLSTATE 22003 (數值超出範圍) ，SQL_ERROR 如果資料列集大小大於 1 (，則會傳回) SQL_SUCCESS_WITH_INFO。  
  
 如果 **SQLFetch** 或 **SQLFetchScroll** 沒有傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，系結資料緩衝區的內容和長度/指標緩衝區都是未定義的。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 資料列狀態陣列用來傳回資料列集中每個資料列的狀態。 這個陣列的位址是使用 SQL_ATTR_ROW_STATUS_PTR 語句屬性來指定。 陣列是由應用程式所配置，而且必須擁有 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性所指定的多個元素。 它的值是由 **SQLFetch**、 **SQLFetchScroll**和 **SQLBulkOperations** 或 **SQLSetPos** 所設定 (除非是在資料指標由 **SQLExtendedFetch**) 定位之後被呼叫。 如果 SQL_ATTR_ROW_STATUS_PTR 語句屬性的值為 null 指標，則這些函數不會傳回資料列狀態。  
  
 如果 **SQLFetch** 或 **SQLFetchScroll** 沒有傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，資料列狀態陣列緩衝區的內容會是未定義的。  
  
 下列值會在資料列狀態陣列中傳回。  
  
|資料列狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|資料列已成功提取，且自上次從這個結果集提取以來尚未變更。|  
|SQL_ROW_SUCCESS_WITH_INFO|資料列已成功提取，且自上次從這個結果集提取以來尚未變更。 但是，傳回有關資料列的警告。|  
|SQL_ROW_ERROR|提取資料列時發生錯誤。|  
|SQL_ROW_UPDATED [1]、[2] 和 [3]|資料列已成功提取，且自上次從這個結果集提取以來已變更。 如果此資料列是從這個結果集再次提取，或是由 **SQLSetPos**重新整理，則狀態會變更為資料列的新狀態。|  
|SQL_ROW_DELETED [3]|已刪除資料列，因為它上次從這個結果集提取。|  
|SQL_ROW_ADDED [4]|**SQLBulkOperations**插入資料列。 如果從這個結果集提取資料列，或由 **SQLSetPos**重新整理，其狀態會是 SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|資料列集重迭了結果集的結尾，而且沒有傳回任何資料列來對應至資料列狀態陣列的這個元素。|  
  
 [1] 針對索引鍵集、混合和動態資料指標，如果索引鍵值已更新，則會將資料列視為已刪除，並加入新的資料列。  
  
 [2] 某些驅動程式無法偵測到資料的更新，因此無法傳回此值。 為了判斷驅動程式是否可以偵測根據資料列的更新，應用程式會使用 SQL_ROW_UPDATES 選項來呼叫 **SQLGetInfo** 。  
  
 [3]   **SQLFetch** 只有在與 **SQLFetchScroll**的呼叫混合時，才會傳回此值。 這是因為 **SQLFetch** 會向前移動結果集，而且如果是以獨佔方式使用，就不會重新擷取任何資料列。 因為不會根據任何資料列，所以 **SQLFetch** 不會偵測先前提取的資料列所做的變更。 但是，如果 **SQLFetchScroll** 在任何先前提取的資料列之前放置資料指標，並使用 **SQLFetch** 來提取這些資料列，則 **SQLFetch** 可以偵測到那些資料列的任何變更。  
  
 只有 SQLBulkOperations 傳回 [4]。 未由 **SQLFetch** 或 **SQLFetchScroll**設定。  
  
### <a name="rows-fetched-buffer"></a>提取的資料列緩衝區  
 提取的資料列會用來傳回所提取的資料列數目，包括未傳回任何資料的資料列，因為它們被提取時發生錯誤。 換句話說，它是資料列狀態陣列中不 SQL_ROW_NOROW 值的資料列數目。 使用 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性指定這個緩衝區的位址。 緩衝區是由應用程式所配置。 它是由 **SQLFetch** 和 **SQLFetchScroll**設定。 如果 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性的值是 null 指標，這些函式不會傳回提取的資料列數目。 若要判斷結果集中目前資料列的數目，應用程式可以使用 SQL_ATTR_ROW_NUMBER 屬性來呼叫 **SQLGetStmtAttr** 。  
  
 如果 **SQLFetch** 或 **SQLFetchScroll** 沒有傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，除非傳回 SQL_NO_DATA，在這種情況下，資料列提取緩衝區中的值會設定為0，否則資料列的資料列內容會是未定義的。  
  
### <a name="error-handling"></a>錯誤處理  
 錯誤和警告可套用至個別的資料列或整個函數。 如需診斷記錄的詳細資訊，請參閱 [診斷](../../../odbc/reference/develop-app/diagnostics.md) 和 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>整個函數的錯誤和警告  
 如果錯誤適用于整個函數，例如 SQLSTATE HYT00 (Timeout 過期) 或 SQLSTATE 24000 (不正確資料指標狀態) ，則 **SQLFetch** 會傳回 SQL_ERROR 和適用的 SQLSTATE。 資料列集緩衝區的內容是未定義的，而且資料指標的位置沒有變更。  
  
 如果將警告套用至整個函數， **SQLFetch** 會傳回 SQL_SUCCESS_WITH_INFO 以及適用的 SQLSTATE。 適用于整個函數之警告的狀態記錄，會在套用至個別資料列的狀態記錄之前傳回。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>個別資料列中的錯誤和警告  
 如果錯誤 (例如 SQLSTATE 22012 (除數為零) # A3 或警告 (例如 SQLSTATE 01004 (資料被截斷) # A7 套用至單一資料列， **SQLFetch**會執行下列動作：  
  
-   設定資料列狀態陣列的對應元素，以 SQL_ROW_ERROR 錯誤或 SQL_ROW_SUCCESS_WITH_INFO 的警告。  
  
-   新增包含錯誤或警告之 SQLSTATEs 的零或多個狀態記錄。  
  
-   設定狀態記錄中的資料列和資料行編號欄位。 如果 **SQLFetch** 無法判斷資料列或資料行編號，則會分別將該數位設定為 SQL_ROW_NUMBER_UNKNOWN 或 SQL_COLUMN_NUMBER_UNKNOWN。 如果狀態記錄未套用至特定資料行， **SQLFetch** 會將資料行編號設定為 SQL_NO_COLUMN_NUMBER。  
  
 **SQLFetch** 會繼續提取資料列，直到提取資料列集中的所有資料列為止。 除非資料列集的每個資料列中發生錯誤，否則會傳回 SQL_SUCCESS_WITH_INFO (不包含狀態 SQL_ROW_NOROW) 的資料列，在這種情況下，它會傳回 SQL_ERROR。 尤其是，如果資料列集大小為1，且該資料列中發生錯誤，則 **SQLFetch** 會傳回 SQL_ERROR。  
  
 **SQLFetch** 會以資料列編號順序傳回狀態記錄。 也就是說，它會傳回未知資料列的所有狀態記錄 (如果有任何) ;接著，它會傳回第一個資料列的所有狀態記錄 (如果有任何) ，然後它會傳回第二個數據列的所有狀態記錄 (如果有任何) 等等。 每個資料列的狀態記錄都會根據排序狀態記錄的一般規則來排序;如需詳細資訊，請參閱 [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)中的「狀態記錄的順序」。  
  
### <a name="descriptors-and-sqlfetch"></a>描述項和 SQLFetch  
 下列各節描述 **SQLFetch** 與描述項的互動方式。  
  
#### <a name="argument-mappings"></a>引數對應  
 驅動程式不會根據 **SQLFetch**的引數來設定任何描述項欄位。  
  
#### <a name="other-descriptor-fields"></a>其他描述項欄位  
 **SQLFetch**會使用下列描述項欄位。  
  
|描述項欄位|Desc.|欄位|設定為|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|ARD|header|SQL_ATTR_ROW_ARRAY_SIZE 語句屬性|  
|SQL_DESC_ARRAY_STATUS_PTR|稅務局|header|SQL_ATTR_ROW_STATUS_PTR 語句屬性|  
|SQL_DESC_BIND_OFFSET_PTR|ARD|header|SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性|  
|SQL_DESC_BIND_TYPE|ARD|header|SQL_ATTR_ROW_BIND_TYPE 語句屬性|  
|SQL_DESC_COUNT|ARD|header|**SQLBindCol**的*ColumnNumber*引數|  
|SQL_DESC_DATA_PTR|ARD|記錄|**SQLBindCol**的*TargetValuePtr*引數|  
|SQL_DESC_INDICATOR_PTR|ARD|記錄|**SQLBindCol**中的*StrLen_or_IndPtr*引數|  
|SQL_DESC_OCTET_LENGTH|ARD|記錄|**SQLBindCol**中的*BufferLength*引數|  
|SQL_DESC_OCTET_LENGTH_PTR|ARD|記錄|**SQLBindCol**中的*StrLen_or_IndPtr*引數|  
|SQL_DESC_ROWS_PROCESSED_PTR|稅務局|header|SQL_ATTR_ROWS_FETCHED_PTR 語句屬性|  
|SQL_DESC_TYPE|ARD|記錄|**SQLBindCol**中的*TargetType*引數|  
  
 所有描述項欄位也都可以透過 **SQLSetDescField**設定。  
  
#### <a name="separate-length-and-indicator-buffers"></a>分隔長度和指標緩衝區  
 應用程式可以系結單一緩衝區或兩個不同的緩衝區，以用來保存長度和指標值。 當應用程式呼叫 **SQLBindCol**時，驅動程式會將 ARD 的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 欄位設定為在 *StrLen_or_IndPtr* 引數中傳遞的相同位址。 當應用程式呼叫 **SQLSetDescField** 或 **SQLSetDescRec**時，可以將這兩個欄位設定為不同的位址。  
  
 **SQLFetch** 會判斷應用程式是否已指定個別的長度和指標緩衝區。 在此情況下，當資料不是 Null 時， **SQLFetch** 會將指標緩衝區設定為0，並傳回長度緩衝區的長度。 當資料為 Null 時， **SQLFetch** 會將指標緩衝區設定為 SQL_Null_DATA，且不會修改長度緩衝區。  
  
### <a name="code-example"></a>程式碼範例  
 請參閱 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)、 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)、 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)和 [SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)。  
  
### <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|關閉語句上的資料指標|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|提取部分或全部資料行|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備要執行的語句|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
