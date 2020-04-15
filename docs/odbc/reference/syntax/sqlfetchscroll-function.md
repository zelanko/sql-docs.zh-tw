---
title: SQLFetchScroll 函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6c65ef71f5c2cb9202ab788cac5e00357674f4a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285878"
---
# <a name="sqlfetchscroll-function"></a>SQLFetchScroll 函數
**一致性**  
 推出版本: ODBC 3.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLFetchScroll**從結果集中獲取指定的數據列集,並返回所有綁定列的數據。 行集可以在絕對或相對位置或通過書籤指定。  
  
 使用 ODBC 2.x 驅動程式時,驅動程式管理員將此函數映射到**SQLExtendedFetch**。 有關詳細資訊,請參閱[映射應用程式向後相容性的替代函數](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *擷取方向*  
 [輸入]  
  
 擷取型態:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 有關詳細資訊,請參閱"註釋"部分中的"定位游標"。  
  
 *擷取位移*  
 [輸入]  
  
 要提取的行數。 此參數的解釋取決於*Fetch 方向*參數的值。 有關詳細資訊,請參閱"註釋"部分中的"定位游標"。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetchScroll**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的句柄類型和語句句柄。 下表列出了**SQLFetchScroll**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。 如果單個列上發生錯誤,可以使用 SQL_DIAG_COLUMN_NUMBER的 Diag標識符調用**SQLGetDiagField**以確定錯誤發生的列;和**SQLGetDiagField**可以使用SQL_DIAG_ROW_NUMBER的 Diag 識別符調用,以確定包含該列的行。  
  
 對於可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT(01xxx SQLSTATEs 除外),如果多行操作的一個或多個行發生錯誤(但不是全部)發生錯誤,則返回SQL_SUCCESS_WITH_INFO,如果單行操作發生錯誤,則返回SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|為列返回的字串或二進位資料導致非空白字元或非 NULL 二進位資料的截斷。 如果它是一個字串值,它是右截斷的。|  
|01S01|行中的錯誤|獲取一個或多個行時出錯。<br /><br /> (如果在 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式時返回此 SQLSTATE,則可以忽略它。|  
|01S06|嘗試在結果集傳回第一個行集之前擷取|請求的行集與提取方向時的結果集的開始重疊,當 Fetch 方向SQL_FETCH_PRIOR,當前位置超過第一行,並且當前行的數量小於或等於行集大小。<br /><br /> 請求的行集與結果集的開始重疊,當 Fetch 方向SQL_FETCH_PRIOR,當前位置超出結果集的末尾,並且行集大小大於結果集大小。<br /><br /> 請求的行集與結果集的開始重疊,當 Fetch 方向SQL_FETCH_RELATIVE時,FetchOffset 為負值,FetchOffset 的絕對值小於或等於行集大小。<br /><br /> 請求的行集與提取方向 SQL_FETCH_ABSOLUTE時的結果集的開始重疊,FetchOffset 為負,FetchOffset 的絕對值大於結果集大小,但小於或等於行集大小。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S07|分數截斷|為列返回的數據被截斷。 對於數位數據類型,數位的小數部分被截斷。 對於包含時間元件的時間、時間戳和間隔數據類型,時間的小數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|無法將結果集中欄資料值轉換為**SQLBindCol**中*TargetType*指定的數據類型。<br /><br /> 列 0 與SQL_C_BOOKMARK數據類型綁定,SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE。<br /><br /> 列 0 與數據類型SQL_C_VARBOOKMARK綁定,並且SQL_ATTR_USE_BOOKMARKS語句屬性未設置為SQL_UB_VARIABLE。|  
|07009|不合法的描述符索引|驅動程式是不支援**SQLExtendedFetch**的 ODBC 2 *.x*驅動程式,在列綁定中指定的列編號為 0。<br /><br /> 列 0 已綁定,SQL_ATTR_USE_BOOKMARKS 語句屬性設置為SQL_UB_OFF。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22001|字串資料,右截斷|為列返回的可變長度書籤被截斷。|  
|22002|需要指標變數,但未提供|NULL 資料被提取到一個列*中,* 該列StrLen_or_IndPtr由**SQLBindCol**設定(或由**SQLSetDescField**或**SQLSetDescRec**設定SQL_DESC_INDICATOR_PTR)為空指標。|  
|22003|數值超範圍|返回一個或多個綁定列的數值(作為數位或字串)將導致數字的整個部分(而不是小數)被截斷。<br /><br /> 關於詳細資訊,請參考[在附錄 D:資料型態](../../../odbc/reference/appendixes/appendix-d-data-types.md)中[將資料從 SQL 轉換為 C 資料型態](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。|  
|22007|不合法日期時間格式|結果集中的字元列綁定到日期、時間或時間戳 C 結構,並且列中的值分別是無效的日期、時間或時間戳。|  
|22012|除零|返回算術表達式中的值,結果除以零。|  
|22015|間隔欄位溢出|從精確數位或間隔 SQL 類型分配給間隔 C 類型會導致前導欄位中的重要數位丟失。<br /><br /> 將資料提取到間隔 C 類型時,間隔 C 類型中沒有 SQL 類型的值表示形式。|  
|22018|強制轉換規範的不合法字元值|結果集中的字元列綁定到字元 C 緩衝區,該列包含緩衝區的字元集中沒有表示的字元。<br /><br /> C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。|  
|24000|指標狀態無效|*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。|  
|40001|序列化失敗|執行提取的事務已終止,以防止死鎖。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLFetchScroll**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 指定的*語句句柄*未處於執行狀態。 調用該函數時沒有首先調用**SQLExecDirect、SQLExecute**或目錄函**SQLExecute**數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) **SQLFetch**在呼叫**SQLExtendedFetch**後與使用SQL_CLOSE選項的**SQLFreeStmt**之前呼叫 *。*|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|SQL_ATTR_USE_BOOKMARK語句屬性設置為SQL_UB_VARIABLE,第 0 列綁定到長度不等於此結果集書簽的最大長度的緩衝區。 (此長度在 IRD 的SQL_DESC_OCTET_LENGTH欄位中可用,可以通過呼叫**SQLDescribeCol、SQLColattribute**或**SQLGetDescField**獲得。 **SQLColAttribute**|  
|HY106|擷取類型範圍外|DM) 為參數 Fetch 方向指定的值無效。<br /><br /> (DM) 參數 Fetch 方向SQL_FETCH_BOOKMARK,SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF。<br /><br /> SQL_ATTR_CURSOR_TYPE語句屬性的值SQL_CURSOR_FORWARD_ONLY,並且參數 Fetch 方向的值不SQL_FETCH_NEXT。<br /><br /> SQL_ATTR_CURSOR_SCROLLABLE語句屬性的值是SQL_NONSCROLLABLE,並且參數 Fetch 方向的值不SQL_FETCH_NEXT。|  
|HY107|行值範圍外|使用SQL_ATTR_CURSOR_TYPE語句屬性指定的值SQL_CURSOR_KEYSET_DRIVEN,但使用SQL_ATTR_KEYSET_SIZE語句屬性指定的值大於 0,小於使用SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定的值。|  
|HY111|不合法的書籤值|參數 FetchOrientation 是SQL_FETCH_BOOKMARK的,並且SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性中的值指向的書籤無效或為空指標。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*和相應列的 SQL 資料類型的組合指定的轉換。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回請求的結果集之前已過期。 超時期間通過 SQL_ATTR_QUERY_TIMEOUT 的 SQLSetStmtAttr 設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQLFetchScroll**從結果集中返回指定的行集。 行集可以由絕對或相對位置或書籤指定。 **SQLFetchScroll**只能在存在結果集時調用 ,即在創建結果集的調用之後以及該結果集上的游標關閉之前。 如果綁定任何列,它將返回這些列中的數據。 如果應用程式指定了指向行狀態陣列的指標或用於返回提取的行數的緩衝區 **,SQLFetchScroll**也返回此資訊。 對**SQLFetchScroll 的**呼叫可以與**SQLFetch**的調用混合,但不能與**SQLAaFetch 的**調用混合。  
  
 有關詳細資訊,請參閱[使用區塊游標](../../../odbc/reference/develop-app/using-block-cursors.md)[與使用可捲軸](../../../odbc/reference/develop-app/using-scrollable-cursors.md)。  
  
## <a name="positioning-the-cursor"></a>定位游標  
 創建結果集時,游標位於結果集開始之前。 **SQLFetchScroll**基於 *「取取方向」* 和「*擷取偏移*」參數的值定位塊游標,如下表所示。 確定新行集開始的確切規則將顯示在下一節中。  
  
|擷取方向|意義|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|返回下一個行集。 這相當於調用**SQLFetch。**<br /><br /> **SQLFetchScroll**忽略*取偏移*的值。|  
|SQL_FETCH_PRIOR|返回以前的行集。<br /><br /> **SQLFetchScroll**忽略*取偏移*的值。|  
|SQL_FETCH_RELATIVE|從當前行集的開頭返回行集 *「提取偏移*」。。|  
|SQL_FETCH_ABSOLUTE|返回從行*提取偏移*開始的行集。|  
|SQL_FETCH_FIRST|返回結果集中的第一個行集。<br /><br /> **SQLFetchScroll**忽略*取偏移*的值。|  
|SQL_FETCH_LAST|返回結果集中的最後一個完整行集。<br /><br /> **SQLFetchScroll**忽略*取偏移*的值。|  
|SQL_FETCH_BOOKMARK|從SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性指定的書籤返回行集 FetchOffset 行。|  
  
 驅動程式不需要支援所有提取方向;應用程式呼叫**SQLGetInfo**的資訊類型為 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或SQL_STATIC_CURSOR_ATTRIBUTES1(取決於游標的類型),以確定驅動程式支援哪些提取方向。 應用程式應查看這些資訊類型中SQL_CA1_NEXT、SQL_CA1_RELATIVE、SQL_CA1_ABSOLUTE和WQL_CA1_BOOKMARK位掩碼。 此外,如果游標是僅轉發的,並且取取方向不是**SQL_FETCH_NEXT,SQLFetchScroll**將返回 SQLSTATE HY106(提取類型不在範圍)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定行集中的行數。 如果**SQLFetchScroll**提取的行集與結果集的末尾重疊,則**SQLFetchScroll**返回一個部分行集。 也就是說,如果 S + R - 1 大於 L,其中 S 是要提取的行集的起始行,R 是行集大小,而 L 是結果集中的最後一行,則只有排集的前一行 L - S = 1 行有效。 其餘行為空,狀態為 SQL_ROW_NOROW。  
  
 **SQLFetchScroll**返回後,當前行是行集的第一行。  
  
## <a name="cursor-positioning-rules"></a>游標定位規則  
 以下各節介紹取取方向的每個值的確切規則。 這些規則使用以下表示法。  
  
|表示法|意義|  
|--------------|-------------|  
|*開始之前*|塊游標位於結果集開始之前。 如果新行集的第一行位於結果集開始之前,**則 SQLFetchScroll**返回SQL_NO_DATA。|  
|*結束後*|塊游標位於結果集結束之後。 如果新行集的第一行位於結果集結束后,**則 SQLFetchScroll**返回SQL_NO_DATA。|  
|*CurrRowset 開始*|當前行集中的第一行的編號。|  
|*最後一個結果列*|結果集中的最後一行的編號。|  
|*行集大小*|行集大小。|  
|*擷取位移*|*提取偏移*參數的值。|  
|*書籤行*|與SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性指定的書籤對應的行。|  
  
## <a name="sql_fetch_next"></a>SQL_FETCH_NEXT  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*開始之前*|1|  
|*CurrRowset 開始 = 行集大小*[1] * \<= 最後一個結果行*|*CurrRowset 開始 = 行集大小*[1]|  
|*CurrRowset 開始 = 行集大小** [1]>最后结果行*|*結束後*|  
|*結束後*|*結束後*|  
  
 {1} 如果自上次調用以提取行以來,行集大小已更改,則這是與上一個調用一起使用的行集大小。  
  
## <a name="sql_fetch_prior"></a>SQL_FETCH_PRIOR  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*開始之前*|*開始之前*|  
|*CurrRowset 開始 = 1*|*開始之前*|  
|*1 < CurrRowset 開始<= 行集大小* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*CurrRowset 開始>行集大小* <sup>[2]</sup>|*CurrRowset 開始 - 行集大小* <sup>[2]</sup>|  
|*結束後和最後一個結果行<行集大小* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*結束和最後的結果列>= 行集大小* <sup>[2]</sup>|*前一個結果行 - 行集大小 = 1* <sup>[2]</sup>|  
  
 [1] **SQLFetchScroll**傳回 SQLSTATE 01S06(嘗試在結果集返回第一個行集之前提取)和SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自上次調用以提取行以來,行集大小已更改,則這是新的行集大小。  
  
## <a name="sql_fetch_relative"></a>SQL_FETCH_RELATIVE  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*(啟動前和提取偏移> 0)OR(結束後和提取偏移< 0)*|*--*<sup>[1]</sup>|  
|*啟動並擷取偏移<= 0*|*開始之前*|  
|*CurrRowset 開始 = 1 和擷取偏移量< 0*|*開始之前*|  
|*currRowset 開始> 1 和 Currrowset 開始 = 提取偏移< 1 和&#124;提取偏移量 &#124; > 行集大小* <sup>[3]</sup>|*開始之前*|  
|*currRowset 開始> 1 和 Currrowset 開始 = 提取偏移< 1 和&#124;提取偏移 &#124; <= 行集大小* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 <= CurrRowset\<開始 = 擷取位移數 = 上次結果行*|*CurrRowset 開始 + 提取位移*|  
|*CurrRowset 開始 = 擷取偏移>最後結果行*|*結束後*|  
|*結束後和提取偏移量>= 0*|*結束後*|  
  
 [1] ***SQLFetchScroll***返回相同的行集,就好像它被調用時,Fetch方向設置為SQL_FETCH_ABSOLUTE。 有關詳細資訊,請參閱"SQL_FETCH_ABSOLUTE"部分。  
  
 [2] **SQLFetchScroll**傳回 SQLSTATE 01S06(嘗試在結果集返回第一個行集之前提取)和SQL_SUCCESS_WITH_INFO。  
  
 [3] 如果自上次調用以提取行以來,行集大小已更改,則這是新的行集大小。  
  
## <a name="sql_fetch_absolute"></a>SQL_FETCH_ABSOLUTE  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*擷取偏移量< 0 和&#124;提取偏移量 &#124; <= 上一個結果行*|*前一個結果列 = 取取位移數 = 1*|  
|*提取偏移< 0 和 &#124; 提取偏移量 &#124; > 上一個結果行和&#124;提取偏移量 &#124; > 行集大小* <sup>[2]</sup>|*開始之前*|  
|*提取偏移< 0 和&#124;提取偏移量 &#124; > 最後結果行和&#124;提取偏移量 &#124; <= 行集大小* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*擷取位移量 = 0*|*開始之前*|  
|*1 <\<= 取取位移 = 上次結果列*|*擷取位移*|  
|*擷取偏移>最後一個結果行*|*結束後*|  
  
 [1] **SQLFetchScroll**傳回 SQLSTATE 01S06(嘗試在結果集返回第一個行集之前提取)和SQL_SUCCESS_WITH_INFO。  
  
 [2] 如果自上次調用以提取行以來,行集大小已更改,則這是新的行集大小。  
  
 對動態游標執行的絕對提取無法提供所需的結果,因為動態游標中的行位置尚未確定。 此類操作等效於先提取,後跟提取相對;它不是原子操作,靜態游標上的絕對提取也是原子操作。  
  
## <a name="sql_fetch_first"></a>SQL_FETCH_FIRST  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*任何*|*1*|  
  
## <a name="sql_fetch_last"></a>SQL_FETCH_LAST  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*行集大小* <sup>[1]</sup> <= 上次結果列|*上次結果列 - 行集大小 = 1* <sup>[1]</sup>|  
|*行集大小* <sup>[1]</sup> >最后一个结果行|*1*|  
  
 [1] 如果自上次調用以提取行以來已更改行集大小,則這是新的行集大小。  
  
## <a name="sql_fetch_bookmark"></a>SQL_FETCH_BOOKMARK  
 以下規則適用。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|*書籤行 = 取取偏移< 1*|*開始之前*|  
|*1<= 書籤\<行 = 取取偏移量 = 上一個結果行*|*書籤行 = 取取位移*|  
|*書籤行 = 提取偏移>最後結果行*|*結束後*|  
  
 有關書籤的資訊,請參閱書籤[(ODBC)。](../../../odbc/reference/develop-app/bookmarks-odbc.md)  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>移除、新增和錯誤行對游標移動的影響  
 靜態和鍵集驅動的遊標有時檢測添加到結果集的行,並刪除從結果集中刪除的行。 通過使用SQL_STATIC_CURSOR_ATTRIBUTES2和SQL_KEYSET_CURSOR_ATTRIBUTES2選項調用**SQLGetInfo**並查看SQL_CA2_SENSITIVITY_ADDITIONS、SQL_CA2_SENSITIVITY_DELETIONS和SQL_CA2_SENSITIVITY_UPDATES位掩碼,應用程式確定由特定驅動程序實現的遊標是否執行此操作。 對於可以檢測已刪除行並刪除行的驅動程式,以下段落將描述此行為的效果。 對於可以檢測已刪除行但無法刪除行的驅動程式,刪除對游標移動沒有影響,並且以下段落不適用。  
  
 如果游標檢測到添加到結果集的行或刪除從結果集中刪除的行,則它看起來好像僅在獲取數據時檢測到這些更改。 這包括將**SQLFetchScroll**調用時,提取方向設置為SQL_FETCH_RELATIVE,FetchOffset 設置為 0 以重新提取相同的行集,但不包括在使用 fOption 設置為 SQL_REFRESH時調用 SQLSetPos 的情況。 在後一種情況下,將刷新行集緩衝區中的數據,但不會重新提取,並且不會從結果集中刪除已刪除的行。 因此,當從當前行集中刪除行或插入到當前行集時,游標不會修改行集緩衝區。 相反,當它獲取以前包含已刪除行或現在包含插入的行的任何行集時,它會檢測到更改。  
  
 例如：  
  
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
  
 當**SQLFetchScroll**傳回具有相對於當前行集的位置的新行集時(即 Fetch 方向是SQL_FETCH_NEXT、SQL_FETCH_PRIOR或SQL_FETCH_RELATIVE - 在計算新行集的起始位置時,它不包括對當前行集的更改。 但是,如果能夠檢測到當前行集之外的更改,它確實包括更改。 此外,當**SQLFetchScroll**返回具有獨立於當前行集的位置的新行集時(即 Fetch 方向是SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE或SQL_FETCH_BOOKMARK - 它包括它能夠檢測到的所有更改,即使這些更改位於當前行集中。  
  
 在確定新添加的行是在當前行集內部還是外部時,部分行集被視為在最後一個有效行結束;即行狀態未SQL_ROW_NOROW的最後一行。 例如,假設游標能夠檢測新添加的行,當前行集是部分行集,應用程式添加新行,游標將這些行添加到結果集的末尾。 如果應用程式呼叫**SQLFetchScroll,** 提取方向設定為**SQL_FETCH_NEXT,SQLFetchScroll**將返回從第一個新添加的行開始的行集。  
  
 例如,假設當前行集包含第 21 行到 30 行,行集大小為 10,游標刪除從結果集中刪除的行,並且游標檢測添加到結果集的行。 下表顯示了**SQLFetchScroll**在各種情況下返回的行。  
  
|變更|擷取類型|擷取位移|新排集[1]|  
|------------|----------------|-----------------|---------------------|  
|刪除行 21|NEXT|0|31 到 40|  
|刪除列 31|NEXT|0|32 到 41|  
|在第 21 行與第 22 行之間插入列|NEXT|0|31 到 40|  
|在第 30 行與第 31 行之間插入列|NEXT|0|插入行,31 到 39|  
|刪除行 21|PRIOR|0|11 到 20|  
|刪除行 20|PRIOR|0|10 到 19|  
|在第 21 行與第 22 行之間插入列|PRIOR|0|11 到 20|  
|在第 20 行與第 21 行之間插入列|PRIOR|0|12 到 20 插入的行|  
|刪除行 21|RELATIVE|0|22 到 31<sup>[2]</sup>|  
|刪除行 21|RELATIVE|1|22 到 31|  
|在第 21 行與第 22 行之間插入列|RELATIVE|0|21,插入行,22 到 29|  
|在第 21 行與第 22 行之間插入列|RELATIVE|1|22 到 31|  
|刪除行 21|ABSOLUTE|21|22 到 31<sup>[2]</sup>|  
|刪除行 22|ABSOLUTE|21|21, 23 到 31|  
|在第 21 行與第 22 行之間插入列|ABSOLUTE|22|插入的行,22 到 29|  
  
 [1] 在插入或刪除任何行之前,此列使用行號。  
  
 [2] 在這種情況下,遊標嘗試返回以第 21 行開頭的行。 由於第 21 行已被刪除,因此返回的第一行是第 22 行。  
  
 錯誤行(即狀態為SQL_ROW_ERROR的行)不會影響游標移動。 例如,如果當前行集以第 11 行開頭,並且第 11 行的狀態為SQL_ROW_ERROR,則使用 Fetch 方向設置為「取向」設置為「SQL_FETCH_RELATIVE」調用**SQLFetchScroll,** 並將 FetchOffset 設置為 5 返回從第 16 行開始的行集,就像該行 11 的狀態SQL_SUCCESS一樣。  
  
## <a name="returning-data-in-bound-columns"></a>在繫結列中傳回資料  
 **SQLFetchScroll**傳回繫定列中的數據的方式與**SQLFetch**相同。 有關詳細資訊,請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的"在綁定列中返回數據」。  
  
 如果未綁定列 **,SQLFetchScroll**不會返回資料,但會將塊游標移動到指定位置。 能否使用**SQLGetData**從塊游標的未綁定列中檢索數據取決於驅動程式。 如果調用**SQLGetInfo**返回SQL_GETDATA_EXTENSIONS資訊類型的SQL_GD_BLOCK位,則支援此功能。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 **SQLFetchScroll**使用相同的公式來確定數據和長度/指標緩衝區的位址與**SQLFetch。** 有關詳細資訊,請參閱[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 **SQLFetchScroll**以與 SQLFetch 相同的方式設定行狀態陣列中的值。 有關詳細資訊,請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的「行狀態陣列」。。  
  
## <a name="rows-fetched-buffer"></a>行擷取緩衝區  
 **SQLFetchScroll**返回行提取緩衝區中的行數,其方式與**SQLFetch**相同。 有關詳細資訊,請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的「行提取緩衝區」。。  
  
## <a name="error-handling"></a>錯誤處理  
 當應用程式在 ODBC 3.x 驅動程式中呼叫**SQLFetchScroll**時,驅動程式管理器在驅動程式中呼叫**SQLFetchScroll。** 當應用程式在 ODBC 2.x 驅動程式中呼叫**SQLFetchScroll**時,驅動程式管理器在驅動程式中呼叫 SQLExtendedFetch。 由於**SQLFetchScroll**和 SQLAaFetch 處理錯誤的方式略有不同,因此應用程式在 ODBC 2.x 和 ODBC 3.x 驅動程式中調用**SQLFetchScroll**時,會看到略有不同的錯誤行為。  
  
 **SQLFetchScroll**以與**SQLFetch**相同的方式傳回錯誤和警告。有關詳細資訊,請參閱**SQLFetch**中的"錯誤處理"。 **SQLExtendedFetch**傳回錯誤的方式與**SQLFetch**相同,但有以下例外情況:  
  
 當發生適用於行集中特定行的警告時,SQLExtendedFetch 將行狀態陣列中的相應條目設置為SQL_ROW_SUCCESS,而不是SQL_ROW_SUCCESS_WITH_INFO。  
  
 如果行集中的每一行都出現錯誤,SQLExtendedFetch 將返回SQL_SUCCESS_WITH_INFO,而不是SQL_ERROR。  
  
 在應用於單個行的每個狀態記錄中,SQLExtendedFetch 返回的第一個狀態記錄必須包含 SQLSTATE 01S01(行中的錯誤);**SQLFetchScroll**不會返回此 SQLSTATE。 如果 SQL 擴展獲取無法返回其他 SQLSTATEs,它仍必須返回此 SQLSTATE。  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll 和樂觀併發  
 如果游標使用樂觀併發 (即SQL_ATTR_CONCURRENCY 語句屬性的值為 SQL_CONCUR_VALUES 或SQL_CONCUR_ROWVER - **SQLFetchScroll**更新數據源用於檢測行是否已更改的樂觀併發值。 每當**SQLFetchScroll**獲取新的行集時(包括重新擷取當前行集時),就會發生這種情況。 (調用它,提取方向設置為SQL_FETCH_RELATIVE和提取偏移設置為 0。  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>SQLFetchScroll 和 ODBC 2.x 驅動程式  
 當應用程式在 ODBC 2.x 驅動程式中呼叫**SQLFetchScroll**時,驅動程式管理員將此呼叫映射到**SQL 延伸 。** 它傳遞 SQL**擴展提取**參數的以下值。  
  
|SQL 延伸參數|值|  
|-------------------------------|-----------|  
|語句句柄|語句處理在**SQLFetchScroll**中。|  
|擷取方向|在**SQLFetchScroll**中獲取方向。|  
|擷取位移|如果未SQL_FETCH_BOOKMARK取取方向,則使用**SQLFetchScroll**中提取偏移參數的值。<br /><br /> 如果fetch方向SQL_FETCH_BOOKMARK,則使用存儲在SQL_ATTR_FETCH_BOOKMARK_PTR語句屬性指定的位址中的值。|  
|羅( 羅) CountPtr|SQL_ATTR_ROWS_FETCHED_PTR 語句屬性指定的位址。|  
|行狀態陣列|由SQL_ATTR_ROW_STATUS_PTR語句屬性指定的位址。|  
  
 有關詳細資訊,請參閱附錄 G 中的[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):向後相容性的驅動程式指南。  
  
## <a name="descriptors-and-sqlfetchscroll"></a>描述符與 SQLFetchScroll  
 **SQLFetchScroll**以與**SQLFetch**相同的方式與描述符進行交互。 有關詳細資訊,請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)中的「描述符和 SQLFetchScroll"部分。  
  
## <a name="code-example"></a>程式碼範例  
 請參考[欄位-Wise 的功能](../../../odbc/reference/develop-app/column-wise-binding.md)、[Wise 的連線](../../../odbc/reference/develop-app/row-wise-binding.md)、 信件化更新[與移除敘述](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), 以及[使用 SQLSetPos 在行集中更新列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行批次插入、更新或移除操作|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回有關結果集中的資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|關閉敘述的游標|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回結果集欄數|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|定位游標、刷新列集中的資料或更新或刪除結果集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
