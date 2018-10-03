---
title: SQLBulkOperations 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBulkOperations
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBulkOperations
helpviewer_keywords:
- SQLBulkOperations function [ODBC]
ms.assetid: 7029d0da-b0f2-44e6-9114-50bd96f47196
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d59e4d93b082312b6ae33fc3c2e2ca1e4177c771
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47815172"
---
# <a name="sqlbulkoperations-function"></a>SQLBulkOperations 函式
**合規性**  
 版本導入： ODBC 3.0 版的標準符合性： ODBC  
  
 **摘要**  
 **SQLBulkOperations**會執行大量插入以及大量的書籤的作業，包括更新、 刪除和擷取書籤。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLBulkOperations(  
     SQLHSTMT       StatementHandle,  
     SQLUSMALLINT   Operation);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *運算*  
 [輸入]若要執行的作業：  
  
 SQL_ADD SQL_UPDATE_BY_BOOKMARK SQL_DELETE_BY_BOOKMARK SQL_FETCH_BY_BOOKMARK  
  
 如需詳細資訊，請參閱 「 註解。 」  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBulkOperations**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLBulkOperations** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前的驅動程式管理員所傳回的 Sqlstate 的描述. 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
 針對所有這些 Sqlstate 可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除了 01xxx Sqlstate)，如果一個或多個，而非全部的資料列的多資料列的作業，發生錯誤，而且如果發生錯誤時，會傳回 SQL_ERROR，則會傳回 SQL_SUCCESS_WITH_INFO單一資料列作業。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料右側截斷|*作業*引數為 SQL_FETCH_BY_BOOKMARK，以及字串或二進位資料傳回的資料行或資料行資料類型為 SQL_C_CHAR 或 SQL_C_BINARY 導致的非空白的字元或非 NULL 的二進位資料截斷。|  
