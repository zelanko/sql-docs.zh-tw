---
title: SQLBindParameter 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13f4c879f94118a2e2302a2032991e85551be0f7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538131"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函數

**合規性**  
 導入的版本：ODBC 2.0 標準合規性：ODBC  
  
 **摘要**  
 **SQLBindParameter**繫結至 SQL 陳述式中的參數標記的緩衝區。 **SQLBindParameter**支援繫結至 Unicode C 資料類型，即使基礎驅動程式不支援 Unicode 資料。  
  
> [!NOTE]  
>  此函數會取代 ODBC 1.0 函式**SQLSetParam**。 如需詳細資訊，請參閱 「 註解。 」  
  
## <a name="syntax"></a>語法  
  
```cpp
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>引數

 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *ParameterNumber*  
 [輸入]參數編號排序依序遞增的參數順序，從 1 開始。  
  
 *InputOutputType*  
 [輸入]參數的型別。 如需詳細資訊，請參閱 「*了*引數 」 中 「 註解。 」  
  
 *ValueType*  
 [輸入]參數的 C 資料類型。 如需詳細資訊，請參閱 「*ValueType*引數 」 中 「 註解。 」  
  
 *ParameterType*  
 [輸入]SQL 資料類型的參數。 如需詳細資訊，請參閱 「*ParameterType*引數 」 中 「 註解。 」  
  
 *ColumnSize*  
 [輸入]資料行或運算式的對應參數標記的大小。 如需詳細資訊，請參閱 「*ColumnSize*引數 」 中 「 註解。 」  
  
 如果您的應用程式將在 64 位元 Windows 作業系統上執行，請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *DecimalDigits*  
 [輸入]資料行或運算式的對應參數標記的小數位數。 如需有關資料行大小的詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *ParameterValuePtr*  
 [延遲的輸入]參數的資料緩衝區的指標。 如需詳細資訊，請參閱 「*ParameterValuePtr*引數 」 中 「 註解。 」  
  
 *BufferLength*  
 [輸入/輸出]長度*ParameterValuePtr*以位元組為單位的緩衝區。 如需詳細資訊，請參閱 「*Columnsize*引數 」 中 「 註解。 」  
  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式會在 64 位元作業系統上執行。  
  
 *StrLen_or_IndPtr*  
 [延遲的輸入]參數的長度的緩衝區指標。 如需詳細資訊，請參閱 「*StrLen_or_IndPtr*引數 」 中 「 註解。 」  
  
## <a name="returns"></a>傳回值

 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷

 當**SQLBindParameter**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLBindParameter** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  

|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|所識別的資料型別*ValueType*引數無法轉換成所識別之資料類型*ParameterType*引數。 請注意，此錯誤可能會傳回**SQLExecDirect**， **SQLExecute**，或**SQLPutData**在執行階段，而不是由**SQLBindParameter**.|  
|07009|描述項索引無效|(DM) 引數指定的值*Sqlbindparameter*是小於 1。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**在 **MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY003|無效的應用程式緩衝區類型|引數所指定的值*ValueType*不是有效的 C 資料類型或 SQL_C_DEFAULT。|  
|HY004|無效的 SQL 資料類型|指定的引數的值*ParameterType*不是有效的 ODBC SQL 資料類型識別項或驅動程式支援的驅動程式專屬 SQL 資料類型識別碼。|  
|HY009|無效的引數值|(DM) 引數*ParameterValuePtr*是 null 指標，該引數*StrLen_or_IndPtr* null 指標，而引數*了*未 SQL_PARAM_輸出。<br /><br /> (DM) SQL_PARAM_OUTPUT，其中的引數*ParameterValuePtr*是 null 指標，C 類型是字元或二進位和 Columnsize (*cbValueMax*) 大於 0。|  
|HY010|函數順序錯誤|(DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLBindParameter**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> (DM) 的呼叫以非同步方式執行的函式*StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY021|不一致的描述元資訊|一致性檢查期間檢查的描述元資訊不一致。 (請參閱 「 一致性檢查 > 一節**SQLSetDescField**。)<br /><br /> 指定的引數的值*DecimalDigits*所指定的 SQL 資料類型的資料行的資料來源所支援的值的範圍之外*ParameterType*引數。|  
|HY090|字串或緩衝區長度無效|(DM) 中的值*Columnsize*為小於 0。 (請參閱中的 SQL_DESC_DATA_PTR 欄位的說明**SQLSetDescField**。)|  
|HY104|無效的有效位數或小數位數的值|指定的引數的值*ColumnSize*或*DecimalDigits*是所指定的 SQL 資料類型的資料行的資料來源所支援的值的範圍之外*ParameterType*引數。|  
|HY105|無效的參數類型|(DM) 引數指定的值*了*無效。 （請參閱 「 註解。"）|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援指定的引數所指定的值組合來轉換*ValueType*和 引數所指定的驅動程式專屬值*ParameterType*.<br /><br /> 指定的引數的值*ParameterType*的驅動程式支援 ODBC 的版本，但不是支援的驅動程式或資料來源是有效的 ODBC SQL 資料類型識別項。<br /><br /> 此驅動程式支援只有 ODBC 2。*x*和引數*ValueType*是下列其中之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 所有間隔 C 資料類型會列在[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d:資料類型。<br /><br /> 此驅動程式只支援之前 3.50 元，並將引數的 ODBC 版本*ValueType*已 SQL_C_GUID。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解

 應用程式呼叫**SQLBindParameter**繫結 SQL 陳述式中的每個參數標記。 繫結的有效日期持續直到應用程式會呼叫**SQLBindParameter**同樣地，呼叫**SQLFreeStmt** SQL_RESET_PARAMS 選項，或呼叫**SQLSetDescField**至APD SQL_DESC_COUNT 標頭欄位設為 0。  
  
 如需有關參數的詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。 如需有關參數的資料型別和參數標記的詳細資訊，請參閱 <<c0> [ 參數的資料型別](../../../odbc/reference/appendixes/parameter-data-types.md)並[參數標記](../../../odbc/reference/appendixes/parameter-markers.md)附錄 c:SQL 文法。  
  
## <a name="parameternumber-argument"></a>Sqlbindparameter 引數  
 如果*Sqlbindparameter*呼叫中**SQLBindParameter** SQL_DESC_COUNT，值大於**SQLSetDescField**呼叫以增加 SQL_DESC_ 值若要計算*Sqlbindparameter*。  
  
## <a name="inputoutputtype-argument"></a>了引數  
 *了*引數會指定參數的型別。 這個引數會設定 IPD SQL_DESC_PARAMETER_TYPE 欄位。 不會呼叫程序，例如 SQL 陳述式中的所有參數**插入**陳述式，都是*輸入 參數*。 程序呼叫中的參數可以輸入、 輸入/輸出或輸出參數。 (應用程式呼叫**SQLProcedureColumns**判斷程序呼叫; 中的參數類型無法判斷其類型的參數會假設為輸入的參數。)  
  
 *了*引數可以是下列值之一：  
  
-   SQL_PARAM_INPUT. 參數標記，例如不會呼叫程序中，SQL 陳述式中的參數**插入**陳述式，或將標記中的程序的輸入的參數。 例如，在參數**INSERT INTO 員工 VALUES (？，？，？)** 是輸入的參數，而在參數 **{呼叫 AddEmp (？，？，？)}** 可以但不一定，輸入的參數。  
  
     當執行陳述式時，驅動程式會將參數的資料傳送至資料來源\* *ParameterValuePtr*緩衝區必須包含有效的輸入的值，或 **StrLen_or_IndPtr*緩衝區必須包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT 的結果_EXEC 巨集。  
  
     如果應用程式無法判斷程序呼叫中參數的型別，它會設定*了*至 SQL_PARAM_INPUT; 如果資料來源傳回參數值，驅動程式會捨棄它。  
  
-   SQL_PARAM_INPUT_OUTPUT. 參數標記的程序中的輸入/輸出參數。 例如，在參數 **{呼叫 GetEmpDept(?)}** 是接受員工的名稱，並傳回該員工的部門名稱的輸入/輸出參數。  
  
     當執行陳述式時，驅動程式會將參數的資料傳送至資料來源\* *ParameterValuePtr*緩衝區必須包含有效的輸入的值，或有\* *StrLen_or_IndPtr*緩衝區必須包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或結果SQL_LEN_DATA_AT_EXEC 巨集。 執行陳述式之後，驅動程式會傳回至應用程式，參數的資料如果資料來源不會傳回輸入/輸出參數的值，驅動程式會將 **StrLen_or_IndPtr*緩衝區為 SQL_NULL_DATA。  
  
    > [!NOTE]  
    >  當 ODBC 1.0 應用程式呼叫**SQLSetParam** ODBC 2.0 驅動程式中，驅動程式管理員會將此呼叫**SQLBindParameter**所在*了*引數會設定為 SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT。 參數標記的程序或在程序; 輸出參數傳回的值在任一情況下，這些值稱為*輸出參數*。 比方說中的參數 **{？ = 呼叫 GetNextEmpID}** 是輸出參數傳回下一步 的員工識別碼。  
  
     執行陳述式之後，驅動程式會傳回參數的資料應用程式，除非*ParameterValuePtr*並*StrLen_or_IndPtr*引數都是 null 指標，在此情況下驅動程式會捨棄輸出值。 如果資料來源不會傳回輸出參數的值，驅動程式會將 **StrLen_or_IndPtr*緩衝區為 SQL_NULL_DATA。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. 指出應該串流處理輸入/輸出參數。 **SQLGetData**可以讀取組件中的參數值。 *BufferLength*因為緩衝區長度將決定在呼叫的所以會忽略**SQLGetData**。 值*StrLen_or_IndPtr*緩衝區必須包含 SQL_NULL_DATA、 SQL_DEFAULT_PARAM，SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。 參數必須繫結來做為輸入的資料在執行 (DAE) 參數，如果將輸出資料流。 *ParameterValuePtr*可以是任何非 null 指標值，就會傳回**SQLParamData**使用者定義權杖的值，傳遞了*ParameterValuePtr*這兩個輸入和輸出。 如需詳細資訊，請參閱 <<c0> [ 使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM. SQL_PARAM_INPUT_OUTPUT_STREAM，輸出參數相同。 **StrLen_or_IndPtr*輸入會被忽略。  
  
 下表列出不同的組合*了*和 **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|結果|在 ParameterValuePtr 注意到百分比|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入中的組件|*ParameterValuePtr*可以是任何會傳回的指標值**SQLParamData**使用者定義權杖的值，傳遞了*ParameterValuePtr*。|  
|SQL_PARAM_INPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入繫結的緩衝區|*ParameterValuePtr*是輸入緩衝區的位址。|  
|SQL_PARAM_OUTPUT|忽略的輸入。|輸出繫結的緩衝區|*ParameterValuePtr*是輸出緩衝區的位址。|  
|SQL_PARAM_OUTPUT_STREAM|忽略的輸入。|資料流的輸出|*ParameterValuePtr*可以是任何指標值，就會傳回**SQLParamData**使用者定義權杖的值，傳遞了*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入中的組件和輸出繫結的緩衝區|*ParameterValuePtr*是也會傳回輸出緩衝區的位址**SQLParamData**使用者定義權杖的值，傳遞了*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入繫結的緩衝區和輸出繫結的緩衝區|*ParameterValuePtr*是共用的輸入/輸出緩衝區的位址。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入中的組件和資料流的輸出|*ParameterValuePtr*可以是任何非 null 指標值，就會傳回**SQLParamData**使用者定義權杖的值，傳遞了*ParameterValuePtr*這兩個輸入和輸出。|  
  
> [!NOTE]  
>  驅動程式必須決定當串流應用程式繫結其輸出或輸入 / 輸出參數時，允許哪些 SQL 類型。 驅動程式管理員不會產生無效的 SQL 類型的錯誤。  
  
## <a name="valuetype-argument"></a>ValueType 引數

 *ValueType*引數會指定參數的 C 資料類型。 這個引數設定 APD 中的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位。 這必須是在值的其中一個[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)一節的附錄 d:資料類型。  
  
 如果*ValueType*引數是其中一個間隔資料類型的 SQL_DESC_TYPE 欄位*Sqlbindparameter* APD 中的記錄設定為 SQL_INTERVAL，APD 中的 [SQL_DESC_CONCISE_TYPE] 欄位設定為簡潔的間隔資料類型和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位*Sqlbindparameter*記錄設定為特定間隔資料類型的次要代碼。 (請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)預設間隔分別在 APD，SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 欄位中所設定開頭有效位數 (2) 和預設的間隔秒數有效位數 (6)，用於資料。 應用程式如果任一個預設有效位數不適用，應該明確設定描述項欄位呼叫**SQLSetDescField**或是**SQLSetDescRec**。  
  
 如果*ValueType*引數是其中一個日期時間資料類型的 SQL_DESC_TYPE 欄位*Sqlbindparameter* APD 中的記錄設定為 如果是 SQL_DATETIME SQL_DESC_CONCISE_TYPE欄位*Sqlbindparameter* APD 中的記錄設定為 C 的精確日期時間資料型別，而且 SQL_DESC_DATETIME_INTERVAL_CODE 欄位*Sqlbindparameter*記錄設定為特定的日期時間子代碼資料型別。 (請參閱[附錄 d:資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)  
  
 如果*ValueType*引數是 SQL_C_NUMERIC 資料類型，則預設有效位數 （它是由驅動程式定義），並用預設小數位數 (0)，在 APD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定的資料。 應用程式的預設有效位數或小數位數不適用，如果應該明確設定描述項欄位呼叫**SQLSetDescField**或是**SQLSetDescRec**。  
  
 SQL_C_DEFAULT 指定針對具有指定的 SQL 資料類型，會從預設 C 資料類型傳送參數值*ParameterType*。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱 < [ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 如需詳細資訊，請參閱 <<c0> [ 預設 C 資料類型](../../../odbc/reference/appendixes/default-c-data-types.md)，[轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)，並[轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附錄 d:資料類型。  
  
## <a name="parametertype-argument"></a>ParameterType 引數

 這必須是其中一個值中所列[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)一節的附錄 d:資料類型或它必須是驅動程式專屬值。 這個引數設定的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE IPD 欄位。  
  
 如果*ParameterType*引數是其中一個 datetime 識別項、 IPD 的 SQL_DESC_TYPE 欄位設定為 如果是 SQL_DATETIME IPD SQL_DESC_CONCISE_TYPE 欄位設定為簡明的日期時間 SQL 資料類型，以及 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為適當的日期時間子代碼值。  
  
 如果*ParameterType*是其中一個間隔的識別項，IPD 的 SQL_DESC_TYPE 欄位設定為 SQL_INTERVAL，IPD SQL_DESC_CONCISE_TYPE 欄位會設定為精簡 SQL 間隔資料類型，以及 SQL_DESC_DATETIME_INTERVAL_CODE IPD 欄位設定為適當的間隔子代碼。 IPD 中的 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 欄位設為間隔開頭有效位數，並 SQL_DESC_PRECISION 欄位設為間隔的秒數有效位數，如果適用的話。 如果不適用 SQL_DESC_DATETIME_INTERVAL_PRECISION 或 SQL_DESC_PRECISION 的預設值，應用程式應該明確設定它藉由呼叫**SQLSetDescField**。 如需這些欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*引數是 SQL_NUMERIC 資料類型，則預設有效位數 （它是由驅動程式定義） 以及預設小數位數 (0)，在 IPD，SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定使用的資料。 應用程式的預設有效位數或小數位數不適用，如果應該明確設定描述項欄位呼叫**SQLSetDescField**或是**SQLSetDescRec**。  
  
 如需如何轉換資料，請參閱[轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)並[轉換將資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附錄 d:資料類型。  
  
## <a name="columnsize-argument"></a>ColumnSize 引數

 *ColumnSize*引數會指定對應至參數標記，該資料，或兩者的長度的運算式之資料行的大小。 這個引數設定的 IPD，根據 SQL 資料類型的不同欄位 ( *ParameterType*引數)。 下列規則適用於此對應：  
  
-   如果*ParameterType* SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY、 或其中一個精簡 SQL 日期時間或間隔資料類型，IPD 的 SQL_DESC_LENGTH 欄位設定為的值*ColumnSize*。 (如需詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)節附錄 d:資料型別。）  
  
-   如果*ParameterType* SQL_DECIMAL、 SQL_NUMERIC、 SQL_FLOAT、 SQL_REAL，或 SQL_DOUBLE，IPD 的 SQL_DESC_PRECISION 欄位設定為值*ColumnSize*。  
  
-   其他資料類型，如*ColumnSize*引數會被忽略。  
  
 如需詳細資訊，請參閱 「 傳遞參數值 」 和 SQL_DATA_AT_EXEC，在 「*StrLen_or_IndPtr*引數。 」  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 引數

 如果*ParameterType* SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP、 SQL_INTERVAL_SECOND、 SQL_INTERVAL_DAY_TO_SECOND、 SQL_INTERVAL_HOUR_TO_SECOND，或 SQL_INTERVAL_MINUTE_TO_SECOND，IPD SQL_DESC_PRECISION 欄位會設定若要*DecimalDigits*。 如果*ParameterType* SQL_NUMERIC 或 SQL_DECIMAL，IPD SQL_DESC_SCALE 欄位設定為*DecimalDigits*。 對於所有其他資料類型， *DecimalDigits*引數會被忽略。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 引數

 *ParameterValuePtr*引數指向的緩衝區，當**SQLExecute**或是**SQLExecDirect**呼叫時，包含參數的實際資料。 資料必須在指定的格式*ValueType*引數。 這個引數設定 SQL_DESC_DATA_PTR 欄位 APD。 應用程式可以設定*ParameterValuePtr*引數為 null 指標，只要 *\*StrLen_or_IndPtr* SQL_NULL_DATA 或 SQL_DATA_AT_EXEC。 （這適用於僅為輸入或輸入/輸出參數。）  
  
 如果\* *StrLen_or_IndPtr*結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集或 SQL_DATA_AT_EXEC，然後*ParameterValuePtr*是與參數相關聯的應用程式定義指標值。 它會傳回到應用程式，透過**SQLParamData**。 例如， *ParameterValuePtr*可能的非零語彙基元，例如參數數目、 資料指標或應用程式用來將輸入的參數繫結結構的指標。 不過，請注意，如果參數是輸入/輸出參數， *ParameterValuePtr*必須是輸出值儲存在緩衝區的指標。 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1，如果應用程式可以使用 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性，並搭配所指向的值*ParameterValuePtr*引數。 例如， *ParameterValuePtr*可能指向值的陣列，而應用程式可能會使用 SQL_ATTR_PARAMS_PROCESSED_PTR 所指向的值，從陣列擷取正確的值。 如需詳細資訊，請參閱本節稍後的 「 傳遞參數值 」。  
  
 如果*了*引數是 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT， *ParameterValuePtr*指向驅動程式會傳回輸出值的緩衝區。 此程序傳回一個或多個結果集，如果\* *ParameterValuePtr*緩衝區不一定是以設定直到已經處理所有結果集/資料列計數。 如果未設定緩衝區，直到處理完成時，輸出參數和傳回值會無法使用，直到**SQLMoreResults**傳回 sql_no_data 為止。 呼叫**SQLCloseCursor**或是**SQLFreeStmt** SQL_CLOSE 選項會導致捨棄這些值。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1， *ParameterValuePtr*指向的陣列。 單一的 SQL 陳述式會處理完整的輸入或輸入/輸出參數的輸入值的陣列，並傳回做為輸入/輸出的輸出值或輸出參數的陣列。  
  
## <a name="bufferlength-argument"></a>BufferLength 引數

 字元和二進位的 C 資料，如*Columnsize*引數指定的長度\* *ParameterValuePtr*緩衝區 （如果它是單一項目） 或中項目的長度\**ParameterValuePtr*陣列 （如果 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1 時）。 這個引數設定 APD SQL_DESC_OCTET_LENGTH 記錄欄位。 如果應用程式指定多個值， *Columnsize*用來判斷中值的位置 **ParameterValuePtr*陣列、 輸入和輸出上。 輸入/輸出和輸出參數，它用來決定是否要截斷字元和二進位輸出上的 C 資料：  
  
-   C 字元資料的位元組可傳回數目是否大於或等於*Columnsize*中的資料\* *ParameterValuePtr*會被截斷成*BufferLength* null 結束字元的長度小於及是以 null 終止的驅動程式。  
  
-   二進位的 C 資料，如果要傳回可用的位元組數目大於*Columnsize*中的資料\* *ParameterValuePtr*會被截斷成*Columnsize*位元組。  
  
 對於所有其他類型的 C 資料*Columnsize*引數會被忽略。 長度\* *ParameterValuePtr*緩衝區 （如果它是單一項目） 或中的項目長度\* *ParameterValuePtr*陣列 （如果應用程式會呼叫**SQLSetStmtAttr**具有*屬性*則 sql_attr_paramset_size 會指定每個參數的多個值的引數) 會假設為 C 資料類型的長度。  
  
 資料流的輸出或資料流處理的輸入/輸出參數，如*Columnsize*中指定的緩衝區長度，因此，系統會忽略引數**SQLGetData**。  
  
> [!NOTE]  
>  當 ODBC 1.0 應用程式呼叫**SQLSetParam**在 ODBC 3。*x*驅動程式、 驅動程式管理員會將此呼叫**SQLBindParameter**所在*Columnsize*引數一定是 SQL_SETPARAM_VALUE_MAX。 因為如果 ODBC 3，則驅動程式管理員會傳回錯誤。*x*應用程式集*Columnsize* SQL_SETPARAM_VALUE_MAX，ODBC 3 以。*x*驅動程式可以使用這個來判斷當它由 ODBC 1.0 應用程式呼叫。  
  
> [!NOTE]  
>  在  **SQLSetParam**，其中應用程式指定的長度與方法 **ParameterValuePtr*緩衝，讓驅動程式可傳回字元或二進位資料，以及將應用程式傳送的方式陣列的字元或二進位的參數值，驅動程式，由驅動程式定義。  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr 引數

 *StrLen_or_IndPtr*引數指向的緩衝區，，當**SQLExecute**或是**SQLExecDirect**呼叫時，包含下列其中之一。 （這個引數設定的應用程式參數指標的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 記錄欄位）。  
  
-   中儲存的參數值的長度 **ParameterValuePtr*。 這會被忽略，但字元或二進位的 C 資料除外。  
  
-   SQL_NTS. 參數值是以 null 結束的字串。  
  
-   SQL_NULL_DATA. 參數值是 NULL。  
  
-   SQL_DEFAULT_PARAM. 程序是參數的使用預設值，而不是參數的從應用程式擷取值。 這個值是在 ODBC 標準語法，在呼叫的程序中才有效，然後才*了*引數是 SQL_PARAM_INPUT、 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 當\* *StrLen_or_IndPtr*是 SQL_DEFAULT_PARAM， *ValueType*， *ParameterType*， *ColumnSize*， *DecimalDigits*， *Columnsize*，以及*ParameterValuePtr*引數會被忽略的輸入參數，並只會用來定義輸入的輸出參數值 /輸出參數。  
  
-   結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集。 參數的資料將會傳送具有**SQLPutData**。 如果*ParameterType*引數是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或長時間，資料來源特有的資料類型，而且驅動程式會傳回"Y"表示 SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo**，*長度*是要傳送的參數; 的資料的位元組數目，否則為*長度*必須為非負數的值並忽略。 如需詳細資訊，請參閱 < 傳遞參數值 > 本節稍後的。  
  
     例如，若要指定 10000 個位元組的資料將會傳送具有**SQLPutData**應用程式設定在一或多個呼叫中，針對 SQL_LONGVARCHAR 參數，**StrLen_or_IndPtr*為 SQL_LEN_DATA_AT_EXEC （10000)。  
  
-   SQL_DATA_AT_EXEC. 參數的資料將會傳送具有**SQLPutData**。 在呼叫 ODBC 3 時，ODBC 1.0 應用程式會使用此值。*x*驅動程式。 如需詳細資訊，請參閱 < 傳遞參數值 > 本節稍後的。  
  
 如果*StrLen_or_IndPtr*為 null 指標，驅動程式假設所有輸入的參數值都不是 NULL，且該字元和二進位資料是以 null 終止。 如果*了*SQL_PARAM_OUTPUT 或 SQL_PARAM_OUTPUT_STREAM 並*ParameterValuePtr*並*StrLen_or_IndPtr*都是 null 指標，驅動程式會捨棄輸出值。  
  
> [!NOTE]  
>  應用程式開發人員會從指定的 null 指標強烈建議您不要*StrLen_or_IndPtr*參數的資料型別時 SQL_C_BINARY。 若要確定該驅動程式非預期不會截斷 SQL_C_BINARY 資料*StrLen_or_IndPtr*應該包含有效的長度值的指標。  
  
 如果*了*引數是 SQL_PARAM_INPUT_OUTPUT、 SQL_PARAM_OUTPUT、 SQL_PARAM_INPUT_OUTPUT_STREAM，還是 SQL_PARAM_OUTPUT_STREAM， *StrLen_or_IndPtr*指向在其中的緩衝區驅動程式會傳回 SQL_NULL_DATA，可用來傳回中的位元組數目\* *ParameterValuePtr* （不含字元資料的 null 終止位元組），或 SQL_NO_TOTAL (如果可用的位元組數目傳回無法判斷）。 如果此程序傳回一個或多個結果集，**StrLen_or_IndPtr*緩衝區不一定是直到所有結果已經都提取的設定。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1， *StrLen_or_IndPtr*指向 SQLLEN 值的陣列。 這些可以是任何在本節中稍早所列的值，然後以單一的 SQL 陳述式處理。  
  
## <a name="passing-parameter-values"></a>傳遞參數值

 應用程式可以傳遞參數的值可能是在\* *ParameterValuePtr*緩衝區或含有一或多個呼叫**SQLPutData**。 資料會使用傳遞的參數**SQLPutData**又稱為*資料在執行*參數。 這些通常用來傳送資料 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 參數，而且可以混合使用與其他參數。  
  
 若要傳遞參數值，應用程式會執行下列步驟順序：  
  
1.  呼叫**SQLBindParameter**每個參數繫結參數的值的緩衝區 (*ParameterValuePtr*引數) 和長度/指標 (*StrLen_or_IndPtr*引數）。 資料在執行中參數，如*ParameterValuePtr*是應用程式定義指標值，例如參數的數目或資料的指標。 此值稍後將會傳回，而且可用來識別參數。  
  
2.  將輸入和輸入/輸出參數中的值放\* *ParameterValuePtr*和 **StrLen_or_IndPtr*緩衝區：  
  
    -   對於一般參數，應用程式會放在參數值\* *ParameterValuePtr*緩衝區，並在該值的長度 **StrLen_or_IndPtr*緩衝區。 如需詳細資訊，請參閱 <<c0> [ 設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   資料在執行中參數，作為應用程式將放 SQL_LEN_DATA_AT_EXEC 的結果 (*長度*) 中的巨集 （當呼叫 ODBC 2.0 驅動程式） **StrLen_or_IndPtr*緩衝區。  
  
3.  呼叫**SQLExecute**或是**SQLExecDirect**執行 SQL 陳述式。  
  
    -   如果不有任何資料在執行中參數，此程序已完成。  
  
    -   如果有任何資料在執行中參數，則函數會傳回 SQL_NEED_DATA。  
  
4.  呼叫**SQLParamData**來擷取應用程式定義的值中指定*ParameterValuePtr*引數**SQLBindParameter**前若要處理的資料在執行參數。 **SQLParamData**會傳回 SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  雖然資料在執行中參數類似於資料在執行中資料行，所傳回的值**SQLParamData**每個不同。 資料在執行中參數已將與傳送資料的 SQL 陳述式中的參數**SQLPutData**當陳述式以**SQLExecDirect**或**SQLExecute**. 使用繫結**SQLBindParameter**。 所傳回的值**SQLParamData**指標值傳遞給**SQLBindParameter**中*ParameterValuePtr*引數。 資料在執行中資料行是資料會傳送使用資料列集中的資料行**SQLPutData**更新或加入一個資料列時**SQLBulkOperations**或更新的**SQLSetPos**. 使用繫結**SQLBindCol**。 所傳回的值**SQLParamData**是中的資料列的地址 **TargetValuePtr*緩衝區 (藉由呼叫設定 **SQLBindCol**) 所處理的。  
  
5.  呼叫**SQLPutData**傳送參數資料的一或多次。 如果資料值是大於，多個呼叫則需要\* *ParameterValuePtr*中指定的緩衝區**SQLPutData**; 多次呼叫**SQLPutData**或傳送二進位的 C 資料行的字元、 二進位，傳送字元 C 資料行的字元、 二進位檔或資料來源特有的資料型別時，只允許相同的參數或資料來源特定的資料類型。  
  
6.  呼叫**SQLParamData**再次來表示，所有資料都傳送的參數。  
  
    -   如果有更多的資料在執行參數**SQLParamData**會傳回 SQL_NEED_DATA 和應用程式定義參數的值為下一步 執行資料處理。 應用程式會重複步驟 4 和 5。  
  
    -   如果沒有其他資料在執行中參數，此程序已完成。 如果陳述式執行成功， **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果執行失敗，則會傳回 SQL_ERROR。 在此時**SQLParamData**可能會傳回任何可以用來執行陳述式之函式所傳回的 SQLSTATE (**SQLExecDirect**或是**SQLExecute**)。  
  
         輸出值的任何輸入/輸出或輸出參數位於\* *ParameterValuePtr*和 **StrLen_or_IndPtr*緩衝處理後的應用程式會擷取所有結果集陳述式所產生。  
  
 呼叫**SQLExecute**或是**SQLExecDirect**置於 SQL_NEED_DATA 狀態中的陳述式。 此時，應用程式可以只呼叫**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**陳述式或*連接控制代碼*陳述式相關聯。 如果它會呼叫其他函式與陳述式或陳述式相關聯的連接，則函數會傳回 SQLSTATE HY010 （函數順序錯誤）。 SQL_NEED_DATA 時狀態的陳述式分葉**SQLParamData**或是**SQLPutData**會傳回錯誤， **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或會取消陳述式。  
  
 如果應用程式會呼叫**SQLCancel**驅動程式時驅動程式仍會需要的資料在執行中參數的資料，會取消陳述式執行，就可以呼叫應用程式**SQLExecute**或**SQLExecDirect**一次。  
  
## <a name="retrieving-streamed-output-parameters"></a>擷取資料流的輸出參數

 當應用程式設定*了*SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM，輸出參數值必須擷取一或多個呼叫**SQLGetData**。 資料流的輸出參數值傳回至應用程式的驅動程式時，它會傳回 SQL_PARAM_DATA_AVAILABLE 下列函式呼叫的回應：**SQLMoreResults**， **SQLExecute**，以及**SQLExecDirect**。 應用程式呼叫**SQLParamData**以判斷可用的參數值。  
  
 如需有關 SQL_PARAM_DATA_AVAILABLE 和資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用參數陣列

 當應用程式會準備具有參數標記，並傳入的參數陣列的陳述式時，有兩種不同的方式，這可以執行。 方法之一是仰賴後端，大小寫的參數陣列的整個陳述式會被視為一個不可部分完成單位的陣列處理功能驅動程式。 Oracle 是資料來源支援陣列處理功能的範例。 若要實作這項功能的另一個方法是驅動程式產生的 SQL 陳述式，針對每個參數陣列中的參數集的一個 SQL 陳述式批次，並執行批次。 參數陣列不能搭配**UPDATE WHERE CURRENT OF**陳述式。  
  
 當處理參數陣列時，個別的結果集/資料列計數 （一個用於每個參數集） 都能使用，或結果集/資料列計數可以彙總成一個。 選項 SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo**指出資料列計數為適用於每一組參數 (SQL_PARC_BATCH) 或只有一個資料列計數為可用 (SQL_PARC_NO_BATCH)。  
  
 選項 SQL_PARAM_ARRAY_SELECTS **SQLGetInfo**指出結果集是否可供每一組參數 (SQL_PAS_BATCH)，或只有一個結果集是可用 (SQL_PAS_NO_BATCH)。 如果驅動程式不允許使用參數陣列來執行的結果集產生陳述式，SQL_PARAM_ARRAY_SELECTS 傳回 SQL_PAS_NO_SELECT。  
  
 如需詳細資訊，請參閱 < [SQLGetInfo 函式](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 若要支援的參數陣列，則 sql_attr_paramset_size 會陳述式屬性設定為指定的每個參數的值數目。 如果欄位是大於 1，APD 中的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位必須指向陣列中。 每個陣列的基數等於 SQL_ATTR_PARAMSET_SIZE 的值。  
  
 APD 中的 [SQL_DESC_ROWS_PROCESSED_PTR] 欄位會指向包含集合的已處理，包括錯誤集的參數數目的緩衝區。 處理每個參數集時，驅動程式會儲存在緩衝區中的新值。 如果這是 null 指標，則會不傳回任何數字。 當使用參數陣列時，即使設定函式會傳回 SQL_ERROR，會填入 APD SQL_DESC_ROWS_PROCESSED_PTR 欄位所指向的值。 如果傳回 SQL_NEED_DATA，APD SQL_DESC_ROWS_PROCESSED_PTR 欄位所指向的值設為 正在處理的參數集。  
  
 當繫結參數陣列，且可能發生的狀況**UPDATE WHERE CURRENT OF**陳述式是由驅動程式定義。  
  
## <a name="column-wise-parameter-binding"></a>資料行取向的參數繫結

 在 資料行取向的繫結，應用程式繫結不同的參數和長度/指標陣列至每個參數。  
  
 若要使用資料行取向的繫結，應用程式首先會將 SQL_PARAM_BIND_BY_COLUMN 設定 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性。 （這是預設值）。每個資料行繫結，應用程式會執行下列步驟：  
  
1.  配置參數緩衝區陣列。  
  
2.  配置陣列的長度/指標緩衝區。  
  
    > [!NOTE]  
    >  如果應用程式時直接寫入描述項會使用資料行取向的繫結，可以使用個別的陣列，長度與指標資料。  
  
3.  呼叫**SQLBindParameter**的下列引數：  
  
    -   *ValueType*是單一項目參數緩衝區陣列中的 C 類型。  
  
    -   *ParameterType*是參數的 SQL 型別。  
  
    -   *ParameterValuePtr*是參數緩衝區陣列的位址。  
  
    -   *BufferLength*參數緩衝區陣列中的單一元素的大小。 *Columnsize*有固定長度資料的資料時，會忽略引數。  
  
    -   *StrLen_or_IndPtr*是長度/指標陣列的位址。  
  
 如需如何使用這項資訊的詳細資訊，請參閱 「 註解中，「 本章節稍後的 「 ParameterValuePtr 引數 」。 參數的資料行取向的繫結的相關資訊，請參閱[繫結陣列的參數](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>資料列取向的參數繫結

 在資料列取向的繫結，應用程式會定義結構，其中包含每個參數繫結的參數和長度/指標緩衝區。  
  
 若要使用資料列取向的繫結，應用程式會執行下列步驟：  
  
1.  定義結構，來保存一組參數 （包括參數和長度/指標緩衝區），並配置這些結構的陣列。  
  
    > [!NOTE]  
    >  如果應用程式時直接寫入描述項會使用資料列取向的繫結，個別的欄位可以用於長度和指標的資料。  
  
2.  結構，其中包含單一參數集的大小或大小的緩衝區，其中的參數會繫結的執行個體，請設定 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性。 長度必須包含所有繫結的參數，以及結構或緩衝區，藉此確定，當繫結參數的位址會隨著指定的長度，結果會指向中同名參數開頭的任何填補的空間下一個資料列。 當您使用*sizeof* ANSI C 中的運算子，保證此行為。  
  
3.  呼叫**SQLBindParameter**每個參數繫結的下列引數：  
  
    -   *ValueType*是繫結至資料行的參數緩衝區成員的型別。  
  
    -   *ParameterType*是參數的 SQL 型別。  
  
    -   *ParameterValuePtr*是參數緩衝區中成員的第一個陣列元素的位址。  
  
    -   *BufferLength*是參數緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是繫結之長度/指標成員的位址。  
  
 如需如何使用這項資訊的詳細資訊，請參閱 「*ParameterValuePtr*引數，「 本主題稍後的。 參數的資料列取向的繫結的相關資訊，請參閱[繫結陣列的參數](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>錯誤資訊

 如果驅動程式未實作參數陣列以批次 （SQL_PARAM_ARRAY_ROW_COUNTS 選項 SQL_PARC_NO_BATCH 等於）、 錯誤情況的處理方式，如同執行一個陳述式。 如果驅動程式未實作參數陣列，以批次，應用程式可以使用 IPD SQL_DESC_ARRAY_STATUS_PTR 標頭欄位以判斷哪一個參數的 SQL 陳述式或參數陣列中的參數造成**SQLExecDirect**或是**SQLExecute**傳回錯誤。 此欄位會包含每個資料列的參數值的狀態資訊。 如果該欄位會指出發生錯誤，診斷資料結構中的欄位會指出失敗的參數資料列和參數數目。 陣列中的項目數會定義由 APD，則 sql_attr_paramset_size 會陳述式屬性可以設定的 SQL_DESC_ARRAY_SIZE 標頭欄位。  
  
> [!NOTE]  
>  APD 中的 [SQL_DESC_ARRAY_STATUS_PTR 首] 欄位用來略過參數。 如需忽略參數的詳細資訊，請參閱下一步 區段中，「 略過一組參數。 」  
  
 當**SQLExecute**或是**SQLExecDirect**傳回 SQL_ERROR，SQL_DESC_ARRAY_STATUS_PTR 欄位 IPD 中所指陣列中的項目會包含 SQL_PARAM_ERROR，SQL_PARAM_SUCCESS，SQL_PARAM_SUCCESS_WITH_INFO、 SQL_PARAM_UNUSED 或 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 對於此陣列中每個項目，診斷資料結構會包含一或多個狀態記錄。 結構的 SQL_DIAG_ROW_NUMBER 欄位會指出造成錯誤的參數值的資料列編號。 如果可以判斷造成錯誤的參數資料列中的特定參數，會 SQL_DIAG_COLUMN_NUMBER 欄位中輸入參數數目。  
  
 參數未用過因為較早的參數，強制發生錯誤時輸入 SQL_PARAM_UNUSED **SQLExecute**或是**SQLExecDirect**中止。 比方說，如果有 50 的參數，而且執行時發生錯誤的參數造成 fortieth 集**SQLExecute**或是**SQLExecDirect**中止，則 SQL_PARAM_UNUSED 進入針對至 50 41 參數狀態陣列。  
  
 驅動程式會將參數陣列當做一個整合型的單位，因此它不會產生此個別參數的資訊層級錯誤時，會輸入 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 在處理單一參數集的一些錯誤導致處理後續的參數集合的陣列中要停止。 其他錯誤不會影響後續的參數處理。 哪些錯誤會停止處理是由驅動程式定義。 如果未停止處理、 處理陣列中的所有參數、 結果錯誤，會傳回 SQL_SUCCESS_WITH_INFO 和 SQL_ATTR_PARAMS_PROCESSED_PTR 所定義的緩衝區設定為已都處理的參數集的總數 (所定義SQL_ATTR_PARAMSET_SIZE 陳述式屬性），其中包括錯誤集。  
  
> [!CAUTION]  
>  ODBC 中的參數陣列處理發生錯誤時的行為是在 ODBC 3 不同。*x*比 ODBC 2。*x*。 在 ODBC 2。*x*，函式會傳回 SQL_ERROR 並處理不。 所指向緩衝區*pirow*引數**SQLParamOptions**包含錯誤資料列數目。 在 ODBC 3。*x*函式會傳回 SQL_SUCCESS_WITH_INFO，可能處理可能停止或繼續。 如果持續發生，SQL_ATTR_PARAMS_PROCESSED_PTR 所指定的緩衝區將所有的參數處理，包括卻造成錯誤的值。 此行為變更可能會導致現有的應用程式的問題。  
  
 當**SQLExecute**或是**SQLExecDirect**傳回之前完成的參數陣列中的所有參數集的處理程序，例如當傳回 SQL_ERROR 或 SQL_NEED_DATA 時，狀態陣列會包含已經處理這些參數的狀態。 IPD 中的 [SQL_DESC_ROWS_PROCESSED_PTR] 欄位所指向的位置就包含造成 SQL_ERROR 或 SQL_NEED_DATA 錯誤程式碼的參數陣列中的資料列編號。 參數的陣列傳送至 SELECT 陳述式時，狀態陣列值時，驅動程式定義，在執行陳述式，或做為結果集提取之後，它們可能可以使用。  
  
## <a name="ignoring-a-set-of-parameters"></a>略過一組參數

 （如同透過 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性） APD SQL_DESC_ARRAY_STATUS_PTR 欄位可用來指出應該忽略的一組 SQL 陳述式中的繫結參數。 若要引導驅動程式在執行期間略過一個或多組參數，應用程式應該遵循下列步驟：  
  
1.  呼叫**SQLSetDescField**設定指向包含狀態資訊的 SQLUSMALLINT 值的陣列 APD SQL_DESC_ARRAY_STATUS_PTR 標頭欄位。 這個欄位也可以藉由呼叫設定**SQLSetStmtAttr**具有*屬性*的 SQL_ATTR_PARAM_OPERATION_PTR，可讓應用程式設定的欄位，而不取得描述項控制代碼。  
  
2.  設定陣列的兩個值的其中一個 APD SQL_DESC_ARRAY_STATUS_PTR 欄位所定義的每個項目：  
  
    -   SQL_PARAM_IGNORE，表示資料列排除陳述式執行。  
  
    -   SQL_PARAM_PROCEED，以指出該資料列會包含在陳述式執行。  
  
3.  呼叫**SQLExecDirect**或是**SQLExecute**執行備妥的陳述式。  
  
 APD 中的 [SQL_DESC_ARRAY_STATUS_PTR] 欄位所定義的陣列，適用下列規則：  
  
-   指標會設定預設為 null。  
  
-   如果指標為 null，會使用所有的參數集，如同所有的項目已設為 SQL_ROW_PROCEED。  
  
-   將項目設定為 SQL_PARAM_PROCEED 不保證作業會使用該特定的一群參數。  
  
-   SQL_PARAM_PROCEED 定義為標頭檔中的 0。  
  
 應用程式可以設定 SQL_DESC_ARRAY_STATUS_PTR 欄位以指向相同的陣列，做為 APD 中指向 SQL_DESC_ARRAY_STATUS_PTR 欄位在 IRD 中。 資料列的資料繫結參數時，這非常有用。 然後會忽略參數，根據資料列資料的狀態。 除了 SQL_PARAM_IGNORE，下列程式碼會導致要忽略的 SQL 陳述式的參數：SQL_ROW_DELETED、 SQL_ROW_UPDATED 和 SQL_ROW_ERROR。 除了 SQL_PARAM_PROCEED，下列程式碼會造成 SQL 陳述式，繼續進行：SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 和 SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新繫結參數

 應用程式可以執行下列其中一個來變更繫結的兩個作業：  
  
-   呼叫**SQLBindParameter**來指定新的繫結已繫結的資料行。 驅動程式會以新的覆寫舊的繫結。  
  
-   指定要加入至繫結呼叫所指定的緩衝區位址的位移**SQLBindParameter**。 如需詳細資訊，請參閱下一步 區段中，「 正在重新繫結的位移。 」  
  
## <a name="rebinding-with-offsets"></a>重新繫結與位移

 當應用程式具有可包含許多參數，但呼叫緩衝區區域設定的參數重新繫結會特別有用**SQLExecDirect**或是**SQLExecute**使用只有幾個參數。 在緩衝區中剩餘的空間可以用於下一個參數集，藉由修改現有的繫結的位移。  
  
 APD 中的 SQL_DESC_BIND_OFFSET_PTR 標頭欄位會指向繫結位移。 如果欄位為非 null，驅動程式會取值指標，如果沒有任何 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位中的值是 null 指標，加入這些描述元中的欄位在執行階段的記錄。 執行 SQL 陳述式時，會使用新的指標值。 位移會在之後重新繫結項目保持有效。 由於 SQL_DESC_BIND_OFFSET_PTR 位移，而不是本身的位移的指標，應用程式可以位移直接變更，而不需要打電話[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或是[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)至變更描述項欄位。 指標會設定預設為 null。 ARD SQL_DESC_BIND_OFFSET_PTR 欄位可以設定由呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或是呼叫[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)具有*件*SQL_ATTR_PARAM_BIND_ 的OFFSET_PTR。  
  
 繫結位移是一律直接新增至 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位中的值。 如果位移變更為不同的值，新的值是仍然直接新增至每個描述項欄位中的值。 新的位移不會加入至欄位值和任何先前的位移的總和。  
  
## <a name="descriptors"></a>描述項

 參數繫結的方式取決於 Apd 和 Ipd 的欄位。 中的引數**SQLBindParameter**會用來設定這些描述項欄位。 也可以藉由設定欄位**SQLSetDescField**函式，雖然**SQLBindParameter**會更有效率使用，因為應用程式不需要取得描述項控制代碼來呼叫**SQLBindParameter**。  
  
> [!CAUTION]  
>  呼叫**SQLBindParameter**的一個陳述式可能會影響其他陳述式。 會發生這種情況是當陳述式相關聯 ARD 明確配置且同時與其他陳述式相關聯。 因為**SQLBindParameter**修改欄位的 APD 中，所做的修改套用至與這個描述元相關聯的所有陳述式。 如果這不是所需的行為，應用程式應該中斷此描述元，從其他陳述式之前它會呼叫**SQLBindParameter**。  
  
 就概念而言， **SQLBindParameter**序列中執行下列步驟：  
  
1.  呼叫[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)取得 APD 控制代碼。  
  
2.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)取得 APD SQL_DESC_COUNT 欄位，而如果值*ColumnNumber* SQL_DESC_COUNT，呼叫的值的引數超過**SQLSetDescField**提升至 SQL_DESC_COUNT 價值*ColumnNumber*。  
  
3.  呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次，以便將值指派給 APD 中的下列欄位：  
  
    -   設的值中的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE *ValueType*，但如果*ValueType*是其中一個的日期時間或間隔的子類型的精確識別碼，它會將 SQL_DESC_TYPE 設 SQL_日期時間或 SQL_INTERVAL，分別將 SQL_DESC_CONCISE_TYPE 簡潔的識別項，並將 SQL_DESC_DATETIME_INTERVAL_CODE 設的相對應的日期時間或間隔子代碼。  
  
    -   值會設定 SQL_DESC_OCTET_LENGTH 欄位*Columnsize*。  
  
    -   設定 SQL_DESC_DATA_PTR 欄位的值*ParameterValue*。  
  
    -   值會設定 SQL_DESC_OCTET_LENGTH_PTR 欄位*Strlen_or_ind&lt*。  
  
    -   值也設定 SQL_DESC_INDICATOR_PTR 欄位*Strlen_or_ind&lt*。  
  
     *Strlen_or_ind&lt*參數會指定指標的資訊和參數值的長度。  
  
4.  呼叫[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)取得 IPD 的控制代碼。  
  
5.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)取得 IPD SQL_DESC_COUNT 欄位，而如果值*ColumnNumber* SQL_DESC_COUNT，呼叫的值的引數超過**SQLSetDescField**提升至 SQL_DESC_COUNT 價值*ColumnNumber*。  
  
6.  呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次，以便將值指派給 IPD 下列欄位：  
  
    -   設的值中的 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE *ParameterType*，但如果*ParameterType*是其中一個的日期時間或間隔的子類型的精確識別碼，它會設定 SQL_DESC_TYPE如果是 SQL_DATETIME 或 SQL_INTERVAL，分別設定 SQL_DESC_CONCISE_TYPE 簡潔的識別項，並設定 SQL_DESC_DATETIME_INTERVAL_CODE 相對應的日期時間或間隔子代碼。  
  
    -   設定一或多個 SQL_DESC_LENGTH、 SQL_DESC_PRECISION 及 SQL_DESC_DATETIME_INTERVAL_PRECISION，視*ParameterType*。  
  
    -   值設定 SQL_DESC_SCALE *DecimalDigits*。  
  
 如果在呼叫**SQLBindParameter**會失敗，它會設定在 APD 中的描述項欄位的內容為未定義，而且 APD SQL_DESC_COUNT 欄位不會變更。 此外，IPD 中適當的記錄的 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_TYPE 欄位為未定義，而且 IPD SQL_DESC_COUNT 欄位不會變更。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam 來回呼叫的轉換

 當 ODBC 1.0 應用程式呼叫**SQLSetParam**在 ODBC 3。*x*驅動程式，而 ODBC 3。*x*驅動程式管理員對應呼叫下, 表所示。  
  
|呼叫 ODBC 1.0 應用程式|呼叫 ODBC 3。*x*驅動程式|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (StatementHandle、 Sqlbindparameter、 SQL_PARAM_INPUT_OUTPUT、 ValueType、 ParameterType， *ColumnSize*， *DecimalDigits*，ParameterValuePtr、 SQL_SETPARAM_VALUE_MAX，     StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會準備 SQL 陳述式將資料插入 ORDERS 資料表。 每個參數的陳述式中，應用程式會呼叫**SQLBindParameter**來指定 ODBC C 資料類型和 SQL 資料類型的參數，並將緩衝區繫結至每個參數。 每個資料列的資料，應用程式將資料值指派給每個參數並呼叫**SQLExecute**執行陳述式。  
  
 下列範例會假設您有 ODBC 資料來源，在電腦上稱為 Northwind 與 Northwind 資料庫相關聯。  
  
 如需更多的程式碼範例，請參閱 < [SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLProcedures 函式](../../../odbc/reference/syntax/sqlprocedures-function.md)， [SQLPutData 函數](../../../odbc/reference/syntax/sqlputdata-function.md)，和[SQLSetPos 函式](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>程式碼範例

 在下列範例中，應用程式會執行 SQL Server 預存程序中使用具名的參數。  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|陳述式中傳回參數的相關資訊|[SQLDescribeParam 函式](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放陳述式的參數緩衝區|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回陳述式的參數數目|[SQLNumParams 函式](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|傳回的資料傳送至下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多個參數值|[SQLParamOptions 函式](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|在執行階段傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱

 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
