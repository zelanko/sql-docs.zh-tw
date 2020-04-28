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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a26319868a4b94b895da73d39b284f612fe35889
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285428"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函數

**標準**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **摘要**  
 **SQLGetDiagField**會傳回包含錯誤、警告和狀態資訊之診斷資料結構（與指定的控制碼相關聯）之記錄欄位的目前值。  
  
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
 源控制碼類型識別碼，描述需要診斷的控制碼類型。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼僅供驅動程式管理員和驅動程式使用。 應用程式不應使用此控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 源*HandleType*所指示之類型的診斷資料結構的控制碼。 如果*HandleType*為 SQL_HANDLE_ENV，則*handle*可以是共用或非共用的環境控制碼。  
  
 *RecNumber*  
 源表示應用程式用來搜尋資訊的狀態記錄。 狀態記錄的編號為1。 如果*以*引數指出診斷標頭的任何欄位，則會忽略*RecNumber* 。 如果不是，則應該大於0。  
  
 *以*  
 源表示要傳回其值的診斷欄位。 如需詳細資訊，請參閱「批註」中的「*以*引數」一節。  
  
 *DiagInfoPtr*  
 輸出要傳回診斷資訊之緩衝區的指標。 資料類型取決於*以*的值。 如果*DiagInfoPtr*是整數類型，則在呼叫此函式之前，應用程式應該使用 SQLULEN 的緩衝區，並將值初始化為0，因為某些驅動程式可能只會寫入較低的32位或16位的緩衝區，並不會變更較高的順序位。  
  
 如果*DiagInfoPtr*為 Null， *StringLengthPtr*仍會傳回*DiagInfoPtr*所指向的緩衝區中可傳回的位元組總數（不包括字元資料的 Null 終止字元）。  
  
 *BufferLength*  
 源如果*以*是 ODBC 定義的診斷，而*DiagInfoPtr*指向字元字串或二進位緩衝區，則這個引數應該是\* *DiagInfoPtr*的長度。 如果*以*是 ODBC 定義的欄位，而\* *DiagInfoPtr*是整數，則會忽略*BufferLength* 。 如果* \*DiagInfoPtr*中的值是 Unicode 字串（在呼叫**SQLGetDiagFieldW**時），則*BufferLength*引數必須是偶數。  
  
 如果*以*是驅動程式定義的欄位，應用程式會藉由設定*BufferLength*引數來指出欄位對驅動程式管理員的本質。 *BufferLength*可以有下列值：  
  
-   如果*DiagInfoPtr*是字元字串的指標， *BufferLength*就是字串或 SQL_NTS 的長度。  
  
-   如果*DiagInfoPtr*是二進位緩衝區的指標，應用程式會將 SQL_LEN_BINARY_ATTR （*長度*）宏的結果放在*BufferLength*中。 這會將負數值放在*BufferLength*中。  
  
-   如果*DiagInfoPtr*是字元字串或二進位字串以外的值指標， *BufferLength*應該會有值 SQL_IS_POINTER。  
  
-   如果* \*DiagInfoPtr*包含固定長度的資料類型，則視情況而定， *BufferLength*會 SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或 SQL_IS_USMALLINT。  
  
 *StringLengthPtr*  
 輸出緩衝區的指標，要在其中傳回字元資料的位元組總數（不包括 null 終止字元所需的位元組數目） \*，以供*DiagInfoPtr*。 如果傳回的位元組數目大於或等於*BufferLength*， \* *DiagInfoPtr*中的文字會被截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagField**不會為其本身張貼診斷記錄。 它會使用下列傳回值來報告其本身執行的結果：  
  
-   SQL_SUCCESS：函數已成功傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO： \* *DiagInfoPtr*太小，無法保存所要求的診斷欄位。 因此，[診斷] 欄位中的資料會被截斷。 若要判斷是否發生截斷，應用程式必須將*BufferLength*與實際可用的位元組數目（寫入 **StringLengthPtr*）進行比較。  
  
-   SQL_INVALID_HANDLE： *HandleType*和*HANDLE*所指示的控制碼不是有效的控制碼。  
  
