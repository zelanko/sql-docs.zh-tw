---
title: SQLBindCol 功能 |微軟文件
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
ms.openlocfilehash: 90bb1c1aa4dbfa2614f689faa47eb0c41a6cecd6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298738"
---
# <a name="sqlbindcol-function"></a>SQLBindCol 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLBindCol**將應用程序數據緩衝區綁定到結果集中的列。  
  
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
 *語句句柄*  
 [輸入]語句句柄。  
  
 *ColumnNumber*  
 [輸入]要綁定的結果集列的編號。 列按增加列順序編號,從 0 開始,其中列 0 是書籤列。 如果未使用書籤(即SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_OFF,則列編號從 1 開始。  
  
 *目標型態*  
 [輸入]\**目標ValuePtr*緩衝區的 C 資料類型的識別碼。 當它使用**SQLFetch、SQLFetchScroll、SQLBulk****操作**或**SQLSetPos**從數據源檢索數據時,驅動程式會將**SQLFetch**數據轉換為此類型;當它使用**SQLBulk 操作**或**SQLSetPos**將數據發送到數據源時,驅動程式將轉換此類型的數據。 有關有效的 C 資料類型和類型識別碼的清單,請參閱附錄 D:資料類型中的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)部分。  
  
 如果*TargetType*參數是間隔數據類型,則分別用於資料中的 SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 欄位中設置的預設間隔前導精度 (2) 和預設間隔秒精度 (6)。 如果*TargetType*參數SQL_C_NUMERIC,則數據將使用在 ARD 的SQL_DESC_PRECISION和SQL_DESC_SCALE欄位中設置的預設精度(驅動程式定義)和預設比例 (0)。 如果任何預設精度或比例不合適,應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**顯式設置相應的描述符欄位。  
  
 您還可以指定延伸的 C 資料類型。 關於詳細資訊,請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 *目標價值Ptr*  
 【 延遲輸入/輸出 】指向要綁定到列的數據緩衝區。 **SQLFetch**和**SQLFetchScroll**傳回此緩衝區中的數據。 當*操作*SQL_FETCH_BY_BOOKMARK時 **,SQLBulk 操作**傳回此緩衝區中的數據;當*操作*SQL_ADD或SQL_UPDATE_BY_BOOKMARK時,它會從該緩衝區檢索數據。 當*操作*SQL_REFRESH時 **,SQLSetPos**傳回此緩衝區中的數據;當*操作*SQL_UPDATE時,它將從該緩衝區檢索數據。  
  
 如果*TargetValuePtr*是空指標,則驅動程式將取消綁定列的數據緩衝區。 應用程式可以通過使用SQL_UNBIND選項調用**SQLFreeStmt**取消綁定所有列。 如果調用**SQLBindCol**中的*TargetValuePtr*參數是空指標,但*StrLen_or_IndPtr*參數是有效的值,則應用程式可以取消綁定列的數據緩衝區,但仍為列綁定長度/ 指示器緩衝區。  
  
 *緩衝區長度*  
 [輸入]以位元組為\*單位*的目標價值Ptr*緩衝區的長度。  
  
 當驅動程式返回可變長度數據(如字元或二進位資料)時,驅動程式使用*BufferLength*來避免\*寫入*TargetValuePtr*緩衝區的末尾。 請注意,當驅動程式將字元數據\*返回到*TargetValuePtr*時,驅動程式會計算 null 終止字元。 \*因此 *,TargetValuePtr*必須包含 null 終止字元的空間,否則驅動程式將截截數據。  
  
 當驅動程式返回固定長度數據(如整數或日期結構)時,驅動程式將忽略*BufferLength*並假定緩衝區足夠大以容納數據。 因此,應用程式為固定長度數據分配足夠大的緩衝區非常重要,否則驅動程式將寫入緩衝區的末尾。  
  
 當*緩衝區長度*小於 0,但當緩衝區長度為 0 時 **,SQLBindCol**返回 SQLSTATE HY090(無效字串或緩衝區長度),但當*緩衝區長度*為 0 時,則返回 SQLSTATE HY090(無效字串或緩衝區長度)。 但是,如果*TargetType*指定字元類型,則應用程式不應將*BufferLength*設置為 0,因為符合 ISO CLI 的驅動程式在這種情況下返回 SQLSTATE HY090(無效字串或緩衝區長度)。  
  
 *StrLen_or_IndPtr*  
 【 延遲輸入/輸出 】指向長度/指示器緩衝區以綁定到列。 **SQLFetch**和**SQLFetchScroll**傳回此緩衝區中的值。 當操作SQL_ADD、SQL_UPDATE_BY_BOOKMARK或SQL_DELETE_BY_BOOKMARK*操作*時 **,SQLBulk 操作**從該緩衝區檢索值。 **sqlBulk 操作**在操作*SQL_FETCH_BY_BOOKMARK時返回*此緩衝區中的值。 當*操作*SQL_REFRESH時 **,SQLSetPos**將傳回此緩衝區中的值;當*操作*SQL_UPDATE時,它將從該緩衝區檢索值。  
  
 **SQLFetch、SQLFetchScroll、SQLBulk****操作**和**SQLSetPos**可以在長度/ 指示器緩衝區**SQLFetch**中傳回以下值:  
  
