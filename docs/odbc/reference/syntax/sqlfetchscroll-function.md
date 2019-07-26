---
title: SQLFetchScroll 函式 |Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb75ebceb1f70ddc8b517a3dc94af97a18965939
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345188"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 函數
**標準**  
 引進的版本:ODBC 3.0 標準合規性:ISO 92  
  
 **摘要**  
 **SQLFetchScroll**會從結果集提取指定的資料列集, 並傳回所有系結資料行的資料。 資料列集可以在絕對或相對位置或依書簽指定。  
  
 使用 ODBC 2.x 驅動程式時, 驅動程式管理員會將此函數對應至**SQLExtendedFetch**。 如需詳細資訊, 請參閱對應取代函式[以取得應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *FetchOrientation*  
 源  
  
 Fetch 的類型:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 如需詳細資訊, 請參閱「批註」一節中的「定位游標」。  
  
 *FetchOffset*  
 源  
  
 要提取的資料列數目。 這個引數的解讀取決於*FetchOrientation*引數的值。 如需詳細資訊, 請參閱「批註」一節中的「定位游標」。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetchScroll**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時, 可以藉由呼叫 SQLGetDiagRec 和 HandleType 的 Handletype 來  和 StatementHandle 的控制碼來取得相關聯的 SQLSTATE 值。 下表列出**SQLFetchScroll**常傳回的 SQLSTATE 值, 並在此函式的內容中說明每一個值;「(DM)」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明, 否則, 與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。 如果單一資料行發生錯誤, 則可以使用 SQL_DIAG_COLUMN_NUMBER 的以來呼叫**SQLGetDiagField** , 以判斷發生錯誤的資料行;您可以使用 SQL_DIAG_ROW_NUMBER 的以來呼叫和**SQLGetDiagField** , 以判斷包含該資料行的資料列。  
  
 對於可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR 的所有 SQLSTATEs (01xxx SQLSTATEs 除外), 如果一或多個 (但非全部) SQL_SUCCESS_WITH_INFO 作業的資料列發生錯誤, 則會傳回多資料列, 如果發生錯誤, 則會傳回 SQL_ERROR單一資料列作業。  
  
|SQLSTATE|Error|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01004|字串資料, 右邊已截斷|傳回資料行的字串或二進位資料導致截斷非空白字元或非 Null 的二進位資料。 如果它是字串值, 則會被右截斷。|  
|01S01|資料列發生錯誤|提取一或多個資料列時發生錯誤。<br /><br /> (如果當 ODBC 3.x 應用程式與 ODBC 2.x  驅動程式搭配使用時, 會傳回此  SQLSTATE, 則可以略過)。|  
|01S06|嘗試在結果集傳回第一個資料列集之前提取|當 FetchOrientation 為 SQL_FETCH_PRIOR、目前的位置超出第一個資料列, 且目前資料列的數目小於或等於資料列集大小時, 要求的資料列集會重迭結果集的開頭。<br /><br /> 當 FetchOrientation 為 SQL_FETCH_PRIOR、目前的位置超出結果集的結尾, 且資料列集大小大於結果集大小時, 要求的資料列集會重迭結果集的開頭。<br /><br /> 當 FetchOrientation 為 SQL_FETCH_RELATIVE、FetchOffset 為負數, 且 FetchOffset 的絕對值小於或等於資料列集大小時, 要求的資料列集會重迭結果集的開頭。<br /><br /> 當 FetchOrientation 為 SQL_FETCH_ABSOLUTE、FetchOffset 為負數, 且 FetchOffset 的絕對值大於結果集大小, 但小於或等於資料列集大小時, 要求的資料列集就會重迭結果集的開頭。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|01S07|小數截斷|針對資料行傳回的資料已被截斷。 若為數值資料類型, 則會截斷數位的小數部分。 若為包含時間元件的時間、時間戳記和間隔資料類型, 則會截斷時間的小數部分。<br /><br /> (函數會傳回 SQL_SUCCESS_WITH_INFO)。|  
|07006|限制的資料類型屬性違規|在結果集中, 資料行的資料值無法轉換成**SQLBindCol**中*TargetType*所指定的資料類型。<br /><br /> 資料行0是以 SQL_C_BOOKMARK 的資料類型系結, 且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE。<br /><br /> 資料行0是以 SQL_C_VARBOOKMARK 的資料類型系結, 而 SQL_ATTR_USE_BOOKMARKS 語句屬性並未設定為 SQL_UB_VARIABLE。|  
|07009|不正確描述項索引|驅動程式是一個不支援  **SQLExtendedFetch**的 ODBC 2.x 驅動程式, 而且資料行的系結中指定的資料行編號是0。<br /><br /> 已系結資料行 0, 而且 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|在函式完成處理之前, 驅動程式連線到驅動程式的資料來源之間的通訊連結失敗。|  
|22001|字串資料, 右邊已截斷|針對資料行傳回的可變長度書簽已截斷。|  
|22002|需要指標變數, 但未提供|已將 Null 資料提取至*StrLen_or_IndPtr*由**SQLBindCol** (或**SQLSETDESCFIELD**或**SQLSetDescRec**設定的 SQL_DESC_INDICATOR_PTR) 所設定的資料行, 其為 null 指標。|  
|22003|數值超出範圍|傳回一個或多個系結資料行的數值 (例如數值或字串), 會造成截斷的整個數位部分 (相對於分數)。<br /><br /> 如需詳細資訊, [](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)請參閱[附錄 D:資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|不正確日期時間格式|結果集中的字元資料行已系結至日期、時間或時間戳記 C 結構, 而且資料行中的值分別為不正確日期、時間或時間戳記。|  
|22012|除數為零|傳回算術運算式的值, 導致零除。|  
|22015|間隔欄位溢位|從精確的數值或間隔 SQL 類型指派到間隔 C 類型, 會導致前置欄位中的有效位數遺失。<br /><br /> 將資料提取到 interval C 類型時, 不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|結果集中的字元資料行已系結至字元 C 緩衝區, 而資料行包含的字元在緩衝區的字元集中沒有標記法。<br /><br /> C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;而資料行中的值不是系結 C 類型的有效常值。|  
|24000|指標狀態無效|*StatementHandle*處於執行中狀態, 但沒有與*StatementHandle*相關聯的結果集。|  
|40001|序列化失敗|執行提取的交易已終止, 以避免發生鎖死。|  
|40003|語句完成不明|此函式執行期間相關聯的連接失敗, 無法判斷交易的狀態。|  
|HY000|一般錯誤|發生錯誤, 但沒有任何特定 SQLSTATE, 且未定義任何執行特定的 SQLSTATE。 MessageText 緩衝區中**的 SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。 *\**|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY008|作業已取消|已啟用*StatementHandle*的非同步處理。 已呼叫函式, 在完成執行之前, 會在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在*StatementHandle*上再次呼叫函式。<br /><br /> 已呼叫函式, 並在完成執行之前, 從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY010|函數順序錯誤|(DM) 已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLFetchScroll**函數時, 這個非同步函式仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** , 並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前, 會呼叫這個函式。<br /><br /> (DM) 指定的*StatementHandle*不是處於執行中狀態。 在未先呼叫**SQLExecDirect**、 **SQLExecute**或目錄函式的情況下呼叫函式。<br /><br /> (DM) 已針對*StatementHandle*呼叫非同步執行的函式 (而非這個函式), 而且在呼叫這個函數時仍在執行中。<br /><br /> (DM) 已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** , 並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前, 已呼叫此函數。<br /><br /> (DM) 在呼叫**SQLExtendedFetch**之後, 以及呼叫具有 SQL_CLOSE 選項的**SQLFreeStmt**之前, 會呼叫*StatementHandle*的**SQLFetch** 。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫, 因為無法存取基礎記憶體物件, 可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|SQL_ATTR_USE_BOOKMARK 語句屬性已設定為 SQL_UB_VARIABLE, 而資料行0已系結至長度不等於此結果集之書簽長度上限的緩衝區。 (此長度適用于 IRD 的 [SQL_DESC_OCTET_LENGTH] 欄位, 可透過呼叫**SQLDescribeCol**、 **SQLColAttribute**或**SQLGetDescField**取得)。|  
|HY106|提取類型超出範圍|DM) 為引數 FetchOrientation 指定的值無效。<br /><br /> (DM) 引數 FetchOrientation 是 SQL_FETCH_BOOKMARK, 而 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE 語句屬性的值是 SQL_CURSOR_FORWARD_ONLY, 而 argument FetchOrientation 的值不是 SQL_FETCH_NEXT。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 語句屬性的值是 SQL_NONSCROLLABLE, 而 argument FetchOrientation 的值不是 SQL_FETCH_NEXT。|  
|HY107|資料列值超出範圍|以 SQL_ATTR_CURSOR_TYPE 語句屬性指定的值是 SQL_CURSOR_KEYSET_DRIVEN, 但是以 SQL_ATTR_KEYSET_SIZE 語句屬性指定的值大於0且小於以 SQL_ATTR_ROW_ARRAY_ 指定的值。SIZE 語句屬性。|  
|HY111|不正確書簽值|引數 FetchOrientation 是 SQL_FETCH_BOOKMARK, 而 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性中的值所指向的書簽無效或為 null 指標。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|(DM) 如需暫停狀態的詳細資訊, 請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*組合和對應資料行的 SQL 資料類型所指定的轉換。|  
|HYT00|已超過逾時的設定|在資料來源傳回要求的結果集之前, 查詢超時時間已過期。 超時期間是透過 SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT 來設定。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前, 連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|(DM) 與*StatementHandle*相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時, 就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING, 而且如果啟用通知模式, 則必須在控制碼上呼叫**SQLCompleteAsync** , 才能執行後置處理並完成作業。|  
  
## <a name="comments"></a>註解  
 **SQLFetchScroll**會從結果集傳回指定的資料列集。 資料列集可以由絕對或相對位置或依書簽來指定。 只有當結果集存在時 (也就是在建立結果集的呼叫之後, 以及該結果集的資料指標關閉之前), 才可以呼叫**SQLFetchScroll** 。 如果系結了任何資料行, 則會傳回這些資料行中的資料。 如果應用程式已指定資料列狀態陣列的指標, 或要傳回提取之資料列數目的緩衝區, 則**SQLFetchScroll**也會傳回這項資訊。 呼叫**SQLFetchScroll**可以與**SQLFetch**的呼叫混合, 但不能與**SQLExtendedFetch**的呼叫混合使用。  
  
 如需詳細資訊, 請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)和[使用可滾動](../../../odbc/reference/develop-app/using-scrollable-cursors.md)的資料指標。  
  
