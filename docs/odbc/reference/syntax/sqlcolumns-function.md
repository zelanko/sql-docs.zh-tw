---
title: SQLColumns 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumns
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumns
helpviewer_keywords:
- SQLColumns function [ODBC]
ms.assetid: 4a3618b7-d2b8-43c6-a1fd-7a4e6fa8c7d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36293c1f2393e9a57351fc8cd19dcc6e3338f5cc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301254"
---
# <a name="sqlcolumns-function"></a>SQLColumns 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: 開放組  
  
 **摘要**  
 **SQLColumn**傳回指定表中的列名稱清單。 驅動程式將返回此資訊作為在指定的*語句句柄*上集的結果。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLColumns(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      CatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      SchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      TableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      ColumnName,  
     SQLSMALLINT    NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *目錄名稱*  
 [輸入]目錄名稱。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串(")表示那些沒有目錄的表。 *目錄名稱*不能包含字串搜尋模式。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,則*目錄名稱*將被視為標識符,其大小寫不重要。 如果SQL_FALSE,目錄名稱是普通參數;如果為「*目錄名稱」,則為「目錄名稱」,* 但為「目錄名稱」,但為「目錄名稱」,但它被從字面上處理,它的情況很重要。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度在 **目錄名稱*的字元中。  
  
 *架構名稱*  
 [輸入]架構名稱的字串搜尋模式。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串(")表示那些沒有架構的表。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 SchemaName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,則 SchemaName 是模式值參數;如果為 SQL_FALSE,則 *「架構名稱」* 是模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度2*  
 [輸入]長度在 **架構名稱*的字元中。  
  
 *表格名稱*  
 [輸入]表名稱的字串搜尋模式。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則表Name*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,*則表名稱*是模式值參數;如果為"表名稱",則表名稱是模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度3*  
 [輸入]=*表名*的字元的長度。  
  
 *ColumnName*  
 [輸入]字串搜尋模式的列名稱。  
  
> [!NOTE]  
>  如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,則*ColumnName*被視為識別碼,其大小寫不重要。 如果SQL_FALSE,則「列名」是模式值參數;如果為「*列名稱」,* 則為「列名」,即為模式值參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度4*  
 [輸入]長度以 =*列名*的字元表示。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColumns**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了 SQLLists 通常傳回的**SQLSTATE**值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|24000|指標狀態無效|語句*處理*上打開了一個游標,並且調用了**SQLFetch**或**SQLFetchScroll。** 如果**SQLFetch**或**SQLFetchScroll**未返回SQL_NO_DATA,則驅動程式管理器將返回此錯誤,如果**SQLFetch**或**SQLFetchScroll**已返回SQL_NO_DATA,則驅動程式將返回此錯誤。<br /><br /> *語句句柄*上打開了一個游標,但未調用**SQLFetch**或**SQLFetchScroll。**|  
|40001|序列化失敗|由於資源與另一個事務死鎖,事務被回滾。|  
|40003|報表完成未知|執行此函數期間,關聯的連接失敗,無法確定事務的狀態。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*目錄名稱*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID敘述屬性設定為SQL_TRUE,*並且 SchemaName*名稱、*表名*或*列名*參數為空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLColumns**函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 其中一個名稱長度參數的值小於 0,但不等於SQL_NTS。|  
|||其中一個名稱長度參數的值超過相應目錄或名稱的最大長度值。 每個目錄或名稱的最大長度可以通過使用*InfoType*值呼叫**SQLGetInfo**獲得。 (請參閱"註釋」。。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了目錄名稱,並且驅動程式或數據源不支援目錄。<br /><br /> 指定了架構名稱,驅動程式或數據源不支援架構。<br /><br /> 為架構名稱、表名稱或列名稱指定了字串搜索模式,數據源不支援一個或多個這些參數的搜索模式。<br /><br /> 驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 此函數通常在語句執行之前用於從數據源的目錄中檢索有關表或表的列的資訊。 **SQLColumns**可用於檢索**SQLTables**傳回的所有類型的項目。 除了基表之外,這可能包括(但不限於)視圖、同義詞、系統表等。 相反,**函數 SQLColAttribute**和**SQLDescribeCol**描述結果集中的列,函數**SQLNumResultCols**傳回結果集中的列數。 關於詳細資訊,請參考[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLColumns**將結果作為標準結果集返回,按TABLE_CAT、TABLE_SCHEM、TABLE_NAME和ORDINAL_POSITION排序。  
  
> [!NOTE]  
>  當應用程式使用ODBC 2時。*x*驅動程式,結果集中不返回ORDINAL_POSITION列。 因此,當使用ODBC 2時。*x*驅動程式 **,SQLColumn**傳回的列清單中列的順序不一定與應用程式對該表中的所有列執行 SELECT 語句時返回的列的順序相同。  
  
> [!NOTE]  
>  **SQLColumns**可能不會返回所有列。 例如,驅動程式可能不會返回有關偽列的資訊,例如 Oracle ROWID。 應用程式可以使用任何有效的列,無論它是由**SQLColumn**返回的。  
>   
>  **SQLStatistics**可以返回的某些列不會由**SQLColumns**返回。 例如 **,SQLColumns**不會返回通過運算式或篩選器創建的索引中的列,例如"工資"或"福利"或"DEPT = 0012"。  
  
 VARCHAR 列的長度不顯示在表中;因此,VARCHAR 列的長度不顯示在表中。實際長度取決於數據源。 要確定TABLE_CAT、TABLE_SCHEM、TABLE_NAME和COLUMN_NAME列的實際長度,應用程式可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN選項調用**SQLGetInfo。**  
  
 以下列已重新命名為 ODBC 3。*x*. . 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC 3.*x*欄|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
|RADIX|NUM_PREC_RADIX|  
  
 以下列已添加到**SQLColumns**為 ODBC 3 返回的結果集中。*x*:  
  
|||  
|-|-|  
|CHAR_OCTET_LENGTH|ORDINAL_POSITION|  
|COLUMN_DEF|SQL_DATA_TYPE|  
|IS_NULLABLE|SQL_DATETIME_SUB|  
  
 下表列出了結果集中的列。 驅動程式可以定義第 18 列(IS_NULLABLE)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行<br /><br /> number|資料類型|註解|  
|-----------------|-----------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|目錄名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有目錄的表。|  
|TABLE_SCHEM (ODBC 1.0)|2|Varchar|架構名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有架構的表。|  
|TABLE_NAME (ODBC 1.0)|3|瓦爾查爾不是 NULL|資料表名稱。|  
|COLUMN_NAME (ODBC 1.0)|4|瓦爾查爾不是 NULL|資料行名稱。 驅動程式返回沒有名稱的列的空字串。|  
|DATA_TYPE (ODBC 1.0)|5|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或特定於驅動程式的 SQL 資料類型。 對於日期時間和間隔數據類型,此列返回簡明的數據類型(如SQL_TYPE_DATE或SQL_INTERVAL_YEAR_TO_MONTH,而不是非簡潔數據類型(如SQL_DATETIME或SQL_INTERVAL)。 有關有效的 ODBC SQL 資料類型的清單,請參閱附錄 D 中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md):資料類型。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。<br /><br /> 為 ODBC 3 傳回的資料類型。*x*和 ODBC 2。*x*應用程式可能不同。 有關詳細資訊,請參閱[向後相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|TYPE_NAME (ODBC 1.0)|6|瓦爾查爾不是 NULL|與數據源相關的數據類型名稱;例如,"CHAR","VARCHAR","金錢","長VARBINAR",或"CHAR ( ) BIT 數據"。|  
|COLUMN_SIZE (ODBC 1.0)|7|整數|如果DATA_TYPE是SQL_CHAR或SQL_VARCHAR,則此列包含列的最大長度(以字元表示)。 對於日期時間數據類型,這是將值轉換為字元時顯示值所需的字元總數。 對於數位數據類型,根據NUM_PREC_RADIX列,這是數位總數或列中允許的位數總數。 對於間隔數據類型,這是間隔文本的字元表示中的字元數(由間隔前導精度定義,請參閱附錄 D 中的[間隔數據類型長度](../../../odbc/reference/appendixes/interval-data-type-length.md):數據類型)。 有關詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):資料類型。|  
|BUFFER_LENGTH (ODBC 1.0)|8|整數|如果指定了SQL_C_DEFAULT,則 SQLGetData、SQLFetch 或 SQLFetchScroll 操作上傳輸的數據的長度(以位元組為單位)。 對於數位資料,此大小可能與存儲在數據源上的數據的大小不同。 此值可能與字元數據的COLUMN_SIZE列不同。 有關長度的詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):數據類型。|  
|DECIMAL_DIGITS (ODBC 1.0)|9|Smallint|小數點右側的重要數位的總數。 對於SQL_TYPE_TIME和SQL_TYPE_TIMESTAMP,此列包含小數秒元件中的位數。 對於其他數據類型,這是數據源上列的小數位數。 對於包含時間分量的間隔數據類型,此列包含小數點右側的數字數(分數秒)。 對於不包含時間元件的間隔數據類型,此列為 0。 有關十進位數字的詳細資訊,請參閱附錄 D 中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md):數據類型。 對於不適用DECIMAL_DIGITS的數據類型,將返回 NULL。|  
|NUM_PREC_RADIX (ODBC 1.0)|10|Smallint|對於數位數據類型,10 或 2。 如果為 10,則COLUMN_SIZE和DECIMAL_DIGITS中的值將給出該列允許的十進位數字數。 例如,DECIMAL(12,5)列將返回NUM_PREC_RADIX 10、COLUMN_SIZE 12 和 DECIMAL_DIGITS 5;FLOAT 列可以返回 10 NUM_PREC_RADIX、COLUMN_SIZE 15 和 null DECIMAL_DIGITS。<br /><br /> 如果是 2,則COLUMN_SIZE和DECIMAL_DIGITS中的值給出列中允許的位數。 例如,FLOAT 列可以返回 2 的 RADIX、COLUMN_SIZE 53 和 NULL DECIMAL_DIGITS。<br /><br /> 對於不適用NUM_PREC_RADIX的數據類型,將返回 NULL。|  
|空值 (ODBC 1.0)|11|Smallint 非 NULL|如果列不能包含 NULL 值,則SQL_NO_NULLS。<br /><br /> 如果列接受 NULL 值,則SQL_NULLABLE。<br /><br /> 如果不知道列是否接受 NULL 值,則SQL_NULLABLE_UNKNOWN。<br /><br /> 此列返回的值不同於為IS_NULLABLE列返回的值。 NULLABLE 列明確指示列可以接受 NULL,但無法肯定地指示列不接受 NUL。 IS_NULLABLE列明確指示列不能接受 NUL,但無法肯定地指示列是否接受 NUL。|  
|備註 (ODBC 1.0)|12|Varchar|列的說明。|  
|COLUMN_DEF (ODBC 3.0)|13|Varchar|資料行的預設值。 如果此列中的值包含在引號中,則應將其解釋為字串。<br /><br /> 如果 NULL 被指定為預設值,則此列是單詞 NULL,而不是用引號括起來。 如果不進行截斷就無法表示預設值,則此列包含截斷,而不包含單個引號。 如果未指定預設值,則此列為 NULL。<br /><br /> COLUMN_DEF的值可用於生成新的列定義,除非它包含 TRUNCATED 的值。|  
|SQL_DATA_TYPE (ODBC 3.0)|14|Smallint 非 NULL|SQL 資料類型,如 iRD 中SQL_DESC_TYPE記錄欄位中顯示的。 這可以是 ODBC SQL 資料類型或特定於驅動程式的 SQL 資料類型。 此列與DATA_TYPE列相同,但日期時間和間隔數據類型除外。 此列返回日期時間和間隔數據類型的非簡明數據類型(如SQL_DATETIME或SQL_INTERVAL),而不是簡明的數據類型(如SQL_TYPE_DATE或SQL_INTERVAL_YEAR_TO_MONTH)。 如果此列返回SQL_DATETIME或SQL_INTERVAL,則可以從SQL_DATETIME_SUB列確定特定的數據類型。 有關有效的 ODBC SQL 資料類型的清單,請參閱附錄 D 中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md):資料類型。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。<br /><br /> 為 ODBC 3 傳回的資料類型。*x*和 ODBC 2。*x*應用程式可能不同。 有關詳細資訊,請參閱[向後相容性和標準合規性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。|  
|SQL_DATETIME_SUB (ODBC 3.0)|15|Smallint|日期時間和間隔數據類型的子類型代碼。 其他資料類型的這個資料行都會傳回 NULL。 有關日期時間和間隔子代碼的詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)中的"SQL_DESC_DATETIME_INTERVAL_CODE"。|  
|CHAR_OCTET_LENGTH (ODBC 3.0)|16|整數|字元或二進位數據類型列的最大長度(以位元組為單位)。 所有其他資料類型的這個資料行都會傳回 NULL。|  
|ORDINAL_POSITION (ODBC 3.0)|17|整數不是 NULL|資料行在資料表中的序數位置。 表中的第一列是數位 1。|  
|IS_NULLABLE (ODBC 3.0)|18|Varchar|如果列不包含 NUL,則為"否"。<br /><br /> 如果列可以包含 NUL,則為"是"。<br /><br /> 如果 Null 屬性不明，這個資料行會傳回長度為零的字串。<br /><br /> 遵照 ISO 規則來決定 Null 屬性。 ISO SQL 標準 DBMS 無法傳回空字串。<br /><br /> 此列返回的值與 NULLABLE 列傳回的值不同。 (請參閱 NULLABLE 列的說明。|  
  
## <a name="code-example"></a>程式碼範例  
 在下面的示例中,應用程式聲明**SQLColumns**返回的結果集的緩衝區。 它調用**SQLColumn**傳回描述 EMPLOYER 表中每一列的結果集。 然後,它調用**SQLBindCol**將結果集中的列綁定到緩衝區。 最後,應用程式使用**SQLFetch**獲取每一行數據並處理它。  
  
```cpp  
// SQLColumns_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqlext.h>  
#define STR_LEN 128 + 1  
#define REM_LEN 254 + 1  
  
// Declare buffers for result set data  
SQLCHAR szSchema[STR_LEN];  
SQLCHAR szCatalog[STR_LEN];  
SQLCHAR szColumnName[STR_LEN];  
SQLCHAR szTableName[STR_LEN];  
SQLCHAR szTypeName[STR_LEN];  
SQLCHAR szRemarks[REM_LEN];  
SQLCHAR szColumnDefault[STR_LEN];  
SQLCHAR szIsNullable[STR_LEN];  
  
SQLINTEGER ColumnSize;  
SQLINTEGER BufferLength;  
SQLINTEGER CharOctetLength;  
SQLINTEGER OrdinalPosition;  
  
SQLSMALLINT DataType;  
SQLSMALLINT DecimalDigits;  
SQLSMALLINT NumPrecRadix;  
SQLSMALLINT Nullable;  
SQLSMALLINT SQLDataType;  
SQLSMALLINT DatetimeSubtypeCode;  
  
SQLHSTMT hstmt = NULL;  
  
// Declare buffers for bytes available to return  
SQLINTEGER cbCatalog;  
SQLINTEGER cbSchema;  
SQLINTEGER cbTableName;  
SQLINTEGER cbColumnName;  
SQLINTEGER cbDataType;  
SQLINTEGER cbTypeName;  
SQLINTEGER cbColumnSize;  
SQLLEN cbBufferLength;  
SQLINTEGER cbDecimalDigits;  
SQLINTEGER cbNumPrecRadix;  
SQLINTEGER cbNullable;  
SQLINTEGER cbRemarks;  
SQLINTEGER cbColumnDefault;  
SQLINTEGER cbSQLDataType;  
SQLINTEGER cbDatetimeSubtypeCode;  
SQLINTEGER cbCharOctetLength;  
SQLINTEGER cbOrdinalPosition;  
SQLINTEGER cbIsNullable;  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
   retcode = SQLColumns(hstmt, NULL, 0, NULL, 0, (SQLCHAR*)"CUSTOMERS", SQL_NTS, NULL, 0);  
  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      // Bind columns in result set to buffers  
      SQLBindCol(hstmt, 1, SQL_C_CHAR, szCatalog, STR_LEN,&cbCatalog);  
      SQLBindCol(hstmt, 2, SQL_C_CHAR, szSchema, STR_LEN, &cbSchema);  
      SQLBindCol(hstmt, 3, SQL_C_CHAR, szTableName, STR_LEN,&cbTableName);  
      SQLBindCol(hstmt, 4, SQL_C_CHAR, szColumnName, STR_LEN, &cbColumnName);  
      SQLBindCol(hstmt, 5, SQL_C_SSHORT, &DataType, 0, &cbDataType);  
      SQLBindCol(hstmt, 6, SQL_C_CHAR, szTypeName, STR_LEN, &cbTypeName);  
      SQLBindCol(hstmt, 7, SQL_C_SLONG, &ColumnSize, 0, &cbColumnSize);  
      SQLBindCol(hstmt, 8, SQL_C_SLONG, &BufferLength, 0, &cbBufferLength);  
      SQLBindCol(hstmt, 9, SQL_C_SSHORT, &DecimalDigits, 0, &cbDecimalDigits);  
      SQLBindCol(hstmt, 10, SQL_C_SSHORT, &NumPrecRadix, 0, &cbNumPrecRadix);  
      SQLBindCol(hstmt, 11, SQL_C_SSHORT, &Nullable, 0, &cbNullable);  
      SQLBindCol(hstmt, 12, SQL_C_CHAR, szRemarks, REM_LEN, &cbRemarks);  
      SQLBindCol(hstmt, 13, SQL_C_CHAR, szColumnDefault, STR_LEN, &cbColumnDefault);  
      SQLBindCol(hstmt, 14, SQL_C_SSHORT, &SQLDataType, 0, &cbSQLDataType);  
      SQLBindCol(hstmt, 15, SQL_C_SSHORT, &DatetimeSubtypeCode, 0, &cbDatetimeSubtypeCode);  
      SQLBindCol(hstmt, 16, SQL_C_SLONG, &CharOctetLength, 0, &cbCharOctetLength);  
      SQLBindCol(hstmt, 17, SQL_C_SLONG, &OrdinalPosition, 0, &cbOrdinalPosition);  
      SQLBindCol(hstmt, 18, SQL_C_CHAR, szIsNullable, STR_LEN, &cbIsNullable);  
  
      while (SQL_SUCCESS == retcode) {  
         retcode = SQLFetch(hstmt);  
         /*  
         if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // show_error();  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
            0;   // Process fetched data  
         else  
            break;  
        */  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回欄或欄的權限|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|取得多行資料|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回唯一識別行的欄,或由事務自動更新的欄位|[SQLSpecialColumns 函式](../../../odbc/reference/syntax/sqlspecialcolumns-function.md)|  
|傳回表統計資訊和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回資料來源的表清單|[SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)|  
|傳回表或表權權限|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
