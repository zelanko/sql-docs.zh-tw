---
title: SQLFetchScroll 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 146967ebc31d5e7d8176d37ee5b8b0b97b6c0674
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769487"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 函數
**合規性**  
 版本導入： ODBC 3.0 版的標準符合性： ISO 92  
  
 **摘要**  
 **SQLFetchScroll**提取從結果集的指定資料列集的資料，並傳回所有繫結的資料行的資料。 在絕對或相對位置或依書籤，則可以指定資料列集。  
  
 驅動程式管理員使用 ODBC 2.x 驅動程式，對應到此函式**SQLExtendedFetch**。 如需詳細資訊，請參閱 <<c0> [ 對應取代函式應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Sqlfetchscroll*  
 [輸入]  
  
 擷取的型別：  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE 但  
  
 要使用 SQL_FETCH_BOOKMARK  
  
 如需詳細資訊，請參閱 「 定位游標 」 「 註解 」 一節。  
  
 *FetchOffset*  
 [輸入]  
  
 要擷取的資料列數目。 這個引數的解譯取決於 windows 7 *Sqlfetchscroll*引數。 如需詳細資訊，請參閱 「 定位游標 」 「 註解 」 一節。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetchScroll**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec** SQL_HANDLE_STMT HandleType 與的控制代碼StatementHandle。 下表列出通常所傳回的 SQLSTATE 值**SQLFetchScroll** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。 如果在單一資料行，就會發生錯誤**SQLGetDiagField** Sqlgetdiagfield 的 SQL_DIAG_COLUMN_NUMBER 來判斷發生錯誤; 資料行也可以呼叫並**SQLGetDiagField**可以呼叫使用 Sqlgetdiagfield 的 SQL_DIAG_ROW_NUMBER 來決定包含該資料行的資料列。  
  
 針對所有這些 Sqlstate 可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除了 01xxx Sqlstate)，如果一個或多個，而非全部的資料列的多資料列的作業，發生錯誤，而且如果發生錯誤時，會傳回 SQL_ERROR，則會傳回 SQL_SUCCESS_WITH_INFO單一資料列作業。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|字串或二進位資料傳回的資料行導致的非空白的字元或非 NULL 的二進位資料截斷。 如果是字串值，則向右截斷。|  