## <a name="positioning-the-cursor"></a>將游標定位  
 建立結果集時, 資料指標會位於結果集的開頭之前。 **SQLFetchScroll**會根據*FetchOrientation*和*FetchOffset*引數的值來放置區塊游標, 如下表所示。 下一節會顯示判斷新資料列集起點的確切規則。  
  
|FetchOrientation|意義|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|傳回下一個資料列集。 這相當於呼叫**SQLFetch**。<br /><br /> **SQLFetchScroll**會忽略*FetchOffset*的值。|  
|SQL_FETCH_PRIOR|傳回先前的資料列集。<br /><br /> **SQLFetchScroll**會忽略*FetchOffset*的值。|  
|SQL_FETCH_RELATIVE|從目前資料列集的開頭傳回資料列集*FetchOffset* 。|  
|SQL_FETCH_ABSOLUTE|傳回從資料列*FetchOffset*開始的資料列集。|  
|SQL_FETCH_FIRST|傳回結果集中的第一個資料列集。<br /><br /> **SQLFetchScroll**會忽略*FetchOffset*的值。|  
|SQL_FETCH_LAST|傳回結果集中最後一個完整的資料列集。<br /><br /> **SQLFetchScroll**會忽略*FetchOffset*的值。|  
|SQL_FETCH_BOOKMARK|從 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性所指定的書簽中, 傳回資料列集 FetchOffset 的資料列。|  
  
 驅動程式不需要支援所有的提取方向;應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 的資訊類型來呼叫**SQLGetInfo** (視游標的類型而定), 以判斷哪些提取方向為受驅動程式支援。 應用程式應該查看這些資訊類型中的 SQL_CA1_NEXT、SQL_CA1_RELATIVE、SQL_CA1_ABSOLUTE 和 WQL_CA1_BOOKMARK 位元遮罩。 此外, 如果資料指標是順向的, 而且 FetchOrientation 不是 SQL_FETCH_NEXT, 則**SQLFetchScroll**會傳回 SQLSTATE HY106 (提取類型超出範圍)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性會指定資料列集中的資料列數目。 如果**SQLFetchScroll**所提取的資料列集與結果集的結尾重迭, **SQLFetchScroll**會傳回部分資料列集。 也就是說, 如果 S + R-1 大於 L, 其中 S 是要提取之資料列集的起始資料列, R 是資料列集大小, 而 L 是結果集中的最後一個資料列, 則只有資料列集的第一個 L-S + 1 資料列才有效。 其餘的資料列是空的, 且狀態為 SQL_ROW_NOROW。  
  
 在**SQLFetchScroll**傳回之後, 目前的資料列就是資料列集的第一個資料列。  
  
