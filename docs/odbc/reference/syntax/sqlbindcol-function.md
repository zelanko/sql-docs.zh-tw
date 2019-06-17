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
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17b907be3e2641fe1dcbbb8fbd96586132e054ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538068"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLBindCol**繫結至結果集資料行的應用程式資料緩衝區。  
  
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
 [輸入]陳述式控制代碼。  
  
 *ColumnNumber*  
 [輸入]結果數目設定繫結的資料行。 資料行的編號 0 開始，資料行 0 的書籤資料行的遞增資料行順序。 如果書籤不會使用-SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_OFF-也就是資料行數字開始 1。  
  
 *TargetType*  
 [輸入]C 資料類型的識別項\* *TargetValuePtr*緩衝區。 當它與資料來源擷取資料**SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，或**SQLSetPos**，驅動程式會將資料轉換成此型別;當傳送資料到資料來源**SQLBulkOperations**或是**SQLSetPos**，驅動程式會將資料轉換從這個型別。 如需有效的 C 資料類型和類型識別碼的清單，請參閱 < [C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)節附錄 d:資料類型。  
  
 如果*TargetType*引數是 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 的欄位中所設定的間隔資料類型，則預設間隔開頭有效位數 (2) 和預設的間隔秒數有效位數 (6)，ARD，分別用於資料。 如果*TargetType*引數是 SQL_C_NUMERIC，（驅動程式定義） 的預設有效位數和預設 ARD SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定的小數位數 (0)，、 所用的資料。 應用程式如果任何預設有效位數或小數位數不適用，應該明確設定適當的描述項欄位呼叫**SQLSetDescField**或是**SQLSetDescRec**。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱 < [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *TargetValuePtr*  
 [延遲的輸入/輸出]要繫結至資料行的資料緩衝區的指標。 **SQLFetch**並**SQLFetchScroll**這個緩衝區中傳回的資料。 **SQLBulkOperations**中傳回的資料緩衝區時*作業*是 SQL_FETCH_BY_BOOKMARK; 它會從這個擷取的資料緩衝區時*作業*SQL_ADD 或 SQL_UPDATE_BY_BOOKMARK。 **SQLSetPos**中傳回的資料緩衝區時*作業*是 SQL_REFRESH; 它會從這個擷取的資料緩衝區時*作業*是 SQL_UPDATE。  
  
 如果*TargetValuePtr*為 null 指標，此驅動程式會解除繫結資料行的資料緩衝區。 應用程式可以解除繫結所有資料行藉由呼叫**SQLFreeStmt**使用 SQL_UNBIND 選項。 應用程式可以解除繫結資料行的資料緩衝區，但仍有繫結資料行的長度/指標緩衝區，如果*TargetValuePtr*呼叫中的引數**SQLBindCol**為 null 指標，但*StrLen_or_IndPtr*引數是有效的值。  
  
 *BufferLength*  
 [輸入]長度 **TargetValuePtr*以位元組為單位的緩衝區。  
  
 驅動程式會使用*Columnsize*若要避免寫入結尾\* *TargetValuePtr*緩衝時它會傳回可變長度的資料，例如字元或二進位資料。 請注意，驅動程式會計算之 null 結束字元，傳回字元資料時\* *TargetValuePtr*。 **TargetValuePtr*因此必須包含空格的 null 終止的字元或驅動程式將會截斷資料。  
  
 驅動程式會傳回固定長度的資料，例如整數或日期結構，此驅動程式會忽略*Columnsize* ，並假設緩衝區是否夠大，無法保存資料。 因此，務必為固定長度的資料配置夠大的緩衝區應用程式或驅動程式會寫入超過緩衝區結尾。  
  
 **SQLBindCol**會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度） 時*Columnsize*是小於 0，但不是會在*Columnsize*為 0。 不過，如果*TargetType*指定字元類型，不應將應用程式*Columnsize*為 0，因為 ISO CLI 相容的驅動程式會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度），大小寫。  
  
 *StrLen_or_IndPtr*  
 [延遲的輸入/輸出]繫結至資料行的長度/指標緩衝區的指標。 **SQLFetch**並**SQLFetchScroll**傳回值，這個緩衝區中。 **SQLBulkOperations**擷取的值從這個緩衝區的時機*作業*SQL_ADD、 SQL_UPDATE_BY_BOOKMARK，或 SQL_DELETE_BY_BOOKMARK。 **SQLBulkOperations**傳回值，在此緩衝區的時機*作業*是 SQL_FETCH_BY_BOOKMARK。 **SQLSetPos**傳回值，在此緩衝區的時機*作業*是 SQL_REFRESH; 它擷取某個值，這個緩衝區時*作業*是 SQL_UPDATE。  
  
 **SQLFetch**， **SQLFetchScroll**， **SQLBulkOperations**，和**SQLSetPos**可以傳回長度/指標緩衝區中的下列值：  
  
-   可用來傳回資料的長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 應用程式可以將下列值放在搭配使用的長度/指標緩衝區**SQLBulkOperations**或是**SQLSetPos**:  
  
-   正在傳送資料的長度  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   結果的 SQL_LEN_DATA_AT_EXEC 巨集  
  
-   SQL_COLUMN_IGNORE  
  
 如果指標緩衝區和長度的緩衝區都是個別的緩衝區，指標緩衝區可以傳回只 SQL_NULL_DATA，而長度的緩衝區可能會傳回所有其他值。  
  
 如需詳細資訊，請參閱 < [SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)， [SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)，和[使用的長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 如果*StrLen_or_IndPtr*是使用 null 指標，沒有長度或指標值。 正在擷取資料和資料為 NULL 時，這會是錯誤。  
  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式會在 64 位元作業系統上執行。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBindCol**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLBindCol** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|(DM) *ColumnNumber*引數為 0，而*TargetType*引數不是 SQL_C_BOOKMARK 或 SQL_C_VARBOOKMARK。|  
|07009|描述項索引無效|指定的引數的值*ColumnNumber*超過結果集資料行的數目上限。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY003|無效的應用程式緩衝區類型|引數*TargetType*不是有效的資料類型或 SQL_C_DEFAULT。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLBindCol**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數指定的值*Columnsize*為小於 0。<br /><br /> (DM) 驅動程式的 ODBC 2。*x*驅動程式*ColumnNumber*引數設定為 0，並指定引數的值*Columnsize*不是等於 4。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援指定的組合來轉換*TargetType*引數和驅動程式特有的 SQL 資料類型，對應資料行。<br /><br /> 引數*ColumnNumber*為 0，且驅動程式不支援書籤。<br /><br /> 此驅動程式支援只有 ODBC 2。*x*和引數*TargetType*是下列其中之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 任何間隔 C 資料類型會列在[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d:資料類型。<br /><br /> 此驅動程式只支援之前 3.50 元，並將引數的 ODBC 版本*TargetType*已 SQL_C_GUID。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 **SQLBindCol**用來建立關聯，或*繫結，* 結果中的資料行設定為資料緩衝區和應用程式中的長度/指標緩衝區。 當應用程式呼叫**SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**來提取資料，驅動程式傳回的資料繫結的資料行中指定的緩衝區詳細資訊，請參閱[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)。 當應用程式呼叫**SQLBulkOperations**若要更新或插入資料列或**SQLSetPos**更新的資料列，驅動程式會擷取資料繫結的資料行，從指定的緩衝區; 如需詳細資訊請參閱[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或是[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md)。 如需有關繫結的詳細資訊，請參閱 <<c0> [ 擷取結果 （基本）](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 請注意，資料行並沒有繫結至從中擷取資料。 應用程式也可以呼叫**SQLGetData**來擷取資料行中的資料。 雖然您可以在資料列，並呼叫某些資料行繫結**SQLGetData**供其他人，這是受到一些限制。 如需詳細資訊，請參閱 < [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>繫結、 解除繫結，以及重新繫結資料行  
 資料行可以繫結、 解除繫結，或在任何時間，即使已經提取從結果集中的資料之後，才會重新繫結。 新的繫結會使用繫結的函式會呼叫在下一次的生效。 例如，假設應用程式繫結結果集與呼叫中的資料行**SQLFetch**。 驅動程式傳回的資料繫結的緩衝區中。 現在，假設應用程式繫結到一組不同的緩衝區資料行。 驅動程式不會將剛剛擷取的資料列的資料放在新的繫結的緩衝區。 相反地，它會等候直到**SQLFetch**稱為一次，然後將下一個資料列的資料放在新的繫結的緩衝區。  
  
> [!NOTE]  
>  陳述式屬性 SQL_ATTR_USE_BOOKMARKS 一律應該繫結至資料行 0 之前設定。 這並非必要，但強烈建議。  
  
## <a name="binding-columns"></a>繫結資料行  
 要繫結資料行，應用程式會呼叫**SQLBindCol**並傳遞資料行數目、 類型、 位址，以及資料緩衝區的長度和長度/指標緩衝區的位址。 如需如何使用這些位址的資訊，請參閱本節稍後的 「 緩衝區位址 」。 如需有關繫結資料行的詳細資訊，請參閱[使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 使用這些緩衝區會延後;也就是應用程式繫結中加以**SQLBindCol**驅動程式存取它們的其他函式-也就是，但**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**。 應用程式必須負責確定中指定的指標**SQLBindCol**保持有效，只要繫結會持續有效。 如果應用程式可讓這些指標變成無效-例如，釋放緩衝區-，而接著會呼叫必須是有效的函式，結果會是未定義。 如需詳細資訊，請參閱 <<c0> [ 延後的緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 繫結會持續有效，直到它被新的繫結、 資料行解除繫結時，或釋放陳述式。  
  
## <a name="unbinding-columns"></a>正在解除繫結的資料行  
 若要解除繫結的單一資料行，應用程式會呼叫**SQLBindCol**與*ColumnNumber*設為該資料行數目和*TargetValuePtr*設為 null 指標。 如果*ColumnNumber*繫結的資料行，是指**SQLBindCol**仍會傳回 SQL_SUCCESS。  
  
 若要解除繫結所有資料行，應用程式會呼叫**SQLFreeStmt**具有*fOption*設定為 SQL_UNBIND。 這也可以透過設定為零 ARD SQL_DESC_COUNT 欄位。  
  
## <a name="rebinding-columns"></a>重新繫結資料行  
 應用程式可以執行下列其中一個來變更繫結的兩個作業：  
  
-   呼叫**SQLBindCol**來指定新的繫結已繫結的資料行。 驅動程式會以新的覆寫舊的繫結。  
  
-   指定要加入至繫結呼叫所指定的緩衝區位址的位移**SQLBindCol**。 如需詳細資訊，請參閱下一步 區段中，「 繫結位移 」。  
  
## <a name="binding-offsets"></a>繫結位移  
 繫結位移是一個值，會加入至資料和長度/指標緩衝區的位址 (中所指定*TargetValuePtr*並*StrLen_or_IndPtr*引數) 他們已取值之前。 當使用位移時，繫結的 「 範本 」 的應用程式的緩衝區的配置方式，而且應用程式可以藉由變更位移到不同區域的記憶體中移動這個 「 範本 」。 因為相同的位移會加入至每個繫結中的每個位址，不同的資料行緩衝區之間的相對位移必須每一個集合的緩衝區中相同。 這一定是 true 時使用資料列取向的繫結;應用程式必須仔細配置其緩衝區，這個值是 true，資料行取向的繫結時使用。  
  
 使用繫結位移效果基本上相同呼叫，資料行重新繫結**SQLBindCol**。 其差異在於，新的呼叫來**SQLBindCol**指定新的資料緩衝區和長度/指標緩衝區的位址，而不會變更位址使用繫結的位移，但只是將它們加上位移。 只要想的話，並將此位移一律加入原始繫結位址，應用程式可以指定新的位移。 特別的是，如果位移設定為 0，或陳述式屬性設為 null 指標，驅動程式會使用原本的繫結的位址。  
  
 若要指定繫結位移，應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性設定為 SQLINTEGER 緩衝區的位址。 應用程式會呼叫使用繫結的函式之前，它會使得這個緩衝區中的位元組位移。 若要判斷要使用之緩衝區的位址，驅動程式會將位移加入至繫結中的位址。 位址和位移的總和必須是有效的地址，但加入位移的位址不需要是有效的。 如需如何使用繫結位移的詳細資訊，請參閱本節稍後的 「 緩衝區位址 」。  
  
## <a name="binding-arrays"></a>繫結陣列  
 如果大於 1 的資料列集大小 （SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性的值），應用程式繫結緩衝區，而非單一的緩衝區的陣列。 如需詳細資訊，請參閱 <<c0> [ 區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 應用程式可以將陣列繫結有兩種：  
  
-   將陣列繫結至每個資料行。 這指*資料行取向的繫結*因為每個資料結構 （陣列） 包含單一資料行的資料。  
  
-   定義的結構來保存整個資料列的資料，並將這些結構的陣列繫結。 這指*資料列取向的繫結*因為每個資料結構包含單一資料列的資料。  
  
 每一個緩衝區陣列做為資料列集大小必須至少為許多項目。  
  
> [!NOTE]  
>  應用程式必須確認對齊有效。 如需對齊考量的詳細資訊，請參閱 <<c0> [ 對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>資料行取向的繫結  
 在 資料行取向的繫結，應用程式繫結不同的資料和長度/指標陣列至每個資料行。  
  
 若要使用資料行取向的繫結，應用程式第一次為 SQL_BIND_BY_COLUMN 設定 SQL_ATTR_ROW_BIND_TYPE 陳述式屬性。 （這是預設值）。每個資料行繫結，應用程式會執行下列步驟：  
  
1.  配置資料緩衝區陣列。  
  
2.  配置陣列的長度/指標緩衝區。  
  
    > [!NOTE]  
    >  如果應用程式時直接寫入描述項會使用資料行取向的繫結，可以使用個別的陣列，長度與指標資料。  
  
3.  呼叫**SQLBindCol**的下列引數：  
  
    -   *TargetType*資料緩衝區陣列中的單一元素的類型。  
  
    -   *TargetValuePtr*是資料緩衝區陣列的位址。  
  
    -   *BufferLength*是資料緩衝區陣列中的單一元素的大小。 *Columnsize*有固定長度資料的資料時，會忽略引數。  
  
    -   *StrLen_or_IndPtr*是長度/指標陣列的位址。  
  
 如需如何使用這項資訊的詳細資訊，請參閱本節稍後的 「 緩衝區位址 」。 如需有關資料行取向的繫結的詳細資訊，請參閱 <<c0> [ 資料行取向的繫結](../../../odbc/reference/develop-app/column-wise-binding.md)。  
  
## <a name="row-wise-binding"></a>資料列取向的繫結  
 在資料列取向的繫結，應用程式會定義結構，其中包含每個資料行繫結的資料和長度/指標緩衝區。  
  
 若要使用資料列取向的繫結，應用程式會執行下列步驟：  
  
1.  定義結構，以容納單一資料列的資料 （包括資料和長度/指標緩衝區），並配置這些結構的陣列。  
  
    > [!NOTE]  
    >  如果應用程式時直接寫入描述項會使用資料列取向的繫結，個別的欄位可以用於長度和指標的資料。  
  
2.  結構，其中包含單一資料列的大小，或執行個體，其中會繫結的結果資料行緩衝區的大小，請設定 SQL_ATTR_ROW_BIND_TYPE 陳述式屬性。 長度必須包含所有繫結的資料行，以及結構或緩衝區，藉此確定，當繫結的資料行的位址會隨著指定的長度，結果會指向相同的資料行中的下一個資料列開頭的任何填補的空間。 使用時*sizeof* ANSI C 中的運算子，保證此行為。  
  
3.  呼叫**SQLBindCol**每個資料行繫結的下列引數：  
  
    -   *TargetType*是繫結至資料行的資料緩衝區成員的型別。  
  
    -   *TargetValuePtr*是緩衝區中資料成員的第一個陣列元素的位址。  
  
    -   *BufferLength*是資料緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是繫結之長度/指標成員的位址。  
  
 如需如何使用這項資訊的詳細資訊，請參閱本節稍後的 「 緩衝區位址 」。 如需有關資料行取向的繫結的詳細資訊，請參閱 <<c0> [ 資料列取向的繫結](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 *緩衝區位址*是實際的資料或長度/指標緩衝區的位址。 驅動程式會計算緩衝區位址之前它會寫入至緩衝區 （例如期間擷取時間）。 它會計算下列公式，它會使用指定的地址*TargetValuePtr*並*StrLen_or_IndPtr*引數、 繫結位移和資料列數目：  
  
 *繫結位址* + *繫結位移*+ ((*資料列編號*-1) x*項目大小*)  
  
 下表中所述，其中會定義公式的變數。  
  
|變數|描述|  
|--------------|-----------------|  
|*繫結位址*|使用指定的資料緩衝區的位址*TargetValuePtr*中的引數**SQLBindCol**。<br /><br /> 使用指定之長度/指標緩衝區的位址*StrLen_or_IndPtr*中的引數**SQLBindCol**。 如需詳細資訊，請參閱 」 描述元和 SQLBindCol 」 一節中的 [其他註解]。<br /><br /> 如果繫結的位址為 0，會傳回任何資料值，即使上述的公式計算出來的地址為非零值。|  
|*繫結位移*|如果使用資料列取向的繫結，在位址中儲存的值指定 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性。<br /><br /> 如果資料行取向的繫結，或 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性的值是 null 指標，*繫結位移*為 0。|  
|*資料列數目*|1 為基底的資料列集中的資料列數目。 針對單一資料列擷取，也就是預設值，這會是 1。|  
|*項目大小*|繫結的陣列中項目的大小。<br /><br /> 如果使用資料行取向的繫結，則**sizeof(SQLINTEGER)** 長度/指標緩衝區。 就資料緩衝區的值*Columnsize*中的引數**SQLBindCol**如果資料類型是可變長度，以及資料類型大小的資料類型為固定長度。<br /><br /> 如果使用資料列取向的繫結，這會是資料和長度/指標緩衝區的 SQL_ATTR_ROW_BIND_TYPE 陳述式屬性的值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>描述項和 SQLBindCol  
 下列各節說明如何**SQLBindCol**描述項進行互動。  
  
> [!CAUTION]  
>  呼叫**SQLBindCol**的一個陳述式可能會影響其他陳述式。 會發生這種情況是當陳述式相關聯 ARD 明確配置且同時與其他陳述式相關聯。 因為**SQLBindCol**修改描述元，所做的修改套用至與這個描述元相關聯的所有陳述式。 如果這不是所需的行為，應用程式應該中斷此描述元，從其他陳述式之前它會呼叫**SQLBindCol**。  
  
## <a name="argument-mappings"></a>引數對應  
 就概念而言， **SQLBindCol**序列中執行下列步驟：  
  
1.  呼叫**SQLGetStmtAttr**取得 ARD 控制代碼。  
  
2.  呼叫**SQLGetDescField**若要取得這個描述元 SQL_DESC_COUNT 欄位中，而且如果中的值*ColumnNumber* SQL_DESC_COUNT，呼叫的值的引數超過**SQLSetDescField**增加至 SQL_DESC_COUNT 值*ColumnNumber*。  
  
3.  呼叫**SQLSetDescField**多次，以便將值指派給 ARD 下列欄位：  
  
    -   設的值中的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE *TargetType*，但如果*TargetType*是其中一個的日期時間或間隔的子類型的精確識別碼，它會將 SQL_DESC_TYPE 設 SQL_日期時間或 SQL_INTERVAL，分別;設定 SQL_DESC_CONCISE_TYPE 簡潔的識別碼;然後設定 SQL_DESC_DATETIME_INTERVAL_CODE 相對應的日期時間或間隔子代碼。  
  
    -   設定一或多個 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，視*TargetType*。  
  
    -   值會設定 SQL_DESC_OCTET_LENGTH 欄位*Columnsize*。  
  
    -   設定 SQL_DESC_DATA_PTR 欄位的值*TargetValue*。  
  
    -   值會設定 SQL_DESC_INDICATOR_PTR 欄位*Strlen_or_ind&lt*。 （請參閱下列段落）。  
  
    -   值會設定 SQL_DESC_OCTET_LENGTH_PTR 欄位*Strlen_or_ind&lt*。 （請參閱下列段落）。  
  
 變數可*Strlen_or_ind&lt*引數會參考用於指標和長度的資訊。 如果提取發生的資料行的 null 值，它會在此變數中; 儲存 SQL_NULL_DATA否則，它會儲存的資料長度在此變數。 傳遞 null 做為指標*Strlen_or_ind&lt*會擷取作業傳回的資料長度，但會失敗，如果遇到 null 值，而且完全沒有辦法傳回 SQL_NULL_DATA 的提取。  
  
 如果在呼叫**SQLBindCol**會失敗，它會設定在 ARD 的描述項欄位的內容為未定義，而且 ARD SQL_DESC_COUNT 欄位的值不變。  
  
## <a name="implicit-resetting-of-count-field"></a>計數欄位的隱含重設  
 **SQLBindCol**的值設定 SQL_DESC_COUNT *ColumnNumber*引數，這會增加 SQL_DESC_COUNT 的值時，才。 如果中的值*TargetValuePtr*引數是 null 指標中的值*ColumnNumber*引數等於 SQL_DESC_COUNT （也就是當解除繫結的最上層繫結資料行），然後 SQL_DESC_計數設定為最高其餘的繫結資料行數目。  
  
## <a name="cautions-regarding-sqldefault"></a>關於 SQL_DEFAULT 的注意事項  
 若要成功擷取資料行的資料，應用程式必須判斷正確的長度和緩衝區中的資料應用程式的起始點。 當應用程式指定的明確*TargetType*，輕鬆地偵測到的應用程式的誤解。 不過，當應用程式指定*TargetType* SQL_DEFAULT 的**SQLBindCol**可以套用至不同的資料類型的資料行從一個的預定由應用程式，從變更中繼資料或將程式碼套用至不同的資料行。 在此情況下，應用程式可能不一定判斷啟動或已擷取的資料行資料的長度。 這可能會導致資料未回報的錯誤或記憶體違規。  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，執行應用程式**選取**依名稱排序傳回的結果集的客戶識別碼、 名稱和電話號碼之 Customers 資料表的陳述式。 然後它會呼叫**SQLBindCol**要繫結的本機緩衝區的資料行。 最後，應用程式會擷取資料的每個資料列**SQLFetch**並列印每個客戶的名稱、 識別碼和電話號碼。  
  
 如需更多的程式碼範例，請參閱 < [SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)， [SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)，和[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
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
  
 另請參閱[ODBC 程式範例](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|在結果集中傳回資料行的相關資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|釋放陳述式上的資料行緩衝區|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|正在擷取部分或全部的資料行|[SQLGetData 函式](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集資料行|[SQLNumResultCols 函式](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
