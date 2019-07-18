---
title: SQLColumnPrivileges 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColumnPrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColumnPrivileges
helpviewer_keywords:
- SQLColumnPrivileges function [ODBC]
ms.assetid: ef233d9a-6ed5-4986-9d42-5e0b1a79fb6e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5e3c54e0e2eb4ad633d35159e1ff010c9388f5d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118710"
---
# <a name="sqlcolumnprivileges-function"></a>SQLColumnPrivileges 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLColumnPrivileges**傳回的資料行和相關聯的權限指定的資料表清單。 驅動程式會傳回當作結果集上指定的資訊*StatementHandle*。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLColumnPrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3,  
     SQLCHAR *     ColumnName,  
     SQLSMALLINT   NameLength4);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *CatalogName*  
 [輸入]目錄名稱。 如果驅動程式支援的名稱，對於某些類別目錄，但不是供其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示那些不會有名稱的目錄。 *CatalogName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*CatalogName*是一般的引數; 也就是，則會視為和其案例很重要。 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]中的字元長度 **CatalogName*。  
  
 *SchemaName*  
 [輸入]結構描述名稱。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有結構描述的資料表。 *SchemaName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *SchemaName*會被視為識別項。 SQL_FALSE，才*SchemaName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength2*  
 [輸入]中的字元長度 **SchemaName*。  
  
 *TableName*  
 [輸入]資料表名稱。 此引數不可為 null 指標。 *TableName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *TableName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*TableName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength3*  
 [輸入]中的字元長度 **TableName*。  
  
 *ColumnName*  
 [輸入]資料行名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *ColumnName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*ColumnName*模式值引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength4*  
 [輸入]中的字元長度 **ColumnName*。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLColumnPrivileges**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可能會取得藉由呼叫**SQLGetDiagRec**具有*HandleType*利用 SQL_HANDLE_STMT 的並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLColumnPrivileges** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前，驅動程式所傳回的 Sqlstate 的描述管理員。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|資料指標是開啟*StatementHandle，* 並**SQLFetch**或**SQLFetchScroll**呼叫。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標是開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|*TableName*引數是 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *CatalogName*引數為 null 指標，以及 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*SchemaName*或是*ColumnName*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 仍在呼叫此函式時執行此非同步函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 其中一個名稱的長度引數的值小於 0，但不是等於 SQL_NTS。|  
|||其中一個名稱的長度引數的值超過最大長度值，對應的名稱。 （請參閱 「 註解。"）|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的目錄名稱，並在驅動程式或資料來源不支援目錄。<br /><br /> 指定的結構描述名稱，且驅動程式或資料來源不支援結構描述。<br /><br /> 資料行名稱，為指定的字串搜尋模式和資料來源不支援該引數的搜尋模式。<br /><br /> SQL_CONCURRENCY 和 SQL_CURSOR_TYPE 的陳述式屬性的目前設定的組合已不支援的驅動程式或資料來源。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 **SQLColumnPrivileges**標準的結果集，按照 TABLE_CAT、 再依據 table_schem 排列、 TABLE_NAME、 COLUMN_NAME 和權限的方式傳回結果。  
  
> [!NOTE]  
>  **SQLColumnPrivileges**可能不會傳回所有資料行的權限。 例如，驅動程式可能不會傳回虛擬資料行，例如 Oracle ROWID 的權限的詳細資訊。 應用程式可以使用任何有效的資料行，不論它會傳回所**SQLColumnPrivileges**。  
  
 VARCHAR 資料行的長度不會顯示在表格中，實際長度取決於資料來源。 若要判斷 CATALOG_NAME，SCHEMA_NAME、 TABLE_NAME、 COLUMN_NAME 資料行的實際長度，應用程式可以呼叫**SQLGetInfo** SQL_MAX_CATALOG_NAME_LEN，SQL_MAX_SCHEMA_NAME_LEN，SQL_MAX_TABLE_NAME_ 與LEN、 以及 SQL_MAX_COLUMN_NAME_LEN 選項。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 下列資料行已重新命名，針對 ODBC 3。*x*。 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3。*x*資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出結果集內的資料行。 驅動程式，可以定義資料行 8 (IS_GRANTABLE) 以外的其他資料行。 應用程式應該取得存取權的驅動程式特有的資料行，倒數，從結果集的結尾，而不是指定明確的序數位置。 如需詳細資訊，請參閱 <<c0> [ 目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|類別目錄識別碼;如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 沒有目錄這些資料表。|  
|再依據 TABLE_SCHEM 排列 (ODBC 1.0)|2|Varchar|結構描述識別碼;如果不適用於資料來源，則為 NULL。 如果驅動程式支援結構描述對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 並沒有結構描述這些資料表。|  
|TABLE_NAME (ODBC 1.0)|3|非 NULL Varchar|資料表識別碼。|  
|COLUMN_NAME (ODBC 1.0)|4|非 NULL Varchar|資料行名稱。 驅動程式會傳回沒有名稱的資料行的空字串。|  
|授與者 (ODBC 1.0)|5|Varchar|授與權限; 使用者名稱如果不適用於資料來源，則為 NULL。<br /><br /> 為被授與者的資料行中值的物件擁有者的所有資料列，GRANTOR 資料行就是"（_s） 」。|  
|被授與者 (ODBC 1.0)|6|非 NULL Varchar|對被授與權限的使用者名稱。|  
|權限 (ODBC 1.0)|7|非 NULL Varchar|識別資料行權限。 可能是下列其中之一 (或其他支援的資料來源時實作所定義):<br /><br /> 選取此項目：被授與者可以擷取資料行的資料。<br /><br /> 插入：被授與者可以提供新的資料列插入相關聯的資料表中的資料行的資料。<br /><br /> 更新：允許 grantee 將更新資料行中的資料。<br /><br /> 參考：是否允許 grantee 將參考條件約束內資料行 (例如，唯一、 參考，或檢查條件約束的資料表)。|  
|IS_GRANTABLE (ODBC 1.0)|8|Varchar|指出是否允許被授與者的權限授與給其他使用者;「 是 」、 「 不行 」 或 「 NULL 」 如果未知或不適用資料來源。<br /><br /> 權限為可授與或可授與，但非兩者皆是。 所傳回的結果集**SQLColumnPrivileges**絕不會包含兩個資料列除了 IS_GRANTABLE 資料行以外的所有資料行包含相同的值。|  
  
## <a name="code-example"></a>程式碼範例  
 類似的函式的程式碼範例，請參閱 < [SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|正在擷取多個資料列|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|傳回針對資料表或資料表的權限|[SQLTablePrivileges 函式](../../../odbc/reference/syntax/sqltableprivileges-function.md)|  
|傳回一份資料表中的資料來源|[SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