-   SQL_ERROR：發生下列其中一種情況：  
  
    -   *以*引數不是其中一個有效的值。  
  
    -   *以*引數已 SQL_DIAG_CURSOR_ROW_COUNT、SQL_DIAG_DYNAMIC_FUNCTION、SQL_DIAG_DYNAMIC_FUNCTION_CODE 或 SQL_DIAG_ROW_COUNT，但*句*柄不是語句控制碼。 （驅動程式管理員會傳回此診斷）。  
  
    -   當*以*指示診斷記錄中的欄位時 *，RecNumber*引數為負數或0。 標頭欄位會忽略*RecNumber* 。  
  
    -   要求的值是字元字串，而*BufferLength*小於零。  
  
    -   使用非同步通知時，控制碼上的非同步作業並未完成。  
  
-   SQL_NO_DATA： *RecNumber*大於 handle 中指定之控制碼所存在的診斷記錄數目 *。* 如果沒有任何適用于*Handle*的診斷記錄，函數也會傳回任何正面*RecNumber*的 SQL_NO_DATA。  
  
## <a name="comments"></a>評價  
 應用程式通常會呼叫**SQLGetDiagField**來完成三個目標的其中一個：  
  
1.  若要在函式呼叫傳回時，取得特定的錯誤或警告資訊 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO （或**SQLBrowseConnect**函數的 SQL_NEED_DATA）。  
  
2.  決定在呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** （從 SQL_DIAG_ROW_COUNT 標頭欄位）執行插入、刪除或更新作業時，資料來源中受影響的資料列數目，或判斷存在於目前開啟資料指標中的資料列數（如果驅動程式可以提供這項資訊，則為）（從 [SQL_DIAG_CURSOR_ROW_COUNT 標頭] 欄位）。  
  
