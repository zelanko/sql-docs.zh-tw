---
title: SQLGetDiagField 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagField
helpviewer_keywords:
- SQLGetDiagField function [ODBC]
ms.assetid: 1dbc4398-97a8-4585-bb77-1f7ea75e24c4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13ab95c762573be002782c06615fc6f01317499f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63258806"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函數

**合規性**  
 導入的版本：ODBC 3.0 版的標準合規性：ISO 92  
  
 **摘要**  
 **SQLGetDiagField**傳回目前的診斷資料結構 （與指定的控制代碼相關聯），其中包含錯誤、 警告和狀態資訊的記錄欄位的值。  
  
## <a name="syntax"></a>語法  
  
```cpp
SQLRETURN SQLGetDiagField(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     DiagIdentifier,  
     SQLPOINTER      DiagInfoPtr,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>引數  
 *HandleType*  
 [輸入]描述診斷所需的控制代碼的型別控制代碼型別識別項。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應使用此控制代碼型別。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[ODBC 驅動程式中開發連接集區覺察](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [輸入]診斷資料結構所表示的類型的控制代碼*HandleType*。 如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或取消共用的環境控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的狀態記錄。 狀態記錄編號 1。 如果*Sqlgetdiagfield*引數會指出診斷標頭的任何欄位*RecNumber*會被忽略。 如果沒有，它應該是大於 0。  
  
 *DiagIdentifier*  
 [輸入]表示其值是要傳回的診斷欄位。 如需詳細資訊，請參閱 「*Sqlgetdiagfield*引數 」 一節中 「 註解。 」  
  
 *DiagInfoPtr*  
 [輸出]若要在其中傳回的診斷資訊的緩衝區的指標。 資料類型而定的值*Sqlgetdiagfield*。 如果*DiagInfoPtr*是整數類型、 應用程式應該使用的緩衝區 SQLULEN 和初始化之前呼叫這個函式，有些驅動程式為 0 的值可能只會寫入較低的 32 位元或 16 位元的緩衝區，並保留較高順序位元不變。  
  
 如果*DiagInfoPtr*為 NULL，就*StringLengthPtr*仍會傳回的總位元組數 （不含字元資料之 null 結束字元） 可用來傳回中指向緩衝區*DiagInfoPtr*。  
  
 *BufferLength*  
 [輸入]如果*Sqlgetdiagfield*是 ODBC 定義的診斷和*DiagInfoPtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *DiagInfoPtr*. 如果*Sqlgetdiagfield*是 ODBC 定義欄位並\* *DiagInfoPtr*是一個整數， *Columnsize*會被忽略。 如果中的值 *\*DiagInfoPtr*是 Unicode 字串 (呼叫時**SQLGetDiagFieldW**)，則*Columnsize*引數必須是偶數。  
  
 如果*Sqlgetdiagfield*驅動程式定義的欄位，應用程式設定指出欄位給驅動程式管理員性質*Columnsize*引數。 *BufferLength*可以有下列值：  
  
-   如果*DiagInfoPtr*是字元字串的指標*Columnsize*是 sql_nts; 之字串的長度。  
  
-   如果*DiagInfoPtr* SQL_LEN_BINARY_ATTR 的結果是二進位緩衝區中，應用程式位置的指標 (*長度*) 中的巨集*Columnsize*。 這會放在負值*Columnsize*。  
  
-   如果*DiagInfoPtr*是字元字串或二進位字串，以外的值的指標*Columnsize*應有 SQL_IS_POINTER 的值。  
  
-   如果 *\*DiagInfoPtr*包含固定長度的資料型別*Columnsize*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，視需要。  
  
 *StringLengthPtr*  
 [輸出]在其中傳回的總位元組數 （不包括 null 結束字元所需的位元組數） 緩衝區的指標來傳回在可用\* *DiagInfoPtr*，字元資料。 傳回可用的位元組數目是否大於或等於*Columnsize*中的文字\* *DiagInfoPtr*會被截斷成*Columnsize*減號null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE，還是 sql_no_data 為止。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagField**不會將本身的診斷記錄。 它會使用下列傳回值報告自己執行的結果：  
  
-   SQL_SUCCESS:此函式會成功地傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO:\**DiagInfoPtr*是太小無法容納要求的診斷欄位。 因此，在 [診斷] 欄位的資料已遭截斷。 若要判斷發生截斷，應用程式必須比較*Columnsize*實際的位元組數目，會寫入至 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE:所表示的控制代碼*HandleType*並*處理*不是有效的控制代碼。  
  
-   SQL_ERROR:發生下列其中一項：  
  
    -   *Sqlgetdiagfield*引數不是其中一個有效的值。  
  
    -   *Sqlgetdiagfield*引數為 SQL_DIAG_CURSOR_ROW_COUNT、 SQL_DIAG_DYNAMIC_FUNCTION、 SQL_DIAG_DYNAMIC_FUNCTION_CODE，還是 SQL_DIAG_ROW_COUNT，但*處理*不是陳述式控制代碼。 （驅動程式管理員會傳回此診斷）。  
  
    -   *RecNumber*引數為負數或 0 的時機*Sqlgetdiagfield*指示的診斷記錄的欄位。 *RecNumber*會忽略標頭欄位。  
  
    -   所要求的值為字元字串和*Columnsize*小於零。  
  
    -   當使用非同步通知時，控制代碼的非同步作業未完成。  
  
-   SQL_NO_DATA 為止：*RecNumber*中指定的控制代碼已存在的診斷記錄的數目大於*處理。* 函式也會傳回 SQL_NO_DATA 任何正*RecNumber*沒有診斷記錄是否*處理*。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫**SQLGetDiagField**完成三個目標的其中一個：  
  
1.  若要取得特定錯誤或警告資訊，當函式呼叫已傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO (或針對 SQL_NEED_DATA **SQLBrowseConnect**函式)。  
  
2.  若要判斷資料來源中插入、 刪除或更新作業所執行的呼叫時所影響的資料列數目**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos** （從 SQL_DIAG_ROW_COUNT 標頭欄位中），或如果此驅動程式可以提供這項資訊判斷存在於目前開啟的資料指標中，資料列數目 (從SQL_DIAG_CURSOR_ROW_COUNT 標頭欄位）。  
  
3.  若要判斷哪一個函式呼叫中執行了**SQLExecDirect**或是**SQLExecute** （從 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 標頭欄位）。  
  
 任何 ODBC 函數可以張貼，零或多個診斷記錄每次呼叫它時，讓應用程式可以呼叫**SQLGetDiagField**之後的任何 ODBC 函數呼叫。 可以一次儲存的診斷記錄的數目沒有限制。 **SQLGetDiagField**只擷取的診斷資訊最近在指定的診斷資料結構相關聯*處理*引數。 如果應用程式呼叫 ODBC 函數以外**SQLGetDiagField**或是**SQLGetDiagRec**，從先前使用相同的控制代碼呼叫任何診斷資訊都會遺失。  
  
 應用程式可以透過累加掃描所有的診斷記錄*RecNumber*，只要**SQLGetDiagField**都會傳回 SQL_SUCCESS。 狀態記錄的數目被表示 SQL_DIAG_NUMBER 標頭欄位。 若要呼叫**SQLGetDiagField**是標頭和記錄欄位。 應用程式可以呼叫**SQLGetDiagField**一次更新一筆記錄，從擷取的欄位，只要在過渡期間，會將記錄張貼相同的控制代碼尚未呼叫以外診斷函式的函式。  
  
 應用程式可以呼叫**SQLGetDiagField**在任何時間，唯一的差別 SQL_DIAG_CURSOR_ROW_COUNT 或 SQL_DIAG_ROW_COUNT，將會傳回 SQL_ERROR，如果傳回的任何診斷欄位*處理*不是陳述式控制代碼。 如果未定義，其他診斷欄位，則呼叫**SQLGetDiagField** （假設沒有其他診斷發生） 會傳回 SQL_SUCCESS 而且未定義的值會傳回欄位。  
  
 如需詳細資訊，請參閱 <<c0> [ 使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)並[實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫不是以非同步方式執行的 API，將會產生 HY010 「 函數順序錯誤 」。 不過，在非同步作業完成之前，無法擷取記錄時發生錯誤。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制代碼類型可以有與其相關聯的診斷資訊。 *HandleType*引數表示的控制代碼型別*處理*。  
  
 某些標頭和資料錄的欄位無法為傳回環境、 連接、 陳述式，以及描述項控制代碼。 這些控制代碼不適用 欄位會以 「 標頭欄位 」 和 「 記錄欄位 」 後面的章節。  
  
 如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或取消共用的環境控制代碼。  
  
 沒有驅動程式特定標頭的診斷欄位應該與環境控制代碼相關聯。  
  
 只有診斷的標頭欄位所定義的描述項控制代碼是 SQL_DIAG_NUMBER 和 SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>Sqlgetdiagfield 引數  
 這個引數表示所需的診斷資料結構之欄位的識別項。 如果*RecNumber*大於或等於 1，欄位中的資料描述函式所傳回的診斷資訊。 如果*RecNumber*為 0，欄位中的診斷資料結構的標頭，並因此會包含不與特定資訊傳回診斷資訊中，函式呼叫的相關資料。  
  
 驅動程式可以定義驅動程式特定標頭和記錄欄位中的診斷資料結構。  
  
 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式將能夠呼叫**SQLGetDiagField**只能搭配*Sqlgetdiagfield*SQL_DIAG_CLASS_ORIGIN、 SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_NUMBER、 SQL_DIAG_RETURNCODE、 SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE 的引數。 其他所有的診斷欄位將會傳回 SQL_ERROR。  
  
## <a name="header-fields"></a>標頭欄位  
 下表所列的標頭欄位可以包含在*Sqlgetdiagfield*引數。  
  
|DiagIdentifier|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此欄位包含資料指標中的資料列的計數。 取決於其語意**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2 和 SQL_STATIC_CURSOR_ATTRIBUTES2，這表示它的資訊類型資料列計數可供每個資料指標類型 （SQL_CA2_CRC_EXACT 和 SQL_CA2_CRC_APPROXIMATE 位元）。<br /><br /> 此欄位的內容會定義只適用於陳述式控制代碼，之後才**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**已呼叫。 呼叫**SQLGetDiagField**具有*Sqlgetdiagfield* SQL_DIAG_CURSOR_ROW_COUNT 上一個陳述式以外的控制代碼將會傳回 SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|這是描述基礎的函式執行的 SQL 陳述式的字串。 （請參閱"欄位的值動態函數，「 稍後在本節中，針對特定的值）。此欄位的內容會定義只適用於陳述式控制代碼，並只有在呼叫之後**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 呼叫**SQLGetDiagField**具有*Sqlgetdiagfield* SQL_DIAG_DYNAMIC_FUNCTION 上一個陳述式以外的控制代碼將會傳回 SQL_ERROR。 事件之前呼叫，這個欄位的值未定義**SQLExecute**或是**SQLExecDirect**。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|這是描述基礎的函式所執行的 SQL 陳述式的數字代碼。 （請參閱"值的動態函式欄位，"稍後在本節中，針對特定的值）。此欄位的內容會定義只適用於陳述式控制代碼，並只有在呼叫之後**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 呼叫**SQLGetDiagField**具有*Sqlgetdiagfield* SQL_DIAG_DYNAMIC_FUNCTION_CODE 上一個陳述式以外的控制代碼將會傳回 SQL_ERROR。 事件之前呼叫，這個欄位的值未定義**SQLExecute**或是**SQLExecDirect**。|  
|SQL_DIAG_NUMBER|SQLINTEGER|可供指定的控制代碼的狀態記錄的數目。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|函式所傳回的傳回碼。 如需傳回碼的清單，請參閱 <<c0> [ 傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)。 驅動程式不需要實作 SQL_DIAG_RETURNCODE;它一律被實作由驅動程式管理員。 如果尚未上呼叫任何函數*處理*，SQL_DIAG_RETURNCODE 就會傳回 SQL_SUCCESS。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|受到 insert、 delete 或 update 所執行的資料列數目**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**. 它是由驅動程式定義之後*資料指標規格*已經執行。 此欄位的內容會定義只適用於陳述式控制代碼。 呼叫**SQLGetDiagField**具有*Sqlgetdiagfield* SQL_DIAG_ROW_COUNT 上一個陳述式以外的控制代碼將會傳回 SQL_ERROR。 在此欄位中的資料也會傳回*RowCountPtr*引數**SQLRowCount**。 在此欄位中的資料會重設每 nondiagnostic 函式呼叫之後，而所傳回的資料列計數**SQLRowCount**維持不變，直到陳述式便會設定為已備妥或已配置的狀態。|  
  
## <a name="record-fields"></a>記錄欄位  
 下表所列的記錄欄位可以包含在*Sqlgetdiagfield*引數。  
  
|DiagIdentifier|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|字串，表示文件定義此記錄的 SQLSTATE 值的類別部分。 其值為"ISO 9075"的所有 Open Group 和 ISO 呼叫層級介面所定義的 Sqlstate。 對於 ODBC 專屬 Sqlstate （所有這些的 SQLSTATE 類別是 「 IM"），其值是"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果 SQL_DIAG_ROW_NUMBER 欄位是有效的資料列中的數字的資料列集或一組參數，此欄位會包含表示結果集中的資料行編號或參數中的數字的一組參數的值。 結果集資料行數字一律從 1 開始;如果此狀態記錄屬於書籤資料行，則欄位可以是零。 參數編號是從 1 開始。 如果狀態記錄的逸出序列所關聯的資料行數或參數數目，它就會有 SQL_NO_COLUMN_NUMBER 的值。 如果驅動程式無法判斷此記錄相關聯的參數數目的資料行數目，此欄位有 SQL_COLUMN_NUMBER_UNKNOWN 的值。<br /><br /> 此欄位的內容會定義只適用於陳述式控制代碼。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|字串，表示連接的診斷記錄與產生的名稱。 此欄位是驅動程式定義。 環境控制代碼相關聯的診斷資料結構，以及任何連線不相關的診斷，則這個欄位會是零長度字串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|參考用錯誤或警告訊息。 此欄位格式中所述[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。 沒有任何診斷訊息文字的最大長度。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驅動程式/資料來源特有的原生錯誤的程式碼。 如果沒有原生錯誤程式碼，此驅動程式會傳回 0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此欄位包含資料列中的數字資料列集或與狀態記錄相關聯的參數集合中的參數號碼。 資料列編號和參數的數字開頭為 1。 此欄位有值 SQL_NO_ROW_NUMBER，如果此狀態記錄的逸出序列所關聯的資料列數目或參數數目。 如果這個記錄相關聯的參數數目的資料列數目，則無法判斷驅動程式，此欄位有 SQL_ROW_NUMBER_UNKNOWN 的值。<br /><br /> 此欄位的內容會定義只適用於陳述式控制代碼。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|表示診斷記錄與相關的伺服器名稱的字串。 它等同於呼叫的傳回值**SQLGetInfo** SQL_DATA_SOURCE_NAME 選項。 環境控制代碼相關聯的診斷資料結構和不相關的任何伺服器的診斷，則這個欄位會是零長度字串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|五個字元 SQLSTATE 診斷程式碼。 如需詳細資訊，請參閱 < [Sqlstate](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|具有相同的格式和有效的值為 SQL_DIAG_CLASS_ORIGIN，可識別子類別一部分的 SQLSTATE 程式碼定義的一部分的字串。 下面是"ODBC 3.0"會傳回 ODBC 專屬 SQLSTATE:<br /><br /> 01S00，01S01，01S02 的警告，01S06，01S07，07S01，08S01 以及 21S01，21S02，25S01，25S02，25S03，42S01，42S02，42S11，42S12，42S21，42S22，HY095、 HY097、 HY098、 HY099、 HY100、 HY101、 包含 SQLSTATE=HY105、 HY107、 HY109、 HY110、 HY111、 HYT00、 HYT01、 IM001、 IM002、 IM003、 IM004、 IM005、 IM006，IM007、 IM008、 IM010、 IM011、 IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動態函數欄位的值  
 下表描述套用至每個類型的呼叫所執行的 SQL 陳述式的值 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE **SQLExecute**或**SQLExecDirect**. 驅動程式可以將驅動程式定義的值加入所列。  
  
|SQL 陳述式<br /><br /> 執行|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain-statement*|「 ALTER 網域 」|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table-statement*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*assertion-definition*|「 建立判斷提示 」|SQL_DIAG_CREATE_ASSERTION|  
|*character-set-definition*|「 建立字元集 」|SQL_DIAG_CREATE_CHARACTER_SET|  
|*collation-definition*|「 建立定序 」|SQL_DIAG_CREATE_COLLATION|  
|*domainn-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|
|*create-index-statement*|「 建立索引 」|SQL_DIAG_CREATE_INDEX|  
|*create-table-statement*|[建立資料表]|SQL_DIAG_CREATE_TABLE|  
|*create-view-statement*|[建立檢視]|SQL_DIAG_CREATE_VIEW|  
|*cursor-specification*|[選取資料指標]|SQL_DIAG_SELECT_CURSOR|  
|*delete-statement-positioned*|「 動態刪除游標 」|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete-statement-searched*|「 刪除的位置 」|SQL_DIAG_DELETE_WHERE|  
|*drop-assertion-statement*|「 卸除判斷提示 」|SQL_DIAG_DROP_ASSERTION|  
|*drop-character-set-stmt*|「 卸除字元集 」|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-collation-statement*|[卸除定序]|SQL_DIAG_DROP_COLLATION|  
|*drop-domain-statement*|「 卸除網域 」|SQL_DIAG_DROP_DOMAIN|  
|*drop-index-statement*|[卸除索引]|SQL_DIAG_DROP_INDEX|  
|*drop-schema-statement*|[卸除結構描述]|SQL_DIAG_DROP_SCHEMA|  
|*drop-table-statement*|「 卸除資料表 」|SQL_DIAG_DROP_TABLE|  
|*drop-translation-statement*|「 卸除轉譯 」|SQL_DIAG_DROP_TRANSLATION|  
|*drop-view-statement*|「 卸除檢視 」|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|「 授與 」|SQL_DIAG_GRANT|
|*insert-statement*|「 插入 」|SQL_DIAG_INSERT|  
|*ODBC-procedure-extension*|[撥號]|SQL_DIAG_ CALL|  
|*revoke-statement*|[撤銷]|SQL_DIAG_REVOKE|  
|*schema-definition*|[建立結構描述]|SQL_DIAG_CREATE_SCHEMA|  
|*translation-definition*|「 建立翻譯 」|SQL_DIAG_CREATE_TRANSLATION|  
|*update-statement-positioned*|「 動態更新游標 」|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update-statement-searched*|「 更新位置 」|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空字串*|SQL_DIAG_UNKNOWN_STATEMENT|  

<!--
These two malformed table rows were fixed by educated GUESS only.
Each pair starts with the original flawed row.
Flawed because treated as only two cells by HTML render,
and because missing info anyway.
Also, these flawed rows lacked '|' as their first nonWhitespace character (although markdown technically allows this omission, unfortunately).
Arguably the following SQL.H file shows the sequence of the flawed rows in the table was suboptimal also.

ftp://www.fpc.org/fpc32/VS6Disk1/VC98/INCLUDE/SQL.H

GeneMi , 2019/01/19
- - - - - - - - - - - - - -

n-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|  

|*domain-definition*|"CREATE DOMAIN"|SQL_DIAG_CREATE_DOMAIN|

-statement*|"GRANT"|SQL_DIAG_GRANT|  

|*grant-statement*|"GRANT"|SQL_DIAG_GRANT|

-->

## <a name="sequence-of-status-records"></a>狀態記錄的順序

 狀態記錄定位順序，根據資料列數目和類型的診斷。 驅動程式管理員會決定最終的順序，在其中傳回它所產生的狀態記錄。 驅動器會決定最終的順序，在其中傳回它所產生的狀態記錄。  
  
 如果診斷記錄所公佈的驅動程式管理員和驅動程式，就有一個驅動程式管理員負責來排序它們。  
  
 如果有兩個或多個狀態記錄，記錄的順序取決於第一次資料列數目。 若要判斷資料列的診斷記錄的順序，適用下列規則：  
  
-   因為 SQL_NO_ROW_NUMBER 會定義為-1，不會對應至任何資料列的記錄會出現在對應到特定的資料列中，記錄之前。  
  
-   因為 SQL_ROW_NUMBER_UNKNOWN 會定義為-2，資料列數目是未知的記錄會出現在所有其他的記錄之前。  
  
-   屬於特定的資料列的所有記錄，記錄會依照 SQL_DIAG_ROW_NUMBER 欄位中的值。 列出所有錯誤和警告的第一個資料列受到影響，並接著所有錯誤和警告的下一個資料都列受影響，依此類推。  
  
> [!NOTE]
>  ODBC 3 *.x*驅動程式管理員不會排序狀態記錄診斷的佇列中如果 SQLSTATE 01S01 （資料列中的錯誤） 由 ODBC 2 *.x*驅動程式或如果 SQLSTATE 01S01 （資料列中的錯誤） 由 ODBC3 *.x*驅動程式時**SQLExtendedFetch**稱為或**SQLSetPos**已將其置於使用資料指標上呼叫**SQLExtendedFetch**.  
  
 中每個資料列，或所有未對應的資料列或資料列數目是未知，這些記錄或資料列數等於 SQL_NO_ROW_NUMBER 所有這些記錄，列出的第一個記錄取決於使用一組的排序規則。 之後第一筆記錄，會影響資料列的其他記錄的順序是未定義。 應用程式不能假設錯誤之前的警告之後第一筆記錄。 應用程式應該掃描完整的診斷資料結構，以取得成功呼叫函式的完整資訊。  
  
 下列規則用來判斷資料列內第一筆記錄。 具有最高順位的記錄是第一筆記錄。 資料錄 （驅動程式管理員、 驅動程式、 閘道和等等） 的來源不是當排名的記錄。  
  
-   **錯誤**描述錯誤的狀態記錄都有最高的等級。 下列規則會套用至排序錯誤：  
  
    -   表示交易失敗或可能的交易失敗的記錄 outrank 其他所有記錄。  
  
    -   如果兩個或多筆記錄會描述相同的錯誤狀況，開啟群組 CLI 規格 （透過 HZ 類別 03） 所定義的 Sqlstate outrank ODBC 和驅動程式定義的 Sqlstate。  
  
-   **實作定義沒有資料值**描述驅動程式定義沒有資料值 （類別 02） 的狀態記錄的第二個最高的等級。  
  
-   **警告**描述警告 （類別 01） 的狀態記錄具有最低順位。 如果兩個或多筆記錄會描述相同的警告狀況，然後警告開啟群組 CLI 規格所定義的 Sqlstate outrank ODBC 定義及驅動程式定義的 Sqlstate。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得多個欄位的診斷資料結構|[SQLGetDiagRec 函式](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
