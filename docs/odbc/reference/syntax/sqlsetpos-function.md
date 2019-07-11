---
title: SQLSetPos 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63bca42adcdfc83d1bdb96361680d0c70c9a031c
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793132"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函式
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLSetPos**設定資料列集中的資料指標位置，並允許應用程式來重新整理資料列集中的資料，或是更新或刪除在結果集中的資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *RowNumber*  
 [輸入]在其上執行作業使用指定的資料列集資料列的位置*作業*引數。 如果*RowNumber*為 0，將作業套用至資料列集中的每個資料列。  
  
 如需詳細資訊，請參閱 「 註解。 」  
  
 *運算*  
 [輸入]若要執行的作業：  
  
 SQL_POSITION SQL_REFRESH SQL_UPDATE SQL_DELETE  
  
> [!NOTE]
>  SQL_ADD algoritmus*作業*引數已被取代適用於 ODBC *3.x*。 ODBC *3.x*支援回溯相容性的 SQL_ADD 所需的驅動程式。 這項功能已取代的呼叫所**SQLBulkOperations**具有*作業*SQL_ADD。 當 ODBC *3.x*應用程式會使用 ODBC *2.x*驅動程式，驅動程式管理員會對應到呼叫**SQLBulkOperations**具有*作業*的以 SQL_ADD **SQLSetPos**具有*作業*SQL_ADD。  
  
 如需詳細資訊，請參閱 「 註解。 」  
  
 *LockType*  
 [輸入]指定如何在執行中指定的作業之後鎖定資料列*作業*引數。  
  
 SQL_LOCK_NO_CHANGE SQL_LOCK_EXCLUSIVE SQL_LOCK_UNLOCK  
  
 如需詳細資訊，請參閱 「 註解。 」  
  
 **傳回**  
  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NEED_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetPos**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSetPos** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
 針對所有這些 Sqlstate 可傳回 SQL_SUCCESS_WITH_INFO 或 SQL_ERROR （除了 01xxx Sqlstate)，如果一個或多個，而非全部的資料列的多資料列的作業，發生錯誤，而且如果發生錯誤時，會傳回 SQL_ERROR，則會傳回 SQL_SUCCESS_WITH_INFO單一資料列作業。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01001|資料指標作業衝突|*作業*引數為 SQL_DELETE 或 SQL_UPDATE，和任何資料列或多個資料列已刪除或更新。 (如需有關更新多個資料列的詳細資訊，請參閱 SQL_ATTR_SIMULATE_CURSOR 描述*屬性*中**SQLSetStmtAttr**。)（函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> *作業*引數為 SQL_DELETE 或 SQL_UPDATE，和作業失敗，因為開放式並行存取。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料右側截斷|*作業*引數為 SQL_REFRESH，以及字串或二進位資料傳回的資料行或資料行資料類型為 SQL_C_CHAR 或 SQL_C_BINARY 導致的非空白的字元或非 NULL 的二進位資料截斷。|  