|01S01|資料列中的錯誤|*作業*引數 SQL_ADD，和時發生一或多個資料列中執行的作業卻已成功加入至少一個資料列。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> （只有在應用程式使用 ODBC 2 時，會引發此錯誤。*x*驅動程式。)|  
|01S07|小數位數截斷|*作業*引數 SQL_FETCH_BY_BOOKMARK、 應用程式緩衝區的資料類型不是 SQL_C_CHAR 或 SQL_C_BINARY 而且傳回的一或多個資料行的應用程式緩衝區的資料已被截斷。 （數字的 C 資料類型的數字的小數部分已遭截斷。 時間、 時間戳記，和包含時間元件的 interval C 資料類型，時間的小數部分截斷。）<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|*作業*引數為 SQL_FETCH_BY_BOOKMARK，並在結果集中的資料行的資料值無法轉換成所指定的資料類型*TargetType* 呼叫中的引數**SQLBindCol**。<br /><br /> *作業*引數為 SQL_UPDATE_BY_BOOKMARK 或 SQL_ADD，和應用程式緩衝區中的資料值無法轉換成資料類型的結果集中的資料行。|  
|07009|描述項索引無效|引數*作業*SQL_ADD，並使用大於結果集中的資料行數目的數字資料行繫結資料行。|  
|21S02|衍生資料表的程度與資料行清單不符|引數*作業*SQL_UPDATE_BY_BOOKMARK; 並沒有資料行已更新，因為所有資料行解除繫結或是唯讀的或繫結的長度/指標緩衝區中的值為 SQL_COLUMN_IGNORE。|  
|22001|字串資料右側截斷|字元或二進位值，以在結果集中的資料行指派導致截斷的非空白 （適用於字元） 或 （適用於二進位） 的非 null 字元或位元組。|  
|22003|數值超出範圍|*作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，並指派一個數值，結果集中的資料行導致要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 引數*作業*SQL_FETCH_BY_BOOKMARK，並傳回一或多個繫結的資料行的數值可能會導致遺失有效位數。|  
|22007|無效的日期時間格式|*作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，和指派的結果集中的資料行的日期或時間戳記值造成年、 月或日欄位超出範圍。<br /><br /> 引數*作業*SQL_FETCH_BY_BOOKMARK，並傳回一或多個繫結的資料行的日期或時間戳記值會造成年、 月或日欄位超出範圍。|  
|22008|日期/時間欄位溢位|*作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，並對資料傳送至結果集中的資料行的日期時間的效能造成日期時間欄位 （年、 月、 日、 小時、 分鐘或秒欄位） 的欄位值的允許的範圍切換或正在無效根據西曆的日期時間的自然規則的結果。<br /><br /> *作業*引數為 SQL_FETCH_BY_BOOKMARK，且運算的結果集從擷取的資料的日期時間的效能造成 datetime （年、 月、 日、 小時、 分鐘或第二個欄位） 的欄位欄位的值允許的範圍切換或無效的結果會根據西曆日曆的日期時間的自然規則。|  
|22015|間隔欄位溢位|*作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，和指派的精確數值或 SQL 資料類型的間隔的間隔 C 類型造成的有效位數遺失。<br /><br /> *作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 指派給 SQL 類型的間隔時，發生間隔 SQL 型別中的 C 類型的值不表示法。<br /><br /> *作業*引數為 SQL_FETCH_BY_BOOKMARK，並將指派從精確數值或時間間隔 SQL 型別，給 C 間隔類型造成的有效位數遺失開頭的欄位中。<br /><br /> *作業*引數是 SQL_FETCH_BY_BOOKMARK; 指派給間隔 C 類型時，發生 C 間隔類型中的 SQL 類型的值不表示法。|  
|22018|轉換規格的字元值無效|*作業*引數為 SQL_FETCH_BY_BOOKMARK; 的 C 類型為精確或近似數值、 日期時間或間隔資料類型; 資料行的 SQL 類型是字元資料類型; 和資料行中的值不是有效的繫結的 C 類型的常值。<br /><br /> 引數*作業*SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 的 SQL 型別為精確或近似數值、 日期時間或間隔資料類型; 的 C 類型是 SQL_C_CHAR; 和資料行中的值不是有效的常值繫結 SQL 型別。|  
|23000|完整性條件約束違規|*作業*引數 SQL_ADD、 SQL_DELETE_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，且違反完整性條件約束。<br /><br /> *作業*引數為 SQL_ADD，以及未繫結的資料行定義為 NOT NULL，而且沒有預設值。<br /><br /> *作業*引數已繫結中指定的長度，SQL_ADD *StrLen_or_IndPtr*緩衝區 SQL_COLUMN_IGNORE，且資料行沒有預設值。|  
|24000|指標狀態無效|*StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|驅動程式無法執行所要求的作業所需的鎖定資料列*作業*引數。|  
|44000|WITH CHECK OPTION 違規|*作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK，以及插入，或檢視的資料表上執行更新 （或衍生自檢視的資料表的資料表） 中建立指定**WITH CHECK OPTION**，方式插入作業所影響的一或多個資料列，或更新將不再會出現在檢視的資料表。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLBulkOperations**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 已呼叫的函式，但是未先呼叫**SQLExecDirect**， **SQLExecute**，或目錄函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 驅動程式的 ODBC 2。*x*驅動程式，並**SQLBulkOperations**針對呼叫*StatementHandle*之前**SQLFetchScroll**或**SQLFetch**呼叫。<br /><br /> (DM) **SQLBulkOperations**後才呼叫**SQLExtendedFetch**上呼叫*StatementHandle*。|  
|HY011|現在無法設定屬性|(DM) 驅動程式的 ODBC 2。*x*驅動程式，以及 sql_attr_row_status_ptr 設定陳述式屬性設定呼叫之間**SQLFetch**或是**SQLFetchScroll**並**SQLBulkOperations**.|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|*作業*引數為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK; 的資料值不是 null 指標; C 資料類型是否 SQL_C_BINARY SQL_C_CHAR; 和資料行的長度值小於 0，但不是等於 SQL_DATA_AT_EXECSQL_COLUMN_IGNORE、 SQL_NTS 或 SQL_NULL_DATA，或是小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指標緩衝區中的值為 SQL_DATA_AT_EXEC;SQL 類型是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或很長的資料來源特定的資料類型使用;和中的 SQL_NEED_LONG_DATA_LEN 資訊類型**SQLGetInfo**是"Y"。<br /><br /> *作業*引數為 SQL_ADD、 SQL_ATTR_USE_BOOKMARK 陳述式屬性設定為 SQL_UB_VARIABLE，且資料行 0 已繫結至其長度不等於此結果集的書籤的最大長度的緩衝區。 (這個長度的 SQL_DESC_OCTET_LENGTH IRD 欄位中而且可由呼叫**SQLDescribeCol**， **SQLColAttribute**，或**SQLGetDescField**。)|  
|HY092|無效的屬性識別碼|(DM) 指定的值*作業*引數無效。<br /><br /> *作業*引數為 SQL_ADD、 SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK，且 SQL_ATTR_CONCURRENCY 陳述式屬性已設定為 SQL_CONCUR_READ_ONLY。<br /><br /> *作業*引數為 SQL_DELETE_BY_BOOKMARK、 SQL_FETCH_BY_BOOKMARK 或 SQL_UPDATE_BY_BOOKMARK，且書籤資料行未繫結或 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設為 SQL_UB_OFF。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援要求中的作業*作業*引數。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**具有*屬性*SQL_ATTR_QUERY_TIMEOUT 引數。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]  
>  如需有關哪個陳述式表示資訊**SQLBulkOperations**可以呼叫而且它必須執行的 ODBC 2 的相容性。*x*應用程式，請參閱[區塊資料指標、 可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)附錄 g： 驅動程式的指導方針提供回溯相容性一節。  
  
 應用程式使用**SQLBulkOperations**來執行下列作業的基底資料表或檢視對應到目前的查詢：  
  
