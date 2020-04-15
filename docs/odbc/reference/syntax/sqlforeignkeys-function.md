---
title: SQL 外鍵功能 |微軟文件
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
ms.openlocfilehash: 5f2769fb378a5ee989fb6a0351537edb3de03469
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285858"
---
# <a name="sqlforeignkeys-function"></a>SQLForeignKeys 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQL 外鍵**可以返回:  
  
-   指定表中的外鍵清單(指定表中引用其他表中主鍵的列)。  
  
-   引用指定表中的主鍵的其他表中的外鍵的清單。  
  
 驅動程式返回每個清單作為指定語句上的結果集。  
  
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
 *語句句柄*  
 [輸入]語句句柄。  
  
 *PK目錄名稱*  
 [輸入]主鍵表目錄名稱。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),空字串("")表示那些沒有目錄的表。 *PK目錄名稱*不能包含字串搜索模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*則 PKCatalogName*被視為識別碼,其大小寫不重要。 如果*SQL_FALSE,PKCatalogName*是一個普通的參數;如果是SQL_FALSE,則 PKCatalogName 是一個普通參數。它被從字面上處理,它的情況很重要。 有關詳細資訊,請參閱[目錄函數 中的參數](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *NameLength1*  
 [輸入]長度 =*PK目錄名稱*,以字元表示。  
  
 *PKSchema 名稱*  
 [輸入]主鍵表架構名稱。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串("")表示那些沒有架構的表。 *PKSchemaName*不能包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為*SQL_TRUE,PKSchemaName*將被視為識別碼,其大小寫不重要。 如果*SQL_FALSE,PKSchemaName*是一個普通的參數;如果是SQL_FALSE,則 PKSchemaName 是一個普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度2*  
 [輸入]長度 =*PKSchema 名稱*,以字元表示。  
  
 *PKTable 名稱*  
 [輸入]主鍵表名稱。 *PKTableName*不能包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設置為*SQL_TRUE,PKTableName*將被視為識別碼,其大小寫不重要。 如果是SQL_FALSE,PKTableName 是一個普通的參數;如果是,*則 PKTableName*是一個普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度3*  
 [輸入]長度 =*PKTableName*,以字元表示。  
  
 *FK 目錄名稱*  
 [輸入]外鍵表目錄名稱。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),空字串("")表示那些沒有目錄的表。 *FKCatalogName*無法包含字串搜尋模式。  
  
 如果將SQL_ATTR_METADATA_ID語句屬性設置為SQL_TRUE,*則 FKCatalogName*將被視為識別符,其大小寫不重要。 如果SQL_FALSE,FKCatalogName 是一個普通的參數;如果是,*則為「FKCatalogName」,* 它是一個普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度4*  
 [輸入]長度 =*FKCatalog 名稱*,以字元表示。  
  
 *FKSchema 名稱*  
 [輸入]外鍵表架構名稱。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),則空字串("")表示那些沒有架構的表。 *FKSchemaName*無法包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID敘述屬性設定為SQL_TRUE,*則 FKSchemaName*將被視為識別符,其大小寫不重要。 如果SQL_FALSE,FKSchemaName 是一個普通的參數;如果是SQL_FALSE,*則 FKSchemaName*是一個普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度5*  
 [輸入]長度 =*FKSchema 名稱*,以字元表示。  
  
 *FKTable 名稱*  
 [輸入]外鍵表名稱。 *FKTableName*無法包含字串搜尋模式。  
  
 如果SQL_ATTR_METADATA_ID語句屬性設定為SQL_TRUE,*則 FKTableName*被視為識別碼,其大小寫不重要。 如果是SQL_FALSE,FKTableName 是一個普通的參數;如果是SQL_FALSE,*則 FKTableName*是一個普通參數。它被從字面上處理,它的情況很重要。  
  
 *名稱長度6*  
 [輸入]長度 =*FKTableName*,以字元表示。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQL 外鍵**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的**句柄*。 下表列出了**SQLOfKeys**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
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
|HY009|不合法的空白指標|(DM) 參數*PKTableName*和*FKTableName*都是空指標。<br /><br /> SQL_ATTR_METADATA_ID語句屬性設定為*SQL_TRUE,FKCatalogName*或*PKCatalogName*參數為空指標,SQL_CATALOG_NAME *InfoType*返回目錄名稱受支援。<br /><br /> (DM) SQL_ATTR_METADATA_ID文句屬性設定為*SQL_TRUE,FKSchema 名稱**、PKSchema 名稱**、FKTableName*或*PKTableName*參數為空指標。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用 SQL 外鍵函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY090|不合法的字串或緩衝區長度|(DM) 其中一個名稱長度參數的值小於 0,但不等於SQL_NTS。|  
|||其中一個名稱長度參數的值超過相應名稱的最大長度值。 (請參閱"註釋」。。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|指定了目錄名稱,並且驅動程式或數據源不支援目錄。<br /><br /> 指定了架構名稱,驅動程式或數據源不支援架構。|  
|||驅動程式或數據來源不支援SQL_ATTR_CONCURRENCY和SQL_ATTR_CURSOR_TYPE語句屬性的當前設置的組合。<br /><br /> SQL_ATTR_USE_BOOKMARKS語句屬性設置為SQL_UB_VARIABLE,SQL_ATTR_CURSOR_TYPE語句屬性設置為驅動程式不支援書籤的游標類型。|  
|HYT00|已超過逾時的設定|查詢超時期限在數據源返回結果集之前已過期。 超時期間通過**sqlSetStmtAttr**SQL_ATTR_QUERY_TIMEOUT設置。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 有關如何使用此函數傳回的資訊的資訊,請參考[目錄資料的使用](../../../odbc/reference/develop-app/uses-of-catalog-data.md)。  
  
 如果\* *PKTableName*包含表名 **,SQLOfKey**將傳回一個結果集,其中包含指定表的主鍵和引用它的所有外鍵。 其他表中的外鍵清單不包括指向指定表中的唯一約束的外鍵。  
  
 如果\* *FKTableName*包含表名 **,SQL 外鍵**將傳回一個結果集,其中包含指定表中指向其他表中的主鍵的所有外鍵及其引用的其他表中的主鍵。 指定表中的外鍵清單不包含引用其他表中的唯一約束的外鍵。  
  
 如果\**PKTableName*\*和*FKTableName*都包含表名 **,SQLOfkey**將傳回\**FKTableName*中指定的表中指定的外鍵,該鍵引用 #*PKTableName*中指定的表的主鍵。 這最多應該是一個關鍵。  
  
> [!NOTE]  
>  有關 ODBC 目錄函數的一般使用、參數和傳回資料的詳細資訊,請參考[目錄函數](../../../odbc/reference/develop-app/catalog-functions.md)。  
  
 **SQL 外鍵**將結果作為標準結果集返回。 如果請求與主鍵關聯的外鍵,則結果集按FKTABLE_CAT、FKTABLE_SCHEM、FKTABLE_NAME和KEY_SEQ排序。 如果請求與外鍵關聯的主鍵,則結果集按PKTABLE_CAT、PKTABLE_SCHEM、PKTABLE_NAME和KEY_SEQ排序。 下表列出了結果集中的列。  
  
 VARCHAR 列的長度不顯示在表中;因此,VARCHAR 列的長度不顯示在表中。實際長度取決於數據源。 要確定PKTABLE_CAT或FKTABLE_CAT、PKTABLE_SCHEM或FKTABLE_SCHEM、PKTABLE_NAME或FKTABLE_NAME以及PKCOLUMN_NAME或FKCOLUMN_NAME列的實際長度,應用程式可以使用SQL_MAX_CATALOG_NAME_LEN、SQL_MAX_SCHEMA_NAME_LEN、SQL_MAX_TABLE_NAME_LEN和SQL_MAX_COLUMN_NAME_LEN選項調用**SQLGetInfo。**  
  
 以下列已重新命名為 ODBC 3 *.x。* 列名稱更改不會影響向後相容性,因為應用程式按列號綁定。  
  
|ODBC 2.0 欄|ODBC 3 *.x*欄|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 下表列出了結果集中的列。 驅動程式可以定義第 14 列 (註釋)以外的其他列。 應用程式應通過從結果集的末尾倒計時而不是指定顯式單位位置來獲得對特定於驅動程式的列的訪問許可權。 有關詳細資訊,請參閱[目錄函數傳回的資料](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)。  
  
|資料行名稱|資料行編號|資料類型|註解|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|主鍵表目錄名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有目錄的表。|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|主鍵表架構名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有架構的表。|  
|PKTABLE_NAME (ODBC 1.0)|3|瓦爾查爾不是 NULL|主鍵表名稱。|  
|PKCOLUMN_NAME (ODBC 1.0)|4|瓦爾查爾不是 NULL|主鍵列名稱。 驅動程式返回沒有名稱的列的空字串。|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|外鍵表目錄名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的目錄,但不支援其他表的目錄(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有目錄的表。|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|外鍵表架構名稱;如果不適用於資料源,則為 NULL。 如果驅動程式支援某些表的架構,但不支援其他表的架構(例如當驅動程式從不同的 DBMS 檢索資料時),它將返回一個空字串(""),用於那些沒有架構的表。|  
|FKTABLE_NAME (ODBC 1.0)|7|瓦爾查爾不是 NULL|外鍵表名稱。|  
|FKCOLUMN_NAME (ODBC 1.0)|8|瓦爾查爾不是 NULL|外鍵列名稱。 驅動程式返回沒有名稱的列的空字串。|  
|KEY_SEQ (ODBC 1.0)|9|Smallint 非 NULL|鍵中的列序列號(以 1 開頭)。|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|SQL 操作為**UPDATE**時要應用於外鍵的操作。 可以具有以下值之一。 (引用的表是具有主鍵的表;引用表是具有外鍵的表。<br /><br /> SQL_CASCADE:更新引用表的主鍵時,引用表的外鍵也會更新。<br /><br /> SQL_NO_ACTION:如果更新引用表的主鍵會導致引用表中的"懸空引用"(即引用表中的行在引用的表中沒有對應項),則更新將被拒絕。 如果引用表的外鍵更新將引入作為引用表的主鍵的值不存在的值,則拒絕更新。 (此操作與 ODBC 2 *.x 中的*SQL_RESTRICT操作相同。<br /><br /> SQL_SET_NULL:當引用表中的一個或多個行以更改主鍵的一個或多個元件的方式更新時,引用表中對應於主鍵更改元件的外鍵的元件將設置為引用表的所有匹配行中的 NULL。<br /><br /> SQL_SET_DEFAULT:當引用表中的一個或多個行以更改主鍵的一個或多個元件的方式更新時,引用表中對應於主鍵已更改元件的外鍵的元件將設置為引用表所有匹配行中的適用預設值。<br /><br /> 如果不適用於資料源,則為 NULL。|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|SQL 操作為**DELETE**時要應用於外鍵的操作。 可以具有以下值之一。 (引用的表是具有主鍵的表;引用表是具有外鍵的表。<br /><br /> SQL_CASCADE:刪除引用表中的行時,引用表中的所有匹配行也將被刪除。<br /><br /> SQL_NO_ACTION:如果刪除引用表中的行會導致引用表中的「懸空引用」(即引用表中的行在引用的表中沒有對應項),則更新將被拒絕。 (此操作與 ODBC 2 *.x 中的*SQL_RESTRICT操作相同。<br /><br /> SQL_SET_NULL:刪除引用表中的一個或多個行時,引用表的外鍵的每個元件都設置為引用表的所有匹配行中的 NULL。<br /><br /> SQL_SET_DEFAULT:刪除引用表中的一個或多個行時,引用表的外鍵的每個元件都設置為引用表所有匹配行中的適用預設值。<br /><br /> 如果不適用於資料源,則為 NULL。|  
|FK_NAME (ODBC 2.0)|12|Varchar|外鍵名稱。 如果不適用於資料源,則為 NULL。|  
|PK_NAME (ODBC 2.0)|13|Varchar|主鍵名稱。 如果不適用於資料源,則為 NULL。|  
|可延遲性(ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED,SQL_INITIALLY_IMMEDIATE,SQL_NOT_DEFERRABLE|  
  
## <a name="code-example"></a>程式碼範例  
 如下表所示,此示例使用三個表,名為 ORDERS、LINES 和客戶。  
  
|訂單|線|客戶|  
|------------|-----------|---------------|  
|訂單ID|訂單ID|CUSTID|  
|CUSTID|線|NAME|  
|開放日期|零件識別碼|位址|  
|售貨員|數量|電話|  
|狀態|||  
  
 在 ORDERS 表中,CUSTID 標識向其銷售的客戶。 它是在 CUSTOMERS 表中引用 CUSTID 的外鍵。  
  
 在 LINES 表中,ORDERID 標識與行物料關聯的銷售訂單。 它是在 ORDERS 表中引用 ORDERID 的外鍵。  
  
 此示例調用**SQL 主要密鑰**來獲取 ORDERS 表的主鍵。 結果集將有一行;結果集將具有一行。下表顯示了重要的列。  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|訂單|訂單ID|1|  
  
 接下來,該示例調用**SQLOfKey**來獲取引用 ORDERS 表主鍵的其他表中的外鍵。 結果集將有一行;結果集將具有一行。下表顯示了重要的列。  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|訂單|CUSTID|線|CUSTID|1|  
  
 最後,該示例調用**SQLOfKey**來獲取 ORDERS 表中引用其他表的主鍵的外鍵。 結果集將有一行;結果集將具有一行。下表顯示了重要的列。  
  
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
|將緩衝區繫結到結果集中的欄|[SQLBindCol 函數](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|以只轉寄方向取得單列或資料區塊|[SQLFetch 函式](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|取得資料塊或捲動瀏覽結果集|[SQLFetchScroll 函式](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|傳回主鍵的欄位|[SQLPrimaryKeys 函式](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|傳回表統計資訊和索引|[SQLStatistics 函式](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