## <a name="cursor-positioning-rules"></a>資料指標定位規則  
 下列各節說明每個 FetchOrientation 值的確切規則。 這些規則使用下列標記法。  
  
|表示法|意義|  
|--------------|-------------|  
|*開始之前*|區塊資料指標位於結果集開頭之前。 如果新資料列集的第一個資料列早于結果集的開頭, 則**SQLFetchScroll**會傳回 SQL_NO_DATA。|  
|*結束之後*|區塊資料指標位於結果集的結尾之後。 如果新資料列集的第一個資料列位於結果集的結尾, 則**SQLFetchScroll**會傳回 SQL_NO_DATA。|  
|*CurrRowsetStart*|目前資料列集中第一個資料列的編號。|  
|*LastResultRow*|結果集中最後一個資料列的編號。|  
|*RowsetSize*|資料列集大小。|  
|*FetchOffset*|*FetchOffset*引數的值。|  
|*BookmarkRow*|對應至 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性所指定之書簽的資料列。|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*開始之前*|1|  
|*CurrRowsetStart + RowsetSize*[1]  *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*sha-1 *> LastResultRow*|*結束之後*|  
|*結束之後*|*結束之後*|  
  
 [1] 如果資料列集大小在上一次呼叫提取資料列之後已經變更, 這就是與上一個呼叫搭配使用的資料列集大小。  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*開始之前*|*開始之前*|  