-   加入新的資料列。  
  
-   更新資料列，其中依書籤識別每個資料列的集。  
  
-   刪除資料列，其中依書籤識別每個資料列的集。  
  
-   擷取一組資料列，其中依書籤識別每個資料列。  
  
 若要在呼叫之後**SQLBulkOperations**，區塊資料指標位置會是未定義。 應用程式必須呼叫**SQLFetchScroll**來設定資料指標位置。 應用程式應該呼叫**SQLFetchScroll**只能搭配*Sqlfetchscroll* SQL_FETCH_FIRST、 SQL_FETCH_LAST、 SQL_FETCH_ABSOLUTE 或要使用 SQL_FETCH_BOOKMARK 的引數。 游標位置是未定義的如果應用程式會呼叫**SQLFetch**或是**SQLFetchScroll**具有*Sqlfetchscroll* SQL_FETCH_PRIOR，SQL_FETCH_NEXT，引數或SQL_FETCH_RELATIVE 但。  
  
 可以呼叫所執行的大量作業中忽略資料行**SQLBulkOperations**藉由設定的呼叫中指定的資料行長度/指標緩衝區**SQLBindCol**，到 SQL_COLUMN_IGNORE。  
  
 您不需要設定 SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性時它會呼叫應用程式**SQLBulkOperations**因為無法在執行大量作業，此函式使用時，忽略資料列。  
  
 指向 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性，緩衝區會包含呼叫受影響的資料列數目**SQLBulkOperations**。  
  
 當*作業*引數是 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK 而且資料指標相關聯的查詢規格的選取清單包含多個參考相同的資料行，它是驅動程式-定義是否發生錯誤產生或驅動程式會忽略重複的參考，並且會執行要求的作業。  
  
 如需有關如何使用**SQLBulkOperations**，請參閱[更新的資料，使用 SQLBulkOperations](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)。  
  
## <a name="performing-bulk-inserts"></a>執行大量插入  
 若要使用插入資料**SQLBulkOperations**，應用程式執行下列步驟順序：  
  
1.  執行查詢，以傳回結果集。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性，設定想要插入的資料列數目。  
  
3.  呼叫**SQLBindCol**將它想要插入的資料繫結。 資料繫結至陣列的大小等於 SQL_ATTR_ROW_ARRAY_SIZE 的值。  
  
    > [!NOTE]  
    >  Sql_attr_row_status_ptr 設定陳述式屬性所指陣列的大小應該是等於 SQL_ATTR_ROW_ARRAY_SIZE 或 sql_attr_row_status_ptr 設定應該是 null 指標。  
  
4.  呼叫**SQLBulkOperations**(*StatementHandle，* SQL_ADD) 以執行插入。  
  
