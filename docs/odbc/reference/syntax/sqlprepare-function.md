---
title: SQLPrepare 函數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLPrepare
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPrepare
helpviewer_keywords:
- SQLPrepare function [ODBC]
ms.assetid: 332e1b4b-b0ed-4e7a-aa4d-4f35f4f4476b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 292b1c4d9cd0281de610af4e53f25aa3d0ab6f90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005762"
---
# <a name="sqlprepare-function"></a>SQLPrepare 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLPrepare**準備執行的 SQL 字串。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLPrepare(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     StatementText,  
     SQLINTEGER    TextLength);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *StatementText*  
 [輸入]SQL 文字的字串。  
  
 *TextLength*  
 [輸入]長度 **StatementText*以字元為單位。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLPrepare**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLPrepare** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01S02|選項值已變更|指定的陳述式屬性是實作運作的情況，因為不正確的因此已暫時替代成類似的值。 (**SQLGetStmtAttr**可以呼叫以判斷其暫時已取代的值為何。)取代值是適用於*StatementHandle*直到關閉資料指標。 您可以變更的陳述式屬性是：SQL_ATTR_CONCURRENCY 設定 SQL_ATTR_CURSOR_TYPE SQL_ATTR_KEYSET_SIZE SQL_ATTR_MAX_LENGTH SQL_ATTR_MAX_ROWS SQL_ATTR_QUERY_TIMEOUT SQL_ATTR_SIMULATE_CURSOR<br /><br /> （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|21S01|插入的值清單不符合資料行清單|\**StatementText*包含**插入**陳述式，以及要插入的值數目不符，衍生資料表的程度。|  
