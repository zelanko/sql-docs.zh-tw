---
title: SQL統計功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLStatistics
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLStatistics
helpviewer_keywords:
- SQLStatistics function [ODBC]
ms.assetid: 45210682-cfea-4e5d-9951-bcf1cbe10f41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2a5ef0b0e54e17a2dc091a98efc972fa608ef15
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302942"
---
# <a name="sqlstatistics-function"></a>SQLStatistics 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLStatistics**檢索有關單個表和與表關聯的索引的統計資訊清單。 驅動程式將返回結果集。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLStatistics(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CatalogName,  
     SQLSMALLINT     NameLength1,  
     SQLCHAR *       SchemaName,  
     SQLSMALLINT     NameLength2,  
     SQLCHAR *       TableName,  
     SQLSMALLINT     NameLength3,  
     SQLUSMALLINT    Unique,  
     SQLUSMALLINT    Reserved);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *目錄名稱*  
 [輸入]目錄名稱。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串(")表示那些沒有目錄的表。 *目錄名稱*不能包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則*目錄名稱*將被視為標識符,其大小寫不重要。 如果SQL_FALSE,目錄名稱是普通參數;如果為「*目錄名稱」,則為「目錄名稱」,* 但為「目錄名稱」,但為「目錄名稱」,但它被從字面上處理,它的情況很重要。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度在 **目錄名稱*的字元中。  
  
 *架構名稱*  
 [輸入]架構名稱。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串(")表示那些沒有架構的表。 *架構名稱*不能包含字串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 SchemaName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,SchemaName 是一個普通的參數;如果是SQL_FALSE,則 *「架構名稱」* 是普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度2*  
 [輸入]長度在 **架構名稱*的字元中。  
  
 *表格名稱*  
 [輸入]表名稱。 此參數不能為空指標。 *架構名稱*不能包含字串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則表Name*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,*則表名*是普通參數;如果為 SQL_FALSE,則表名稱為普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度3*  
 [輸入]=*表名*的字元的長度。  
  
 *獨特*  
 [輸入]索引類型:SQL_INDEX_UNIQUE或SQL_INDEX_ALL。  
  
 *Reserved*  
 [輸入]指示結果集中的「卡迪內」列和頁面列的重要性。 以下選項僅影響「卡迪」列和 PAGES 列的返回;即使不返回 CARDINALITY 和 PAGES,也會返回索引資訊。  
  
 SQL_ENSURE請求驅動程式無條件檢索統計資訊。 (僅符合開放組標準且不支援 ODBC 擴展的驅動程式將無法支援SQL_ENSURE。  
  
 SQL_QUICK請求驅動程式僅在伺服器隨時可用時才能檢索其卡迪內蒂和頁面。 在這個情況下，驅動程式無法確保這些值是否為最新的。 (寫入開放組標準的應用程式始終會從符合 ODBC *3.x*的驅動程式中獲取SQL_QUICK行為。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLStatistics**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_STMT的*句柄類型*和*語句句柄*。 下表列出了 SQLSTATISTICS 通常返回的**SQLSTATE**值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|語句*處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。|  
|40001|序列化失敗|由於資源與另一個事務死鎖,事務被回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫該函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**在*語句句柄*上調用 ,然後在*語句句柄*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|*表名稱*參數是空指標。<br /><br /> SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*目錄名稱*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID文句屬性設定為SQL_TRUE,*而 SchemaName*參數是空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLStatistics**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 其中一個名稱長度參數的值小於 0,但不等於SQL_NTS。<br /><br /> 其中一個名稱長度參數的值超過相應名稱的最大長度值。|  
|HY100|唯一性選項類型範圍外|(DM) 指定了無效*的唯一*值。|  
|HY101|精確度選項類型範圍外|(DM) 指定了無效*的保留*值。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了目錄,驅動程式或數據源不支援目錄。<br /><br /> 已指定架構,驅動程式或數據源不支援架構。<br /><br /> 驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回請求的結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 **SQLStatistics**將有關單個表的資訊作為標準結果集返回,按NON_UNIQUE、TYPE、INDEX_QUALIFIER、INDEX_NAME和ORDINAL_POSITION排序。 結果集將表的統計資訊(在結果集的 CARDINALITY 列和 PAGES 列中)與有關每個索引的資訊相結合。 關於如何使用此資訊的資訊,請參考[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 要確定TABLE_CAT、TABLE_SCHEM、TABLE_NAME和COLUMN_NAME列的實際長度,應用程式可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN選項調用**SQLGetInfo。**  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 以下列已重新命名為 ODBC *3.x*。 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC *3.x*欄|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|SEQ_IN_INDEX|ORDINAL_POSITION|  
|COLLATION|ASC_OR_DESC|  
  
 下表列出了結果集中的列。 驅動程式可以定義第 13 列(FILTER_CONDITION)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|應用統計資訊或索引的表的目錄名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有目錄的表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|應用統計資訊或索引的表的架構名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有架構的表。|  
|TABLE_NAME (ODBC 1.0)|3|瓦爾查爾不是 NULL|應用統計資訊或索引的表的表的表名稱。|  
|NON_UNIQUE (ODBC 1.0)|4|Smallint|指示索引是否不允許重複值:<br /><br /> 如果索引值可以是非唯一的,SQL_TRUE。<br /><br /> 如果索引值必須是唯一的,SQL_FALSE。<br /><br /> 如果 TYPE 是SQL_TABLE_STAT,則傳回 NULL。|  
|INDEX_QUALIFIER (ODBC 1.0)|5|Varchar|用於限定執行**DROP INDEX**的索引名稱的標識碼;如果資料來源不支援索引限定符,或者 SQL_TABLE_STAT TYPE,則傳回 NULL。 如果在此列中返回非空值,則必須使用它來限定 DROP INDEX 語句上的索引名稱;如果在此列中返回非空值,則必須將其用於限定**DROP INDEX**語句上的索引名稱。否則,應使用TABLE_SCHEM限定索引名稱。|  
|INDEX_NAME (ODBC 1.0)|6|Varchar|索引名稱;如果 TYPE 是SQL_TABLE_STAT,則傳回 NULL。|  
|型態(ODBC 1.0)|7|Smallint 非 NULL|傳回的資訊型態:<br /><br /> SQL_TABLE_STAT指示表的統計資訊(在「卡迪蒂」或「頁面」列中)。<br /><br /> SQL_INDEX_BTREE表示 B 樹索引。<br /><br /> SQL_INDEX_CLUSTERED表示群集索引。<br /><br /> SQL_INDEX_CONTENT表示內容索引。<br /><br /> SQL_INDEX_HASHED表示哈希索引。<br /><br /> SQL_INDEX_OTHER表示另一種類型的索引。|  
|ORDINAL_POSITION (ODBC 1.0)|8|Smallint|索引中的列序列號(以 1 開頭);如果 TYPE 是SQL_TABLE_STAT,則傳回 NULL。|  
|COLUMN_NAME (ODBC 1.0)|9|Varchar|資料行名稱。 如果列基於表達式(如"工資 + 福利"),則返回表達式;如果列基於表達式,則返回該表達式。如果無法確定表達式,則返回一個空字串。 如果 TYPE 是SQL_TABLE_STAT,則傳回 NULL。|  
|ASC_OR_DESC (ODBC 1.0)|10|Char(1)|對列排序序列:「A」表示升序;下降的「D」;如果資料來源不支援列排序序列,或者 TYPE SQL_TABLE_STAT,則傳回 NULL。|  
|基數(ODBC 1.0)|11|整數|表或索引的基數;如果 TYPE 為 SQL_TABLE_STAT,則表中的行數;如果 TYPE 未SQL_TABLE_STAT,則索引中的唯一值數;如果該值從資料源中不可用,則傳回 NULL。|  
|頁 (ODBC 1.0)|12|整數|用於存儲索引或表的頁數;如果 TYPE 是 SQL_TABLE_STAT,則表的頁數;如果 TYPE 未SQL_TABLE_STAT,則索引的頁數;如果該值從資料源中不可用,或者不適用於數據源,則返回 NULL。|  
|FILTER_CONDITION (ODBC 2.0)|13|Varchar|如果索引是篩選索引,則這是篩選條件,例如 SALARY > 30000;如果無法確定篩選器條件,則這是一個空字串。<br /><br /> 如果索引不是篩選索引,則無法確定索引是篩選索引還是 TYPE SQL_TABLE_STAT。|  
  
 如果結果集中的行對應於表,則驅動程式將 TYPE 設置為SQL_TABLE_STAT並將NON_UNIQUE、INDEX_QUALIFIER、INDEX_NAME、ORDINAL_POSITION、COLUMN_NAME和ASC_OR_DESC設置為 NULL。 如果從資料源中不可用 CARDINALITY 或 PAGES,驅動程式將它們設置為 NULL。  
  
## <a name="code-example"></a>程式碼範例  
 有關類似函數的代碼範例,請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以僅轉發方向獲取單個行或數據塊。|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|返回外鍵列|[SQLForeignKeys 函數](../../../odbc/reference/syntax/sqlforeignkeys-function.md)|  
|傳回主鍵的欄位|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