5.  如果應用程式已設定 sql_attr_row_status_ptr 設定陳述式屬性，它可以檢查這個陣列，若要查看作業的結果。  
  
 如果應用程式在呼叫之前，將繫結資料行 0 **SQLBulkOperations**具有*作業*SQL_ADD 引數，此驅動程式將會更新繫結的資料行 0 緩衝區的書籤值新插入的資料列。 進行這項連線，應用程式必須已設定 SQL_ATTR_USE_BOOKMARKS 陳述式屬性將 SQL_UB_VARIABLE 執行陳述式之前。 （這不適用於 ODBC 2。*x*驅動程式。)  
  
 Long 資料可以在中加入組件 SQLBulkOperations，藉由使用 SQLParamData 和 SQLPutData 呼叫。 如需詳細資訊，請參閱此函式的參考後面的 「 提供長資料大量插入和更新 」。  
  
 您不需要應用程式以呼叫**SQLFetch**或**SQLFetchScroll**再呼叫**SQLBulkOperations** (除了時針對 ODBC 2。*x*驅動程式; 請參閱[回溯相容性與標準相容性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md))。  
  
 行為是驅動程式定義如果**SQLBulkOperations**，以*作業*SQL_ADD，引數含有重複的資料行的資料指標上呼叫。 驅動程式可以傳回驅動程式定義的 SQLSTATE 中，加入要出現在結果中的第一個資料行的資料集，或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-updates-by-using-bookmarks"></a>使用書籤執行大量更新  
 使用來執行大量更新與書籤**SQLBulkOperations**，應用程式順序執行下列步驟：  
  
1.  設定 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 陳述式屬性。  
  
2.  執行查詢，以傳回結果集。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性，設定想要更新的資料列數目。  
  
4.  呼叫**SQLBindCol**將它想要更新的資料繫結。 資料繫結至陣列的大小等於 SQL_ATTR_ROW_ARRAY_SIZE 的值。 它也會呼叫**SQLBindCol**繫結資料行 0 （書籤資料行）。  
  
5.  複製有它所需要的更新陣列中的資料列的書籤的繫結至資料行 0。  
  
6.  更新繫結的緩衝區中的資料。  
  
    > [!NOTE]  
    >  Sql_attr_row_status_ptr 設定陳述式屬性所指陣列的大小應該是等於 SQL_ATTR_ROW_ARRAY_SIZE 或 sql_attr_row_status_ptr 設定應該是 null 指標。  
  
7.  呼叫**SQLBulkOperations**(*StatementHandle，* SQL_UPDATE_BY_BOOKMARK)。  
  
    > [!NOTE]  
    >  如果應用程式已設定 sql_attr_row_status_ptr 設定陳述式屬性，它可以檢查這個陣列，若要查看作業的結果。  
  
8.  選擇性地呼叫**SQLBulkOperations**(*StatementHandle*，SQL_FETCH_BY_BOOKMARK) 擷取資料到繫結的應用程式緩衝區，以確認更新已發生。  
  
9. 如果資料已更新，則驅動程式會將適當的資料列的資料列狀態陣列中的值變成 SQL_ROW_UPDATED。  
  
 大量更新由**SQLBulkOperations**可以藉由呼叫包含 long 資料**SQLParamData**並**SQLPutData**。 如需詳細資訊，請參閱此函式的參考後面的 「 提供長資料大量插入和更新 」。  
  
 如果保存跨資料指標的書籤，應用程式不需要呼叫**SQLFetch**或是**SQLFetchScroll**之前更新的書籤。 它可以使用它已從先前的資料指標中儲存的書籤。 書籤不會保存跨資料指標，如果應用程式必須呼叫**SQLFetch**或是**SQLFetchScroll**擷取書籤。  
  
 行為是驅動程式定義如果**SQLBulkOperations**，以*作業*SQL_UPDATE_BY_BOOKMARK，引數含有重複的資料行的資料指標上呼叫。 驅動程式可傳回驅動程式定義的 SQLSTATE、 更新會出現在結果集中，第一個資料行，或執行其他驅動程式定義的行為。  
  
## <a name="performing-bulk-fetches-using-bookmarks"></a>執行大量擷取使用書籤  
 若要執行使用書籤與大量擷取**SQLBulkOperations**，應用程式順序執行下列步驟：  
  
1.  設定 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 陳述式屬性。  
  
