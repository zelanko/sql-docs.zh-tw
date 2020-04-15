---
title: SQL 特殊列函數 :微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSpecialColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSpecialColumns
helpviewer_keywords:
- SQLSpecialColumns function [ODBC]
ms.assetid: bb2d9f21-bda0-4e50-a8be-f710db660034
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 826630e1d344322268a2f2638310b3a1e182de6d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287168"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 開放組  
  
 **摘要**  
 **SQL特別列**檢索有關指定表中列的以下資訊:  
  
-   唯一標識表中行的最佳列集。  
  
-   當行中的任何值由事務更新時自動更新的列。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLSpecialColumns(  
     SQLHSTMT      StatementHandle,  
     SQLSMALLINT   IdentifierType,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLSMALLINT   Scope,  
     SQLSMALLINT   Nullable);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *識別項類型*  
 [輸入]要返回的列的類型。 必須為下列其中一個值：  
  
 SQL_BEST_ROWID:返回最佳列或列集,通過從列或列檢索值,允許唯一標識指定表中的任何行。 列可以是專門為此設計的偽列(如 Oracle ROWID 或 Inres TID 中),也可以是表任何唯一索引的列或列。  
  
 SQL_ROWVER:返回指定表中的列或列(如果有),當行中的任何值由任何事務更新時(如 SQLBase ROWID 或 Sybase TIMESTAMP 中),數據源會自動更新的列(  
  
 *目錄名稱*  
 [輸入]表的目錄名稱。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),空字串("")表示那些沒有目錄的表。 *目錄名稱*不能包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則*目錄名稱*將被視為標識符,其大小寫不重要。 如果SQL_FALSE,目錄名稱是普通參數;如果為「*目錄名稱」,則為「目錄名稱」,* 但為「目錄名稱」,但為「目錄名稱」,但它被從字面上處理,它的情況很重要。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度在 **目錄名稱*的字元中。  
  
 *架構名稱*  
 [輸入]表的架構名稱。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串("")表示那些沒有架構的表。 *架構名稱*不能包含字串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 SchemaName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,SchemaName 是一個普通的參數;如果是SQL_FALSE,則 *「架構名稱」* 是普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度2*  
 [輸入]長度在 **架構名稱*的字元中。  
  
 *表格名稱*  
 [輸入]表名稱。 此參數不能為空指標。 *表名稱*不能包含字串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則表Name*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,*則表名*是普通參數;如果為 SQL_FALSE,則表名稱為普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度3*  
 [輸入]=*表名*的字元的長度。  
  
 *影響範圍*  
 [輸入]排 ID 的最小所需範圍。 返回的劃線可能具有更大的範圍。 必須是下列其中之一：  
  
 SQL_SCOPE_CURROW:保證行 id 僅在定位該行時有效。 如果行已更新或刪除另一個事務,則稍後使用行重新選擇可能不會返回該行。  
  
 SQL_SCOPE_TRANSACTION: 保證行 id 在當前事務期間有效。  
  
 SQL_SCOPE_SESSION:保證行 id 在會話期間(跨事務邊界)有效。  
  
 *可為 Null*  
 [輸入]確定是否返回具有 NULL 值的特殊欄。 必須是下列其中之一：  
  
 SQL_NO_NULLS:排除具有 NULL 值的特殊列。 某些驅動程式不支援SQL_NO_NULLS,如果指定了SQL_NO_NULLS,這些驅動程式將返回空結果集。 申請應為本案例做好準備,只有在絕對需要的情況下才SQL_NO_NULLS請求。  
  
 SQL_NULLABLE:返回特殊列,即使它們可以具有 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQL 特別列**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的**句柄*。 下表列出了**SQLSpecialColumns**通常返回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|語句*處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *語句句柄*上打開了一個游標,但**SQLFetch**或**SQLFetchScroll**尚未調用。|  
