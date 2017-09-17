---
title: "SQLFetchScroll 函數 |Microsoft 文件"
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
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 79224469fe1e6e4f0840eceb394b30cec63fcd2a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLFetchScroll**從結果集提取資料之指定資料列集，並傳回所有的繫結資料行的資料。 在絕對或相對的位置或書籤，可以指定資料列集。  
  
 當使用 ODBC 2.x 驅動程式，驅動程式管理員會對應到此函式**SQLExtendedFetch**。 如需詳細資訊，請參閱[對應取代函式的應用程式的回溯相容性](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
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
  
 擷取的類型：  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE 但  
  
 要使用 SQL_FETCH_BOOKMARK  
  
 如需詳細資訊，請參閱 「 定位資料指標 」 的 [意見] 區段中。  
  
 *FetchOffset*  
 [輸入]  
  
 要擷取的資料列數目。 這個引數的解譯取決於值*Sqlfetchscroll*引數。 如需詳細資訊，請參閱 「 定位資料指標 」 的 [意見] 區段中。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetchScroll**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec** SQL_HANDLE_STMT HandleType 與控制代碼StatementHandle。 下表列出通常所傳回的 SQLSTATE 值**SQLFetchScroll** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。 如果在單一資料行，就會發生錯誤**SQLGetDiagField** Sqlgetdiagfield 的 SQL_DIAG_COLUMN_NUMBER 來判斷資料行發生錯誤; 也可以呼叫和**SQLGetDiagField**可以呼叫Sqlgetdiagfield 的 SQL_DIAG_ROW_NUMBER 來判斷資料列與包含該資料行。  
  
 針對所有這些 Sqlstate 可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除了 01xxx Sqlstate)，如果上一個或多個，但不是全部資料列的多重資料列的作業，就會發生錯誤，而且如果發生錯誤時，會傳回 SQL_ERROR，會傳回 SQL_SUCCESS_WITH_INFO單一資料列作業。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|字串或資料行所傳回的二進位資料會導致非空白的字元或二進位資料為非 NULL 的截斷。 如果是字串值，它就是向右截斷。|  
