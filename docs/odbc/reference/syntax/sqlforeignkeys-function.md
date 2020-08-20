---
description: SQLForeignKeys 函數
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 802153837d53c6886b44511fbdffe6efa6b83281
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491301"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLForeignKeys** 可以傳回：  
  
-   指定之資料表中的外鍵清單 (指定之資料表中的資料行，這些資料行會參考其他資料表) 中的主鍵。  
  
-   其他資料表中參考指定資料表之主鍵的外鍵清單。  
  
 驅動程式會傳回每個清單，做為指定之語句的結果集。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
 輸出語句控制碼。  
  
 *Sqlforeignkeys*  
 輸出主鍵資料表目錄名稱。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示這些資料表沒有目錄。 *Sqlforeignkeys* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *sqlforeignkeys* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *sqlforeignkeys* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。 如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 輸出**Sqlforeignkeys*的長度（以字元為單位）。  
  
 *PKSchemaName*  
 輸出主鍵資料表架構名稱。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示那些沒有架構的資料表。 *PKSchemaName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *PKSchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *PKSchemaName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength2*  
 輸出**PKSchemaName*的長度（以字元為單位）。  
  
 *PKTableName*  
 輸出主鍵資料表名稱。 *PKTableName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *PKTableName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *PKTableName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength3*  
 輸出**PKTableName*的長度（以字元為單位）。  
  
 *FKCatalogName*  
 輸出外鍵資料表目錄名稱。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示這些資料表沒有目錄。 *FKCatalogName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *FKCatalogName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *FKCatalogName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength4*  
 輸出**FKCatalogName*的長度（以字元為單位）。  
  
 *FKSchemaName*  
 輸出外鍵資料表架構名稱。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示那些沒有架構的資料表。 *FKSchemaName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *FKSchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *FKSchemaName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength5*  
 輸出**FKSchemaName*的長度（以字元為單位）。  
  
 *FKTableName*  
 輸出外鍵資料表名稱。 *FKTableName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *FKTableName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *FKTableName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength6*  
 輸出**FKTableName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLForeignKeys**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLForeignKeys** 通常會傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在 *StatementHandle*上開啟了資料指標，且已呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 如果 **SQLFetch** 或 **SQLFetchScroll** 尚未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果 **SQLFetch** 或 **SQLFetchScroll** 已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 在 *StatementHandle*上開啟了資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。|  