|01S01|資料列中的錯誤|擷取一或多個資料列時發生錯誤。<br /><br /> (如果 ODBC 3 時，會傳回此 SQLSTATE *.x*應用程式正在使用的 ODBC 2 *.x*驅動程式，可以忽略它。)|  
|01S06|嘗試擷取結果集傳回第一個資料列集之前|要求的資料列集重疊時 Sqlfetchscroll 已 SQL_FETCH_PRIOR、 目前的位置是在第一個資料列，和目前資料列數目小於或等於資料列集大小的結果集的開頭。<br /><br /> 要求的資料列集重疊時 Sqlfetchscroll 是 SQL_FETCH_PRIOR、 目前的位置已超過結果集的結尾，且資料列集大小大於結果集大小的結果集的開頭。<br /><br /> 要求的資料列集重疊時 Sqlfetchscroll 已 sql_fetch_relative 但、 FetchOffset 是負值，和 FetchOffset 的絕對值是小於或等於資料列集大小的結果集的開頭。<br /><br /> 要求的資料列集重疊時 Sqlfetchscroll 已 SQL_FETCH_ABSOLUTE、 FetchOffset 是負值，和 FetchOffset 絕對值已超過結果集大小的結果集的開頭，但小於或等於資料列集大小。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數位數截斷|傳回資料行的資料已遭截斷。 數值資料類型已遭截斷數字的小數部分。 時間、 時間戳記，和包含時間元件的 interval 資料類型，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|在結果集中的資料行的資料值無法轉換成所指定的資料類型*TargetType*中**SQLBindCol**。<br /><br /> 資料類型為 SQL_C_BOOKMARK，繫結資料行 0 且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_VARIABLE。<br /><br /> 資料類型為 SQL_C_VARBOOKMARK，繫結資料行 0 和 SQL_ATTR_USE_BOOKMARKS 陳述式屬性未設定為 SQL_UB_VARIABLE。|  
|07009|描述項索引無效|驅動程式的 ODBC 2 *.x*不支援的驅動程式**SQLExtendedFetch**，和資料行繫結中指定資料行編號為 0。<br /><br /> 繫結資料行 0，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊已截斷|傳回資料行的可變長度書籤已遭截斷。|  
|22002|指標變數但未提供|NULL 的資料擷取成資料行其*StrLen_or_IndPtr*來設定**SQLBindCol** (或所設定的 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 為 null 指標。|  
|22003|數值超出範圍|傳回數字的值 （做為數值或字串），一或多個繫結的資料行可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 如需詳細資訊，請參閱 <<c0> [ 轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中[附錄 d： 資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|無效的日期時間格式|在結果集中的字元資料行已繫結至日期、 時間或時間戳記 C 結構，但資料行的值，分別無效的日期、 時間戳記。|  
|22012|除數為零|算術運算式的值傳回，因而導致除數為零。|  
|22015|間隔欄位溢位|將指派從精確數值或時間間隔 SQL 型別，給 C 間隔類型造成有效位數的遺失開頭的欄位中。<br /><br /> 當 C 間隔類型以提取資料時，發生 C 間隔類型中的 SQL 類型的值不表示。|  
|22018|轉換規格的字元值無效|在結果集中的字元資料行已繫結至字元 C 的緩衝區，和資料行包含緩衝區的字元集中未表示的字元。<br /><br /> C 類型為精確或近似數值、 日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;和資料行中的值不是有效的常值的繫結的 C 類型。|  
|24000|指標狀態無效|*StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。|  
|40001|序列化失敗|擷取已執行所在的交易已終止避免死結。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLFetchScroll**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 已呼叫的函式，但是未先呼叫**SQLExecDirect**， **SQLExecute**或目錄函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLFetch**針對呼叫*StatementHandle*之後**SQLExtendedFetch**呼叫之前**SQLFreeStmt** SQL_ 與已呼叫關閉選項。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|SQL_ATTR_USE_BOOKMARK 陳述式屬性已設定為 SQL_UB_VARIABLE，而且資料行 0 已繫結至其長度不等於此結果集的書籤的最大長度的緩衝區。 (這個長度的 SQL_DESC_OCTET_LENGTH IRD 欄位中而且可由呼叫**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY106|擷取類型超出範圍|DM) Sqlfetchscroll 引數所指定的值無效。<br /><br /> (DM) Sqlfetchscroll 的引數是要使用 SQL_FETCH_BOOKMARK，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE 陳述式屬性的值為 SQL_CURSOR_FORWARD_ONLY 和 Sqlfetchscroll 未 SQL_FETCH_NEXT 的引數的值。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 陳述式屬性的值為 SQL_NONSCROLLABLE 和 Sqlfetchscroll 未 SQL_FETCH_NEXT 的引數的值。|  
|HY107|資料列值超出範圍|SQL_ATTR_CURSOR_TYPE 陳述式屬性所指定的值是 SQL_CURSOR_KEYSET_DRIVEN，但使用 SQL_ATTR_KEYSET_SIZE 陳述式屬性所指定的值是大於 0 且小於 SQL_ATTR_ROW_ARRAY_ 與指定的值大小陳述式屬性。|  
|HY111|無效的書籤值|Sqlfetchscroll 的引數是要使用 SQL_FETCH_BOOKMARK，和 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性中的值所指向的書籤無效或為 null 指標。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援指定的組合來轉換*TargetType*中**SQLBindCol**和對應的資料行的 SQL 資料類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 透過 SQLSetStmtAttr，sql_attr_query_timeout 時設定的逾時期限。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLFetchScroll**從結果集中傳回指定的資料列集。 以絕對或相對位置，或依書籤，則可以指定資料列集。 **SQLFetchScroll**只在結果集存在時，才可以呼叫 — 也就是說，在呼叫之後，建立結果集，而且游標之前關閉結果集的移轉。 如果任何資料行已繫結，它會傳回這些資料行中的資料。 如果應用程式具有指定資料列狀態陣列或在其中傳回擷取的資料列數目的緩衝區的指標**SQLFetchScroll**這項資訊也會傳回。 呼叫**SQLFetchScroll**可以透過呼叫混合**SQLFetch**但不能呼叫的方式來混合**SQLExtendedFetch**。  
  
 如需詳細資訊，請參閱 <<c0> [ 使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)並[使用可捲動資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)。  
  
## <a name="positioning-the-cursor"></a>遊標定位在  
 建立結果集時，資料指標位於結果集的開頭之前。 **SQLFetchScroll**放置區塊資料指標的值為基礎*Sqlfetchscroll*並*FetchOffset*引數下表所示。 下一節顯示的確切規則來判斷新的資料列集的開頭。  
  
|Sqlfetchscroll|意義|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|傳回下一個資料列集。 這就相當於呼叫**SQLFetch**。<br /><br /> **SQLFetchScroll**的值會略過*FetchOffset*。|  
|SQL_FETCH_PRIOR|傳回先前的資料列集。<br /><br /> **SQLFetchScroll**的值會略過*FetchOffset*。|  
|SQL_FETCH_RELATIVE 但|傳回資料列集*FetchOffset*從目前的資料列集的開頭。|  
|SQL_FETCH_ABSOLUTE|傳回資料列集資料列開始*FetchOffset*。|  
|SQL_FETCH_FIRST|在結果集中傳回的第一個資料列集。<br /><br /> **SQLFetchScroll**的值會略過*FetchOffset*。|  
|SQL_FETCH_LAST|在結果集中傳回最後一個完整的資料列集。<br /><br /> **SQLFetchScroll**的值會略過*FetchOffset*。|  
|要使用 SQL_FETCH_BOOKMARK|傳回資料列集 FetchOffset 的資料列從 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指定的書籤。|  
  
 驅動程式不需要支援所有 fetch 方向;應用程式呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （取決於資料指標類型） 的資訊類型來判斷哪一個 fetch驅動程式支援的方向。 應用程式應該看看這些資訊類型在 SQL_CA1_NEXT、 SQL_CA1_RELATIVE、 SQL_CA1_ABSOLUTE 和 WQL_CA1_BOOKMARK 位元遮罩。 此外，如果資料指標是順向的而不 SQL_FETCH_NEXT，Sqlfetchscroll。 **SQLFetchScroll**傳回 SQLSTATE HY106 （擷取類型超出範圍）。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性會指定資料列集中的資料列數目。 如果所要提取的資料列集**SQLFetchScroll**重疊的結果集結尾**SQLFetchScroll**傳回部分的資料列集。 也就是說，如果 S + R，-1 大於 L，其中 S 資料列集擷取，R 的起始資料列是資料列集大小，而 L 最後一個資料列結果集中則只有第一個左 – S + 1 個資料列集的資料列都有效。 剩餘的資料列是空的且狀態為 SQL_ROW_NOROW。  
  
 在後**SQLFetchScroll**傳回時，目前的資料列是資料列集的第一個資料列。  
  
## <a name="cursor-positioning-rules"></a>資料指標定位規則  
 下列各節描述每個值的 Sqlfetchscroll 確切的規則。 這些規則會使用下列標記法。  
  
|表示法|意義|  
|--------------|-------------|  
|*開始之前*|區塊資料指標位於結果集的開頭之前。 如果新的資料列集的第一個資料列的結果集中，開始之前**SQLFetchScroll**傳回 sql_no_data 為止。|  
|*後端*|區塊資料指標位於結果結尾設定之後。 如果新的資料列集的第一個資料列之後的結果集結尾**SQLFetchScroll**傳回 sql_no_data 為止。|  
|*CurrRowsetStart*|中目前資料列集的第一個資料列數目。|  
|*LastResultRow*|在結果集中的最後一個資料列數目。|  
|*RowsetSize*|資料列集大小。|  
|*FetchOffset*|值*FetchOffset*引數。|  
|*BookmarkRow*|對應至 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指定的書籤的資料列。|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*開始之前*|1|  
|*CurrRowsetStart + RowsetSize*[1]  *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*後端*|  
|*後端*|*後端*|  
  
 [1] 如果自前一個呼叫來擷取資料列之後已變更的資料列集大小，這是先前呼叫所使用的資料列集大小。  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*開始之前*|*開始之前*|  
|*CurrRowsetStart = 1*|*開始之前*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2]。</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*後端和 LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*後端和 LastResultRow > = RowsetSize* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2]。</sup>|  
  
 [1] **SQLFetchScroll**傳回 SQLSTATE 01S06 （之前嘗試擷取結果集傳回第一個資料列集） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自前一個呼叫來擷取資料列之後已變更的資料列集大小，這會是新的資料列集大小。  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE 但  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*(之前啟動和 FetchOffset > 0)或者 (後端和 FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 和 FetchOffset < = 0*|*開始之前*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*開始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*開始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*後端*|  
|*後端和 FetchOffset > = 0*|*後端*|  
  
 [1] ***SQLFetchScroll***傳回相同的資料列集，如同使用 Sqlfetchscroll 設 SQL_FETCH_ABSOLUTE 呼叫它。 如需詳細資訊，請參閱"SQL_FETCH_ABSOLUTE 」 一節。  
  
 [2] **SQLFetchScroll**傳回 SQLSTATE 01S06 （之前嘗試擷取結果集傳回第一個資料列集） 和 SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果自前一個呼叫來擷取資料列之後已變更的資料列集大小，這會是新的資料列集大小。  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*FetchOffset < 0 與&#124;FetchOffset &#124; < = LastResultRow*|*LastResultRow FetchOffset + 1*|  
|*FetchOffset < 0 與&#124;FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*開始之前*|  
|*FetchOffset < 0 與&#124;FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*開始之前*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*後端*|  
  
 [1] **SQLFetchScroll**傳回 SQLSTATE 01S06 （之前嘗試擷取結果集傳回第一個資料列集） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自前一個呼叫來擷取資料列之後已變更的資料列集大小，這會是新的資料列集大小。  
  
 針對動態資料指標執行的絕對提取無法提供所需的結果，因為動態資料指標中的資料列位置不明。 這類作業相當於 fetch relative，接著再一次擷取它不是不可部分完成的作業，因為靜態資料指標上的絕對提取。  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 如果自前一個呼叫來擷取資料列之後已變更的資料列集大小，這會是新的資料列集大小。  
  
## <a name="sqlfetchbookmark"></a>要使用 SQL_FETCH_BOOKMARK  
 適用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*開始之前*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*後端*|  
  
 書籤的相關資訊，請參閱[書籤 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>已刪除、 加入的效果和錯誤資料列，對於資料指標移動  
 靜態和索引鍵集驅動資料指標有時會偵測新增至結果的資料列設定，並移除從結果集中刪除的資料列。 藉由呼叫**SQLGetInfo** SQL_KEYSET_CURSOR_ATTRIBUTES2 SQL_STATIC_CURSOR_ATTRIBUTES2 與選項，並查看 SQL_CA2_SENSITIVITY_ADDITIONS、 SQL_CA2_SENSITIVITY_DELETIONS 和 SQL_CA2_SENSITIVITY_更新位元遮罩，應用程式會決定是否實作特定的驅動程式的資料指標執行這項操作。 驅動程式，可以偵測已刪除的資料列，並將它們移除下, 面段落會說明此行為的影響。 驅動程式，可以偵測已刪除的資料列，但無法將它們移除，刪除不會影響資料指標移動，且不會套用下列段落。  
  
 如果資料指標會偵測新增至結果集的資料列，或移除從結果集中刪除的資料列，它會顯示如同時偵測到這些變更只會在擷取資料。 這包括案例時**SQLFetchScroll**呼叫 Sqlfetchscroll 設 sql_fetch_relative 但 FetchOffset 設定為 0，重新擷取相同的資料列集，但不包含大小寫，fOption 設 SQL_ 的呼叫 SQLSetPos 時重新整理。 在後者的情況下，資料列集的緩衝區中的資料重新整理，但不是 refetched，和已刪除的資料列不會移除從結果集。 因此，當從刪除或插入至目前的資料列集資料列，資料指標不會修改資料列集的緩衝區。 相反地，它會偵測變更它擷取任何資料列集，先前包含刪除的資料列，或是現在插入的資料列。  
  
 例如：  
  
```  
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
  
 時**SQLFetchScroll**傳回新的資料列集具有相對於目前資料列集的位置，也就是 Sqlfetchscroll 是 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR 或 sql_fetch_relative，但 — 它不包含目前資料列集的變更當計算新的資料列集的開始位置。 不過，它包含目前資料列集外的變更是否能夠偵測它們。 此外，當**SQLFetchScroll**傳回新的資料列集有獨立的目前資料列集的位置，也就是 Sqlfetchscroll 是 SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE，還是要使用 SQL_FETCH_BOOKMARK — 它包含所有的變更，它可以偵測，即使它們位於目前的資料列集。  
  
 在決定新加入的資料列是否為內部或外部的目前資料列集時，部分的資料列集視為在最後一個有效的資料列; 結束也就是其中的資料列狀態不是 SQL_ROW_NOROW 的最後一個資料列。 例如，假設資料指標可以偵測新加入的資料列、 目前的資料列集是部分的資料列集、 應用程式加入了新的資料列和資料指標會將這些資料列加入至結果集的結尾。 如果應用程式會呼叫**SQLFetchScroll**與設為 SQL_FETCH_NEXT，Sqlfetchscroll **SQLFetchScroll**傳回資料列集的第一個新加入的資料列開始。  
  
 例如，假設目前的資料列集包含 21 到 30 的資料列、 資料列集大小為 10、 資料指標會移除從結果集中，刪除資料列和資料指標會偵測新增至結果集的資料列。 下表顯示的資料列**SQLFetchScroll**在各種情況下傳回。  
  
|變更|擷取型別|FetchOffset|新的資料列集 [1]|  
|------------|----------------|-----------------|---------------------|  
|刪除資料列 21|NEXT|0|31 到 40|  
|刪除資料列 31|NEXT|0|32 到 41|  
|插入資料列 21 到 22 之間的資料列|NEXT|0|31 到 40|  
|插入資料列 30 和 31 之間的資料列|NEXT|0|插入的資料列，31 到 39|  
|刪除資料列 21|PRIOR|0|11 到 20|  
|刪除資料列 20|PRIOR|0|10 到 19|  
|插入資料列 21 到 22 之間的資料列|PRIOR|0|11 到 20|  
|插入資料列 20 和 21 之間的資料列|PRIOR|0|12 到 20，插入的資料列|  
|刪除資料列 21|RELATIVE|0|22 至 31 日<sup>[2]</sup>|  
|刪除資料列 21|RELATIVE|1|22 至 31 日|  
|插入資料列 21 到 22 之間的資料列|RELATIVE|0|21，插入資料列，22 到 29|  
|插入資料列 21 到 22 之間的資料列|RELATIVE|1|22 至 31 日|  
|刪除資料列 21|ABSOLUTE|21|22 至 31 日<sup>[2]</sup>|  
|刪除資料列 22|ABSOLUTE|21|21、 23 至 31 日|  
|插入資料列 21 到 22 之間的資料列|ABSOLUTE|22|插入的資料列，22 到 29|  
  
 [1] 此資料行之前插入或刪除任何資料列，使用資料列編號。  
  
 [2] 在此情況下，資料指標會嘗試傳回開頭為 21 的資料列的資料列。 因為已刪除資料列 21，它會傳回第一個資料列就會是資料列 22。  
  
 錯誤資料列 （亦即，資料列狀態 SQL_ROW_ERROR） 不會影響資料指標移動。 例如，如果目前的資料列集的開頭資料列 11 及狀態資料列 11 是 SQL_ROW_ERROR 呼叫**SQLFetchScroll** Sqlfetchscroll 設 sql_fetch_relative 但 FetchOffset 設為 5 會傳回資料列 16，開始的資料列集就如同如果 11 的資料列的狀態是 SQL_SUCCESS。  
  
## <a name="returning-data-in-bound-columns"></a>繫結的資料行中傳回的資料  
 **SQLFetchScroll**繫結的資料行中傳回資料，做為相同的方式**SQLFetch**。 如需詳細資訊，請參閱 「 傳回資料中繫結資料行 」 中[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 如果沒有資料行已繫結， **SQLFetchScroll**不會傳回資料，但未將區塊資料指標移至指定的位置。 是否可以從使用區塊資料指標的未繫結的資料行擷取資料**SQLGetData**取決於驅動程式。 如果呼叫，這項功能的支援**SQLGetInfo**傳回 SQL_GD_BLOCK SQL_GETDATA_EXTENSIONS 資訊類型的位元。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 **SQLFetchScroll**會使用相同的公式來判斷做為資料和長度/指標緩衝區的位址**SQLFetch**。 如需詳細資訊，請參閱 「 緩衝區位址 」 中[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 **SQLFetchScroll** SQLFetch 相同方式設定資料列狀態陣列中的值。 如需詳細資訊，請參閱 「 資料列狀態陣列 」 中[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="rows-fetched-buffer"></a>擷取緩衝區資料列。  
 **SQLFetchScroll**傳回相同的方式擷取的資料列緩衝區中提取的資料列數目**SQLFetch**。 如需詳細資訊，請參閱 「 資料列提取緩衝區 」 中[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="error-handling"></a>錯誤處理  
 當應用程式呼叫**SQLFetchScroll** ODBC 3.x 驅動程式，在驅動程式管理員會呼叫**SQLFetchScroll**驅動程式中。 當應用程式呼叫**SQLFetchScroll**在 ODBC 2.x 驅動程式、 驅動程式管理員會呼叫 SQLExtendedFetch 驅動程式中。 因為**SQLFetchScroll** SQLExtendedFetch 處理方式稍有不同的錯誤、 應用程式會看到稍有不同的錯誤行為時它會呼叫**SQLFetchScroll**在 ODBC 2.x 和 ODBC3.x 驅動程式。  
  
 **SQLFetchScroll**相同的方式傳回錯誤和警告**SQLFetch**; 如需詳細資訊，請參閱 「 錯誤處理 」 中**SQLFetch**。 **SQLExtendedFetch**會傳回錯誤，以相同的方式**SQLFetch**，但有下列例外狀況：  
  
 警告發生時套用至特定的資料列中資料列集，則 SQLExtendedFetch 設定 SQL_ROW_SUCCESS，不 SQL_ROW_SUCCESS_WITH_INFO 資料列狀態陣列中對應的項目。  
  
 如果資料列集中的每個資料列中發生錯誤，SQLExtendedFetch 就會傳回 SQL_SUCCESS_WITH_INFO，不 SQL_ERROR。  
  
 在每個群組套用到個別的資料列狀態記錄，第一個 SQLExtendedFetch 所傳回的狀態記錄必須包含 SQLSTATE 01S01 （錯誤資料列中的）;**SQLFetchScroll**不會傳回此 SQLSTATE。 如果無法傳回其他 Sqlstate SQLExtendedFetch，仍然必須傳回此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和開放式並行存取  
 如果資料指標使用開放式並行存取，也就是 SQL_ATTR_CONCURRENCY 陳述式屬性具有值為 SQL_CONCUR_VALUES 或 SQL_CONCUR_ROWVER — **SQLFetchScroll**更新資料所使用的開放式並行存取值若要偵測是否已變更的資料列的來源。 發生這種情況每當**SQLFetchScroll**擷取新資料列集，包括當它 refetches 目前資料列集。 （呼叫 Sqlfetchscroll 設 sql_fetch_relative 但 FetchOffset 設為 0。）  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驅動程式  
 當應用程式呼叫**SQLFetchScroll** ODBC 2.x 驅動程式，驅動程式管理員會對應至這個呼叫**SQLExtendedFetch**。 它會傳遞下列值的引數**SQLExtendedFetch**。  
  
|SQLExtendedFetch 引數|值|  
|-------------------------------|-----------|  
|StatementHandle|在 StatementHandle **SQLFetchScroll**。|  
|Sqlfetchscroll|中的 Sqlfetchscroll **SQLFetchScroll**。|  
|FetchOffset|Sqlfetchscroll 是否不是要使用 SQL_FETCH_BOOKMARK FetchOffset 引數中的值**SQLFetchScroll**用。<br /><br /> 如果要使用 SQL_FETCH_BOOKMARK Sqlfetchscroll 即會使用 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指定的位址儲存的值。|  
|RowCountPtr|SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性所指定的位址。|  
|RowStatusArray|Sql_attr_row_status_ptr 設定陳述式屬性所指定的位址。|  
  
 如需詳細資訊，請參閱 <<c0> [ 區塊資料指標、 可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)附錄 g： 驅動程式指導方針，為了與舊版相容。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>描述項和 SQLFetchScroll  
 **SQLFetchScroll**互動以相同方式的描述元**SQLFetch**。 如需詳細資訊，請參閱中的 「 描述項和 SQLFetchScroll 」 一節[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)，[資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)，[定位的 Update 和 Delete 陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)，和[使用 SQLSetPos更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行大量插入、 更新或刪除作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|在結果集中傳回資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|擷取單一資料列或順向方向中的資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|關閉資料指標陳述式上|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回結果集資料行|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|遊標定位、 重新整理此資料列集中，或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