|40001|序列化失敗|由於與另一個事務的資源死鎖,事務已回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|*表名稱*參數是空指標。<br /><br /> SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*目錄名稱*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID文句屬性設定為SQL_TRUE,*而 SchemaName*參數是空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 呼叫**SQL 特殊列時**,此函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 長度參數之一的值小於 0,但不等於SQL_NTS。<br /><br /> 其中一個長度參數的值超過了相應名稱的最大長度值。 使用*InfoType*值呼叫**SQLGetInfo,** 可以取得每個名稱的最大長度:SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 或SQL_MAX_TABLE_NAME_LEN。|  
|HY097|欄型別範圍|(DM) 指定了無效的*識別碼類型*值。|  
|HY098|範圍類型範圍外|(DM) 指定了無效*的範圍*值。|  
|HY099|空白型別範圍|(DM) 指定*了無效的空值*。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了目錄,驅動程式或數據源不支援目錄。<br /><br /> 已指定架構,驅動程式或數據源不支援架構。<br /><br /> 驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回請求的結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 當*識別符類型*參數SQL_BEST_ROWID時 **,SQL特別列**將返回唯一標識表中每一行的列。 這些列始終可用於*選擇清單*或**WHERE**子句。 **SQLColumns**用於返回表列上的各種資訊,但不一定返回唯一標識每行的列,也不一定返回在事務更新行中的任何值時自動更新的列。 例如 **,SQLColumn**可能不會返回 Oracle 偽列 ROWID。 這就是為什麼**SQL 特殊列**用於返回這些列的原因。 關於詳細資訊,請參考[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果沒有唯一標識表中每行的列 **,SQLSpecialColumns**將返回一個沒有行的行集;如果清單將返回一行。語句上的**SQLFetch**或**SQLFetchScroll**的後續調用返回SQL_NO_DATA。  
  
 如果*識別符類型*、*作用域*或*空參數*指定數據源不支援的特徵 **,SQL特別列**將返回一個空的結果集。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則*目錄名稱*、*架構名稱*和*表名稱*參數將被視為標識符,因此在某些情況下無法將其設置為空指標。 (關於詳細資訊,請參考[目錄函數中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 **SQL特別列**將結果作為標準結果集返回,由SCOPE排序。  
  
 以下列已重新命名為 ODBC *3.x*。 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC *3.x*欄|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 要確定COLUMN_NAME列的實際長度,應用程式可以使用SQL_MAX_COLUMN_NAME_LEN選項調用**SQLGetInfo。**  
  
 下表列出了結果集中的列。 驅動程式可以定義第 8 列(PSEUDO_COLUMN)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|範圍(ODBC 1.0)|1|Smallint|行ID的實際範圍。 包含以下值之一:<br /><br /> SQL_SCOPE_CURROWSQL_SCOPE_TRANSACTIONSQL_SCOPE_SESSION<br /><br /> 當*識別子類型*SQL_ROWVER時,將傳回 NULL。 有關每個值的說明,請參閱本節前面"語法"中*的範圍*說明。|  
|COLUMN_NAME (ODBC 1.0)|2|瓦爾查爾不是 NULL|資料行名稱。 驅動程式返回沒有名稱的列的空字串。|  
|DATA_TYPE (ODBC 1.0)|3|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或特定於驅動程式的 SQL 資料類型。 有關有效的 ODBC SQL 資料類型的清單,請參閱[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。|  
|TYPE_NAME (ODBC 1.0)|4|瓦爾查爾不是 NULL|與數據源相關的數據類型名稱;例如,"CHAR","VARCHAR","金錢","長VARBINARY",或"CHAR ( ) BIT 數據"。|  
|COLUMN_SIZE (ODBC 1.0)|5|整數|數據源上的列的大小。 關於列大小的詳細資訊,請參閱[欄大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH (ODBC 1.0)|6|整數|如果指定了SQL_C_DEFAULT,則在**SQLGetData**或**SQLFetch**操作上傳輸的數據的長度(以位元組為單位)。 對於數位資料,此大小可能與存儲在數據源上的數據的大小不同。 此值與字元或二進位數據的COLUMN_SIZE列相同。 有關詳細資訊,請參閱[列大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|數據源上列的小數位數。 對於不適用十進位數字的數據類型,傳回 NULL。 有關十進位數字的詳細資訊,請參閱[列大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|指示列是否是偽列,例如 Oracle ROWID:<br /><br /> SQL_PC_UNKNOWNSQL_PC_NOT_PSEUDOSQL_PC_PSEUDO**注意:** 為了最大的互操作性,不應引用**SQLGetInfo**返回的標識符引號字元。|  
  
 應用程式檢索SQL_BEST_ROWID的值後,應用程式可以使用這些值在定義的作用域中重新選擇該行。 **SELECT**語句保證不返回任何行或一行。  
  
 如果應用程式根據行 id 列或列重新選擇行,但找不到該行,則應用程式可以假定該行已被刪除或已修改行。 相反的不是:即使行 ID 未更改,行中的其他列也可能已更改。  
  
 為列類型返回的列SQL_BEST_ROWID對於需要在結果集中向前和向後滾動以從一組行中檢索最新數據的應用程式很有用。 行 id 的列或列保證在定位該行時不會更改。  
  
 即使游標未放置在行上,劃線器的列也可能保持有效;應用程式可以通過檢查結果集中的 SCOPE 列來確定這一點。  
  
 為列類型返回的列SQL_ROWVER對於需要能夠檢查給定行中的任何列是否已更新,而使用行重新選擇行的應用程式非常有用。 例如,使用 rowid 重新選擇行後,應用程式可以將SQL_ROWVER列中以前的值與剛剛提取的值進行比較。 如果SQL_ROWVER列中的值與前一個值不同,應用程式可以提醒使用者顯示上的數據已更改。  
  
## <a name="code-example"></a>程式碼範例  
 有關類似函數的代碼範例,請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回表或表中的欄位|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主鍵的欄位|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