|01S01|資料列中的錯誤|*RowNumber*引數為 0，並執行時發生錯誤一或多個資料列中具有指定的作業*作業*引數。<br /><br /> （如果上一個或多個，而非全部的資料列的多資料列的作業，發生錯誤，而且在單一資料列的作業發生錯誤時，會傳回 SQL_ERROR 會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> (此 SQLSTATE 會傳回時，才**SQLSetPos**之後，會呼叫**SQLExtendedFetch**，如果驅動程式為 ODBC *2.x*不會使用驅動程式和資料指標程式庫。)|  
|01S07|小數位數截斷|*作業*引數 SQL_REFRESH、 應用程式緩衝區的資料類型不是 SQL_C_CHAR 或 SQL_C_BINARY 而且傳回的一或多個資料行的應用程式緩衝區的資料已被截斷。 數值資料類型已遭截斷數字的小數部分。 時間、 時間戳記，和包含時間元件的 interval 資料類型，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|在結果集中的資料行的資料值無法轉換成所指定的資料類型*TargetType*呼叫中**SQLBindCol**。|  
|07009|描述項索引無效|引數*作業*SQL_REFRESH 或 SQL_UPDATE，和資料行已繫結與結果集資料行的數目大於資料行編號。|  
|21S02|衍生資料表的程度與資料行清單不符|引數*作業*SQL_UPDATE，且沒有資料行已更新，因為所有資料行可能為未繫結、 唯讀的或繫結的長度/指標緩衝區中的值為 SQL_COLUMN_IGNORE。|  
|22001|字串資料，右側截斷|*作業*引數為 SQL_UPDATE，並導致截斷 （適用於字元為單位） 的非空白或 （適用於二進位） 的非 null 字元或位元組的字元或二進位資料行的值指派。|  
|22003|數值超出範圍|引數*作業*SQL_UPDATE，並指派一個數值，結果集中的資料行導致要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 引數*作業*SQL_REFRESH，並傳回一或多個繫結的資料行的數值可能會導致遺失有效位數。|  
|22007|無效的日期時間格式|引數*作業*SQL_UPDATE，並指派結果集中的資料行的日期或時間戳記值造成年、 月或日欄位超出範圍。<br /><br /> 引數*作業*SQL_REFRESH，並傳回一或多個繫結的資料行的日期或時間戳記值會造成年、 月或日欄位超出範圍。|  
|22008|日期/時間欄位溢位|*作業*引數為 SQL_UPDATE，且運算的資料傳送至結果集中的資料行的日期時間的效能造成之結果的日期時間欄位 （年、 月、 日、 小時、 分鐘或第二個欄位）以外的欄位，或無效的值所允許的範圍會根據西曆日曆的日期時間的自然規則。<br /><br /> *作業*引數為 SQL_REFRESH，且運算的結果集從擷取的資料的日期時間的效能造成之結果的日期時間欄位 （年、 月、 日、 小時、 分鐘或第二個欄位）以外的欄位，或無效的值所允許的範圍會根據西曆日曆的日期時間的自然規則。|  
|22015|間隔欄位溢位|*作業*引數為 SQL_UPDATE，和指派的精確數值或 SQL 資料類型的間隔的間隔 C 類型造成的有效位數遺失。<br /><br /> *作業*引數是 SQL_UPDATE; 指派給 SQL 類型的間隔時，發生間隔 SQL 型別中的 C 類型的值不表示法。<br /><br /> *作業*引數為 SQL_REFRESH，並將指派從精確數值或時間間隔 SQL 型別，給 C 間隔類型造成的有效位數遺失開頭的欄位中。<br /><br /> *作業*引數已重新整理 SQL_; 指派給間隔 C 類型時，發生 C 間隔類型中的 SQL 類型的值不表示法。|  
|22018|轉換規格的字元值無效|*作業*引數為 SQL_REFRESH; 的 C 類型為精確或近似數值、 日期時間或間隔資料類型; 資料行的 SQL 類型是字元資料類型; 和資料行中的值不是有效的常值繫結 C 類型。<br /><br /> 引數*作業*已 SQL_UPDATE; 的 SQL 型別為精確或近似數值、 日期時間或間隔資料類型; 的 C 類型是 SQL_C_CHAR; 和資料行中的值不是有效的常值的繫結的 SQL 類型。|  
|23000|完整性條件約束違規|引數*作業*SQL_DELETE 或 SQL_UPDATE，以及是否違反完整性條件約束。|  
|24000|指標狀態無效|*StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。<br /><br /> (DM) 資料指標是開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。<br /><br /> 資料指標是開啟*StatementHandle*，並**SQLFetch**或**SQLFetchScroll**呼叫，但指標置於開始或之後的結果集之前結果集的結尾。<br /><br /> 引數*作業*為 SQL_DELETE、 SQL_REFRESH 或 SQL_UPDATE，和指標置於結果集或結果集的結尾之後開始之前。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|42000|語法錯誤或存取違規|驅動程式無法執行要求的引數中的作業所需的鎖定資料列*作業*。<br /><br /> 驅動程式無法鎖定該資料列的引數中的要求*LockType*。|  
|44000|WITH CHECK OPTION 違規|*作業*引數為 SQL_UPDATE，和檢視的資料表上執行更新或衍生自檢視的資料表，這藉由指定所建立的資料表**WITH CHECK OPTION**，讓一或多個資料列受影響的更新將不再會出現在檢視的資料表。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，並接著呼叫函式上再次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍執行時呼叫 SQLSetPos 函式。<br /><br /> (DM) 指定*StatementHandle*不處於執行狀態。 已呼叫的函式，但是未先呼叫**SQLExecDirect**， **SQLExecute**，或目錄函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) 驅動程式的 ODBC *2.x*驅動程式，並**SQLSetPos**針對呼叫*StatementHandle*之後**SQLFetch**呼叫。|  
|HY011|現在無法設定屬性|(DM) 驅動程式的 ODBC *2.x*驅動程式; sql_attr_row_status_ptr 設定陳述式屬性已設定，然後**SQLSetPos**之前已呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**呼叫。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|*作業*引數為 SQL_UPDATE、 資料值是 null 指標，和資料行長度值不是 0，SQL_DATA_AT_EXEC，SQL_COLUMN_IGNORE SQL_NULL_DATA，或是小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> *作業*引數為 SQL_UPDATE; 的資料值不是 null 指標; C 資料類型是否 SQL_C_BINARY SQL_C_CHAR; 和資料行的長度值小於 0，但不是等於 SQL_DATA_AT_EXEC，SQL_COLUMN_IGNORESQL_NTS 或 SQL_NULL_DATA，或是小於或等於 SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指標緩衝區中的值為 SQL_DATA_AT_EXEC;SQL 類型是 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或很長的資料來源特有的資料類型使用;和中的 SQL_NEED_LONG_DATA_LEN 資訊類型**SQLGetInfo**是"Y"。|  
|HY092|無效的屬性識別碼|(DM) 指定的值*作業*引數無效。<br /><br /> (DM) 指定的值*LockType*引數無效。<br /><br /> *作業*引數是 SQL_UPDATE 或 SQL_DELETE，而 SQL_ATTR_CONCURRENCY 陳述式屬性是 SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|資料列值超出範圍|指定的引數的值*RowNumber*大於資料列集中的資料列數目。|  
|HY109|無效的資料指標位置|與相關聯的游標*StatementHandle*定義為順向的因此資料指標不可以位於資料列集內。 請參閱中的 SQL_ATTR_CURSOR_TYPE 屬性的描述**SQLSetStmtAttr**。<br /><br /> *作業*引數為 SQL_UPDATE、 SQL_DELETE 或 SQL_REFRESH，以及所識別的資料列*RowNumber*引數都已刪除或尚未擷取。<br /><br /> (DM) *RowNumber*引數為 0，而*作業*引數為 SQL_POSITION。<br /><br /> **SQLSetPos**後才呼叫**SQLBulkOperations**呼叫，以及之前**SQLFetchScroll**或是**SQLFetch**呼叫。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援要求中的作業*作業*引數或有*LockType*引數。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**具有*屬性*的 sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]
>  針對陳述式上的資訊指出**SQLSetPos**可以呼叫，而且需要進行相容性，使用 ODBC *2.x*應用程式，請參閱[區塊資料指標、 可捲動資料指標，和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>RowNumber 引數  
 *RowNumber*引數會指定在其上執行所指定的作業資料列集中的資料列編號*作業*引數。 如果*RowNumber*為 0，將作業套用至資料列集中的每個資料列。 *RowNumber*必須是介於 0 到資料列集中的資料列數目的值。  
  
> [!NOTE]  
>  在 C 語言中，陣列是以 0 為基礎而*RowNumber*引數是以 1 為基礎。 例如，若要更新資料列集的第五個資料列，應用程式修改資料列集緩衝區的陣列索引 4，但指定*RowNumber*為 5。  
  
 所有作業會將游標都放在指定的資料列*RowNumber*。 下列作業需要的資料指標位置：  
  
-   定位 update 和 delete 陳述式。  
  
-   若要呼叫**SQLGetData**。  
  
-   若要呼叫**SQLSetPos** SQL_DELETE、 SQL_REFRESH 和 SQL_UPDATE 選項。  
  
 比方說，如果*RowNumber*為 2 來呼叫**SQLSetPos**具有*作業*SQL_DELETE 的資料指標位於資料列集的第二個資料列，並刪除該資料列。 實作資料列狀態陣列 （由指向 sql_attr_row_status_ptr 設定陳述式屬性） 的第二個資料列中的項目會變更為 SQL_ROW_DELETED。  
  
 應用程式在呼叫時，可以指定資料指標位置**SQLSetPos**。 一般而言，它會呼叫**SQLSetPos** SQL_POSITION 或 SQL_REFRESH 作業，將游標放置之前執行定位更新或刪除陳述式或呼叫**SQLGetData**。  
  
## <a name="operation-argument"></a>運算引數  
 *作業*引數支援下列作業。 若要判斷資料來源所支援的選項，應用程式會呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1，或 SQL_STATIC_CURSOR_ATTRIBUTES1 （取決於資料指標類型） 的資訊類型。  
  
|*運算*<br /><br /> Argument - 引數|運算|  
|------------------------------|---------------|  
|SQL_POSITION|驅動程式會將游標置於指定的資料列*RowNumber*。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性所指的資料列狀態陣列的內容會忽略 SQL_POSITION*作業*。|  
|SQL_REFRESH|驅動程式會將游標置於指定的資料列*RowNumber*重新整理該資料列的資料列集緩衝區中的資料。 如需驅動程式的資料列集的緩衝區中所傳回的資料的詳細資訊，請參閱中的資料列取向和資料行取向繫結的說明**SQLBindCol**。<br /><br /> **SQLSetPos**具有*作業*SQL_REFRESH 的更新 狀態 和 目前的已擷取資料列集內的資料列的內容。 這包括重新整理書籤。 因為緩衝區中的資料重新整理，但不是 refetched，被固定的資料列集中的成員資格。 這點不同於呼叫所執行的重新整理**SQLFetchScroll**具有*Sqlfetchscroll*的 sql_fetch_relative，但並*RowNumber*等於 0，refetches如果驅動程式和資料指標支援這些作業，從結果集，讓它可以顯示加入的資料，並移除資料列集刪除資料。<br /><br /> 成功重新整理**SQLSetPos**不會變更資料列狀態為 SQL_ROW_DELETED。 已刪除的資料列集中的資料列會繼續將會標示為下一個擷取，才能刪除。 如果資料指標支援封裝，將會消失在下一個擷取的資料列 (在其中的後續**SQLFetch**或是**SQLFetchScroll**不會傳回已刪除的資料列)。<br /><br /> 加入資料列時的重新整理不會出現**SQLSetPos**會執行。 此行為是不同於**SQLFetchScroll**具有*FetchType*的 sql_fetch_relative 但和*RowNumber*等於 0，這也會重新整理但將目前資料列集顯示已新增的記錄，或組件已刪除的記錄，如果資料指標所支援這些作業。<br /><br /> 成功重新整理**SQLSetPos**會變成資料列狀態為 SQL_ROW_ADDED SQL_ROW_SUCCESS （如果資料列狀態陣列的話）。<br /><br /> 成功重新整理**SQLSetPos**會變成 SQL_ROW_UPDATED 資料列狀態的資料列的新狀態 （如果資料列狀態陣列的話）。<br /><br /> 如果發生錯誤時**SQLSetPos**作業的資料列，資料列狀態設定為 SQL_ROW_ERROR （如果資料列狀態陣列的話）。<br /><br /> 資料指標開啟 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES，以重新整理的陳述式屬性 SQL_ATTR_CONCURRENCY **SQLSetPos**可能會更新用來偵測到資料來源的開放式並行存取值資料列已經變更。 如果發生這種情況，用來確保資料指標並行值的資料列版本會會更新每次資料列集的緩衝區會從伺服器重新整理。 發生這種情況會重新整理每個資料列。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性所指的資料列狀態陣列的內容會忽略 SQL_REFRESH*作業*。|  
|SQL_UPDATE|驅動程式會將游標置於指定的資料列*RowNumber* ，並更新資料的基礎資料列與資料列集的緩衝區中的值 ( *TargetValuePtr*中的引數**SQLBindCol**)。 它會從長度/指標緩衝區中擷取之資料的長度 ( *StrLen_or_IndPtr*中的引數**SQLBindCol**)。 如果任何資料行的長度是 SQL_COLUMN_IGNORE，不會更新資料行。 在更新之後之資料列，驅動程式變更資料列狀態陣列對應的項的目 SQL_ROW_UPDATED 或 SQL_ROW_SUCCESS_WITH_INFO （如果資料列狀態陣列的話）。<br /><br /> 它是由驅動程式定義的行為的是如果**SQLSetPos**具有*作業*SQL_UPDATE 引數含有重複的資料行的資料指標上呼叫。 驅動程式可傳回驅動程式定義的 SQLSTATE、 可以更新第一個資料行，會出現在結果集中，或執行其他驅動程式定義的行為。<br /><br /> 資料列作業陣列指向 SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性可用來指出大量更新期間，應該忽略中目前資料列集的資料列。 如需詳細資訊，請參閱此函式的參考後面的 「 狀態和作業陣列 」。|  
|SQL_DELETE|驅動程式會將游標置於指定的資料列*RowNumber*並刪除基礎資料列的資料。 變更資料列狀態陣列的對應項目為 SQL_ROW_DELETED。 在刪除資料列之後，以下不是有效的資料列： 定位 update 和 delete 陳述式，呼叫**SQLGetData**，並呼叫**SQLSetPos**使用*作業*設定為 SQL_POSITION 以外的項目。 支援封裝的驅動程式，會在從資料指標刪除資料列從資料來源擷取新的資料時。<br /><br /> 是否在資料列仍保持可見，則資料指標類型而定。 比方說，已刪除的資料列會顯示靜態和索引鍵集驅動資料指標，但看不到動態資料指標。<br /><br /> 資料列作業陣列指向 SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性可用來指出大量刪除期間，應該忽略中目前資料列集的資料列。 如需詳細資訊，請參閱此函式的參考後面的 「 狀態和作業陣列 」。|  
  
## <a name="locktype-argument"></a>LockType 引數  
 *LockType*引數可讓應用程式來控制並行存取。 在大部分情況下，支援並行存取等級和交易的資料來源將會支援只有 SQL_LOCK_NO_CHANGE 值*LockType*引數。 *LockType*引數通常僅用於檔案為基礎的支援。  
  
 *LockType*引數會指定資料列之後的鎖定狀態**SQLSetPos**已經執行。 如果驅動程式無法鎖定該資料列來執行要求的作業，或滿足*LockType*引數，它會傳回 SQL_ERROR，而且 SQLSTATE 42000 （語法錯誤或存取違規）。  
  
 雖然*LockType*引數指定為單一陳述式，則鎖定 accords 連接上的所有陳述式的相同權限。 特別是，連接上一個陳述式所取得的鎖定來解除鎖定不同的陳述式，針對相同的連接。  
  
 透過鎖定的資料列**SQLSetPos**就會保持鎖定直到應用程式會呼叫**SQLSetPos**之資料列的*LockType*設定為 SQL_LOCK_UNLOCK，或直到應用程式呼叫**SQLFreeHandle**陳述式或**SQLFreeStmt** SQL_CLOSE 選項。 為支援交易的驅動程式，一個資料列鎖定透過**SQLSetPos**時，才能解除鎖定應用程式會呼叫**SQLEndTran**認可或回復交易在連接上 （如果資料指標已關閉當認可或回復，以傳回 SQL_CURSOR_COMMIT_BEHAVIOR 和 SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊類型的交易**SQLGetInfo**)。  
  
 *LockType*引數支援下列類型的鎖定。 若要判斷資料來源所支援的鎖定，應用程式會呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1，或 SQL_STATIC_CURSOR_ATTRIBUTES1 （取決於資料指標類型） 的資訊類型。  
  
