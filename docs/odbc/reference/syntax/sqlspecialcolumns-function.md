---
title: SQLSpecialColumns 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2bae2c5a51d7d16798bc2d7fca0e9d38509a0d6e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32923623"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： Open Group  
  
 **摘要**  
 **SQLSpecialColumns**擷取指定之資料表中的資料行的下列資訊：  
  
-   最佳資料行集可唯一識別資料表中的資料列。  
  
-   會自動更新時的交易更新資料列中的任何值的資料行。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *IdentifierType*  
 [輸入]要傳回的資料行類型。 必須是下列值之一：  
  
 SQL_BEST_ROWID： 傳回最佳資料行或一組資料行，指定用來唯一識別資料表中擷取值，從資料行或資料行，允許任何資料列。 資料行可以是任何一個虛擬資料行專為此用途 （如 Oracle ROWID 或 Ingres TID） 或資料行或資料行的唯一索引的資料表。  
  
 SQL_ROWVER： 傳回的資料行或資料行中指定的資料表，如果有的話，自動更新資料來源時 （如同 SQLBase ROWID 或 Sybase 時間戳記） 的任何交易更新資料列中的任何值。  
  
 *CatalogName*  
 [輸入]資料表的目錄名稱。 如果驅動程式支援目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料的不同 Dbms，空字串 ("") 表示沒有目錄的資料表。 *CatalogName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*會被視為識別項和其案例並不重要。 如果是 SQL_FALSE， *CatalogName*是一般的引數; 將它視為常值，和其案例很重要。 如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]中的字元長度 **CatalogName*。  
  
 *schemaName*  
 [輸入]資料表的結構描述名稱。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料的不同 Dbms，空字串 ("") 表示沒有結構描述的資料表。 *SchemaName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *SchemaName*會被視為識別項和其案例並不重要。 如果是 SQL_FALSE， *SchemaName*是一般的引數; 將它視為常值，和其案例很重要。  
  
 *NameLength2*  
 [輸入]中的字元長度 **SchemaName*。  
  
 *TableName*  
 [輸入]資料表名稱。 這個引數不可為 null 指標。 *TableName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *TableName*會被視為識別項和其案例並不重要。 如果是 SQL_FALSE， *TableName*是一般的引數; 將它視為常值，和其案例很重要。  
  
 *NameLength3*  
 [輸入]中的字元長度 **TableName*。  
  
 *範圍*  
 [輸入]Rowid 的最小必要的範圍。 範圍更大的可能傳回的 rowid。 必須是下列其中之一：  
  
 針對 SQL_SCOPE_CURROW： 保證 rowid 只有在位於這個資料列時，才有效。 如果資料列已更新或刪除另一項交易，後來再利用 rowid 可能不會傳回一個資料列。  
  
 SQL_SCOPE_TRANSACTION: Rowid 保證為有效的目前交易的持續時間。  
  
 SQL_SCOPE_SESSION: Rowid 保證為有效的工作階段持續期間 （跨越交易界限）。  
  
 *可為 Null*  
 [輸入]決定是否要傳回特殊資料行可以有 NULL 值。 必須是下列其中之一：  
  
 SQL_NO_NULLS： 排除可以有 NULL 值的特殊資料行。 有些驅動程式不支援 SQL_NO_NULLS，以及這些驅動程式會傳回空的結果集，如果已指定 SQL_NO_NULLS。 只在絕對必要時，應該針對此案例和要求 SQL_NO_NULLS 準備應用程式。  
  
 SQL_NULLABLE： 傳回特殊資料行，即使這些值可以有 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSpecialColumns**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLSpecialColumns** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在開啟游標的*StatementHandle*，和**SQLFetch**或**SQLFetchScroll**如同呼叫。 傳回這個錯誤是由驅動程式管理員如果**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，如果驅動程式傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 在開啟游標的*StatementHandle*，但**SQLFetch**或**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復由於與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|相關聯的連接失敗，此函式，在執行期間，無法決定交易的狀態。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|無效的 null 指標使用|*TableName*引數為 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*引數為 null 指標和 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*SchemaName*引數為 null 指標。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此函式還在執行時**SQLSpecialColumns**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY090|字串或緩衝區長度無效|(DM) 的長度引數的其中一個值小於 0 卻不等於 SQL_NTS。<br /><br /> 對應名稱的最大長度值超過長度引數的其中一個值。 每個名稱的長度上限可以藉由呼叫取得**SQLGetInfo**與*資訊類型*值： SQL_MAX_CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN 或 SQL_MAX_TABLE_NAME_LEN。|  
