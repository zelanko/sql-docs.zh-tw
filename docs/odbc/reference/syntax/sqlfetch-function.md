---
title: SQLFetch 功能 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285968"
---
# <a name="sqlfetch-function"></a>SQLFetch 函式
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLFetch**從結果集中獲取下一個數據行集,並返回所有綁定列的數據。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLFetch(  
     SQLHSTMT     StatementHandle);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLFetch**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫[SQLGetDiagRec 函數](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)來取得關聯的 SQLSTATE 值,該函數具有*Handle*SQL_HANDLE_STMT的*句柄類型*和*語句句柄*。 下表列出了**SQLFetch**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。 如果單個列上發生錯誤,可以使用 SQL_DIAG_COLUMN_NUMBER*的 Diag 標識符*調用[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)以確定錯誤發生的列;和**SQLGetDiagField**可以使用SQL_DIAG_ROW_NUMBER*的 Diag 識別符*調用,以確定包含該列的行。  
  
 對於可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT(01xxx SQLSTATEs 除外),如果多行操作的一個或多個行發生錯誤(但不是全部)發生錯誤,則返回SQL_SUCCESS_WITH_INFO,如果單行操作發生錯誤,則返回SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|為列返回的字串或二進位資料導致非空白字元或非 NULL 二進位資料的截斷。 如果它是一個字串值,它是右截斷的。|  