|*LockType*引數|鎖定類型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驅動程式或資料來源可確保資料列在相同的鎖定或解除鎖定狀態跟以前**SQLSetPos**呼叫。 此值*LockType*可讓她能夠使用所需的任何鎖定是目前的並行存取和交易隔離層級的明確資料列層級鎖定不支援的資料來源。|  
|SQL_LOCK_EXCLUSIVE|驅動程式或資料來源以獨佔方式鎖定資料列。 對不同的連線，或在不同的應用程式中的陳述式無法用來取得任何資料列上的鎖定中。|  
|SQL_LOCK_UNLOCK|驅動程式或資料來源會解除鎖定資料列。|  
  
 如果驅動程式支援 SQL_LOCK_EXCLUSIVE，但不支援 SQL_LOCK_UNLOCK，已鎖定的資料列會保持鎖定，直到發生其中一種函式會呼叫先前段落中所述。  
  
 如果驅動程式支援 SQL_LOCK_EXCLUSIVE，但不支援 SQL_LOCK_UNLOCK，已鎖定的資料列就會保持鎖定直到應用程式會呼叫**SQLFreeHandle**陳述式或**SQLFreeStmt**與SQL_CLOSE 選項。 如果驅動程式支援交易，並關閉資料指標在認可或回復交易，應用程式會呼叫**SQLEndTran**。  
  
 在 update 和 delete 作業**SQLSetPos**，應用程式會使用*LockType*引數，如下所示：  
  