2.  執行查詢，以傳回結果集。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性，設定想要擷取的資料列數目。  
  
4.  呼叫**SQLBindCol**將它想要擷取的資料繫結。 資料繫結至陣列的大小等於 SQL_ATTR_ROW_ARRAY_SIZE 的值。 它也會呼叫**SQLBindCol**繫結資料行 0 （書籤資料行）。  
  
5.  複製有它所需要的陣列中擷取的資料列的書籤的繫結至資料行 0。 （這假設應用程式已取得的書籤分開）。  
  
    > [!NOTE]  
    >  Sql_attr_row_status_ptr 設定陳述式屬性所指陣列的大小應該是等於 SQL_ATTR_ROW_ARRAY_SIZE 或 sql_attr_row_status_ptr 設定應該是 null 指標。  
  
6.  呼叫**SQLBulkOperations**(*StatementHandle，* SQL_FETCH_BY_BOOKMARK)。  
  
7.  如果應用程式已設定 sql_attr_row_status_ptr 設定陳述式屬性，它可以檢查這個陣列，若要查看作業的結果。  
  
 書籤保存跨資料指標，如果應用程式不需要呼叫**SQLFetch**或是**SQLFetchScroll**之前擷取的書籤。 它可以使用它已從先前的資料指標中儲存的書籤。 書籤不會保存跨資料指標，如果應用程式必須呼叫**SQLFetch**或是**SQLFetchScroll**一次，以擷取書籤。  
  
## <a name="performing-bulk-deletes-using-bookmarks"></a>執行大量刪除使用書籤  
 若要執行大量刪除使用與書籤**SQLBulkOperations**，應用程式順序執行下列步驟：  
  
1.  設定 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 陳述式屬性。  
  
2.  執行查詢，以傳回結果集。  
  
3.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性，設定想要刪除的資料列數目。  
  
4.  呼叫**SQLBindCol**繫結資料行 0 （書籤資料行）。  
  
5.  複製有它所需要的刪除陣列中的資料列的書籤的繫結至資料行 0。  
  
    > [!NOTE]  
    >  Sql_attr_row_status_ptr 設定陳述式屬性所指陣列的大小應該是等於 SQL_ATTR_ROW_ARRAY_SIZE 或 sql_attr_row_status_ptr 設定應該是 null 指標。  
  
6.  呼叫**SQLBulkOperations**(*StatementHandle，* SQL_DELETE_BY_BOOKMARK)。  
  
7.  如果應用程式已設定 sql_attr_row_status_ptr 設定陳述式屬性，它可以檢查這個陣列，若要查看作業的結果。  
  
 如果保存跨資料指標的書籤，應用程式沒有呼叫**SQLFetch**或是**SQLFetchScroll**之前刪除的書籤。 它可以使用它已從先前的資料指標中儲存的書籤。 書籤不會保存跨資料指標，如果應用程式必須呼叫**SQLFetch**或是**SQLFetchScroll**一次，以擷取書籤。  
  
## <a name="providing-long-data-for-bulk-inserts-and-updates"></a>提供完整的資料大量插入與更新  
 Long 資料可供 bulk insert 及 update 呼叫執行的**SQLBulkOperations**。 插入或更新的 long 資料，應用程式會執行下列步驟，除了 「 執行大量插入 」 和 「 執行大量更新使用書籤 」 區段中稍早在本主題中所述的步驟。  
  
1.  當它的資料繫結使用**SQLBindCol**，應用程式就會進入應用程式定義值，例如資料行編號 *\*TargetValuePtr*執行資料的緩衝區資料行。 值可以用來識別的資料行的更新版本。  
  
     應用程式會放 SQL_LEN_DATA_AT_EXEC 的結果 (*長度*) 中的巨集 *\*StrLen_or_IndPtr*緩衝區。 如果 SQL 資料類型的資料行是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或 long 資料來源特定的資料類型和驅動程式會傳回"Y"表示 SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo**，*長度*是參數; 傳送資料的位元組數目，否則必須為非負數值，並會被忽略。  
  
2.  當**SQLBulkOperations**呼叫時，如果有資料在執行中資料行，函數會傳回 SQL_NEED_DATA，繼續進行步驟 3 中，哪一種。 （如果沒有執行資料的資料行，此程序已完成。）  
  