|01S01|資料列中的錯誤|擷取一或多個資料列時發生錯誤。<br /><br /> (如果 ODBC 3 時，會傳回此 SQLSTATE*.x*應用程式使用 ODBC 2*.x*驅動程式，可以忽略它。)|  
|01S06|嘗試擷取結果集傳回第一個資料列集之前|要求的資料列集重疊時 Sqlfetchscroll SQL_FETCH_PRIOR、 目前的位置已超出第一個資料列，且目前的資料列數目小於或等於資料列集大小的結果集的開頭。<br /><br /> 要求的資料列集重疊時 Sqlfetchscroll SQL_FETCH_PRIOR、 目前的位置已超過結果集的結尾，資料列集大小大於結果集大小的結果集的開頭。<br /><br /> 要求的資料列集重疊時 Sqlfetchscroll 即 sql_fetch_relative 但、 FetchOffset 是負值，而且 FetchOffset 的絕對值小於或等於資料列集大小的結果集的開頭。<br /><br /> 要求的資料列集重疊時 Sqlfetchscroll 即 SQL_FETCH_ABSOLUTE、 FetchOffset 是負值，而且 FetchOffset 的絕對值大於結果集大小的結果集的開頭，但小於或等於資料列集大小。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S07|小數位數截斷|傳回資料行的資料已遭截斷。 數值資料類型已截斷的數字的小數部分。 時間、 時間戳記，和間隔資料型別包含時間元件，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|結果集中的資料行的資料值無法轉換成資料類型所指定*TargetType*中**SQLBindCol**。<br /><br /> 資料類型為 SQL_C_BOOKMARK，繫結資料行 0，並且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE。<br /><br /> 資料類型為 SQL_C_VARBOOKMARK，繫結資料行 0 和 SQL_ATTR_USE_BOOKMARKS 陳述式屬性未設定為 SQL_UB_VARIABLE。|  
|07009|無效的描述元索引|驅動程式為 ODBC 2*.x*不支援的驅動程式**SQLExtendedFetch**，和資料行繫結中指定的資料行編號為 0。<br /><br /> 資料行 0 已繫結，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22001|字串資料，右邊遭截斷|可變長度的書籤，傳回的資料行已截斷。|  
|22002|需要指標變數，但是未提供|NULL 的資料提取到資料行的*StrLen_or_IndPtr*設定**SQLBindCol** (或所設定的 SQL_DESC_INDICATOR_PTR **SQLSetDescField**或**SQLSetDescRec**) 為 null 指標。|  
|22003|數值超出範圍|傳回一或多個繫結的資料行 （做為數值或字串） 的數值可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 如需詳細資訊，請參閱[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)中[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|無效的 datetime 格式|在結果集中的字元資料行已繫結至日期、 時間或時間戳記 C 結構，但資料行的值，分別無效的日期、 時間戳記。|  
|22012|除數為零|算術運算式中的值傳回，因而導致除數為零。|  
|22015|間隔欄位溢位|C 間隔類型指派從精確數值或 SQL 類型的間隔 [前置] 欄位中造成有效位數的遺失。<br /><br /> 當資料擷取至 C 間隔類型，時發生沒有 C 間隔類型中的 SQL 型別值的表示。|  
|22018|轉換規格的字元值無效|結果集中的字元資料行已繫結至 C 字元緩衝區，而且資料行包含字元集的緩衝區中沒有表示為一個字元。<br /><br /> C 類型為精確或大約的數字、 日期時間或間隔資料類型。資料行的 SQL 類型是字元資料類型。和資料行中的值不是有效的常值的繫結 C 類型。|  
|24000|指標狀態無效|*StatementHandle*目前處於執行狀態，但任何結果集與*StatementHandle*。|  
|40001|序列化失敗|擷取已執行的交易已結束避免死結。|  
|40003|未知的陳述式完成|相關聯的連接失敗，此函式，在執行期間，無法決定交易的狀態。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLFetchScroll**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 呼叫此函式時未先呼叫**SQLExecDirect**， **SQLExecute**或類別目錄函式。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) **SQLFetch**針對呼叫*StatementHandle*之後**SQLExtendedFetch**呼叫之前**SQLFreeStmt** SQL_ 與已呼叫關閉選項。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|SQL_ATTR_USE_BOOKMARK 陳述式屬性設定為 SQL_UB_VARIABLE，並繫結的緩衝區，其長度不等於此結果集的書籤的最大長度的資料行 0。 (這個長度隨附於 SQL_DESC_OCTET_LENGTH IRD 欄位中，可以藉由呼叫取得**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY106|提取類型超出範圍|DM) 指定 Sqlfetchscroll 的引數的值無效。<br /><br /> (DM) Sqlfetchscroll 引數是要使用 SQL_FETCH_BOOKMARK，並且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE 陳述式屬性的值是 SQL_CURSOR_FORWARD_ONLY，Sqlfetchscroll 未 SQL_FETCH_NEXT 的引數的值。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE 陳述式屬性的值為 SQL_NONSCROLLABLE 和 Sqlfetchscroll 未 SQL_FETCH_NEXT 的引數的值。|  
|HY107|資料列值超出範圍|SQL_ATTR_CURSOR_TYPE 陳述式屬性具有指定的值為 SQL_CURSOR_KEYSET_DRIVEN，但 SQL_ATTR_KEYSET_SIZE 陳述式屬性具有指定的值是大於 0 且小於 SQL_ATTR_ROW_ARRAY_ 與指定的值大小陳述式屬性。|  
|HY111|無效的書籤值|Sqlfetchscroll 引數是要使用 SQL_FETCH_BOOKMARK，而且 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性中的值所指向的書籤不正確，或為 null 指標。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援的組合所指定的轉換*TargetType*中**SQLBindCol**和對應的資料行的 SQL 資料類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 逾時期限是透過 SQLSetStmtAttr，sql_attr_query_timeout 時設定。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLFetchScroll**從結果集中傳回指定的資料列集。 絕對或相對位置或書籤，可以指定資料列集。 **SQLFetchScroll**可以被呼叫時才會存在結果集，也就是在呼叫之後，建立結果集和資料指標之前關閉結果集的移轉。 如果任何資料行繫結，它會傳回這些資料行中的資料。 如果應用程式具有指定資料列狀態陣列或其傳回的擷取，資料列數目的緩衝區的指標**SQLFetchScroll**這項資訊也會傳回。 呼叫**SQLFetchScroll**可以混合與呼叫**SQLFetch**但不能混合呼叫**SQLExtendedFetch**。  
  
 如需詳細資訊，請參閱[使用區塊資料指標](../../../odbc/reference/develop-app/using-block-cursors.md)和[使用可捲動資料指標](../../../odbc/reference/develop-app/using-scrollable-cursors.md)。  
  
