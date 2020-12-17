---
description: SQLBindCol 函數
title: SQLBindCol 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindCol
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e6eaebf18b37df69ebe922aa4b42671378fc659
ms.sourcegitcommit: 8a8c89b0ff6d6dfb8554b92187aca1bf0f8bcc07
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/17/2020
ms.locfileid: "97617517"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLBindCol** 會將應用程式資料緩衝區系結至結果集內的資料行。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *ColumnNumber*  
 輸出要系結的結果集資料行數目。 資料行的編號是從0開始遞增資料行順序，其中資料行0是書簽資料行。 如果未使用書簽，也就是 SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_OFF，則資料行編號會從1開始。  
  
 *TargetType*  
 輸出TargetValuePtr 緩衝區之 C 資料類型的識別碼 \*  。 當它使用 **SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations** 或 **SQLSetPos** 從資料來源抓取資料時，驅動程式會將資料轉換成此類型;當它使用 **SQLBulkOperations** 或 **SQLSetPos** 將資料傳送到資料來源時，驅動程式會轉換此類型的資料。 如需有效的 C 資料類型和類型識別碼的清單，請參閱附錄 D：資料類型中的 [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md) 一節。  
  
 如果 *TargetType* 引數是 interval 資料類型，則預設的間隔 (2) 和預設間隔秒精確度 (6) （分別在 ARD 的 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 和 [SQL_DESC_PRECISION] 欄位中設定）用於資料。 如果有 SQL_C_NUMERIC *TargetType* 引數，則會使用資料的預設有效位數 (驅動程式定義的) 和預設小數位數 (0) （如同在 ARD 的 [SQL_DESC_PRECISION] 和 [SQL_DESC_SCALE] 欄位中所設定）。 如果任何預設有效位數或小數位數不適當，則應用程式應該透過呼叫 **SQLSetDescField** 或 **SQLSetDescRec** 明確地設定適當的描述項欄位。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱 [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [延遲的輸入/輸出]要系結至資料行之資料緩衝區的指標。 **SQLFetch** 和 **SQLFetchScroll** 會傳回這個緩衝區中的資料。 *當作業 SQL_FETCH_BY_BOOKMARK 時，* **SQLBulkOperations** 會傳回這個緩衝區中的資料;當 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK 作業 *時，它* 會從這個緩衝區中取出資料。 *當作業 SQL_REFRESH 時，* **SQLSetPos** 會傳回這個緩衝區中的資料;*當 SQL_UPDATE 作業時，* 它會從這個緩衝區中取出資料。  
  
 如果 *TargetValuePtr* 為 null 指標，驅動程式會將資料行的資料緩衝區解除系結。 應用程式可以使用 SQL_UNBIND 選項來呼叫 **SQLFreeStmt** ，以將所有資料行解除系結。 如果呼叫 **SQLBindCol** 的 *TargetValuePtr* 引數為 null 指標，但 *StrLen_or_IndPtr* 引數是有效的值，則應用程式可以解除資料行的資料緩衝區系結，但仍會有系結至資料行的長度/指標緩衝區。  
  
 *BufferLength*  
 輸出\* *TargetValuePtr* 緩衝區的長度（以位元組為單位）。  
  
 驅動程式會使用 *BufferLength* 來避免在傳回 \* 可變長度的資料（例如字元或二進位資料）時，寫入超過 *TargetValuePtr* 緩衝區的結尾。 請注意，驅動程式會在將字元資料傳回至 TargetValuePtr 時，計算 null 終止字元 \* **。 \*因此， *TargetValuePtr* 必須包含 null 終止字元的空格，否則驅動程式將會截斷資料。  
  
 當驅動程式傳回固定長度的資料（例如整數或日期結構）時，驅動程式會忽略 *BufferLength* ，並假設緩衝區夠大而足以容納資料。 因此，應用程式必須為固定長度的資料配置夠大的緩衝區，否則驅動程式將寫入超過緩衝區結尾。  
  
 當 *BufferLength* 小於0時， **SQLBINDCOL** 會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度，而當 *BufferLength* 為0時則不會傳回緩衝區) 長度。 但是，如果 *TargetType* 指定了字元類型，應用程式不應該將 *BufferLength* 設定為0，因為符合 ISO CLI 規範的驅動程式會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 在該情況下。  
  
 *StrLen_or_IndPtr*  
 [延遲的輸入/輸出]要系結至資料行之長度/指標緩衝區的指標。 **SQLFetch** 和 **SQLFetchScroll** 會在此緩衝區中傳回值。 當 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK 的作業 *時，* **SQLBulkOperations** 會從此緩衝區抓取值。 當 SQL_FETCH_BY_BOOKMARK *操作* 時， **SQLBulkOperations** 會傳回這個緩衝區中的值。 當 SQL_REFRESH *操作* 時， **SQLSetPos** 會在此緩衝區中傳回值;當 SQL_UPDATE *操作* 時，它會從這個緩衝區抓取值。  
  
 **SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations** 和 **SQLSetPos** 可以傳回長度/指標緩衝區中的下列值：  
  
