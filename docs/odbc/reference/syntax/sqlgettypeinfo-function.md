---
title: SQLGetTypeInfo 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetTypeInfo
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetTypeInfo
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC]
ms.assetid: bdedb044-8924-4ca4-85f3-8b37578e0257
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47273c75a005f11b33e9929977b57607b36898de
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303259"
---
# <a name="sqlgettypeinfo-function"></a>SQLGetTypeInfo 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLGetTypeInfo**傳回有關資料來源支援的資料類型的資訊。 驅動程式以 SQL 結果集的形式返回資訊。 資料類型用於資料定義語言 (DDL) 語句。  
  
> [!IMPORTANT]  
>  應用程式必須使用在**ALTER TABLE**和 CREATE **TABLE**敘述中**SQLGetTypeInfo**結果集的TYPE_NAME列中傳回的類型名稱。 **SQLGetTypeInfo**可能會返回DATA_TYPE列中具有相同值的多行。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLGetTypeInfo(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   DataType);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]結果集的語句句柄。  
  
 *DataType*  
 [輸入]SQL 資料類型。 這必須是附錄 D:數據類型或特定於驅動程式的 SQL 數據類型的[SQL 資料類型中的值](../../../odbc/reference/appendixes/sql-data-types.md)之一。 SQL_ALL_TYPES指定應返回有關所有數據類型的資訊。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLGetTypeInfo**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLGetTypeInfo**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01S02|選項值已變更|由於實現工作條件,指定的語句屬性無效,因此臨時替換了類似的值。 (調用**SQLGetStmtAttr**以確定臨時替換的值。在游標關閉之前,替換值對*語句處理*有效。 可以更改的語句屬性包括:SQL_ATTR_CONCURRENCY、SQL_ATTR_CURSOR_TYPE、SQL_ATTR_KEYSET_SIZE、SQL_ATTR_MAX_LENGTH、SQL_ATTR_MAX_ROWS、SQL_ATTR_QUERY_TIMEOUT和SQL_ATTR_SIMULATE_CURSOR。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|*語句處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *在語句句柄*上打開了結果集,但未調用**SQLFetch**或**SQLFetchScroll。**|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY004|無效的 SQL 資料類型|為參數*DataType*指定的值既不是有效的 ODBC SQL 資料類型識別碼,也不是驅動程式支援的特定於驅動程式的資料類型識別碼。|  
|HY008|已取消作業|非同步處理為*語句句柄*啟用,然後調用函數,並在函數完成執行之前,在語句句柄上調用**SQLCancel**或**SQLCancelHandle。** *StatementHandle* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,並在它完成執行之前 **,SQLCancel**或**SQLCancelHandle**從多線程式中的不同線程呼叫*了敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 呼叫**SQLGetTypeInfo**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*對應的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQLGetTypeInfo**將結果作為標準結果集返回,該結果由DATA_TYPE排序,然後按數據類型映射到相應 ODBC SQL 資料類型的緊密程度排序。 數據源定義的數據類型優先於使用者定義的數據類型。 因此,排序順序不一定一致,但可以概括為DATA_TYPE第一,然後是TYPE_NAME,兩者都是提升。 例如,假設數據源定義了 INTEGER 和 COUNTER 數據類型,其中 COUNTER 正在自動遞增,並且使用者定義的數據類型也已定義。 這些數據將按 INTEGER、WHOLENUM 和 COUNTER 的順序返回,因為 WHOLENUM 與 ODBC SQL 資料類型緊密映射SQL_INTEGER,而自動遞增數據類型(即使受數據源支援)也不會緊密映射到 ODBC SQL 數據類型。 有關如何使用此資訊的資訊,請參閱[DDL 語句](../../../odbc/reference/develop-app/ddl-statements.md)。  
  
 如果*DataType*參數指定對驅動程式支援的 ODBC 版本有效的數據類型,但驅動程式不支援該資料類型,則它將返回一個空結果集。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 以下列已重新命名為 ODBC 3。*x*. . 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC 3.*x*欄|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|MONEY|FIXED_PREC_SCALE|  
|AUTO_INCREMENT|AUTO_UNIQUE_VALUE|  
  
 以下列已添加到**SQLGetTypeInfo**為 ODBC 3 返回的結果集中。*x*:  
  
-   SQL_DATA_TYPE  
  
-   INTERVAL_PRECISION  
  
-   SQL_DATETIME_SUB  
  
-   NUM_PREC_RADIX  
  
 下表列出了結果集中的列。 驅動程式可以定義第 19 列(INTERVAL_PRECISION)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
> [!NOTE]  
>  **SQLGetTypeInfo**可能不會返回所有數據類型。 例如,驅動程式可能不會返回使用者定義的數據類型。 應用程式可以使用任何有效的資料類型,而不管它是否由**SQLGetTypeInfo**返回。 **SQLGetTypeInfo**傳回的資料類型是資料源支援的資料類型。 它們用於數據定義語言 (DDL) 語句。 驅動程式可以使用**SQLGetTypeInfo**傳回的類型以外的資料類型傳回結果集資料。 在為目錄函數創建結果集時,驅動程式可能使用數據源不支援的數據類型。  
  
|資料行名稱|資料行<br /><br /> number|資料類型|註解|  
|-----------------|-----------------------|---------------|--------------|  
|TYPE_NAME (ODBC 2.0)|1|瓦爾查爾不是 NULL|與數據源相關的數據類型名稱;例如,"CHAR()","VARCHAR()","金錢","長VARBINARY"或"CHAR ( ) BIT 數據"。 應用程式必須在**創建表**和**ALTER TABLE**語句中使用此名稱。|  
|DATA_TYPE (ODBC 2.0)|2|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或特定於驅動程式的 SQL 資料類型。 對於日期時間或間隔數據類型,此列返回簡潔的數據類型(如SQL_TYPE_TIME或SQL_INTERVAL_YEAR_TO_MONTH)。 有關有效的 ODBC SQL 資料類型的清單,請參閱附錄 D 中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md):資料類型。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。|  
|COLUMN_SIZE (ODBC 2.0)|3|整數|伺服器支援此資料類型的最大列大小。 對於數字數據,這是最大精度。 對於字串數據,這是字元的長度。 對於日期時間數據類型,這是字串表示的字元長度(假設小數秒元件允許的最大精度)。 對於不適用的列大小資料類型,將傳回 NULL。 對於間隔數據類型,這是間隔文本的字元表示中的字元數(由間隔前導精度定義;請參閱附錄 D 中的[間隔數據類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md):數據類型)。<br /><br /> 關於欄位的詳細資訊,請參考附入的 D:資料型態中的[欄位、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|LITERAL_PREFIX (ODBC 2.0)|4|Varchar|用於首碼的字元或字元;例如,字元數據類型的單個引號 (') 或二進位資料類型的 0x;對於不適用文本前置的資料類型,將傳回 NULL。|  
|LITERAL_SUFFIX (ODBC 2.0)|5|Varchar|用於終止文本的字元或字元;例如,字元數據類型的單個引號 (');對於不適用於文本後綴的數據類型,將返回 NULL。|  
|CREATE_PARAMS (ODBC 2.0)|6|Varchar|關鍵字清單,用逗號分隔,對應於應用程式在使用TYPE_NAME欄位中返回的名稱時在括弧中指定的每個參數。 清單中的關鍵字可以是以下任一關鍵字:長度、精度或比例。 它們按語法要求使用它們的順序出現。 例如,DECIMALCREATE_PARAMS是「精度、縮放」;VARCHAR 的CREATE_PARAMS等於"長度"。 如果數據類型定義沒有參數,則傳回 NULL;例如,INTEGER。<br /><br /> 驅動程式以使用該驅動程式的國家/地區的語言提供CREATE_PARAMS文本。|  
|空值 (ODBC 2.0)|7|Smallint 非 NULL|資料型態是否接受 NULL 值:<br /><br /> 如果資料類型不接受 NULL 值,則SQL_NO_NULLS。<br /><br /> 如果資料類型接受 NULL 值,SQL_NULLABLE。<br /><br /> 如果不知道列是否接受 NULL 值,則SQL_NULLABLE_UNKNOWN。|  
|CASE_SENSITIVE (ODBC 2.0)|8|Smallint 非 NULL|字元資料類型在排序規則和比較中是否區分大小寫:<br /><br /> 如果數據類型為字元數據類型且區分大小寫,SQL_TRUE。<br /><br /> 如果數據類型不是字元數據類型或區分大小寫,SQL_FALSE。|  
|可搜尋 (ODBC 2.0)|9|Smallint 非 NULL|**在 WHERE**子句中如何使用資料類型:<br /><br /> 如果列不能在**WHERE**子句中使用,則SQL_PRED_NONE。 (這與 ODBC 2 中的SQL_UNSEARCHABLE值相同。*x*.)<br /><br /> SQL_PRED_CHAR列是否可以在**WHERE**子句中使用,但只能與**LIKE**謂詞一起使用。 (這與 ODBC 2 中的SQL_LIKE_ONLY值相同。*x*.)<br /><br /> SQL_PRED_BASIC如果該列可以在**WHERE**子句中使用,並且所有比較運算符 **(LIKE、** 量化比較 **、"匹配****"、"差異****"、IN、MATCH**和**UNIQUE)** 除外。 **MATCH** (這與 ODBC 2 中的SQL_ALL_EXCEPT_LIKE值相同。*x*.)<br /><br /> SQL_SEARCHABLE列是否可以在任何比較運算符的**WHERE**子句中使用。|  
|UNSIGNED_ATTRIBUTE (ODBC 2.0)|10|Smallint|資料型態是否未簽署:<br /><br /> SQL_TRUE數據類型是否未簽名。<br /><br /> 如果數據類型已簽名,SQL_FALSE。<br /><br /> 如果屬性不適用於資料類型或資料類型不是數位,則傳回 NULL。|  
|FIXED_PREC_SCALE (ODBC 2.0)|11|Smallint 非 NULL|資料類型是否具有預先定義的固定精度和縮放(這是特定於資料來源的),例如貨幣資料類型:<br /><br /> SQL_TRUE,如果它具有預定義的固定精度和比例。<br /><br /> SQL_FALSE,如果它沒有預定義的固定精度和比例。|  
|AUTO_UNIQUE_VALUE (ODBC 2.0)|12|Smallint|資料型態是否自動遞增:<br /><br /> 如果數據類型自動遞增,SQL_TRUE。<br /><br /> 如果數據類型不是自動遞增,則SQL_FALSE。<br /><br /> 如果屬性不適用於資料類型或資料類型不是數位,則傳回 NULL。<br /><br /> 應用程式可以將值插入具有此屬性的列中,但通常無法更新列中的值。<br /><br /> 當將插入到自動增量列中時,在插入時將一個唯一值插入到列中。 增量未定義,但特定於數據源。 應用程式不應假定自動增量列從任何特定點開始,或由任何特定值增量。|  
|LOCAL_TYPE_NAME (ODBC 2.0)|13|Varchar|資料類型之資料來源相依名稱的當地語系化版本。 如果資料來源不支援當地語系化名稱，便傳回 NULL。 此名稱僅用於顯示,例如在對話框中。|  
|MINIMUM_SCALE (ODBC 2.0)|14|Smallint|數據源上數據類型的最小比例。 如果資料類型有固定的小數位數，MINIMUM_SCALE 和 MAXIMUM_SCALE 資料行都包含這個值。 例如,SQL_TYPE_TIMESTAMP列可能具有小數秒的固定比例。 當小數位數不適用時，會傳回 NULL。 有關詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):資料類型。|  
|MAXIMUM_SCALE (ODBC 2.0)|15|Smallint|數據源上數據類型的最大比例。 當小數位數不適用時，會傳回 NULL。 如果在數據源上未單獨定義最大比例,而是定義為與最大精度相同,則此列包含與COLUMN_SIZE列相同的值。 有關詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):資料類型。|  
|SQL_DATA_TYPE (ODBC 3.0)|16|小值不為空|SQL 資料類型的值,如它在描述符的SQL_DESC_TYPE欄位中顯示的。 此列與DATA_TYPE列相同,間隔和日期時間數據類型除外。<br /><br /> 對於間隔和日期時間數據類型,結果集中的SQL_DATA_TYPE欄位將返回SQL_INTERVAL或SQL_DATETIME,SQL_DATETIME_SUB欄位將返回特定間隔或日期時間數據類型的子代碼。 ( 參見[附錄 D:資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|17|Smallint|當SQL_DATA_TYPE值為SQL_DATETIME或SQL_INTERVAL時,此列包含日期時間/間隔子代碼。 對於日期時間和間隔以外的數據類型,此欄位為 NULL。<br /><br /> 對於間隔或日期時間數據類型,結果集中的SQL_DATA_TYPE欄位將返回SQL_INTERVAL或SQL_DATETIME,SQL_DATETIME_SUB欄位將返回特定間隔或日期時間數據類型的子代碼。 ( 參見[附錄 D:資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。|  
|NUM_PREC_RADIX (ODBC 3.0)|18|整數|如果數據類型是近似數值類型,則此列包含值 2 以指示COLUMN_SIZE指定多個位。 對於確切的數值類型,此列包含值 10 以指示COLUMN_SIZE指定小數位數。 否則，這個資料行就是 NULL。|  
|INTERVAL_PRECISION (ODBC 3.0)|19|Smallint|如果數據類型是間隔數據類型,則此列包含間隔前導精度的值。 (請參閱附錄 D 中的[間隔資料類型精度](../../../odbc/reference/appendixes/interval-data-type-precision.md):資料類型。否則,此列為 NULL。|  
  
 屬性資訊可以應用於數據類型或結果集中的特定列。 **SQLGetTypeInfo**傳回有關與資料類型關聯的屬性的資訊;**SQLColAttribute**傳回有關與結果集中列關聯的屬性的資訊。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回有關結果集中的資訊|[SQLColAttribute 函式](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回關於驅動程式或資料來源的資訊|[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
