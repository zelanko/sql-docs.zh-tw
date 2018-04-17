---
title: SQLBindParameter 函數 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54a22ecb571f6a6831023ee5c5d6c18149bff575
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函數
**一致性**  
 版本引進了： ODBC 2.0 標準相容性： ODBC  
  
 **摘要**  
 **SQLBindParameter**將緩衝區繫結至 SQL 陳述式中的參數標記。 **SQLBindParameter**支援 Unicode C 資料型別，繫結，即使基礎驅動程式不支援 Unicode 資料。  
  
> [!NOTE]  
>  這個函式取代 ODBC 1.0 函式**SQLSetParam**。 如需詳細資訊，請參閱 「 註解。 」  
  
## <a name="syntax"></a>語法  
  
```  
  
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
  
 *Sqlbindparameter*  
 [輸入]參數編號排序循序遞增的參數順序，從 1 開始。  
  
 *InputOutputType*  
 [輸入]參數的型別。 如需詳細資訊，請參閱 「*了*引數 」 中 「 註解 」。  
  
 *ValueType*  
 [輸入]參數的 C 資料類型。 如需詳細資訊，請參閱 「*ValueType*引數 」 中 「 註解 」。  
  
 *ParameterType*  
 [輸入]SQL 資料類型的參數。 如需詳細資訊，請參閱 「*ParameterType*引數 」 中 「 註解 」。  
  
 *ColumnSize*  
 [輸入]資料行或運算式的對應參數標記的大小。 如需詳細資訊，請參閱 「*ColumnSize*引數 」 中 「 註解 」。  
  
 如果您的應用程式會在 64 位元 Windows 作業系統上執行，請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *D*  
 [輸入]運算式的對應參數標記之資料行的小數位數。 如需資料行大小的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *ParameterValuePtr*  
 [延遲的輸入]參數的資料緩衝區的指標。 如需詳細資訊，請參閱 「*ParameterValuePtr*引數 」 中 「 註解 」。  
  
 *BufferLength*  
 [輸入/輸出]長度*ParameterValuePtr*以位元組為單位的緩衝區。 如需詳細資訊，請參閱 「*Columnsize*引數 」 中 「 註解 」。  
  
 請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)，如果您的應用程式將在 64 位元作業系統上執行。  
  
 *StrLen_or_IndPtr*  
 [延遲的輸入]為參數的長度的緩衝區指標。 如需詳細資訊，請參閱 「*StrLen_or_IndPtr*引數 」 中 「 註解 」。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLBindParameter**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLBindParameter** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|所識別的資料型別*ValueType*引數無法轉換成所識別的資料型別*ParameterType*引數。 請注意，此錯誤可能會傳回**SQLExecDirect**， **SQLExecute**，或**SQLPutData**在執行階段，而不是由**SQLBindParameter**.|  
|07009|無效的描述元索引|(DM) 指定的引數的值*Sqlbindparameter*是小於 1。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 **MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY003|應用程式緩衝區類型無效|引數所指定的值*ValueType*不是有效的 C 資料類型或 SQL_C_DEFAULT。|  
|HY004|無效的 SQL 資料類型|指定的引數的值*ParameterType*已不是有效的 ODBC SQL 資料類型識別碼，也不是驅動程式特有的 SQL 資料類型識別碼驅動程式支援。|  
|HY009|引數值無效|(DM) 引數*ParameterValuePtr*是 null 指標，而引數*StrLen_or_IndPtr* null 指標，以及引數*了*未 SQL_PARAM_輸出。<br /><br /> (DM) SQL_PARAM_OUTPUT 位置引數*ParameterValuePtr*是 null 指標，C 類型是字元或二進位和 Columnsize (*cbValueMax*) 大於 0。|  
|HY010|函數順序錯誤|(DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLBindParameter**呼叫。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式的呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY021|不一致的描述項資訊|檢查一致性檢查期間的描述項資訊不一致。 (請參閱 「 一致性檢查 > 一節**SQLSetDescField**。)<br /><br /> 指定的引數的值*d*超出所指定的 SQL 資料類型的資料行的資料來源所支援的值範圍*ParameterType*引數。|  
|HY090|字串或緩衝區長度無效|(DM) 中的值*Columnsize*小於 0。 (請參閱中的 SQL_DESC_DATA_PTR 欄位描述**SQLSetDescField**。)|  
|HY104|無效的有效位數或小數位數的值|指定的引數的值*ColumnSize*或*d*超出所指定的 SQL 資料類型的資料行的資料來源所支援的值範圍*ParameterType*引數。|  
|HY105|無效的參數類型|(DM) 指定的引數的值*了*無效。 （請參閱 「 註解。"）|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|未實作選擇性功能|驅動程式或資料來源不支援指定的引數所指定的值組合的轉換*ValueType*和指定的引數的驅動程式專屬值*ParameterType*.<br /><br /> 指定的引數的值*ParameterType*驅動程式支援 ODBC 的版本，但不支援的驅動程式或資料來源是有效的 ODBC SQL 資料類型識別項。<br /><br /> 此驅動程式支援只 ODBC 2。*x*和引數*ValueType*是下列其中之一：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 所有間隔 C 資料類型會列在[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d： 資料型別中。<br /><br /> 此驅動程式只支援 3.50 和引數之前的 ODBC 版本*ValueType*已 SQL_C_GUID。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
  
## <a name="comments"></a>註解  
 應用程式呼叫**SQLBindParameter**繫結 SQL 陳述式中的每個參數標記。 繫結仍作用中直到應用程式呼叫**SQLBindParameter**再次呼叫**SQLFreeStmt** SQL_RESET_PARAMS 選項或呼叫與**SQLSetDescField**至APD SQL_DESC_COUNT 標頭欄位設為 0。  
  
 如需參數的詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)。 如需參數的資料型別和參數標記的詳細資訊，請參閱[參數資料型別](../../../odbc/reference/appendixes/parameter-data-types.md)和[參數標記](../../../odbc/reference/appendixes/parameter-markers.md)附錄 c: SQL 文法中。  
  
## <a name="parameternumber-argument"></a>Sqlbindparameter 引數  
 如果*Sqlbindparameter*呼叫**SQLBindParameter**大於 SQL_DESC_COUNT，值**SQLSetDescField**呼叫以增加 SQL_DESC_ 的值若要計算*Sqlbindparameter*。  
  
## <a name="inputoutputtype-argument"></a>了引數  
 *了*引數會指定參數的型別。 這個引數設定 IPD SQL_DESC_PARAMETER_TYPE 欄位。 沒有這類呼叫程序的 SQL 陳述式中的所有參數**插入**陳述式，*輸入 * * 參數*。 程序呼叫中的參數可以輸入、 輸入/輸出或輸出參數。 (應用程式呼叫**SQLProcedureColumns**判斷程序呼叫; 中的參數類型無法判別其型別參數會假設是輸入的參數。)  
  
 *了*引數可以是下列值之一：  
  
-   SQL_PARAM_INPUT。 參數標記中不會是程序，例如呼叫的 SQL 陳述式的參數**插入**陳述式，或它將標記中的程序的輸入的參數。 例如，在參數**插入到員工值 (？，？，？)**會輸入的參數，而不包含在參數**{呼叫 AddEmp (？，？，？)}**可以但不一定，輸入的參數。  
  
     當執行陳述式時，驅動程式會將參數資料傳送至資料來源;\* *ParameterValuePtr*緩衝區必須包含有效的輸入的值，或 **StrLen_or_IndPtr*緩衝區必須包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT 結果_EXEC 巨集。  
  
     如果應用程式無法判斷程序呼叫中參數的類型，它會設定*了*至 SQL_PARAM_INPUT; 如果資料來源傳回參數的值驅動程式就會捨棄它。  
  
-   SQL_PARAM_INPUT_OUTPUT。 參數標記的程序中的輸入/輸出參數。 例如，在參數**{呼叫 GetEmpDept(?)}**是輸入/輸出參數會接受員工的名稱，並傳回員工的部門名稱。  
  
     當執行陳述式時，驅動程式會將參數資料傳送至資料來源;\* *ParameterValuePtr*緩衝區必須包含有效的輸入的值，或\* *StrLen_or_IndPtr*緩衝區必須包含 SQL_NULL_DATA、 SQL_DATA_AT_EXEC 或結果SQL_LEN_DATA_AT_EXEC 巨集。 陳述式之後，驅動程式會傳回至應用程式，參數的資料資料來源不會傳回輸入/輸出參數的值，此驅動程式會將 **StrLen_or_IndPtr*緩衝區為 SQL_NULL_DATA。  
  
    > [!NOTE]  
    >  當 ODBC 1.0 應用程式呼叫**SQLSetParam** ODBC 2.0 驅動程式中驅動程式管理員將此呼叫**SQLBindParameter**所在*了*引數會設定為 SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT。 參數標記的程序或輸出參數的程序; 中的傳回值在任一情況下，這些值稱為*輸出參數*。 例如，在參數**{？ = 呼叫 GetNextEmpID}**是輸出參數傳回下一步的員工識別碼。  
  
     陳述式之後，驅動程式會傳回參數資料應用程式，除非*ParameterValuePtr*和*StrLen_or_IndPtr*引數都是 null 指標，在此情況下驅動程式會捨棄的輸出值。 資料來源未傳回輸出參數的值，此驅動程式會將 **StrLen_or_IndPtr*緩衝區為 SQL_NULL_DATA。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM。 指出應該串流處理輸入/輸出參數。 **SQLGetData**可以讀取組件中的參數值。 *Columnsize*已忽略，因為緩衝區長度將決定在呼叫的**SQLGetData**。 值*StrLen_or_IndPtr*緩衝區必須包含 SQL_NULL_DATA、 SQL_DEFAULT_PARAM，SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 巨集的結果。 參數必須繫結來做為在輸入資料上執行 (DAE) 參數，如果將會在輸出資料流。 *ParameterValuePtr*可以是會傳回任何非 null 指標值**SQLParamData**為使用者定義的語彙基元的值傳遞了*ParameterValuePtr*這兩個輸入和輸出。 如需詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM。 SQL_PARAM_INPUT_OUTPUT_STREAM，輸出參數相同。 **StrLen_or_IndPtr*在輸入會被忽略。  
  
 下表列出的不同組合*了*和 **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|결과|在每 ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入中的組件|*ParameterValuePtr*可以是任何會傳回的指標值**SQLParamData**為使用者定義的語彙基元的值傳遞了*ParameterValuePtr*。|  
|SQL_PARAM_INPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入繫結緩衝區|*ParameterValuePtr*是輸入緩衝區的位址。|  
|SQL_PARAM_OUTPUT|在輸入會被忽略。|輸出繫結的緩衝區|*ParameterValuePtr*是輸出緩衝區的位址。|  
|SQL_PARAM_OUTPUT_STREAM|在輸入會被忽略。|資料流處理的輸出|*ParameterValuePtr*可以是任何指標值，會傳回**SQLParamData**為使用者定義的語彙基元的值傳遞了*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入中的組件和輸出繫結的緩衝區|*ParameterValuePtr*也會傳回的輸出緩衝區的位址**SQLParamData**為使用者定義的語彙基元的值傳遞了*ParameterValuePtr*。|  
|SQL_PARAM_INPUT_OUTPUT|不 SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入繫結緩衝區和輸出繫結的緩衝區|*ParameterValuePtr*是共用的輸入/輸出緩衝區的位址。|  
L_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) 或 SQL_DATA_AT_EXEC|輸入中的組件和資料流處理的輸出|*ParameterValuePtr*可以是任何非 null 指標值，會傳回**SQLParamData**為使用者定義的語彙基元的值傳遞了*ParameterValuePtr*這兩個輸入和輸出。|  
  
> [!NOTE]  
>  驅動程式必須決定當串流應用程式繫結其輸出或輸入輸出參數時，允許 SQL 類型。 驅動程式管理員不會產生錯誤。 無效的 SQL 型別。  
  
## <a name="valuetype-argument"></a>ValueType 引數  
 *ValueType*引數會指定參數的 C 資料類型。 這個引數設定 APD 中的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位。 這必須是其中一個值在[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)附錄 d： 資料類型 > 一節。  
  
 如果*ValueType*引數是其中一個間隔資料類型的 SQL_DESC_TYPE 欄位*Sqlbindparameter* APD 中的記錄設定為 SQL_INTERVAL，APD SQL_DESC_CONCISE_TYPE 欄位設定為精簡的間隔資料類型和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位*Sqlbindparameter*記錄設定為特定間隔資料型別子代碼。 (請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)預設間隔分別在 APD SQL_DESC_DATETIME_INTERVAL_PRECISION 和 SQL_DESC_PRECISION 欄位中所設定開頭有效位數 (2) 和預設間隔秒數有效位數 (6)，可用的資料。 如果其中一個預設有效位數不適用，應用程式應該明確設定描述項欄位呼叫**SQLSetDescField**或**SQLSetDescRec**。  
  
 如果*ValueType*引數是其中一個 datetime 資料類型的 SQL_DESC_TYPE 欄位*Sqlbindparameter* APD 中的記錄設定為 SQL_DATETIME， SQL_DESC_CONCISE_TYPE欄位*Sqlbindparameter* APD 中的記錄設定為精簡 datetime C 資料類型，而且 SQL_DESC_DATETIME_INTERVAL_CODE 欄位*Sqlbindparameter*記錄設定為子代碼，特定的日期時間資料型別。 (請參閱[附錄 d： 資料型別](../../../odbc/reference/appendixes/appendix-d-data-types.md)。)  
  
 如果*ValueType*引數是 SQL_C_NUMERIC 資料類型，則預設有效位數 （它是由驅動程式定義），並用預設小數位數 (0)，在 APD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定的資料。 如果預設有效位數或小數位數不適用，應用程式應該明確設定描述項欄位呼叫**SQLSetDescField**或**SQLSetDescRec**。  
  
 SQL_C_DEFAULT 指定參數值在傳輸的預設 C 資料類型，針對與指定的 SQL 資料型別*ParameterType*。  
  
 您也可以指定擴充的 C 資料類型。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 如需詳細資訊，請參閱[預設 C 資料類型](../../../odbc/reference/appendixes/default-c-data-types.md)，[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)，和[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附錄 d： 資料型別中。  
  
## <a name="parametertype-argument"></a>ParameterType 引數  
 這必須是其中一個值中所列[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d： 資料類型，或它的區段必須是驅動程式專屬值。 這個引數設定的 SQL_DESC_TYPE、 SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE IPD 欄位。  
  
 如果*ParameterType*引數是其中一個 datetime 識別項、 IPD 的 SQL_DESC_TYPE 欄位設定為 SQL_DATETIME、 SQL_DESC_CONCISE_TYPE IPD 欄位設定為精簡 datetime SQL 資料類型和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位設定為適當的日期時間子代碼值。  
  
 如果*ParameterType*是其中一個時間間隔的識別項，IPD 的 SQL_DESC_TYPE 欄位設為 SQL_INTERVAL，IPD SQL_DESC_CONCISE_TYPE 欄位會設定為精簡 SQL 間隔資料類型，以及 SQL_DESC_DATETIME_INTERVAL_CODE IPD 欄位設定為適當的間隔子代碼。 IPD SQL_DESC_DATETIME_INTERVAL_PRECISION 欄位會設定為間隔開頭有效位數，而且 SQL_DESC_PRECISION 欄位設定為間隔的秒數有效位數，如果適用的話。 如果 SQL_DESC_DATETIME_INTERVAL_PRECISION 或 SQL_DESC_PRECISION 的預設值是不適當，應用程式應該明確設定它藉由呼叫**SQLSetDescField**。 如需這些欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*引數是 SQL_NUMERIC 資料類型，則預設有效位數 （它是由驅動程式定義），並用預設小數位數 (0)，在 IPD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定的資料。 如果預設有效位數或小數位數不適用，應用程式應該明確設定描述項欄位呼叫**SQLSetDescField**或**SQLSetDescRec**。  
  
 如需如何轉換資料，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)和[轉換資料從 SQL 到 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)附錄 d： 資料型別中。  
  
## <a name="columnsize-argument"></a>ColumnSize 引數  
 *ColumnSize*引數會指定資料行或運算式，對應至參數標記，該資料，或兩者的長度的大小。 這個引數設定 IPD，取決於 SQL 資料類型的不同欄位 ( *ParameterType*引數)。 下列規則適用於此對應：  
  
-   如果*ParameterType* SQL_CHAR、 SQL_VARCHAR、 SQL_LONGVARCHAR、 SQL_BINARY、 SQL_VARBINARY、 SQL_LONGVARBINARY、 或精簡 SQL 日期時間或間隔資料型別之一，IPD 的 SQL_DESC_LENGTH 欄位設為值*ColumnSize*。 (如需詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)附錄 d： 資料類型 > 一節。)  
  
-   如果*ParameterType* SQL_DECIMAL、 SQL_NUMERIC、 SQL_FLOAT、 SQL_REAL，或 SQL_DOUBLE，IPD 的 SQL_DESC_PRECISION 欄位設定為值*ColumnSize*。  
  
-   對於其他資料類型， *ColumnSize*會忽略引數。  
  
 如需詳細資訊，請參閱 < 傳遞參數值 > 和 SQL_DATA_AT_EXEC 中的 「*StrLen_or_IndPtr*引數。"  
  
## <a name="decimaldigits-argument"></a>D 引數  
 如果*ParameterType* SQL_TYPE_TIME、 SQL_TYPE_TIMESTAMP、 SQL_INTERVAL_SECOND、 SQL_INTERVAL_DAY_TO_SECOND、 SQL_INTERVAL_HOUR_TO_SECOND，或 SQL_INTERVAL_MINUTE_TO_SECOND，IPD SQL_DESC_PRECISION 欄位會設定若要*d*。 如果*ParameterType* SQL_NUMERIC 或 SQL_DECIMAL，IPD 的 SQL_DESC_SCALE 欄位設定為*d*。 對於所有其他資料類型， *d*會忽略引數。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 引數  
 *ParameterValuePtr*引數指向的緩衝區，，當**SQLExecute**或**SQLExecDirect**呼叫時，包含參數的實際資料。 資料必須在指定的格式*ValueType*引數。 這個引數設定 APD SQL_DESC_DATA_PTR 欄位。 應用程式可以設定*ParameterValuePtr*引數為 null 指標，只要 *\*StrLen_or_IndPtr* SQL_NULL_DATA 或 SQL_DATA_AT_EXEC。 （這適用於僅為輸入或輸入/輸出參數。）  
  
 如果\* *StrLen_or_IndPtr*結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集或 SQL_DATA_AT_EXEC，然後*ParameterValuePtr*是與參數相關聯的應用程式定義指標值。 它會傳回到應用程式透過**SQLParamData**。 例如， *ParameterValuePtr*可能的非零語彙基元，例如參數數目、 資料、 指標或應用程式用來將輸入的參數繫結結構的指標。 不過，請注意，如果參數是輸入/輸出參數， *ParameterValuePtr*必須是輸出值儲存在緩衝區的指標。 將 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1，如果應用程式可以使用 SQL_ATTR_PARAMS_PROCESSED_PTR 陳述式屬性，並搭配所指向的值*ParameterValuePtr*引數。 例如， *ParameterValuePtr*可能指向的值陣列，而應用程式可能會使用 SQL_ATTR_PARAMS_PROCESSED_PTR 所指向的值從陣列中擷取正確的值。 如需詳細資訊，請參閱本節稍後的 「 傳遞參數值 」。  
  
 如果*了*引數是 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT， *ParameterValuePtr*指向其中驅動程式傳回的輸出值的緩衝區。 如果程序會傳回一或多個結果集， \* *ParameterValuePtr*緩衝區不保證已處理所有結果集/資料列數之後，才能設定。 如果未設定緩衝區，直到處理完成時，輸出參數和傳回值是無法使用，直到**SQLMoreResults**傳回 sql_no_data 為止。 呼叫**SQLCloseCursor**或**SQLFreeStmt**以 SQL_CLOSE 的選項將會導致這些值會被捨棄。  
  
 如果將 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1， *ParameterValuePtr*指向的陣列。 單一 SQL 陳述式會處理完整陣列的輸入或輸入/輸出參數的輸入值，並傳回輸出值的輸入/輸出或輸出參數的陣列。  
  
## <a name="bufferlength-argument"></a>Columnsize 引數  
 字元和二進位的 C 資料*Columnsize*引數指定的長度\* *ParameterValuePtr*緩衝區 （如果它是單一項目） 或中項目的長度\**ParameterValuePtr*陣列 （如果 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1）。 這個引數設定 APD SQL_DESC_OCTET_LENGTH 記錄欄位。 如果應用程式指定多個值， *Columnsize*用來判斷中值的位置 **ParameterValuePtr*陣列內部的輸入和輸出上。 輸入/輸出和輸出參數，它用來決定是否要截斷字元和二進位輸出上的 C 資料：  
  
-   C 字元資料，可用來傳回的位元組數目是否大於或等於*Columnsize*中的資料\* *ParameterValuePtr*會被截斷成*Columnsize* null 結束字元的長度小於而且是以 null 結束的驅動程式。  
  
-   二進位的 C 資料，如果要傳回可用的位元組數目大於*Columnsize*中的資料\* *ParameterValuePtr*會被截斷成*Columnsize*位元組。  
  
 對於所有其他類型的 C 資料*Columnsize*會忽略引數。 長度\* *ParameterValuePtr*緩衝區 （如果它是單一項目） 或中項目的長度\* *ParameterValuePtr*陣列 （如果應用程式呼叫**SQLSetStmtAttr**與*屬性*則 sql_attr_paramset_size 會指定每個參數的多個值的引數) 會假設為 C 資料類型的長度。  
  
 資料流處理的輸出或資料流處理的輸入/輸出參數， *Columnsize*會忽略引數，原因在指定的緩衝區長度**SQLGetData**。  
  
> [!NOTE]  
>  當 ODBC 1.0 應用程式呼叫**SQLSetParam**在 ODBC 3。*x*驅動程式，驅動程式管理員將此呼叫**SQLBindParameter**所在*Columnsize*引數一定是 SQL_SETPARAM_VALUE_MAX。 因為如果 ODBC 3，驅動程式管理員會傳回錯誤。*x*應用程式集*Columnsize*至 SQL_SETPARAM_VALUE_MAX，ODBC 3。*x*驅動程式可以使用這個來判斷呼叫 ODBC 1.0 應用程式時。  
  
> [!NOTE]  
>  在**SQLSetParam**、 應用程式在其中指定長度的方式 **ParameterValuePtr*緩衝區，以便驅動程式可傳回字元或二進位資料，以及將應用程式傳送的方式陣列的字元或二進位的參數值，驅動程式，為驅動程式定義。  
  
## <a name="strlenorindptr-argument"></a>StrLen_or_IndPtr 引數  
 *StrLen_or_IndPtr*引數指向的緩衝區，，當**SQLExecute**或**SQLExecDirect**呼叫時，包含下列其中之一。 （這個引數設定的應用程式參數指標的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 記錄欄位）。  
  
-   中儲存的參數值的長度 **ParameterValuePtr*。 這會被忽略，但字元或二進位的 C 資料除外。  
  
-   SQL_NTS。 參數值是以 null 結束的字串。  
  
-   SQL_NULL_DATA。 參數值是 NULL。  
  
-   SQL_DEFAULT_PARAM。 程序是使用預設參數的值，而不是從應用程式擷取值。 這個值是在呼叫 ODBC 標準語法中的程序中才有效，然後才*了*引數是 SQL_PARAM_INPUT、 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 當\* *StrLen_or_IndPtr*是 SQL_DEFAULT_PARAM， *ValueType*， *ParameterType*， *ColumnSize*， *D*， *Columnsize*，和*ParameterValuePtr*引數會被忽略的輸入參數，並只會用來定義輸入的輸出參數值 /輸出參數。  
  
-   結果的 SQL_LEN_DATA_AT_EXEC (*長度*) 巨集。 參數的資料會傳送具有**SQLPutData**。 如果*ParameterType*引數是 SQL_LONGVARBINARY、 SQL_LONGVARCHAR 或長時間，資料來源專用的資料類型，而且驅動程式會傳回"Y"SQL_NEED_LONG_DATA_LEN 資訊類型中的**SQLGetInfo**，*長度*是數個位元組的資料傳送給參數，否則*長度*必須是負值，而且會被忽略。 如需詳細資訊，請參閱 < 傳遞參數值 > 本節稍後。  
  
     例如，若要指定 10000 個位元組的資料將會傳送具有**SQLPutData**應用程式設定在一個或多個呼叫中，針對 SQL_LONGVARCHAR 參數，**StrLen_or_IndPtr*為 SQL_LEN_DATA_AT_EXEC （10000)。  
  
-   SQL_DATA_AT_EXEC。 參數的資料會傳送具有**SQLPutData**。 當它們呼叫 ODBC 3 時，ODBC 1.0 應用程式會使用此值。*x*驅動程式。 如需詳細資訊，請參閱 < 傳遞參數值 > 本節稍後。  
  
 如果*StrLen_or_IndPtr*為 null 指標，驅動程式假設所有的輸入的參數值都不是 NULL，而且字元和二進位資料是以 null 結束。 如果*了*SQL_PARAM_OUTPUT 或 SQL_PARAM_OUTPUT_STREAM 和*ParameterValuePtr*和*StrLen_or_IndPtr*都是 null 指標，驅動程式捨棄輸出值。  
  
> [!NOTE]  
>  應用程式開發人員會從指定的 null 指標強烈建議您不要*StrLen_or_IndPtr*參數的資料型別時 SQL_C_BINARY。 若要確定該驅動程式非預期不會截斷 SQL_C_BINARY 資料*StrLen_or_IndPtr*應該包含有效的長度值的指標。  
  
 如果*了*引數是 SQL_PARAM_INPUT_OUTPUT、 SQL_PARAM_OUTPUT、 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM， *StrLen_or_IndPtr*指向的緩衝區驅動程式會傳回 SQL_NULL_DATA，可用來傳回中的位元組數目\* *ParameterValuePtr* （不含字元資料的 null 結束位元組），或 SQL_NO_TOTAL (如果可用的位元組數目傳回無法判斷）。 如果程序會傳回一或多個結果集，**StrLen_or_IndPtr*緩衝區不一定是直到所有結果已經都提取的設定。  
  
 如果將 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的值大於 1， *StrLen_or_IndPtr*指向 SQLLEN 值的陣列。 這些可以是任何本節稍早所列的值，然後使用單一的 SQL 陳述式處理。  
  
## <a name="passing-parameter-values"></a>傳遞參數值  
 應用程式可以傳遞參數的值可能是在\* *ParameterValuePtr*緩衝區或含有一或多個呼叫**SQLPutData**。 參數的資料會與**SQLPutData**稱為*資料在執行*參數。 這些通常用來傳送的資料進行 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 參數，並可以混合與其他參數。  
  
 為了傳遞參數值，應用程式會執行下列步驟順序：  
  
1.  呼叫**SQLBindParameter**每個參數繫結參數的值的緩衝區 (*ParameterValuePtr*引數) 和長度/指標 (*StrLen_or_IndPtr*引數）。 資料在執行中參數，如*ParameterValuePtr*是應用程式定義指標值，例如參數數目或資料指標。 值稍後將會傳回，而且可用來識別參數。  
  
2.  將輸入和輸入/輸出中的參數值放\* *ParameterValuePtr*和 **StrLen_or_IndPtr*緩衝區：  
  
    -   對於一般參數，應用程式會放在參數值\* *ParameterValuePtr*緩衝區並在該值的長度 **StrLen_or_IndPtr*緩衝區。 如需詳細資訊，請參閱[設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   應用程式的資料在執行中參數，將 SQL_LEN_DATA_AT_EXEC 結果 (*長度*) 巨集 （當呼叫 ODBC 2.0 驅動程式） 中的 **StrLen_or_IndPtr*緩衝區。  
  
3.  呼叫**SQLExecute**或**SQLExecDirect**執行 SQL 陳述式。  
  
    -   如果有任何資料在執行中參數，程序已完成。  
  
    -   如果有任何資料在執行中參數，則函數會傳回 SQL_NEED_DATA。  
  
4.  呼叫**SQLParamData**來擷取應用程式定義的值中指定*ParameterValuePtr*引數的**SQLBindParameter**第一個要處理的資料在執行參數。 **SQLParamData**傳回 SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  雖然資料在執行中參數類似於資料在執行中資料行，所傳回的值**SQLParamData**每個不同。 資料在執行中參數是資料將傳送的 SQL 陳述式中的參數**SQLPutData**當陳述式與**SQLExecDirect**或**SQLExecute**. 以繫結它們**SQLBindParameter**。 所傳回的值**SQLParamData**指標值傳遞至**SQLBindParameter**中*ParameterValuePtr*引數。 資料在執行中資料行是在資料行的資料列集資料會傳送具有**SQLPutData**更新或加入一個資料列時**SQLBulkOperations**或更新與**SQLSetPos**. 以繫結它們**SQLBindCol**。 所傳回的值**SQLParamData**是中的資料列的位址 **TargetValuePtr*緩衝區 (透過呼叫設定**SQLBindCol**) 正在處理。  
  
5.  呼叫**SQLPutData**傳送參數資料的一或多次。 如果資料值大於需要多個呼叫\* *ParameterValuePtr*中指定的緩衝區**SQLPutData**; 多個呼叫**SQLPutData**只有當傳送字元 C 資料行的字元、 二進位、 或資料來源特定的資料型別或是傳送二進位 C 資料行的字元、 二進位，允許相同的參數或資料來源專用的資料類型。  
  
6.  呼叫**SQLParamData**再次以表示參數，已傳送所有資料。  
  
    -   如果有多個資料在執行中參數， **SQLParamData**傳回 SQL_NEED_DATA 和應用程式定義參數的值為下一個資料執行處理。 應用程式重複步驟 4 和 5。  
  
    -   如果沒有其他資料在執行中參數，程序已完成。 如果陳述式執行成功， **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO; 如果執行失敗，它會傳回 SQL_ERROR。 此時， **SQLParamData**可以傳回任何可以用來執行陳述式函數所傳回的 SQLSTATE (**SQLExecDirect**或**SQLExecute**)。  
  
         輸出值的任何輸入/輸出或輸出參數會用於\* *ParameterValuePtr*和 **StrLen_or_IndPtr*緩衝處理後的應用程式會擷取所有結果集陳述式所產生。  
  
 呼叫**SQLExecute**或**SQLExecDirect**陳述式置於 SQL_NEED_DATA 狀態。 此時，應用程式可以只呼叫**SQLCancel**， **SQLGetDiagField**， **SQLGetDiagRec**， **SQLGetFunctions**， **SQLParamData**，或**SQLPutData**與陳述式或*連接控制代碼*陳述式相關聯。 如果呼叫的陳述式或陳述式相關聯連接的任何其他函式，則函數會傳回 SQLSTATE HY010 （函數順序錯誤）。 陳述式分葉 SQL_NEED_DATA 狀態**SQLParamData**或**SQLPutData**會傳回錯誤， **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或取消陳述式。  
  
 如果應用程式呼叫**SQLCancel**而驅動程式仍會需要的資料在執行中參數的資料，此驅動程式會取消陳述式執行; 接著應用程式可以呼叫**SQLExecute**或**SQLExecDirect**一次。  
  
## <a name="retrieving-streamed-output-parameters"></a>擷取的資料流的輸出參數  
 當應用程式設定*了*SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM，輸出參數值必須擷取一個或多個呼叫**SQLGetData**。 資料流的輸出參數值傳回至應用程式的驅動程式時，它會傳回 SQL_PARAM_DATA_AVAILABLE 下列函式呼叫的回應： **SQLMoreResults**， **SQLExecute**，和**SQLExecDirect**。 應用程式呼叫**SQLParamData**以判定哪個參數值。  
  
 如需 SQL_PARAM_DATA_AVAILABLE 和資料流的輸出參數的詳細資訊，請參閱[使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用參數陣列  
 當應用程式會準備具有參數標記，並傳遞參數陣列中的陳述式時，有可以執行這兩種不同方式。 其中一種方式是依賴後端，整個陳述式與陣列參數的情況下會被視為一個不可部分完成單位的陣列處理功能的驅動程式。 Oracle 是支援的資料來源陣列的處理能力的範例。 若要實作這項功能的另一個方法是產生的 SQL 陳述式，針對每個參數陣列中的參數集的一個 SQL 陳述式批次，並執行批次的驅動程式。 參數陣列不能與**更新 WHERE CURRENT OF**陳述式。  
  
 當處理的參數陣列時，都能使用個別的結果集/資料列計數 （一個用於每個參數集），或結果集/資料列計數可以彙總成一個。 SQL_PARAM_ARRAY_ROW_COUNTS 選項**SQLGetInfo**指出資料列計數可供每個參數 (SQL_PARC_BATCH) 集或只有一個資料列計數為可用 (SQL_PARC_NO_BATCH)。  
  
 SQL_PARAM_ARRAY_SELECTS 選項**SQLGetInfo**指出結果集是否可供每個參數 (SQL_PAS_BATCH) 集，或只有一個結果集是可用 (SQL_PAS_NO_BATCH)。 如果驅動程式不允許使用參數陣列來執行的結果集 – 產生陳述式，SQL_PARAM_ARRAY_SELECTS 傳回 SQL_PAS_NO_SELECT。  
  
 如需詳細資訊，請參閱[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 若要支援的參數陣列，則 sql_attr_paramset_size 會陳述式屬性設定為指定的每個參數的值數目。 如果欄位是大於 1，APD 中的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位必須指向陣列中。 每個陣列之基數等於 SQL_ATTR_PARAMSET_SIZE 的值。  
  
 APD 中的 [SQL_DESC_ROWS_PROCESSED_PTR] 欄位會指向包含已處理，包括錯誤集參數的集合數目的緩衝區。 處理每個參數集時，驅動程式會儲存在緩衝區中的新值。 如果這是 null 指標，將會傳回沒有數字。 陣列的參數使用時，即使設定函式會傳回 SQL_ERROR，會填入 APD SQL_DESC_ROWS_PROCESSED_PTR 欄位所指向的值。 如果傳回 SQL_NEED_DATA，APD SQL_DESC_ROWS_PROCESSED_PTR 欄位所指向的值會設正在處理的參數集。  
  
 當繫結參數陣列而，會發生什麼情況**更新 WHERE CURRENT OF**執行陳述式是由驅動程式定義。  
  
## <a name="column-wise-parameter-binding"></a>資料行取向的參數繫結  
 在資料行取向的繫結、 應用程式繫結不同的參數和長度/指標陣列至每個參數。  
  
 若要使用資料行取向的繫結，應用程式第一次將 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性設定為 SQL_PARAM_BIND_BY_COLUMN。 (這是預設值。)每個資料行繫結，應用程式會執行下列步驟：  
  
1.  配置參數緩衝區陣列。  
  
2.  配置陣列的長度/指標緩衝區。  
  
    > [!NOTE]  
    >  如果應用程式時直接寫入描述項會使用資料行取向的繫結，可以使用個別的陣列，長度和指標資料。  
  
3.  呼叫**SQLBindParameter**具有下列引數：  
  
    -   *ValueType*參數緩衝區陣列中的單一元素的 C 類型。  
  
    -   *ParameterType*是參數的 SQL 型別。  
  
    -   *ParameterValuePtr*是參數緩衝區陣列的位址。  
  
    -   *Columnsize*是參數緩衝區陣列中的單一元素的大小。 *Columnsize*有固定長度資料的資料時，會忽略引數。  
  
    -   *StrLen_or_IndPtr*是長度/指標陣列的位址。  
  
 如需如何使用這項資訊的詳細資訊，請參閱 「 註解中，「 本節稍後的 < ParameterValuePtr 引數 >。 參數的資料行取向的繫結的相關資訊，請參閱[的參數陣列繫結](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>資料列取向的參數繫結  
 在資料列取向的繫結應用程式會定義結構，其中包含每個參數繫結的參數和長度/指標緩衝區。  
  
 若要使用資料列取向的繫結，應用程式會執行下列步驟：  
  
1.  定義結構來保留一組參數 （包括參數和長度/指標緩衝區），並配置這些結構的陣列。  
  
    > [!NOTE]  
    >  如果應用程式時直接寫入描述項會使用資料列取向的繫結，個別欄位可用於長度及指標資料。  
  
2.  包含單一參數集的結構的大小或執行個體到其中的參數會繫結之緩衝區的大小，請設定 SQL_ATTR_PARAM_BIND_TYPE 陳述式屬性。 長度必須包含所有繫結的參數，以及結構或緩衝區，以確定當繫結參數的位址會隨著指定的長度，結果將會為中的相同參數的開頭的任何填補的空間下一個資料列。 當您使用*sizeof* ANSI C 中的運算子，保證此行為。  
  
3.  呼叫**SQLBindParameter**與下列每個參數繫結引數：  
  
    -   *ValueType*是繫結至資料行的參數緩衝區成員的型別。  
  
    -   *ParameterType*是參數的 SQL 型別。  
  
    -   *ParameterValuePtr*是參數緩衝區中成員的第一個陣列元素的位址。  
  
    -   *Columnsize*參數緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是繫結的長度/指標成員的位址。  
  
 如需有關如何使用這項資訊的詳細資訊，請參閱 「*ParameterValuePtr*引數，「 本章節稍後。 參數的資料列取向的繫結的相關資訊，請參閱[的參數陣列繫結](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>錯誤資訊  
 如果驅動程式不會實作為批次 （SQL_PARAM_ARRAY_ROW_COUNTS 選項 SQL_PARC_NO_BATCH 等於） 的參數陣列，如同執行一個陳述式處理錯誤情況。 如果驅動程式確實有實作做為批次的參數陣列，應用程式就可以使用 IPD 的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位來判斷哪一個參數的 SQL 陳述式或參數的參數陣列中造成**SQLExecDirect**或**SQLExecute**傳回錯誤。 此欄位會包含每個資料列的參數值的狀態資訊。 如果此欄位會指出發生錯誤，診斷資料結構中的欄位會指出失敗的參數資料列和參數數目。 陣列中的項目數目會定義在 APD 中，您可以將 SQL_ATTR_PARAMSET_SIZE 陳述式屬性中的 SQL_DESC_ARRAY_SIZE 標頭欄位。  
  
> [!NOTE]  
>  APD 中的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位用來略過參數。 如需忽略參數的詳細資訊，請參閱下節中，「 略過一組參數。"  
  
 當**SQLExecute**或**SQLExecDirect**傳回 SQL_ERROR，IPD SQL_DESC_ARRAY_STATUS_PTR 欄位所指陣列中的項目會包含 SQL_PARAM_ERROR，SQL_PARAM_SUCCESS，SQL_PARAM_SUCCESS_WITH_INFO、 SQL_PARAM_UNUSED 或 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 對於此陣列中每個項目，此診斷資料結構會包含一個或多個狀態記錄。 結構的 SQL_DIAG_ROW_NUMBER 欄位指出造成錯誤的參數值的資料列數目。 如果可以判斷造成錯誤的參數資料列中的特定參數，將 SQL_DIAG_COLUMN_NUMBER 欄位中輸入參數數目。  
  
 參數尚未使用因為較早的參數，強制發生錯誤時，會輸入 SQL_PARAM_UNUSED **SQLExecute**或**SQLExecDirect**中止。 例如，如果有 50 的參數和執行時發生錯誤 fortieth 造成的參數集**SQLExecute**或**SQLExecDirect**中止，則 SQL_PARAM_UNUSED 進入參數至 50 41 狀態陣列。  
  
 輸入 SQL_PARAM_DIAG_UNAVAILABLE 時驅動程式會將參數的陣列視為龐大的單位，因此不會產生這個個別參數的資訊層級錯誤。  
  
 中的單一參數集處理的部分錯誤會導致處理後續的參數集合的陣列中要停止。 其他錯誤不會影響後續的參數處理。 哪些錯誤將會停止處理是由驅動程式定義。 如果不會停止處理、 處理陣列中的所有參數、 結果錯誤，會傳回 SQL_SUCCESS_WITH_INFO 和 SQL_ATTR_PARAMS_PROCESSED_PTR 所定義的緩衝區設定為已都處理的參數集的總數 (所定義SQL_ATTR_PARAMSET_SIZE 陳述式屬性），其中包含錯誤的集合。  
  
> [!CAUTION]  
>  參數陣列的處理中發生錯誤時的 ODBC 行為是在 ODBC 3 不同。*x*比 ODBC 2。*x*。 在 ODBC 2。*x*，函式會傳回 SQL_ERROR 並處理該值。 所指向之緩衝區*pirow*引數的**SQLParamOptions**包含錯誤資料列數目。 在 ODBC 3。*x*函式會傳回 SQL_SUCCESS_WITH_INFO，可能處理可能停止或繼續。 如果它仍繼續，SQL_ATTR_PARAMS_PROCESSED_PTR 所指定的緩衝區會設定所有的參數處理，包括卻造成錯誤的值。 此行為變更可能會導致現有的應用程式的問題。  
  
 當**SQLExecute**或**SQLExecDirect**傳回前完成的參數陣列中的所有參數集的處理，例如狀態陣列傳回 SQL_ERROR 或 SQL_NEED_DATA 時，包含已經處理這些參數的狀態。 IPD 中的 SQL_DESC_ROWS_PROCESSED_PTR 欄位所指向的位置包含造成 SQL_ERROR 或 SQL_NEED_DATA 錯誤程式碼的參數陣列中的資料列編號。 參數的陣列傳送至 SELECT 陳述式時，狀態陣列值的可用性時，驅動程式定義。在執行陳述式，或做為結果集提取之後，它們可能可以使用。  
  
## <a name="ignoring-a-set-of-parameters"></a>正在略過一組參數  
 （如同透過 SQL_ATTR_PARAM_STATUS_PTR 陳述式屬性） APD SQL_DESC_ARRAY_STATUS_PTR 欄位可以用來表示應該忽略的一組 SQL 陳述式中的繫結參數。 若要引導驅動程式在執行期間略過一個或多組參數，應用程式應該遵循下列步驟：  
  
1.  呼叫**SQLSetDescField**設定為指向包含狀態資訊的 SQLUSMALLINT 值的陣列 APD SQL_DESC_ARRAY_STATUS_PTR 標頭欄位。 這個欄位也可以藉由呼叫設定**SQLSetStmtAttr**與*屬性*的 SQL_ATTR_PARAM_OPERATION_PTR，可讓應用程式設定的欄位，而不取得描述項控制代碼。  
  
2.  設定陣列的兩個值的其中一個 APD SQL_DESC_ARRAY_STATUS_PTR 欄位所定義的每個項目：  
  
    -   SQL_PARAM_IGNORE，表示資料列排除陳述式執行。  
  
    -   SQL_PARAM_PROCEED，表示該資料列包含在陳述式執行。  
  
3.  呼叫**SQLExecDirect**或**SQLExecute**執行備妥的陳述式。  
  
 下列規則適用於陣列的 APD SQL_DESC_ARRAY_STATUS_PTR 欄位所定義：  
  
-   指標會設定預設為 null。  
  
-   如果指標為 null，所有的參數集使用，如同所有項目已設為 SQL_ROW_PROCEED。  
  
-   將項目設定為 SQL_PARAM_PROCEED 不保證此作業，將使用的一組特定的參數。  
  
-   SQL_PARAM_PROCEED 定義為標頭檔中為 0。  
  
 應用程式可以設定 SQL_DESC_ARRAY_STATUS_PTR 欄位指向相同的陣列做為 APD 中指向 SQL_DESC_ARRAY_STATUS_PTR 欄位在 IRD 中。 資料列的資料繫結參數時，這非常有用。 然後會忽略參數，依據資料列資料的狀態。 SQL_PARAM_IGNORE，除了下列的程式碼會導致參數被忽略的 SQL 陳述式： SQL_ROW_DELETED、 SQL_ROW_UPDATED 和 SQL_ROW_ERROR。 除了 SQL_PARAM_PROCEED，下列程式碼會造成 SQL 陳述式，繼續： SQL_ROW_SUCCESS、 SQL_ROW_SUCCESS_WITH_INFO 和 SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新繫結參數  
 應用程式可以執行兩項作業若要變更繫結的其中之一：  
  
-   呼叫**SQLBindParameter**來指定新的繫結資料行已繫結。 驅動程式會以新的覆寫舊的繫結。  
  
-   指定要加入至指定的繫結呼叫的緩衝區位址位移**SQLBindParameter**。 如需詳細資訊，請參閱下節中，「 重新位移與繫結。 」  
  
## <a name="rebinding-with-offsets"></a>位移與重新繫結  
 重新繫結的參數，特別適用於應用程式已經可以包含許多參數，但呼叫緩衝區區域安裝**SQLExecDirect**或**SQLExecute**使用只有少數的參數。 在緩衝區中剩餘的空間可以用於下一個參數集，藉由修改現有的繫結的位移。  
  
 APD 中的 SQL_DESC_BIND_OFFSET_PTR 標頭欄位會指向繫結位移。 如果非 null 的欄位，驅動程式會取值指標而且，若無 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位中的值是 null 指標，將已取值的值加入描述元中這些欄位在執行階段的記錄。 執行 SQL 陳述式時，會使用新的指標值。 位移之後重新繫結就持續有效。 因為 SQL_DESC_BIND_OFFSET_PTR 位移，而不是本身的位移的指標，應用程式可以位移直接變更，而不必呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)至變更描述項欄位。 指標會設定預設為 null。 ARD SQL_DESC_BIND_OFFSET_PTR 欄位可以設定由呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或透過呼叫[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)與*件*SQL_ATTR_PARAM_BIND_ 的OFFSET_PTR。  
  
 繫結位移是一律直接加入 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位中的值。 如果位移變更為不同的值，新的值仍然會加入直接至每個描述項欄位中的值。 新的位移不會加入至欄位值與任何舊版的位移的總和。  
  
## <a name="descriptors"></a>描述元  
 參數繫結的方式取決於 Apd 和 Ipd 欄位。 中的引數**SQLBindParameter**用來設定這些描述項欄位。 欄位也可以設定**SQLSetDescField**函式，雖然**SQLBindParameter**會更有效率使用，因為應用程式並沒有取得描述項控制代碼來呼叫**SQLBindParameter**。  
  
> [!CAUTION]  
>  呼叫**SQLBindParameter**為一個陳述式可能會影響其他陳述式。 會發生這種情況是當陳述式相關聯的 ARD 明確配置，而且也與其他陳述式相關聯。 因為**SQLBindParameter**修改欄位的 APD 所做的修改會套用到與此描述元相關聯的所有陳述式。 如果這不是必要的行為，應用程式應該中斷關聯此描述元的陳述式之前它會呼叫**SQLBindParameter**。  
  
 就概念而言， **SQLBindParameter**序列中執行下列步驟：  
  
1.  呼叫[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)取得 APD 控制代碼。  
  
2.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)取得 APD SQL_DESC_COUNT 欄位中，如果值*ColumnNumber*引數超過 SQL_DESC_COUNT，呼叫的值**SQLSetDescField**增加至 SQL_DESC_COUNT 值*ColumnNumber*。  
  
3.  呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次，以便將值指派給 APD 中的下列欄位：  
  
    -   SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定的值為*ValueType*，不過，如果*ValueType*是其中一個日期時間或間隔子型別精確的識別項，它會將 SQL_DESC_TYPE 設 SQL_日期時間或 SQL_INTERVAL，分別 SQL_DESC_CONCISE_TYPE 簡潔的識別項並 SQL_DESC_DATETIME_INTERVAL_CODE 設的相對應的日期時間或間隔子代碼。  
  
    -   設定為值的 SQL_DESC_OCTET_LENGTH 欄位*Columnsize*。  
  
    -   值設定 SQL_DESC_DATA_PTR 欄位*ParameterValue*。  
  
    -   設定為值的 SQL_DESC_OCTET_LENGTH_PTR 欄位*StrLen_or_Ind*。  
  
    -   值也設定 SQL_DESC_INDICATOR_PTR 欄位*StrLen_or_Ind*。  
  
     *StrLen_or_Ind*參數所指定的標記資訊和參數值的長度。  
  
4.  呼叫[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)取得 IPD 控制代碼。  
  
5.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)取得 IPD SQL_DESC_COUNT 欄位中，如果值*ColumnNumber*引數超過 SQL_DESC_COUNT，呼叫的值**SQLSetDescField**增加至 SQL_DESC_COUNT 值*ColumnNumber*。  
  
6.  呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)多次，以便將值指派給 IPD 下列欄位：  
  
    -   SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定的值為*ParameterType*，不過，如果*ParameterType*是其中一個日期時間或間隔子型別精確的識別項，它會將 SQL_DESC_TYPE如果是 SQL_DATETIME 或 SQL_INTERVAL，若要精簡的識別項，並設定 SQL_DESC_DATETIME_INTERVAL_CODE 相對應的日期時間或間隔的次要代碼來分別設定 SQL_DESC_CONCISE_TYPE。  
  
    -   設定一或多個 SQL_DESC_LENGTH、 SQL_DESC_PRECISION，以及 SQL_DESC_DATETIME_INTERVAL_PRECISION，視*ParameterType*。  
  
    -   值設定 SQL_DESC_SCALE *d*。  
  
 如果呼叫**SQLBindParameter**會失敗，它會設定在 APD 中的描述項欄位的內容會是未定義，且 APD SQL_DESC_COUNT 欄位是不變。 此外，IPD 中的適當資料錄的 SQL_DESC_LENGTH、 SQL_DESC_PRECISION、 SQL_DESC_SCALE 和 SQL_DESC_TYPE 欄位會定義和 IPD 的 SQL_DESC_COUNT 欄位是不變。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>呼叫 SQLSetParam 來回轉換  
 當 ODBC 1.0 應用程式呼叫**SQLSetParam**在 ODBC 3。*x*驅動程式，而 ODBC 3。*x*驅動程式管理員將在下表所示對應呼叫。  
  
|呼叫 ODBC 1.0 應用程式|呼叫 ODBC 3。*x*驅動程式|  
|----------------------------------|-------------------------------|  
|SQLSetParam StatementHandle、 Sqlbindparameter、 ValueType、 ParameterType、 LengthPrecision、 ParameterScale、 ParameterValuePtr (StrLen_or_IndPtr）;|SQLBindParameter (StatementHandle、 Sqlbindparameter、 SQL_PARAM_INPUT_OUTPUT、 ValueType、 ParameterType， *ColumnSize*， *d*，ParameterValuePtr、 SQL_SETPARAM_VALUE_MAX，     StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式正在準備 SQL 陳述式將資料插入 ORDERS 資料表。 每個參數的陳述式中，應用程式呼叫**SQLBindParameter**指定 ODBC C 資料類型和參數的 SQL 資料類型，以及緩衝區繫結到每個參數。 每個資料列的資料，應用程式將資料值指派給每個參數並呼叫**SQLExecute**執行陳述式。  
  
 下列範例會假設您擁有的 ODBC 資料來源，在電腦上稱為 Northwind 與 Northwind 資料庫相關聯。  
  
 如需更多的程式碼範例，請參閱[SQLBulkOperations 函式](../../../odbc/reference/syntax/sqlbulkoperations-function.md)， [SQLProcedures 函數](../../../odbc/reference/syntax/sqlprocedures-function.md)， [SQLPutData 函數](../../../odbc/reference/syntax/sqlputdata-function.md)，和[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
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
  
```  
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
|傳回將資料傳送下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多個參數值|[SQLParamOptions 函式](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|傳送參數資料在執行階段|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