## <a name="positioning-the-cursor"></a>定位資料指標  
 建立結果集時，資料指標位於結果集的開頭之前。 **SQLFetchScroll**根據的值將區塊游標置於*Sqlfetchscroll*和*FetchOffset*下表所示的引數。 確切的規則，以判斷新的資料列集的開頭會顯示在下一節。  
  
|Sqlfetchscroll|意義|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|傳回下一個資料列集。 這就相當於呼叫**SQLFetch**。<br /><br /> **SQLFetchScroll**會忽略此值的*FetchOffset*。|  
|SQL_FETCH_PRIOR|傳回先前的資料列集。<br /><br /> **SQLFetchScroll**會忽略此值的*FetchOffset*。|  
|SQL_FETCH_RELATIVE 但|傳回資料列集*FetchOffset*從目前的資料列集的開頭。|  
|SQL_FETCH_ABSOLUTE|傳回資料列集資料列開始*FetchOffset*。|  
|SQL_FETCH_FIRST|在結果集傳回第一個資料列集。<br /><br /> **SQLFetchScroll**會忽略此值的*FetchOffset*。|  
|SQL_FETCH_LAST|在結果集中傳回最後一個完整的資料列集。<br /><br /> **SQLFetchScroll**會忽略此值的*FetchOffset*。|  
|要使用 SQL_FETCH_BOOKMARK|傳回資料列集 FetchOffset 資料列從 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指定的書籤。|  
  
 驅動程式不需要支援所有 fetch 方向。應用程式呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （取決於資料指標的類型） 的資訊類型來判斷哪些提取驅動程式支援的方向。 應用程式應該查看在這些資訊類型 SQL_CA1_NEXT、 SQL_CA1_RELATIVE、 SQL_CA1_ABSOLUTE 和 WQL_CA1_BOOKMARK 位元遮罩。 此外，如果資料指標是順向和 Sqlfetchscroll 不 SQL_FETCH_NEXT， **SQLFetchScroll**傳回 SQLSTATE HY106 （提取類型超出範圍）。  
  
 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性會指定資料列集中的資料列數目。 如果所要提取的資料列集**SQLFetchScroll**重疊的結果集時，結尾**SQLFetchScroll**傳回部分資料列集。 也就是說，如果 S + R-1 是大於 L，其中 S 資料列集的提取，R 的起始資料列的是資料列集大小，和 L 是最後一個資料列在結果集中，然後只的第一個 L – S + 1 個資料列的資料列集都有效。 剩餘的資料列是空的且狀態為 SQL_ROW_NOROW。  
  
 之後**SQLFetchScroll**傳回目前的資料列是資料列集的第一個資料列。  
  
## <a name="cursor-positioning-rules"></a>資料指標定位規則  
 下列章節說明每個值的 Sqlfetchscroll 的確切規則。 這些規則會使用下列標記法。  
  
|表示法|意義|  
|--------------|-------------|  
|*開始之前*|區塊資料指標位於結果集的開頭之前。 如果新的資料列集的第一個資料列之前的結果集時，開始**SQLFetchScroll**傳回 sql_no_data 為止。|  
|*結束後*|區塊資料指標位於設定結果的結尾之後。 如果新的資料列集的第一個資料列之後的結果集時，結尾**SQLFetchScroll**傳回 sql_no_data 為止。|  
|*CurrRowsetStart*|中目前資料列集的第一個資料列數目。|  
|*LastResultRow*|在結果集中的最後一個資料列數目。|  
|*RowsetSize*|資料列集大小。|  
|*FetchOffset*|值*FetchOffset*引數。|  
|*BookmarkRow*|對應到 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指定的書籤的資料列。|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*開始之前*|1|  
|*CurrRowsetStart + RowsetSize*[1] * \<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*結束後*|  
|*結束後*|*結束後*|  
  
 [1] 如果自上次擷取資料列呼叫後已變更資料列集大小，這是前一次呼叫搭配使用的資料列集大小。  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*開始之前*|*開始之前*|  