|40001|序列化失敗|交易已復原，因為另一個交易發生資源鎖死。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 已呼叫函式，並在它完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** ，然後在*StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效| (DM) 引數 *PKTableName* 和 *FKTableName* 都是 null 指標。<br /><br /> SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE、 *FKCatalogName* 或 *sqlforeignkeys* 引數為 null 指標，且 SQL_CATALOG_NAME *InfoType* 會傳回支援的目錄名稱。<br /><br />  (DM) SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，且 *FKSchemaName*、 *PKSchemaName*、 *FKTableName*或 *PKTableName* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 SQLForeignKeys 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。|  
|||其中一個名稱長度引數的值超過對應名稱的最大長度值。  (請參閱「批註」。) |  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|指定了目錄名稱，而驅動程式或資料來源不支援目錄。<br /><br /> 指定了架構名稱，而驅動程式或資料來源不支援架構。|  
|||驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而且 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回結果集之前過期。 Timeout 期限是透過 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 如需有關如何使用此函數所傳回信息的詳細資訊，請參閱 [目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 如果 \* *PKTableName*包含資料表名稱， **SQLForeignKeys**會傳回結果集，其中包含指定之資料表的主鍵，以及參考該資料表的所有外鍵。 其他資料表中的外鍵清單不包含在指定資料表中指向 unique 條件約束的外鍵。  
  
 如果 \* *FKTableName*包含資料表名稱， **SQLForeignKeys**會傳回結果集，其中包含指定資料表中指向其他資料表之主鍵的所有外鍵，以及它們所參考的其他資料表中的主鍵。 指定之資料表中的外鍵清單未包含參考其他資料表中 unique 條件約束的外鍵。  
  
 如果 \* *PKTableName*和 \* *FKTableName*都包含資料表名稱， **SQLForeignKeys**會傳回 FKTableName 中指定之資料表的外鍵，該資料表表示 \* *FKTableName* **PKTableName*中指定之資料表的主鍵。 這應該是最多一個索引鍵。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱 [目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQLForeignKeys** 會以標準結果集的形式傳回結果。 如果要求與主鍵相關聯的外鍵，則會依 FKTABLE_CAT、FKTABLE_SCHEM、FKTABLE_NAME 和 KEY_SEQ 來排序結果集。 如果要求與外鍵相關聯的主鍵，則會依 PKTABLE_CAT、PKTABLE_SCHEM、PKTABLE_NAME 和 KEY_SEQ 來排序結果集。 下表列出結果集中的資料行。  
  
 VARCHAR 資料行的長度不會顯示在資料表中;實際的長度取決於資料來源。 若要判斷 PKTABLE_CAT 的實際長度或 FKTABLE_CAT、PKTABLE_SCHEM 或 FKTABLE_SCHEM、PKTABLE_NAME 或 FKTABLE_NAME，以及 PKCOLUMN_NAME 或 FKCOLUMN_NAME 資料行，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN 和 SQL_MAX_COLUMN_NAME_LEN 選項來呼叫 **SQLGetInfo** 。  
  
 已重新命名 ODBC 3.x 的下列資料行 *。* 資料行名稱的變更不會影響回溯相容性，因為應用程式會依資料行編號進行系結。  
  
|ODBC 2.0 資料行|ODBC 3.x*資料行*|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 下表列出結果集中的資料行。 除了資料行14以外的其他資料行 (備註) 可以由驅動程式定義。 應用程式應該從結果集的結尾算下，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱 [目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0) |1|Varchar|主鍵資料表目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄，例如當驅動程式從不同 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串 ( "" ) 。|  
|PKTABLE_SCHEM (ODBC 1.0) |2|Varchar|主鍵資料表架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則會針對沒有架構的資料表傳回空字串 ( "" ) 。|  
|PKTABLE_NAME (ODBC 1.0) |3|Varchar not Null|主鍵資料表名稱。|  
|PKCOLUMN_NAME (ODBC 1.0) |4|Varchar not Null|主要索引鍵資料行名稱。 驅動程式會針對沒有名稱的資料行傳回空字串。|  
|FKTABLE_CAT (ODBC 1.0) |5|Varchar|外鍵資料表目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄，例如當驅動程式從不同 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串 ( "" ) 。|  
|FKTABLE_SCHEM (ODBC 1.0) |6|Varchar|外鍵資料表架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則會針對沒有架構的資料表傳回空字串 ( "" ) 。|  
|FKTABLE_NAME (ODBC 1.0) |7|Varchar not Null|外鍵資料表名稱。|  
|FKCOLUMN_NAME (ODBC 1.0) |8|Varchar not Null|外鍵資料行名稱。 驅動程式會針對沒有名稱的資料行傳回空字串。|  
|KEY_SEQ (ODBC 1.0) |9|Smallint 非 NULL|從 1) 開始，索引鍵 (中的資料行序號。|  
|UPDATE_RULE (ODBC 1.0) |10|Smallint|當 SQL 作業 **更新**時，要套用至外鍵的動作。 可以具有下列其中一個值。  (參考的資料表是具有主鍵的資料表;參考資料表是具有外鍵的資料表。 ) <br /><br /> SQL_CASCADE：當更新參考資料表的主鍵時，也會更新參考資料表的外鍵。<br /><br /> SQL_NO_ACTION：如果參考資料表的主鍵更新在參考資料表中造成「無關聯參考」， (也就是說，參考資料表中的資料列在參考的資料表) 中沒有任何對應項，則會拒絕更新。 如果參考資料表的外鍵更新會產生一個值，而這個值不是被參考資料表之主鍵的值，則會拒絕更新。  (此動作與 ODBC 2.x 中的 SQL_RESTRICT 動作*相同。 ) *<br /><br /> SQL_SET_Null：當參考資料表中的一個或多個資料列更新時，如果變更了一個或多個主鍵的元件，則在參考資料表中對應至變更元件的外鍵元件的元件會在參考資料表的所有相符資料列中設定為 Null。<br /><br /> SQL_SET_DEFAULT：當參考資料表中的一個或多個資料列更新時，如果變更了一個或多個主鍵的元件，則參考資料表中對應至主鍵變更元件的外鍵元件，會在參考資料表的所有相符資料列中設定為適用的預設值。<br /><br /> 如果不適用於資料來源，則為 Null。|  
|DELETE_RULE (ODBC 1.0) |11|Smallint|當 SQL 作業 **刪除**時，要套用至外鍵的動作。 可以具有下列其中一個值。  (參考的資料表是具有主鍵的資料表;參考資料表是具有外鍵的資料表。 ) <br /><br /> SQL_CASCADE：當刪除參考資料表中的資料列時，也會一併刪除參考資料表中所有相符的資料列。<br /><br /> SQL_NO_ACTION：如果在參考資料表中刪除資料列時，會在參考資料表中造成「無關聯參考」 (也就是說，參考資料表中的資料列在參考的資料表) 中沒有任何對應項，則會拒絕更新。  (此動作與 ODBC 2.x 中的 SQL_RESTRICT 動作*相同。 ) *<br /><br /> SQL_SET_Null：當刪除所參考資料表中的一個或多個資料列時，參考資料表中所有相符資料列的參考資料表之外鍵的每個元件都會設定為 Null。<br /><br /> SQL_SET_DEFAULT：當刪除參考資料表中的一個或多個資料列時，參考資料表之外鍵的每個元件都會在參考資料表的所有相符資料列中設定為適用的預設值。<br /><br /> 如果不適用於資料來源，則為 Null。|  
|FK_NAME (ODBC 2.0) |12|Varchar|外鍵名稱。 如果不適用於資料來源，則為 Null。|  
|PK_NAME (ODBC 2.0) |13|Varchar|主要索引鍵名稱。 如果不適用於資料來源，則為 Null。|  
|DEFERRABILITY (ODBC 3.0) |14|Smallint|SQL_INITIALLY_DEFERRED、SQL_INITIALLY_IMMEDIATE SQL_NOT_DEFERRABLE。|  
  
## <a name="code-example"></a>程式碼範例  
 如下表所示，此範例使用三個數據表，名為 ORDERS、LINES 和 CUSTOMERS。  
  
|訂單|線|客戶|  
|------------|-----------|---------------|  
|分組|分組|CUSTID|  
|CUSTID|線|NAME|  
|OPENDATE|PARTID|位址|  
|售貨員|數量|電話|  
|狀態|||  
  
 在 ORDERS 資料表中，CUSTID 會識別已進行銷售的客戶。 這是參考 CUSTOMERS 資料表中 CUSTID 的外鍵。  
  
 在 [行] 資料表中，[訂單識別碼] 會識別與明細專案相關聯的銷售訂單。 這是參考 ORDERS 資料表中之訂單的外鍵。  
  
 這個範例會呼叫 **SQLPrimaryKeys** 來取得 ORDERS 資料表的主鍵。 結果集將會有一個資料列;下表顯示重要的資料行。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|訂單|分組|1|  
  
 接下來，此範例會呼叫 **SQLForeignKeys** 來取得其他資料表中的外鍵，以參考 ORDERS 資料表的主鍵。 結果集將會有一個資料列;下表顯示重要的資料行。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|訂單|CUSTID|線|CUSTID|1|  
  
 最後，此範例會呼叫 **SQLForeignKeys** ，以取得 ORDERS 資料表中參考其他資料表之主鍵的外鍵。 結果集將會有一個資料列;下表顯示重要的資料行。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|客戶|CUSTID|訂單|CUSTID|1|  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主要索引鍵的資料行|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|傳回資料表統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
