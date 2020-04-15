---
title: SQLBulk 操作函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f4f294a6d84856bc3065b599a370bb5658e3ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301328"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函式
**一致性**  
 版本介紹: ODBC 3.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLBulk操作**執行批量插入和批量書籤操作,包括按書籤更新、刪除和提取。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *操作*  
 [輸入]操作執行:  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARKSQL_DELETE_BY_BOOKMARKSQL_DELETE_BY_BOOKMARKSQL_ADDSQL_FETCH_BY_BOOKMARK  
  
 有關詳細資訊,請參閱"註釋"。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBulk 操作**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLBulk 操作**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
 對於可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT(01xxx SQLSTATEs 除外),如果多行操作的一個或多個行發生錯誤(但不是全部)發生錯誤,則返回SQL_SUCCESS_WITH_INFO,如果單行操作發生錯誤,則返回SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料右截斷|*SQL_FETCH_BY_BOOKMARK操作*參數,為資料類型為SQL_C_CHAR或SQL_C_BINARY的列返回的字串或二進位資料會導致非空白字元或非 NULL 二進位資料的截斷。|  
|01S01|行中的錯誤|*操作*參數SQL_ADD,在執行操作時,一個或多個行中發生錯誤,但至少已成功添加一行。 (函數返回SQL_SUCCESS_WITH_INFO。<br /><br /> (僅當應用程式使用 ODBC 2 時,才會引發此錯誤。*x*驅動程式。|  
|01S07|分數截斷|*操作*參數SQL_FETCH_BY_BOOKMARK,應用程式緩衝區的數據類型未SQL_C_CHAR或SQL_C_BINARY,返回到一個或多個列的應用程序緩衝區的數據被截斷。 (對於數位 C 數據類型,數位的小數部分被截斷。 對於包含時間元件的時間、時間戳和間隔 C 數據類型,時間的小數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|*操作*參數SQL_FETCH_BY_BOOKMARK,並且結果集中列的數據值無法轉換為對**SQLBindCol**調用中*的目標類型*參數指定的數據類型。<br /><br /> *操作*參數SQL_UPDATE_BY_BOOKMARK或SQL_ADD,並且應用程式緩衝區中的數據值無法轉換為結果集中列的數據類型。|  
|07009|不合法的描述符索引|參數*操作*SQL_ADD,並且對列綁定的列數大於結果集中的列數。|  
|21S02|衍生表的程度與列清單不符合|參數*操作*是SQL_UPDATE_BY_BOOKMARK;並且沒有列是可向上的,因為所有列都是未綁定的或唯讀的,或者綁定長度/指示器緩衝區中的值SQL_COLUMN_IGNORE。|  
|22001|字串資料右截斷|將字元或二進位值分配給結果集中的列會導致截斷非空白(對於字元)或非空字元(二進位元字元或字節)。|  
|22003|數值超範圍|*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK,並將數值分配給結果集中的列會導致數字的整個(而不是小數)部分被截斷。<br /><br /> 參數*操作*SQL_FETCH_BY_BOOKMARK,返回一個或多個綁定列的數值將導致重要數位的損失。|  
|22007|不合法日期時間格式|*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK,並將日期或時間戳值分配給結果集中的列會導致年份、月份或日欄段超過範圍。<br /><br /> 參數*操作*SQL_FETCH_BY_BOOKMARK,傳回一個或多個綁定列的日期或時間戳值將導致年份、月份或日欄位超出範圍。|  
|22008|日期/時間欄位溢出|*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK,並且對發送到結果集中的列的數據執行日期時間算術,導致結果超出欄位允許的值範圍或根據公曆的約會時間的自然規則無效的約會時間欄位(年份、月份、日、小時、分鐘或第二個字段)。<br /><br /> *操作*參數SQL_FETCH_BY_BOOKMARK,並且對從結果集中檢索的數據執行日期時間算術,導致結果的日期時間欄位(年份、月份、天、小時、分鐘或第二個字段)超出欄位的允許值範圍,或者根據公曆的約會時間自然規則無效。|  
|22015|間隔欄位溢出|*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK,將精確數位或間隔 C 類型分配給間隔 SQL 資料類型會導致重要數位丟失。<br /><br /> *操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK;當分配給間隔 SQL 類型時,間隔 SQL 類型中沒有 C 類型的值表示形式。<br /><br /> *操作*參數SQL_FETCH_BY_BOOKMARK,並將精確的數位或間隔 SQL 類型分配給間隔 C 類型會導致前導欄位中的重要數位丟失。<br /><br /> *行動*論點SQL_FETCH_BY_BOOKMARK;當分配給間隔 C 類型時,間隔 C 類型中沒有 SQL 類型的值表示形式。|  
|22018|強制轉換規範的不合法字元值|*行動*論點SQL_FETCH_BY_BOOKMARK;C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。<br /><br /> 參數*操作*SQL_ADD或SQL_UPDATE_BY_BOOKMARK;SQL 類型是精確或近似的數位、日期時間或間隔數據類型;C 類型為SQL_C_CHAR;列中的值不是綁定 SQL 類型的有效文本。|  
|23000|完整性約束衝突|*操作*參數SQL_ADD、SQL_DELETE_BY_BOOKMARK或SQL_UPDATE_BY_BOOKMARK,並且違反了完整性約束。<br /><br /> *操作*參數SQL_ADD,未綁定的列定義為非 NULL 且沒有預設值。<br /><br /> *操作*參數SQL_ADD,在綁定*StrLen_or_IndPtr*緩衝區中指定的長度SQL_COLUMN_IGNORE,並且列沒有預設值。|  
|24000|指標狀態無效|*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。|  
|40001|序列化失敗|由於資源與另一個事務死鎖,事務被回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|42000|語法錯誤或存取衝突|驅動程式無法根據需要鎖定該行,以執行*操作*參數中請求的操作。|  
|44000|WITH CHECK OPTION 違規|*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK,插入或更新是在通過指定 **「使用 CHECK 選項**」創建的已查看表(或從已查看表派生的表)上執行的,這樣受插入或更新影響的一個或多個行將不再存在於查看的表中。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLBulk 操作**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 指定的*語句句柄*未處於執行狀態。 調用該函數時沒有首先調用**SQLExecDirect、SQLExecute**或目錄函**SQLExecute**數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLSetPos**被調用用於*語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 驅動程式是 ODBC 2。*x*驅動程式,在呼叫**SQLFetchScroll**或**SQLFetch**之前,呼叫**SQLBulk 操作**為*敘述的句柄*。<br /><br /> (DM) **SQLBulk操作**是在語句*句柄*上調用**SQL 擴展獲取**後調用的。|  
|HY011|無法立即設定屬性|(DM) 驅動程式是 ODBC 2。*x*驅動程式,並在對**SQLFetch**或**SQLFetchScroll**和**SQLBulk 操作**的調用之間設置了SQL_ATTR_ROW_STATUS_PTR語句屬性。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK;數據值不是空指標;數據值不是空指標。C 數據類型為SQL_C_BINARY或SQL_C_CHAR;並且列長度值小於 0,但不等於SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS或SQL_NULL_DATA,或小於或等於SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指示器緩衝區中的值SQL_DATA_AT_EXEC;SQL 類型要麼是SQL_LONGVARCHAR、SQL_LONGVARBINARY,要麼是長數據源特定的數據類型;**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN資訊類型為"Y"。<br /><br /> *操作*參數SQL_ADD,SQL_ATTR_USE_BOOKMARK語句屬性設置為SQL_UB_VARIABLE,第 0 列綁定到長度不等於此結果集書簽的最大長度的緩衝區。 (此長度在 IRD 的SQL_DESC_OCTET_LENGTH欄位中可用,可以通過呼叫**SQLDescribeCol、SQLColattribute**或**SQLGetDescField**獲得。 **SQLColAttribute**|  
|HY092|不合法屬性識別碼|(DM) 為*操作*參數指定的值無效。<br /><br /> *操作*參數SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或SQL_DELETE_BY_BOOKMARK,SQL_ATTR_CONCURRENCY語句屬性設置為SQL_CONCUR_READ_ONLY。<br /><br /> *操作*參數SQL_DELETE_BY_BOOKMARK、SQL_FETCH_BY_BOOKMARK或SQL_UPDATE_BY_BOOKMARK,書簽列未綁定,或者SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或數據源不支援*操作*參數中請求的操作。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**SQLSetStmtAttr**設置,*屬性*參數為SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]  
>  有關哪些語句聲明**SQLBulk 操作**可以調用,以及它必須做什麼才能與 ODBC 2 相容。*x*應用程式,請參閱附錄 G:向後相容性的驅動程式指南中的[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)部分。  
  
 應用程式使用**SQLBulk 操作**對目前查詢對應的基表或檢視執行以下操作:  
  
-   添加新行。  
  
-   更新一組行,其中每行由書簽標識。  
  
-   刪除一組行,其中每行由書籤標識。  
  
-   獲取一組行,其中每行由書簽標識。  
  
 調用**SQLBulk 操作**後,塊游標位置未定義。 應用程式必須調用**SQLFetchScroll**來設置游標位置。 應用程式應僅使用SQL_FETCH_FIRST、SQL_FETCH_LAST、SQL_FETCH_ABSOLUTE或SQL_FETCH_BOOKMARK的 Fetch 方向參數調用**SQLFetchScroll。** *FetchOrientation* 如果應用程式呼叫**SQLFetch**或**SQLFetchScroll,** 並帶有SQL_FETCH_PRIOR、SQL_FETCH_NEXT或SQL_FETCH_RELATIVE*的提取方向*參數,則游標位置未定義。  
  
 通過將調用**SQLBindCol**中指定的列長度/ 指示器緩衝區設置為SQL_COLUMN_IGNORE,可以在對**SQLBulk 操作**執行的批量操作中忽略列。  
  
 應用程式在調用**SQLBulk 操作**時不必設置SQL_ATTR_ROW_OPERATION_PTR語句屬性,因為使用此函數執行批量操作時不能忽略行。  
  
 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性指向的緩衝區包含受對**SQLBulk 操作**的調用影響的行數。  
  
 當*操作*參數SQL_ADD或SQL_UPDATE_BY_BOOKMARK,並且與游標關聯的查詢規範的選擇清單包含對同一列的多個引用時,它是驅動程式定義的,無論是生成錯誤還是驅動程式忽略重複的引用並執行請求的操作。  
  
 有關如何使用**SQLBulk 操作**的詳細資訊,請參閱使用[SQLBulk 操作更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>執行批次插入  
 若要使用**SQLBulk 操作**插入資料,應用程式將執行以下步驟序列:  
  
1.  執行返回結果集的查詢。  
  
2.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為要插入的行數。  
  
3.  調用**SQLBindCol**以綁定要插入的數據。 數據綁定到大小等於SQL_ATTR_ROW_ARRAY_SIZE值的陣列。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性指向的陣列的大小應等於SQL_ATTR_ROW_ARRAY_SIZE,SQL_ATTR_ROW_STATUS_PTR應為空指標。  
  
4.  呼叫**SQLBulk 操作**(*語句句柄,SQL_ADD)* 以執行插入。  
  
5.  如果應用程式設置了SQL_ATTR_ROW_STATUS_PTR語句屬性,則可以檢查此陣列以查看操作的結果。  
  
 如果應用程式在調用**SQLBulk 操作**之前綁定列 0,該*參數*為 SQL_ADD,則驅動程式將使用新插入行的書籤值更新綁定列 0 緩衝區。 為此,應用程式必須在執行語句之前將SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE。 (這不適用於 ODBC 2。*x*驅動程式。  
  
 通過使用對 SQLParamData 和 SQLPutData 的調用,SQLBulk 操作可以分部分添加長數據。 有關詳細資訊,請參閱此函數引用後面的"為批量插入和更新提供長數據"。  
  
 應用程式無需在調用**SQLBulk 操作**之前調用**SQLFetch**或**SQLFetchScroll(** 與 ODBC 2 相比除外)。*x*驅動程式;請參閱[向後相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
 如果**SQLBulk 操作**(*操作參數為*SQL_ADD)在包含重複列的游標上調用,則該行為是驅動程式定義的。 驅動程式可以返回驅動程式定義的 SQLSTATE,將數據添加到結果集中顯示的第一列,或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用書籤執行批次更新  
 要使用帶有**SQLBulk 操作**的書籤執行大量更新,應用程式按順序執行以下步驟:  
  
1.  將SQL_ATTR_USE_BOOKMARKS語句屬性設置到SQL_UB_VARIABLE。  
  
2.  執行返回結果集的查詢。  
  
3.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為要更新的行數。  
  
4.  調用**SQLBindCol**以綁定要更新的數據。 數據綁定到大小等於SQL_ATTR_ROW_ARRAY_SIZE值的陣列。 它還調用**SQLBindCol**來綁定列 0(書籤列)。  
  
5.  複製它有興趣更新到綁定到列 0 的陣列中的行的書籤。  
  
6.  更新綁定緩衝區中的數據。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性指向的陣列的大小應等於SQL_ATTR_ROW_ARRAY_SIZE,或者SQL_ATTR_ROW_STATUS_PTR應為空指標。  
  
7.  呼叫**SQLBulk 操作**(*語句句柄,* SQL_UPDATE_BY_BOOKMARK)。  
  
    > [!NOTE]  
    >  如果應用程式設置了SQL_ATTR_ROW_STATUS_PTR語句屬性,則可以檢查此陣列以查看操作的結果。  
  
8.  可選地調用**SQLBulk 操作**(*語句處理*,SQL_FETCH_BY_BOOKMARK),將數據提取到綁定的應用程式緩衝區中,以驗證是否發生了更新。  
  
9. 如果數據已更新,驅動程式將相應行的行狀態陣列中的值更改為SQL_ROW_UPDATED。  
  
 **SQLBulk 操作**執行的量產更新可以透過調用**SQLParamData**和**SQLPutData**來包括長數據。 有關詳細資訊,請參閱此函數引用後面的"為批量插入和更新提供長數據"。  
  
 如果書籤在游標之間保留,則應用程式不需要在按書籤更新之前調用**SQLFetch**或**SQLFetchScroll。** 它可以使用從前一個游標存儲的書籤。 如果書籤不保留在游標上,則應用程式必須調用**SQLFetch**或**SQLFetchScroll**來檢索書籤。  
  
 如果**SQLBulk 操作**(*操作參數為*SQL_UPDATE_BY_BOOKMARK)在包含重複列的游標上調用,則該行為是驅動程式定義的。 驅動程式可以返回驅動程式定義的 SQLSTATE、更新結果集中顯示的第一列或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>使用書籤執行批次  
 要使用**SQLBulk 操作**中的書籤執行批次提取,應用程式按順序執行以下步驟:  
  
1.  將SQL_ATTR_USE_BOOKMARKS語句屬性設置到SQL_UB_VARIABLE。  
  
2.  執行返回結果集的查詢。  
  
3.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為要提取的行數。  
  
4.  調用**SQLBindCol**以綁定要獲取的數據。 數據綁定到大小等於SQL_ATTR_ROW_ARRAY_SIZE值的陣列。 它還調用**SQLBindCol**來綁定列 0(書籤列)。  
  
5.  複製它有興趣提取到綁定到列 0 的陣列中的行的書籤。 (這假定應用程式已單獨獲取書籤。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性指向的陣列的大小應等於SQL_ATTR_ROW_ARRAY_SIZE,或者SQL_ATTR_ROW_STATUS_PTR應為空指標。  
  
6.  呼叫**SQLBulk 操作**(*語句句柄,* SQL_FETCH_BY_BOOKMARK)。  
  
7.  如果應用程式設置了SQL_ATTR_ROW_STATUS_PTR語句屬性,則可以檢查此陣列以查看操作的結果。  
  
 如果書籤在游標之間保留,則應用程式不需要在通過書籤獲取之前調用**SQLFetch**或**SQLFetchScroll。** 它可以使用從前一個游標存儲的書籤。 如果書籤不保留在游標上,則應用程式必須調用**SQLFetch**或**SQLFetchScroll**一次才能檢索書籤。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>使用書籤執行批次刪除  
 要使用**SQLBulk 操作**中的書籤執行批次刪除,應用程式按順序執行以下步驟:  
  
1.  將SQL_ATTR_USE_BOOKMARKS語句屬性設置到SQL_UB_VARIABLE。  
  
2.  執行返回結果集的查詢。  
  
3.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為要刪除的行數。  
  
4.  調用**SQLBindCol**綁定欄 0(書籤列)。  
  
5.  複製它有興趣刪除到列 0 列的陣列中的行的書籤。  
  
    > [!NOTE]  
    >  SQL_ATTR_ROW_STATUS_PTR 語句屬性指向的陣列的大小應等於SQL_ATTR_ROW_ARRAY_SIZE,或者SQL_ATTR_ROW_STATUS_PTR應為空指標。  
  
6.  呼叫**SQLBulk 操作**(*語句句柄,* SQL_DELETE_BY_BOOKMARK)。  
  
7.  如果應用程式設置了SQL_ATTR_ROW_STATUS_PTR語句屬性,則可以檢查此陣列以查看操作的結果。  
  
 如果書籤在游標之間保留,則應用程式不必在按書籤刪除之前調用**SQLFetch**或**SQLFetchScroll。** 它可以使用從前一個游標存儲的書籤。 如果書籤不保留在游標上,則應用程式必須調用**SQLFetch**或**SQLFetchScroll**一次才能檢索書籤。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>為批次插入及更新提供長資料  
 可以為通過調用**SQLBulk 操作**執行的批量插入和更新提供長數據。 若要插入或更新長數據,應用程式除了在本主題前面"執行批量插入"和"使用書籤執行批量更新"部分中描述的步驟外,還執行以下步驟。  
  
1.  當應用程式使用**SQLBindCol**綁定數據時,應用程式將應用程式定義的值(如列號)放在*\*TargetValuePtr*緩衝區中,用於執行時的數據列。 該值以後可用於標識列。  
  
     應用程式將SQL_LEN_DATA_AT_EXEC(*長度*)宏*\** 的結果放在 StrLen_or_IndPtr 緩衝區中。 如果列的 SQL 資料類型SQL_LONGVARBINARY、SQL_LONGVARCHAR 或長數據來源特定的資料類型,並且驅動程式返回**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN資訊類型的「Y」,*則長度*是要為參數發送的數據位元;否則,它必須是非負值,並且被忽略。  
  
2.  當調用**SQLBulk 操作時**,如果存在執行時的數據列,則函數將返回SQL_NEED_DATA並繼續執行步驟 3,如下所示。 (如果沒有執行時的數據列,則該過程已完成。  
  
3.  應用程式呼叫**SQLParamData***\** 檢索 要處理的第一個執行資料列的 TargetValuePtr 緩衝區的位址。 **SQLParamData**返回SQL_NEED_DATA。 應用程式從*\*TargetValuePtr*緩衝區檢索應用程式定義的值。  
  
    > [!NOTE]  
    >  儘管執行時的數據參數類似於執行時的數據列,但**SQLParamData**返回的值因每個參數而異。  
  
     執行時的資料列是行集中的欄,當使用**SQLBulk 操作**更新或插入行時,將隨**SQLPutData**一起發送數據。 它們與**SQLBindCol**綁定。 **SQLParamData**傳回的值是正在處理的 @*TargetValuePtr*緩衝區中的行的位址。  
  
4.  應用程式呼叫**SQLPutData**一次或多次以發送列的資料。 如果在**SQLPutData**中指定的*\*TargetValuePtr*緩衝區中無法返回所有數據值,則需要多個調用。僅當將字元 C 資料發送到具有字元、二進位或資料來源特定資料類型的列或將二進位C資料發送到具有字元、二進位或資料來源特定資料類型的列時,才允許對同一列的**SQLPutData**進行多次調用。  
  
5.  應用程式再次調用**SQLParamData**以發出已為該列發送所有數據的信號。  
  
    -   如果有更多的執行數據列 **,SQLParamData**將返回要處理的下一個執行數據列的SQL_NEED_DATA和目標*ValuePtr*緩衝區的位址。 應用程式重複步驟 4 和 5。  
  
    -   如果沒有更多的數據執行列,該過程將完成。 如果語句成功執行 **,SQLParamData**將返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO;如果執行失敗,它將返回SQL_ERROR。 此時 **,SQLParamData**可以返回**SQLBulk 操作**可以返回的任何 SQLSTATE。  
  
 如果**SQLBulk 操作**傳回SQL_NEED_DATA後**SQLParamData**或**SQLPutData**中發生錯誤,並且在發送所有資料執行列的資料之前,應用程式只能調用 SQLCancel、SQLGetDiagField、SQLGetDiagRec、SQLGet**函數****、SQLParamData**或**SQLPutData**的語句或與語句關聯的連接。 **SQLCancel** **SQLGetDiagField** **SQLGetDiagRec** 如果它調用語句或與 語句關聯的連接的任何其他函數,則函數將返回SQL_ERROR和 SQLSTATE HY010(函數序列錯誤)。  
  
 如果應用程式調用**SQLCancel,** 而驅動程式仍然需要執行時的數據列,則驅動程式將取消該操作。 然後,應用程式可以再次調用**SQLBulk 操作**;取消不會影響游標狀態或當前游標位置。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 行狀態陣列包含行集中每行數據在調用**SQLBulk 操作**後的狀態值。 呼叫**SQLFetch**SQLFetch、SQLFetchScroll、SQLSetPos 或**SQLBulk 操作**後**SQLSetPos**,驅動程式將設定此**SQLFetchScroll**陣列中的狀態值。 如果**SQLFetch**或**SQLFetchScroll**尚未在**SQLBulk 操作**之前調用,則此陣列最初由對**SQLBulk 操作的**呼叫填充。 此陣列由SQL_ATTR_ROW_STATUS_PTR語句屬性指向。 行狀態陣列中的元素數必須等於行集中的行數(由SQL_ATTR_ROW_ARRAY_SIZE語句屬性定義)。 有關此行狀態陣列的資訊,請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下面的範例一次從"客戶"表中獲取10行資料。 然後,它會提示使用者執行操作。 為了減少網路流量,示例緩衝區在綁定陣列中本地更新、刪除和插入,但在偏移量超過行集數據時。 當使用者選擇資料來源傳送更新、刪除與插入時,代碼會將適當地設定結合的偏移量並呼叫**SQLBulk 。** 為簡單起見,使用者不能緩衝超過 10 個更新、刪除或插入。  
  
```cpp  
// SQLBulkOperations_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#include "stdio.h"  
  
#define UPDATE_ROW 100  
#define DELETE_ROW 101  
#define ADD_ROW 102  
#define SEND_TO_DATA_SOURCE 103  
#define UPDATE_OFFSET 10  
#define INSERT_OFFSET 20  
#define DELETE_OFFSET 30  
  
// Define structure for customer data (assume 10 byte maximum bookmark size).  
typedef struct tagCustStruct {  
   SQLCHAR Bookmark[10];  
   SQLINTEGER BookmarkLen;  
   SQLUINTEGER CustomerID;  
   SQLINTEGER CustIDInd;  
   SQLCHAR CompanyName[51];  
   SQLINTEGER NameLenOrInd;  
   SQLCHAR Address[51];  
   SQLINTEGER AddressLenOrInd;  
   SQLCHAR Phone[11];  
   SQLINTEGER PhoneLenOrInd;  
} CustStruct;  
  
// Allocate 40 of these structures. Elements 0-9 are for the current rowset,  
// elements 10-19 are for the buffered updates, elements 20-29 are for  
// the buffered inserts, and elements 30-39 are for the buffered deletes.  
CustStruct CustArray[40];  
SQLUSMALLINT RowStatusArray[10], Action, RowNum, NumUpdates = 0, NumInserts = 0,  
NumDeletes = 0;  
SQLLEN BindOffset = 0;  
SQLRETURN retcode;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLHSTMT hstmt = NULL;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // Set the following statement attributes:  
   // SQL_ATTR_CURSOR_TYPE:           Keyset-driven  
   // SQL_ATTR_ROW_BIND_TYPE:         Row-wise  
   // SQL_ATTR_ROW_ARRAY_SIZE:        10  
   // SQL_ATTR_USE_BOOKMARKS:         Use variable-length bookmarks  
   // SQL_ATTR_ROW_STATUS_PTR:        Points to RowStatusArray  
   // SQL_ATTR_ROW_BIND_OFFSET_PTR:   Points to BindOffset  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER)SQL_CURSOR_KEYSET_DRIVEN, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER)sizeof(CustStruct), 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_USE_BOOKMARKS, (SQLPOINTER)SQL_UB_VARIABLE, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
   retcode = SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_OFFSET_PTR, &BindOffset, 0);  
  
   // Bind arrays to the bookmark, CustomerID, CompanyName, Address, and Phone columns.  
   retcode = SQLBindCol(hstmt, 0, SQL_C_VARBOOKMARK, CustArray[0].Bookmark, sizeof(CustArray[0].Bookmark), &CustArray[0].BookmarkLen);  
   retcode = SQLBindCol(hstmt, 1, SQL_C_ULONG, &CustArray[0].CustomerID, 0, &CustArray[0].CustIDInd);  
   retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, CustArray[0].CompanyName, sizeof(CustArray[0].CompanyName), &CustArray[0].NameLenOrInd);  
   retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, CustArray[0].Address, sizeof(CustArray[0].Address), &CustArray[0].AddressLenOrInd);  
   retcode = SQLBindCol(hstmt, 4, SQL_C_CHAR, CustArray[0].Phone, sizeof(CustArray[0].Phone), &CustArray[0].PhoneLenOrInd);  
  
   // Execute a statement to retrieve rows from the Customers table.  
   retcode = SQLExecDirect(hstmt, (SQLCHAR*)"SELECT CustomerID, CompanyName, Address, Phone FROM Customers", SQL_NTS);  
  
   // Fetch and display the first 10 rows.  
   retcode = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
   // DisplayCustData(CustArray, 10);  
  
   // Call GetAction to get an action and a row number from the user.  
   // while (GetAction(&Action, &RowNum)) {  
   Action = SQL_FETCH_NEXT;  
   RowNum = 2;  
   switch (Action) {  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmt, Action, RowNum);  
         // DisplayCustData(CustArray, 10);  
         break;  
  
      case UPDATE_ROW:  
         // Check if we have reached the maximum number of buffered updates.  
         if (NumUpdates < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered updates section of CustArray, copy the bookmark of the row  
            // being updated to the same element, and increment the update counter.  
            // Checking to see we have not already buffered an update for this  
            // row not shown.  
            // GetNewCustData(CustArray, UPDATE_OFFSET + NumUpdates);  
            memcpy(CustArray[UPDATE_OFFSET + NumUpdates].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
            CustArray[UPDATE_OFFSET + NumUpdates].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
            NumUpdates++;  
         } else {  
            printf("Buffers full. Send buffered changes to the data source.");  
         }  
         break;  
      case DELETE_ROW:  
         // Check if we have reached the maximum number of buffered deletes.  
         if (NumDeletes < 10) {  
            // Copy the bookmark of the row being deleted to the next available element  
            // of the buffered deletes section of CustArray and increment the delete  
            // counter. Checking to see we have not already buffered an update for  
            // this row not shown.  
            memcpy(CustArray[DELETE_OFFSET + NumDeletes].Bookmark,  
               CustArray[RowNum - 1].Bookmark,  
               CustArray[RowNum - 1].BookmarkLen);  
  
            CustArray[DELETE_OFFSET + NumDeletes].BookmarkLen =  
               CustArray[RowNum - 1].BookmarkLen;  
  
            NumDeletes++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case ADD_ROW:  
         // reached maximum number of buffered inserts?  
         if (NumInserts < 10) {  
            // Get the new customer data and place it in the next available element of  
            // the buffered inserts section of CustArray and increment insert counter.  
            // GetNewCustData(CustArray, INSERT_OFFSET + NumInserts);  
            NumInserts++;  
         } else  
            printf("Buffers full. Send buffered changes to the data source.");  
         break;  
  
      case SEND_TO_DATA_SOURCE:  
         // If there are any buffered updates, inserts, or deletes, set the array size  
         // to that number, set the binding offset to use the data in the buffered  
         // update, insert, or delete part of CustArray, and call SQLBulkOperations to  
         // do the updates, inserts, or deletes. Because we will never have more than  
         // 10 updates, inserts, or deletes, we can use the same row status array.  
         if (NumUpdates) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumUpdates, 0);  
            BindOffset = UPDATE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_UPDATE_BY_BOOKMARK);  
            NumUpdates = 0;  
         }  
  
         if (NumInserts) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumInserts, 0);  
            BindOffset = INSERT_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_ADD);  
            NumInserts = 0;  
         }  
  
         if (NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)NumDeletes, 0);  
            BindOffset = DELETE_OFFSET * sizeof(CustStruct);  
            SQLBulkOperations(hstmt, SQL_DELETE_BY_BOOKMARK);  
            NumDeletes = 0;  
         }  
  
         // If there were any updates, inserts, or deletes, reset the binding offset  
         // and array size to their original values.  
         if (NumUpdates || NumInserts || NumDeletes) {  
            SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER)10, 0);  
            BindOffset = 0;  
         }  
         break;  
   }  
   // }  
  
   // Close the cursor.  
   SQLFreeStmt(hstmt, SQL_CLOSE);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述符的單欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述符的多個字段|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定描述符的單欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定描述符的多個字欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|定位游標、刷新列集中中的資料或更新或移除列集中中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
