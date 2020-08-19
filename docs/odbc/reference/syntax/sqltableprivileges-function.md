---
description: SQLTablePrivileges 函數
title: SQLTablePrivileges 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf50953a42d9a7557e3f57ebaa749f3cd116a0d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421052"
---
# <a name="sqltableprivileges-function"></a>SQLTablePrivileges 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ODBC  
  
 **總結**  
 **SQLTablePrivileges** 會傳回資料表清單以及與每個資料表相關聯的許可權。 驅動程式會將資訊傳回為指定之語句上的結果集。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *CatalogName*  
 輸出資料表目錄。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示這些資料表沒有目錄。 *CatalogName* 不能包含字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *CatalogName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *CatalogName* 是一般的引數;它是以真正的方式處理，而其大小寫相當重要。 如需詳細資訊，請參閱 [目錄函數中的引數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 輸出**CatalogName*的長度（以字元為單位）。  
  
 *SchemaName*  
 輸出架構名稱的字串搜尋模式。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則空字串 ( "" ) 表示那些沒有架構的資料表。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *SchemaName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *SchemaName* 就是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength2*  
 輸出**SchemaName*的長度（以字元為單位）。  
  
 *名*  
 輸出資料表名稱的字串搜尋模式。  
  
 如果 SQL_ATTR_METADATA_ID 語句屬性設定為 SQL_TRUE， *TableName* 會被視為識別碼，而其大小寫並不重要。 如果 SQL_FALSE， *TableName* 是模式值引數;它是以真正的方式處理，而其大小寫相當重要。  
  
 *NameLength3*  
 輸出**TableName*的長度（以字元為單位）。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLTablePrivileges**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLTablePrivileges** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|24000|指標狀態無效|在 *StatementHandle*上開啟了資料指標，且已呼叫 **SQLFetch** 或 **SQLFetchScroll** 。 如果 **SQLFetch** 或 **SQLFetchScroll** 尚未傳回 SQL_NO_DATA，驅動程式管理員會傳回此錯誤，如果 **SQLFetch** 或 **SQLFetchScroll** 已傳回 SQL_NO_DATA，驅動程式會傳回此錯誤。<br /><br /> 在 *StatementHandle*上開啟了資料指標，但尚未呼叫 **SQLFetch** 或 **SQLFetchScroll** 。|  
|40001|序列化失敗|因為另一個交易發生資源鎖死，所以已回復交易。|  
|40003|語句完成不明|在此函數執行期間，相關聯的連接失敗，而且無法判斷交易的狀態。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫**SQLTablePrivileges**函式，並在它完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後，在*StatementHandle*上再次呼叫**SQLTablePrivileges**函數。<br /><br /> 呼叫**SQLTablePrivileges**函式，並在它完成執行之前，從多執行緒應用程式中的不同執行緒呼叫*StatementHandle*上的**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效|SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE、 *CatalogName* 引數為 null 指標，且 SQL_CATALOG_NAME *InfoType* 會傳回支援的目錄名稱。<br /><br />  (DM) SQL_ATTR_METADATA_ID 語句屬性已設定為 SQL_TRUE，且 *SchemaName* 或 *TableName* 引數為 null 指標。|  
|HY010|函數順序錯誤| (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 **SQLTablePrivileges** 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。<br /><br /> 針對*StatementHandle*呼叫 (DM) **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送所有資料執行中參數或資料行的資料之前，會呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY090|不正確字串或緩衝區長度| (DM) 其中一個名稱長度引數的值小於0，但不等於 SQL_NTS。<br /><br /> 其中一個名稱長度引數的值超過對應辨識符號或名稱的最大長度值。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未執行選用功能|已指定目錄，且驅動程式或資料來源不支援目錄。<br /><br /> 指定了架構，而驅動程式或資料來源不支援架構。<br /><br /> 為數據表架構、資料表名稱或資料行名稱指定了字串搜尋模式，且資料來源不支援一或多個這些引數的搜尋模式。<br /><br /> 驅動程式或資料來源不支援 SQL_ATTR_CONCURRENCY 和 SQL_ATTR_CURSOR_TYPE 語句屬性的目前設定組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS 語句屬性已設定為 SQL_UB_VARIABLE，而且 SQL_ATTR_CURSOR_TYPE 語句屬性已設定為驅動程式不支援書簽的資料指標類型。|  
|HYT00|已超過逾時的設定|查詢超時時間已在資料來源傳回結果集之前過期。 Timeout 期限是透過 **SQLSetStmtAttr**、SQL_ATTR_QUERY_TIMEOUT 設定。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
## <a name="comments"></a>註解  
 *SchemaName*和*TableName*引數接受搜尋模式。 如需有效搜尋模式的詳細資訊，請參閱 [模式值引數](../../../odbc/reference/develop-app/pattern-value-arguments.md)。  
  
 **SQLTablePrivileges** 會將結果傳回為標準結果集，並依 TABLE_CAT、TABLE_SCHEM、TABLE_NAME、許可權和被授與者排序。  
  
 若要判斷 TABLE_CAT、TABLE_SCHEM 和 TABLE_NAME 資料行的實際長度，應用程式可以使用 SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN 和 SQL_MAX_TABLE_NAME_LEN 選項來呼叫 **SQLGetInfo** 。  
  
> [!NOTE]  
>  如需 ODBC 目錄函數的一般使用、引數和傳回資料的詳細資訊，請參閱 [目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 已重新命名 ODBC 3.x 的下列資料*行。* 資料行名稱的變更不會影響回溯相容性，因為應用程式會依資料行編號進行系結。  
  
|ODBC 2.0 資料行|ODBC *3.x* 資料行|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 下表列出結果集中的資料行。 資料行7以外的其他資料行 (IS_GRANTABLE) 可以由驅動程式定義。 應用程式應該從結果集的結尾算下，而不是指定明確的序數位置，藉以取得驅動程式特定資料行的存取權。 如需詳細資訊，請參閱 [目錄函數所傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0) |1|Varchar|目錄名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的目錄，但不支援其他資料表的目錄，例如當驅動程式從不同 Dbms 抓取資料時，它會針對沒有目錄的那些資料表傳回空字串 ( "" ) 。|  
|TABLE_SCHEM (ODBC 1.0) |2|Varchar|架構名稱;如果不適用於資料來源，則為 Null。 如果驅動程式支援某些資料表的架構，但不支援其他資料表的架構（例如，當驅動程式從不同 Dbms 抓取資料時），則會針對沒有架構的資料表傳回空字串 ( "" ) 。|  
|TABLE_NAME (ODBC 1.0) |3|Varchar not Null|資料表名稱。|  
| (ODBC 1.0) 的授權者|4|Varchar|授與許可權的使用者名稱;如果不適用於資料來源，則為 Null。<br /><br /> 針對被授與者資料行中的值是物件擁有者的所有資料列，「授與者」資料行將會是「_SYSTEM」。|  
|被授與者 (ODBC 1.0) |5|Varchar not Null|授與許可權之使用者的名稱。|  
| (ODBC 1.0) 的許可權|6|Varchar not Null|資料表許可權。 可能是下列其中一項，或是資料來源特定的許可權。<br /><br /> SELECT：允許被授與者抓取資料表中一或多個資料行的資料。<br /><br /> INSERT：被授與者可以將包含一或多個資料行之資料的新資料列插入資料表中。<br /><br /> UPDATE：允許被授與者更新資料表中一或多個資料行的資料。<br /><br /> DELETE：允許被授與者從資料表中刪除資料列。<br /><br /> 參考：被授與者可以參考條件約束內資料表的一或多個資料行 (例如，唯一、參考或資料表檢查條件約束) 。<br /><br /> 給定資料表許可權允許被授與者的動作範圍與資料來源相依。 例如，UPDATE 許可權可能會允許被授與者更新某個資料來源上資料表中的所有資料行，而且只有授與者在另一個資料來源上具有 UPDATE 許可權的資料行。|  
|IS_GRANTABLE (ODBC 1.0) |7|Varchar|指出是否允許被授與者將許可權授與其他使用者;如果未知或不適用於資料來源，則為 "YES"、"NO" 或 Null。<br /><br /> 許可權是可授與或非可授與，但不能同時是兩者。 **SQLColumnPrivileges**所傳回的結果集會永遠沒有包含兩個數據列，但 IS_GRANTABLE 資料行以外的所有資料行都包含相同的值。|  
  
## <a name="code-example"></a>程式碼範例  
 如需類似功能的程式碼範例，請參閱 [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區系結至結果集內的資料行|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|傳回資料行或資料行的許可權|[SQLColumnPrivileges 函式](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|傳回資料表或資料表中的資料行|[SQLColumns 函式](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|以順向方向提取單一資料列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|提取資料區塊或滾動整個結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回資料表統計資料和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|傳回資料來源中的資料表清單|[SQLTables 函式](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