|21S02|衍生資料表的程度與資料行清單不符|\**StatementText*包含**CREATE VIEW**陳述式和指定的名稱數目不是做為查詢規格所定義的衍生資料表相同的程度。|  
|22018|轉換規格的字元值無效|**StatementText*包含 SQL 陳述式包含的常值或參數，且值為與之相關聯的資料表資料行的資料類型不相容。|  
|22019|無效的逸出字元|引數*StatementText*包含**像是**述詞，以及**逸出**中**其中**子句和逸出的長度之後的字元**逸出**不是等於 1。|  
|22025|無效的逸出序列|引數*StatementText*包含 「**像是**_模式值_**逸出**_逸出字元_"中**其中**子句，並遵循模式值的逸出字元的字元不是"%"或"_"。|  
|24000|指標狀態無效|(DM) 上開啟游標的*StatementHandle*，並**SQLFetch**或是**SQLFetchScroll**呼叫。<br /><br /> 資料指標是開啟*StatementHandle*，但**SQLFetch**或是**SQLFetchScroll**尚未呼叫。|  
|34000|指標名稱無效|\**StatementText*包含定位**刪除**或定位**更新**，和正在準備的陳述式所參考的資料指標並未開啟。|  
|3D000|無效的目錄名稱|中指定的目錄名稱*StatementText*無效。|  
|3F000|無效的結構描述名稱|中指定的結構描述名稱*StatementText*無效。|  
|42000|語法錯誤或存取違規|\**StatementText*包含 SQL 陳述式不是 preparable 或包含語法錯誤。<br /><br /> **StatementText*包含使用者沒有必要的權限的陳述式。|  
|42S01|基底資料表或檢視已經存在|\**StatementText*包含**CREATE TABLE**或是**CREATE VIEW**陳述式和資料表名稱或檢視名稱已經存在。|  
|42S02|基底資料表或檢視找不到|\**StatementText*包含**DROP TABLE**或是**DROP VIEW**陳述式和指定的資料表名稱或檢視名稱不存在。<br /><br /> \**StatementText*包含**ALTER TABLE**陳述式和指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**CREATE VIEW**陳述式和資料表名稱或檢視查詢規格所定義的名稱不存在。<br /><br /> \**StatementText*包含**CREATE INDEX**陳述式和指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**GRANT**或是**撤銷**陳述式和指定的資料表名稱或檢視名稱不存在。<br /><br /> \**StatementText*包含**選取**陳述式和指定的資料表名稱或檢視名稱不存在。<br /><br /> \**StatementText*包含**刪除**，**插入**，或**更新**陳述式和指定的資料表名稱不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**陳述式，並指定條件約束 （參考資料表以外所建立） 中的資料表不存在。|  
|42S11|索引已經存在|\**StatementText*包含**CREATE INDEX**陳述式中，與指定的索引名稱已存在。|  
|42S12|找不到索引|\**StatementText*包含**DROP INDEX**陳述式和指定的索引名稱不存在。|  
|42S21|資料行已經存在|\**StatementText*包含**ALTER TABLE**陳述式，並在指定的資料行**新增**子句不是唯一的或識別現有的資料行在基底資料表中。|  
|42S22|找不到的資料行|\**StatementText*包含**CREATE INDEX**陳述式，和一或多個資料行清單中指定的名稱不存在的資料行。<br /><br /> \**StatementText*包含**GRANT**或是**撤銷**陳述式，並指定資料行名稱不存在。<br /><br /> \**StatementText*包含**選取**，**刪除**，**插入**，或**更新**陳述式，並指定資料行名稱不存在。<br /><br /> \**StatementText*包含**CREATE TABLE**陳述式，並指定條件約束 （參考資料表以外所建立） 中的資料行不存在。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*，並接著呼叫函式上再次*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|(DM) *StatementText*是 null 指標。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLPrepare**呼叫函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY090|字串或緩衝區長度無效|(DM) 引數*TextLength*小於或等於 0，但不是等於 SQL_NTS。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|類型的定義資料指標並行設定無效。<br /><br /> SQL_ATTR_USE_BOOKMARKS 陳述式屬性設定為 SQL_UB_VARIABLE，且 SQL_ATTR_CURSOR_TYPE 陳述式屬性已設定為驅動程式不支援書籤的資料指標類型。|  
|HYT00|已超過逾時的設定|在逾時期限到期之前的資料來源傳回結果集。 透過設定的逾時期限**SQLSetStmtAttr**，sql_attr_query_timeout 時。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 應用程式會呼叫**SQLPrepare**傳送來準備資料來源的 SQL 陳述式。 如需備妥的執行的詳細資訊，請參閱[已備妥執行](../../../odbc/reference/develop-app/prepared-execution-odbc.md)。 應用程式可以包含一或多個參數標記中的 SQL 陳述式。 若要包含的參數標記，應用程式會嵌入在適當的位置上的 SQL 字串的問號 （？）。 如需參數的資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
> [!NOTE]  
>  如果應用程式使用**SQLPrepare**準備並**SQLExecute**提交**認可**或**回復**陳述式，它不會DBMS 的產品之間的互通性。 若要認可或回復交易，呼叫**SQLEndTran**。  
  
 驅動程式可以修改要使用 SQL 資料來源所使用的形式，然後將它提交至資料來源來準備的陳述式。 特別是，驅動程式會修改用來定義特定功能的 SQL 語法的逸出序列。 (如需 SQL 陳述式語法的說明，請參閱[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)和[附錄 c:SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。)驅動程式，陳述式控制代碼是類似的陳述式識別項中內嵌的 SQL 程式碼。 如果資料來源支援陳述式的識別項，驅動程式可以傳送到資料來源的陳述式識別項和參數值。  
  
 備妥的陳述式之後，應用程式會使用參考至更新版本的函式呼叫的陳述式的陳述式控制代碼。 藉由呼叫可以重新執行陳述式控制代碼相關聯的已備妥之陳述式**SQLExecute**應用程式會釋放呼叫的陳述式直到**SQLFreeStmt** SQL_DROP 選項或等到陳述式控制代碼會在呼叫**SQLPrepare**， **SQLExecDirect**，或其中一個目錄函數 (**SQLColumns**， **SQLTables**等等)。 一旦應用程式會準備陳述式，它可以要求結果集的格式的相關資訊。 針對某些實作中，呼叫**SQLDescribeCol**或是**SQLDescribeParam**之後**SQLPrepare**可能不是那麼有效率，做為呼叫函式之後**SQLExecute**或是**SQLExecDirect**。  
  
 有些驅動程式無法傳回語法錯誤或存取違規，當應用程式會呼叫**SQLPrepare**。 驅動程式可以處理語法錯誤，並存取違規，只有語法錯誤，或不語法錯誤或存取違規。 因此，應用程式必須能夠處理這些狀況，例如呼叫後續相關函式時**SQLNumResultCols**， **SQLDescribeCol**， **SQLColAttribute**，並**SQLExecute**。  
  
 視驅動程式和資料來源的功能，而定 （如果所有參數都已繫都結），準備陳述式時，就可能會檢查參數資訊 （例如資料類型），或執行時 （如果所有參數都不已繫都都結）。 最大的互通性，應用程式應該解除繫結套用至舊的 SQL 陳述式之前準備新的 SQL 陳述式，在相同的陳述式上的所有參數。 這可避免因為舊套用到新的陳述式的參數資訊的錯誤。  
  
> [!IMPORTANT]  
>  認可交易，藉由明確呼叫**SQLEndTran**或藉由使用自動認可模式中，可能會導致要刪除的連接上所有陳述式的存取方案的資料來源。 如需詳細資訊，請參閱 SQL_CURSOR_COMMIT_BEHAVIOR SQL_CURSOR_ROLLBACK_BEHAVIOR 資訊中的和類型[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)並[影響的資料指標和已備妥的陳述式上交易](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md)。  
  
## <a name="code-example"></a>程式碼範例  
 請參閱[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)， [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)，並[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|配置陳述式控制代碼|[SQLAllocHandle 函式](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|繫結至結果集的資料行的緩衝區|[SQLBindCol 函式](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|繫結至參數的緩衝區|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行認可或復原作業|[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回陳述式所影響的資料列的數目|[SQLRowCount 函式](../../../odbc/reference/syntax/sqlrowcount-function.md)|  
|設定資料指標名稱|[SQLSetCursorName 函式](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
