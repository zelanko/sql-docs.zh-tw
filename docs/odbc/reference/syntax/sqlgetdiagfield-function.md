---
description: SQLGetDiagField 函數
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
ms.openlocfilehash: 92043f5deb505d60ebe168a9c219c4d37a304ed5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461023"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函數

**一致性**  
 引進的版本： ODBC 3.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLGetDiagField** 會傳回診斷資料結構之記錄欄位的目前值 (與包含錯誤、警告和狀態資訊的指定控制碼) 相關聯。  
  
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
 輸出控制碼類型識別碼，描述需要診斷的控制碼類型。 必須是下列其中之一：  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN 控制碼只能由驅動程式管理員和驅動程式使用。 應用程式不應該使用這個控制碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱 [在 ODBC 驅動程式中開發連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 輸出診斷資料結構的控制碼， *HandleType*所指出的型別。 如果 *HandleType* 是 SQL_HANDLE_ENV， *控制碼* 可以是共用或非共用的環境控制碼。  
  
 *RecNumber*  
 輸出指出應用程式用來搜尋資訊的狀態記錄。 狀態記錄是從1開始編號。 如果 *以* 引數指出診斷標頭的任何欄位，則會忽略 *RecNumber* 。 如果不是，則應大於0。  
  
 *以*  
 輸出表示要傳回其值的診斷欄位。 如需詳細資訊，請參閱「批註」中的「*以* 引數」一節。  
  
 *DiagInfoPtr*  
 出要傳回診斷資訊之緩衝區的指標。 資料類型取決於 *以*的值。 如果 *DiagInfoPtr* 是整數類型，則應用程式應該使用 SQLULEN 的緩衝區，並在呼叫此函式之前將值初始化為0，因為某些驅動程式可能只會寫入較低的32位或16位的緩衝區，而不會讓較高的順序位保持不變。  
  
 如果 *DiagInfoPtr* 為 Null， *StringLengthPtr* 仍會傳回位元組總數 (排除字元資料的 Null 終止字元) 可在 *DiagInfoPtr*所指向的緩衝區中傳回。  
  
 *BufferLength*  
 輸出如果*以*是 ODBC 定義的診斷，且*DiagInfoPtr*指向字元字串或二進位緩衝區，此引數應該是 \* *DiagInfoPtr*的長度。 如果*以*是 ODBC 定義的欄位，而 \* *DiagInfoPtr*是整數，則會忽略*BufferLength* 。 如果* \* DiagInfoPtr*中的值是在呼叫**SQLGetDiagFieldW**) 時 (的 Unicode 字串，則*BufferLength*引數必須是偶數。  
  
 如果 *以* 是驅動程式定義的欄位，則應用程式會藉由設定 *BufferLength* 引數，將欄位的本質指出至驅動程式管理員。 *BufferLength* 可以有下列值：  
  
-   如果 *DiagInfoPtr* 是字元字串的指標，則 *BufferLength* 是字串或 SQL_NTS 的長度。  
  
-   如果 *DiagInfoPtr* 是二進位緩衝區的指標，則應用程式會將 SQL_LEN_BINARY_ATTR (*長度*) 宏的結果放在 *BufferLength*中。 這會在 *BufferLength*中放置負數值。  
  
-   如果 *DiagInfoPtr* 是字元字串或二進位字串以外的值指標， *BufferLength* 應該會有 SQL_IS_POINTER 的值。  
  
-   如果* \* DiagInfoPtr*包含固定長度的資料類型，則會視需要將*BufferLength* SQL_IS_INTEGER、SQL_IS_UINTEGER、SQL_IS_SMALLINT 或 SQL_IS_USMALLINT。  
  
 *StringLengthPtr*  
 出緩衝區的指標，此緩衝區會傳回位元組總數 (不包括 null 終止字元所需的位元組數目，) 可在 DiagInfoPtr 中傳回的 \* *DiagInfoPtr*字元資料。 如果可傳回的位元組數目大於或等於*BufferLength*，DiagInfoPtr 中的文字 \* *DiagInfoPtr*會被截斷為*BufferLength*減去 null 終止字元的長度。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR、SQL_INVALID_HANDLE 或 SQL_NO_DATA。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagField** 不會張貼本身的診斷記錄。 它會使用下列傳回值來報告本身執行的結果：  
  
-   SQL_SUCCESS：函式已成功傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO： \* *DiagInfoPtr*太小，無法保存要求的診斷欄位。 因此，[診斷] 欄位中的資料會被截斷。 若要判斷是否發生截斷，應用程式必須將 *BufferLength* 與可用的實際位元組數目（寫入 **StringLengthPtr*）進行比較。  
  
-   SQL_INVALID_HANDLE： *HandleType* 和 *Handle* 所指出的控制碼不是有效的控制碼。  
  
-   SQL_ERROR：發生下列其中一種情況：  
  
    -   *以* 引數不是有效的值之一。  
  
    -   *以* 引數是 SQL_DIAG_CURSOR_ROW_COUNT、SQL_DIAG_DYNAMIC_FUNCTION、SQL_DIAG_DYNAMIC_FUNCTION_CODE 或 SQL_DIAG_ROW_COUNT，但 *句* 柄不是語句控制碼。  (驅動程式管理員會傳回此診斷。 )   
  
    -   當*以*指出來自診斷記錄的欄位時 *，RecNumber*引數為負數或0。 標頭欄位會忽略*RecNumber* 。  
  
    -   要求的值是字元字串，而 *BufferLength* 小於零。  
  
    -   使用非同步通知時，控制碼上的非同步作業未完成。  
  
-   SQL_NO_DATA： *RecNumber*大於*控制碼*中指定之控制碼所存在的診斷記錄數目。 如果沒有任何用於*處理*的診斷記錄，此函數也會傳回任何正面*RecNumber* SQL_NO_DATA。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫 **SQLGetDiagField** 來完成三個目標的其中一個：  
  
1.  當函式呼叫傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO (或 SQL_NEED_DATA **SQLBrowseConnect** 函數) 時，取得特定的錯誤或警告資訊。  
  
2.  若要在使用 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos** 的呼叫來執行插入、刪除或更新作業時，判斷受影響的資料列數目 (從 SQL_DIAG_ROW_COUNT 的標頭欄位) ，或判斷存在於目前開啟之資料指標中的資料列數目，如果驅動程式可以從 SQL_DIAG_CURSOR_ROW_COUNT 標頭欄位) 中提供這項資訊 (。  
  
3.  判斷 **SQLExecDirect** 或 **SQLExecute** 的呼叫所執行的函式 (從 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 標頭欄位) 。  
  
 任何 ODBC 函數都可以在每次呼叫時張貼零個或更多的診斷記錄，讓應用程式可以在任何 ODBC 函式呼叫之後呼叫 **SQLGetDiagField** 。 任何一次都可以儲存的診斷記錄數目沒有任何限制。 **SQLGetDiagField** 只會抓取最近與 *控制碼* 引數中所指定之診斷資料結構相關聯的診斷資訊。 如果應用程式呼叫 **SQLGetDiagField** 或 **SQLGETDIAGREC**以外的 ODBC 函數，則會遺失先前呼叫中具有相同控制碼的任何診斷資訊。  
  
 只要**SQLGetDiagField**傳回 SQL_SUCCESS，應用程式就可以藉由遞增*RecNumber*來掃描所有診斷記錄。 狀態記錄的數目會顯示在 SQL_DIAG_NUMBER 標頭欄位中。 對 **SQLGetDiagField** 的呼叫不會與標頭和記錄欄位有破壞性。 應用程式稍後可以再次呼叫 **SQLGetDiagField** ，以從記錄取出欄位，只要在過渡期間未呼叫診斷函數以外的函式，就會在相同的控制碼上張貼記錄。  
  
 應用程式可以在任何時間呼叫 **SQLGetDiagField** 來傳回任何診斷欄位，但 SQL_DIAG_CURSOR_ROW_COUNT 或 SQL_DIAG_ROW_COUNT，除非 *控制碼* 不是語句控制碼，否則會傳回 SQL_ERROR。 如果未定義任何其他診斷欄位，則呼叫 **SQLGetDiagField** 將會傳回 SQL_SUCCESS (未提供任何其他診斷) 且未針對該欄位傳回未定義的值。  
  
 如需詳細資訊，請參閱 [使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) 和 [執行 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫非以非同步方式執行的 API 將會產生 HY010 「函式順序錯誤」。 但是，在非同步作業完成之前，無法抓取錯誤記錄。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制碼類型都可以有相關聯的診斷資訊。 *HandleType*引數會指出*句*柄的控制碼類型。  
  
 某些標頭和記錄欄位無法針對環境、連接、語句和描述項控制碼傳回。 欄位未適用的控制碼，會在後面的「標頭欄位」和「記錄欄位」區段中指出。  
  
 如果 *HandleType* 是 SQL_HANDLE_ENV， *控制碼* 可以是共用或非共用的環境控制碼。  
  
 沒有任何驅動程式特定的標頭診斷欄位應該與環境控制碼相關聯。  
  
 描述項控制碼唯一定義的診斷標頭欄位是 SQL_DIAG_NUMBER 和 SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>以引數  
 這個引數表示診斷資料結構所需的欄位識別碼。 如果 *RecNumber* 大於或等於1，則欄位中的資料會描述函式所傳回的診斷資訊。 如果 *RecNumber* 為0，則欄位位於診斷資料結構的標頭中，因此會包含傳回診斷資訊之函式呼叫的相關資料，而不是特定資訊。  
  
 驅動程式可以在診斷資料結構中定義驅動程式特定的標頭和記錄欄位。  
  
 使用 ODBC 2.x*驅動程式的 odbc 3.x 應用程式*將 *.x*只能使用 SQL_DIAG_CLASS_ORIGIN、SQL_DIAG_CLASS_SUBCLASS_ORIGIN、SQL_DIAG_CONNECTION_NAME、SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_NUMBER、SQL_DIAG_RETURNCODE、SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE 的*以*引數來呼叫**SQLGetDiagField** 。 所有其他診斷欄位將會傳回 SQL_ERROR。  
  
## <a name="header-fields"></a>標頭欄位  
 下表所列的標頭欄位可以包含在 *以* 引數中。  
  
|以|傳回類型|傳回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此欄位包含資料指標中的資料列計數。 其語義取決於 **SQLGetInfo** 資訊類型 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2 和 SQL_STATIC_CURSOR_ATTRIBUTES2，指出 (和 SQL_CA2_CRC_EXACT 位 SQL_CA2_CRC_APPROXIMATE 中，每個資料指標類型) 可使用的資料列計數。<br /><br /> 只有在呼叫 **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResults** 之後，這個欄位的內容才會定義給語句控制碼。 在語句控制碼以外的 SQL_DIAG_CURSOR_ROW_COUNT*以*呼叫**SQLGetDiagField**將會傳回 SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR|這是描述基礎函數所執行之 SQL 語句的字串。  (請參閱本節後面的「動態函式欄位的值」，以取得特定值。 ) 此欄位的內容只會定義給語句控制碼，而且只會在呼叫 **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResults**時定義。 在語句控制碼以外的 SQL_DIAG_DYNAMIC_FUNCTION*以*呼叫**SQLGetDiagField**將會傳回 SQL_ERROR。 在呼叫 **SQLExecute** 或 **SQLExecDirect**之前，這個欄位的值是未定義的。|  
|SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|這是描述基礎函數所執行之 SQL 語句的數值代碼。  (請參閱本節後面的「動態函式欄位的值」，以取得特定值。 ) 此欄位的內容只會定義給語句控制碼，而且只會在呼叫 **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResults**之後。 在語句控制碼以外的 SQL_DIAG_DYNAMIC_FUNCTION_CODE*以*呼叫**SQLGetDiagField**將會傳回 SQL_ERROR。 在呼叫 **SQLExecute** 或 **SQLExecDirect**之前，這個欄位的值是未定義的。|  
|SQL_DIAG_NUMBER|SQLINTEGER|適用于指定之控制碼的狀態記錄數目。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|傳回由函式傳回的程式碼。 如需傳回碼清單，請參閱傳回 [碼](../../../odbc/reference/develop-app/return-codes-odbc.md)。 驅動程式不需要執行 SQL_DIAG_RETURNCODE;它一律由驅動程式管理員來執行。 如果 *控制碼*上尚未呼叫函式，則會傳回 SQL_DIAG_RETURNCODE 的 SQL_SUCCESS。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|受 **SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或 **SQLSetPos**所執行之插入、刪除或更新影響的資料列數目。 它是在執行資料 *指標規格* 之後定義的驅動程式。 此欄位的內容只會針對語句控制碼來定義。 在語句控制碼以外的 SQL_DIAG_ROW_COUNT*以*呼叫**SQLGetDiagField**將會傳回 SQL_ERROR。 這個欄位中的資料也會在**SQLRowCount**的*RowCountPtr*引數中傳回。 這個欄位中的資料會在每次 nondiagnostic 函式呼叫之後重設，而 **SQLRowCount** 所傳回的資料列計數會維持不變，直到將語句設回備妥或配置的狀態。|  
  
## <a name="record-fields"></a>記錄欄位  
 下表所列的記錄欄位可以包含在 *以* 引數中。  
  
|以|傳回類型|傳回|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR|字串，表示定義此記錄中 SQLSTATE 值之類別部分的檔。 針對 Open Group 和 ISO 呼叫層級介面所定義的所有 SQLSTATEs，其值為 "ISO 9075"。 針對 ODBC 特定的 SQLSTATEs (其 SQLSTATE 類別為 "IM" 的所有 ) ，其值為 "ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果 SQL_DIAG_ROW_NUMBER 欄位在資料列集或一組參數中是有效的資料列編號，這個欄位就會包含代表結果集中資料行編號的值，或是參數集中的參數編號。 結果集資料行編號一律從1開始;如果此狀態記錄與書簽資料行有關，則欄位可以為零。 參數編號從1開始。 如果狀態記錄未與資料行編號或參數編號相關聯，則它的值 SQL_NO_COLUMN_NUMBER。 如果驅動程式無法判斷與此記錄相關聯的資料行編號或參數編號，此欄位的值 SQL_COLUMN_NUMBER_UNKNOWN。<br /><br /> 此欄位的內容只會針對語句控制碼來定義。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR|字串，表示與診斷記錄相關之連接的名稱。 此欄位為驅動程式定義。 針對與環境控制碼相關聯的診斷資料結構，以及與任何連接沒有關聯的診斷資料結構，此欄位是長度為零的字串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR|有關錯誤或警告的告知性訊息。 此欄位的格式如 [診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)中所述。 診斷郵件內文沒有最大長度。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驅動程式/資料來源特定的原生錯誤碼。 如果沒有原生錯誤碼，驅動程式會傳回0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此欄位包含資料列集中的資料列編號，或是與狀態記錄相關聯的參數集合中的參數編號。 資料列編號和參數編號的開頭為1。 如果此狀態記錄未與資料列編號或參數編號相關聯，這個欄位的值 SQL_NO_ROW_NUMBER。 如果驅動程式無法判斷與此記錄相關聯的資料列編號或參數編號，此欄位的值 SQL_ROW_NUMBER_UNKNOWN。<br /><br /> 此欄位的內容只會針對語句控制碼來定義。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR|字串，表示診斷記錄所關聯的伺服器名稱。 這與使用 SQL_DATA_SOURCE_NAME 選項針對 **SQLGetInfo** 呼叫所傳回的值相同。 針對與環境控制碼相關聯的診斷資料結構，以及與任何伺服器無關的診斷資料結構，此欄位是長度為零的字串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR|五個字元的 SQLSTATE 診斷程式代碼。 如需詳細資訊，請參閱 [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR|具有與 SQL_DIAG_CLASS_ORIGIN 相同格式和有效值的字串，可識別 SQLSTATE 程式碼子類別部分的定義部分。 傳回 "ODBC 3.0" 的 ODBC 特定 SQLSTATES 包含下列各項：<br /><br /> 01S00、01S01、01S02、01S06、01S07、07S01、08S01、21S01、21S02、25S01、25S02、25S03、42S01、42S02、42S11、42S12、42S21、42S22、HY095、HY097、HY098、HY099、HY100、HY101、HY105、HY107、HY109、HY110、HY111、HYT00、HYT01、IM001、IM002、IM003、IM004、IM005、IM006、IM007、IM008、IM010、IM011、IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動態函數位段的值  
 下表描述適用于 **SQLExecute** 或 **SQLExecDirect**呼叫所執行之每個 SQL 語句類型的 SQL_DIAG_DYNAMIC_FUNCTION 和 SQL_DIAG_DYNAMIC_FUNCTION_CODE 值。 驅動程式可以將驅動程式定義的值新增至列出的值。  
  
|SQL 陳述式<br /><br /> 執行| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION| 的值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter-domain 語句*|"ALTER DOMAIN"|SQL_DIAG_ALTER_DOMAIN|  
|*alter table 語句*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*判斷提示-定義*|「建立判斷提示」|SQL_DIAG_CREATE_ASSERTION|  
|*字元集定義*|「建立字元集」|SQL_DIAG_CREATE_CHARACTER_SET|  
|*定序-定義*|[建立定序]|SQL_DIAG_CREATE_COLLATION|  
|*domainn>-定義*|[建立網域]|SQL_DIAG_CREATE_DOMAIN|
|*create-index 語句*|「建立索引」|SQL_DIAG_CREATE_INDEX|  
|*create-table 語句*|"CREATE TABLE"|SQL_DIAG_CREATE_TABLE|  
|*create-view 語句*|「建立視圖」|SQL_DIAG_CREATE_VIEW|  
|*資料指標規格*|「選取資料指標」|SQL_DIAG_SELECT_CURSOR|  
|*delete 語句位置*|「動態刪除資料指標」|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete 語句-已搜尋*|"DELETE WHERE"|SQL_DIAG_DELETE_WHERE|  
|*drop assertion 語句*|「DROP ASSERTION」|SQL_DIAG_DROP_ASSERTION|  
|*drop-字元集-stmt*|「DROP CHARACTER SET」|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop-定序-語句*|「捨棄定序」|SQL_DIAG_DROP_COLLATION|  
|*drop-domain 語句*|"DROP DOMAIN"|SQL_DIAG_DROP_DOMAIN|  
|*drop-index 語句*|"DROP INDEX"|SQL_DIAG_DROP_INDEX|  
|*drop-schema 語句*|"DROP SCHEMA"|SQL_DIAG_DROP_SCHEMA|  
|*drop table 語句*|"DROP TABLE"|SQL_DIAG_DROP_TABLE|  
|*drop-轉譯語句*|「捨棄轉譯」|SQL_DIAG_DROP_TRANSLATION|  
|*drop view 語句*|"DROP VIEW"|SQL_DIAG_DROP_VIEW|  
|*grantstatement*|准許|SQL_DIAG_GRANT|
|*insert 語句*|插入|SQL_DIAG_INSERT|  
|*ODBC-程式延伸*|聯繫|SQL_DIAG_ 呼叫|  
|*revoke 語句*|[|SQL_DIAG_REVOKE|  
|*架構定義*|[建立架構]|SQL_DIAG_CREATE_SCHEMA|  
|*轉譯-定義*|[建立翻譯]|SQL_DIAG_CREATE_TRANSLATION|  
|*update-語句-定位*|「動態更新資料指標」|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update 語句-搜尋*|"UPDATE WHERE"|SQL_DIAG_UPDATE_WHERE|  
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

 狀態記錄會根據資料列編號和診斷型別放置於序列中。 驅動程式管理員會決定傳回其產生之狀態記錄的最終順序。 驅動程式會決定傳回其產生之狀態記錄的最終順序。  
  
 如果驅動程式管理員和驅動程式都張貼診斷記錄，驅動程式管理員會負責排序它們。  
  
 如果有兩個以上的狀態記錄，則會先以資料列編號來決定記錄的順序。 下列規則適用于判斷每個資料列的診斷記錄順序：  
  
-   未對應至任何資料列的記錄會出現在對應到特定資料列的記錄前面，因為 SQL_NO_ROW_NUMBER 定義為-1。  
  
-   資料列編號未知的記錄會出現在所有其他記錄前面，因為 SQL_ROW_NUMBER_UNKNOWN 定義為-2。  
  
-   對於特定資料列的所有記錄，記錄都會依 [SQL_DIAG_ROW_NUMBER] 欄位中的值來排序。 系統會列出受影響的第一個資料列的所有錯誤和警告，然後影響下一個資料列的所有錯誤和警告，依此類推。  
  
> [!NOTE]
>  如果 odbc 2.x 驅動程式傳回資料列) 中的 SQLSTATE 01S01 (錯誤，或者)  (*如果 odbc 3.x*驅動程式在已定位於**SQLExtendedFetch**的資料**指標上呼叫** **SQLSetPos** ，*則 odbc 3.x 驅動程式管理員*不會排序診斷佇列中的狀態記錄由*odbc 2.x 驅動*程式傳回。  
  
 在每個資料列中，或針對未對應到資料列或資料列編號不是未知的所有記錄，或是資料列編號等於 SQL_NO_ROW_NUMBER 的所有記錄內，所列的第一個記錄是由使用一組排序規則來決定。 第一筆記錄之後，其他會影響資料列的記錄順序未定義。 應用程式無法在第一次記錄之後，假設錯誤之前的警告。 應用程式應該掃描完整的診斷資料結構，以取得函式呼叫失敗的完整資訊。  
  
 下列規則是用來判斷資料列中的第一筆記錄。 具有最高排名的記錄是第一筆記錄。 排名記錄時，不會考慮記錄 (驅動程式管理員、驅動程式、閘道等) 的來源。  
  
-   **錯誤** 描述錯誤的狀態記錄具有最高等級。 下列規則適用于排序錯誤：  
  
    -   指出交易失敗或可能交易失敗的記錄 outrank 所有其他記錄。  
  
    -   如果有兩個以上的記錄描述相同的錯誤狀況，則 SQLSTATEs 由 Open Group CLI 規格所定義 (類別03到 HZ) outrank ODBC 和驅動程式定義的 SQLSTATEs。  
  
-   **執行-未定義資料值** 描述驅動程式未定義任何資料值 (類別 02) 具有第二個最高排名的狀態記錄。  
  
-   **警告** 描述 (類別 01) 之警告的狀態記錄具有最低等級。 如果有兩個以上的記錄描述相同的警告條件，則會 outrank ODBC 定義和驅動程式定義的 SQLSTATEs 所定義的警告 SQLSTATEs。  
  
## <a name="related-functions"></a>相關函數  
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|取得診斷資料結構的多個欄位|[SQLGetDiagRec 函式](sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