|01S01|行中的錯誤|獲取一個或多個行時出錯。<br /><br /> (如果在 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式時返回此 SQLSTATE,則可以忽略它。|  
|01S07|分數截斷|為列返回的數據被截斷。 對於數位數據類型,數位的小數部分被截斷。 對於包含時間元件的時間、時間戳和間隔數據類型,時間的小數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|無法將結果集中欄資料值轉換為**SQLBindCol**中*TargetType*指定的數據類型。<br /><br /> 列 0 與SQL_C_BOOKMARK數據類型綁定,SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE。<br /><br /> 列 0 與數據類型SQL_C_VARBOOKMARK綁定,並且SQL_ATTR_USE_BOOKMARKS語句屬性未設置為SQL_UB_VARIABLE。|  
|07009|不合法的描述符索引|驅動程式是不支援**SQLExtendedFetch**的 ODBC 2 *.x*驅動程式,在列綁定中指定的列編號為 0。<br /><br /> 列 0 已綁定,SQL_ATTR_USE_BOOKMARKS 語句屬性設置為SQL_UB_OFF。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22001|字串資料,右截斷|為列返回的可變長度書籤被截斷。|  
|22002|需要指標變數,但未提供|NULL 資料被提取到一個列*中,* 該列StrLen_or_IndPtr由**SQLBindCol**設定(或由**SQLSetDescField**或**SQLSetDescRec**設定SQL_DESC_INDICATOR_PTR)為空指標。|  
|22003|數值超範圍|將數值作為一個或多個綁定列的數位或字串返回將導致數位的整個部分(而不是小數)被截斷。<br /><br /> 關於詳細資訊,請參閱在附錄 D:資料類型中[將資料從 SQL 轉換為 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。|  
|22007|不合法日期時間格式|結果集中的字元列綁定到日期、時間或時間戳 C 結構,並且列中的值分別是無效的日期、時間或時間戳。|  
|22012|除零|返回算術表達式中的值,結果除以零。|  
|22015|間隔欄位溢出|從精確數位或間隔 SQL 類型分配給間隔 C 類型會導致前導欄位中的重要數位丟失。<br /><br /> 將資料提取到間隔 C 類型時,間隔 C 類型中沒有 SQL 類型的值表示形式。|  
|22018|強制轉換規範的不合法字元值|結果集中的字元列綁定到字元 C 緩衝區,該列包含緩衝區的字元集中沒有表示的字元。<br /><br /> C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。|  
|24000|指標狀態無效|*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。|  
|40001|序列化失敗|執行提取的事務已終止,以防止死鎖。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 **SQLFetch**函數被呼叫,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**調用了*敘述的句柄*。 然後在*語句句柄*上再次調用**SQLFetch**函數。<br /><br /> 或者 **,SQLFetch**函數被呼叫,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程應用程式中的不同線程呼叫*的語句處理*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLFetch**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 指定的*語句句柄*未處於執行狀態。 調用該函數時沒有首先調用**SQLExecDirect、SQLExecute**或目錄函**SQLExecute**數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) **SQLFetch**在呼叫**SQLExtendedFetch**後與使用SQL_CLOSE選項的**SQLFreeStmt**之前呼叫 *。*|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|SQL_ATTR_USE_BOOKMARK語句屬性設置為SQL_UB_VARIABLE,第 0 列綁定到長度不等於此結果集書簽的最大長度的緩衝區。 (此長度在 IRD 的SQL_DESC_OCTET_LENGTH欄位中可用,可以通過呼叫**SQLDescribeCol、SQLColattribute**或**SQLGetDescField**獲得。 **SQLColAttribute**|  
|HY107|行值範圍外|使用SQL_ATTR_CURSOR_TYPE語句屬性指定的值SQL_CURSOR_KEYSET_DRIVEN,但使用SQL_ATTR_KEYSET_SIZE語句屬性指定的值大於 0,小於使用SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定的值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或資料來源不支援**SQLBindCol**中的*TargetType*和相應列的 SQL 資料類型的組合指定的轉換。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回請求的結果集之前已過期。 超時期間通過 SQL_ATTR_QUERY_TIMEOUT 的 SQLSetStmtAttr 設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQLFetch**傳回結果集中的下一個行集。 僅當結果集存在時才能調用它:也就是說,在創建結果集的調用之後和在該結果集上的游標關閉之前。 如果綁定任何列,它將返回這些列中的數據。 如果應用程式指定了指向行狀態陣列的指標或用於返回提取的行數的緩衝區 **,SQLFetch**還會返回此資訊。 對**SQLFetch 的**呼叫可以與**SQLFetchScroll**的調用混合,但不能與**SQLAaFetch 的**調用混合。 有關詳細資訊,請參閱[取得一行資料](../../../odbc/reference/develop-app/fetching-a-row-of-data.md)。  
  
 如果 ODBC 3 *.x*應用程式與 ODBC 2 *.x*驅動程式一起工作,驅動程式管理器會將**SQLFetch**呼叫映射到**SQLExtendedFetch,** 用於支援**SQLDb.x 的**ODBC 2 *.x*驅動程式。 如果 ODBC 2 *.x*驅動程式不支援**SQLExtendedFetch,** 驅動程式管理員將**SQLFetch**呼叫映射到 ODBC 2 *.x*驅動程式中的**SQLFetch,** 該驅動程式只能取得一行。  
  
 有關詳細資訊,請參閱附錄 G 中的[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):向後相容性的驅動程式指南。  
  
## <a name="positioning-the-cursor"></a>定位游標  
 創建結果集時,游標位於結果集開始之前。 **SQLFetch**獲取下一個行集。 它等效於將*取取定向*設置為SQL_FETCH_NEXT調用**SQLFetchScroll。** 有關游標的詳細資訊,請參閱[游標](../../../odbc/reference/develop-app/cursors.md)與[區塊游標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定行集中的行數。 如果**SQLFetch**提取的行集與結果集的末尾重疊,則**SQLFetch**將返回部分行集。 也就是說,如果 S + R - 1 大於 L,其中 S 是要提取的行集的起始行,R 是行集大小,而 L 是結果集中的最後一行,則只有排集的前一行 L - S = 1 行有效。 其餘行為空,狀態為 SQL_ROW_NOROW。  
  
 **SQLFetch**返回後,當前行是行集的第一行。  
  
 下表中列出的規則基於本節中第二表中列出的條件,描述調用**SQLFetch**后游標定位。  
  
|條件|新行集的第一行|  
|---------------|-----------------------------|  
|開始之前|1|  
|*CurrRowset 開始*\<= *上一個結果行 - 行集大小*[1]|*CurrRowset 開始* + *行集大小*[2]】|  
|*CurrRowset 開始* > *上一個結果行 - 行集大小*[1]|結束後|  
|結束後|結束後|  
  
 [1] 如果在提取之間更改了行集大小,則這是與上一個提取一起使用的行集大小。  
  
 [2] 如果在提取之間更改了行集大小,則這是與新提取一起使用的行集大小。  
  
|表示法|意義|  
|--------------|-------------|  
|開始之前|塊游標位於結果集開始之前。 如果新行集的第一行位於結果集開始之前 **,SQLFetch**將返回SQL_NO_DATA。|  
|結束後|塊游標位於結果集結束之後。 如果新行集的第一行位於結果集結束后 **,SQLFetch**將返回SQL_NO_DATA。|  
|*CurrRowset 開始*|當前行集中的第一行的編號。|  
|*最後一個結果列*|結果集中的最後一行的編號。|  
|*行集大小*|行集大小。|  
  
 例如,假設結果集有 100 行,行集大小為 5。 下表顯示了**SQLFetch**為不同的起始位置返回的行集和返回代碼。  
  
|目前列集|傳回碼|新行集|擷取的行數|  
|--------------------|-----------------|----------------|------------------------|  
|開始之前|SQL_SUCCESS|1 到 5|5|  
|1 到 5|SQL_SUCCESS|6 到 10|5|  
|52 到 56|SQL_SUCCESS|57 到 61|5|  
|91 到 95|SQL_SUCCESS|96 到 100|5|  
|93 到 97|SQL_SUCCESS|98 到 100。 行狀態陣列的第 4 行和第 5 行設置為SQL_ROW_NOROW。|3|  
|96 到 100|SQL_NO_DATA|無。|0|  
|99 到 100|SQL_NO_DATA|無。|0|  
|結束後|SQL_NO_DATA|無。|0|  
  
## <a name="returning-data-in-bound-columns"></a>在繫結列中傳回資料  
 當**SQLFetch**返回每行時,它將每個綁定列的數據放在綁定到該列的緩衝區中。 如果未綁定列 **,SQLFetch**將返回任何數據,但會向前移動塊游標。 仍可以使用**SQLGetData**檢索數據。 如果游標是多行游標(即SQL_ATTR_ROW_ARRAY_SIZE大於1),則僅當使用SQL_GETDATA_EXTENSIONS*資訊類型*調用**SQLGetInfo**時返回SQL_GD_BLOCK才能調用**SQLGetData。** (有關詳細資訊,請參閱[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
 對於行中的每個綁定列 **,SQLFetch**執行以下操作:  
  
1.  將長度/指示器緩衝區設置為SQL_NULL_DATA,如果資料為 NULL,則繼續到下一列。 如果資料為 NULL 且未綁定長度/ 指示器緩衝區 **,SQLFetch**將返回該行的 SQLSTATE 22002(需要但未提供指標變數),然後繼續執行下一行。 有關如何確定長度/指示器緩衝區的位址的資訊,請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的"緩衝區位址"。  
  
     如果列的數據不是**NULL,SQLFetch**將繼續執行步驟 2。  
  
2.  如果SQL_ATTR_MAX_LENGTH語句屬性設置為非零值,並且列包含字元或二進位資料,則數據將截斷為SQL_ATTR_MAX_LENGTH位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH語句屬性旨在減少網路流量。 它通常由數據源實現,數據源在通過網路返回數據之前會截截數據。 驅動程序和數據源不需要支援它。 因此,為了保證數據被截斷到特定大小,應用程式應分配該大小的緩衝區,並在**SQLBindCol**中指定*cbValueMax*參數中的大小。  
  
3.  將資料轉換為**SQLBindCol**中*TargetType*指定的類型。  
  
4.  如果數據轉換為可變長度數據類型(如字元或二進位 **),SQLFetch**將檢查數據的長度是否超過數據緩衝區的長度。 如果字元數據的長度(包括空終止字元)超過數據緩衝區的長度 **,SQLFetch**會將數據截取到數據緩衝區的長度,而減去空終止字元的長度。 然後,它將終止數據。 如果二進位數據的長度超過數據緩衝區的長度 **,SQLFetch**會將其截截到數據緩衝區的長度。 在**SQLBindCol**中,使用*緩衝區長度*指定數據緩衝區的長度。  
  
     **SQLFetch**從不截取轉換為固定長度數據類型的數據;它始終假定數據緩衝區的長度是數據類型的大小。  
  
5.  將轉換後的數據(可能截斷)數據放入數據緩衝區中。 有關如何確定數據緩衝區位址的資訊,請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的「緩衝區位址」。  
  
6.  將數據的長度放在長度/指示器緩衝區中。 如果指標指標和長度指標都設置為相同的緩衝區(與**SQLBindCol**的調用相同),則長度將寫入緩衝區中,用於有效數據,並在 NULL 數據的緩衝區中寫入SQL_NULL_DATA。 如果未綁定長度/指示器緩衝區 **,SQLFetch**不會返回長度。  
  
    -   對於字元或二進位數據,這是轉換後和截斷前由於數據緩衝區太小而截斷之前的數據長度。 如果驅動程式無法確定轉換後的數據長度(有時與長數據的情況一樣),它將長度設置為SQL_NO_TOTAL。 如果資料由於SQL_ATTR_MAX_LENGTH語句屬性而被截斷,則此屬性的值將放在長度/指示器緩衝區中,而不是實際長度 。 這是因為此屬性旨在在轉換之前截截伺服器上的數據,以便驅動程式無法確定實際長度。  
  
    -   對於所有其他數據類型,這是轉換后的數據長度;也就是說,它是數據轉換到的類型的大小。  
  
     有關如何確定長度/指示器緩衝區的位址的資訊,請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)中的"緩衝區位址"。  
  
7.  如果在轉換過程中將數據截斷而不丟失有效數位(例如,轉換時,實際數位 1.234 被截斷到整數**1),SQLFetch**將返回 SQLSTATE 01S07(分數截斷)並SQL_SUCCESS_WITH_INFO。 如果數據由於數據緩衝區的長度太小而被截斷(例如,字串"abcdef"放在 4 位元組緩衝區中 **),SQLFetch**將返回 SQLSTATE 01004(數據截斷)並SQL_SUCCESS_WITH_INFO。 如果數據由於SQL_ATTR_MAX_LENGTH語句屬性而截斷 **,SQLFetch**將返回SQL_SUCCESS,並且不返回 SQLSTATE 01S07(分數截斷)或 SQLSTATE 01004(數據截斷)。 如果在轉換過程中截斷數據,丟失有效數位(例如,如果大於 100,000 的SQL_INTEGER值轉換為**SQL_C_TINYINT),SQLFetch**將返回 SQLSTATE 22003(範圍外的數位值)和SQL_ERROR(如果行集大小為 1)或SQL_SUCCESS_WITH_INFO(如果行集大小大於 1)。  
  
 如果**SQLFetch**或**SQLFetchScroll**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則綁定數據緩衝區和長度/指示器緩衝區的內容未定義。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 行狀態數組用於返回行集中每行的狀態。 此陣列的位址是使用SQL_ATTR_ROW_STATUS_PTR語句屬性指定的。 陣列由應用程式分配,並且必須具有SQL_ATTR_ROW_ARRAY_SIZE語句屬性指定的元素數。 其值由**SQLFetch、SQLFetchScroll**和**SQLBulk 操作**或**SQLSetPos**設定(在**SQLAeFetch**定位**SQLFetch**後調用它們時除外)。 如果SQL_ATTR_ROW_STATUS_PTR語句屬性的值為空指標,則這些函數不會返回行狀態。  
  
 如果**SQLFetch**或**SQLFetchScroll**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則行狀態陣列緩衝區的內容未定義。  
  
 行狀態陣列中返回以下值。  
  
|行狀態陣列值|描述|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|該行已成功提取,自上次從此結果集提取以來一直未更改。|  
|SQL_ROW_SUCCESS_WITH_INFO|該行已成功提取,自上次從此結果集提取以來一直未更改。 但是,返回了有關該行的警告。|  
|SQL_ROW_ERROR|提取行時出錯。|  
|SQL_ROW_UPDATED[1]、[2]和[3]|該行已成功提取,自上次從此結果集提取以來已更改。 如果此行再次從此結果集中提取,或者由**SQLSetPos**刷新,則狀態將更改為該行的新狀態。|  
|SQL_ROW_DELETED[3]|自上次從此結果集中提取行以來,該行已被刪除。|  
|SQL_ROW_ADDED[4]|該行由**SQLBulk 操作**插入。 如果再次從此結果集中提取該行,或由**SQLSetPos**刷新,則其狀態SQL_ROW_SUCCESS。|  
|SQL_ROW_NOROW|行集與結果集的末尾重疊,並且不會返回對應於行狀態陣列的此元素的行。|  
  
 [1] 對於鍵集、混合游標和動態游標,如果更新了鍵值,則數據行將被視為已刪除並添加新行。  
  
 [2] 某些驅動程式無法檢測數據的更新,因此無法返回此值。 要確定驅動程式是否可以檢測更新以重新提取行,應用程式使用SQL_ROW_UPDATES選項調用**SQLGetInfo。**  
  
 [3] **SQLFetch**只有在與**SQLFetchScroll**的調用混合時才能返回此值。 這是因為**SQLFetch**在結果集中向前移動,並且當它被獨佔使用時,不會重新提取任何行。 由於沒有重新提取任何行 **,SQLFetch**不會檢測以前提取的行所做的更改。 但是,如果**SQLFetchScroll**在以前提取的任何行之前定位游標,並且**SQLFetch**用於獲取這些行,**則 SQLFetch**可以檢測對這些行的任何更改。  
  
 [4] 僅由 SQLBulk 操作返回。 未由**SQLFetch**或**SQLFetchScroll**設定。  
  
### <a name="rows-fetched-buffer"></a>行擷取緩衝區  
 取自緩衝區的行用於返回提取的行數,包括由於在提取行時發生錯誤而未返回數據的行。 換句話說,它是行狀態陣列中的值不SQL_ROW_NOROW的行數。 此緩衝區的位址使用SQL_ATTR_ROWS_FETCHED_PTR語句屬性指定。 緩衝區由應用程式分配。 它由**SQLFetch**和**SQLFetchScroll**設定。 如果SQL_ATTR_ROWS_FETCHED_PTR語句屬性的值為空指標,則這些函數不會返回獲取的行數。 要確定結果集中的當前行數,應用程式可以使用 SQL_ATTR_ROW_NUMBER 屬性調用**SQLGetStmtAttr。**  
  
 如果**SQLFetch**或**SQLFetchScroll**不返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,則行提取緩衝區的內容未定義,除非返回SQL_NO_DATA,在這種情況下,行提取緩衝區中的值設置為 0。  
  
### <a name="error-handling"></a>錯誤處理  
 錯誤和警告可以應用於單個行或整個函數。 有關診斷記錄的詳細資訊,請參閱[診斷](../../../odbc/reference/develop-app/diagnostics.md)和[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)。  
  
#### <a name="errors-and-warnings-on-the-entire-function"></a>整個函數上的錯誤和警告  
 如果錯誤應用於整個函數,例如 SQLSTATE HYT00(超時已過期)或 SQLSTATE 24000(無效游標狀態 **),SQLFetch**將返回SQL_ERROR和適用的 SQLSTATE。 行集緩衝區的內容未定義,游標位置保持不變。  
  
 如果警告應用於整個函數 **,SQLFetch**將返回SQL_SUCCESS_WITH_INFO和適用的 SQLSTATE。 應用於整個函數的警告的狀態記錄在應用於單個行的狀態記錄之前返回。  
  
#### <a name="errors-and-warnings-in-individual-rows"></a>單列中的錯誤和警告  
 如果錯誤(如 SQLSTATE 22012(除零)))或警告(如 SQLSTATE 01004(資料截斷)))應用於單個行 **,SQLFetch**執行以下操作:  
  
-   將行狀態陣列的相應元素設置為SQL_ROW_ERROR錯誤或SQL_ROW_SUCCESS_WITH_INFO警告。  
  
-   添加包含 SQLSTAT 的零個或多個狀態記錄,以查找錯誤或警告。  
  
-   設置狀態記錄中的行和列編號欄位。 如果**SQLFetch**無法確定行或列號,它將該數位分別設置為SQL_ROW_NUMBER_UNKNOWN或SQL_COLUMN_NUMBER_UNKNOWN。 如果狀態記錄不適用於特定列 **,SQLFetch**會將列號設置為SQL_NO_COLUMN_NUMBER。  
  
 **SQLFetch**繼續提取行,直到它獲取行集中的所有行。 除非行集的每一行(不包括狀態SQL_ROW_NOROW的行)中發生錯誤,否則它將返回SQL_SUCCESS_WITH_INFO,在這種情況下,它將返回SQL_ERROR。 特別是,如果行集大小為 1,並且該行中出現錯誤,則**SQLFetch**將返回SQL_ERROR。  
  
 **SQLFetch**按行號順序返回狀態記錄。 也就是說,它返回未知行的所有狀態記錄(如果有);接下來,它返回第一行的所有狀態記錄(如果有),然後返回第二行的所有狀態記錄(如果有),等等。 每行的狀態記錄根據常規規則排序狀態記錄;有關詳細資訊,請參閱[SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)中的「狀態記錄序列」。  
  
### <a name="descriptors-and-sqlfetch"></a>描述符與 SQLFetch  
 以下各節介紹**SQLFetch**如何與描述符進行交互。  
  
#### <a name="argument-mappings"></a>參數對應  
 驅動程式不設置任何描述符欄位基於**SQLFetch**的參數。  
  
#### <a name="other-descriptor-fields"></a>其他描述字欄位  
 **SQLFetch**使用以下描述符欄位。  
  
|描述項欄位|德克|欄位|設置通過|  
|----------------------|-----------|--------------|-----------------|  
|SQL_DESC_ARRAY_SIZE|阿爾德|頁首|SQL_ATTR_ROW_ARRAY_SIZE語句屬性|  
|SQL_DESC_ARRAY_STATUS_PTR|稅務局|頁首|SQL_ATTR_ROW_STATUS_PTR語句屬性|  
|SQL_DESC_BIND_OFFSET_PTR|阿爾德|頁首|SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性|  
|SQL_DESC_BIND_TYPE|阿爾德|頁首|SQL_ATTR_ROW_BIND_TYPE敘述屬性|  
|SQL_DESC_COUNT|阿爾德|頁首|**SQLBindCol**的*欄位號*參數|  
|SQL_DESC_DATA_PTR|阿爾德|記錄|**SQLBindCol** *的目標值 Ptr*參數|  
|SQL_DESC_INDICATOR_PTR|阿爾德|記錄|*StrLen_or_IndPtr*在**SQLBindCol**中參數|  
|SQL_DESC_OCTET_LENGTH|阿爾德|記錄|**SQLBindCol**中的*緩衝區長度*參數|  
|SQL_DESC_OCTET_LENGTH_PTR|阿爾德|記錄|*StrLen_or_IndPtr*在**SQLBindCol**中參數|  
|SQL_DESC_ROWS_PROCESSED_PTR|稅務局|頁首|SQL_ATTR_ROWS_FETCHED_PTR語句屬性|  
|SQL_DESC_TYPE|阿爾德|記錄|**SQLBindCol**中*的目標類型*參數|  
  
 所有描述符位也可以通過**SQLSetDescField 進行**設置。  
  
#### <a name="separate-length-and-indicator-buffers"></a>單獨的長度和指示器緩衝區  
 應用程式可以綁定單個緩衝區或兩個單獨的緩衝區,可用於保存長度和指標值。 當應用程式調用**SQLBindCol**時,驅動程式將 ARD 的SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_INDICATOR_PTR欄位設置到同一位址,該位址在*StrLen_or_IndPtr*參數中傳遞。 當應用程式呼叫**SQLSetDescField**或**SQLSetDescRec**時,它可以將這兩個字段設置為不同的位址。  
  
 **SQLFetch**確定應用程式是否指定了單獨的長度和指示器緩衝區。 在這種情況下,當數據不是 NULL 時 **,SQLFetch**將指示器緩衝區設置為 0 並返回長度緩衝區中的長度。 當數據為 NULL 時 **,SQLFetch**將指示器緩衝區設置為SQL_NULL_DATA,並且不修改長度緩衝區。  
  
### <a name="code-example"></a>程式碼範例  
 請參閱[SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md)SQLBindCol、SQLColumns、SQLGetData 和 SQL 程式。 [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md) [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md) [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)  
  
### <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回有關結果集中的資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|關閉敘述的游標|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|取得資料欄的一部份或全部|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集欄數|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|準備執行敘述|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