|*CurrRowsetStart = 1*|*開始之前*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2]。</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart – RowsetSize* <sup>[2]</sup>|  
|*之後結束和 LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*之後結束和 LastResultRow > = RowsetSize* <sup>[2]</sup>|*LastResultRow – RowsetSize + 1* <sup>[2]。</sup>|  
  
 [1] **SQLFetchScroll**傳回 SQLSTATE 01S06 （嘗試的結果集傳回第一個資料列集之前提取） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自上次擷取資料列呼叫後已變更資料列集大小，這是新的資料列集大小。  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE 但  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*(之前啟動和 FetchOffset > 0)或者 (之後結束和 FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart 和 FetchOffset < = 0*|*開始之前*|  
|*CurrRowsetStart = 1 AND FetchOffset < 0*|*開始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124;FetchOffset &#124;> RowsetSize* <sup>[3]</sup>|*開始之前*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124;FetchOffset &#124;< = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*結束後*|  
|*之後結束和 FetchOffset > = 0*|*結束後*|  
  
 [1] ***SQLFetchScroll***傳回相同的資料列集，如同使用 Sqlfetchscroll 設 SQL_FETCH_ABSOLUTE 呼叫它。 如需詳細資訊，請參閱"SQL_FETCH_ABSOLUTE 」 一節。  
  
 [2] **SQLFetchScroll**傳回 SQLSTATE 01S06 （嘗試的結果集傳回第一個資料列集之前提取） 和 SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果自上次擷取資料列呼叫後已變更資料列集大小，這是新的資料列集大小。  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124;FetchOffset &#124;< = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 AND &#124;FetchOffset &#124;> LastResultRow AND &#124;FetchOffset &#124;> RowsetSize* <sup>[2]</sup>|*開始之前*|  
|*FetchOffset < 0 AND &#124;FetchOffset &#124;> LastResultRow AND &#124;FetchOffset &#124;< = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*開始之前*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*結束後*|  
  
 [1] **SQLFetchScroll**傳回 SQLSTATE 01S06 （嘗試的結果集傳回第一個資料列集之前提取） 和 SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自上次擷取資料列呼叫後已變更資料列集大小，這是新的資料列集大小。  
  
 針對動態資料指標執行的絕對提取無法提供所需的結果，因為動態資料指標中的資料列位置是不明。 這類作業相當於 fetch，接著再設定 fetch relative;它不是不可部分完成的作業，因為靜態資料指標上的絕對提取。  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow – RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] 如果自上次擷取資料列呼叫後已變更資料列集大小，這是新的資料列集大小。  
  
## <a name="sqlfetchbookmark"></a>要使用 SQL_FETCH_BOOKMARK  
 套用下列規則。  
  
