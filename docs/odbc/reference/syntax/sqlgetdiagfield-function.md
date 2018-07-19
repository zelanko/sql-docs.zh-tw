---
title: SQLGetDiagField 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 39ae1a58454a7ce70f5ae2a33d951a769223fdd1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32922793"
---
# <a name="sqlgetdiagfield-function"></a>SQLGetDiagField 函數
**一致性**  
 版本引進了： ODBC 3.0 版的標準相容性： ISO 92  
  
 **摘要**  
 **SQLGetDiagField**傳回的欄位包含錯誤、 警告和狀態資訊的診斷資料結構 （與指定的控制代碼相關聯） 之記錄的目前值。  
  
## <a name="syntax"></a>語法  
  
```  
  
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
 [輸入]描述診斷所需的控制代碼的類型控制代碼類型識別項。 必須是下列其中之一：  
  
-   利用 SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   利用 SQL_HANDLE_STMT  
  
 只在驅動程式管理員和驅動程式會使用 SQL_HANDLE_DBC_INFO_TOKEN 控制代碼。 應用程式不應該使用此控制代碼類型。 如需 SQL_HANDLE_DBC_INFO_TOKEN 的詳細資訊，請參閱[開發 ODBC 驅動程式中的連接集區感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)。  
  
 *Handle*  
 [輸入]如需診斷資料結構，所指定的類型的控制代碼*HandleType*。 如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或共用的環境控制代碼。  
  
 *RecNumber*  
 [輸入]指出從中應用程式搜尋資訊的狀態記錄。 狀態記錄編號 1。 如果*Sqlgetdiagfield*引數指出診斷標頭的任何欄位*RecNumber*會被忽略。 如果沒有，它應該是大於 0。  
  
 *Sqlgetdiagfield*  
 [輸入]表示其值是要傳回的診斷欄位。 如需詳細資訊，請參閱 「*Sqlgetdiagfield*引數 」 一節中的 [意見]。  
  
 *DiagInfoPtr*  
 [輸出]這是要傳回的診斷資訊的緩衝區指標。 資料型別取決於值*Sqlgetdiagfield*。 如果*DiagInfoPtr*是整數類型、 應用程式應使用的緩衝區 SQLULEN 和初始化的值為 0，然後再呼叫這個函式，為部分驅動程式可能只寫入的低 32 位元或 16 位元的緩衝區，並將較高順序位元不變。  
  
 如果*DiagInfoPtr*是 NULL， *StringLengthPtr*仍會傳回的總位元組數 （不含字元資料 null 結束字元） 可用來傳回所指向之緩衝區中*DiagInfoPtr*。  
  
 *BufferLength*  
 [輸入]如果*Sqlgetdiagfield*是 ODBC 定義的診斷和*DiagInfoPtr*指向字元字串或二進位的緩衝區，這個引數應該是長度\* *DiagInfoPtr*. 如果*Sqlgetdiagfield*是 ODBC 定義的欄位和\* *DiagInfoPtr*是整數， *Columnsize*會被忽略。 如果中的值 *\*DiagInfoPtr*是 Unicode 字串 (當呼叫**SQLGetDiagFieldW**)、 *Columnsize*引數必須是偶數。  
  
 如果*Sqlgetdiagfield*是驅動程式定義的欄位，應用程式設定指出欄位驅動程式管理員性質*Columnsize*引數。 *Columnsize*可以是下列值：  
  
-   如果*DiagInfoPtr*是字元字串的指標*Columnsize*是 SQL_NTS 之字串的長度。  
  
-   如果*DiagInfoPtr* SQL_LEN_BINARY_ATTR 的結果是二進位的緩衝區，應用程式位置的指標 (*長度*) 中的巨集*Columnsize*。 這樣做會放在負值*Columnsize*。  
  
-   如果*DiagInfoPtr*是字元字串或二進位字串以外的值的指標*Columnsize*應該有 SQL_IS_POINTER 的值。  
  
-   如果 *\*DiagInfoPtr*包含固定長度資料類型， *Columnsize*是 SQL_IS_INTEGER、 SQL_IS_UINTEGER、 SQL_IS_SMALLINT 或 SQL_IS_USMALLINT，視需要。  
  
 *StringLengthPtr*  
 [輸出]這是要傳回的總位元組數 （不包括 null 結束字元所需的位元組數） 的緩衝區指標可用來傳回中\* *DiagInfoPtr*，字元資料。 如果傳回可用的位元組數目大於或等於*Columnsize*中的文字\* *DiagInfoPtr*會被截斷成*Columnsize*減號null 結束字元的長度。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR、 SQL_INVALID_HANDLE 或 sql_no_data 為止。  
  
## <a name="diagnostics"></a>診斷  
 **SQLGetDiagField**不會將其本身的診斷記錄。 它會使用下列傳回值報告自己執行的結果：  
  
-   SQL_SUCCESS： 函式成功地傳回診斷資訊。  
  
-   SQL_SUCCESS_WITH_INFO: \* *DiagInfoPtr*太小，無法存放要求的診斷欄位。 因此，[診斷] 欄位中的資料已遭截斷。 若要判定發生截斷，應用程式必須比較*Columnsize*實際可用的位元組數目，這會寫入至 **StringLengthPtr*。  
  
-   SQL_INVALID_HANDLE： 所指定的控制代碼*HandleType*和*處理*不是有效的控制代碼。  
  
-   SQL_ERROR： 下列其中一項發生：  
  
    -   *Sqlgetdiagfield*引數不是其中一個有效的值。  
  
    -   *Sqlgetdiagfield*引數是 SQL_DIAG_CURSOR_ROW_COUNT、 SQL_DIAG_DYNAMIC_FUNCTION、 為 SQL_DIAG_DYNAMIC_FUNCTION_CODE 或 SQL_DIAG_ROW_COUNT，但*處理*不是陳述式控制代碼。 （驅動程式管理員會傳回此診斷）。  
  
    -   *RecNumber*引數是負數或 0 時*Sqlgetdiagfield*指示的診斷記錄的欄位。 *RecNumber*會忽略標頭欄位。  
  
    -   所要求的值為字元字串和*Columnsize*小於零。  
  
    -   當使用非同步通知時，控制代碼的非同步作業未完成。  
  
-   SQL_NO_DATA: *RecNumber*診斷記錄中指定的控制代碼已存在的數目大於*處理。* 函式也會傳回 SQL_NO_DATA 任何正值*RecNumber*是否有任何的診斷記錄*處理*。  
  
## <a name="comments"></a>註解  
 應用程式通常會呼叫**SQLGetDiagField**完成三個目標的其中一個：  
  
1.  若要取得特定錯誤或警告資訊時傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 函式呼叫 (如 SQL_NEED_DATA 或**SQLBrowseConnect**函式)。  
  
2.  若要判斷資料來源中插入、 刪除或更新作業所執行之呼叫時所影響的資料列數目**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos** （從 SQL_DIAG_ROW_COUNT 標頭欄位），或要判定目前開啟資料指標中所存在的資料列數目，如果此驅動程式可以提供這項資訊 (從SQL_DIAG_CURSOR_ROW_COUNT 標頭欄位）。  
  
3.  若要判斷哪些函式呼叫中執行了**SQLExecDirect**或**SQLExecute** （從 SQL_DIAG_DYNAMIC_FUNCTION 和為 SQL_DIAG_DYNAMIC_FUNCTION_CODE 標頭欄位）。  
  
 任何 ODBC 函數可以張貼零或多個診斷記錄每次呼叫它時，讓應用程式可以呼叫**SQLGetDiagField**之後的任何 ODBC 函數呼叫。 可以一次儲存的診斷記錄的數目沒有限制。 **SQLGetDiagField**只擷取的診斷資訊中指定的診斷資料結構與最近關聯*處理*引數。 如果應用程式呼叫 ODBC 函數以外**SQLGetDiagField**或**SQLGetDiagRec**，從先前使用相同的控制代碼呼叫任何診斷資訊都會遺失。  
  
 應用程式可以是遞增掃描所有的診斷記錄*RecNumber*，只要**SQLGetDiagField**都會傳回 SQL_SUCCESS。 狀態記錄的數目會指出在 SQL_DIAG_NUMBER 標頭欄位。 呼叫**SQLGetDiagField**會恢復至標頭和記錄欄位。 應用程式可以呼叫**SQLGetDiagField**稍後再記錄，從擷取的欄位，只要在過渡時期，會在相同的控制代碼張貼記錄尚未呼叫以外診斷函式的函式。  
  
 應用程式可以呼叫**SQLGetDiagField**傳回任何診斷欄位，在任何時候，除了 SQL_DIAG_CURSOR_ROW_COUNT 或 SQL_DIAG_ROW_COUNT，則會傳回 SQL_ERROR*處理*不是陳述式控制代碼。 如果未定義，任何其他診斷欄位，則呼叫**SQLGetDiagField**會傳回 SQL_SUCCESS，（假設沒有其他診斷就會發生） 且未定義的值會傳回欄位。  
  
 如需詳細資訊，請參閱[使用 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)和[實作 SQLGetDiagRec 和 SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)。  
  
 呼叫不同的非同步執行的應用程式開發介面，將會產生 HY010 「 函數順序錯誤 」。 不過，在非同步作業完成之前，無法擷取記錄時發生錯誤。  
  
## <a name="handletype-argument"></a>HandleType 引數  
 每個控制代碼類型可以有與其相關聯的診斷資訊。 *HandleType*引數表示的控制代碼類型*處理*。  
  
 某些標頭和記錄欄位無法傳回的環境、 連接、 陳述式，以及描述項控制代碼。 不適用欄位這些控點會以 「 標頭欄位 」 和 「 記錄欄位 」 後面的章節。  
  
 如果*HandleType*為 SQL_HANDLE_ENV，*處理*可以是共用或共用的環境控制代碼。  
  
 沒有驅動程式特定標頭的診斷欄位應該與環境控制代碼相關聯。  
  
 只有診斷標頭欄位所定義的描述項控制代碼是 SQL_DIAG_NUMBER 和 SQL_DIAG_RETURNCODE。  
  
## <a name="diagidentifier-argument"></a>Sqlgetdiagfield 引數  
 這個引數表示從診斷資料結構所需之欄位的識別項。 如果*RecNumber*大於或等於 1，欄位中的資料描述函數所傳回的診斷資訊。 如果*RecNumber*是 0，則欄位診斷資料結構中的標頭中，因此會包含屬於函式呼叫不傳回的特定資訊的診斷資訊的資料。  
  
 驅動程式可以定義驅動程式特定標頭和記錄欄位中的診斷資料結構。  
  
 ODBC 3 *.x*應用程式使用 ODBC 2 *.x*驅動程式將無法呼叫**SQLGetDiagField**只能搭配*Sqlgetdiagfield*SQL_DIAG_CLASS_ORIGIN、 SQL_DIAG_CLASS_SUBCLASS_ORIGIN、 SQL_DIAG_CONNECTION_NAME、 SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_NUMBER、 SQL_DIAG_RETURNCODE、 SQL_DIAG_SERVER_NAME 或 SQL_DIAG_SQLSTATE 的引數。 所有其他診斷欄位將會傳回 SQL_ERROR。  
  
## <a name="header-fields"></a>標頭欄位  
 下表所列的標頭欄位可以包含在*Sqlgetdiagfield*引數。  
  
|Sqlgetdiagfield|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CURSOR_ROW_COUNT|SQLLEN|此欄位包含資料指標中的資料列的計數。 其語意取決於**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2 和 SQL_STATIC_CURSOR_ATTRIBUTES2，這表示它的資訊類型資料列計數可供每個資料指標類型 （SQL_CA2_CRC_EXACT 和 SQL_CA2_CRC_APPROXIMATE 位元）。<br /><br /> 定義此欄位的內容只適用於陳述式控制代碼，之後才**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**已呼叫。 呼叫**SQLGetDiagField**與*Sqlgetdiagfield* SQL_DIAG_CURSOR_ROW_COUNT 上以外的陳述式的控制代碼將會傳回 SQL_ERROR。|  
|SQL_DIAG_DYNAMIC_FUNCTION|SQLCHAR *|這是描述基礎函式執行的 SQL 陳述式的字串。 （請參閱"欄位的值動態函數，「 稍後在本節中的特定值）。定義此欄位的內容只適用於陳述式控制代碼，只有在呼叫之後**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 呼叫**SQLGetDiagField**與*Sqlgetdiagfield* SQL_DIAG_DYNAMIC_FUNCTION 上以外的陳述式的控制代碼將會傳回 SQL_ERROR。 這個欄位的值未定義呼叫之前**SQLExecute**或**SQLExecDirect**。|  
|為 SQL_DIAG_DYNAMIC_FUNCTION_CODE|SQLINTEGER|這是描述由基礎函式執行的 SQL 陳述式的數字代碼。 （請參閱 「 值的動態函式欄位，」 稍後在本章節，特定值）。定義此欄位的內容只適用於陳述式控制代碼，只有在呼叫之後**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**。 呼叫**SQLGetDiagField**與*Sqlgetdiagfield*上為 SQL_DIAG_DYNAMIC_FUNCTION_CODE 以外的陳述式的控制代碼將會傳回 SQL_ERROR。 這個欄位的值未定義呼叫之前**SQLExecute**或**SQLExecDirect**。|  
|SQL_DIAG_NUMBER|SQLINTEGER|狀態記錄可供指定的控制代碼數目。|  
|SQL_DIAG_RETURNCODE|SQLRETURN|函數所傳回的傳回碼。 如需傳回碼的清單，請參閱[傳回碼](../../../odbc/reference/develop-app/return-codes-odbc.md)。 驅動程式不需要實作 SQL_DIAG_RETURNCODE;它一律被實作由驅動程式管理員。 如果尚未上呼叫任何函數*處理*，SQL_DIAG_RETURNCODE 就會傳回 SQL_SUCCESS。|  
|SQL_DIAG_ROW_COUNT|SQLLEN|受到 insert、 delete 或 update 所執行的資料列數目**SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**. 它是由驅動程式定義之後*資料指標規格*已經執行。 此欄位的內容只能陳述式控制代碼定義。 呼叫**SQLGetDiagField**與*Sqlgetdiagfield* SQL_DIAG_ROW_COUNT 上以外的陳述式的控制代碼將會傳回 SQL_ERROR。 此欄位中的資料也會傳回在*RowCountPtr*引數的**SQLRowCount**。 此欄位中的資料會重設在每次 nondiagnostic 函式呼叫，而所傳回的資料列計數**SQLRowCount**維持不變，直到陳述式重設為已備妥或已配置的狀態。|  
  
## <a name="record-fields"></a>記錄欄位  
 下表所列的記錄欄位可以包含在*Sqlgetdiagfield*引數。  
  
|Sqlgetdiagfield|傳回類型|傳回值|  
|--------------------|-----------------|-------------|  
|SQL_DIAG_CLASS_ORIGIN|SQLCHAR *|字串，表示此記錄中定義的 SQLSTATE 值的類別部分文件。 其值為"ISO 9075"Open Group 和 ISO 呼叫層級介面所定義的所有 Sqlstate。 對於特定的 ODBC Sqlstate （所有項目，其 SQLSTATE 類別是"IM"），其值是"ODBC 3.0"。|  
|SQL_DIAG_COLUMN_NUMBER|SQLINTEGER|如果 SQL_DIAG_ROW_NUMBER 欄位為有效的資料列中的資料列集或一組參數，此欄位包含值，表示結果集中的資料行編號或參數中的數字的參數集。 結果集資料行數字一定會開始於 1。如果這個狀態記錄屬於書籤資料行，此欄位可以是零。 參數號碼從 1 開始。 如果狀態記錄不是相關聯的資料行數字或參數數目，有 SQL_NO_COLUMN_NUMBER 的值。 如果驅動程式無法判斷這個記錄相關聯的參數數目的資料行數目，此欄位有 SQL_COLUMN_NUMBER_UNKNOWN 的值。<br /><br /> 此欄位的內容只能陳述式控制代碼定義。|  
|SQL_DIAG_CONNECTION_NAME|SQLCHAR *|字串，表示連接至相關的診斷記錄的名稱。 這個欄位是驅動程式定義。 環境控制代碼相關聯的診斷資料結構和任何連接並沒有關聯的診斷，這個欄位是零長度字串。|  
|SQL_DIAG_MESSAGE_TEXT|SQLCHAR *|參考用錯誤或警告訊息。 此欄位格式中所述[診斷訊息](../../../odbc/reference/develop-app/diagnostic-messages.md)。 沒有最大長度為診斷訊息文字。|  
|SQL_DIAG_NATIVE|SQLINTEGER|驅動程式/資料來源專用原生錯誤碼。 如果沒有原生錯誤程式碼，此驅動程式會傳回 0。|  
|SQL_DIAG_ROW_NUMBER|SQLLEN|此欄位會包含資料列中的數字資料列集或一組參數，與相關聯的狀態記錄中的參數號碼。 資料列號碼和參數號碼從 1 開始。 如果這個狀態記錄的逸出序列所關聯的資料列數目或參數數目，此欄位有 SQL_NO_ROW_NUMBER 的值。 如果驅動程式無法判斷這個記錄相關聯的參數數目的資料列數目，此欄位有 SQL_ROW_NUMBER_UNKNOWN 的值。<br /><br /> 此欄位的內容只能陳述式控制代碼定義。|  
|SQL_DIAG_SERVER_NAME|SQLCHAR *|表示與診斷記錄相關的伺服器名稱的字串。 它等同於呼叫的傳回值**SQLGetInfo** SQL_DATA_SOURCE_NAME 選項。 環境控制代碼相關聯的診斷資料結構，以及任何伺服器並沒有關聯的診斷，這個欄位是零長度字串。|  
|SQL_DIAG_SQLSTATE|SQLCHAR *|五個字元 SQLSTATE 診斷程式碼。 如需詳細資訊，請參閱[Sqlstate](../../../odbc/reference/develop-app/sqlstates.md)。|  
|SQL_DIAG_SUBCLASS_ORIGIN|SQLCHAR *|具有相同的格式和有效的值字串做為 SQL_DIAG_CLASS_ORIGIN 可識別子類別的部分的 SQLSTATE 程式碼定義的一部分。 這傳回"ODBC 3.0"ODBC 專屬 SQLSTATE 包括下列各項：<br /><br /> 01S00，01S01，01S02 的警告，01S06，01S07，07S01，08S01 以及 21S01，21S02，25S01，25S02，25S03，42S01，42S02，42S11，42S12，42S21，42S22，HY095、 HY097、 HY098、 HY099、 HY100、 HY101、 HY105、 HY107、 HY109、 HY110、 HY111、 HYT00、 HYT01、 IM001、 IM002、 IM003、 IM004、 IM005、 IM006，IM007、 IM008、 IM010、 IM011、 IM012。|  
  
## <a name="values-of-the-dynamic-function-fields"></a>動態函數欄位的值  
 下表描述 SQL_DIAG_DYNAMIC_FUNCTION 和為 SQL_DIAG_DYNAMIC_FUNCTION_CODE 的值，顯示套用至每個類型的呼叫所執行的 SQL 陳述式**SQLExecute**或**SQLExecDirect**. 驅動程式可以將驅動程式定義的值加入所列。  
  
|SQL 陳述式<br /><br /> 執行|值<br /><br /> SQL_DIAG_DYNAMIC_FUNCTION|值<br /><br /> 為 SQL_DIAG_DYNAMIC_FUNCTION_CODE|  
|--------------------------------|-----------------------------------------------|-----------------------------------------------------|  
|*alter 網域陳述式*|「 ALTER 網域 」|SQL_DIAG_ALTER_DOMAIN|  
|*alter table 陳述式*|"ALTER TABLE"|SQL_DIAG_ALTER_TABLE|  
|*判斷提示定義*|「 建立判斷提示 」|SQL_DIAG_CREATE_ASSERTION|  
|*字元設定定義*|「 建立字元集 」|SQL_DIAG_CREATE_CHARACTER_SET|  
|*定序定義*|「 建立定序 」|SQL_DIAG_CREATE_COLLATION|  
|*建立索引陳述式*|< CREATE INDEX >|SQL_DIAG_CREATE_INDEX|  
|*建立資料表陳述式*|「 建立資料表 」|SQL_DIAG_CREATE_TABLE|  
|*建立檢視陳述式*|「 建立檢視 」|SQL_DIAG_CREATE_VIEW|  
|*資料指標規格*|「 選取資料指標 」|SQL_DIAG_SELECT_CURSOR|  
|*delete 陳述式置於*|「 動態刪除 CURSOR"|SQL_DIAG_DYNAMIC_DELETE_CURSOR|  
|*delete 陳述式搜尋*|「 刪除位置 」|SQL_DIAG_DELETE_WHERE|  
n 層定義 *|「 建立網域 」|SQL_DIAG_CREATE_DOMAIN|  
|*drop 判斷提示陳述式*|「 卸除 ASSERTION 」|SQL_DIAG_DROP_ASSERTION|  
|*卸除字元-組 stmt*|「 卸除字元集 」|SQL_DIAG_DROP_CHARACTER_SET|  
|*drop 定序陳述式*|[卸除定序]|SQL_DIAG_DROP_COLLATION|  
|*drop 網域陳述式*|「 卸除網域 」|SQL_DIAG_DROP_DOMAIN|  
|*drop index 陳述式*|「 卸除索引 」|SQL_DIAG_DROP_INDEX|  
|*drop schema 陳述式*|「 卸除結構描述 」|SQL_DIAG_DROP_SCHEMA|  
|*drop table 陳述式*|「 卸除資料表 」|SQL_DIAG_DROP_TABLE|  
|*drop 轉譯陳述式*|「 卸除轉譯 」|SQL_DIAG_DROP_TRANSLATION|  
|*drop view 陳述式*|「 卸除檢視 」|SQL_DIAG_DROP_VIEW|  
-陳述式 *|「 授權 」|SQL_DIAG_GRANT|  
|*insert 陳述式*|「 插入 」|SQL_DIAG_INSERT|  
|*ODBC 程序延伸模組*|「 呼叫 」|SQL_DIAG_ 呼叫|  
|*revoke 陳述式*|「 REVOKE 」|SQL_DIAG_REVOKE|  
|*結構描述定義*|[建立結構描述]|SQL_DIAG_CREATE_SCHEMA|  
|*翻譯定義*|「 建立轉譯 」|SQL_DIAG_CREATE_TRANSLATION|  
|*update 陳述式置於*|「 動態更新資料指標 」|SQL_DIAG_DYNAMIC_UPDATE_CURSOR|  
|*update 陳述式搜尋*|「 更新位置 」|SQL_DIAG_UPDATE_WHERE|  
|Unknown|*空字串*|SQL_DIAG_UNKNOWN_STATEMENT|  
  
## <a name="sequence-of-status-records"></a>狀態記錄的序列  
 狀態記錄定位順序，根據資料列號碼和診斷的型別中。 驅動程式管理員會決定最終的順序，以傳回它產生的狀態記錄。 驅動程式會判斷要傳回狀態記錄，它會產生最終的順序。  
  
 診斷記錄所公佈的驅動程式管理員和驅動程式，驅動程式管理員會負責排序它們。  
  
 如果兩個或多個狀態記錄的記錄順序取決於第一次資料列數目。 下列規則適用於資料列所決定的診斷記錄順序：  
  
-   因為 SQL_NO_ROW_NUMBER 定義為-1 對應到特定的資料列中，記錄出現未對應到任何資料列的記錄。  
  
-   因為 SQL_ROW_NUMBER_UNKNOWN 定義為 – 2，資料列號碼為未知的記錄會出現在所有其他的記錄之前。  
  
-   屬於特定的資料列的所有記錄，記錄會依照 SQL_DIAG_ROW_NUMBER 欄位中的值。 列出所有錯誤和警告的第一個資料列受到影響，，然後所有錯誤和警告的下一個資料都列受影響，依此類推。  
  
> [!NOTE]  
>  ODBC 3 *.x*驅動程式管理員不會排序狀態記錄診斷的佇列中如果 SQLSTATE 01S01 （資料列中的錯誤） 由 ODBC 2 *.x*驅動程式或如果 SQLSTATE 01S01 （資料列中的錯誤） 由 ODBC3 *.x*驅動程式時**SQLExtendedFetch**稱為或**SQLSetPos**已被使用定位資料指標上呼叫**SQLExtendedFetch**.  
  
 內每個資料列，或所有未對應的資料列或資料列號碼是未知，這些記錄或資料列數等於 SQL_NO_ROW_NUMBER 所有這些記錄，第一個列出的記錄是由使用一組的排序規則決定。 第一筆記錄之後, 會影響資料列的其他記錄的順序是未定義。 應用程式不能假設錯誤之前的警告之後第一筆記錄。 應用程式應該掃描完成診斷資料結構，以取得失敗呼叫的函式的完整資訊。  
  
 下列規則可用來判斷資料列內的第一筆記錄。 具有最高等級的記錄是第一筆記錄。 資料錄 （驅動程式管理員、 驅動程式、 閘道和等等） 的來源不會被視為時排序記錄。  
  
-   **錯誤**描述錯誤的狀態記錄擁有最高的等級。 若要排序錯誤套用下列規則：  
  
    -   表示交易失敗或可能的交易失敗的記錄 outrank 所有其他的記錄。  
  
    -   如果兩個或多個記錄描述相同的錯誤狀況，請開啟群組 CLI 規格 （透過 HZ 類別 03） 所定義的 Sqlstate outrank ODBC 和驅動程式定義的 Sqlstate。  
  
-   **實作定義沒有資料值**描述驅動程式定義沒有資料值 （類別 02） 的狀態記錄都有第二個最高的等級。  
  
-   **警告**描述警告 （類別 01） 的狀態記錄具有最低順位。 如果兩個或多個記錄描述相同的警告狀況，然後警告開啟群組 CLI 規格所定義的 Sqlstate outrank ODBC 定義及驅動程式定義的 Sqlstate。  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|取得多個欄位的診斷資料結構|[SQLGetDiagRec 函式](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