-   可供傳回的資料的長度  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 應用程式可以將以下值放在長度/指示器緩衝區中,以便與**SQLBulk 操作**或**SQLSetPos**一起使用 :  
  
-   傳送的資料的長度  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   SQL_LEN_DATA_AT_EXEC宏的結果  
  
-   SQL_COLUMN_IGNORE  
  
 如果指標緩衝區和長度緩衝區是單獨的緩衝區,則指示器緩衝區只能返回SQL_NULL_DATA,而長度緩衝區可以返回所有其他值。  
  
 有關詳細資訊,請參閱[SQLBulk 操作函數](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)函數[、SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)函數[與使用長度/指標值](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)。  
  
 如果*StrLen_or_IndPtr*為空指標,則不使用長度或指標值。 這是提取數據時的錯誤,並且數據為 NULL。  
  
 如果應用程式將在 64 位元作業系統上執行,請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBindCol**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLBindCol**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|(DM)*列編號*參數為 0,*並且 TargetType*參數不SQL_C_BOOKMARK或SQL_C_VARBOOKMARK。|  
|07009|不合法的描述符索引|為參數*ColumnNumber*指定的值超過了結果集中的最大列數。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY003|不合法的應用程式緩衝區型態|參數*TargetType*既不是有效的資料類型,也不是SQL_C_DEFAULT。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLBindCol**時,此非同步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 為參數*BufferLength*指定的值小於 0。<br /><br /> (DM) 驅動程式是 ODBC 2。*x*驅動程式 *,ColumnNumber*參數設置為 0,並為參數*BufferLength*指定的值不等於 4。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或資料來源不支援*由 TargetType*參數和相應列的特定於驅動程式的 SQL 資料類型的組合指定的轉換。<br /><br /> 參數*列編號*為 0,驅動程式不支援書籤。<br /><br /> 驅動程式僅支援 ODBC 2。*x*與參數*TargetType*是以下原因之一:<br /><br /> SQL_C_NUMERICSQL_C_SBIGINTSQL_C_UBIGINT<br /><br /> 和附錄 D 中的[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)中列出的任何間隔 C 資料類型:資料類型。<br /><br /> 驅動程式僅支援 3.50 之前的 ODBC 版本,並且參數*TargetType* SQL_C_GUID。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解  
 **SQLBindCol**用於將結果集中的列關聯或*綁定*到應用程式中的數據緩衝區和長度/指示器緩衝區。 當應用程式呼叫**SQLFetch、SQLFetchScroll**或**SQLSetPos**來取得資料時,驅動程式將返回指定緩衝區中綁定列的資料;否則,驅動程式將返回指定緩衝區中**SQLFetchScroll**綁定列的數據。有關詳細資訊,請參閱[SQLFetch 函數](../../../odbc/reference/syntax/sqlfetch-function.md)。 當應用程式呼叫**SQLBulk 操作**以更新或插入行或**SQLSetPos**以更新行時,驅動程式將從指定的緩衝區檢索綁定列的數據;否則,驅動程式將檢索綁定列的數據。有關詳細資訊,請參閱[SQLBulk 操作函數](../../../odbc/reference/syntax/sqlbulkoperations-function.md)或[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。 有關繫結出詳細資訊,請參閱[檢索結果(基本)](../../../odbc/reference/develop-app/retrieving-results-basic.md)。  
  
 請注意,列不必綁定來從它們檢索數據。 應用程式還可以調用**SQLGetData**從列檢索數據。 儘管可以綁定行中的某些列併為其他列調用**SQLGetData,** 但受一些限制。 有關詳細資訊,請參閱[SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)。  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>繫結、取消繫結和重新繫結欄  
 即使從結果集中獲取數據,也可以在任何時候綁定、取消綁定或反彈。 下次調用使用綁定的函數時,新綁定將生效。 例如,假設應用程式將列綁定到結果集中並呼叫**SQLFetch**。 驅動程式返回綁定緩衝區中的數據。 現在假設應用程式將列綁定到一組不同的緩衝區。 驅動程式不會在新綁定的緩衝區中放置剛提取的行的數據。 相反,它會等待,直到再次調用**SQLFetch,** 然後將下一行的數據放在新綁定的緩衝區中。  
  
> [!NOTE]  
>  語句屬性SQL_ATTR_USE_BOOKMARKS應始終在將列綁定到列 0 之前進行設置。 這不是必需的,但強烈建議這樣做。  
  
## <a name="binding-columns"></a>繫結資料行  
 要綁定列,應用程式調用**SQLBindCol**並傳遞數據緩衝區的列號、類型、位址和長度以及長度/指示器緩衝區的位址。 有關如何使用這些位址的資訊,請參閱本節後面的"緩衝區位址"。 有關繫結列的詳細資訊,請參閱使用[SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)。  
  
 推遲使用這些緩衝區;也就是說,應用程式在**SQLBindCol**中綁定它們,但驅動程式從其他函數(即**SQLBulk 操作****、SQLFetch、SQLFetchScroll**或**SQLSetPos)** 訪問它們。 **SQLFetchScroll** 應用程式有責任確保**SQLBindCol**中指定的指標保持有效,只要綁定仍然有效。 如果應用程式允許這些指標無效(例如,它釋放緩衝區),然後調用期望它們有效的函數,則後果未定義。 有關詳細資訊,請參閱[延遲緩衝區](../../../odbc/reference/develop-app/deferred-buffers.md)。  
  
 綁定仍然有效,直到它被新的綁定替換,列未綁定,或釋放語句。  
  
## <a name="unbinding-columns"></a>取消繫結欄  
 要取消綁定單個列,應用程式調用**SQLBindCol,***其中列號*設置為該列的編號,而*TargetValuePtr*設置為空指標。 如果*列編號*引用未綁定列 **,SQLBindCol**仍返回SQL_SUCCESS。  
  
 要取消綁定所有列,應用程式將**SQLFreeStmt**調用 *,fOption*設置為SQL_UNBIND。 這也可以通過將ARD的SQL_DESC_COUNT欄位設置為零來實現。  
  
## <a name="rebinding-columns"></a>重新繫結欄  
 應用程式可以執行兩個操作中的任何一個來更改繫結:  
  
-   調用**SQLBindCol**為已綁定的列指定新綁定。 驅動程式用新綁定覆蓋舊綁定。  
  
-   指定要添加到由綁定調用**SQLBindCol**指定的緩衝區位址的偏移量。 有關詳細資訊,請參閱下一節"綁定偏移量"。  
  
## <a name="binding-offsets"></a>繫結位移  
 綁定偏移量是在取消引用之前添加到資料和長度/指標緩衝區的位址(如*TargetValuePtr*和*StrLen_or_IndPtr*參數中指定的值。 使用偏移時,綁定是應用程式緩衝區佈局方式的"範本",應用程式可以通過更改偏移量將此"範本"移動到不同的記憶體區域。 由於相同的偏移量添加到每個綁定中的每個位址,因此不同列的緩衝區之間的相對偏移量必須與每組緩衝區中的相對偏移量相同。 使用按行綁定時,始終如此;應用程式必須仔細佈局其緩衝區,這樣在使用按列綁定時為 true。  
  
 使用綁定偏移量與通過調用**SQLBindCol**重新綁定列的效果基本相同。 區別在於,對**SQLBindCol**的新調用指定數據緩衝區和長度/指示器緩衝區的新位址,而使用綁定偏移量不會更改位址,而只會向位址添加偏移量。 應用程式可以隨時指定新的偏移量,並且此偏移量始終添加到最初綁定的位址。 特別是,如果偏移量設置為 0,或者如果語句屬性設置為空指標,則驅動程式將使用最初綁定的位址。  
  
 要指定綁定偏移量,應用程式將SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性設置到 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用綁定的函數之前,它會在此緩衝區中放置一個偏移量。 要確定要使用的緩衝區的位址,驅動程式將偏移量添加到綁定中的位址。 位址和偏移量的總和必須是有效位址,但向其添加偏移量的位址不必有效。 有關如何使用綁定偏移量的詳細資訊,請參閱本節後面的"緩衝區位址"。  
  
## <a name="binding-arrays"></a>繫結陣列  
 如果行集大小(SQL_ATTR_ROW_ARRAY_SIZE語句屬性的值)大於 1,則應用程式將綁定緩衝區的陣列而不是單個緩衝區。 有關詳細資訊,請參閱[區塊游標](../../../odbc/reference/develop-app/block-cursors.md)。  
  
 應用程式可以通過兩種方式綁定陣列:  
  
-   將陣列綁定到每列。 這稱為*按列綁定*,因為每個數據結構(陣列)包含單個列的數據。  
  
-   定義一個結構來保存整個行的數據並綁定這些結構的陣列。 這稱為*行綁定*,因為每個數據結構都包含單個行的數據。  
  
 每個緩衝區陣組必須具有至少與行集大小相同的元素數。  
  
> [!NOTE]  
>  應用程式必須驗證對齊是否有效。 有關對齊注意事項的詳細資訊,請參閱[對齊](../../../odbc/reference/develop-app/alignment.md)。  
  
## <a name="column-wise-binding"></a>資料行取向的繫結  
 在按列綁定中,應用程式將單獨的數據和長度/指示器陣列綁定到每列。  
  
 要使用按列綁定,應用程式首先將SQL_ATTR_ROW_BIND_TYPE語句屬性設置為SQL_BIND_BY_COLUMN。 (這是預設值。對於要綁定的每個列,應用程式執行以下步驟:  
  
1.  分配數據緩衝區陣列。  
  
2.  分配長度/指示器緩衝區的陣列。  
  
    > [!NOTE]  
    >  如果使用按列綁定時應用程式直接寫入描述符,則可以將單獨的陣列用於長度和指標數據。  
  
3.  使用以下參數呼叫**SQLBindCol:**  
  
    -   *TargetType*是數據緩衝區陣列中單個元素的類型。  
  
    -   *目標價值Ptr*是數據緩衝區陣列的位址。  
  
    -   *緩衝區長度*是數據緩衝區陣列中單個元素的大小。 當數據為固定長度數據時,將忽略*BufferLength*參數。  
  
    -   *StrLen_or_IndPtr*長度/指示器陣列的位址。  
  
 有關如何使用此資訊的詳細資訊,請參閱本節後面的"緩衝區位址"。 有關依列綁的詳細資訊,請參閱[欄-Wise 綁定](../../../odbc/reference/develop-app/column-wise-binding.md)。  
  
## <a name="row-wise-binding"></a>資料列取向的繫結  
 在按行綁定中,應用程式定義一個結構,其中包含要綁定的每個列的數據和長度/指示器緩衝區。  
  
 要使用行綁定,應用程式將執行以下步驟:  
  
1.  定義一個結構來保存一行數據(包括數據和長度/指標緩衝區),並分配這些結構的陣列。  
  
    > [!NOTE]  
    >  如果使用按行綁定時應用程式直接寫入描述符,則可以將單獨的欄位用於長度和指標數據。  
  
2.  將SQL_ATTR_ROW_BIND_TYPE語句屬性設置為包含單個數據行的結構大小,或將結果列綁定到的緩衝區實例的大小。 長度必須包含所有綁定列的空間以及結構或緩衝區的任何填充,以確保當綁定列的位址以指定長度遞增時,結果將指向下一行中同一列的開頭。 在 ANSI C 中使用*大小*運算符時,此行為得到保證。  
  
3.  呼叫**SQLBindCol,** 對要繫列每個列有以下參數:  
  
    -   *TargetType*是要綁定到列的數據緩衝區成員的類型。  
  
    -   *TargetValuePtr*是第一個陣列元素中數據緩衝區成員的位址。  
  
    -   *緩衝區長度*是數據緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是要綁定的長度/指示器成員的位址。  
  
 有關如何使用此資訊的詳細資訊,請參閱本節後面的"緩衝區位址"。 有關依列綁的詳細資訊,請參閱[行-Wise 綁定](../../../odbc/reference/develop-app/row-wise-binding.md)。  
  
## <a name="buffer-addresses"></a>緩衝區位址  
 *緩衝區位址*是數據或長度/指示器緩衝區的實際位址。 驅動程式在緩衝區寫入緩衝區之前(如在提取時間)之前計算緩衝區位址。 它根據以下公式計算,該公式使用*TargetValuePtr*中指定的位址 *,StrLen_or_IndPtr*參數、綁定偏移量和行號:  
  
 *繫結位址* + *繫結位位移*量 = ((*行號*- 1) x*元素大小*)  
  
 其中公式的變數定義如下表所述。  
  
|變數|描述|  
|--------------|-----------------|  
|*繫結位址*|對於數據緩衝區,在**SQLBindCol**中使用*TargetValuePtr*參數指定的位址。<br /><br /> 對於長度/指示器緩衝區,使用**SQLBindCol**中*StrLen_or_IndPtr*參數指定的位址。 有關詳細資訊,請參閱"描述符和 SQLBindCol"部分中的"附加註釋」。。<br /><br /> 如果綁定位址為 0,則不返回任何數據值,即使前一個公式計算的位址為非零。|  
|*繫結位移*|如果使用按行綁定,則存儲在使用SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性指定的位址的值。<br /><br /> 如果使用按列綁定,或者SQL_ATTR_ROW_BIND_OFFSET_PTR語句屬性的值為空指標,*則綁定偏移*量為 0。|  
|*Row Number*|行集中的行的 1 個基於的編號。 對於預設的單行提取,這是 1。|  
|*元素大小*|綁定陣列中元素的大小。<br /><br /> 如果使用按列綁定,則長度/指示器緩衝區的大小**為(SQLINTEGER)。** 對於數據緩衝區,如果數據類型為可變長度,則為**SQLBindCol**中的*BufferLength*參數的值;如果數據類型為固定長度,則為數據類型的大小。<br /><br /> 如果使用按行綁定,則這是數據和長度/指示器緩衝區SQL_ATTR_ROW_BIND_TYPE語句屬性的值。|  
  
## <a name="descriptors-and-sqlbindcol"></a>描述符與 SQLBindCol  
 以下各節介紹**SQLBindCol**如何與描述符進行交互。  
  
> [!CAUTION]  
>  為一個語句調用**SQLBindCol**可能會影響其他語句。 當顯式分配與語句關聯的 ARD 並且也與其他語句關聯時,將發生這種情況。 由於**SQLBindCol**修改了描述符,因此修改將應用於與此描述符關聯的所有語句。 如果這不是必需的行為,則應用程式在調用**SQLBindCol**之前應將其描述符與其他語句分離。  
  
## <a name="argument-mappings"></a>參數對應  
 從概念上講 **,SQLBindCol**按順序執行以下步驟:  
  
1.  調用**SQLGetStmtAttr**以獲取 ARD 句柄。  
  
2.  呼叫**SQLGetDescField**取得此描述符號SQL_DESC_COUNT, 如果*欄位*參數中的值超過SQL_DESC_COUNT的值,則呼叫**SQLSetDescField**以將SQL_DESC_COUNT的值增加到*欄號*。  
  
3.  多次調用**SQLSetDescField**將值分配給 ARD 的以下欄位:  
  
    -   將SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE設置為*TargetType*的值,但如果*TargetType*是日期時間或間隔子類型的簡潔標識符之一,則分別將SQL_DESC_TYPE設置為SQL_DATETIME或SQL_INTERVAL;將SQL_DESC_CONCISE_TYPE設置到簡潔標識符;並將SQL_DESC_DATETIME_INTERVAL_CODE設置為相應的日期時間或間隔子代碼。  
  
    -   設置一個或多個適用於*TargetType*的SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_DATETIME_INTERVAL_PRECISION。  
  
    -   將SQL_DESC_OCTET_LENGTH欄位設置為*緩衝區長度*的值。  
  
    -   將SQL_DESC_DATA_PTR欄位設置為*目標值*的值。  
  
    -   將SQL_DESC_INDICATOR_PTR欄位設置為*StrLen_or_Ind*的值。 (請參閱以下段落。  
  
    -   將SQL_DESC_OCTET_LENGTH_PTR欄位設置為*StrLen_or_Ind*的值。 (請參閱以下段落。  
  
 *StrLen_or_Ind*參數引用的變數用於指標和長度資訊。 如果提取遇到列的空值,它將存儲SQL_NULL_DATA此變數中;如果提取遇到列的 null 值,則它將存儲SQL_NULL_DATA。否則,它將數據長度存儲在此變數中。 將空指標傳遞為*StrLen_or_Ind*防止提取操作返回數據長度,但如果遇到空值且無法返回SQL_NULL_DATA,則使提取失敗。  
  
 如果對**SQLBindCol**的調用失敗,它將在 ARD 中設置的描述符欄位的內容未定義,並且 ARD SQL_DESC_COUNT欄位的值保持不變。  
  
## <a name="implicit-resetting-of-count-field"></a>COUNT 欄位的隱式重置  
 **SQLBindCol**僅當增加SQL_DESC_COUNT值時,才會將SQL_DESC_COUNT*列編號*參數的值設置。 如果*TargetValuePtr*參數中的值為空指標,而*ColumnNumber*參數中的值等於SQL_DESC_COUNT(即,取消綁定最高綁定列時),則SQL_DESC_COUNT設置為最高剩餘綁定列的數量。  
  
## <a name="cautions-regarding-sql_default"></a>關於SQL_DEFAULT注意事項  
 要成功檢索列數據,應用程式必須正確確定應用程式緩衝區中數據的長度和起始點。 當應用程式指定顯式*TargetType*時,很容易檢測到應用程式誤解。 但是,當應用程式指定*SQL_DEFAULT的TargetType*時 **,SQLBindCol**可以應用於與應用程式預期資料類型不同的資料類型的列,從更改元資料或將代碼應用於其他列。 在這種情況下,應用程式可能並不總是確定提取的列數據的開始或長度。 這可能導致未報告的數據錯誤或記憶體衝突。  
  
## <a name="code-example"></a>程式碼範例  
 在下面的示例中,應用程式在客戶表上執行**SELECT**語句,以返回按名稱排序的客戶帳號、名稱和電話號碼的結果集。 然後,它調用**SQLBindCol**將數據列綁定到本地緩衝區。 最後,應用程式使用**SQLFetch**提取每行數據,並列印每個客戶的姓名、ID 和電話號碼。  
  
 有關更多程式碼範例,請參閱[SQLBulk 操作函數](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQLColumns 函數](../../../odbc/reference/syntax/sqlcolumns-function.md)[、SQLFetchScroll 函數](../../../odbc/reference/syntax/sqlfetchscroll-function.md)與[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
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
  
 另請參考[範例 ODBC 計畫](../../../odbc/reference/sample-odbc-program.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回有關結果集中的資訊|[SQLDescribeCol 函式](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得多行資料|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|在語句上釋放列緩衝區|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|取得資料欄的一部份或全部|[SQLGetData 函數](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|傳回結果集欄數|[SQLNumResultCols 函數](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
