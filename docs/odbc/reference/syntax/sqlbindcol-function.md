---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c1c89ff79ee0fcac37f7b6e231e957e051c9db2e
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/12/2019
ms.locfileid: "72289281"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函數
**標準**  
 引進的版本：ODBC 1.0 標準合規性：ISO 92  
  
 **摘要**  
 **SQLBindCol**會將應用程式資料緩衝區系結至結果集內的資料行。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 源語句控制碼。  
  
 *ColumnNumber*  
 源要系結的結果集資料行數目。 資料行是以遞增的資料行順序編號，從0開始，其中資料行0是書簽資料行。 如果未使用書簽（也就是，SQL_ATTR_USE_BOOKMARKS 語句屬性設定為 SQL_UB_OFF），則資料行編號會從1開始。  
  
 *TargetType*  
 源@No__t-0*TargetValuePtr*緩衝區的 C 資料類型識別碼。 當它從資料來源使用**SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**或**SQLSetPos**來抓取資料時，驅動程式會將資料轉換成此類型。當它使用**SQLBulkOperations**或**SQLSetPos**將資料傳送到資料來源時，驅動程式會轉換此類型的資料。 如需有效 C 資料類型和類型識別碼的清單，請參閱附錄 D：中的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)一節。資料類型。  
  
 如果*TargetType*引數是 interval 資料類型，則為預設的間隔前置精確度（2）和預設間隔秒數精確度（6），分別在 ARD 的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 欄位中設定。會用於資料。 如果*TargetType*引數是 SQL_C_NUMERIC，則會針對資料使用預設的有效位數（驅動程式定義）和預設小數位數（0）（如 ARD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定）。 如果任何預設的有效位數或小數位數不適當，應用程式應該藉由呼叫**SQLSetDescField**或**SQLSetDescRec**來明確設定適當的描述項欄位。  
  
 您也可以指定擴充 C 資料類型。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [延遲的輸入/輸出]要系結至資料行之資料緩衝區的指標。 **SQLFetch**和**SQLFetchScroll**會傳回此緩衝區中的資料。 當*Operation*為 SQL_FETCH_BY_BOOKMARK 時， **SQLBulkOperations**會傳回此緩衝區中的資料;當*Operation*為 SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK 時，它會從這個緩衝區抓取資料。 當*Operation*為 SQL_REFRESH 時， **SQLSetPos**會傳回此緩衝區中的資料;SQL_UPDATE*作業時，它會從*這個緩衝區中抓取資料。  
  
 如果*TargetValuePtr*是 null 指標，驅動程式會將資料行的資料緩衝區解除系結。 應用程式可以使用 SQL_UNBIND 選項呼叫**SQLFreeStmt** ，將所有資料行解除系結。 如果**SQLBindCol**呼叫中的*TargetValuePtr*引數為 Null 指標，但*StrLen_or_IndPtr*引數是有效的，則應用程式可以解除系結資料行的資料緩衝區，但仍具有系結至該資料行的長度/指標緩衝區。value.  
  
 *BufferLength*  
 源@No__t-0*TargetValuePtr*緩衝區的長度（以位元組為單位）。  
  
 驅動程式會使用*BufferLength*來避免在傳回可變長度的資料（例如字元或二進位資料）時，寫入超過 @no__t 1*TargetValuePtr*緩衝區的結尾。 請注意，驅動程式會在將字元資料傳回給 \**TargetValuePtr*時，計算 null 終止字元。 \* *TargetValuePtr*因此必須包含空格的 null 終止的字元或驅動程式將會截斷資料。  
  
 當驅動程式傳回固定長度的資料（例如整數或日期結構）時，驅動程式會忽略*BufferLength* ，並假設緩衝區夠大，足以容納資料。 因此，應用程式必須為固定長度的資料配置夠大的緩衝區，否則驅動程式將會寫入超過緩衝區的結尾。  
  
 當*BufferLength*小於0時， **SQLBINDCOL**會傳回 SQLSTATE HY090 （不正確字串或緩衝區長度），但當*BufferLength*為0時則不會傳回。 不過，如果*TargetType*指定了字元類型，應用程式就不應該將*BufferLength*設定為0，因為符合 ISO CLI 的驅動程式會在該情況下傳回 SQLSTATE HY090 （不正確字串或緩衝區長度）。  
  
 *StrLen_or_IndPtr*  
 [延遲的輸入/輸出]要系結至資料行之長度/指標緩衝區的指標。 **SQLFetch**和**SQLFetchScroll**會傳回這個緩衝區中的值。 當*Operation*為 SQL_ADD、SQL_UPDATE_BY_BOOKMARK 或 SQL_DELETE_BY_BOOKMARK 時， **SQLBulkOperations**會從這個緩衝區中抓取值。 當作業為 SQL_FETCH_BY_BOOKMARK*時，* **SQLBulkOperations**會傳回這個緩衝區中的值。 當*Operation*為 SQL_REFRESH 時， **SQLSetPos**會傳回此緩衝區中的值;當 SQL_UPDATE 作業時，*它會從*這個緩衝區中抓取值。  
  
 **SQLFetch**、 **SQLFetchScroll**、 **SQLBulkOperations**和**SQLSetPos**可以傳回長度/指標緩衝區中的下列值：  
  
