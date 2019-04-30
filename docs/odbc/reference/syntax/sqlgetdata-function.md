---
title: SQLGetData 函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b42339c74102b86fe08c84b15da3266a1040dfd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258954"
---
# <a name="sqlgetdata-function"></a>SQLGetData 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLGetData**擷取結果集中單一資料行或之後的單一參數資料**SQLParamData**傳回 SQL_PARAM_DATA_AVAILABLE。 它可以呼叫多次來擷取組件中的可變長度資料。  
  
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
 [輸入]用於擷取資料行的資料，是要傳回資料的資料行數目。 從 1 開始的遞增資料行順序會依結果集資料行編號。 書籤資料行是資料行編號 0;這可以是指定是否已啟用書籤。  
  
 正在擷取參數資料，則是從 1 開始的參數的序數。  
  
 *TargetType*  
 [輸入]C 資料類型的類型識別碼 **TargetValuePtr*緩衝區。 如需有效的 C 資料類型和類型識別碼的清單，請參閱 < [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)節附錄 d:資料類型。  
  
 如果*TargetType*是 SQL_ARD_TYPE，型別識別項欄位中指定 SQL_DESC_CONCISE_TYPE ARD 的驅動程式使用。 如果*TargetType*是 SQL_APD_TYPE， **SQLGetData**會使用相同的 C 資料類型中指定**SQLBindParameter**。 C 資料類型中的指定，否則為**SQLGetData**覆寫中指定的 C 資料類型**SQLBindParameter**。 如果是 SQL_C_DEFAULT，驅動程式就會選取來源的 SQL 資料類型為基礎的預設 C 資料類型。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱 < [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [輸出]要傳回的資料緩衝區的指標。  
  
 *TargetValuePtr*不能是 NULL。  
  
 *BufferLength*  
 [輸入]長度 **TargetValuePtr*以位元組為單位的緩衝區。  
  
 驅動程式會使用*Columnsize*若要避免寫入結尾\* *TargetValuePtr*緩衝區傳回可變長度的資料，例如字元或二進位資料時。 請注意，此驅動程式都之 null 結束字元，傳回字元資料時\* *TargetValuePtr*。 **TargetValuePtr*因此必須包含空間 null 終止的字元，或驅動程式將會截斷資料。  
  
 驅動程式會傳回固定長度的資料，例如整數或日期結構，此驅動程式會忽略*Columnsize* ，並假設緩衝區是否夠大，無法保存資料。 因此是很重要的應用程式為固定長度的資料配置夠大的緩衝區，或驅動程式會寫入超過緩衝區結尾。  
  
 **SQLGetData**會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時*Columnsize*是小於 0，但不是會在*Columnsize*為 0。  
  
 *StrLen_or_IndPtr*  
 [輸出]這是要傳回的長度或指標值的緩衝區指標。 如果這是 null 指標，則會傳回沒有長度或指標值。 正在提取的資料為 NULL 時，這會傳回錯誤。  
  
 **SQLGetData**可以傳回長度/指標緩衝區中的下列值：  
  
-   可用來傳回資料的長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 如需詳細資訊，請參閱 <<c0> [ 使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)和本主題中的 [註解]。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_NO_DATA、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetData**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，可取得相關聯的 SQLSTATE 值，請呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLGetData** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|並非所有指定的資料行的資料*Col_or_Param_Num*，無法在函式的單一呼叫中擷取。 SQL_NO_TOTAL 或之前的目前呼叫指定的資料行中剩餘的資料長度**SQLGetData**會傳回\* *StrLen_or_IndPtr*。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。<br /><br /> 如需有關使用多個呼叫**SQLGetData**單一資料行，請參閱 「 註解。 」|  
|01S07|小數位數截斷|傳回一或多個資料行的資料已遭截斷。 數值資料類型已遭截斷數字的小數部分。 時間、 時間戳記，和包含時間元件的 interval 資料類型，已截斷的小數部分的時間。<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|在結果集中的資料行的資料值無法轉換成 C 資料類型引數指定*TargetType*。|  
|07009|描述項索引無效|指定的引數的值*Col_or_Param_Num*為 0，且 SQL_ATTR_USE_BOOKMARKS 陳述式屬性已設定為 SQL_UB_OFF。<br /><br /> 指定的引數的值*Col_or_Param_Num*大於結果集中的資料行數目。<br /><br /> *Col_or_Param_Num*值不是等於所提供的參數的序數。<br /><br /> (DM) 指定的資料行已繫結。 此描述不適用於傳回 SQL_GD_BOUND 位元遮罩 SQL_GETDATA_EXTENSIONS 選項中的驅動程式**SQLGetInfo**。<br /><br /> (DM) 指定的資料行數目是小於或等於最高的繫結資料行數目。 此描述不適用於傳回 SQL_GD_ANY_COLUMN 位元遮罩 SQL_GETDATA_EXTENSIONS 選項中的驅動程式**SQLGetInfo**。<br /><br /> (DM) 應用程式已呼叫**SQLGetData**目前資料列; 目前的呼叫中指定的資料行數目小於上述的呼叫; 中所指定的資料行數目和驅動程式不會傳回 SQL_SQL_GETDATA_EXTENSIONS 選項中的位元遮罩 GD_ANY_ORDER **SQLGetInfo**。<br /><br /> (DM) *TargetType*引數為 SQL_ARD_TYPE，而*Col_or_Param_Num* ARD 中的描述項記錄未通過一致性檢查。<br /><br /> (DM) *TargetType*引數是 SQL_ARD_TYPE，且 ARD SQL_DESC_COUNT 欄位中的值小於*Col_or_Param_Num*引數。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22002|指標變數但未提供|*StrLen_or_IndPtr*是 null 指標，並擷取 NULL 的資料。|  
|22003|數值超出範圍|傳回數字的值 （做為數值或字串），資料行可能已造成要截斷的數字 （相對於小數） 的整數部分。<br /><br /> 如需詳細資訊，請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|無效的日期時間格式|在結果集中的字元資料行已繫結至 C 日期、 時間或時間戳記結構和資料行中的值可為無效的日期、 時間戳記，分別。 如需詳細資訊，請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|除數為零|傳回從導致除數為零的算術運算式的值。|  
|22015|間隔欄位溢位|將指派從精確數值或時間間隔 SQL 型別，給 C 間隔類型造成有效位數的遺失開頭的欄位中。<br /><br /> C 間隔類型以傳回資料，當發生 C 間隔類型中的 SQL 類型的值不表示。|  
|22018|轉換規格的字元值無效|字元 C 的緩衝區，以傳回結果集內的字元資料行和資料行包含緩衝區的字元集中未表示的字元。<br /><br /> C 類型為精確或近似數值、 日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;和資料行中的值不是有效的常值的繫結的 C 類型。|  
|24000|指標狀態無效|(DM) 呼叫的函式但是未先呼叫**SQLFetch**或是**SQLFetchScroll**若要將游標放在所需資料的資料列。<br /><br /> (DM) *StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。<br /><br /> 資料指標是開啟*StatementHandle*並**SQLFetch**或**SQLFetchScroll**呼叫，但指標置於開始或之後的結果集之前結果集的結尾。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY003|超出範圍的程式類型|(DM) 引數*TargetType*不是有效的資料類型、 SQL_C_DEFAULT，SQL_ARD_TYPE （如果是擷取資料行的資料） 或 SQL_APD_TYPE （如果是擷取參數資料）。<br /><br /> (DM) 引數*Col_or_Param_Num*是 0，而引數*TargetType*未 SQL_C_BOOKMARK 固定長度書籤或 SQL_C_VARBOOKMARK 可變長度書籤。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，並接著呼叫函式上再次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式，然後按一下 函式一次上呼叫*StatementHandle*。|  
|HY009|使用無效的 null 指標|(DM) 引數*TargetValuePtr*是 null 指標。|  
|HY010|函數順序錯誤|(DM) 指定*StatementHandle*不處於執行狀態。 已呼叫的函式，但是未先呼叫**SQLExecDirect**， **SQLExecute**或目錄函式。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLGetData**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。<br /><br /> (DM) *StatementHandle*處於執行狀態，但與相關聯的任何結果集已*StatementHandle*。<br /><br /> 呼叫**SQLExeceute**， **SQLExecDirect**，或**SQLMoreResults**傳回 SQL_PARAM_DATA_AVAILABLE，但**SQLGetData**呼叫而不是**SQLParamData**。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*Columnsize*為小於 0。<br /><br /> 指定引數的值*Columnsize*為小於 4 *Col_or_Param_Num*引數設定為 0，且驅動程式的 ODBC 2 *.x*驅動程式。|  
|HY109|無效的資料指標位置|指標置於 (由**SQLSetPos**， **SQLFetch**， **SQLFetchScroll**，或**SQLBulkOperations**) 已刪除的資料列無法擷取或。<br /><br /> 資料指標是順向資料指標，但大於一的資料列集大小。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援使用**SQLGetData**中的多個資料列**SQLFetchScroll**。 此描述不適用於傳回 SQL_GD_BLOCK 位元遮罩 SQL_GETDATA_EXTENSIONS 選項中的驅動程式**SQLGetInfo**。<br /><br /> 驅動程式或資料來源不支援指定的組合來轉換*TargetType*引數和對應的資料行的 SQL 資料類型。 SQL 資料類型資料行的已對應至驅動程式專屬的 SQL 資料型別時，就會適用這項錯誤。<br /><br /> 此驅動程式支援只有 ODBC 2 *.x*，並將引數*TargetType*是下列其中之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 任何間隔 C 資料類型會列在[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d:資料類型。<br /><br /> 此驅動程式只支援之前 3.50 元，並將引數的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 對應的驅動程式*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLGetData**傳回指定之資料行中的資料。 **SQLGetData**只有在已提取從結果集的一或多個資料列之後，才可以呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLExtendedFetch**。 如果可變長度的資料太大的單一呼叫中傳回**SQLGetData** （因為應用程式中限制）， **SQLGetData**可以擷取組件中。 您可在資料列，並呼叫某些資料行繫結**SQLGetData**供其他人，雖然這會受限於一些限制。 如需詳細資訊，請參閱 <<c0> [ 取得長資料](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 如需有關使用資訊**SQLGetData**含有經過資料流處理的輸出參數，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGetData  
 如果驅動程式不支援延伸模組**SQLGetData**，函式可以傳回以數字的未繫結資料行的資料大於最後一個繫結的資料行。 此外，資料值的資料列內*Col_or_Param_Num*每次呼叫中的引數**SQLGetData**必須是大於或等於值*Col_or_Param_Num*先前的呼叫;也就是說，必須以遞增的數字的資料行順序擷取資料。 最後，如果沒有延伸模組都有支援， **SQLGetData**無法呼叫，如果資料列集大小大於 1。  
  
 驅動程式可能會放寬任何限制。 若要判斷驅動程式會放寬的限制，應用程式會呼叫**SQLGetInfo**搭配任何下列 SQL_GETDATA_EXTENSIONS 選項：  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData**可以呼叫以傳回輸出參數值。 如需詳細資訊，請參閱 <<c0> [ 使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN。 如果傳回此選項，則**SQLGetData**可以針對任何未繫結的資料行，包括上次繫結資料行之前呼叫。  
  
-   SQL_GD_ANY_ORDER。 如果傳回此選項，則**SQLGetData**可以針對未繫結的資料行，依任何順序呼叫。  
  
-   SQL_GD_BLOCK。 如果此選項由**SQLGetInfo** SQL_GETDATA_EXTENSIONS 資訊類型的驅動程式支援的呼叫**SQLGetData**時資料列集大小大於 1，且應用程式可以呼叫**SQLSetPos** SQL_POSITION 選項，將游標放在正確的資料列，然後再呼叫**SQLGetData。**  
  
-   SQL_GD_BOUND。 如果傳回此選項，則**SQLGetData**可以呼叫繫結的資料行，以及未繫結的資料行。  
  
 有兩個例外狀況，這些限制，以及放寬這些驅動程式的能力。 首先， **SQLGetData**永遠不可叫用順向資料指標的資料列集大小大於 1 時。 其次，如果驅動程式支援書籤，它必須一律支援，以及呼叫**SQLGetData**資料行 0，即使它不允許應用程式呼叫**SQLGetData**最後一個以外的其他資料行繫結的資料行。 (當應用程式使用 ODBC 2 *.x*驅動程式**SQLGetData**會成功傳回時呼叫的書籤*Col_or_Param_Num*等於 0 之後呼叫**SQLFetch**，因為**SQLFetch**由 ODBC 3 對應 *.x*驅動程式管理員**SQLExtendedFetch** 與*Sqlfetchscroll*的 SQL_FETCH_NEXT，並**SQLGetData**具有*Col_or_Param_Num*為 0 會對應由 ODBC 3 *.x*驅動程式管理員**SQLGetStmtOption**具有*fOption*的 SQL_GET_BOOKMARK。)  
  
 **SQLGetData**無法用來擷取藉由呼叫剛插入的資料列的書籤**SQLBulkOperations**帶有 SQL_ADD 選項，因為資料指標沒有定位的資料列。 應用程式可以繫結資料行 0 之前先呼叫來擷取這類資料列的書籤**SQLBulkOperations** SQL_ADD，在此情況下使用**SQLBulkOperations**傳回繫結緩衝區中的書籤。 **SQLFetchScroll**然後可以使用 SQL_FETCH_BOOKMARK 重新定位資料指標，該資料列上呼叫。  
  
 如果*TargetType*引數是 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 的欄位中所設定的間隔資料類型，則預設間隔開頭有效位數 (2) 和預設的間隔秒數有效位數 (6)，ARD，分別用於資料。 如果*TargetType*引數是 SQL_C_NUMERIC 資料類型，則預設有效位數 （驅動程式定義） 和預設 ARD SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定的小數位數 (0)，、 所用的資料。 應用程式如果任何預設有效位數或小數位數不適用，應該明確設定適當的描述項欄位呼叫**SQLSetDescField**或是**SQLSetDescRec**。 它可以將 SQL_DESC_CONCISE_TYPE 欄位為 SQL_C_NUMERIC 然後呼叫**SQLGetData**具有*TargetType* SQL_ARD_TYPE，這會導致有效位數和小數位數的值，描述項欄位中的引數若要使用。  
  
> [!NOTE]
>  ODBC 2 *.x*，應用程式組*TargetType* SQL_C_DATE、 SQL_C_TIME，或 SQL_C_TIMESTAMP 表示\* *TargetValuePtr*是日期、 時間，或時間戳記結構。 在 ODBC 3 *.x*，應用程式組*TargetType* SQL_C_TYPE_DATE、 SQL_C_TYPE_TIME，或 SQL_C_TYPE_TIMESTAMP。 驅動程式管理員會建立適當的對應必要時，根據的應用程式和驅動程式版本。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>擷取組件中的可變長度資料  
 **SQLGetData**可用來擷取 SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_WCHAR、 SQL_WVARCHAR、 SQL_ SQL 資料類型的資料行的識別碼時，也就是包含組件-中的可變長度資料的資料行中的資料WLONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY、 或可變長度類型的驅動程式專屬識別碼。  
  
 若要從組件中的資料行擷取資料，應用程式會呼叫**SQLGetData**中相同的資料行的連續數次。 每次呼叫中， **SQLGetData**傳回資料的下一個部分。 它是由應用程式重新組合的組件，並小心移除之 null 結束字元的字元資料的中間部分。 如果沒有更多的資料，以傳回，或未終止的字元，則請配置足夠的緩衝區**SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004 （資料已截斷）。 當它傳回的資料，最後的一部分**SQLGetData**都會傳回 SQL_SUCCESS。 SQL_NO_TOTAL 」 和 「 零 」 都不可以在最後一個有效的呼叫來擷取資料行中的資料傳回，因為應用程式接著會有沒有辦法知道多少應用程式緩衝區中的資料有效。 如果**SQLGetData**呼叫之後，它會傳回 sql_no_data 為止。 如需詳細資訊，請參閱下一步 區段中，「 使用 SQLGetData 擷取資料 」。  
  
 中的組件可傳回可變長度的書籤**SQLGetData**。 如同其他資料，呼叫**SQLGetData**傳回組件中的可變長度書籤會傳回 SQLSTATE 01004 （字串資料，右邊已截斷） 和 SQL_SUCCESS_WITH_INFO，要傳回的更多資料時。 可變長度的書籤呼叫會被截斷時，這是不同的案例**SQLFetch**或是**SQLFetchScroll**，它會傳回 SQL_ERROR，而且 SQLSTATE 22001 （字串資料，右邊已截斷）。  
  
 **SQLGetData**無法用來傳回組件中的固定長度的資料。 如果**SQLGetData**會呼叫一次以上的資料列中，包含固定長度的資料之資料行，它傳回 sql_no_data 為止的所有呼叫的第一個之後。  
  
## <a name="retrieving-streamed-output-parameters"></a>擷取資料流的輸出參數  
 如果驅動程式支援資料流的輸出參數，應用程式可以呼叫**SQLGetData**使用小型緩衝區多次來擷取大型參數值。 如需有關資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>使用 SQLGetData 擷取資料  
 若要傳回所指定的資料行的資料**SQLGetData**會執行下列步驟順序：  
  
1.  如果它已傳回所有資料行的資料，請傳回 sql_no_data 為止。  
  
2.  設定組\* *StrLen_or_IndPtr*為 SQL_NULL_DATA，如果資料為 NULL。 如果資料為 NULL 並*StrLen_or_IndPtr*是 null 指標， **SQLGetData**傳回 SQLSTATE 22002 （指標變數所需但未提供）。  
  
     如果資料行的資料不是 NULL， **SQLGetData**繼續進行步驟 3。  
  
3.  如果 SQL_ATTR_MAX_LENGTH 陳述式屬性設定為非零值，如果資料行包含字元或二進位資料，而且**SQLGetData**先前尚未呼叫資料行，資料會被截斷成 SQL_ATTR_MAX_LENGTH位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 陳述式屬性被要減少網路流量。 它通常被藉由資料來源，再透過網路進行截斷的資料。 驅動程式和資料來源不需要支援它。 因此，若要確保資料會截斷成特定的大小，應用程式應該配置該大小的緩衝區和指定的大小以*Columnsize*引數。  
  
4.  將資料轉換成在指定的型別*TargetType*。 資料是針對該資料類型提供的預設有效位數和小數位數。 如果*TargetType*是 SQL_ARD_TYPE，資料種 ARD SQL_DESC_CONCISE_TYPE 欄位中的使用。 如果*TargetType*是 SQL_ARD_TYPE，提供資料的有效位數和小數位數的 SQL_DESC_DATETIME_INTERVAL_PRECISION SQL_DESC_PRECISION，在輸入 SQL_DESC_CONCISE SQL_DESC_SCALE ARD，根據資料欄位類型 （_t） 欄位。 應用程式如果任何預設有效位數或小數位數不適用，應該明確設定適當的描述項欄位呼叫**SQLSetDescField**或是**SQLSetDescRec**。  
  
5.  如果資料已轉換成可變長度資料類型，例如字元或二進位**SQLGetData**會檢查資料的長度是否超過*Columnsize*。 如果字元資料 （包括 null 結束字元） 的長度超過*Columnsize*， **SQLGetData**截斷的資料來*Columnsize*小於長度null 結束字元。 它接著 null 終止的資料。 如果二進位資料的長度超過資料緩衝區的長度**SQLGetData**才會截斷*Columnsize*位元組。  
  
     提供的資料緩衝區太小無法容納在字元的 null 終止後，是否**SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004。  
  
     **SQLGetData**永遠不會截斷轉換為固定長度資料類型的資料，它一律假設的長度 **TargetValuePtr*是資料類型的大小。  
  
6.  會將已轉換 （以及可能已截斷） 的資料，在放置\* *TargetValuePtr*。 請注意， **SQLGetData**無法傳回資料列。  
  
7.  會放置在資料的長度\* *StrLen_or_IndPtr*。 如果*StrLen_or_IndPtr*是 null 指標， **SQLGetData**不會傳回長度。  
  
    -   針對字元或二進位資料，這是資料的長度轉換後再因為截斷*Columnsize*。 如果驅動程式無法在轉換之後，判斷資料的長度，因為有時候是 long 資料的情況，它會傳回 SQL_SUCCESS_WITH_INFO，並將長度設定為 SQL_NO_TOTAL。 (在上次呼叫**SQLGetData**必須一律會傳回資料，而不為零或 SQL_NO_TOTAL 的長度。)如果資料已截斷由於 SQL_ATTR_MAX_LENGTH 陳述式屬性，這個屬性-而不是實際的長度-值會置於\* *StrLen_or_IndPtr*。 這是因為此屬性可讓驅動程式有沒有辦法找出的實際長度會截斷轉換之前, 在伺服器上的資料。 當**SQLGetData**是連續的多次呼叫相同的資料行中，這是在目前的呼叫開頭的可用資料的長度; 長度也就是減少與每個後續的呼叫。  
  
    -   對於所有其他資料類型，這是在轉換後資料的長度也就是說，它是已轉換的目標資料類型的大小。  
  
8.  如果資料不會遺失重要的在轉換時截斷 （例如，實數 1.234 時會被截斷轉換成整數 1），或因為*Columnsize*太小 （例如，字串"abcdef"位於在 4 個位元組的緩衝區）， **SQLGetData**傳回 SQLSTATE 01004 （資料已截斷） 和 SQL_SUCCESS_WITH_INFO。 如果資料遭到截斷而不會遺失精確度 SQL_ATTR_MAX_LENGTH 陳述式屬性，因為**SQLGetData**都會傳回 SQL_SUCCESS，且沒有傳回 SQLSTATE 01004 （資料已截斷）。  
  
 繫結的資料緩衝區的內容 (如果**SQLGetData**繫結的資料行上呼叫) 和長度/指標緩衝區是未定義的如果**SQLGetData**不會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。  
  
 後續呼叫**SQLGetData**會從要求的最後一個資料行擷取資料; 先前的位移會變成無效。 例如，下列順序執行時：  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 第二個呼叫 SQLGetData(icol=n) 從 n 的資料行中開頭擷取資料。 中的資料，因為先前呼叫的任何位移**SQLGetData**的資料行已不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>描述項和 SQLGetData  
 **SQLGetData**不會直接與任何描述項欄位互動。  
  
 如果*TargetType*是 SQL_ARD_TYPE，資料種 ARD SQL_DESC_CONCISE_TYPE 欄位中的使用。 如果*TargetType*是 SQL_ARD_TYPE 或 SQL_C_DEFAULT，資料提供的有效位數和小數位數的 SQL_DESC_DATETIME_INTERVAL_PRECISION SQL_DESC_PRECISION，SQL_DESC_SCALE 欄位 ARD，根據的資料類型在 [SQL_DESC_CONCISE_TYPE] 欄位中。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，執行應用程式**選取**陳述式來傳回結果集的客戶識別碼、 名稱和電話號碼依名稱、 識別碼和電話號碼。 針對每個資料列，它會呼叫**SQLFetch**若要將游標移至下一個資料列位置。 它會呼叫**SQLGetData**擷取的已擷取的資料，針對資料而傳回的位元組數目的緩衝區中指定呼叫**SQLGetData**。 最後，它會列印每位員工的名稱、 識別碼和電話號碼。  
  
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
|指派儲存體中結果集資料行|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行區塊資料指標位置無關的大量作業|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消陳述式處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|擷取單一資料列或順向方向中的資料區塊|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在執行階段傳送參數資料|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|遊標定位、 重新整理此資料列集中，或更新或刪除資料列集中的資料|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