|條件|新的資料列集的第一個資料列|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*開始之前*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*結束後*|  
  
 如需書籤的詳細資訊，請參閱[書籤 (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md)。  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>已刪除、 加入，效果和在資料指標移動的錯誤資料列  
 靜態和索引鍵集驅動資料指標有時候偵測設定加入至結果的資料列，並移除從結果集中刪除資料列。 藉由呼叫**SQLGetInfo** SQL_KEYSET_CURSOR_ATTRIBUTES2 SQL_STATIC_CURSOR_ATTRIBUTES2 與選項，並查看 SQL_CA2_SENSITIVITY_ADDITIONS、 SQL_CA2_SENSITIVITY_DELETIONS 和 SQL_CA2_SENSITIVITY_更新遮罩，應用程式會決定是否實作特定的驅動程式的資料指標執行這項操作。 驅動程式可以偵測已刪除的資料列，並將它們移除，如下列段落說明此行為的影響。 驅動程式，可以偵測已刪除的資料列，但無法將它們移除，刪除已不會影響資料指標移動，並不會套用下列段落。  
  
 如果資料指標偵測到資料列加入至結果集，或移除從結果集中刪除資料列，則會出現如同時偵測到這些變更只提取資料。 這包括案例時**SQLFetchScroll**稱為 Sqlfetchscroll 設 sql_fetch_relative 但和 FetchOffset 設定為 0，重新擷取相同的資料列集，但不包含大小寫，fOption 設 SQL_ 呼叫 SQLSetPos 時重新整理。 在後者的情況下，重新整理的資料列集的緩衝區中的資料，但不是 refetched，和已刪除的資料列不會移除從結果集。 因此，當資料列遭到刪除或插入至目前的資料列集，資料指標不會修改的資料列集的緩衝區。 相反地，它會偵測變更它擷取任何資料列的先前包含刪除的資料列，或是現在插入的資料列。  
  
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
  
 當**SQLFetchScroll**傳回新的資料列集具有相對於目前資料列集的位置 — 也就是 Sqlfetchscroll 是 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR 或 sql_fetch_relative，但 — 不包含目前資料列集的變更當計算新的資料列集的開始位置。 不過，其中包括目前的資料列集之外的變更是否能夠偵測它們。 此外，當**SQLFetchScroll**傳回新的資料列集有獨立的目前資料列集的位置，也就是 Sqlfetchscroll 是 SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE 或要使用 SQL_FETCH_BOOKMARK — 它包含它是能夠偵測，即使是在目前的資料列集中的所有變更。  
  
 在決定新加入的資料列是否為內部或外部的目前資料列集時，部分的資料列集視為有效的最後一個資料列; 在結束也就是說，其中的資料列狀態不是 SQL_ROW_NOROW 的最後一個資料列。 例如，假設資料指標是能夠偵測新加入的資料列、 目前的資料列集是部分的資料列集、 在應用程式新增新的資料列和資料指標會將這些資料列加入至結果集的結尾。 如果應用程式呼叫**SQLFetchScroll** Sqlfetchscroll 設 SQL_FETCH_NEXT，與**SQLFetchScroll**傳回資料列集的第一個新加入的資料列開始。  
  
 例如，假設目前的資料列集包含資料列 21 到 30、 資料列集大小為 10、 資料指標會移除從結果集中，刪除資料列和資料指標偵測到資料列加入至結果集。 下表顯示的資料列**SQLFetchScroll**在各種情況下會傳回。  
  
|變更|提取類型|FetchOffset|新的資料列集 [1]|  
|------------|----------------|-----------------|---------------------|  
|刪除資料列 21|NEXT|0|31 到 40|  
|刪除資料列 31|NEXT|0|32 到 41|  
|插入資料列 21 歲到 22 之間的資料列|NEXT|0|31 到 40|  
|插入資料列 30 和 31 之間的資料列|NEXT|0|插入的資料列，31 到 39|  
|刪除資料列 21|PRIOR|0|11 到 20|  
|刪除資料列 20|PRIOR|0|10 至 19|  
|插入資料列 21 歲到 22 之間的資料列|PRIOR|0|11 到 20|  
|插入資料列 20 和 21 之間的資料列|PRIOR|0|12 到 20，插入的資料列|  
|刪除資料列 21|RELATIVE|0|22 到 31<sup>[2]</sup>|  
|刪除資料列 21|RELATIVE|1|22 到 31|  
|插入資料列 21 歲到 22 之間的資料列|RELATIVE|0|21，插入資料列，22 到 29|  
|插入資料列 21 歲到 22 之間的資料列|RELATIVE|1|22 到 31|  
|刪除資料列 21|ABSOLUTE|21|22 到 31<sup>[2]</sup>|  
|刪除資料列 22|ABSOLUTE|21|21，23 到 31|  
|插入資料列 21 歲到 22 之間的資料列|ABSOLUTE|22|插入的資料列，22 到 29|  
  
 [1] 此資料行使用的資料列號碼之前插入或刪除任何資料列。  
  
 [2] 在此情況下，資料指標會嘗試傳回資料列 21 開始的資料列。 因為已刪除資料列 21，它會傳回第一個資料列是資料列 22。  
  
 錯誤資料列 （亦即，資料列狀態 SQL_ROW_ERROR） 不會影響資料指標移動。 例如，如果目前資料列集的資料列 11 及狀態資料列 11 是 SQL_ROW_ERROR 呼叫**SQLFetchScroll** Sqlfetchscroll 設 sql_fetch_relative 但和 FetchOffset 設為 5 會傳回 16，資料列開始的資料列集就像資料列 11 的狀態是 SQL_SUCCESS 一樣。  
  
## <a name="returning-data-in-bound-columns"></a>繫結資料行中傳回資料  
 **SQLFetchScroll**繫結資料行中傳回資料做為相同的方式**SQLFetch**。 如需詳細資訊，請參閱 「 傳回資料中繫結資料行 」 中[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
 如果沒有資料行繫結， **SQLFetchScroll**未傳回的資料，但未將區塊資料指標移至指定的位置。 是否可以從使用區塊資料指標的未繫結的資料行擷取資料**SQLGetData**取決於驅動程式。 如果呼叫，這項功能支援**SQLGetInfo**傳回 SQL_GD_BLOCK SQL_GETDATA_EXTENSIONS 資訊類型的位元。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 **SQLFetchScroll**使用相同的公式來判斷做為資料和長度/指標緩衝區的位址**SQLFetch**。 如需詳細資訊，請參閱 「 緩衝區位址 」 [SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 **SQLFetchScroll** SQLFetch 相同方式設定資料列狀態陣列中的值。 如需詳細資訊，請參閱 「 資料列狀態陣列" [SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="rows-fetched-buffer"></a>擷取緩衝區資料列。  
 **SQLFetchScroll**傳回以相同的方式提取資料列提取緩衝區中的資料列數目**SQLFetch**。 如需詳細資訊，請參閱 「 資料列提取緩衝區 」 中的[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="error-handling"></a>錯誤處理  
 當應用程式呼叫**SQLFetchScroll** ODBC 3.x 驅動程式，在驅動程式管理員會呼叫**SQLFetchScroll**驅動程式中。 當應用程式呼叫**SQLFetchScroll** ODBC 2.x 驅動程式，在驅動程式管理員會呼叫 SQLExtendedFetch 驅動程式中。 因為**SQLFetchScroll**和 SQLExtendedFetch 稍有不同的方式處理錯誤、 應用程式稍有不同的錯誤行為時看到它會呼叫**SQLFetchScroll**在 ODBC 2.x 和 ODBC3.x 驅動程式。  
  
 **SQLFetchScroll**以相同的方式傳回錯誤和警告**SQLFetch**; 如需詳細資訊，請參閱 「 錯誤處理" **SQLFetch**。 **SQLExtendedFetch**以相同的方式傳回錯誤**SQLFetch**，但有下列例外狀況：  
  
 警告發生時，適用於資料列集中的特定資料列，則 SQLExtendedFetch 設定 SQL_ROW_SUCCESS，不 SQL_ROW_SUCCESS_WITH_INFO 資料列狀態陣列中對應的項目。  
  
 如果資料列集中的每個資料列中發生錯誤，SQLExtendedFetch 會傳回 SQL_SUCCESS_WITH_INFO，不 SQL_ERROR。  
  
 在每個群組套用到個別的資料列狀態記錄，第一個 SQLExtendedFetch 所傳回的狀態記錄必須包含 SQLSTATE 01S01 （錯誤資料列中的）;**SQLFetchScroll**不會傳回此 SQLSTATE。 如果無法傳回其他 Sqlstate SQLExtendedFetch，它仍必須傳回此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和開放式並行存取  
 如果資料指標使用開放式並行存取，也就是 SQL_ATTR_CONCURRENCY 陳述式屬性具有 SQL_CONCUR_VALUES 或值 SQL_CONCUR_ROWVER — **SQLFetchScroll**更新資料所使用的開放式並行存取值若要偵測是否已變更的資料列的來源。 發生這種情況時**SQLFetchScroll**擷取新資料列集，包括它 refetches 目前資料列集。 （它是使用設 sql_fetch_relative 但和 FetchOffset 設為 0 的 Sqlfetchscroll 呼叫）。  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驅動程式  
 當應用程式呼叫**SQLFetchScroll** ODBC 2.x 驅動程式，驅動程式管理員會對應至這個呼叫**SQLExtendedFetch**。 將傳遞的引數的下列值**SQLExtendedFetch**。  
  
|SQLExtendedFetch 引數|值|  
|-------------------------------|-----------|  
|StatementHandle|在 StatementHandle **SQLFetchScroll**。|  
|Sqlfetchscroll|中的 Sqlfetchscroll **SQLFetchScroll**。|  
|FetchOffset|Sqlfetchscroll 不是要使用 SQL_FETCH_BOOKMARK FetchOffset 引數中的值**SQLFetchScroll**用。<br /><br /> 如果要使用 SQL_FETCH_BOOKMARK Sqlfetchscroll，使用 SQL_ATTR_FETCH_BOOKMARK_PTR 陳述式屬性所指定的位址儲存的值。|  
|RowCountPtr|將 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性所指定的位址。|  
|RowStatusArray|將 sql_attr_row_status_ptr 設定陳述式屬性所指定的位址。|  
  
 如需詳細資訊，請參閱[區塊資料指標，可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附錄 g： 驅動程式的指導方針回溯相容性。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>描述項和 SQLFetchScroll  
 **SQLFetchScroll**互動以相同方式的描述元**SQLFetch**。 如需詳細資訊，請參閱 」 描述元和 SQLFetchScroll 」 一節[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)，[資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)，[定位 Update 和 Delete 陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)，和[SQLSetPos以更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行大量插入、 更新或刪除作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回結果集內的資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|擷取單一資料列或資料區塊的順向的方向|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|關閉資料指標的陳述式上|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回結果集資料行|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位資料指標，重新整理此資料列集中，或更新或刪除在結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