-   可傳回的資料長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 應用程式可以將下列值放在長度/指標緩衝區中，以與**SQLBulkOperations**或**SQLSetPos**搭配使用：  
  
-   傳送的資料長度  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC 宏的結果  
  
-   SQL_COLUMN_IGNORE  
  
 如果指標緩衝區和長度緩衝區是個別的緩衝區，則指標緩衝區只能傳回 SQL_Null_DATA，而長度緩衝區則可以傳回所有其他值。  
  
 如需詳細資訊，請參閱[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)函式、 [SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)、 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)函式和[使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 如果*StrLen_or_IndPtr*為 null 指標，則不會使用長度或指示器值。 這是在提取資料且資料為 Null 時的錯誤。  
  
 如果您的應用程式將在64位作業系統上執行，請參閱[ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBindCol**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉**由呼叫 SQLGetDiagRec HandleType handletype 來**和*StatementHandle* *的* *控制碼*來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLBindCol**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  
  
|SQLSTATE|Error|說明|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|限制的資料類型屬性違規|（DM） *ColumnNumber*引數為0，而*TargetType*引數不是 SQL_C_BOOKMARK 或 SQL_C_VARBOOKMARK。|  
|07009|不正確描述項索引|為引數*ColumnNumber*指定的值超過結果集內的最大資料行數目。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 *MessageText\*緩衝區中的 **SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY003|不正確應用程式緩衝區類型|引數*TargetType*不是有效的資料類型，也不是 SQL_C_DEFAULT。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLBindCol**時，這個非同步函數仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY090|不正確字串或緩衝區長度|（DM）為引數*BufferLength*指定的值小於0。<br /><br /> （DM）驅動程式是 ODBC 2。*x*驅動程式， *ColumnNumber*引數設定為0，且為引數*BufferLength*指定的值不等於4。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援*TargetType*引數與對應資料行之驅動程式特定 SQL 資料類型的組合所指定的轉換。<br /><br /> 引數*ColumnNumber*為0，且驅動程式不支援書簽。<br /><br /> 此驅動程式僅支援 ODBC 2。*x*和引數*TargetType*為下列其中一項：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 以及附錄 D：中[c 資料類型](../../../odbc/reference/appendixes/c-data-types.md)所列的任何間隔 c 資料類型資料類型。<br /><br /> 驅動程式只支援3.50 之前的 ODBC 版本，並 SQL_C_GUID 引數*TargetType* 。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT 來設定。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解  
 **SQLBindCol**是用來將結果集中的*資料行與*應用程式中的資料緩衝區和長度/指標緩衝區建立關聯或系結。 當應用程式呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**來提取資料時，驅動程式會在指定的緩衝區中傳回系結資料行的資料。如需詳細資訊，請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。 當應用程式呼叫**SQLBulkOperations**來更新或插入資料列或**SQLSetPos**以更新資料列時，驅動程式會從指定的緩衝區抓取系結資料行的資料;如需詳細資訊，請參閱[SQLBulkOperations function](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos function](../../../odbc/reference/syntax/sqlsetpos-function.md)。 如需系結的詳細資訊，請參閱抓取[結果（基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 請注意，您不需要系結資料行來抓取它們的資料。 應用程式也可以呼叫**SQLGetData** ，以從資料行取得資料。 雖然可以系結資料列中的某些資料行，並為其他人呼叫**SQLGetData** ，但這會受到一些限制。 如需詳細資訊，請參閱[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>系結、解除系結和重新系結資料行  
 資料行可以隨時系結、解除系結或重新系結，即使已從結果集提取資料之後也一樣。 新的系結會在下一次呼叫使用系結的函式時生效。 例如，假設應用程式系結結果集中的資料行，並呼叫**SQLFetch**。 驅動程式會傳回系結緩衝區中的資料。 現在，假設應用程式將資料行系結至不同的緩衝區集。 驅動程式不會在新系結的緩衝區中，將剛提取之資料列的資料放入。 相反地，它會等到再次呼叫**SQLFetch** ，然後將資料放在新系結緩衝區中的下一個資料列。  
  
> [!NOTE]  
>  在將資料行系結至資料行0之前，一定要先設定語句屬性 SQL_ATTR_USE_BOOKMARKS。 這不是必要的，但強烈建議使用。  
  
## <a name="binding-columns"></a>繫結資料行  
 若要系結資料行，應用程式會呼叫**SQLBindCol** ，並傳遞資料緩衝區的資料行編號、類型、位址和長度，以及長度/指標緩衝區的位址。 如需如何使用這些位址的詳細資訊，請參閱本節稍後的「緩衝區位址」。 如需系結資料行的詳細資訊，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 這些緩衝區的使用會延遲;也就是說，應用程式會將它們系結至**SQLBindCol** ，但驅動程式會從其他函式（也就是**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**）進行存取。 只要系結仍然有效，應用程式就必須負責確保在**SQLBindCol**中指定的指標仍然有效。 如果應用程式允許這些指標變成無效-例如，它會釋出緩衝區，然後呼叫預期它們有效的函式，則會產生未定義的結果。 如需詳細資訊，請參閱[延遲的緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 系結會持續有效，直到被新的系結取代、資料行未系結或語句釋放為止。  
  
## <a name="unbinding-columns"></a>解除系結資料行  
 若要解除系結單一資料行，應用程式會呼叫**SQLBindCol** ，並將*ColumnNumber*設定為該資料行的數目，並將*TargetValuePtr*設定為 null 指標。 如果*ColumnNumber*參考未系結的資料行， **SQLBindCol**仍會傳回 SQL_SUCCESS。  
  
 若要將所有資料行解除系結，應用程式會呼叫**SQLFreeStmt** ，並將*FOPTION*設定為 SQL_UNBIND。 您也可以將 ARD 的 SQL_DESC_COUNT 欄位設定為零來完成這項作業。  
  
## <a name="rebinding-columns"></a>重新系結資料行  
 應用程式可以執行兩項作業之一來變更系結：  
  
-   呼叫**SQLBindCol** ，為已經系結的資料行指定新的系結。 驅動程式會以新的系結覆寫舊的系結。  
  
-   指定要加入至**SQLBindCol**的系結呼叫所指定的緩衝區位址位移。 如需詳細資訊，請參閱下一節「系結位移」。  
  
## <a name="binding-offsets"></a>系結位移  
 系結位移是一個值，會加入至資料和長度/指標緩衝區的位址（如*TargetValuePtr*和*StrLen_or_IndPtr*引數中所指定），然後再進行取值。 使用位移時，系結會是應用程式緩衝區配置方式的「範本」，而應用程式可以藉由變更位移，將此「範本」移至不同的記憶體區域。 因為每個系結中的每個位址都會加入相同的位移，所以不同資料行的緩衝區之間的相對位移在每一組緩衝區內必須相同。 使用資料列取向的系結時，一定會發生這種情況;使用資料行取向的系結時，應用程式必須仔細配置其緩衝區，使其成為 true。  
  
 使用系結位移基本上與透過呼叫**SQLBindCol**來重新系結資料行的效果相同。 差別在於新的**SQLBindCol**呼叫會指定資料緩衝區和長度/指標緩衝區的新位址，而使用系結位移並不會變更位址，而只會在其中加上位移。 應用程式可以在需要時指定新的位移，而且這個位移一律會加入至原始系結的位址。 特別是，如果 offset 設定為0，或如果語句屬性設為 null 指標，則驅動程式會使用原始系結的位址。  
  
 若要指定系結位移，應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用系結的函式之前，它會以位元組為單位將位移放在這個緩衝區中。 為了判斷要使用的緩衝區位址，驅動程式會將該位移新增至系結中的位址。 位址和位移的總和必須是有效的位址，但要新增位移的位址不一定有效。 如需如何使用系結位移的詳細資訊，請參閱本節稍後的「緩衝區位址」。  
  
## <a name="binding-arrays"></a>系結陣列  
 如果資料列集大小（SQL_ATTR_ROW_ARRAY_SIZE 語句屬性的值）大於1，則應用程式會系結緩衝區陣列，而不是單一緩衝區。 如需詳細資訊，請參閱[區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 應用程式可以透過兩種方式系結陣列：  
  
-   將陣列系結至每個資料行。 這稱為資料*行*取向系結，因為每個資料結構（陣列）都包含單一資料行的資料。  
  
-   定義結構來保存整個資料列的資料，並系結這些結構的陣列。 這稱為資料*列*取向的系結，因為每個資料結構都會包含單一資料列的資料。  
  
 每個緩衝區陣列的專案數必須至少與資料列集的大小相同。  
  
> [!NOTE]  
>  應用程式必須確認對齊方式是否有效。 如需對齊考慮的詳細資訊，請參閱[對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>資料行取向的繫結  
 在資料行取向的系結中，應用程式會將不同的資料和長度/指標陣列系結至每個資料行。  
  
 若要使用資料行取向的系結，應用程式會先將 SQL_ATTR_ROW_BIND_TYPE 語句屬性設定為 SQL_BIND_BY_COLUMN。 （這是預設值）。針對每個要系結的資料行，應用程式會執行下列步驟：  
  
1.  配置資料緩衝區陣列。  
  
2.  配置長度/指標緩衝區的陣列。  
  
    > [!NOTE]  
    >  當使用資料行取向的系結時，如果應用程式直接寫入至描述元，則可以將不同的陣列用於長度和指標資料。  
  
3.  使用下列引數呼叫**SQLBindCol** ：  
  
    -   *TargetType*是資料緩衝區陣列中單一元素的類型。  
  
    -   *TargetValuePtr*是資料緩衝區陣列的位址。  
  
    -   *BufferLength*是資料緩衝區陣列中單一元素的大小。 當資料為固定長度的資料時，會忽略*BufferLength*引數。  
  
    -   *StrLen_or_IndPtr*是長度/指標陣列的位址。  
  
 如需有關如何使用這項資訊的詳細資訊，請參閱本節稍後的「緩衝區位址」。 如需有關資料行取向系結的詳細資訊，請參閱資料[行](../../../odbc/reference/develop-app/column-wise-binding.md)取向系結。  
  
## <a name="row-wise-binding"></a>資料列取向的繫結  
 在資料列取向的系結中，應用程式會定義一個結構，其中包含要系結之每個資料行的資料和長度/指標緩衝區。  
  
 若要使用資料列取向的系結，應用程式會執行下列步驟：  
  
1.  定義結構來保存單一資料列（包括資料和長度/指標緩衝區），並配置這些結構的陣列。  
  
    > [!NOTE]  
    >  如果使用資料列取向的系結時，應用程式會直接寫入至描述元，則可以將不同的欄位用於長度和指標資料。  
  
2.  將 SQL_ATTR_ROW_BIND_TYPE 語句屬性設定為包含單一資料列的結構大小，或將結果資料行系結至之緩衝區實例的大小。 長度必須包含所有系結資料行的空間，以及結構或緩衝區的任何填補，以確保當系結的資料行位址以指定的長度遞增時，結果會指向下一個資料列中相同資料行的開頭。 在 ANSI C 中使用*sizeof*運算子時，會保證此行為。  
  
3.  針對每個要系結的資料行，呼叫具有下列引數的**SQLBindCol** ：  
  
    -   *TargetType*是要系結至資料行之資料緩衝區成員的類型。  
  
    -   *TargetValuePtr*是第一個陣列元素中資料緩衝區成員的位址。  
  
    -   *BufferLength*是資料緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是要系結之長度/指標成員的位址。  
  
 如需有關如何使用這項資訊的詳細資訊，請參閱本節稍後的「緩衝區位址」。 如需有關資料[行](../../../odbc/reference/develop-app/row-wise-binding.md)取向系結的詳細資訊，請參閱資料列取向系結。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 *緩衝區位址*是資料或長度/指標緩衝區的實際位址。 驅動程式會在寫入緩衝區（例如提取時間）之前，先計算緩衝區位址。 其計算方式為下列公式，其使用*TargetValuePtr*和*StrLen_or_IndPtr*引數中指定的位址、系結位移和資料列編號：  
  
 系結*位址* +  系結*位移*+ （（資料*列數*-1） x*元素大小*）  
  
 公式的變數定義如下表中所述。  
  
|變數|描述|  
|--------------|-----------------|  
|*系結位址*|針對資料緩衝區，在**SQLBindCol**中使用*TargetValuePtr*引數指定的位址。<br /><br /> 對於長度/指標緩衝區，使用**SQLBindCol**中的*StrLen_or_IndPtr*引數指定的位址。 如需詳細資訊，請參閱「描述元和 SQLBindCol」一節中的「其他留言」。<br /><br /> 如果系結的位址為0，則不會傳回任何資料值，即使前一個公式所計算的位址不是零也一樣。|  
|*系結位移*|如果使用資料列取向的系結，則儲存在使用 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性指定之位址的值。<br /><br /> 如果使用資料行取向的系結，或 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性的值為 null 指標，則系結*位移*為0。|  
|*資料列編號*|資料列集中以1為基礎的資料列編號。 如果是預設的單一資料列提取，這就是1。|  
|*元素大小*|系結陣列中元素的大小。<br /><br /> 如果使用資料行取向的系結，這就是長度/指標緩衝區的**sizeof （SQLINTEGER）** 。 對於資料緩衝區，如果資料類型是可變長度，則為**SQLBindCol**中*BufferLength*引數的值，如果資料類型是固定長度，則為資料類型的大小。<br /><br /> 如果使用資料列取向的系結，這就是資料和長度/指標緩衝區的 SQL_ATTR_ROW_BIND_TYPE 語句屬性值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>描述項和 SQLBindCol  
 下列各節說明**SQLBindCol**如何與描述項互動。  
  
> [!CAUTION]  
>  呼叫一個語句的**SQLBindCol**可能會影響其他語句。 當與語句相關聯的 ARD 已明確配置，而且也與其他語句相關聯時，就會發生這種情況。 由於**SQLBindCol**會修改描述項，因此修改會套用到與此描述項相關聯的所有語句。 如果這不是必要的行為，應用程式應該在呼叫**SQLBindCol**之前，將此描述元與其他語句中斷關聯。  
  
## <a name="argument-mappings"></a>引數對應  
 就概念而言， **SQLBindCol**會依序執行下列步驟：  
  
1.  呼叫**SQLGetStmtAttr**以取得 ARD 控制碼。  
  
2.  呼叫**SQLGetDescField**以取得此描述項的 SQL_DESC_COUNT 欄位，如果*ColumnNumber*引數中的值超過 SQL_DESC_COUNT 的值，則會呼叫**SQLSetDescField** ，以將 SQL_DESC_COUNT 的值增加到*ColumnNumber*。  
  
3.  多次呼叫**SQLSetDescField** ，以將值指派給 ARD 的下欄欄位：  
  
    -   將 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定為*TargetType*的值，不同之處在于如果*TargetType*是 datetime 或 interval 子類型的其中一個精簡識別碼，它會分別將 SQL_DESC_TYPE 設定為 SQL_DATETIME 或 SQL_INTERVAL。將 SQL_DESC_CONCISE_TYPE 設定為簡潔識別碼;和會將 SQL_DESC_DATETIME_INTERVAL_CODE 設定為對應的 DATETIME 或 INTERVAL 子代碼。  
  
    -   設定一或多個 SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，適用于*TargetType*。  
  
    -   將 SQL_DESC_OCTET_LENGTH 欄位設定為*BufferLength*的值。  
  
    -   將 SQL_DESC_DATA_PTR 欄位設定為*TargetValue*的值。  
  
    -   將 SQL_DESC_INDICATOR_PTR 欄位設定為*StrLen_or_Ind*的值。 （請參閱下列段落）。  
  
    -   將 SQL_DESC_OCTET_LENGTH_PTR 欄位設定為*StrLen_or_Ind*的值。 （請參閱下列段落）。  
  
 *StrLen_or_Ind*引數所參考的變數會用於指標和長度資訊。 如果提取遇到資料行的 null 值，它會將 SQL_Null_DATA 儲存在此變數中。否則，它會將資料長度儲存在此變數中。 傳遞 null 指標做為*StrLen_or_Ind*會讓提取作業不會傳回資料長度，但如果遇到 null 值且沒有任何方法可傳回 SQL_Null_DATA，則會使提取失敗。  
  
 如果**SQLBindCol**的呼叫失敗，則會在 ARD 中設定的描述項欄位內容未定義，而且 ARD 的 SQL_DESC_COUNT 欄位值不會變更。  
  
## <a name="implicit-resetting-of-count-field"></a>[計數] 欄位的隱含重設  
 只有當這會增加 SQL_DESC_COUNT 的值時， **SQLBindCol**才會將 SQL_DESC_COUNT 設定為*ColumnNumber*引數的值。 如果*TargetValuePtr*引數中的值是 null 指標，且*ColumnNumber*引數中的值等於 SQL_DESC_COUNT （也就是在解除系結最大的系結資料行時），則 SQL_DESC_COUNT 會設為最高值的數位剩餘的系結資料行。  
  
## <a name="cautions-regarding-sql_default"></a>關於 SQL_DEFAULT 的注意事項  
 若要成功地抓取資料行資料，應用程式必須正確地判斷應用程式緩衝區中資料的長度和開始點。 當應用程式指定明確的*TargetType*時，可以輕鬆地偵測應用程式誤解。 不過，當應用程式指定 SQL_DEFAULT 的*TargetType*時， **SQLBindCol**可以從應用程式所使用的資料行（從變更到中繼資料，或將程式碼套用至不同的）套用至不同的資料類型。排. 在此情況下，應用程式可能不一定會決定已提取之資料行資料的開始或長度。 這可能會導致未報告的資料錯誤或記憶體違規。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會在 Customers 資料表上執行**SELECT**語句，以傳回客戶識別碼、名稱和電話號碼的結果集（依名稱排序）。 然後它會呼叫**SQLBindCol** ，以將資料行系結至本機緩衝區。 最後，應用程式會使用**SQLFetch**提取每個資料列，並列印每個客戶的名稱、識別碼和電話號碼。  
  
 如需更多程式碼範例，請參閱[SQLBulkOperations function](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLColumns Function](../../../odbc/reference/syntax/sqlcolumns-function.md)、 [SQLFetchScroll function](../../../odbc/reference/syntax/sqlfetchscroll-function.md)和[SQLSetPos function](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
```cpp  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
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
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
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
  
 另請參閱[範例 ODBC 程式](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|傳回結果集中資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取資料區塊或透過結果集進行滾動|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|提取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|釋放語句上的資料行緩衝區|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|正在提取部分或所有資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集資料行的數目|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