|HY097|資料行類型超出範圍|(DM) 無效*IdentifierType*指定的值。|  
|HY098|範圍類型超出範圍|(DM) 無效*範圍*指定的值。|  
|HY099|可為 null 類型超出範圍|(DM) 無效*Nullable*指定的值。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定類別目錄，並且在驅動程式或資料來源不支援目錄。<br /><br /> 指定結構描述，並且在驅動程式或資料來源不支援結構描述。<br /><br /> 驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，，並且 SQL_ATTR_CURSOR_TYPE 陳述式屬性設定為 驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前要求的結果集傳回的資料來源。 逾時期限透過設定**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 當*IdentifierType*引數是 SQL_BEST_ROWID， **SQLSpecialColumns**傳回唯一識別資料表中的每個資料列的資料行。 這些資料行一定可以用在*select 清單*或**其中**子句。 **SQLColumns**、 用來傳回在資料表的資料行上的各種資訊不一定是傳回資料行可唯一識別每個資料列，或由更新資料列中的任何值時自動更新的資料行交易。 例如， **SQLColumns**可能不會傳回 ROWID Oracle 虛擬資料行。 這就是為什麼**SQLSpecialColumns**用來傳回這些資料行。 如需詳細資訊，請參閱[的目錄資料會使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果沒有唯一識別資料表中的每個資料列的資料行**SQLSpecialColumns**傳回一個資料列集有任何資料列，後續呼叫**SQLFetch**或**SQLFetchScroll**陳述式會傳回 sql_no_data 為止。  
  
 如果*IdentifierType*，*範圍*，或*Nullable*引數指定的資料來源，不支援特性**SQLSpecialColumns**傳回空的結果集。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*， *SchemaName*，和*TableName*引數都會當成識別項，因此它們無法設定為 null 指標，在某些情況下。 (如需詳細資訊，請參閱[目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。)  
  
 **SQLSpecialColumns**做為標準的結果集，依 SCOPE 來排序傳回的結果。  
  
 下列資料行已重新命名為 ODBC 3 *.x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3 *.x*資料行|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 若要判斷 COLUMN_NAME 資料行的實際長度，應用程式可以呼叫**SQLGetInfo** SQL_MAX_COLUMN_NAME_LEN 選項。  
  
 下表列出結果集內的資料行。 資料行 8 (PSEUDO_COLUMN) 以外的其他資料行可以定義由驅動程式。 應用程式應該要存取驅動程式特有的資料行向下計數從結果集的結尾，而非指定明確的序數位置。 如需詳細資訊，請參閱[目錄函數所傳回資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|範圍 (ODBC 1.0)|1|Smallint|Rowid 實際範圍。 包含下列值之一：<br /><br /> 針對 SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> 會傳回 NULL 時*IdentifierType*是 SQL_ROWVER。 如需每個值的說明，請參閱描述*範圍*中 「 語法 」，稍早在本章節中。|  
|COLUMN_NAME (ODBC 1.0)|2|Varchar 不是 NULL|資料行名稱。 驅動程式傳回的資料行沒有名稱為空字串。|  
|DATA_TYPE (ODBC 1.0)|3|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式專屬 SQL 資料類型。 如需有效的 ODBC SQL 資料類型的清單，請參閱[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)。 如需驅動程式特有的 SQL 資料類型資訊，請參閱驅動程式的文件。|  
|TYPE_NAME (ODBC 1.0)|4|Varchar 不是 NULL|資料來源而定的資料型別名稱。例如，"CHAR"、"VARCHAR"、"MONEY"、"長 VARBINARY"或者 「 CHAR （） FOR BIT DATA 中的 」。|  
|COLUMN_SIZE (ODBC 1.0)|5|Integer|資料來源之資料行的大小。 如需有關資料行大小，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH (ODBC 1.0)|6|Integer|以位元組為單位的傳輸上的資料長度**SQLGetData**或**SQLFetch**作業時，如果指定 SQL_C_DEFAULT。 針對數值資料，這個大小可能會與資料來源上所儲存之資料的大小不同。 這個值可以是字元或二進位資料的 COLUMN_SIZE 資料行相同。 如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS (ODBC 1.0)|7|Smallint|資料來源之資料行的小數位數。 會傳回 NULL 的資料類型小數位數不適用。 關於十進位數字的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN (ODBC 2.0)|8|Smallint|指出資料行是否為虛擬資料行，例如 Oracle ROWID:<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO**附註：** 最大的互通性，虛擬資料行應不會加上引號的引號字元所傳回的識別項**SQLGetInfo**。|  
  
 應用程式會擷取 SQL_BEST_ROWID 值之後，應用程式可以使用這些值以重新選取該資料列定義的範圍內。 **選取**保證陳述式會傳回任何資料列或一個資料列。  
  
 如果應用程式 reselects 根據 rowid 資料行或資料行的資料列，而且找不到資料列，應用程式可以假設已刪除資料列，或已修改 rowid 資料行。 反之則為 true： 即使 rowid 尚未變更，可能已變更的資料列中的其他資料行。  
  
 傳回 SQL_BEST_ROWID 和都很實用的應用程式，需要向前捲動的結果來擷取一組資料列的最新的資料集內傳回的資料行類型的資料行。 資料行或資料行的 rowid 會保證不會變更放在該資料列時。  
  
 資料行或資料行的 rowid 可能會維持有效資料指標沒有定位資料列即使應用程式可以判定這檢查範圍中的資料行的結果集。  
  
 傳回 SQL_ROWVER 是適用於應用程式需要，能夠先檢查資料列已被使用 rowid 時是否已經更新任何給定的資料列中的資料行的資料行類型的資料行。 例如之後重新使用 rowid 資料列，應用程式可以比較 SQL_ROWVER 資料行，只擷取的項目中先前的值。 如果 SQL_ROWVER 資料行中的值不同於先前的值，應用程式可以警示使用者顯示的資料已變更。  
  
## <a name="code-example"></a>程式碼範例  
 函式類似的程式碼範例，請參閱[SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集內的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回的資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|擷取單一資料列或資料區塊的順向的方向|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主索引鍵資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