|*CurrRowsetStart = 1*|*開始之前*|  
|*1 < CurrRowsetStart <= RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart - RowsetSize* <sup>[2]</sup>|  
|*結束和 LastResultRow 之後 < RowsetSize*<sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*結束和 LastResultRow 之後 > = RowsetSize*<sup>[2]</sup>|*LastResultRow-RowsetSize + 1*<sup>[2]</sup>|  
  
 [1] **SQLFetchScroll**會傳回 SQLSTATE 01S06 (嘗試在結果集傳回第一個資料列集之前提取) 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果資料列集大小在上一次呼叫提取資料列之後已經變更, 這就是新的資料列集大小。  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*(Start 和 FetchOffset > 0 之前)或 (在 end 和 FetchOffset 之後 < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 和 FetchOffset < = 0*|*開始之前*|  
|*CurrRowsetStart = 1 和 FetchOffset < 0*|*開始之前*|  
|*CurrRowsetStart > 1 和 CurrRowsetStart + FetchOffset < 1 和&#124; FetchOffset &#124; > RowsetSize*<sup>[3]</sup>|*開始之前*|  
|*CurrRowsetStart > 1 和 CurrRowsetStart + FetchOffset < 1 和&#124; FetchOffset &#124; < = RowsetSize*<sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*結束之後*|  
|*結束和 FetchOffset 之後 > = 0*|*結束之後*|  
  
 [1] ***SQLFetchScroll***會傳回與 FetchOrientation 設定為 SQL_FETCH_ABSOLUTE 時所呼叫的相同資料列集。 如需詳細資訊, 請參閱 "SQL_FETCH_ABSOLUTE" 一節。  
  
 [2] **SQLFetchScroll**會傳回 SQLSTATE 01S06 (嘗試在結果集傳回第一個資料列集之前提取) 和 SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果資料列集大小在上一次呼叫提取資料列之後已經變更, 這就是新的資料列集大小。  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*FetchOffset < 0 和&#124; FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 和&#124; FETCHOFFSET &#124; > LastResultRow 和&#124; FetchOffset &#124; > RowsetSize*<sup>[2]</sup>|*開始之前*|  
|*FetchOffset < 0 和&#124; FETCHOFFSET &#124; > LastResultRow 和&#124; FetchOffset &#124; < = RowsetSize*<sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*開始之前*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*結束之後*|  
  
 [1] **SQLFetchScroll**會傳回 SQLSTATE 01S06 (嘗試在結果集傳回第一個資料列集之前提取) 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果資料列集大小在上一次呼叫提取資料列之後已經變更, 這就是新的資料列集大小。  
  
 針對動態資料指標執行的絕對提取無法提供所需的結果, 因為動態資料指標中的資料列位置無法確定。 這類作業相當於第一個 fetch, 後面接著 fetch 相對的;這不是不可部分完成的作業, 因為它是靜態資料指標上的絕對提取。  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*RowsetSize*<sup>[1]</sup> < = LastResultRow|*LastResultRow-RowsetSize + 1*<sup>[1]</sup>|  
|*RowsetSize*<sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 如果資料列集大小在上一次呼叫提取資料列之後已經變更, 這就是新的資料列集大小。  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 適用下列規則。  
  
|條件|新資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*開始之前*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*結束之後*|  
  
 如需書簽的詳細資訊, 請參閱[書簽 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>資料指標移動時已刪除、加入和錯誤資料列的效果  
 靜態和索引鍵集驅動資料指標有時會偵測加入至結果集的資料列, 並移除從結果集刪除的資料列。 藉由使用 SQL_STATIC_CURSOR_ATTRIBUTES2 和 SQL_KEYSET_CURSOR_ATTRIBUTES2 選項呼叫**SQLGetInfo** , 並查看 SQL_CA2_SENSITIVITY_ADDITIONS、SQL_CA2_SENSITIVITY_DELETIONS 和 SQL_CA2_SENSITIVITY_UPDATES 位元遮罩,應用程式會判斷特定驅動程式所執行的資料指標是否執行此動作。 對於可偵測已刪除資料列並加以移除的驅動程式, 下列段落描述此行為的效果。 對於可以偵測已刪除資料列, 但無法移除它們的驅動程式, 刪除不會影響資料指標移動, 而且下列段落不適用。  
  
 如果資料指標偵測到已加入至結果集的資料列, 或移除從結果集刪除的資料列, 就會顯示為只有在提取資料時才會偵測到這些變更。 這包括在呼叫**SQLFetchScroll**時, 將 FetchOrientation 設為 SQL_FETCH_RELATIVE, 並將 FetchOffset 設定為 0, 以重新擷取相同的資料列集, 但不包括使用 SQLSetPos 設定為 fOption 來呼叫 SQL_REFRESH 時的情況。 在後者的情況下, 資料列集緩衝區中的資料會重新整理, 但不會根據, 而且不會從結果集中移除已刪除的資料列。 因此, 當資料列從目前的資料列集刪除或插入時, 資料指標不會修改資料列集緩衝區。 相反地, 它會在提取任何先前包含已刪除資料列的資料列集, 或現在包含插入的資料列時, 偵測到變更。  
  
 例如:  
  
```cpp  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 當**SQLFetchScroll**傳回的新資料列集具有相對於目前資料列集的位置時, 也就是 FETCHORIENTATION 為 SQL_FETCH_NEXT、SQL_FETCH_PRIOR 或 SQL_FETCH_RELATIVE, 計算時不會包含目前資料列集的變更。新資料列集的開始位置。 不過, 它會包含目前資料列集外部的變更 (如果它能夠偵測到)。 此外, 當**SQLFetchScroll**傳回的新資料列集具有與目前資料列集無關的位置時, 也就是 FETCHORIENTATION 為 SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE 或 SQL_FETCH_BOOKMARK-它包含所有變更能夠偵測, 即使它們位於目前的資料列集中也一樣。  
  
 當判斷新加入的資料列是否在目前資料列集的內部或外部時, 會將部分資料列集視為最後一個有效資料列的結尾。也就是不會 SQL_ROW_NOROW 資料列狀態的最後一個資料列。 例如, 假設資料指標能夠偵測到新加入的資料列, 目前的資料列集是部分資料列集, 應用程式會加入新的資料列, 而資料指標會將這些資料列加入結果集的結尾。 如果應用程式呼叫**SQLFetchScroll** , 並將 FetchOrientation 設為 SQL_FETCH_NEXT, 則**SQLFetchScroll**會傳回從第一個新加入的資料列開始的資料列集。  
  
 例如, 假設目前的資料列集是由資料列21到30組成, 資料列集大小為 10, 則資料指標會移除從結果集刪除的資料列, 而且資料指標會偵測加入至結果集的資料列。 下表顯示**SQLFetchScroll**在各種情況下傳回的資料列。  
  
|變更|Fetch 類型|FetchOffset|新的資料列集 [1]|  
|------------|----------------|-----------------|---------------------|  
|刪除資料列21|NEXT|0|31到40|  
|刪除資料列31|NEXT|0|32到41|  
|在資料列21和22之間插入資料列|NEXT|0|31到40|  
|在資料列30和31之間插入資料列|NEXT|0|已插入資料列, 31 到39|  
|刪除資料列21|PRIOR|0|11至20|  
|刪除資料列20|PRIOR|0|10至19|  
|在資料列21和22之間插入資料列|PRIOR|0|11至20|  
|在資料列20和21之間插入資料列|PRIOR|0|12到 20, 插入的資料列|  
|刪除資料列21|RELATIVE|0|22到 31<sup>[2]</sup>|  
|刪除資料列21|RELATIVE|1|22到31|  
|在資料列21和22之間插入資料列|RELATIVE|0|21, 插入的資料列, 22 到29|  
|在資料列21和22之間插入資料列|RELATIVE|1|22到31|  
|刪除資料列21|ABSOLUTE|21|22到 31<sup>[2]</sup>|  
|刪除資料列22|ABSOLUTE|21|21、23到31|  
|在資料列21和22之間插入資料列|ABSOLUTE|22|已插入資料列, 22 至29|  
  
 [1] 此資料行在插入或刪除任何資料列之前, 會先使用資料列編號。  
  
 [2] 在此情況下, 資料指標會嘗試傳回從資料列21開始的資料列。 因為已刪除資料列 21, 所以它傳回的第一個資料列是資料列22。  
  
 錯誤資料列 (也就是狀態為 SQL_ROW_ERROR 的資料列) 不會影響資料指標移動。 例如, 如果目前的資料列集是以資料列11開頭, 而資料列11的狀態是 SQL_ROW_ERROR, 則呼叫**SQLFetchScroll**並將 FetchOrientation 設為 SQL_FETCH_RELATIVE, 並將 FetchOffset 設定為 5, 就會傳回從資料列16開始的資料列集, 就像已 SQL_SUCCESS 資料列11的狀態。  
  
## <a name="returning-data-in-bound-columns"></a>傳回系結資料行中的資料  
 **SQLFetchScroll**會以與**SQLFetch**相同的方式傳回系結資料行中的資料。 如需詳細資訊, 請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的「傳回系結資料行中的資料」。  
  
 如果未系結任何資料行, 則**SQLFetchScroll**不會傳回資料, 但會將區塊游標移到指定的位置。 是否可以使用**SQLGetData** , 從區塊資料指標的未系結資料行抓取資料, 取決於驅動程式。 如果對**SQLGetInfo**的呼叫會傳回 SQL_GETDATA_EXTENSIONS 資訊類型的 SQL_GD_BLOCK 位, 則支援這項功能。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 **SQLFetchScroll**會使用相同的公式, 將資料和長度/指標緩衝區的位址判斷為**SQLFetch**。 如需詳細資訊, 請參閱[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 **SQLFetchScroll**會以與 SQLFetch 相同的方式, 來設定資料列狀態陣列中的值。 如需詳細資訊, 請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的「資料列狀態陣列」。  
  
## <a name="rows-fetched-buffer"></a>讀取的資料列緩衝區  
 **SQLFetchScroll**會傳回在資料列提取緩衝區中提取的資料列數目, 其方式與**SQLFetch**相同。 如需詳細資訊, 請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的「資料列提取緩衝區」。  
  
## <a name="error-handling"></a>錯誤處理  
 當應用程式在 ODBC 3.x 驅動程式中呼叫**SQLFetchScroll**時, 驅動程式管理員會呼叫驅動程式中的**SQLFetchScroll** 。 當應用程式在 ODBC 2.x 驅動程式中呼叫**SQLFetchScroll**時, 驅動程式管理員會呼叫驅動程式中的 SQLExtendedFetch。 由於**SQLFetchScroll**和 SQLExtendedFetch 會以稍微不同的方式處理錯誤, 因此當應用程式呼叫 odbc 2.X 和 odbc 3.x 驅動程式中的**SQLFetchScroll**時, 會看到稍微不同的錯誤行為。  
  
 **SQLFetchScroll**會以與**SQLFetch**相同的方式傳回錯誤和警告;如需詳細資訊, 請參閱**SQLFetch**中的「錯誤處理」。 **SQLExtendedFetch**會以與**SQLFetch**相同的方式傳回錯誤, 但有下列例外狀況:  
  
 當資料列集中的特定資料列發生警告時, SQLExtendedFetch 會將資料列狀態陣列中對應的專案設定為 SQL_ROW_SUCCESS, 而不是 SQL_ROW_SUCCESS_WITH_INFO。  
  
 如果在資料列集的每個資料列中發生錯誤, SQLExtendedFetch 會傳回 SQL_SUCCESS_WITH_INFO, 而非 SQL_ERROR。  
  
 在套用至個別資料列的每個狀態記錄群組中, SQLExtendedFetch 所傳回的第一個狀態記錄必須包含 SQLSTATE 01S01 (資料列中的錯誤)。**SQLFetchScroll**不會傳回此 SQLSTATE。 如果 SQLExtendedFetch 無法傳回其他 SQLSTATEs, 它仍然必須傳回此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和開放式平行存取  
 如果資料指標使用開放式平行存取 (亦即, SQL_ATTR_CONCURRENCY 語句屬性的值為 SQL_CONCUR_VALUES 或 SQL_CONCUR_ROWVER),  則會更新資料來源所使用的開放式並行值, 以偵測是否資料列已變更。 每當**SQLFetchScroll**提取新的資料列集時, 就會發生這種情況, 包括 refetches 目前資料列集的時間。 (其呼叫方式是將 FetchOrientation 設定為 SQL_FETCH_RELATIVE, 並將 FetchOffset 設定為0。)  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驅動程式  
 當應用程式在 ODBC 2.x 驅動程式中呼叫**SQLFetchScroll**時, 驅動程式管理員會將此呼叫對應至**SQLExtendedFetch**。 它會傳遞**SQLExtendedFetch**之引數的下列值。  
  
|SQLExtendedFetch 引數|值|  
|-------------------------------|-----------|  
|StatementHandle|**SQLFetchScroll**中的 StatementHandle。|  
|FetchOrientation|**SQLFetchScroll**中的 FetchOrientation。|  
|FetchOffset|如果 FetchOrientation 不是 SQL_FETCH_BOOKMARK, 則會使用**SQLFetchScroll**中的 FetchOffset 引數值。<br /><br /> 如果 FetchOrientation 為 SQL_FETCH_BOOKMARK, 則會使用儲存在 SQL_ATTR_FETCH_BOOKMARK_PTR 語句屬性所指定之位址的值。|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR 語句屬性所指定的位址。|  
|RowStatusArray|SQL_ATTR_ROW_STATUS_PTR 語句屬性所指定的位址。|  
  
 如需詳細資訊, 請參閱附錄 G 中的[區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):回溯相容性的驅動程式方針。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>描述項和 SQLFetchScroll  
 **SQLFetchScroll**與描述項的互動方式與**SQLFetch**相同。 如需詳細資訊, 請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)函式中的 < 描述項和 SQLFetchScroll 一節。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱資料行取向系[](../../../odbc/reference/develop-app/row-wise-binding.md)結、資料列取向系結、[定位 Update 和 Delete 語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), 以及[使用 SQLSetPos 更新](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)資料列集中的資料[列](../../../odbc/reference/develop-app/column-wise-binding.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行 bulk insert、update 或 delete 作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|關閉語句上的資料指標|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位游標、重新整理資料列集中的資料, 或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定語句屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