-   可傳回的資料長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_Null_DATA  
  
 應用程式可將下列值放在長度/指標緩衝區中，以搭配 **SQLBulkOperations** 或 **SQLSetPos** 使用：  
  
-   正在傳送的資料長度  
  
-   SQL_NTS  
  
-   SQL_Null_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 宏的結果  
  
-   SQL_COLUMN_IGNORE  
  
 如果指標緩衝區和長度緩衝區是不同的緩衝區，指標緩衝區只能傳回 SQL_Null_DATA，而長度緩衝區可以傳回所有其他值。  
  
 如需詳細資訊，請參閱 [SQLBulkOperations 函數](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)函式、 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)函式，以及 [使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 如果 *StrLen_or_IndPtr* 為 null 指標，則不會使用長度或指標值。 這是在提取資料和資料為 Null 時的錯誤。  
  
 如果您的應用程式將在64位作業系統上執行，請參閱 [ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當 **SQLBindCol** 傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫 **SQLGetDiagRec** 和 *HandleType* （SQL_HANDLE_STMT）和 *StatementHandle* 的 *控制碼* 來取得相關聯的 SQLSTATE 值。 下表列出 **SQLBindCol** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規| (DM) *ColumnNumber* 引數為0，但 *TargetType* 引數不 SQL_C_BOOKMARK 或 SQL_C_VARBOOKMARK。|  
|07009|描述元索引無效|針對引數 *ColumnNumber* 指定的值超過結果集中的資料行數目上限。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec** 在 *\* MessageText* 緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY003 以及|不正確應用程式緩衝區類型|引數 *TargetType* 不是有效的資料類型，也不是 SQL_C_DEFAULT。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle* 相關聯的連接控制碼所呼叫。 呼叫 **SQLBindCol** 時，這個非同步函數仍在執行中。<br /><br /> 針對 *StatementHandle* 呼叫 **SQLExecute**、 **SQLEXECDIRECT** 或 **SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 針對 *StatementHandle* 呼叫非同步執行的函式，但在呼叫此函式時仍在執行。<br /><br /> 針對 *StatementHandle* 呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations** 或 **SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 引數 *BufferLength* 指定的值小於0。<br /><br />  (DM) 驅動程式是 ODBC 2。*x* 驅動程式， *ColumnNumber* 引數設定為0，而針對引數 *BufferLength* 指定的值不等於4。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|驅動程式或資料來源不支援由 *TargetType* 引數和對應資料行之驅動程式特定的 SQL 資料類型的組合所指定的轉換。<br /><br /> 引數 *ColumnNumber* 為0，驅動程式不支援書簽。<br /><br /> 此驅動程式僅支援 ODBC 2。*x* 和引數 *TargetType* 是下列其中一項：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 以及附錄 D：資料類型中 [c 資料類型](../../../odbc/reference/appendixes/c-data-types.md) 所列的任何間隔 c 資料類型。<br /><br /> 驅動程式只支援3.50 之前的 ODBC 版本，且引數 *TargetType* 已 SQL_C_GUID。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 **SQLBindCol** 是用來將結果集中的 *資料行與* 應用程式中的資料緩衝區和長度/指標緩衝區相關聯或系結。 當應用程式呼叫 **SQLFetch**、 **SQLFetchScroll** 或 **SQLSetPos** 來提取資料時，驅動程式會在指定的緩衝區中傳回系結資料行的資料;如需詳細資訊，請參閱 [SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。 當應用程式呼叫 **SQLBulkOperations** 來更新或插入資料列或 **SQLSetPos** 來更新資料列時，驅動程式會從指定的緩衝區抓取系結資料行的資料;如需詳細資訊，請參閱 [SQLBulkOperations 函數](../../../odbc/reference/syntax/sqlbulkoperations-function.md) 或 [SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。 如需系結的詳細資訊，請參閱 [ (基本) 取得結果 ](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 請注意，資料行不需要系結以從中抓取資料。 應用程式也可以呼叫 **SQLGetData** ，以從資料行中取出資料。 雖然可以系結資料列中的某些資料行，並為其他資料行呼叫 **SQLGetData** ，但這會受到某些限制。 如需詳細資訊，請參閱 [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>系結、解除系結和重新系結資料行  
 您可以隨時系結、解除系結或解除系結資料行，即使已經從結果集提取資料。 新的系結會在下一次呼叫使用系結的函數時生效。 例如，假設應用程式系結結果集中的資料行，並呼叫 **SQLFetch**。 驅動程式會傳回系結緩衝區中的資料。 現在假設應用程式將資料行系結至一組不同的緩衝區。 驅動程式不會將剛剛提取資料列的資料放在新系結緩衝區中。 相反地，它會等到再次呼叫 **SQLFetch** ，然後將下一個資料列的資料放在新系結的緩衝區中。  
  
> [!NOTE]  
>  您應該一律先設定語句屬性 SQL_ATTR_USE_BOOKMARKS，再將資料行系結至資料行0。 這並非必要，但強烈建議使用。  
  
## <a name="binding-columns"></a>繫結資料行  
 為了系結資料行，應用程式會呼叫 **SQLBindCol** ，並傳遞資料緩衝區的資料行編號、類型、位址和長度，以及長度/指標緩衝區的位址。 如需有關如何使用這些位址的詳細資訊，請參閱本節稍後的「緩衝區位址」。 如需系結資料行的詳細資訊，請參閱 [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 這些緩衝區的使用會延後;也就是說，應用程式會在 **SQLBindCol** 中系結它們，但驅動程式會從其他函式存取它們，也就是 **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll** 或 **SQLSetPos**。 應用程式必須負責確定在 **SQLBindCol** 中指定的指標保持有效，只要系結仍有效。 如果應用程式允許這些指標變成無效-例如，它會釋出緩衝區，然後呼叫預期它們有效的函式，則結果會是未定義的。 如需詳細資訊，請參閱 [延遲的緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 系結會一直有效，直到以新系結取代、將資料行解除系結，或釋放語句為止。  
  
## <a name="unbinding-columns"></a>解除系結資料行  
 若要解除單一資料行的系結，應用程式會呼叫 **SQLBindCol** ，並將 *ColumnNumber* 設定為該資料行的數目，並將 *TargetValuePtr* 設定為 null 指標。 如果 *ColumnNumber* 參考未系結的資料行，則 **SQLBindCol** 仍會傳回 SQL_SUCCESS。  
  
 若要解除系結所有資料行，應用程式會呼叫 **SQLFreeStmt** ，並將 *fOption* 設定為 SQL_UNBIND。 將 ARD 的 SQL_DESC_COUNT 欄位設定為零，也可以完成這項作業。  
  
## <a name="rebinding-columns"></a>重新系結資料行  
 應用程式可以執行兩項作業的其中之一來變更系結：  
  
-   呼叫 **SQLBindCol** 可為已系結的資料行指定新的系結。 驅動程式會以新的系結覆寫舊的系結。  
  
-   指定要加入至 **SQLBindCol** 的系結呼叫所指定的緩衝區位址之位移。 如需詳細資訊，請參閱下一節「系結位移」。  
  
## <a name="binding-offsets"></a>系結位移  
 系結位移是一個值，這個值會加入至資料的位址和長度/指標緩衝區 (如 *TargetValuePtr* 和 *StrLen_or_IndPtr* 引數) 中所指定的值，然後再進行取值。 使用位移時，系結是應用程式緩衝區配置方式的「範本」，而應用程式可以藉由變更位移，將此「範本」移至不同的記憶體區域。 因為會將相同的位移加入每個系結中的每個位址，不同資料行的緩衝區之間的相對位移必須在每一組緩衝區內都相同。 當使用資料列取向的系結時，這一律為 true;應用程式必須仔細配置緩衝區，以便在使用資料行取向的系結時，將此值設為 true。  
  
 使用系結位移基本上與透過呼叫 **SQLBindCol** 來重新系結資料行的效果相同。 不同之處在于，對 **SQLBindCol** 的新呼叫會指定資料緩衝區和長度/指標緩衝區的新位址，而使用系結位移並不會變更位址，而只會在其中加上位移。 應用程式可以在需要時指定新的位移，而此位移一律會新增至原始系結的位址。 尤其是，如果位移設定為0，或如果語句屬性設為 null 指標，則驅動程式會使用原始系結的位址。  
  
 若要指定系結位移，應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用系結的函式之前，它會在此緩衝區中以位元組為單位放置位移。 為了判斷要使用的緩衝區位址，驅動程式會將位移新增至系結中的位址。 位址和位移的總和必須是有效的位址，但是加入位移的位址不一定要有效。 如需如何使用系結位移的詳細資訊，請參閱本節稍後的「緩衝區位址」。  
  
## <a name="binding-arrays"></a>系結陣列  
 如果資料列集大小 (SQL_ATTR_ROW_ARRAY_SIZE 語句屬性的值) 大於1，則應用程式會系結緩衝區的陣列，而不是單一緩衝區。 如需詳細資訊，請參閱 [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 應用程式可透過兩種方式來系結陣列：  
  
-   將陣列系結至每個資料行。 這稱為資料 *行* 取向系結，因為每個資料結構 (陣列) 包含單一資料行的資料。  
  
-   定義結構來保存整個資料列的資料，並系結這些結構的陣列。 這稱為資料 *列* 取向系結，因為每個資料結構都包含單一資料列的資料。  
  
 緩衝區的每個陣列至少必須有與資料列集大小一樣多的元素。  
  
> [!NOTE]  
>  應用程式必須確認對齊有效。 如需對齊考慮的詳細資訊，請參閱 [對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>資料行取向的繫結  
 在資料行取向的系結中，應用程式會將不同的資料和長度/指標陣列系結至每個資料行。  
  
 若要使用資料行取向的系結，應用程式會先將 SQL_ATTR_ROW_BIND_TYPE 語句屬性設定為 SQL_BIND_BY_COLUMN。  (這是預設值。 ) 每個要系結的資料行，應用程式會執行下列步驟：  
  
1.  配置資料緩衝區陣列。  
  
2.  配置長度/指標緩衝區的陣列。  
  
    > [!NOTE]  
    >  如果在使用資料行取向的系結時，應用程式直接寫入描述元，則可以將不同的陣列用於長度和指標資料。  
  
3.  使用下列引數呼叫 **SQLBindCol** ：  
  
    -   *TargetType* 是資料緩衝區陣列中單一元素的型別。  
  
    -   *TargetValuePtr* 是資料緩衝區陣列的位址。  
  
    -   *BufferLength* 是資料緩衝區陣列中單一元素的大小。 當資料是固定長度的資料時，會忽略 *BufferLength* 引數。  
  
    -   *StrLen_or_IndPtr* 是長度/指標陣列的位址。  
  
 如需有關如何使用這項資訊的詳細資訊，請參閱本節稍後的「緩衝區位址」。 如需資料行取向系結的詳細資訊，請參閱資料 [行](../../../odbc/reference/develop-app/column-wise-binding.md)取向的系結。  
  
## <a name="row-wise-binding"></a>資料列取向的繫結  
 在資料列取向系結中，應用程式會定義結構，其中包含要系結之每個資料行的資料和長度/指標緩衝區。  
  
 若要使用資料列取向的系結，應用程式會執行下列步驟：  
  
1.  定義結構來保存單一資料列 (包括資料和長度/指標緩衝區) 並配置這些結構的陣列。  
  
    > [!NOTE]  
    >  如果使用資料列取向的系結時，應用程式直接寫入描述元，則可以使用不同的欄位來表示長度和指標資料。  
  
2.  將 SQL_ATTR_ROW_BIND_TYPE 語句屬性設定為包含單一資料列的結構大小，或將結果資料行系結至的緩衝區實例大小。 長度必須包含所有系結資料行的空間，以及結構或緩衝區的任何填補，以確保當系結資料行的位址以指定的長度遞增時，結果會指向下一個資料列中相同資料行的開頭。 在 ANSI C 中使用 *sizeof* 運算子時，會保證此行為。  
  
3.  針對要系結的每個資料行，使用下列引數呼叫 **SQLBindCol** ：  
  
    -   *TargetType* 是要系結至資料行之資料緩衝區成員的型別。  
  
    -   *TargetValuePtr* 是第一個陣列元素中資料緩衝區成員的位址。  
  
    -   *BufferLength* 是資料緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr* 是要系結之長度/指標成員的位址。  
  
 如需有關如何使用這項資訊的詳細資訊，請參閱本節稍後的「緩衝區位址」。 如需資料 [行](../../../odbc/reference/develop-app/row-wise-binding.md)取向系結的詳細資訊，請參閱資料列取向的系結。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 *緩衝區位址* 是資料或長度/指標緩衝區的實際位址。 驅動程式會在寫入緩衝區之前計算緩衝區位址， (例如提取期間) 。 其計算方式是使用下列公式，此公式會使用 *TargetValuePtr* 和 *StrLen_or_IndPtr* 引數中指定的位址、系結位移和資料列編號：  
  
 系結 *位址*  + *Binding Offset* + ( # B1 *Row Number* -1) x *元素大小*)   
  
 公式的變數定義如下表中所述。  
  
|變數|描述|  
|--------------|-----------------|  
|*系結位址*|針對資料緩衝區，在 **SQLBindCol** 中使用 *TargetValuePtr* 引數指定的位址。<br /><br /> 針對長度/指標緩衝區，以 **SQLBindCol** 中的 *StrLen_or_IndPtr* 引數指定的位址。 如需詳細資訊，請參閱「描述元和 SQLBindCol」一節中的「其他批註」。<br /><br /> 如果系結的位址是0，則不會傳回任何資料值，即使先前公式所計算的位址不是零也一樣。|  
|*系結位移*|如果使用資料列取向的系結，則會將值儲存在使用 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性指定的位址。<br /><br /> 如果使用了資料行取向的系結，或者 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性的值是 null 指標，系結 *位移* 就是0。|  
|*資料列編號*|資料列集中的資料列編號，以1為基點數。 若為單一資料列提取（預設值），則為1。|  
|*元素大小*|系結陣列中元素的大小。<br /><br /> 如果使用資料行取向的系結，這會是 sizeof (長度/指標緩衝區的 **SQLINTEGER)** 。 針對資料緩衝區，如果資料類型是可變長度，則為 **SQLBindCol** 中 *BufferLength* 引數的值，如果資料類型為固定長度，則為資料類型的大小。<br /><br /> 如果使用資料列取向的系結，這就是資料和長度/指標緩衝區的 SQL_ATTR_ROW_BIND_TYPE 語句屬性值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>描述項和 SQLBindCol  
 下列各節描述 **SQLBindCol** 與描述項的互動方式。  
  
> [!CAUTION]  
>  針對一個語句呼叫 **SQLBindCol** 可能會影響其他語句。 當明確配置與語句相關聯的 ARD，而且也與其他語句相關聯時，就會發生這種情況。 因為 **SQLBindCol** 會修改描述項，所以會將修改套用至與這個描述項相關聯的所有語句。 如果這不是必要的行為，應用程式應該在呼叫 **SQLBindCol** 之前，將此描述項與其他語句中斷關聯。  
  
## <a name="argument-mappings"></a>引數對應  
 就概念而言， **SQLBindCol** 會依序執行下列步驟：  
  
1.  呼叫 **SQLGetStmtAttr** 以取得 ARD 控制碼。  
  
2.  呼叫 **SQLGetDescField** 以取得此描述項的 SQL_DESC_COUNT 欄位，如果 *ColumnNumber* 引數中的值超過 SQL_DESC_COUNT 的值，則會呼叫 **SQLSetDescField** 將 SQL_DESC_COUNT 的值增加為 *ColumnNumber*。  
  
3.  呼叫 **SQLSetDescField** 多次，將值指派給 ARD 的下欄欄位：  
  
    -   將 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定為 *TargetType* 的值，不同之處在于如果 *TargetType* 是 datetime 或 interval 子類型的其中一個精確識別碼，則會將 SQL_DESC_TYPE 分別設定為 SQL_DATETIME 或 SQL_INTERVAL。將 SQL_DESC_CONCISE_TYPE 設定為簡潔的識別碼;並將 SQL_DESC_DATETIME_INTERVAL_CODE 設定為對應的日期時間或間隔子代碼。  
  
    -   設定一或多個 SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，適用于 *TargetType*。  
  
    -   將 SQL_DESC_OCTET_LENGTH 欄位設定為 *BufferLength* 的值。  
  
    -   將 SQL_DESC_DATA_PTR 欄位設定為 *TargetValuePtr* 的值。  
  
    -   將 SQL_DESC_INDICATOR_PTR 欄位設定為 *StrLen_or_IndPtr* 的值。  (請參閱下列段落。 )   
  
    -   將 SQL_DESC_OCTET_LENGTH_PTR 欄位設定為 *StrLen_or_IndPtr* 的值。  (請參閱下列段落。 )   
  
 *StrLen_or_IndPtr* 引數所參考的變數會用於指標和長度資訊。 如果 fetch 遇到資料行的 null 值，則會將 SQL_Null_DATA 儲存在此變數中;否則，它會儲存此變數中的資料長度。 將 null 指標傳遞為 *StrLen_or_IndPtr* 會讓 fetch 作業不會傳回資料長度，但如果它遇到 null 值，而且沒有任何方法可傳回 SQL_Null_DATA，則會讓提取作業失敗。  
  
 如果 **SQLBindCol** 的呼叫失敗，則會在 ARD 中設定的描述項欄位內容未定義，且 ARD 的 SQL_DESC_COUNT 欄位值不會變更。  
  
## <a name="implicit-resetting-of-count-field"></a>[計數] 欄位的隱含重設  
 只有在這會增加 SQL_DESC_COUNT 的值時， **SQLBindCol** 才會將 SQL_DESC_COUNT 設定為 *ColumnNumber* 引數的值。 如果 *TargetValuePtr* 引數中的值為 null 指標，而 *ColumnNumber* 引數中的值等於 SQL_DESC_COUNT (也就是說，當您將最高系結的資料行解除系結) 時，SQL_DESC_COUNT 會設定為最高剩餘系結資料行的數目。  
  
## <a name="cautions-regarding-sql_default"></a>關於 SQL_DEFAULT 的注意事項  
 若要成功地取出資料行資料，應用程式必須正確地判斷應用程式緩衝區中資料的長度和起點。 當應用程式指定明確的 *TargetType* 時，很容易就會偵測到應用程式誤解。 不過，當應用程式指定 SQL_DEFAULT 的 *TargetType* 時，可以將 **SQLBindCol** 套用至不同資料類型的資料行，而不是來自應用程式所需的資料行，不論是中繼資料的變更或將程式碼套用至不同的資料行。 在此情況下，應用程式不一定會判斷提取的資料行資料的開始或長度。 這可能會導致未報告的資料錯誤或記憶體違規。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會在 Customers 資料表上執行 **SELECT** 語句，以傳回客戶識別碼、名稱和電話號碼的結果集（依名稱排序）。 然後，它會呼叫 **SQLBindCol** ，將資料的資料行系結至本機緩衝區。 最後，應用程式會使用 **SQLFetch** 提取每個資料列，並列印每個客戶的名稱、識別碼和電話號碼。  
  
 如需更多程式碼範例，請參閱 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)函式、 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)函式、 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函式和 [SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 60
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_WCHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_WCHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_WCHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (int i=0 ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                     {
                        //replace wprintf with printf
                        //%S with %ls
                        //warning C4477: 'wprintf' : format string '%S' requires an argument of type 'char *'
                        //but variadic argument 2 has type 'SQLWCHAR *'
                        //wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                        printf("%d: %ls %ls %ls\n", i + 1, sCustID, szName, szPhone);  
                    }    
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 另請參閱 [ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函數](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|釋放語句上的資料行緩衝區|[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|提取部分或全部資料行|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
