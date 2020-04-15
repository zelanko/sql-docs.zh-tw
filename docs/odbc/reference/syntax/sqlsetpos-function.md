---
title: SQLSetPos 函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetPos
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetPos
helpviewer_keywords:
- SQLSetPos function [ODBC]
ms.assetid: 80190ee7-ae3b-45e5-92a9-693eb558f322
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a8839f1ae540ac9e5f29e144f7f57fb754e50ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287328"
---
# <a name="sqlsetpos-function"></a>SQLSetPos 函式
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLSetPos**設置行集中的游標位置,並允許應用程式刷新行集中的數據或更新或刪除結果集中的數據。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSetPos(  
      SQLHSTMT        StatementHandle,  
      SQLSETPOSIROW   RowNumber,  
      SQLUSMALLINT    Operation,  
      SQLUSMALLINT    LockType);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *行號*  
 [輸入]行在行集中的位置,用於執行使用 *「操作」* 參數指定的操作。 如果*RowNumber*為 0,則該操作將應用於行集中的每一行。  
  
 有關詳細資訊,請參閱"註釋"。  
  
 *操作*  
 [輸入]操作執行:  
  
 SQL_POSITIONSQL_REFRESHSQL_UPDATESQL_DELETE  
  
> [!NOTE]
>  *操作*參數的SQL_ADD值已被棄用為 ODBC *3.x*。 ODBC *3.x*驅動程式需要支援SQL_ADD,以便向後相容。 此功能已取代為對**SQLBulk 操作**的呼叫,並帶有SQL_ADD*操作*。 當 ODBC *3.x*應用程式與 ODBC *2.x*驅動程式配合使用時,驅動程式管理器*Operation*將調用映射到**SQLBulk 操作**,操作操作為*Operation***SQL_ADD,** 操作操作為 SQL_ADD。  
  
 有關詳細資訊,請參閱"註釋"。  
  
 *LockType*  
 [輸入]指定在執行*操作*參數中指定的操作後如何鎖定行。  
  
 SQL_LOCK_NO_CHANGESQL_LOCK_EXCLUSIVESQL_LOCK_UNLOCK  
  
 有關詳細資訊,請參閱"註釋"。  
  
 **返回**  
  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NEED_DATA、SQL_STILL_EXECUTING、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSetPos**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLSetPos**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
 對於可以返回SQL_SUCCESS_WITH_INFO或SQL_ERROR的所有 SQLSTAT(01xxx SQLSTATEs 除外),如果多行操作的一個或多個行發生錯誤(但不是全部)發生錯誤,則返回SQL_SUCCESS_WITH_INFO,如果單行操作發生錯誤,則返回SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01001|游標操作衝突|*操作*參數SQL_DELETE或SQL_UPDATE,並且沒有刪除或更新任何行或多行。 (有關對多行的更新的詳細資訊,請參閱**SQLSetStmtAttr**中的SQL_ATTR_SIMULATE_CURSOR*屬性*的說明。(函數返回SQL_SUCCESS_WITH_INFO。<br /><br /> *操作*參數SQL_DELETE或SQL_UPDATE,並且操作由於樂觀併發而失敗。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料右截斷|*SQL_REFRESH操作*參數,為資料類型為SQL_C_CHAR或SQL_C_BINARY的列返回字串或二進位資料,從而導致非空白字元或非 NULL 二進位資料的截斷。|  
|01S01|行中的錯誤|*RowNumber*參數為 0,在執行使用 *「操作」* 參數指定的操作時,一個或多個行中發生錯誤。<br /><br /> (如果多行操作的一個或多個行發生錯誤(但不是全部),則返回SQL_SUCCESS_WITH_INFO,如果單行操作發生錯誤,則返回SQL_ERROR。<br /><br /> (僅當**SQLATPos**在**SQLExtendedFetch**之後呼叫 SQLSetPos 時,如果驅動程式是 ODBC *2.x*驅動程式且未使用遊標庫,則僅返回此 SQLSTATE。|  
|01S07|分數截斷|*SQL_REFRESH操作*參數,應用程式緩衝區的數據類型未SQL_C_CHAR或SQL_C_BINARY,返回到一個或多個列的應用程序緩衝區的數據被截斷。 對於數位數據類型,數位的小數部分被截斷。 對於包含時間元件的時間、時間戳和間隔數據類型,時間的小數部分被截斷。<br /><br /> (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|無法將結果集中欄資料值轉換為*TargetType*在調用**SQLBindCol**時指定的數據類型。|  
|07009|不合法的描述符索引|參數*操作*SQL_REFRESH或SQL_UPDATE,並且對列綁定的列數大於結果集中的列數。|  
|21S02|衍生表的程度與列清單不符合|參數*操作*是SQL_UPDATE的,沒有列是可升的,因為所有列要麼是未綁定的、唯讀的,要麼是綁定長度/指示器緩衝區中的值SQL_COLUMN_IGNORE。|  
|22001|字串資料,右截斷|*操作*參數SQL_UPDATE,將字元或二進位值分配給列會導致非空白(字元)或非空字元(二進位元)或位元組的截斷。|  
|22003|數值超範圍|參數*操作*SQL_UPDATE,並將數值分配給結果集中的列會導致數位的整個部分(而不是小數)被截斷。<br /><br /> 參數*操作*SQL_REFRESH,返回一個或多個綁定列的數值將導致重要數位的損失。|  
|22007|不合法日期時間格式|參數*操作*SQL_UPDATE,並將日期或時間戳值分配給結果集中的列會導致年份、月份或日欄位超過範圍。<br /><br /> 參數*操作*SQL_REFRESH,返回一個或多個綁定列的日期或時間戳值將導致年份、月份或日欄位超出範圍。|  
|22008|日期/時間欄位溢出|*操作*參數SQL_UPDATE,並且對發送到結果集中的列的數據執行日期時間算術,導致結果超出欄位允許的值範圍,或根據公曆的約會時間自然規則無效。<br /><br /> *操作*參數SQL_REFRESH,並且對從結果集中檢索的數據執行日期時間算術,導致結果超出欄位允許的值範圍,或根據公曆的約會時間自然規則無效。|  
|22015|間隔欄位溢出|*操作*參數SQL_UPDATE,將精確數位或間隔 C 類型分配給間隔 SQL 數據類型會導致重要數位丟失。<br /><br /> *行動*論點SQL_UPDATE;當分配給間隔 SQL 類型時,間隔 SQL 類型中沒有 C 類型的值表示形式。<br /><br /> *操作*參數SQL_REFRESH,並將從精確數位或間隔 SQL 類型分配給間隔 C 類型會導致前導欄位中的重要數位遺失。<br /><br /> *操作*參數SQL_ REFRESH;當分配給間隔 C 類型時,間隔 C 類型中沒有 SQL 類型的值表示形式。|  
|22018|強制轉換規範的不合法字元值|*行動*論點SQL_REFRESH;C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列中的值不是綁定 C 型態的有效文字。<br /><br /> 參數*操作*是SQL_UPDATE;SQL 類型是精確或近似的數位、日期時間或間隔數據類型;C 類型為SQL_C_CHAR;列中的值不是綁定 SQL 類型的有效文本。|  
|23000|完整性約束衝突|參數*操作*SQL_DELETE或SQL_UPDATE,並且違反了完整性約束。|  
|24000|指標狀態無效|*語句句柄*處於已執行狀態,但沒有與*語句句柄*關聯的結果集。<br /><br /> (DM)*語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。<br /><br /> 在*語句句柄*上打開一個游標,並且已調用**SQLFetch**或**SQLFetchScroll,** 但游標位於結果集開始之前或結果集結束之後。<br /><br /> 參數*操作*SQL_DELETE、SQL_REFRESH 或SQL_UPDATE,游標位於結果集開始之前或結果集結束之後。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|42000|語法錯誤或存取衝突|驅動程式無法根據需要鎖定該行,以執行參數*操作*中請求的操作。<br /><br /> 驅動程式無法按參數*LockType*中的請求鎖定該行。|  
|44000|WITH CHECK OPTION 違規|*操作*參數SQL_UPDATE,更新是在查看的表或從已查看表派生的表上執行的,該表是通過指定 **"使用 CHECK 選項**"創建的,以便受更新影響的一個或多個行不再存在於查看的表中。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**在*語句句柄*上調用 ,然後在*語句句柄*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用 SQLSetPos 函數時,此異步函數仍在執行。<br /><br /> (DM) 指定的*語句句柄*未處於執行狀態。 調用該函數時沒有首先調用**SQLExecDirect、SQLExecute**或目錄函**SQLExecute**數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。<br /><br /> (DM) 驅動程式是 ODBC *2.x*驅動程式,在呼叫**SQLFetch**後呼叫**SQLSetPos***進行敘述處理*。|  
|HY011|無法立即設定屬性|(DM) 驅動程式是 ODBC *2.x*驅動程式;已設置SQL_ATTR_ROW_STATUS_PTR語句屬性;然後**SQLSetPos**在調用**SQLFetch、SQLFetchScroll**或 SQL**SQLFetchScroll****擴展獲取**之前調用。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|*SQL_UPDATE操作*參數,資料值為空指標,列長度值不是 0、SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NULL_DATA或小於或等於SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> *行動*論點SQL_UPDATE;數據值不是空指標;數據值不是空指標。C 數據類型為SQL_C_BINARY或SQL_C_CHAR;並且列長度值小於 0 但不等於SQL_DATA_AT_EXEC、SQL_COLUMN_IGNORE、SQL_NTS或SQL_NULL_DATA,或小於或等於SQL_LEN_DATA_AT_EXEC_OFFSET。<br /><br /> 長度/指示器緩衝區中的值SQL_DATA_AT_EXEC;SQL 類型要麼是SQL_LONGVARCHAR、SQL_LONGVARBINARY,要麼是長數據源特定的數據類型;**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN資訊類型為"Y"。|  
|HY092|不合法屬性識別碼|(DM) 為*操作*參數指定的值無效。<br /><br /> (DM) 為*LockType*參數指定的值無效。<br /><br /> *操作*參數SQL_UPDATE或SQL_DELETE,SQL_ATTR_CONCURRENCY語句屬性SQL_ATTR_CONCUR_READ_ONLY。|  
|HY107|行值範圍外|為參數*RowNumber*指定的值大於行集中的行數。|  
|HY109|游標位置無效|與*語句句柄*關聯的游標定義為僅轉發,因此游標無法定位在行集中。 請參閱**SQLSetStmtAttr**中SQL_ATTR_CURSOR_TYPE屬性的說明。<br /><br /> *操作*參數SQL_UPDATE、SQL_DELETE或SQL_REFRESH,*並且 RowNumber*參數標識的行已被刪除或未提取。<br /><br /> (DM)*行編號*參數為 0,*操作*參數SQL_POSITION。<br /><br /> **SQLSetPos**是在調用**SQLBulk 操作**後以及調用**SQLFetchScroll**或**SQLFetch**之前調用的。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或資料來源不支援*操作*參數或*LockType*參數中請求的操作。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**SQLSetStmtAttr**設置,*屬性*為 SQL_ATTR_QUERY_TIMEOUT。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
  
> [!CAUTION]
>  有關該語句的資訊,指出**SQLSetPos**可以呼叫,以及它需要做什麼才能與 ODBC *2.x*應用程式相容,請參閱[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
## <a name="rownumber-argument"></a>列編號參數  
 *RowNumber*參數指定列集中要執行*操作*參數指定的操作的行數。 如果*RowNumber*為 0,則該操作將應用於行集中的每一行。 *行編號*必須是從 0 到行集中行數的值。  
  
> [!NOTE]  
>  在 C 語言中,陣列基於 0,*行數*參數基於 1。 例如,要更新行集的第五行,應用程式會修改陣列索引4處的行集緩衝區,但指定*行數*為5。  
  
 所有操作都將游標放置在*行編號*指定的行上。 以下操作需要游標位置:  
  
-   定位更新和刪除語句。  
  
-   呼叫**SQLGetData**。  
  
-   使用SQL_DELETE、SQL_REFRESH和SQL_UPDATE選項調用**SQLSetPos。**  
  
 例如,如果對**SQLSetPos**的調用的*RowNumber*為*Operation*2,並且操作為 SQL_DELETE,則游標將定位在行集的第二行上,並刪除該行。 第二行的實現行狀態陣列中的條目(由SQL_ATTR_ROW_STATUS_PTR語句屬性指向)更改為SQL_ROW_DELETED。  
  
 應用程式可以在調用**SQLSetPos**時指定游標位置。 通常,它呼叫**SQLSetPos**與SQL_POSITION或SQL_REFRESH操作,以定位游標之前執行定位的更新或刪除語句或呼叫**SQLGetData**。  
  
## <a name="operation-argument"></a>操作參數  
 *操作*參數支援以下操作。 要確定資料來源支援哪些選項,應用程式使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1資訊類型(取決於游標的類型)調用**SQLGetInfo。**  
  
|*操作*<br /><br /> 引數|作業|  
|------------------------------|---------------|  
|SQL_POSITION|驅動程式將游標定位在*行數指定的行*上。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 敘述屬性指向的行狀態陣列的內容會忽略SQL_POSITION *。*|  
|SQL_REFRESH|驅動程式將游標定位在*RowNumber*指定的行上,並在該行的行集緩衝區中刷新數據。 有關驅動程式如何返回行集緩衝區中的數據的詳細資訊,請參閱**SQLBindCol**中按行和按列綁定的說明。<br /><br /> 具有"SQL_REFRESH*操作*的**SQLSetPos**更新當前提取排集中行的狀態和內容。 這包括刷新書籤。 由於緩衝區中的數據將刷新但不重新提取,因此行集中的成員身份是固定的。 這與調用**SQLFetchScroll**執行的刷新不同,該刷新的*取取方向*為 SQL_FETCH_RELATIVE,*行號*等於 0,後者從結果集中重新提取行集,以便在驅動程式和游標支援這些操作時,可以顯示添加的數據並刪除已刪除的數據。<br /><br /> 使用**SQLSetPos**成功刷新不會更改SQL_ROW_DELETED的行狀態。 行集中已刪除的行將繼續標記為已刪除,直到下一次提取。 如果游標支援打包(其中後續**SQLFetch**或**SQLFetchScroll**不會返回已刪除的行),則行將在下一個提取時消失。<br /><br /> 使用**SQLSetPos**執行刷新時,不會顯示添加的行。 此行為不同於**SQLFetchScroll,** 其*提取類型*為 SQL_FETCH_RELATIVE,*行號*等於 0,後者也會刷新當前行集,但如果游標支援這些操作,則將顯示添加的記錄或打包已刪除的記錄。<br /><br /> 使用**SQLSetPos**成功刷新將SQL_ROW_ADDED的行狀態更改為SQL_ROW_SUCCESS(如果存在行狀態陣列)。<br /><br /> 使用**SQLSetPos**成功刷新會將SQL_ROW_UPDATED行狀態更改為行的新狀態(如果存在行狀態陣列)。<br /><br /> 如果行上的**SQLSetPos**操作中發生錯誤,則行狀態設置為SQL_ROW_ERROR(如果存在行狀態陣列)。<br /><br /> 對於使用SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES的SQL_ATTR_CONCURRENCY語句屬性打開的游標,使用**SQLSetPos**刷新可能會更新數據源用於檢測行已更改的樂觀併發值。 如果發生這種情況,每當從伺服器刷新行集緩衝區時,用於確保游標併發的行版本或值都會更新。 對於刷新的每行,將發生這種情況。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性指向的行狀態陣列的內容會忽略SQL_REFRESH*操作*。|  
|SQL_UPDATE|驅動程式將游標定位在*RowNumber*指定的行上,並使用行集緩衝區中的值 **(SQLBindCol**中的*TargetValuePtr*參數)更新基礎數據行。 它從長度/指標緩衝區 **(SQLBindCol**中的*StrLen_or_IndPtr*參數)檢索數據的長度。 如果任何列的長度SQL_COLUMN_IGNORE,則不更新該列。 更新行后,驅動程式將行狀態陣列的相應元素更改為SQL_ROW_UPDATED或SQL_ROW_SUCCESS_WITH_INFO(如果存在行狀態陣列)。<br /><br /> 如果在包含重複列的游標上調用具有SQL_UPDATE*的"操作"* 參數的**SQLSetPos,** 則該行為是驅動程式定義的。 驅動程式可以返回驅動程式定義的 SQLSTATE,可以更新結果集中顯示的第一列,或執行其他驅動程式定義的行為。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性指向的行操作陣列可用於指示在當前行集中的行應在批量更新期間忽略。 有關詳細資訊,請參閱此函數引用後面的"狀態和操作陣列"。|  
|SQL_DELETE|驅動程式將游標定位在*行數指定的行*上,並刪除基礎數據行。 它將行狀態陣列的相應元素更改為SQL_ROW_DELETED。 刪除行後,以下行無效:定位更新和刪除語句、對**SQLGetData**的調用以及對**SQLSetPos** *的*調用,操作設置為除SQL_POSITION以外的任何內容。 對於支援打包的驅動程式,當從數據源檢索新數據時,該行將從游標中刪除。<br /><br /> 行是否保持可見取決於游標類型。 例如,已刪除的行對靜態和鍵集驅動的游標可見,但動態游標不可見。<br /><br /> SQL_ATTR_ROW_OPERATION_PTR 語句屬性指向的行操作陣列可用於指示在當前行集中的行應在批量刪除期間忽略。 有關詳細資訊,請參閱此函數引用後面的"狀態和操作陣列"。|  
  
## <a name="locktype-argument"></a>鎖類型參數  
 *LockType*參數為應用程式提供了一種控制併發的方法。 在大多數情況下,支援併發級別和事務的數據源將僅支援*LockType*參數的SQL_LOCK_NO_CHANGE值。 *LockType*參數通常僅用於基於文件的支援。  
  
 *LockType*參數指定執行**SQLSetPos**後行的鎖狀態。 如果驅動程式無法鎖定行以執行請求的操作或滿足*LockType*參數,它將返回SQL_ERROR和 SQLSTATE 42000(語法錯誤或存取衝突)。  
  
 儘管*LockType*參數是為單個語句指定的,但鎖對連接上的所有語句都授予相同的許可權。 特別是,連接上的一個語句獲取的鎖可以通過同一連接上的不同語句解鎖。  
  
 透過**SQLSetPos**鎖定的行將保持鎖定狀態,直到應用程式為*LockType*設定為SQL_LOCK_UNLOCK的行調用**SQLSetPos,** 或者直到應用程式使用SQL_CLOSE選項呼叫**SQLFreeHandle**或**SQLFreeStmt。** 對於支援事務的驅動程式,當應用程式呼叫**SQLEndTran**提交或回滾連接上的事務時(如果游標在提交或回滾事務時關閉,如**SQLGetInfo**返回SQL_CURSOR_COMMIT_BEHAVIOR和SQL_CURSOR_ROLLBACK_BEHAVIOR資訊類型所示,通過**SQLSetPos**鎖定的行將解鎖。  
  
 *LockType*參數支援以下類型的鎖。 要確定資料源支援哪些鎖,應用程式使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1資訊類型(取決於游標的類型)調用**SQLGetInfo。**  
  
|*鎖類型*參數|鎖定類型|  
|-------------------------|---------------|  
|SQL_LOCK_NO_CHANGE|驅動程式或資料源可確保該行處於與調用**SQLSetPos**之前相同的鎖定或解鎖狀態。 *LockType*的此值允許不支援顯式行級鎖定的數據源使用當前併發和事務隔離級別所需的任何鎖定。|  
|SQL_LOCK_EXCLUSIVE|驅動程式或數據源專門鎖定行。 不能使用不同連接或不同應用程式中的語句來獲取行上的任何鎖。|  
|SQL_LOCK_UNLOCK|驅動程式或數據源解鎖該行。|  
  
 如果驅動程式支援SQL_LOCK_EXCLUSIVE但不支援SQL_LOCK_UNLOCK,則鎖定的行將保持鎖定狀態,直到發生上一段中描述的函數調用之一。  
  
 如果驅動程式支援SQL_LOCK_EXCLUSIVE但不支援SQL_LOCK_UNLOCK,則鎖定的行將保持鎖定狀態,直到應用程式呼叫**SQLFreeHandle**進行語句或**SQLFreeStmt** SQL_CLOSE 選項。 如果驅動程式支援事務並在提交或回捲此事務時關閉游標,則應用程式將呼叫**SQLEndTran**。  
  
 對於**SQLSetPos**中的更新和刪除操作,應用程式使用*LockType*參數,如下所示:  
  
-   為了保證行在檢索後不會更改,應用程式呼叫**SQLSetPos,***操作*設定為*SQL_REFRESH,LockType*設置為SQL_LOCK_EXCLUSIVE。  
  
-   如果應用程式將*LockType*設定為SQL_LOCK_NO_CHANGE,則驅動程式保證僅當為SQL_ATTR_CONCURRENCY語句屬性指定的應用程式SQL_CONCUR_LOCK時,更新或刪除操作才會成功。  
  
-   如果應用程式為SQL_ATTR_CONCURRENCY語句屬性指定SQL_CONCUR_ROWVER或SQL_CONCUR_VALUES,則驅動程式將比較行版本或值,如果行自應用程式獲取行以來已更改,則拒絕該操作。  
  
-   如果應用程式為SQL_ATTR_CONCURRENCY語句屬性指定SQL_CONCUR_READ_ONLY,則驅動程式將拒絕任何更新或刪除操作。  
  
 有關SQL_ATTR_CONCURRENCY語句屬性的詳細資訊,請參閱[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)。  
  
## <a name="status-and-operation-arrays"></a>狀態與操作陣列  
 呼叫**SQLSetPos**時使用以下狀態和操作陣列:  
  
-   行狀態陣列(如 IRD 中的SQL_DESC_ARRAY_STATUS_PTR欄位和SQL_ATTR_ROW_STATUS_ARRAY語句屬性)包含行集中每行數據的狀態值。 調用**SQLFetch、SQLFetchScroll、SQLBulk****操作**或**SQLSetPos**後,驅動程式將設定此陣**SQLFetch**列中的狀態值。 此陣列由SQL_ATTR_ROW_STATUS_PTR語句屬性指向。  
  
-   行操作陣列(如ARD中的SQL_DESC_ARRAY_STATUS_PTR欄位和SQL_ATTR_ROW_OPERATION_ARRAY語句屬性)包含行集中每行的值,指示是忽略還是執行批量操作對**SQLSetPos**的調用。 陣列中的每個元素都設置為SQL_ROW_PROCEED(預設值)或SQL_ROW_IGNORE。 此陣列由SQL_ATTR_ROW_OPERATION_PTR語句屬性指向。  
  
 狀態和操作陣列中的元素數必須等於行集中的行數(由SQL_ATTR_ROW_ARRAY_SIZE語句屬性定義)。  
  
 有關行狀態陣列的資訊,請參閱[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)。 有關行操作陣列的資訊,請參閱本節後面的"忽略批量操作中的行"。  
  
## <a name="using-sqlsetpos"></a>使用 SQLSetPos  
 在應用程式呼叫**SQLSetPos**之前,它必須執行以下步驟序列:  
  
1.  如果應用程式將呼叫**SQLSetPos,***操作*設定為SQL_UPDATE,請為每個列呼叫**SQLBindCol(** 或**SQLSetDescRec),** 以指定其資料類型,並綁定列的資料和長度的緩衝區。  
  
2.  如果應用程式將調用**SQLSetPos,***操作*設定為SQL_DELETE或SQL_UPDATE,則調用**SQLColAttribute**以確保要刪除或更新的列是可更新的。  
  
3.  呼叫**SQLExecDirect、SQLExecute**或目錄函數以創建結果**SQLExecute**集。  
  
4.  呼叫**SQLFetch**或**SQLFetchScroll**來檢索資料。  
  
 有關使用**SQLSetPos**的詳細資訊,請參閱[使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
## <a name="deleting-data-using-sqlsetpos"></a>使用 SQLSetPos 刪除資料  
 要使用**SQLSetPos**刪除資料,應用程式呼叫**SQLSetPos,***其中行號*設定為要刪除的行數,*操作*設置為SQL_DELETE。  
  
 刪除資料後,驅動程式將相應行的實現行狀態陣列中的值更改為SQL_ROW_DELETED(或SQL_ROW_ERROR)。  
  
## <a name="updating-data-using-sqlsetpos"></a>使用 SQLSetPos 更新資料  
 應用程式可以在綁定的數據緩衝區中傳遞列的值,也可以通過對**SQLPutData**的一個或多個調用來傳遞列的值。 其資料隨**SQLPutData**傳遞的欄型稱為*執行時的資料**欄*位 。 它們通常用於發送SQL_LONGVARBINARY和SQL_LONGVARCHAR列的數據,並可以與其他列混合。  
  
#### <a name="to-update-data-with-sqlsetpos-an-application"></a>使用 SQLSetPos 更新資料,應用程式:  
  
1.  在資料中放置值,長度/指標緩衝區與**SQLBindCol**繫結 :  
  
    -   對於普通列,應用程式將新列值放在*\*TargetValuePtr*緩衝區中,並將該值的長*\** 度放在 StrLen_or_IndPtr 緩衝區中。 如果不應更新該行,應用程式將SQL_ROW_IGNORE放在該行操作陣列的該行元素中。  
  
    -   對於執行時的數據列,應用程式在*\*TargetValuePtr*緩衝區中放置應用程式定義的值(如列號)。 該值以後可用於標識列。  
  
         應用程式將SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果放在 +*StrLen_or_IndPtr*緩衝區中。 如果列的 SQL 資料類型SQL_LONGVARBINARY、SQL_LONGVARCHAR 或長數據來源特定的資料類型,並且驅動程式返回**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN資訊類型的「Y」,*則長度*是要為參數發送的數據位元;否則,它必須是非負值,並且被忽略。  
  
2.  調用**SQLSetPos,***將操作*參數設定為SQL_UPDATE更新數據行。  
  
    -   如果沒有執行時的數據列,則該過程已完成。  
  
    -   如果存在任何執行時的數據列,則函數將返回SQL_NEED_DATA並繼續執行步驟 3。  
  
3.  調用**SQLParamData**以檢索要處理的第一個執行數據列的目標*\*值 Ptr*緩衝區的位址。 **SQLParamData**返回SQL_NEED_DATA。 應用程式從*\*TargetValuePtr*緩衝區檢索應用程式定義的值。  
  
    > [!NOTE]  
    >  儘管執行時的數據參數與執行時的數據列類似,但**SQLParamData**返回的值因每個列而異。  
  
    > [!NOTE]  
    >  執行時的資料參數是 SQL 語句中的參數,當使用**SQLExecDirect**或**SQLExecute**執行敘述時,將隨**SQLPutData**一起發送數據。 它們與**SQLBind 參數**綁定,或者通過使用**SQLSetDescRec**設置描述符。 **SQLParamData**傳回的值是 32 位元值,在*參數值Ptr*參數中傳遞給**SQLBind 參數**。  
  
    > [!NOTE]  
    >  執行時的資料列是行集中的欄 **,當使用** **SQLSetPos**更新行時,將為此發送資料。 它們與**SQLBindCol**綁定。 **SQLParamData**傳回的值是正在處理的 @*TargetValuePtr*緩衝區中的行的位址。  
  
4.  調用**SQLPutData**一次或多次以發送列的數據。 如果在**SQLPutData**中指定的*\*TargetValuePtr*緩衝區中無法返回所有數據值,則需要多個調用。僅當將字元 C 資料發送到具有字元、二進位或資料來源特定資料類型的列或將二進位C資料發送到具有字元、二進位或資料來源特定資料類型的列時,才允許對同一列的**SQLPutData**進行多次調用。  
  
5.  再次調用**SQLParamData**以發出已為該列發送所有數據的信號。  
  
    -   如果有更多的執行數據列 **,SQLParamData**將返回要處理的下一個執行數據列的SQL_NEED_DATA和目標*ValuePtr*緩衝區的位址。 應用程式重複步驟 4 和 5。  
  
    -   如果沒有更多的數據執行列,該過程將完成。 如果語句成功執行 **,SQLParamData**將返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO;如果執行失敗,它將返回SQL_ERROR。 此時 **,SQLParamData**可以返回**SQLSetPos**可以返回的任何 SQLSTATE。  
  
 如果數據已更新,驅動程式將相應行的實現行狀態陣列中的值更改為SQL_ROW_UPDATED。  
  
 如果操作被取消或在**SQLParamData**或**SQLPutData**中發生錯誤,則**在 SQLSetPos**返回SQL_NEED_DATA並在為執行時的所有數據發送數據之前,應用程式只能調用 SQLCancel、SQLGetDiagField、SQLGetDiagrec、SQLGet**函數****、SQLParamData**或**SQLPutData**的語句或與語句關聯的連接。 **SQLCancel** **SQLGetDiagField** **SQLGetDiagRec** 如果它調用語句或與 語句關聯的連接的任何其他函數,則函數將返回SQL_ERROR和 SQLSTATE HY010(函數序列錯誤)。  
  
 如果應用程式調用**SQLCancel,** 而驅動程式仍然需要執行時的數據列,則驅動程式將取消該操作。 然後,應用程式可以再次調用**SQLSetPos;** 取消不會影響游標狀態或當前游標位置。  
  
 當與游標關聯的查詢規範的 SELECT 清單包含對同一列的多個引用時,無論生成錯誤還是驅動程式忽略重複的引用並執行請求的操作都是驅動程式定義的。  
  
## <a name="performing-bulk-operations"></a>執行大量操作  
 如果*RowNumber*參數為 0,則驅動程式將執行行集中的每一行的 *「操作*」參數中指定的操作,這些行在行操作陣列中的值為 SQL_ROW_PROCEED,該行位於SQL_ATTR_ROW_OPERATION_PTR語句屬性指向的行操作陣列中。 這是 *「**操作*」參數(SQL_DELETE、SQL_REFRESH 或SQL_UPDATE)的有效值,但不是SQL_POSITION。 操作SQL_POSITION和*行號*等於 0*的***SQLSetPos**將傳回 SQLSTATE HY109(無效游標位置)。  
  
 如果發生與整個行集相關的錯誤(如 SQLSTATE HYT00(超時已過期),驅動程式將返回SQL_ERROR和相應的 SQLSTATE。 行集緩衝區的內容未定義,游標位置保持不變。  
  
 如果發生與單列相關的錯誤,驅動程式:  
  
-   將行狀態陣列中SQL_ATTR_ROW_STATUS_PTR語句屬性指向SQL_ROW_ERROR中行的元素。  
  
-   為錯誤佇列中的錯誤過帳一個或多個附加 SQLSTATE,並在診斷數據結構中設置SQL_DIAG_ROW_NUMBER欄位。  
  
 處理錯誤或警告后,如果驅動程式完成行集中其餘行的操作,它將返回SQL_SUCCESS_WITH_INFO。 因此,對於返回錯誤的每行,錯誤佇列包含零個或多個其他 SQLSTATE。 如果驅動程式在處理了錯誤或警告后停止操作,則返回SQL_ERROR。  
  
 如果驅動程式返回任何警告,如 SQLSTATE 01004(數據截斷),它將返回應用於整個行集或行集中的未知行的警告,然後再返回適用於特定行的錯誤資訊。 它返回特定行的警告以及有關這些行的任何其他錯誤資訊。  
  
 如果*RowNumber*等於 0,*並且操作*SQL_UPDATE、SQL_REFRESH或SQL_DELETE,**則 SQLSetPos**操作的行數由SQL_ATTR_ROWS_FETCHED_PTR語句屬性指出。  
  
 如果*RowNumber*等於 0,*並且操作*SQL_DELETE、SQL_REFRESH 或SQL_UPDATE,則操作後的當前行與操作前的當前行相同。  
  
## <a name="ignoring-a-row-in-a-bulk-operation"></a>忽略批次操作中的行號  
 行操作陣列可用於指示在當前行集中的行應在使用**SQLSetPos**進行批量操作期間忽略。 要指示驅動程式在大量操作期間忽略一個或多個行,應用程式應執行以下步驟:  
  
1.  調用**SQLSetStmtAttr**將SQL_ATTR_ROW_OPERATION_PTR語句屬性設置為指向 SQLUSMALLINT 陣列。 此欄位也可以通過調用**SQLSetDescField**來設置 ARD 的SQL_DESC_ARRAY_STATUS_PTR標頭欄位,該欄位要求應用程式獲取描述符句柄。  
  
2.  將行操作陣列的每個元素設定為兩個值之一:  
  
    -   SQL_ROW_IGNORE,以指示為批量操作排除該行。  
  
    -   SQL_ROW_PROCEED,以指示該行包含在批量操作中。 (這是預設值)。  
  
3.  調用**SQLSetPos**以執行批量操作。  
  
 以下規則適用於列操作陣列:  
  
-   SQL_ROW_IGNORE和SQL_ROW_PROCEED僅影響使用**SQLSetPos**執行SQL_DELETE或SQL_UPDATE*的批次操作*。 它們不會影響對**SQLSetPos***的調用*,操作SQL_REFRESH或SQL_POSITION。  
  
-   預設情況下,指標設定為 null。  
  
-   如果指標為空,則所有行都將更新,就像所有元素都設置為SQL_ROW_PROCEED一樣。  
  
-   將元素設置為SQL_ROW_PROCEED並不保證該操作將發生在該特定行上。 例如,如果行集中的某個行具有SQL_ROW_ERROR狀態,則無論應用程式是否指定SQL_ROW_PROCEED,驅動程式可能無法更新該行。 應用程式必須始終檢查行狀態陣列以查看操作是否成功。  
  
-   SQL_ROW_PROCEED在標頭檔中定義為 0。 應用程式可以將行操作陣組初始化為 0,以便處理所有行。  
  
-   如果行操作陣列中的元素編號「n」設定為SQL_ROW_IGNORE,並且調用**SQLSetPos**執行批量更新或刪除操作,則行集中的第 n 行在調用**SQLSetPos**後保持不變。  
  
-   應用程式應自動將唯讀列設置為SQL_ROW_IGNORE。  
  
## <a name="ignoring-a-column-in-a-bulk-operation"></a>忽略大量操作中的欄位  
 為了避免嘗試更新一個或多個唯讀列而生成不必要的處理診斷,應用程式可以將綁定長度/指示器緩衝區中的值設置為SQL_COLUMN_IGNORE。 有關詳細資訊,請參閱[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)。  
  
## <a name="code-example"></a>程式碼範例  
 在下面的示例中,應用程式允許用戶瀏覽 ORDERS 表並更新訂單狀態。 游標由鍵集驅動,行集大小為 20,並使用比較行版本的樂觀併發控件。 提取每個行集后,應用程式將列印它,並允許用戶選擇和更新訂單的狀態。 應用程式使用**SQLSetPos**將游標定位到所選行上,並執行行的位置更新。 (為了清楚起見,省略了錯誤處理。  
  
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
  
 有關更多範例,請參閱[使用 SQLSetPos 在行集中](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)[定位更新和刪除語句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)以及更新行。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行與區塊游標位置無關的批次操作|[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得描述符的單欄位|[SQLGetDescField 函式](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|取得描述符的多個字段|[SQLGetDescRec 函式](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|設定描述符的單欄位|[SQLSetDescField 函式](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|設定描述符的多個字欄位|[SQLSetDescRec 函式](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
|設定敘述屬性|[SQLSetStmtAttr 函式](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
