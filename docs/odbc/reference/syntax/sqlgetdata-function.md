---
description: SQLGetData 函數
title: SQLGetData 函式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a659e1bb5ad7765dbfcbcb01dbc16744de7cfc20
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461076"
---
# <a name="sqlgetdata-function"></a>SQLGetData 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetData** 會在結果集中取得單一資料行的資料，或在 **SQLParamData** 傳回 SQL_PARAM_DATA_AVAILABLE 之後，取得單一參數的資料。 您可以多次呼叫它，以在元件中取出可變長度的資料。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 輸出語句控制碼。  
  
 *Col_or_Param_Num*  
 輸出若要取得資料行資料，它是要傳回資料的資料行編號。 結果集資料行的編號是從1開始的遞增資料行順序。 書簽資料行是資料行編號 0;只有在啟用書簽時，才能指定此功能。  
  
 針對抓取參數資料，它是參數的序數，從1開始。  
  
 *TargetType*  
 輸出**TargetValuePtr* 緩衝區之 C 資料類型的類型識別碼。 如需有效的 C 資料類型和類型識別碼的清單，請參閱附錄 D：資料類型中的 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md) 一節。  
  
 如果 *TargetType* 是 SQL_ARD_TYPE，驅動程式會使用 ARD 的 SQL_DESC_CONCISE_TYPE 欄位中所指定的類型識別碼。 如果 *TargetType* 是 SQL_APD_TYPE， **SQLGetData** 將會使用 **SQLBindParameter**中所指定的相同 C 資料類型。 否則，在 **SQLGetData** 中指定的 c 資料類型會覆寫 **SQLBindParameter**中指定的 c 資料類型。 如果 SQL_C_DEFAULT，驅動程式會根據來源的 SQL 資料類型，選取預設的 C 資料類型。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱 [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 出要傳回資料之緩衝區的指標。  
  
 *TargetValuePtr* 不可為 Null。  
  
 *BufferLength*  
 輸出**TargetValuePtr* 緩衝區的長度（以位元組為單位）。  
  
 驅動程式會使用*BufferLength*來避免 \* 在傳回可變長度的資料（例如字元或二進位資料）時寫入超過*TargetValuePtr*緩衝區的結尾。 請注意，在將字元資料傳回至 TargetValuePtr 時，驅動程式會計算 null 終止字元 \* * *。 *因此， *TargetValuePtr*必須包含 null 終止字元的空格，否則驅動程式將會截斷資料。  
  
 當驅動程式傳回固定長度的資料（例如整數或日期結構）時，驅動程式會忽略 *BufferLength* ，並假設緩衝區夠大而足以容納資料。 因此，應用程式必須為固定長度的資料配置夠大的緩衝區，否則驅動程式將寫入超過緩衝區結尾。  
  
 當*BufferLength*小於0時， **SQLGETDATA**會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度，而當*BufferLength*為0時則不會傳回緩衝區) 長度。  
  
 *StrLen_or_IndPtr*  
 出要在其中傳回長度或指標值之緩衝區的指標。 如果這是 null 指標，則不會傳回長度或指標值。 當提取的資料為 Null 時，就會傳回錯誤。  
  
 **SQLGetData** 可以傳回長度/指標緩衝區中的下列值：  
  
-   可傳回的資料長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_Null_DATA  
  
 如需詳細資訊，請參閱本主題中的 [使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) 和「批註」。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetData**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLGetData** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|無法在函式的單一呼叫中，取得指定之資料行 *Col_or_Param_Num*的所有資料。 SQL_NO_TOTAL 或在目前呼叫**SQLGetData**之前，指定的資料行中剩餘的資料長度會以 \* *StrLen_or_IndPtr*傳回。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) <br /><br /> 如需針對單一資料行使用多個 **SQLGetData** 呼叫的詳細資訊，請參閱「批註」。|  
