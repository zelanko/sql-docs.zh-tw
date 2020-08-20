---
description: SQLSpecialColumns 函數
title: SQLSpecialColumns 函式 |Microsoft Docs
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
ms.openlocfilehash: ca29bf8bbef30296ad1aef17bda6890b23da8fb4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476064"
---
# <a name="sqlspecialcolumns-function"></a>SQLSpecialColumns 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性：開啟群組  
  
 **總結**  
 **SQLSpecialColumns** 會抓取有關指定資料表內資料行的下列資訊：  
  
-   可在資料表中唯一識別資料列的最佳資料行集合。  
  
-   當交易更新資料列中的任何值時，會自動更新的資料行。  
  
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
 *StatementHandle*  
 輸出語句控制碼。  
  
 *IdentifierType*  
 輸出要傳回的資料行類型。 必須為下列其中一個值：  
  
 SQL_BEST_ROWID：會傳回最適合的資料行或資料行集合，藉由從資料行或資料行中取得值，允許唯一識別指定之資料表中的任何資料列。 資料行可以是特別針對此用途所設計的虛擬資料行 (如同在 Oracle ROWID 或 Ingres TID) 或資料表之任何唯一索引的資料行或資料行中。  
  
 SQL_ROWVER：傳回指定資料表中的資料行（如果有的話），當任何交易更新資料列中的任何值時，資料來源會自動更新此資料行（如果有的話）， (如 SQLBase ROWID 或 Sybase TIMESTAMP) 。  
  
 *CatalogName*  
 輸出資料表的目錄名稱。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示這些資料表沒有目錄。 *CatalogName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *CatalogName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *CatalogName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。 如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 輸出**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 輸出資料表的架構名稱。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示那些沒有架構的資料表。 *SchemaName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *SchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *SchemaName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength2*  
 輸出**SchemaName*的長度（以字元為單位）。  
  
 *名*  
 輸出資料表名稱。 這個引數不可以是 null 指標。 *TableName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *TableName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *TableName* 就是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength3*  
 輸出**TableName*的長度（以字元為單位）。  
  
 *範圍*  
 輸出Rowid 的最小必要範圍。 傳回的 rowid 可能是較大的範圍。 必須是下列其中之一：  
  
 SQL_SCOPE_CURROW：只有在定位於該資料列時，rowid 才保證有效。 如果另一個交易已更新或刪除資料列，則使用 rowid 之後重新選擇可能不會傳回資料列。  
  
 SQL_SCOPE_TRANSACTION：在目前交易的持續時間內，rowid 保證是有效的。  
  
 SQL_SCOPE_SESSION：在跨交易界限) 的會話 (期間，會保證 rowid 有效。  
  
 *可為 Null*  
 輸出判斷是否傳回可以有 Null 值的特殊資料行。 必須是下列其中之一：  
  
 SQL_NO_NullS：排除可以有 Null 值的特殊資料行。 某些驅動程式無法支援 SQL_NO_NullS，如果指定 SQL_NO_NullS，這些驅動程式將會傳回空的結果集。 應用程式應該針對此案例做好準備，並只在絕對必要時要求 SQL_NO_NullS。  
  
 SQL_NullABLE：傳回特殊資料行，即使它們可以有 Null 值也是如此。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLSpecialColumns**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLSpecialColumns** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在 *StatementHandle*上開啟了資料指標，且已呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 如果 **SQLFetch** 或 **SQLFetchScroll** 尚未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果 **SQLFetch** 或 **SQLFetchScroll** 已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 在 *StatementHandle*上開啟了資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一個交易發生資源鎖死，所以已回復交易。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在 *StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效|*TableName*引數為 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE、 *CatalogName* 引數為 null 指標，且 SQL_CATALOG_NAME *InfoType* 會傳回支援的目錄名稱。<br /><br />  (DM) SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，且 *SchemaName* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLSpecialColumns** 時，仍在執行此函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 其中一個長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個長度引數的值超過對應名稱的最大長度值。 藉由呼叫 **SQLGetInfo** 和 *InfoType* 值，即可取得每個名稱的最大長度： SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 或 SQL_MAX_TABLE_NAME_LEN。|  
|HY097|資料行類型超出範圍| (DM) 指定了不正確 *IdentifierType* 值。|  
|HY098|範圍類型超出範圍| (DM) 指定了不正確 *範圍* 值。|  
|HY099|可為 null 的類型超出範圍| (DM) 指定了不正確 *可為 null* 值。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|已指定目錄，且驅動程式或資料來源不支援目錄。<br /><br /> 指定了架構，而驅動程式或資料來源不支援架構。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而且 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回要求的結果集之前過期。 Timeout 期限是透過 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 當 SQL_BEST_ROWID *IdentifierType* 引數時， **SQLSpecialColumns** 會傳回可唯一識別資料表中每個資料列的資料行。 這些資料行一律可以用在 *選取清單* 或 **WHERE** 子句中。 **SQLColumns**（用來傳回資料表之資料行的各種資訊）不一定會傳回可唯一識別每個資料列的資料行，或是當交易更新資料列中的任何值時，自動更新的資料行。 例如， **SQLColumns** 可能不會傳回「Oracle 虛擬資料行」。 這就是為什麼使用 **SQLSpecialColumns** 來傳回這些資料行的原因。 如需詳細資訊，請參閱 [目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱 [目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 如果沒有任何資料行可唯一識別資料表中的每個資料列， **SQLSpecialColumns** 會傳回沒有資料列的資料列集;對語句的 **SQLFetch** 或 **SQLFetchScroll** 後續呼叫會傳回 SQL_NO_DATA。  
  
 如果 *IdentifierType*、 *Scope*或 *Nullable* 引數指定資料來源不支援的特性， **SQLSpecialColumns** 會傳回空的結果集。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *CatalogName*、 *SchemaName*和 *TableName* 引數會被視為識別碼，因此在某些情況下不能將它們設為 null 指標。  (如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。 )   
  
 **SQLSpecialColumns** 會將結果傳回為標準結果集（依範圍排序）。  
  
 已重新命名 ODBC 3.x 的下列資料*行。* 資料行名稱的變更不會影響回溯相容性，因為應用程式會依資料行編號進行系結。  
  
|ODBC 2.0 資料行|ODBC *3.x* 資料行|  
|---------------------|-----------------------|  
|PRECISION|COLUMN_SIZE|  
|LENGTH|BUFFER_LENGTH|  
|SCALE|DECIMAL_DIGITS|  
  
 若要判斷 COLUMN_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫 **SQLGetInfo** 。  
  
 下表列出結果集中的資料行。 資料行8以外的其他資料行 (PSEUDO_COLUMN) 可以由驅動程式定義。 應用程式應該從結果集的結尾算下，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱 [目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|範圍 (ODBC 1.0) |1|Smallint|Rowid 的實際範圍。 包含下列其中一個值：<br /><br /> SQL_SCOPE_CURROW SQL_SCOPE_TRANSACTION SQL_SCOPE_SESSION<br /><br /> 當 SQL_ROWVER *IdentifierType* 時，會傳回 Null。 如需每個值的描述，請參閱本節稍早的「語法」中的 *範圍* 描述。|  
|COLUMN_NAME (ODBC 1.0) |2|Varchar not Null|資料行名稱。 驅動程式會針對沒有名稱的資料行傳回空字串。|  
|DATA_TYPE (ODBC 1.0) |3|Smallint 非 NULL|SQL 資料類型。 這可以是 ODBC SQL 資料類型或驅動程式特定的 SQL 資料類型。 如需有效 ODBC SQL 資料類型的清單，請參閱 [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)。 如需有關驅動程式特定的 SQL 資料類型的詳細資訊，請參閱驅動程式的檔。|  
|TYPE_NAME (ODBC 1.0) |4|Varchar not Null|與資料來源相關的資料類型名稱;例如，「CHAR」、「VARCHAR」、「MONEY」、「LONG VARBINARY」或「CHAR ( ) FOR BIT DATA」。|  
|COLUMN_SIZE (ODBC 1.0) |5|整數|資料來源上的資料行大小。 如需有關資料行大小的詳細資訊，請參閱資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|BUFFER_LENGTH (ODBC 1.0) |6|整數|如果指定 SQL_C_DEFAULT，則在 **SQLGetData** 或 **SQLFetch** 作業上傳送的資料長度（以位元組為單位）。 若為數值資料，此大小可能會與儲存在資料來源上的資料大小不同。 這個值與字元或二進位資料的 COLUMN_SIZE 資料行相同。 如需詳細資訊，請參閱資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|DECIMAL_DIGITS (ODBC 1.0) |7|Smallint|資料來源上之資料行的小數位數。 如果沒有適用十進位數的資料類型，則會傳回 Null。 如需十進位數的詳細資訊，請參閱資料 [行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。|  
|PSEUDO_COLUMN (ODBC 2.0) |8|Smallint|指出資料行是否為虛擬資料行，例如 Oracle ROWID：<br /><br /> SQL_PC_UNKNOWN SQL_PC_NOT_PSEUDO SQL_PC_PSEUDO **注意：**  如需最大互通性，虛擬資料行不應以 **SQLGetInfo**所傳回的識別碼引號字元括住。|  
  
 在應用程式抓取 SQL_BEST_ROWID 的值之後，應用程式可以使用這些值在定義的範圍內重新選擇該資料列。 **SELECT**語句保證不會傳回任何資料列或一個資料列。  
  
 如果應用程式根據 rowid 資料行或資料行來 reselects 資料列，但找不到該資料列，則應用程式可以假設該資料列已被刪除，或已修改 rowid 資料行。 相反的是：即使 rowid 未變更，資料列中的其他資料行也可能已變更。  
  
 針對資料行 SQL_BEST_ROWID 類型所傳回的資料行，對於需要在結果集中向前及向後移動，以從一組資料列中取出最新資料的應用程式很有用。 在定位於該資料列時，不會變更 rowid 的資料行。  
  
 當資料指標不在資料列上時，rowid 的資料行可能仍然有效，應用程式可以藉由檢查結果集中的 [範圍] 資料行來判斷這一點。  
  
 針對資料行 SQL_ROWVER 類型所傳回的資料行，適用于需要能夠檢查指定資料列中的任何資料行是否已在使用 rowid 問題資料列時更新的應用程式。 例如，在使用 rowid reselecting 資料列之後，應用程式可以將 SQL_ROWVER 資料行中之前的值與剛剛提取的值進行比較。 如果 SQL_ROWVER 資料行中的值與先前的值不同，則應用程式可以警告使用者顯示的資料已變更。  
  
## <a name="code-example"></a>程式碼範例  
 如需類似功能的程式碼範例，請參閱 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主要索引鍵的資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