-   若要保證資料列不會變更擷取後，應用程式呼叫**SQLSetPos**與*作業*設為 SQL_REFRESH 並*LockType*設 SQL_LOCK_獨佔的。  
  
-   如果應用程式設定*LockType* SQL_LOCK_NO_CHANGE，來驅動程式可確保只有當應用程式指定 SQL_CONCUR_LOCK SQL_ATTR_CONCURRENCY 陳述式屬性，將會成功的 update 或 delete 作業。  
  
-   如果應用程式會指定 SQL_CONCUR_ROWVER 或 SQL_CONCUR_VALUES SQL_ATTR_CONCURRENCY 陳述式屬性，驅動程式會比較資料列版本或值，並且會拒絕該作業，如果資料列已經變更，因為應用程式提取資料列。  
  
-   如果應用程式指定 SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY 陳述式屬性，驅動程式會拒絕任何更新或刪除作業。  
  
 如需有關 SQL_ATTR_CONCURRENCY 陳述式屬性的詳細資訊，請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>狀態和作業陣列  
 呼叫時，會使用下列的狀態和作業陣列**SQLSetPos**:  
  
-   （如指向由 IRD 和 SQL_ATTR_ROW_STATUS_ARRAY 陳述式屬性的 SQL_DESC_ARRAY_STATUS_PTR 欄位），才會進行資料列狀態陣列包含每個資料列集中的資料列的 [狀態] 值。 驅動程式呼叫之後，此陣列中設定狀態值**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，或**SQLSetPos**. 這個陣列會指到 sql_attr_row_status_ptr 設定陳述式屬性。  
  