|01S07|小數截斷|針對一或多個資料行傳回的資料已被截斷。 若為數值資料類型，則會截斷數位的小數部分。 若是時間、時間戳記和包含時間元件的間隔資料類型，時間的小數部分會被截斷。<br /><br />  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|結果集中資料行的資料值無法轉換成引數 *TargetType*所指定的 C 資料類型。|  
|07009|描述元索引無效|為引數 *Col_or_Param_Num* 指定的值為0，而且 SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_OFF。<br /><br /> 為引數 *Col_or_Param_Num* 指定的值大於結果集中的資料行數目。<br /><br /> *Col_or_Param_Num*值不等於可用參數的序數。<br /><br />  (DM) 指定的資料行已系結。 這項描述並不適用于在 **SQLGetInfo**中傳回 SQL_GETDATA_EXTENSIONS 選項之 SQL_GD_BOUND 位元遮罩的驅動程式。<br /><br />  (DM) 指定之資料行的數目小於或等於最大系結資料行的數目。 這項描述並不適用于在 **SQLGetInfo**中傳回 SQL_GETDATA_EXTENSIONS 選項之 SQL_GD_ANY_COLUMN 位元遮罩的驅動程式。<br /><br />  (DM) 應用程式已經針對目前的資料列呼叫 **SQLGetData** ;目前呼叫中所指定的資料行數目小於之前呼叫中所指定的資料行數目;而且，驅動程式不會傳回 **SQLGetInfo**中 SQL_GETDATA_EXTENSIONS 選項的 SQL_GD_ANY_ORDER 位元遮罩。<br /><br />  (DM) *TargetType* 引數是 SQL_ARD_TYPE 的，而且 ARD 中的 *Col_or_Param_Num* 描述項記錄無法進行一致性檢查。<br /><br />  (DM) *TargetType* 引數是 SQL_ARD_TYPE 的，而且 ARD 的 [SQL_DESC_COUNT] 欄位中的值小於 *Col_or_Param_Num* 引數。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22002|需要指標變數，但未提供|*StrLen_or_IndPtr* 為 null 指標，且已取出 null 資料。|  
|22003|數值超出範圍|傳回數值 (為數據行的數值或字串) ，會導致整個 (與要截斷之數位的小數部分) 相對。<br /><br /> 如需詳細資訊，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22007|不正確日期時間格式|結果集中的字元資料行系結至 C 日期、時間或時間戳記結構，而且資料行中的值分別是不正確日期、時間或時間戳記。 如需詳細資訊，請參閱 [附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|22012|零除|傳回的算術運算式值產生零除的值。|  
|22015|間隔欄位溢位|從確切數值或間隔 SQL 類型指派至間隔 C 類型，會導致在前置欄位中遺失有效位數。<br /><br /> 將資料傳回至間隔 C 類型時，不會在間隔 C 類型中表示 SQL 類型的值。|  
|22018|轉換規格的字元值無效|結果集中的字元資料行已傳回字元 C 緩衝區，而且資料行包含的字元沒有在緩衝區的字元集中表示。<br /><br /> C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;且資料行中的值不是系結 C 類型的有效常值。|  
|24000|指標狀態無效| (DM) 在未先呼叫 **SQLFetch** 或 **SQLFetchScroll** 的情況下呼叫函式，以將資料指標放在所需的資料列上。<br /><br />  (DM) *StatementHandle* 處於執行中狀態，但沒有與 *StatementHandle*相關聯的結果集。<br /><br /> 在 *StatementHandle* 上開啟了資料指標，但已呼叫 **SQLFetch** 或 **SQLFetchScroll** ，但資料指標位於結果集的開頭或結果集結尾之後。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在*MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY003 以及|程式類型超出範圍| (DM) 引數 *TargetType* 並不是有效的資料類型、SQL_C_DEFAULT、SQL_ARD_TYPE (（如果是在抓取資料行資料的情況下），或) SQL_APD_TYPE () 的參數資料。<br /><br />  (DM) 引數 *Col_or_Param_Num* 為0，且引數 *TargetType* 不 SQL_C_BOOKMARK 固定長度書簽或 SQL_C_VARBOOKMARK 作為可變長度書簽。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 已呼叫函式，並在它完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫該函式。<br /><br /> 已呼叫函式，並在完成執行之前 *，從多*執行緒應用程式中的不同執行緒呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫該函式。|  
|HY009|Null 指標的用法無效| (DM) 引數 *TargetValuePtr* 為 null 指標。|  
|HY010|函數順序錯誤| (DM) 指定的 *StatementHandle* 未處於執行中狀態。 在未先呼叫 **SQLExecDirect**、 **SQLExecute** 或 catalog 函數的情況下呼叫函式。<br /><br />  (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLGetData** 函式時，仍在執行此非同步函式。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。<br /><br />  (DM) *StatementHandle* 處於執行中狀態，但沒有與 *StatementHandle*相關聯的結果集。<br /><br /> 呼叫 **SQLExeceute**、 **SQLExecDirect**或 **SQLMoreResults** 傳回 SQL_PARAM_DATA_AVAILABLE，但呼叫 **SQLGetData** ，而不是 **SQLParamData**。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *BufferLength* 指定的值小於0。<br /><br /> 為引數 *BufferLength* 指定的值小於4， *Col_or_Param_Num* 引數設定為0，而驅動程式是 ODBC*2.x 驅動程式* 。|  
|HY109|不正確資料指標位置|資料指標在已刪除或無法提取的資料列上， **SQLSetPos**、 **SQLFetch**、 **SQLFetchScroll**或 **SQLBulkOperations**) 定位 (。<br /><br /> 資料指標是順向資料指標，且資料列集大小大於1。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援在**SQLFetchScroll**中使用具有多個資料列的**SQLGetData** 。 這項描述並不適用于在 **SQLGetInfo**中傳回 SQL_GETDATA_EXTENSIONS 選項之 SQL_GD_BLOCK 位元遮罩的驅動程式。<br /><br /> 驅動程式或資料來源不支援由 *TargetType* 引數和對應資料行之 SQL 資料類型的組合所指定的轉換。 只有當資料行的 SQL 資料類型對應至驅動程式特定的 SQL 資料類型時，才會套用這個錯誤。<br /><br /> 驅動程式僅支援 ODBC 2.x *，而*引數 *TargetType* 是下列其中一項：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 以及附錄 D：資料類型中 [c 資料類型](../../../odbc/reference/appendixes/c-data-types.md) 所列的任何間隔 c 資料類型。<br /><br /> 驅動程式只支援3.50 之前的 ODBC 版本，且引數 *TargetType* 已 SQL_C_GUID。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 對應至 *StatementHandle* 的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 **SQLGetData** 會傳回指定之資料行中的資料。 只有在由**SQLFetch**、 **SQLFetchScroll**或**SQLExtendedFetch**從結果集中提取一或多個資料列之後，才能呼叫**SQLGetData** 。 如果可變長度的資料太大而無法在 **SQLGetData** (的單一呼叫中傳回，因為應用程式) 有限制，所以 **SQLGetData** 可以在元件中取出。 您可以系結資料列中的某些資料行，並為其他資料行呼叫 **SQLGetData** ，但這會受到某些限制。 如需詳細資訊，請參閱 [取得較長的資料](../../../odbc/reference/develop-app/getting-long-data.md)。  
  
 如需搭配使用 **SQLGetData** 與資料流程輸出參數的相關資訊，請參閱 [使用 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-sqlgetdata"></a>使用 SQLGetData  
 如果驅動程式不支援 **SQLGetData**的延伸模組，此函式只會傳回未系結資料行的資料，而該資料行的數位大於最後一個系結資料行的資料行。 此外，在資料列中，每個**SQLGetData**呼叫中的*Col_or_Param_Num*引數值必須大於或等於上一個呼叫中*Col_or_Param_Num*的值;也就是說，您必須以遞增的資料行編號順序來抓取資料。 最後，如果不支援延伸模組，則如果資料列集大小大於1，就無法呼叫 **SQLGetData** 。  
  
 驅動程式可以放寬這些限制。 為了判斷驅動程式所放寬的限制，應用程式會使用下列任何一個 SQL_GETDATA_EXTENSIONS 選項來呼叫 **SQLGetInfo** ：  
  
-   您可以呼叫 SQL_GD_OUTPUT_PARAMS = **SQLGetData** 來傳回輸出參數值。 如需詳細資訊，請參閱 [使用 SQLGetData 來取出輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_GD_ANY_COLUMN。 如果傳回這個選項，就可以針對任何未系結的資料行呼叫 **SQLGetData** ，包括最後一個系結資料行之前的資料行。  
  
-   SQL_GD_ANY_ORDER。 如果傳回這個選項，則會以任何順序針對未系結的資料行呼叫 **SQLGetData** 。  
  
-   SQL_GD_BLOCK。 如果 **SQLGetInfo** 針對 SQL_GETDATA_EXTENSIONS InfoType 傳回這個選項，則當資料列集大小大於1時，驅動程式支援對 **SQLGetData** 的呼叫，而應用程式可使用 SQL_POSITION 選項來呼叫 **SQLSetPos** ，以在呼叫 SQLGetData 之前將游標放在正確的資料列上 **。**  
  
-   SQL_GD_BOUND。 如果傳回這個選項，則可以針對系結的資料行以及未系結的資料行呼叫 **SQLGetData** 。  
  
 這些限制有兩種例外狀況，以及驅動程式放寬這些限制的能力。 首先，當資料列集大小大於1時，永遠不應該針對順向資料指標呼叫 **SQLGetData** 。 其次，如果驅動程式支援書簽，它一定會支援對資料行0呼叫 **SQLGetData** 的能力，即使它不允許應用程式在最後一個系結資料行之前，對其他資料行呼叫 **SQLGetData** 也是如此。 當應用程式使用 ODBC 2 時， (*。 x*驅動程式時 **，SQLGetData**會在呼叫**SQLFetch**之後，以*Col_or_Param_Num*等於0的方式，成功傳回書簽，因為 odbc 3.x 驅動程式管理員會將**SQLFetch**對應到**SQLExtendedFetch** *FETCHORIENTATION* of SQL_FETCH_NEXT，而**SQLGetData** *的* *Col_or_Param_Num*為0則是由 odbc 3.x*驅動程式管理員*對應**到 SQLGetStmtOption fOption**的 *。 ) * SQL_GET_BOOKMARK  
  
 **SQLGetData** 不能用來針對剛剛藉由呼叫 **SQLBulkOperations** 與 SQL_ADD 選項所插入的資料列來取出書簽，因為資料指標不是位於資料列上。 應用程式可以在使用 SQL_ADD 呼叫 **SQLBulkOperations** 之前，先系結資料行0來取得這類資料列的書簽，在此情況下， **SQLBulkOperations** 會傳回系結緩衝區中的書簽。 然後，您可以使用 SQL_FETCH_BOOKMARK 來呼叫**SQLFetchScroll** ，以將資料指標重新置放至該資料列。  
  
 如果 *TargetType* 引數是 interval 資料類型，則預設的間隔 (2) 和預設間隔秒精確度 (6) （分別在 ARD 的 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 和 [SQL_DESC_PRECISION] 欄位中設定）用於資料。 如果 *TargetType* 引數是 SQL_C_NUMERIC 資料類型，則會使用資料的預設有效位數 (驅動程式定義的) 和預設小數位數 (0) （如同在 ARD 的 [SQL_DESC_PRECISION] 和 [SQL_DESC_SCALE] 欄位中所設定）。 如果任何預設有效位數或小數位數不適當，則應用程式應該透過呼叫 **SQLSetDescField** 或 **SQLSetDescRec**明確地設定適當的描述項欄位。 它可以將 SQL_DESC_CONCISE_TYPE 欄位設定為 SQL_C_NUMERIC，並使用 SQL_ARD_TYPE 的*TargetType*引數來呼叫**SQLGetData** ，這會導致使用描述項欄位中的有效位數和小數位數值。  
  
> [!NOTE]
>  在 ODBC 2.x*中，應用*程式會將*TargetType*設定為 SQL_C_DATE、SQL_C_TIME 或 SQL_C_TIMESTAMP，以表示 \* *TargetValuePtr*是日期、時間或時間戳記結構。 在 ODBC 3.x*中，應用*程式會將 *TargetType* 設定為 SQL_C_TYPE_DATE、SQL_C_TYPE_TIME 或 SQL_C_TYPE_TIMESTAMP。 視需要，驅動程式管理員會根據應用程式和驅動程式版本，進行適當的對應。  
  
## <a name="retrieving-variable-length-data-in-parts"></a>在元件中取出可變長度的資料  
 **SQLGetData** 可以用來從包含可變長度資料的資料行中取出資料，也就是當資料行的 SQL 資料類型識別碼是 SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_WCHAR、SQL_WVARCHAR、SQL_WLONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY，或變數長度類型的驅動程式特定識別碼。  
  
 若要從元件的資料行中取出資料，應用程式會連續針對相同的資料行呼叫 **SQLGetData** 多次。 在每次呼叫時， **SQLGetData** 會傳回資料的下一個部分。 應用程式會負責重組元件，並小心從字元資料的中間部分移除 null 終止字元。 如果有更多資料要傳回或沒有足夠的緩衝區配置給終止字元， **SQLGetData** 會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004， (資料截斷) 。 當它傳回資料的最後一部分時， **SQLGetData** 會傳回 SQL_SUCCESS。 在最後一個有效的呼叫上，不能傳回 SQL_NO_TOTAL 或零，以從資料行取出資料，因為應用程式不會知道應用程式緩衝區中有多少資料是有效的。 如果在這個之後呼叫 **SQLGetData** ，它會傳回 SQL_NO_DATA。 如需詳細資訊，請參閱下一節「使用 SQLGetData 抓取資料」。  
  
 **SQLGetData**可在部分中傳回可變長度的書簽。 如同其他資料，呼叫 **SQLGetData** 以傳回元件中可變長度的書簽將會傳回 SQLSTATE 01004 (字串資料，當有更多資料要傳回時，則會以右截斷) 和 SQL_SUCCESS_WITH_INFO。 這與 **SQLFetch** 或 **SQLFetchScroll**的呼叫截斷變數長度書簽時的情況不同，後者會傳回 SQL_ERROR 和 SQLSTATE 22001 (字串資料，右邊已截斷) 。  
  
 **SQLGetData** 不能用來傳回部分中的固定長度資料。 如果在包含固定長度資料之資料行的資料列中呼叫 **SQLGetData** 一次以上，就會傳回第一個呼叫之後的所有呼叫 SQL_NO_DATA。  
  
## <a name="retrieving-streamed-output-parameters"></a>正在抓取資料流程輸出參數  
 如果驅動程式支援串流的輸出參數，應用程式可以使用較小的緩衝區呼叫 **SQLGetData** 多次，以抓取大型參數值。 如需有關資料流程輸出參數的詳細資訊，請參閱 [使用 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="retrieving-data-with-sqlgetdata"></a>使用 SQLGetData 抓取資料  
 為了傳回指定之資料行的資料， **SQLGetData** 會執行下列一連串的步驟：  
  
1.  如果已傳回資料行的所有資料，則會傳回 SQL_NO_DATA。  
  
2.  \*如果資料為 Null，則將*StrLen_or_IndPtr*設定為 SQL_Null_DATA。 如果資料為 Null，且 *StrLen_or_IndPtr* 為 null 指標，則 **SQLGetData** 會傳回所需的 SQLSTATE 22002 (指標變數，但未提供) 。  
  
     如果資料行的資料不是 Null，則 **SQLGetData** 會繼續進行步驟3。  
  
3.  如果 SQL_ATTR_MAX_LENGTH 語句屬性設定為非零值，如果資料行包含字元或二進位資料，而且先前尚未針對資料行呼叫 **SQLGetData** ，則資料會被截斷為 SQL_ATTR_MAX_LENGTH 個位元組。  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 語句屬性的目的是要減少網路流量。 它通常是由資料來源所執行，這會在透過網路傳回資料之前截斷資料。 驅動程式和資料來源不需要支援。 因此，若要確保資料會被截斷為特定大小，應用程式應配置該大小的緩衝區，並在 *BufferLength* 引數中指定大小。  
  
4.  將資料轉換成 *TargetType*中指定的型別。 資料會獲得該資料類型的預設精確度和小數位數。 如果 *TargetType* 為 SQL_ARD_TYPE，則會使用 ARD 之 SQL_DESC_CONCISE_TYPE 欄位中的資料類型。 如果 *TargetType* 為 SQL_ARD_TYPE，則會根據 [SQL_DESC_CONCISE_TYPE] 欄位中的資料類型，在 ARD 的 [SQL_DESC_DATETIME_INTERVAL_PRECISION]、[SQL_DESC_PRECISION] 和 [SQL_DESC_SCALE] 欄位中提供資料的精確度和小數位數。 如果任何預設有效位數或小數位數不適當，則應用程式應該透過呼叫 **SQLSetDescField** 或 **SQLSetDescRec**明確地設定適當的描述項欄位。  
  
5.  如果資料已轉換成可變長度的資料類型（例如字元或二進位）， **SQLGetData** 會檢查資料的長度是否超過 *BufferLength*。 如果字元資料的長度 (包括 null 終止字元) 超過 *BufferLength*， **SQLGetData** 就會截斷資料，以 *BufferLength* 較少的 null 終止字元長度。 然後，它會以 null 結束資料。 如果二進位資料的長度超過資料緩衝區的長度， **SQLGetData** 會將它截斷為 *BufferLength* 的位元組。  
  
     如果提供的資料緩衝區太小而無法容納 null 終止字元， **SQLGetData** 會傳回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01004。  
  
     **SQLGetData** 絕對不會截斷轉換成固定長度資料類型的資料;它一律會假設 **TargetValuePtr* 的長度是資料類型的大小。  
  
6.  將已轉換的 (以及可能截斷的) 資料放在 \* *TargetValuePtr*中。 請注意， **SQLGetData** 無法傳回資料行。  
  
7.  將資料的長度放在 \* *StrLen_or_IndPtr*中。 如果 *StrLen_or_IndPtr* 為 null 指標，則 **SQLGetData** 不會傳回長度。  
  
    -   若為字元或二進位資料，這是轉換後和截斷之前的資料長度（因為 *BufferLength*）。 如果驅動程式無法在轉換後判斷資料的長度，有時會有 long 資料的情況，它會傳回 SQL_SUCCESS_WITH_INFO，並將長度設定為 SQL_NO_TOTAL。  (最後一次呼叫**SQLGetData**時，必須一律傳回資料的長度，而不是零或 SQL_NO_TOTAL。 ) 如果資料因為 SQL_ATTR_MAX_LENGTH 語句屬性而遭截斷，則此屬性的值（相對於實際的長度）會置於 \* *StrLen_or_IndPtr*中。 這是因為這個屬性是設計用來在轉換之前截斷伺服器上的資料，因此驅動程式無法找出實際的長度為何。 針對相同的資料行連續多次呼叫 **SQLGetData** 時，這是目前呼叫開始時可用的資料長度;也就是說，長度會隨著每個後續的呼叫而減少。  
  
    -   對於所有其他資料類型，這是轉換後的資料長度;也就是說，它是轉換資料的類型大小。  
  
8.  如果在轉換期間，資料會被截斷而不會失去精確度 (例如，在轉換成整數 1) 時，會截斷實數的1.234，或因為 *BufferLength* 太小 (例如，字串 "abcdef" 放在4位元組的緩衝區) 中， **SQLGETDATA** 會傳回 SQLSTATE 01004 (資料截斷) 和 SQL_SUCCESS_WITH_INFO。 如果資料因為 SQL_ATTR_MAX_LENGTH 語句屬性而被截斷而不會失去精確度，則 **SQLGetData** 會傳回 SQL_SUCCESS，而不會傳回 SQLSTATE 01004 (截斷的資料) 。  
  
 系結資料緩衝區的內容 (如果在系結資料) 行上呼叫 **SQLGetData** ，且如果 **SQLGetData** 未傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，則長度/指標緩衝區是未定義的。  
  
 後續呼叫 **SQLGetData** 將會從所要求的最後一個資料行中取出資料。先前的位移會變成無效。 例如，執行下列順序時：  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData (icol =) n 的第二次呼叫會從 n 資料行的開頭抓取資料。 由於先前對資料行的 **SQLGetData** 呼叫，資料中的任何位移都不再有效。  
  
## <a name="descriptors-and-sqlgetdata"></a>描述項和 SQLGetData  
 **SQLGetData** 不會直接與任何描述項欄位互動。  
  
 如果 *TargetType* 為 SQL_ARD_TYPE，則會使用 ARD 之 SQL_DESC_CONCISE_TYPE 欄位中的資料類型。 如果 *TargetType* 是 SQL_ARD_TYPE 或 SQL_C_DEFAULT，則會根據 [SQL_DESC_SCALE] 欄位中的資料類型，在 ARD 的 [SQL_DESC_DATETIME_INTERVAL_PRECISION]、[SQL_DESC_PRECISION] 和 [SQL_DESC_CONCISE_TYPE] 欄位中提供資料的精確度和小數位數。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會執行 **SELECT** 語句，以傳回客戶識別碼、名稱和電話號碼的結果集（依名稱、識別碼和電話號碼排序）。 針對每個資料列，它會呼叫 **SQLFetch** ，將資料指標定位至下一個資料列。 它會呼叫 **SQLGetData** 來取出提取的資料;對 **SQLGetData**的呼叫中指定了資料的緩衝區和傳回的位元組數目。 最後，它會列印每個員工的姓名、識別碼及電話號碼。  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|為結果集中的資料行指派儲存空間|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|執行與區塊資料指標位置無關的大量作業|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|取消語句處理|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 語句|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在執行時間傳送參數資料|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|定位資料指標、重新整理資料列集內的資料，或更新或刪除資料列集中的資料|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
