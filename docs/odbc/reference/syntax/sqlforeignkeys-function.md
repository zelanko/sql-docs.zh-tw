---
title: SQLForeignKeys 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e0db81314355b987d139b678d292f5cfe293a7e
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206477"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLForeignKeys**可以傳回：  
  
-   指定的資料表 （資料行指定的資料表中參考其他資料表中的主索引鍵） 中的外部索引鍵的清單。  
  
-   在指定的資料表中的主索引鍵參考其他資料表中的外部索引鍵的清單。  
  
 驅動程式會傳回每個當作結果集上指定的陳述式的清單。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *PKCatalogName*  
 [輸入]主索引鍵資料表目錄名稱。 如果驅動程式支援的目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有目錄的資料表。 *PKCatalogName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *PKCatalogName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*PKCatalogName*是一般的引數; 也就是，則會視為和其案例很重要。 如需詳細資訊，請參閱 <<c0> [ 目錄函式中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度 **PKCatalogName*，以字元為單位。  
  
 *PKSchemaName*  
 [輸入]主索引鍵資料表的結構描述名稱。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有結構描述的資料表。 *PKSchemaName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *PKSchemaName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*PKSchemaName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength2*  
 [輸入]長度 **PKSchemaName*，以字元為單位。  
  
 *PKTableName*  
 [輸入]主索引鍵資料表名稱。 *PKTableName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *PKTableName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*PKTableName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength3*  
 [輸入]長度 **PKTableName*，以字元為單位。  
  
 *FKCatalogName*  
 [輸入]外部索引鍵資料表目錄名稱。 如果驅動程式支援的目錄，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有目錄的資料表。 *FKCatalogName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *FKCatalogName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*FKCatalogName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength4*  
 [輸入]長度 **FKCatalogName*，以字元為單位。  
  
 *FKSchemaName*  
 [輸入]外部索引鍵的資料表結構描述名稱。 如果驅動程式支援的結構描述，對於某些資料表，但不適用於其他人使用，例如當驅動程式會擷取資料從不同的 Dbms，空字串 ("") 表示沒有結構描述的資料表。 *FKSchemaName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *FKSchemaName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*FKSchemaName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength5*  
 [輸入]長度 **FKSchemaName*，以字元為單位。  
  
 *FKTableName*  
 [輸入]外部索引鍵資料表名稱。 *FKTableName*不能包含字串的搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *FKTableName*會被視為識別項和其案例並不重要。 SQL_FALSE，才*FKTableName*是一般的引數; 也就是，則會視為和其案例很重要。  
  
 *NameLength6*  
 [輸入]長度 **FKTableName*，以字元為單位。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLForeignKeys**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLForeignKeys** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|資料指標是開啟*StatementHandle*，並**SQLFetch**或是**SQLFetchScroll**呼叫。 如果此錯誤會傳回由驅動程式管理員**SQLFetch**或**SQLFetchScroll**尚未傳回 sql_no_data 之後，以及如果驅動程式會傳回**SQLFetch**或**SQLFetchScroll**傳回 sql_no_data 為止。<br /><br /> 資料指標是開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|40001|序列化失敗|交易已回復，因為與另一個交易資源鎖死。|  
|40003|未知的陳述式完成|此函式執行期間失敗的相關聯的連接，並無法判斷交易的狀態。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，並接著呼叫函式上再次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|(DM) 引數*PKTableName*並*FKTableName*是這兩個 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE， *FKCatalogName*或是*PKCatalogName*引數為 null 指標，以及 SQL_CATALOG_NAME*資訊類型*支援的目錄名稱，傳回。<br /><br /> (DM) SQL_ATTR_METADATA_ID 陳述式屬性設定為 SQL_TRUE，而*FKSchemaName*， *PKSchemaName*， *FKTableName*，或*PKTableName*引數是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 仍在 SQLForeignKeys 函式呼叫時執行此非同步函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 其中一個名稱的長度引數的值小於 0，但不是等於 SQL_NTS。|  
|||其中一個名稱的長度引數的值超過最大長度值，對應的名稱。 （請參閱 「 註解。"）|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|指定的目錄名稱，並在驅動程式或資料來源不支援目錄。<br /><br /> 指定的結構描述名稱，且驅動程式或資料來源不支援結構描述。|  
|||驅動程式或資料來源不支援陳述式屬性 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 的目前設定的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 如需如何使用此函式所傳回的資訊，請參閱[使用的目錄資料](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 如果\* *PKTableName*包含資料表名稱， **SQLForeignKeys**傳回結果集，其中包含指定之資料表的主索引鍵和參考它的所有外部索引鍵。 在其他資料表中的外部索引鍵的清單不包含點至指定的資料表中的唯一條件約束的外部索引鍵。  
  
 如果\* *FKTableName*包含資料表名稱， **SQLForeignKeys**傳回結果集，其中包含所有外部索引鍵中指定的資料表，指向 其他資料表中的主索引鍵，它們參考其他資料表中的主索引鍵。 指定的資料表中的外部索引鍵的清單不包含參考其他資料表中的唯一條件約束的外部索引鍵。  
  
 如果兩個\* *PKTableName*並\* *FKTableName*包含資料表名稱**SQLForeignKeys**傳回指定之資料表中的外部索引鍵在  \* *FKTableName*中指定之資料表的主索引鍵，請參閱 **PKTableName*。 這應該最多是一個索引鍵。  
  
> [!NOTE]  
>  如需一般用途、 引數和 ODBC 目錄函數的傳回的資料的詳細資訊，請參閱[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLForeignKeys**做為標準的結果集傳回的結果。 如果要求的主索引鍵相關聯的外部索引鍵，結果集被依 FKTABLE_CAT、 FKTABLE_SCHEM、 FKTABLE_NAME 和 key_seq 來排序。 如果要求的外部索引鍵相關聯的主索引鍵，結果集被依 PKTABLE_CAT、 PKTABLE_SCHEM、 PKTABLE_NAME&AMP;LT 和 key_seq 來排序。 下表列出結果集內的資料行。  
  
 VARCHAR 資料行的長度不會顯示在表格中，實際長度取決於資料來源。 若要判斷 PKTABLE_CAT 或 FKTABLE_CAT、 PKTABLE_SCHEM 或 FKTABLE_SCHEM 的實際長度，PKTABLE_NAME&AMP;LT 或 FKTABLE_NAME 和 PKCOLUMN_NAME FKCOLUMN_NAME 資料行，應用程式可以呼叫**SQLGetInfo** SQL_MAX_ 與CATALOG_NAME_LEN、 SQL_MAX_SCHEMA_NAME_LEN、 SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項。  
  
 下列資料行已重新命名為 ODBC 3 *。 x。* 因為應用程式繫結的資料行編號的資料行名稱變更不會影響回溯相容性。  
  
|ODBC 2.0 資料行|ODBC 3 *.x*資料行|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 下表列出結果集內的資料行。 超過 14 （< 備註 >） 的資料行的其他資料行可以驅動程式所定義。 應用程式應該透過從結果集而不是指定明確的序數位置的結尾算起往下取得驅動程式特有的資料行權限。 如需詳細資訊，請參閱 <<c0> [ 目錄函式所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|主索引鍵資料表目錄名稱;如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 沒有目錄這些資料表。|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|主索引鍵資料表的結構描述名稱;如果不適用於資料來源，則為 NULL。 如果驅動程式支援結構描述對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 並沒有結構描述這些資料表。|  
|PKTABLE_NAME&AMP;LT (ODBC 1.0)|3|非 NULL Varchar|主索引鍵資料表名稱。|  
|PKCOLUMN_NAME (ODBC 1.0)|4|非 NULL Varchar|主索引鍵資料行名稱。 驅動程式會傳回沒有名稱的資料行的空字串。|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|外部索引鍵資料表目錄名稱;如果不適用於資料來源，則為 NULL。 如果驅動程式支援目錄對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 沒有目錄這些資料表。|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|外部索引鍵的資料表結構描述名稱;如果不適用於資料來源，則為 NULL。 如果驅動程式支援結構描述對於某些資料表，但不適用於其他項目，例如當驅動程式會擷取不同 Dbms 中的資料，它會傳回空字串 ("") 並沒有結構描述這些資料表。|  
|FKTABLE_NAME (ODBC 1.0)|7|非 NULL Varchar|外部索引鍵資料表名稱。|  
|FKCOLUMN_NAME (ODBC 1.0)|8|非 NULL Varchar|外部索引鍵資料行名稱。 驅動程式會傳回沒有名稱的資料行的空字串。|  
|KEY_SEQ 來排序 (ODBC 1.0)|9|Smallint 非 NULL|（從 1 開始） 的索引鍵資料行順序編號。|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|當 SQL 作業是套用至外部索引鍵的動作**更新**。 可以有下列值之一。 （參考的資料表是具有主索引鍵的資料表，參考的資料表會具有外部索引鍵的資料表）。<br /><br /> SQL_NO_ACTION:當更新所參考之資料表的主索引鍵時，也會更新參考資料表的外部索引鍵。<br /><br /> SQL_NO_ACTION:如果所參考之資料表的主索引鍵更新會導致參考資料表中的 < 懸吊參考 > （也就是參考資料表中的資料列會有任何對應項目中參考的資料表），就會拒絕更新。 如果參考資料表的外部索引鍵更新會導入值做為參考資料表的主索引鍵的值不存在，則會拒絕更新。 (這個動作等同於 ODBC 2 SQL_RESTRICT 動作 *.x*。)<br /><br /> SQL_SET_NULL:對應至已變更元件的主索引鍵的外部索引鍵參考資料表中的元件時參考的資料表中的一或多個資料列會更新的方式，會變更的主索引鍵的一或多個元件，都會在所有設為 NULL參考資料表的相符的資料列。<br /><br /> SQL_SET_DEFAULT:當參考資料表中的一或多個資料列會更新的方式，會變更的主索引鍵的一或多個元件時，對應至已變更元件的主索引鍵的外部索引鍵參考資料表中的元件會設定為 applicable 參考資料表的所有相符的資料列中的預設值。<br /><br /> 如果不適用於資料來源，則為 NULL。|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|當 SQL 作業是套用至外部索引鍵的動作**刪除**。 可以有下列值之一。 （參考的資料表是具有主索引鍵的資料表，參考的資料表會具有外部索引鍵的資料表）。<br /><br /> SQL_NO_ACTION:刪除參考的資料表中的資料列時，會一併刪除參考的資料表中的所有相符資料列。<br /><br /> SQL_NO_ACTION:如果參考的資料表中的資料列刪除會導致 「 懸吊參考 」 參考資料表中的 （也就是參考資料表中的資料列會有任何對應項目中參考的資料表），就會拒絕更新。 (這個動作等同於 ODBC 2 SQL_RESTRICT 動作 *.x*。)<br /><br /> SQL_SET_NULL:參考的資料表中的一或多個資料列已刪除時，參考資料表的外部索引鍵的每個元件設為 NULL 參考資料表的所有相符的資料列中。<br /><br /> SQL_SET_DEFAULT:刪除參考的資料表中的一或多個資料列，每個元件的參考資料表的外部索引鍵設為適用的預設值，在參考資料表的所有相符的資料列。<br /><br /> 如果不適用於資料來源，則為 NULL。|  
|FK_NAME (ODBC 2.0)|12|Varchar|外部索引鍵的名稱。 如果不適用於資料來源，則為 NULL。|  
|PK_NAME (ODBC 2.0)|13|Varchar|主索引鍵的名稱。 如果不適用於資料來源，則為 NULL。|  
|延遲性 (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED，SQL_INITIALLY_IMMEDIATE，SQL_NOT_DEFERRABLE。|  
  
## <a name="code-example"></a>程式碼範例  
 下表所示，此範例會使用名為訂單、 線條和客戶的三個資料表。  
  
|訂單|程式行|客戶|  
|------------|-----------|---------------|  
|訂單編號|訂單編號|CUSTID|  
|CUSTID|程式行|NAME|  
|OPENDATE|PARTID|地址|  
|銷售人員|數量|電話|  
|STATUS|||  
  
 在 「 訂單 」 資料表，CUSTID 會識別已發生之銷售者的客戶。 它是指 CUSTID CUSTOMERS 資料表中的外部索引鍵。  
  
 在 [線條] 資料表中，訂單編號會識別與明細項目相關聯的銷售訂單。 它是指訂單編號，ORDERS 資料表中的外部索引鍵。  
  
 這個範例會呼叫**SQLPrimaryKeys**取得 「 訂單 」 資料表的主索引鍵。 結果集中會有一個資料列;下表顯示重要的資料行。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|訂單|訂單編號|1|  
  
 接下來，此範例會呼叫**SQLForeignKeys**以取得其他參考的 「 訂單 」 資料表的主索引鍵的資料表中的外部索引鍵。 結果集中會有一個資料列;下表顯示重要的資料行。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|訂單|CUSTID|程式行|CUSTID|1|  
  
 最後，此範例會呼叫**SQLForeignKeys**取得 「 訂單 」 資料表中參考其他資料表的主索引鍵的外部索引鍵。 結果集中會有一個資料列;下表顯示重要的資料行。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|客戶|CUSTID|訂單|CUSTID|1|  
  
```  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|擷取單一資料列或順向方向中的資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料的區塊，或捲動結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主索引鍵資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|傳回資料表的統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