3.  判斷呼叫**SQLExecDirect**或**SQLExecute** （從 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 標頭欄位）所執行的函式。  
  
 任何 ODBC 函數每次呼叫時都可以張貼零個或多個診斷記錄，因此應用程式可以在任何 ODBC 函數呼叫之後呼叫**SQLGetDiagField** 。 任何一次可以儲存的診斷記錄數目並無任何限制。 **SQLGetDiagField**只會抓取最近與*Handle*引數中指定之診斷資料結構相關聯的診斷資訊。 如果應用程式呼叫**SQLGetDiagField**或**SQLGETDIAGREC**以外的 ODBC 函數，則會遺失先前呼叫中具有相同控制碼的任何診斷資訊。  
  
 只要**SQLGetDiagField**傳回 SQL_SUCCESS，應用程式就可以藉由遞增*RecNumber*來掃描所有診斷記錄。 狀態記錄的數目會顯示在 [SQL_DIAG_NUMBER 標頭] 欄位中。 對**SQLGetDiagField**的呼叫在標頭和記錄欄位中是非破壞性的。 應用程式稍後可以再次呼叫**SQLGetDiagField** ，以從記錄中取出欄位，只要未在過渡中呼叫診斷函式以外的函式，就會在相同的控制碼上張貼記錄。  
  
 除了 SQL_DIAG_CURSOR_ROW_COUNT 或 SQL_DIAG_ROW_COUNT 之外，應用程式可以呼叫**SQLGetDiagField**來傳回任何診斷欄位，如果*Handle*不是語句控制碼，則會傳回 SQL_ERROR。 如果未定義任何其他診斷欄位， **SQLGetDiagField**的呼叫將會傳回 SQL_SUCCESS （如果未遇到其他診斷），而且會針對欄位傳回未定義的值。  
  
 如需詳細資訊，請參閱[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)和[執行 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫不是以非同步方式執行的 API，將會產生 HY010 「函數順序錯誤」。 不過，在非同步作業完成之前，無法抓取錯誤記錄。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制碼類型都可以有相關聯的診斷資訊。 *HandleType*引數會指出*句*柄的控制碼類型。  
  
 某些標頭和記錄欄位無法針對環境、連接、語句和描述項控制碼傳回。 欄位不適用的控制碼會在後面的「標頭欄位」和「記錄欄位」章節中指出。  
  
 如果*HandleType*為 SQL_HANDLE_ENV，則*handle*可以是共用或非共用的環境控制碼。  
  
 沒有任何驅動程式專屬的標頭診斷欄位應與環境控制碼相關聯。  
  
 唯一為描述項控制碼定義的診斷標頭欄位是 SQL_DIAG_NUMBER 和 SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>以引數  
 這個引數會指出診斷資料結構所需之欄位的識別碼。 如果*RecNumber*大於或等於1，則欄位中的資料會描述函數所傳回的診斷資訊。 如果*RecNumber*為0，則欄位會在診斷資料結構的標頭中，因此會包含與傳回診斷資訊之函式呼叫相關的資料，而不是特定資訊。  
  
 驅動程式可以在診斷資料結構中定義驅動程式特有的標頭和記錄欄位。  
  
 使用 ODBC 2.x*驅動程式的 odbc 3.x 應用程式*將 *.x*只能使用 SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE 的*以*引數來呼叫**SQLGetDiagField** 。 所有其他診斷欄位都會傳回 SQL_ERROR。  
  
## <a name="header-fields"></a>標頭欄位  
 下表所列的標頭欄位可以包含在*以*引數中。  
  
|以|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此欄位包含資料指標中的資料列計數。 其語義取決於**SQLGetInfo**資訊類型 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2 和 SQL_STATIC_CURSOR_ATTRIBUTES2，這會指出每個資料指標類型（在 SQL_CA2_CRC_EXACT 和 SQL_CA2_CRC_APPROXIMATE 位）中可使用的資料列計數。<br /><br /> 只有在呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults**之後，才會針對語句控制碼定義此欄位的內容。 在語句控制碼以外，以 SQL_DIAG_CURSOR_ROW_COUNT 的*以*呼叫**SQLGetDiagField** ，將會傳回 SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR|這是描述基礎函數所執行之 SQL 語句的字串。 （如需特定值，請參閱本節稍後的「動態函數位段的值」）。此欄位的內容只會定義給語句控制碼，而且只會在呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults**之後。 在語句控制碼以外，以 SQL_DIAG_DYNAMIC_FUNCTION 的*以*呼叫**SQLGetDiagField** ，將會傳回 SQL_ERROR。 在呼叫**SQLExecute**或**SQLExecDirect**之前，此欄位的值是未定義的。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|這是一個數位代碼，用來描述基礎函數所執行的 SQL 語句。 （如需特定值，請參閱本節稍後的「動態函數位段的值」）。此欄位的內容只會定義給語句控制碼，而且只會在呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults**之後。 在語句控制碼以外，以 SQL_DIAG_DYNAMIC_FUNCTION_CODE 的*以*呼叫**SQLGetDiagField** ，將會傳回 SQL_ERROR。 在呼叫**SQLExecute**或**SQLExecDirect**之前，此欄位的值是未定義的。|  
|SQL_DIAG_NUMBER|SQLINTEGER|可用於指定控制碼的狀態記錄數目。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|傳回函式所傳回的程式碼。 如需傳回碼的清單，請參閱傳回[碼](../../../odbc/reference/develop-app/return-codes-odbc.md)。 驅動程式不需要執行 SQL_DIAG_RETURNCODE;它一律由驅動程式管理員執行。 如果尚未在*控制碼*上呼叫函式，則會針對 SQL_DIAG_RETURNCODE 傳回 SQL_SUCCESS。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|由**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos**所執行的插入、刪除或更新所影響的資料列數目。 它是在執行資料*指標規格*之後定義的驅動程式。 此欄位的內容只會定義給語句控制碼。 在語句控制碼以外，以 SQL_DIAG_ROW_COUNT 的*以*呼叫**SQLGetDiagField** ，將會傳回 SQL_ERROR。 此欄位中的資料也會在**SQLRowCount**的*RowCountPtr*引數中傳回。 此欄位中的資料會在每次 nondiagnostic 函式呼叫之後重設，而**SQLRowCount**所傳回的資料列計數會維持不變，直到語句設定回到備妥或已配置狀態為止。|  
  
## <a name="record-fields"></a>記錄欄位  
 下表所列的記錄欄位可以包含在*以*引數中。  
  
|以|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR|字串，表示定義此記錄中 SQLSTATE 值之類別部分的檔。 其值為 "ISO 9075"，適用于開放群組和 ISO 呼叫層級介面所定義的所有 SQLSTATEs。 針對 ODBC 特定的 SQLSTATEs （其 SQLSTATE 類別為 "IM" 的所有元件），其值為 "ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果 SQL_DIAG_ROW_NUMBER 欄位在資料列集或一組參數中是有效的資料列編號，此欄位會包含代表結果集中之資料行編號的值，或參數集合中的參數編號。 結果集資料行數位一律從1開始;如果此狀態記錄與書簽資料行相關，欄位可以是零。 參數編號從1開始。 如果狀態記錄未與資料行編號或參數編號相關聯，它就會有 SQL_NO_COLUMN_NUMBER 的值。 如果驅動程式無法判斷與此記錄相關聯的資料行編號或參數編號，此欄位的值會是 SQL_COLUMN_NUMBER_UNKNOWN。<br /><br /> 此欄位的內容只會定義給語句控制碼。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR|字串，表示與診斷記錄相關聯的連接名稱。 此欄位為驅動程式定義。 針對與環境控制碼相關聯的診斷資料結構，以及與任何連接無關的診斷，此欄位是長度為零的字串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR|錯誤或警告上的參考用訊息。 此欄位的格式如[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)中所述。 診斷郵件內文沒有最大長度。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驅動程式/資料來源特定的原生錯誤碼。 如果沒有原生錯誤碼，驅動程式會傳回0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此欄位包含資料列集中的資料列編號，或參數的參數編號，與狀態記錄相關聯。 資料列編號和參數編號的開頭為1。 如果此狀態記錄未與資料列編號或參數編號相關聯，此欄位的值 SQL_NO_ROW_NUMBER。 如果驅動程式無法判斷與此記錄相關聯的資料列編號或參數編號，此欄位的值會 SQL_ROW_NUMBER_UNKNOWN。<br /><br /> 此欄位的內容只會定義給語句控制碼。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR|字串，表示與診斷記錄相關聯的伺服器名稱。 這與使用 SQL_DATA_SOURCE_NAME 選項呼叫**SQLGetInfo**時所傳回的值相同。 針對與環境控制碼相關聯的診斷資料結構，以及與任何伺服器無關的診斷，此欄位是長度為零的字串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR|五個字元的 SQLSTATE 診斷碼。 如需詳細資訊，請參閱[SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR|具有與 SQL_DIAG_CLASS_ORIGIN 相同格式和有效值的字串，可識別 SQLSTATE 程式碼之子類別部分的定義部分。 傳回 "ODBC 3.0" 的 ODBC 特定 SQLSTATES 包括下列各項：<br /><br /> 01S00、01S01、01S02、01S06、01S07、07S01、08S01、21S01、21S02、25S01、25S02、25S03、42S01、42S02、42S11、42S12、42S21、42S22、HY095、HY097、HY098、HY099、HY100、HY101、HY105、HY107、HY109、HY110、HY111、HYT00、HYT01、IM001、IM002、IM003、IM004、IM005、IM006。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動態函數位段的值  
 下表描述適用于**SQLExecute**或**SQLExecDirect**呼叫所執行之每個 SQL 語句類型的 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 值。 驅動程式可以將驅動程式定義的值新增至列出的值。  
  
|SQL 陳述式<br /><br /> 執行| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain 語句*|"ALTER DOMAIN"|SQL_DIAG_ALTER_DOMAIN|  
|*alter-table 語句*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*判斷提示-定義*|「建立判斷提示」|SQL_DIAG_CREATE_ASSERTION|  
|*字元集定義*|「建立字元集」|SQL_DIAG_CREATE_CHARACTER_SET|  
|*定序定義*|「建立定序」|SQL_DIAG_CREATE_COLLATION|  
|*domainn>-定義*|「建立網域」|SQL_DIAG_CREATE_DOMAIN|
|*create-index 語句*|「建立索引」|SQL_DIAG_CREATE_INDEX|  
|*create-table 語句*|"CREATE TABLE"|SQL_DIAG_CREATE_TABLE|  
|*create-view 語句*|「建立視圖」|SQL_DIAG_CREATE_VIEW|  
|*資料指標規格*|「選取游標」|SQL_DIAG_SELECT_CURSOR|  
|*delete 語句-定位*|「動態刪除資料指標」|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete 語句-搜尋*|「刪除位置」|SQL_DIAG_DELETE_WHERE|  
|*drop-判斷提示語句*|「捨棄判斷提示」|SQL_DIAG_DROP_ASSERTION|  
|*drop-character-set-stmt*|「捨棄字元集」|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-定序語句*|「捨棄定序」|SQL_DIAG_DROP_COLLATION|  
|*drop-domain 語句*|「捨棄網域」|SQL_DIAG_DROP_DOMAIN|  
|*drop index 語句*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop 架構語句*|「捨棄架構」|SQL_DIAG_DROP_SCHEMA|  
|*drop table 語句*|「卸載資料表」|SQL_DIAG_DROP_TABLE|  
|*drop-轉譯語句*|「捨棄轉譯」|SQL_DIAG_DROP_TRANSLATION|  
|*drop view 語句*|「捨棄視圖」|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|把|SQL_DIAG_GRANT|
|*insert 語句*|插入|SQL_DIAG_INSERT|  
|*ODBC-程式-延伸模組*|拜訪|SQL_DIAG_ 呼叫|  
|*revoke 語句*|[|SQL_DIAG_REVOKE|  
|*架構定義*|「建立架構」|SQL_DIAG_CREATE_SCHEMA|  
|*轉譯-定義*|「建立翻譯」|SQL_DIAG_CREATE_TRANSLATION|  
|*更新語句-定位*|「動態更新資料指標」|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update 語句-搜尋*|「更新位置」|SQL_DIAG_UPDATE_WHERE|  
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

 狀態記錄會根據資料列編號和診斷類型放置在序列中。 驅動程式管理員會決定傳回其所產生之狀態記錄的最終順序。 驅動程式會決定傳回其所產生之狀態記錄的最終順序。  
  
 如果驅動程式管理員和驅動程式都同時張貼診斷記錄，驅動程式管理員就會負責排序它們。  
  
 如果有兩個以上的狀態記錄，記錄的順序會先由資料列編號決定。 下列規則適用于依資料列來判斷診斷記錄的順序：  
  
-   未對應到任何資料列的記錄會出現在對應到特定資料列的記錄前面，因為 SQL_NO_ROW_NUMBER 定義為-1。  
  
-   資料列編號未知的記錄會出現在所有其他記錄前面，因為 SQL_ROW_NUMBER_UNKNOWN 定義為-2。  
  
-   對於特定資料列相關的所有記錄，記錄都會依照 [SQL_DIAG_ROW_NUMBER] 欄位中的值來排序。 系統會列出受影響的第一個資料列的所有錯誤和警告，然後顯示下一個受影響資料列的所有錯誤和警告，依此類推。  
  
> [!NOTE]
>  如果 odbc*2.x 驅動程式*傳回 SQLSTATE 01S01 （row 中的錯誤），或 odbc 3.x 驅動程式傳回 SQLSTATE 01S01 （row 中的錯誤），**或在已**定位**SQLExtendedFetch**的資料指標上呼叫**SQLSetPos** ，則 odbc 3.x*驅動程式*管理員 *.x*不會排序診斷佇列中的狀態記錄。  
  
 在每個資料列中，或針對未對應至資料列或資料列數目不明的所有記錄，或針對資料列數等於 SQL_NO_ROW_NUMBER 的所有記錄，會使用一組排序規則來決定第一個列出的記錄。 第一筆記錄之後，不會定義影響資料列之其他記錄的順序。 應用程式無法假設錯誤在第一筆記錄之後的警告前面。 應用程式應該掃描完整的診斷資料結構，以取得函式不成功呼叫的完整資訊。  
  
 下列規則是用來判斷資料列中的第一筆記錄。 具有最高等級的記錄是第一筆記錄。 記錄的來源（驅動程式管理員、驅動程式、閘道等）不會在排名記錄時考慮。  
  
-   **錯誤**描述錯誤的狀態記錄具有最高等級。 下列規則適用于排序錯誤：  
  
    -   指出交易失敗或可能的交易失敗的記錄 outrank 所有其他記錄。  
  
    -   如果有兩個以上的記錄描述相同的錯誤狀況，則 SQLSTATEs 由 Open Group CLI 規格（類別03到 HZ）所定義，會 outrank ODBC 和驅動程式定義的 SQLSTATEs。  
  
-   **執行-未定義任何資料值**描述驅動程式定義的無資料值（類別02）的狀態記錄具有第二個最高等級。  
  
-   **警告**描述警告的狀態記錄（類別01）具有最低的排名。 如果有兩個以上的記錄描述相同的警告條件，則會由 Open Group CLI 規格所定義的警告 SQLSTATEs，outrank ODBC 定義和驅動程式定義的 SQLSTATEs。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得診斷資料結構的多個欄位|[SQLGetDiagRec 函式](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
