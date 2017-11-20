---
title: "SQLGetData 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
caps.latest.revision: 46
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 463a6b68149786cd9cc14ca913e3a2b2104a59e9
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdata-function"></a>SQLGetData 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetData**擷取資料，結果集中的單一資料行或之後的單一參數**SQLParamData**傳回 SQL_PARAM_DATA_AVAILABLE。 它可以多次呼叫來擷取組件中的可變長度資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Col_or_Param_Num*  
 [輸入]擷取資料行資料，它是要傳回資料的資料行數目。 結果集資料行是從 1 開始的遞增資料行順序編號。 書籤資料行是資料行編號 0;這可以指定是否已啟用書籤。  
  
 擷取參數資料，則是從 1 開始之參數的序數。  
  
 *TargetType*  
 [輸入]C 資料類型的類型識別碼 **TargetValuePtr*緩衝區。 如需有效的 C 資料類型和類型識別碼的清單，請參閱[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d： 資料類型 > 一節。  
  
 如果*TargetType*是 SQL_ARD_TYPE，驅動程式中使用 ARD SQL_DESC_CONCISE_TYPE 欄位中指定的類型識別項。 如果*TargetType*是 SQL_APD_TYPE， **SQLGetData**會使用相同的 C 資料類型中所指定的**SQLBindParameter**。 否則，將 C 資料類型指定在**SQLGetData**中指定的 C 資料類型會覆寫**SQLBindParameter**。 如果是 SQL_C_DEFAULT，驅動程式會選取 SQL 資料類型的來源為基礎的預設 C 資料類型。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [輸出]要傳回的資料緩衝區的指標。  
  
 *TargetValuePtr*不能是 NULL。  
  
 *Columnsize*  
 [輸入]長度 **TargetValuePtr*以位元組為單位的緩衝區。  
  
 驅動程式會使用*Columnsize*來避免結尾寫入\* *TargetValuePtr*傳回可變長度的資料，例如字元或二進位資料時，緩衝。 請注意，此驅動程式都 null 結束字元，傳回字元資料時\* *TargetValuePtr*。 **TargetValuePtr*因此必須包含空間 null 結束的字元，或驅動程式將會截斷資料。  
  
 驅動程式會傳回固定長度的資料，例如整數或日期結構，此驅動程式會忽略*Columnsize* ，並假設緩衝區已足夠容納資料。 因此是很重要的應用程式為固定長度的資料配置夠大的緩衝區，或驅動程式將寫入緩衝區的結尾。  
  
 **SQLGetData**傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時*Columnsize*為小於 0，但不是會在*Columnsize*為 0。  
  
 *StrLen_or_IndPtr*  
 [輸出]這是要傳回的長度或指標值的緩衝區指標。 如果這是 null 指標，則會傳回沒有長度或指標值。 擷取的資料為 NULL 時，這會傳回錯誤。  
  
 **SQLGetData**可以長度/指標緩衝區中傳回下列值：  
  
-   可用來傳回資料的長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 如需詳細資訊，請參閱[使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)和本主題中的 [意見]。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetData**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可以藉由呼叫取得相關聯的 SQLSTATE 值**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetData** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|並非所有指定的資料行的資料*Col_or_Param_Num*，無法擷取函式的單一呼叫中。 SQL_NO_TOTAL 或之前的目前呼叫指定的資料行中所剩餘的資料長度**SQLGetData**中傳回\* *StrLen_or_IndPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> 如需有關使用多個呼叫**SQLGetData**單一資料行，請參閱 「 註解 」。|  
|01S07|小數位數截斷|傳回一或多個資料行的資料已遭截斷。 數值資料類型已截斷的數字的小數部分。 時間、 時間戳記，和間隔資料型別包含時間元件，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|在結果集中的資料行的資料值無法轉換成 C 資料類型引數指定*TargetType*。|  
|07009|無效的描述元索引|指定的引數的值*Col_or_Param_Num*為 0，並且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF。<br /><br /> 指定的引數的值*Col_or_Param_Num*大於結果集中的資料行數目。<br /><br /> *Col_or_Param_Num*值不等於使用所提供參數的序數。<br /><br /> (DM) 指定的資料行已繫結。 傳回 SQL_GD_BOUND 位元遮罩 SQL_GETDATA_EXTENSIONS 選項中的驅動程式則不適用這項描述**SQLGetInfo**。<br /><br /> (DM) 指定的資料行的數目小於或等於最高的繫結資料行數目。 傳回 SQL_GD_ANY_COLUMN 位元遮罩 SQL_GETDATA_EXTENSIONS 選項中的驅動程式則不適用這項描述**SQLGetInfo**。<br /><br /> 已呼叫 (DM) 應用程式具有**SQLGetData**目前資料列; 目前的呼叫中指定的資料行的數目小於指定先前的呼叫; 中的資料行數目和驅動程式不會傳回 SQL_GD_ANY_ORDER 位元遮罩中 SQL_GETDATA_EXTENSIONS 選項**SQLGetInfo**。<br /><br /> (DM) *TargetType*引數以前是 SQL_ARD_TYPE，而*Col_or_Param_Num* ARD 中的描述項記錄失敗的一致性檢查。<br /><br /> (DM) *TargetType*引數是 SQL_ARD_TYPE，且 ARD SQL_DESC_COUNT 欄位中的值小於*Col_or_Param_Num*引數。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22002|需要指標變數，但是未提供|*StrLen_or_IndPtr*為 null 指標，而且原先擷取資料為 NULL。|  
|22003|數值超出範圍|傳回數字的值 （做為數值或字串），資料行可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 如需詳細資訊，請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|無效的 datetime 格式|在結果集中的字元資料行已繫結至 C 日期、 時間或時間戳記結構，但資料行中的值無效的日期、 時間戳記，分別。 如需詳細資訊，請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|除數為零|傳回導致除以零的算術運算式中的值。|  
|22015|間隔欄位溢位|C 間隔類型指派從精確數值或 SQL 類型的間隔 [前置] 欄位中造成有效位數的遺失。<br /><br /> 將資料傳回至 C 間隔類型，當時發生沒有 C 間隔類型中的 SQL 型別值的表示。|  
|22018|轉換規格的字元值無效|C 字元緩衝區，以傳回結果集內的字元資料行和資料行包含字元集的緩衝區中沒有表示為一個字元。<br /><br /> C 類型為精確或大約的數字、 日期時間或間隔資料類型。資料行的 SQL 類型是字元資料類型。和資料行中的值不是有效的常值的繫結 C 類型。|  
|24000|指標狀態無效|(DM) 函式呼叫，但沒有先呼叫**SQLFetch**或**SQLFetchScroll**以將游標放在所需資料的資料列。<br /><br /> (DM) *StatementHandle*目前處於執行狀態，但任何結果集與*StatementHandle*。<br /><br /> 在開啟游標的*StatementHandle*和**SQLFetch**或**SQLFetchScroll**如同呼叫，但指標置於結果集或之後開始之前結果集的結尾。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY003|超出範圍的程式類型|(DM) 引數*TargetType*不是有效的資料類型、 SQL_C_DEFAULT、 SQL_ARD_TYPE （如果是擷取資料行的資料） 或 SQL_APD_TYPE （如果是擷取參數資料）。<br /><br /> (DM) 引數*Col_or_Param_Num*是 0，而引數*TargetType*未 SQL_C_BOOKMARK 固定長度的書籤或 SQL_C_VARBOOKMARK 可變長度的書籤。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，然後被呼叫函式上一次*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式，然後再函式一次上呼叫*StatementHandle*。|  
|HY009|無效的 null 指標使用|(DM) 引數*TargetValuePtr*為 null 指標。|  
|HY010|函數順序錯誤|(DM) 指定*StatementHandle*不處於執行狀態。 呼叫此函式時未先呼叫**SQLExecDirect**， **SQLExecute**或類別目錄函式。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLGetData**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) *StatementHandle*目前處於執行狀態，但任何結果集與*StatementHandle*。<br /><br /> 呼叫**SQLExeceute**， **SQLExecDirect**，或**SQLMoreResults**傳回 SQL_PARAM_DATA_AVAILABLE，但**SQLGetData**呼叫而不是**SQLParamData**。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*Columnsize*小於 0。<br /><br /> 指定的引數的值*Columnsize*為小於 4 *Col_or_Param_Num*引數設定為 0，且驅動程式為 ODBC 2*.x*驅動程式。|  
|HY109|無效的資料指標位置|指標置於 (由**SQLSetPos**， **SQLFetch**， **SQLFetchScroll**，或**SQLBulkOperations**) 都已刪除的資料列或無法讀取。<br /><br /> 資料指標是順向資料指標，但大於一的資料列集大小。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援使用**SQLGetData**中的多個資料列與**SQLFetchScroll**。 傳回 SQL_GD_BLOCK 位元遮罩 SQL_GETDATA_EXTENSIONS 選項中的驅動程式則不適用這項描述**SQLGetInfo**。<br /><br /> 驅動程式或資料來源不支援的組合所指定的轉換*TargetType*引數，而對應的資料行的 SQL 資料類型。 SQL 資料類型的資料行對應至驅動程式專屬 SQL 資料類型時，才會發生這個錯誤。<br /><br /> 此驅動程式支援 ODBC 2 只*.x*，引數和*TargetType*是下列其中之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 任何間隔 C 資料類型會列在[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d： 資料型別中。<br /><br /> 此驅動程式只支援 3.50 和引數之前的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLGetData**傳回指定之資料行中的資料。 **SQLGetData**已經提取從結果集的一或多個資料列之後，才可以呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**. 如果可變長度的資料太大的單一呼叫中傳回**SQLGetData** （因為應用程式中限制）， **SQLGetData**可以擷取組件中。 很可能在資料列和呼叫某些資料行繫結**SQLGetData**代表其他項目，雖然這受限於一些限制。 如需詳細資訊，請參閱[擷取長資料](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 如需使用**SQLGetData**與資料流的輸出參數，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGetData  
 如果驅動程式不支援擴充功能**SQLGetData**，函式可以傳回以數字的未繫結資料行的資料大於最後一個繫結的資料行。 此外，資料值的資料列內*Col_or_Param_Num*每次呼叫中的引數**SQLGetData**必須大於或等於值*Col_or_Param_Num*中先前的呼叫。也就是必須以遞增的數字的資料行順序擷取資料。 最後，如果沒有任何延伸支援， **SQLGetData**如果資料列集大小大於 1，無法呼叫。  
  
 驅動程式可能會放寬任何這些限制。 若要判斷哪些驅動程式會放寬的限制，應用程式呼叫**SQLGetInfo**與任何下列 SQL_GETDATA_EXTENSIONS 選項：  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以呼叫以傳回輸出參數值。 如需詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN。 如果傳回此選項，則**SQLGetData**可以針對任何未繫結的資料行，包括上次繫結資料行之前呼叫。  
  
-   SQL_GD_ANY_ORDER。 如果傳回此選項，則**SQLGetData**可以針對未繫結的資料行，以任何順序呼叫。  
  
-   SQL_GD_BLOCK。 如果這個選項由**SQLGetInfo** SQL_GETDATA_EXTENSIONS 資訊類型的驅動程式支援的呼叫**SQLGetData**當資料列集大小大於 1，而且應用程式可以呼叫**SQLSetPos** SQL_POSITION 選項，將游標放在正確的資料列，然後再呼叫**SQLGetData。**  
  
-   SQL_GD_BOUND。 如果傳回此選項，則**SQLGetData**可以呼叫繫結資料行，以及未繫結的資料行。  
  
 有兩個例外狀況，這些限制和放寬這些驅動程式的能力。 首先， **SQLGetData**永遠不可叫用順向資料指標資料列集大小大於 1 時。 其次，如果驅動程式支援書籤，它必須一律支援能夠呼叫**SQLGetData**資料行 0，即使不允許應用程式呼叫**SQLGetData**最後一個以外的其他資料行繫結的資料行。 (當應用程式使用 ODBC 2*.x*驅動程式， **SQLGetData**已成功將會傳回呼叫時的書籤*Col_or_Param_Num*等於 0 後呼叫**SQLFetch**，因為**SQLFetch**對應的 ODBC 3*.x*驅動程式管理員**SQLExtendedFetch** 與*Sqlfetchscroll*的 SQL_FETCH_NEXT，和**SQLGetData**與*Col_or_Param_Num*為 0 會對應由 ODBC 3*.x*驅動程式管理員**SQLGetStmtOption**與*fOption*的 SQL_GET_BOOKMARK。)  
  
 **SQLGetData**無法用來擷取藉由呼叫只插入一個資料列的書籤**SQLBulkOperations**帶有 SQL_ADD 選項，因為資料指標沒有定位的資料列。 應用程式可以擷取繫結資料行 0 之前先呼叫這類資料列的書籤**SQLBulkOperations** SQL_ADD，在此情況下使用**SQLBulkOperations**傳回繫結緩衝區中的書籤。 **SQLFetchScroll**然後可以使用 SQL_FETCH_BOOKMARK 重新定位資料指標，該資料列上呼叫。  
  
 如果*TargetType*引數是在的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 欄位中所設定的間隔資料類型，則預設間隔開頭有效位數 (2) 和預設間隔秒數有效位數 (6)，ARD，分別是針對資料使用。 如果*TargetType*引數 SQL_C_NUMERIC 資料型別，則預設有效位數 （驅動程式定義） 和預設小數位數 (0)，在 ARD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定，可用的資料。 如果任何預設有效位數或小數位數不適用，應用程式應該明確設定適當的描述項欄位呼叫**SQLSetDescField**或**SQLSetDescRec**。 它可以設 SQL_C_NUMERIC 和呼叫 SQL_DESC_CONCISE_TYPE 欄位**SQLGetData**與*TargetType* SQL_ARD_TYPE，會導致的描述項欄位中的有效位數和小數位數的值的引數若要使用。  
  
> [!NOTE]  
>  ODBC 2*.x*，應用程式會設定*TargetType* SQL_C_DATE、 SQL_C_TIME，或 SQL_C_TIMESTAMP 表示\* *TargetValuePtr*是日期、 時間，或時間戳記結構。 在 ODBC 3*.x*，應用程式會設定*TargetType* SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，或 SQL_C_TYPE_TIMESTAMP。 驅動程式管理員會建立適當的對應如果需要，根據的應用程式和驅動程式版本。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>擷取組件中的可變長度資料  
 **SQLGetData**可用來從包含組件中的可變長度資料的資料行擷取資料，亦即，當資料行的 SQL 資料類型的識別項是 SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_WCHAR、 SQL_WVARCHAR、 SQL_WLONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY、 或可變長度類型的驅動程式特定識別項。  
  
 若要從組件中的資料行擷取資料，應用程式會呼叫**SQLGetData**中相同的資料行的連續多次。 在每次呼叫， **SQLGetData**傳回資料的下一個部分。 這是由要切割的組件，務必移除 null 結束字元的字元資料的中間部分的應用程式。 如果沒有更多的資料，以傳回足夠的緩衝區配置給結束的字元，或不**SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （資料已截斷）。 當它傳回資料的最後一部分**SQLGetData**都會傳回 SQL_SUCCESS。 因為應用程式會再有無從得知多少應用程式緩衝區中的資料有效，可以上最後一次的有效呼叫以擷取資料行，資料傳回 SQL_NO_TOTAL 都零。 如果**SQLGetData**呼叫之後，傳回 sql_no_data 為止。 如需詳細資訊，請參閱下節中，「 使用 SQLGetData 擷取資料 」。  
  
 可變長度的書籤中的組件可傳回**SQLGetData**。 如同其他資料，呼叫**SQLGetData**傳回組件中的可變長度書籤時將會傳回 SQLSTATE 01004 （字串資料，右邊已截斷） 和 SQL_SUCCESS_WITH_INFO 傳回其他資料。 時，這與大小寫不同的呼叫方式，刪去可變長度的書籤**SQLFetch**或**SQLFetchScroll**，它會傳回 SQL_ERROR 並 SQLSTATE 22001 （字串資料，右邊已截斷）。  
  
 **SQLGetData**無法用來傳回組件中的固定長度的資料。 如果**SQLGetData**會呼叫一次以上的資料列中包含固定長度資料的資料行，傳回 sql_no_data 為止的所有呼叫的第一個之後。  
  
## <a name="retrieving-streamed-output-parameters"></a>擷取的資料流的輸出參數  
 如果驅動程式支援資料流的輸出參數，應用程式可以呼叫**SQLGetData**以小的緩衝區許多次來擷取大型參數值。 如需有關資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>使用 SQLGetData 擷取資料  
 若要傳回指定之資料行，資料**SQLGetData**會執行下列步驟順序：  
  
1.  如果它已傳回所有資料行的資料，請傳回 sql_no_data 為止。  
  
2.  設定\* *StrLen_or_IndPtr*為 SQL_NULL_DATA，如果資料為 NULL。 如果資料 unll 和*StrLen_or_IndPtr*是 null 指標， **SQLGetData**傳回 SQLSTATE 22002 （指標變數所需但未提供）。  
  
     如果資料行的資料不是 NULL， **SQLGetData**繼續進行步驟 3。  
  
3.  如果 SQL_ATTR_MAX_LENGTH 陳述式屬性設定為非零值，如果資料行包含字元或二進位資料，而且如果**SQLGetData**先前尚未呼叫資料行，資料會被截斷成 SQL_ATTR_MAX_LENGTH個位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 陳述式屬性被要減少網路流量。 它通常被藉由截斷的資料，再加以傳回網路上的資料來源中。 驅動程式和資料來源都不需要來支援它。 因此，若要保證資料會截斷成特定的大小，應用程式應該配置該大小的緩衝區和指定的大小以*Columnsize*引數。  
  
4.  將資料轉換成在指定的型別*TargetType*。 資料會指定預設有效位數和小數位數，該資料類型。 如果*TargetType*是 SQL_ARD_TYPE，資料種 ARD SQL_DESC_CONCISE_TYPE 欄位中的使用。 如果*TargetType* SQL_ARD_TYPE、 資料不一致的有效位數和小數位數的 SQL_DESC_DATETIME_INTERVAL_PRECISION SQL_DESC_PRECISION，並輸入 SQL_DESC_CONCISE SQL_DESC_SCALE ARD，根據資料欄位（_t） 欄位。 如果任何預設有效位數或小數位數不適用，應用程式應該明確設定適當的描述項欄位呼叫**SQLSetDescField**或**SQLSetDescRec**。  
  
5.  如果資料已轉換成可變長度資料類型，例如字元或二進位檔， **SQLGetData**會檢查資料的長度是否超過*Columnsize*。 如果字元資料 （包括 null 結束字元） 的長度超過*Columnsize*， **SQLGetData**會截斷資料*Columnsize*長度小於null 結束字元。 它然後 null 終止的資料。 如果二進位資料的長度超過資料緩衝區的長度**SQLGetData**會截斷以*Columnsize*位元組。  
  
     如果提供的資料緩衝區太小，來保存 null 結束的字元， **SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004。  
  
     **SQLGetData**永遠不會截斷資料轉換成固定長度的資料類型，它一律假設的長度 **TargetValuePtr*是資料類型的大小。  
  
6.  在此放置在已轉換 （與可能已截斷） 資料\* *TargetValuePtr*。 請注意， **SQLGetData**無法傳回資料列。  
  
7.  將放在資料的長度\* *StrLen_or_IndPtr*。 如果*StrLen_or_IndPtr*是 null 指標， **SQLGetData**不會傳回長度。  
  
    -   針對字元或二進位資料，這是資料的長度轉換之後，以及之前截斷，因為*Columnsize*。 如果驅動程式無法在轉換之後，判斷資料的長度，因為有時候是使用 long 資料的情況下，它會傳回 SQL_SUCCESS_WITH_INFO，並將長度設定 SQL_NO_TOTAL。 (在上次呼叫**SQLGetData**一律會傳回長度的資料，而不零或 SQL_NO_TOTAL。)如果資料已截斷 SQL_ATTR_MAX_LENGTH 陳述式屬性，這個屬性的值，而不是實際的長度，放在\* *StrLen_or_IndPtr*。 這是因為這個屬性為了讓驅動程式並沒有方式找出的實際長度會截斷前轉換，在伺服器上的資料。 當**SQLGetData**連續多次呼叫同一個資料行，這是在目前的呼叫開始處的可用資料的長度; 也就是說，長度會減少，每個後續的呼叫。  
  
    -   對於所有其他資料類型，這必須是資料的長度轉換之後也就是說，它是已轉換成資料類型的大小。  
  
8.  如果將資料截斷而不會遺失精確度轉換期間 （例如，實數 1.234 時會被截斷轉換成整數 1），或因為*Columnsize*太小 （例如，字串"abcdef"位於在 4 位元組緩衝區中）， **SQLGetData**傳回 SQLSTATE 01004 （資料已截斷） 和 SQL_SUCCESS_WITH_INFO。 如果資料會遭到截斷，而不會遺失精確度 SQL_ATTR_MAX_LENGTH 陳述式屬性，因為**SQLGetData**都會傳回 SQL_SUCCESS，且沒有傳回 SQLSTATE 01004 （資料已截斷）。  
  
 繫結的資料緩衝區的內容 (如果**SQLGetData**繫結的資料行上呼叫)，長度/指標緩衝區是未定義**SQLGetData**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 後續呼叫**SQLGetData**會從要求的最後一個資料行擷取資料; 先前的位移會變成無效。 例如，下列順序執行時：  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 第二個呼叫 SQLGetData(icol=n) 從開頭的 n 個資料行擷取資料。 任何資料，因為先前的呼叫中的位移**SQLGetData**的資料行已不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>描述項和 SQLGetData  
 **SQLGetData**不會直接與任何描述項欄位互動。  
  
 如果*TargetType*是 SQL_ARD_TYPE，資料種 ARD SQL_DESC_CONCISE_TYPE 欄位中的使用。 如果*TargetType* SQL_ARD_TYPE 或 SQL_C_DEFAULT，資料不一致的有效位數和小數位數的 SQL_DESC_DATETIME_INTERVAL_PRECISION SQL_DESC_PRECISION，SQL_DESC_SCALE 欄位中的 ARD，根據資料輸入在 [SQL_DESC_CONCISE_TYPE] 欄位中。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式執行**選取**陳述式來傳回結果集之客戶的名稱、 識別碼和電話號碼依名稱、 識別碼和電話號碼。 針對每個資料列，它會呼叫**SQLFetch**來定位到下一個資料列資料指標。 它會呼叫**SQLGetData**擷取提取的資料; 資料和傳回的位元組數目的緩衝區中指定的呼叫**SQLGetData**。 最後，它會列印每位員工的名稱、 識別碼和電話號碼。  
  
```  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|指派儲存體中的結果集資料行|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行區塊資料指標的位置無關的大量作業|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取單一資料列或資料區塊的順向的方向|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳送參數資料在執行階段|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|定位資料指標，重新整理此資料列集中，或更新或刪除資料列集中的資料|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)