3.  應用程式會呼叫**SQLParamData**擷取的地址 *\*TargetValuePtr*第一個要處理的資料在執行資料行的緩衝區。 **SQLParamData**會傳回 SQL_NEED_DATA。 應用程式擷取應用程式定義的值，從 *\*TargetValuePtr*緩衝區。  
  
    > [!NOTE]  
    >  雖然資料在執行中參數類似於資料在執行中資料行，所傳回的值**SQLParamData**每個不同。  
  
     資料在執行中資料行是資料會傳送使用資料列集中的資料行**SQLPutData**更新或插入資料列時**SQLBulkOperations**。 使用繫結**SQLBindCol**。 所傳回的值**SQLParamData**是中的資料列的地址 **TargetValuePtr*正在處理的緩衝區。  
  
4.  應用程式會呼叫**SQLPutData**一或多次來傳送資料行的資料。 如果無法以傳回所有資料值，就需要超過一次呼叫 *\*TargetValuePtr*中指定的緩衝區**SQLPutData**; 多次呼叫**SQLPutData**或傳送二進位的 C 資料行的字元、 二進位，傳送字元 C 資料行的字元、 二進位檔或資料來源特定的資料型別時，只允許相同的資料行或資料來源特有的資料型別。  
  
5.  應用程式會呼叫**SQLParamData**再次來表示，所有資料都傳送的資料行。  
  
    -   如果有更多的資料在執行資料行**SQLParamData**會傳回 SQL_NEED_DATA 和位址*TargetValuePtr*緩衝區的下一個處理的資料在執行資料行。 應用程式會重複步驟 4 和 5。  
  
    -   如果沒有其他資料在執行中資料行，此程序已完成。 如果陳述式執行成功， **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果執行失敗，則會傳回 SQL_ERROR。 在此時**SQLParamData**可能會傳回任何可傳回的 SQLSTATE **SQLBulkOperations**。  
  
 如果在作業取消或發生錯誤時**SQLParamData**或**SQLPutData**之後**SQLBulkOperations**會傳回 SQL_NEED_DATA，資料會傳送所有之前資料在執行中資料行，應用程式可以只呼叫**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**陳述式或陳述式相關聯的連接。 如果陳述式或陳述式相關聯的連接，它就會呼叫其他函式，則函數會傳回 SQL_ERROR，而且 SQLSTATE HY010 （函數順序錯誤）。  
  
 如果應用程式會呼叫**SQLCancel**驅動程式時驅動程式仍需要資料的資料在執行中資料行時，取消作業。 應用程式接著可以呼叫**SQLBulkOperations**再次; 取消不會影響資料指標狀態或目前的游標位置。  
  
## <a name="row-status-array"></a>資料列狀態陣列  
 資料列狀態陣列會包含每個資料列集中的資料列的 status 值之後呼叫**SQLBulkOperations**。 驅動程式呼叫之後，此陣列中設定狀態值**SQLFetch**， **SQLFetchScroll**， **SQLSetPos**，或**SQLBulkOperations**. 這個陣列一開始填入藉由呼叫**SQLBulkOperations**如果**SQLFetch**或是**SQLFetchScroll**之前尚未呼叫**SQLBulkOperations**. 這個陣列會指到 sql_attr_row_status_ptr 設定陳述式屬性。 在資料列狀態陣列中的項目數必須等於資料列集 （如 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性所定義） 中的資料列數目。 此資料列狀態陣列的相關資訊，請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下列範例會從 [客戶] 資料表擷取一次的 10 個資料列的資料。 然後，它會提示使用者輸入動作來採取。 若要減少網路流量，範例緩衝區更新、 刪除，並將在本機插入，繫結的陣列，但在過去的資料列集資料的位移。 當使用者選擇要傳送更新、 刪除和插入到資料來源時，設定適當位移的繫結的程式碼，並呼叫**SQLBulkOperations**。 為了簡單起見，使用者無法緩衝的 10 個以上的更新、 刪除或插入。  
  
```  
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
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述元的單一欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述元的多個欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定的單一欄位的描述元|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個欄位的描述元|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|遊標定位、 重新整理此資料列集中，或更新或刪除資料列集中的資料|[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