-   資料列作業陣列 （為指向由 ARD 和 SQL_ATTR_ROW_OPERATION_ARRAY 陳述式屬性的 SQL_DESC_ARRAY_STATUS_PTR 欄位） 包含的值，指出資料列集中的每個資料列是否呼叫**SQLSetPos**大量作業會略過或執行。 陣列中的每個項目設為 SQL_ROW_PROCEED （預設值） 或 SQL_ROW_IGNORE。 這個陣列會指到 SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性。  
  
 狀態和作業陣列中元素數目必須等於資料列集 （如 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性所定義） 中的資料列數目。  
  
 資料列狀態陣列的相關資訊，請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 如需資料列作業陣列的資訊，請參閱 「 略過資料列中大量作業，」 本節稍後的。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 應用程式呼叫之前**SQLSetPos**，它必須執行下列步驟順序：  
  
1.  如果應用程式會呼叫**SQLSetPos**具有*作業*設定為 SQL_UPDATE，呼叫**SQLBindCol** (或**SQLSetDescRec**) 針對每個若要指定其資料類型，並繫結的資料行的資料和長度的緩衝區的資料行。  
  
2.  如果應用程式會呼叫**SQLSetPos**具有*作業*設定為 SQL_DELETE] 或 [SQL_UPDATE，呼叫**SQLColAttribute** ，確定要刪除或更新的資料行為更新的資料表。  
  
3.  呼叫**SQLExecDirect**， **SQLExecute**，或目錄函式來建立結果集。  
  
4.  呼叫**SQLFetch**或是**SQLFetchScroll**來擷取資料。  
  
 如需使用詳細資訊**SQLSetPos**，請參閱[更新的資料，使用 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>使用 SQLSetPos 刪除資料  
 若要刪除的資料**SQLSetPos**，應用程式呼叫**SQLSetPos**具有*RowNumber*設定為資料列數目，以刪除和*作業*設定為 SQL_DELETE。  
  
 已刪除的資料之後，驅動程式會變更為 SQL_ROW_DELETED （或 SQL_ROW_ERROR） 的實作資料列狀態陣列，針對適當的資料列中的值。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新資料  
 應用程式可以將傳遞的資料行的值，繫結的資料緩衝區中或透過一或多個呼叫**SQLPutData**。 資料會使用傳遞的資料行**SQLPutData**又稱為*資料在執行* *資料行*。 這些通常用來傳送 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 資料行的資料，並可以混合使用與其他資料行。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>若要更新的資料使用 SQLSetPos，應用程式：  
  
1.  資料和長度/指標緩衝區中的位置值繫結**SQLBindCol**:  
  
    -   對於一般的資料行，應用程式會放在新的資料行值 *\*TargetValuePtr*緩衝區，並在該值的長度 *\*StrLen_or_IndPtr*緩衝區。 如果不應更新之資料列，則應用程式會將 SQL_ROW_IGNORE 置於該資料列的資料列作業陣列的項目。  
  
    -   執行資料的資料行，應用程式置於應用程式定義值，例如資料行編號 *\*TargetValuePtr*緩衝區。 值可以用來識別的資料行的更新版本。  
  
         應用程式會放 SQL_LEN_DATA_AT_EXEC 的結果 (*長度*) 中的巨集 **StrLen_or_IndPtr*緩衝區。 如果 SQL 資料類型的資料行是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或 long 資料來源特有的資料類型和驅動程式會傳回"Y"表示 SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo**，*長度*是參數; 傳送資料的位元組數目，否則必須為非負數值，並會被忽略。  
  
2.  呼叫**SQLSetPos**具有*作業*引數設定為 SQL_UPDATE，以更新資料的資料列。  
  
    -   如果沒有執行資料的資料行，此程序已完成。  
  
    -   如果有任何資料在執行中資料行，函數會傳回 SQL_NEED_DATA，並繼續進行步驟 3。  
  
3.  呼叫**SQLParamData**擷取的地址 *\*TargetValuePtr*第一個要處理的資料在執行資料行的緩衝區。 **SQLParamData**會傳回 SQL_NEED_DATA。 應用程式擷取應用程式定義的值，從 *\*TargetValuePtr*緩衝區。  
  
    > [!NOTE]  
    >  雖然資料在執行中參數類似於資料在執行中資料行，所傳回的值**SQLParamData**每個不同。  
  
    > [!NOTE]  
    >  資料在執行中參數已將與傳送資料的 SQL 陳述式中的參數**SQLPutData**當陳述式以**SQLExecDirect**或**SQLExecute**. 使用繫結**SQLBindParameter**或藉由設定具有描述元**SQLSetDescRec**。 所傳回的值**SQLParamData**是 32 位元值傳遞給**SQLBindParameter**中*ParameterValuePtr*引數。  
  
    > [!NOTE]  
    >  資料在執行中資料行是資料會傳送使用資料列集中的資料行**SQLPutData**與更新資料列時**SQLSetPos**。 使用繫結**SQLBindCol**。 所傳回的值**SQLParamData**是中的資料列的地址 **TargetValuePtr*正在處理的緩衝區。  
  
4.  呼叫**SQLPutData**一或多次來傳送資料行的資料。 如果無法以傳回所有資料值，則需要一個以上的通話 *\*TargetValuePtr*中指定的緩衝區**SQLPutData**; 多次呼叫**SQLPutData**或傳送二進位的 C 資料行的字元、 二進位，傳送字元 C 資料行的字元、 二進位檔或資料來源特有的資料型別時，只允許相同的資料行或資料來源特定的資料類型。  
  
5.  呼叫**SQLParamData**再次來表示，所有資料都傳送的資料行。  
  
    -   如果有更多的資料在執行資料行**SQLParamData**會傳回 SQL_NEED_DATA 和位址*TargetValuePtr*緩衝區的下一個處理的資料在執行資料行。 應用程式會重複步驟 4 和 5。  
  
    -   如果沒有其他資料在執行中資料行，此程序已完成。 如果陳述式執行成功， **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果執行失敗，則會傳回 SQL_ERROR。 在此時**SQLParamData**可能會傳回任何可傳回的 SQLSTATE **SQLSetPos**。  
  
 如果已更新資料，此驅動程式會變成 SQL_ROW_UPDATED 中實作資料列狀態陣列，針對適當的資料列的值。  
  
 如果在作業取消或發生錯誤時**SQLParamData**或**SQLPutData**後**SQLSetPos**會傳回 SQL_NEED_DATA，資料會傳送所有之前資料在執行中資料行，應用程式可以只呼叫**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**陳述式或陳述式相關聯的連接。 如果陳述式或陳述式相關聯的連接，它就會呼叫其他函式，則函數會傳回 SQL_ERROR，而且 SQLSTATE HY010 （函數順序錯誤）。  
  
 如果應用程式會呼叫**SQLCancel**驅動程式時驅動程式仍需要資料的資料在執行中資料行時，取消作業。 應用程式接著可以呼叫**SQLSetPos**再次; 取消不會影響資料指標狀態或目前的游標位置。  
  
 當資料指標相關聯的查詢規格之 SELECT 清單包含多個參考相同的資料行，是否會產生錯誤，或驅動程式會忽略重複的參考，並且會執行要求的作業是由驅動程式定義。  
  
## <a name="performing-bulk-operations"></a>執行大量作業  
 如果*RowNumber*引數為 0 時，驅動程式會執行指定的作業*作業*在資料列作業中的欄位具有數值 SQL_ROW_PROCEED 的資料列集中的每個資料列的引數SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性所指向陣列。 這是有效的值*RowNumber*引數*作業*SQL_DELETE、 SQL_REFRESH，或是 SQL_UPDATE，但不是 SQL_POSITION 引數。 **SQLSetPos**具有*操作*SQL_POSITION 的並*RowNumber*等於 0 會傳回 SQLSTATE HY109 （無效的資料指標位置）。  
  
 如果發生的錯誤屬於整個資料列集，例如 SQLSTATE HYT00 （逾時過期），驅動程式會傳回 SQL_ERROR，而且適當的 SQLSTATE。 資料列集緩衝區的內容為未定義，並不會變更游標位置。  
  
 如果發生錯誤，與單一的資料列中，驅動程式：  
  
-   設定 SQL_ROW_ERROR sql_attr_row_status_ptr 設定陳述式屬性所指的資料列狀態陣列中的資料列的項目。  
  
-   錯誤佇列中張貼一或多個錯誤的其他 Sqlstate 並設定 SQL_DIAG_ROW_NUMBER 欄位中的診斷資料結構。  
  
 已經處理的錯誤或警告，如果驅動程式完成剩餘的資料列中資料列集的作業之後，它會傳回 SQL_SUCCESS_WITH_INFO。 因此，每個資料列，傳回錯誤，錯誤佇列包含零個或多個其他的 Sqlstate。 如果它已處理的錯誤或警告之後，驅動程式會停止作業，它會傳回 SQL_ERROR。  
  
 如果驅動程式會傳回任何警告，例如 SQLSTATE 01004 （資料已截斷），它會傳回套用至整個資料列集或未知的資料列中資料列集，它會傳回適用於特定的資料列的錯誤資訊之前的警告。 它會傳回任何其他錯誤相關資訊的資料列的特定資料列的警告。  
  
 如果*RowNumber*等於 0 並*作業*SQL_UPDATE、 SQL_REFRESH，或 SQL_DELETE，，資料列數目**SQLSetPos**運作上指向 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性。  
  
 如果*RowNumber*等於 0 並*作業*SQL_DELETE、 SQL_REFRESH，或 SQL_UPDATE，目前的資料列作業之後目前的資料列，在作業之前相同。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>略過大量作業中的資料列  
 資料列作業陣列可以用來表示應該忽略在大量作業使用的目前資料列集中的資料列**SQLSetPos**。 若要直接在大量作業期間忽略一或多個資料列的驅動程式，應用程式應該執行下列步驟：  
  
1.  呼叫**SQLSetStmtAttr**設為指向陣列 SQLUSMALLINTs SQL_ATTR_ROW_OPERATION_PTR 陳述式屬性。 這個欄位也可以藉由呼叫設定**SQLSetDescField**設 ARD，這需要應用程式取得描述項控制代碼的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位。  
  
2.  將資料列作業陣列的每個項目設定為兩個值之一：  
  
    -   SQL_ROW_IGNORE，以表示資料列會排除大量作業。  
  
    -   SQL_ROW_PROCEED，以指出在大量作業中包含的資料列。 (這是預設值)。  
  
3.  呼叫**SQLSetPos**執行大量作業。  
  
 下列規則適用於資料列作業陣列：  
  
-   SQL_ROW_IGNORE 和 SQL_ROW_PROCEED 影響只會大量使用的作業**SQLSetPos**具有*作業*SQL_DELETE 或 SQL_UPDATE。 它們不會影響呼叫**SQLSetPos**具有*作業*SQL_REFRESH 或 SQL_POSITION。  
  
-   指標會設定預設為 null。  
  
-   如果指標為 null，如同所有的項目已設為 SQL_ROW_PROCEED，會更新所有資料列。  
  
-   將項目設定為 SQL_ROW_PROCEED 不保證此作業會在該特定的資料列上進行。 例如，如果資料列集中的某個資料列的狀態 SQL_ROW_ERROR，驅動程式可能無法更新該資料列，不論應用程式是否指定 SQL_ROW_PROCEED。 應用程式必須一律會檢查資料列狀態陣列，若要查看作業是否成功。  
  
-   SQL_ROW_PROCEED 定義為標頭檔中的 0。 應用程式可以初始化為 0 的資料列作業陣列，以便處理所有資料列。  
  
-   如果資料列作業陣列中的元素數目"n"設定為 SQL_ROW_IGNORE 並**SQLSetPos**呼叫來執行大量更新或刪除作業，在資料列集仍在呼叫之後未變更的第 n 個資料列**SQLSetPos**.  
  
-   應用程式應該自動設定 SQL_ROW_IGNORE 唯讀的資料行。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>略過大量作業中的資料行  
 若要避免不必要的處理嘗試一或多個唯讀資料行的更新所產生的診斷，應用程式可以設定 SQL_COLUMN_IGNORE 繫結的長度/指標緩衝區中的值。 如需詳細資訊，請參閱 < [SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式可讓使用者瀏覽 「 訂單 」 資料表，並更新訂單狀態。 資料指標為索引鍵集導向資料列集大小為 20，並使用開放式並行存取控制比較資料列版本。 擷取每個資料列集之後，應用程式會將它列印，可讓使用者選取和更新的訂單狀態。 應用程式會使用**SQLSetPos**若要將游標放在選取的資料列，並執行定位的更新的資料列。 （為了清楚起見會忽略錯誤處理）。  
  
```cpp  
#define ROWS 20  
#define STATUS_LEN 6  
  
SQLCHAR        szStatus[ROWS][STATUS_LEN], szReply[3];  
SQLINTEGER     cbStatus[ROWS], cbOrderID;  
SQLUSMALLINT   rgfRowStatus[ROWS];  
SQLUINTEGER    sOrderID, crow = ROWS, irow;  
SQLHSTMT       hstmtS, hstmtU;  
  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CONCURRENCY, (SQLPOINTER) SQL_CONCUR_ROWVER, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_CURSOR_TYPE, (SQLPOINTER) SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
SQLSetStmtAttr(hstmtS, SQL_ATTR_ROW_STATUS_PTR, (SQLPOINTER) rgfRowStatus, 0);  
SQLSetCursorName(hstmtS, "C1", SQL_NTS);  
SQLExecDirect(hstmtS, "SELECT ORDERID, STATUS FROM ORDERS ", SQL_NTS);  
  
SQLBindCol(hstmtS, 1, SQL_C_ULONG, &sOrderID, 0, &cbOrderID);  
SQLBindCol(hstmtS, 2, SQL_C_CHAR, szStatus, STATUS_LEN, &cbStatus);  
  
while ((retcode == SQLFetchScroll(hstmtS, SQL_FETCH_NEXT, 0)) != SQL_ERROR) {  
   if (retcode == SQL_NO_DATA_FOUND)  
      break;  
   for (irow = 0; irow < crow; irow++) {  
      if (rgfRowStatus[irow] != SQL_ROW_DELETED)  
         printf("%2d %5d %*s\n", irow+1, sOrderID, NAME_LEN-1, szStatus[irow]);  
   }  
   while (TRUE) {  
      printf("\nRow number to update?");  
      gets_s(szReply, 3);  
      irow = atoi(szReply);  
      if (irow > 0 && irow <= crow) {  
         printf("\nNew status?");  
         gets_s(szStatus[irow-1], (ROWS * STATUS_LEN));  
         SQLSetPos(hstmtS, irow, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
         SQLPrepare(hstmtU,  
          "UPDATE ORDERS SET STATUS=? WHERE CURRENT OF C1", SQL_NTS);  
         SQLBindParameter(hstmtU, 1, SQL_PARAM_INPUT,  
            SQL_C_CHAR, SQL_CHAR,  
            STATUS_LEN, 0, szStatus[irow], 0, NULL);  
         SQLExecute(hstmtU);  
      } else if (irow == 0) {  
         break;  
      }  
   }  
}  
```  
  
 如需其他範例，請參閱 <<c0> [ 定位更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)並[的資料列集使用 SQLSetPos 更新資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行區塊資料指標位置無關的大量作業|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述元的單一欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述元的多個欄位|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定的單一欄位的描述元|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定多個欄位的描述元|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|設定陳述式屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
