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
ms.openlocfilehash: 65f6145f0cbfbd59fffb71e030f6427ea1f551c0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036212"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函數

**標準**  
 引進的版本： ODBC 2.0 標準合規性： ODBC  
  
 **摘要**  
 **SQLBindParameter**會將緩衝區系結至 SQL 語句中的參數標記。 **SQLBindParameter**支援系結至 unicode C 資料類型，即使基礎驅動程式不支援 unicode 資料也一樣。  
  
> [!NOTE]  
>  此函式會取代 ODBC 1.0 函數**SQLSetParam**。 如需詳細資訊，請參閱「批註」。  
  
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
 源語句控制碼。  
  
 *ParameterNumber*  
 源參數編號，以遞增的參數順序順序排序，從1開始。  
  
 *InputOutputType*  
 源參數的類型。 如需詳細資訊，請參閱「批註」中的「*InputOutputType*引數」。  
  
 *ValueType*  
 源參數的 C 資料類型。 如需詳細資訊，請參閱「批註」中的「*ValueType*引數」。  
  
 *ParameterType*  
 源參數的 SQL 資料類型。 如需詳細資訊，請參閱「批註」中的「*ParameterType*引數」。  
  
 *ColumnSize*  
 源對應的參數標記之資料行或運算式的大小。 如需詳細資訊，請參閱「批註」中的「*ColumnSize*引數」。  
  
 如果您的應用程式將在64位的 Windows 作業系統上執行，請參閱[ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *DecimalDigits*  
 源對應的參數標記之資料行或運算式的十進位數。 如需有關資料行大小的詳細資訊，請參閱資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *ParameterValuePtr*  
 [延後輸入]參數資料的緩衝區指標。 如需詳細資訊，請參閱「批註」中的「*ParameterValuePtr*引數」。  
  
 *BufferLength*  
 [輸入/輸出]*ParameterValuePtr*緩衝區的長度（以位元組為單位）。 如需詳細資訊，請參閱「批註」中的「*BufferLength*引數」。  
  
 如果您的應用程式將在64位作業系統上執行，請參閱[ODBC 64 位資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *StrLen_or_IndPtr*  
 [延後輸入]參數長度之緩衝區的指標。 如需詳細資訊，請參閱「批註」中的「*StrLen_or_IndPtr*引數」。  
  
## <a name="returns"></a>傳回值

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷

 當**SQLBindParameter**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫具有 SQL_HANDLE_STMT *HandleType*和*StatementHandle**控制碼*的**SQLGetDiagRec**來取得相關聯的 SQLSTATE 值。 下表列出通常由**SQLBindParameter**所傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「（DM）」標記法優先于驅動程式管理員所傳回之 SQLSTATEs 的描述。 除非另有說明，否則，與每個 SQLSTATE 值相關聯的傳回碼都是 SQL_ERROR。  

|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的參考用訊息。 （函數會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|限制的資料類型屬性違規|*ValueType*引數所識別的資料類型無法轉換成*ParameterType*引數所識別的資料類型。 請注意， **SQLExecDirect**、 **SQLExecute**或**SQLPutData**可能會在執行時間傳回此錯誤，而不是**SQLBindParameter**。|  
|07009|不正確描述項索引|（DM）為引數*ParameterNumber*指定的值小於1。|  
|HY000|一般錯誤|發生錯誤，但沒有任何特定 SQLSTATE，且未定義任何執行特定的 SQLSTATE。 **MessageText*緩衝區中的**SQLGetDiagRec**所傳回的錯誤訊息描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函數所需的記憶體。|  
|HY003 以及|不正確應用程式緩衝區類型|引數*ValueType*指定的值不是有效的 C 資料類型或 SQL_C_DEFAULT。|  
|HY004|不正確 SQL 資料類型|為引數*ParameterType*指定的值不是有效的 ODBC SQL 資料類型識別碼，也不是驅動程式所支援的驅動程式特定的 SQL 資料類型識別碼。|  
|HY009|不正確引數值|（DM）引數*ParameterValuePtr*是 null 指標，引數*StrLen_or_IndPtr*是 null 指標，而引數*InputOutputType*不是 SQL_PARAM_OUTPUT。<br /><br /> （DM） SQL_PARAM_OUTPUT，其中引數*ParameterValuePtr*為 null 指標，C 類型為 char 或 binary，而 BufferLength （*cbValueMax*）大於0。|  
|HY010|函數順序錯誤|（DM）已針對與*StatementHandle*相關聯的連接控制碼呼叫以非同步方式執行的函式。 呼叫**SQLBindParameter**時，這個非同步函數仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResults** ，並 SQL_PARAM_DATA_AVAILABLE 傳回。 在抓取所有資料流程參數的資料之前，會呼叫這個函式。<br /><br /> （DM）已針對*StatementHandle*呼叫非同步執行的函式，且在呼叫此函式時仍在執行中。<br /><br /> （DM）已針對*StatementHandle*呼叫**SQLExecute**、 **SQLExecDirect**、 **SQLBulkOperations**或**SQLSetPos** ，並傳回 SQL_NEED_DATA。 在傳送資料給所有資料執行中參數或資料行之前，已呼叫此函數。|  
|HY013|記憶體管理錯誤|無法處理函數呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的狀況。|  
|HY021|不一致的描述項資訊|在一致性檢查期間檢查的描述項資訊不一致。 （請參閱**SQLSetDescField**中的「一致性檢查」一節）。<br /><br /> 針對引數*DecimalDigits*所指定的值，超出*ParameterType*引數所指定之 SQL 資料類型資料行的資料來源所支援的值範圍。|  
|HY090|不正確字串或緩衝區長度|（DM） *BufferLength*中的值小於0。 （請參閱**SQLSetDescField**中 [SQL_DESC_DATA_PTR] 欄位的描述）。|  
|HY104|有效位數或小數位數值無效|針對引數*ColumnSize*或*DecimalDigits*所指定的值，超出*ParameterType*引數所指定之 SQL 資料類型資料行的資料來源所支援的值範圍。|  
|HY105|不正確參數類型|（DM）為引數*InputOutputType*指定的值無效。 （請參閱「留言」）。|  
|HY117|連接因未知的交易狀態而暫停。 僅允許中斷連線和唯讀功能。|（DM）如需暫停狀態的詳細資訊，請參閱[SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md)函式。|  
|HYC00|未執行的選擇性功能|驅動程式或資料來源不支援指定給引數*ValueType*的值組合所指定的轉換，以及為引數*ParameterType*指定的驅動程式特定值。<br /><br /> 為引數*ParameterType*指定的值是驅動程式所支援之 odbc 版本的有效 odbc SQL 資料類型識別碼，但驅動程式或資料來源不支援。<br /><br /> 此驅動程式僅支援 ODBC 2。*x*和引數的*ValueType*為下列其中一項：<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 以及附錄 D：資料類型中[c 資料類型](../../../odbc/reference/appendixes/c-data-types.md)所列的所有 interval c 資料類型。<br /><br /> 驅動程式只支援3.50 之前的 ODBC 版本，並 SQL_C_GUID 引數*ValueType* 。|  
|HYT01|連接逾時已過期|在資料來源回應要求之前，連接逾時時間已過期。 連接逾時時間是透過**SQLSetConnectAttr**設定，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此功能|（DM）與*StatementHandle*相關聯的驅動程式不支援此功能。|  
  
## <a name="comments"></a>註解

 應用程式會呼叫**SQLBindParameter** ，以系結 SQL 語句中的每個參數標記。 系結會持續有效，直到應用程式再次呼叫**SQLBindParameter** 、以 SQL_RESET_PARAMS 選項呼叫**SQLFreeStmt** ，或呼叫**SQLSetDescField**將 APD 的 SQL_DESC_COUNT 標頭欄位設定為0。  
  
 如需參數的詳細資訊，請參閱[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。 如需參數資料類型和參數標記的詳細資訊，請參閱附錄 C： SQL 文法中的[參數資料類型](../../../odbc/reference/appendixes/parameter-data-types.md)和[參數標記](../../../odbc/reference/appendixes/parameter-markers.md)。  
  
## <a name="parameternumber-argument"></a>ParameterNumber 引數  
 如果**SQLBindParameter**呼叫中的*ParameterNumber*大於 SQL_DESC_COUNT 的值，則會呼叫**SQLSetDescField**來將 SQL_DESC_COUNT 的值增加至*ParameterNumber*。  
  
## <a name="inputoutputtype-argument"></a>InputOutputType 引數  
 *InputOutputType*引數會指定參數的類型。 這個引數會設定 IPD 的 SQL_DESC_PARAMETER_TYPE 欄位。 不會呼叫程式的 SQL 語句中的所有參數（例如**INSERT**語句）都是*輸入 * * 參數*。 程序呼叫中的參數可以是輸入、輸入/輸出或輸出參數。 （應用程式會呼叫**SQLProcedureColumns**來判斷程序呼叫中的參數類型; 無法判斷其類型的參數會假設為輸入參數）。  
  
 *InputOutputType*引數是下列其中一個值：  
  
-   SQL_PARAM_INPUT。 參數會在不會呼叫程式的 SQL 語句（例如**INSERT**語句）中標記參數，或在程式中標記輸入參數。 例如，**插入 EMPLOYEE 值（?,?,?）** 中的參數是輸入參數，而 **{call AddEmp （?,?,?）}** 中的參數可以是，但不一定是輸入參數。  
  
     執行語句時，驅動程式會將參數的資料傳送至資料來源;\* *ParameterValuePtr*緩衝區必須包含有效的輸入值，或 **StrLen_or_IndPtr*緩衝區必須包含 SQL_LEN_DATA_AT_EXEC 宏的 SQL_Null_DATA、SQL_DATA_AT_EXEC 或結果。  
  
     如果應用程式無法在程序呼叫中判斷參數的類型，它會將*InputOutputType*設定為 SQL_PARAM_INPUT;如果資料來源傳回參數的值，驅動程式會將它捨棄。  
  
-   SQL_PARAM_INPUT_OUTPUT。 參數會標記程式中的輸入/輸出參數。 例如， **{Call GetEmpDept （？）}** 中的參數是一個輸入/輸出參數，可接受員工的名稱並傳回員工部門的名稱。  
  
     執行語句時，驅動程式會將參數的資料傳送至資料來源;\* *ParameterValuePtr*緩衝區必須包含有效的輸入值，或者\* *StrLen_or_IndPtr*緩衝區必須包含 SQL_LEN_DATA_AT_EXEC 宏的 SQL_Null_DATA、SQL_DATA_AT_EXEC 或結果。 在執行語句之後，驅動程式會將參數的資料傳回給應用程式。如果資料來源未傳回輸入/輸出參數的值，驅動程式會將 **StrLen_or_IndPtr*緩衝區設定為 SQL_Null_DATA。  
  
    > [!NOTE]  
    >  當 ODBC 1.0 應用程式在 ODBC 2.0 驅動程式中呼叫**SQLSetParam**時，驅動程式管理員會將此轉換成**SQLBindParameter**的呼叫，其中*InputOutputType*引數會設定為 SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT。 參數會標記程式的傳回值或程式中的輸出參數。不論是哪一種情況，都稱為「*輸出參數*」。 例如， **{？ = Call GetNextEmpID}** 中的參數是 output 參數，它會傳回下一個員工識別碼。  
  
     執行語句之後，驅動程式會將參數的資料傳回給應用程式，除非*ParameterValuePtr*和*StrLen_or_IndPtr*引數都是 null 指標，在這種情況下，驅動程式會捨棄輸出值。 如果資料來源未傳回輸出參數的值，驅動程式會將 **StrLen_or_IndPtr*緩衝區設定為 SQL_Null_DATA。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM。 表示輸入/輸出參數應經過資料流程處理。 **SQLGetData**可以讀取部分中的參數值。 *BufferLength*會被忽略，因為緩衝區長度會在呼叫**SQLGetData**時決定。 *StrLen_or_IndPtr*緩衝區的值必須包含 SQL_LEN_DATA_AT_EXEC 宏的 SQL_Null_DATA、SQL_DEFAULT_PARAM、SQL_DATA_AT_EXEC 或結果。 參數必須在輸入時系結為數據執行中（DAE）參數，如果它將在輸出中進行資料流程處理。 *ParameterValuePtr*可以是**SQLParamData**傳回的任何非 null 指標值，做為使用者定義的 token，其值是以*ParameterValuePtr*針對輸入和輸出來傳遞。 如需詳細資訊，請參閱[使用 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM。 與 SQL_PARAM_INPUT_OUTPUT_STREAM 相同，適用于輸出參數。 *在輸入時，會忽略*StrLen_or_IndPtr* 。  
  
 下表列出不同的*InputOutputType*和 **StrLen_or_IndPtr*組合：  
  
|*InputOutputType*|**StrLen_or_IndPtr*|成果|ParameterValuePtr 上的備註|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC （*LEN*）或 SQL_DATA_AT_EXEC|部分輸入|*ParameterValuePtr*可以是任何會由**SQLParamData**傳回的指標值，做為使用者定義的 token，其值是以*ParameterValuePtr*傳遞。|  
|SQL_PARAM_INPUT|不 SQL_LEN_DATA_AT_EXEC （*LEN*）或 SQL_DATA_AT_EXEC|輸入系結緩衝區|*ParameterValuePtr*是輸入緩衝區的位址。|  
|SQL_PARAM_OUTPUT|在輸入時忽略。|輸出系結緩衝區|*ParameterValuePtr*是輸出緩衝區的位址。|  
|SQL_PARAM_OUTPUT_STREAM|在輸入時忽略。|資料流程輸出|*ParameterValuePtr*可以是任何指標值， **SQLParamData**會傳回其值與*ParameterValuePtr*一起傳遞的使用者定義 token。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC （*LEN*）或 SQL_DATA_AT_EXEC|元件中的輸入和輸出系結緩衝區|*ParameterValuePtr*是輸出緩衝區的位址， **SQLParamData**也會傳回其值與*ParameterValuePtr*一起傳遞的使用者定義 token。|  
|SQL_PARAM_INPUT_OUTPUT|不 SQL_LEN_DATA_AT_EXEC （*LEN*）或 SQL_DATA_AT_EXEC|輸入系結緩衝區和輸出系結緩衝區|*ParameterValuePtr*是共用輸入/輸出緩衝區的位址。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC （*LEN*）或 SQL_DATA_AT_EXEC|元件和資料流程輸出中的輸入|*ParameterValuePtr*可以是任何非 null 指標值，而**SQLParamData**會傳回其值是以*ParameterValuePtr*針對輸入和輸出傳遞的使用者定義 token。|  
  
> [!NOTE]  
>  當應用程式將輸出或輸入輸出參數系結為數據流處理時，驅動程式必須決定允許哪些 SQL 類型。 驅動程式管理員不會針對不正確 SQL 類型產生錯誤。  
  
## <a name="valuetype-argument"></a>ValueType 引數

 *ValueType*引數會指定參數的 C 資料類型。 這個引數會設定 APD 的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位。 這必須是附錄 D：資料類型之[C 資料類型](../../../odbc/reference/appendixes/c-data-types.md)區段中的其中一個值。  
  
 如果*ValueType*引數是其中一個 interval 資料類型，則 APD 之*ParameterNumber*記錄的 [SQL_DESC_TYPE] 欄位會設定為 [SQL_INTERVAL]，APD 的 [SQL_DESC_CONCISE_TYPE] 欄位會設定為 [精確的間隔] 資料類型，而*ParameterNumber*記錄的 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位會設定為特定 [間隔] 資料類型的子代碼。 （請參閱[附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)）。預設的間隔前置精確度（2）和預設間隔秒數精確度（6），會分別在 APD 的 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 和 [SQL_DESC_PRECISION] 欄位中設定，用於資料。 如果任何一個預設有效位數不適當，應用程式應該呼叫**SQLSetDescField**或**SQLSetDescRec**來明確設定描述項欄位。  
  
 如果*ValueType*引數是其中一個 datetime 資料類型，則 APD 之*ParameterNumber*記錄的 [SQL_DESC_TYPE] 欄位會設定為 [SQL_DATETIME]，APD 之*ParameterNumber*記錄的 [SQL_DESC_CONCISE_TYPE] 欄位會設定為 [簡明日期時間 C] 資料類型，而*ParameterNumber*記錄的 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位會設定為特定 datetime 資料類型的子代碼。 （請參閱[附錄 D：資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)）。  
  
 如果*ValueType*引數是 SQL_C_NUMERIC 資料類型，則會針對資料使用預設的有效位數（以驅動程式定義）和預設小數位數（0），如 APD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定。 如果預設的有效位數或小數位數不適合，應用程式應該藉由呼叫**SQLSetDescField**或**SQLSetDescRec**來明確設定描述項欄位。  
  
 SQL_C_DEFAULT 指定要從使用*ParameterType*指定之 SQL 資料類型的預設 C 資料類型，傳送參數值。  
  
 您也可以指定擴充 C 資料類型。 如需詳細資訊，請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 如需詳細資訊，請參閱[預設 C 資料類型](../../../odbc/reference/appendixes/default-c-data-types.md)、[將資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)和在附錄 D：資料類型中[將資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
## <a name="parametertype-argument"></a>ParameterType 引數

 這必須是附錄 D：資料類型的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)一節中所列的其中一個值，或者必須是驅動程式特定的值。 這個引數會設定 IPD 的 SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE 和 SQL_DESC_DATETIME_INTERVAL_CODE 欄位。  
  
 如果*ParameterType*引數是其中一個日期時間識別碼，ipd 的 [SQL_DESC_TYPE] 欄位會設定為 [SQL_DATETIME]、[ipd] 的 [SQL_DESC_CONCISE_TYPE] 欄位會設定為 [簡明日期時間] SQL 資料類型，而 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位會設定為適當的 datetime 子代碼值。  
  
 如果*ParameterType*是其中一個間隔識別碼，ipd 的 [SQL_DESC_TYPE] 欄位會設定為 [SQL_INTERVAL]、[ipd] 的 [SQL_DESC_CONCISE_TYPE] 欄位會設定為 [簡潔的 SQL 間隔] 資料類型，而 [ipd] 的 [SQL_DESC_DATETIME_INTERVAL_CODE] 欄位會設定為適當的間隔子代碼。 IPD 的 [SQL_DESC_DATETIME_INTERVAL_PRECISION] 欄位會設定為間隔的有效位數，而且 [SQL_DESC_PRECISION] 欄位會設定為間隔的秒數有效位數（如果適用的話）。 如果 SQL_DESC_DATETIME_INTERVAL_PRECISION 或 SQL_DESC_PRECISION 的預設值不適合，應用程式應該藉由呼叫**SQLSetDescField**來明確加以設定。 如需這些欄位的詳細資訊，請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*引數是 SQL_NUMERIC 資料類型，則會針對資料使用預設的有效位數（以驅動程式定義）和預設小數位數（0）（如 IPD 的 SQL_DESC_PRECISION 和 SQL_DESC_SCALE 欄位中所設定）。 如果預設的有效位數或小數位數不適合，應用程式應該藉由呼叫**SQLSetDescField**或**SQLSetDescRec**來明確設定描述項欄位。  
  
 如需如何轉換資料的詳細資訊，請參閱附錄 D：資料類型中的將[資料從 C 轉換成 Sql 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)和[將資料從 SQL 轉換成 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
## <a name="columnsize-argument"></a>ColumnSize 引數

 *ColumnSize*引數會指定對應至參數標記的資料行或運算式的大小、該資料的長度，或兩者。 這個引數會根據 SQL 資料類型（ *ParameterType*引數），設定 IPD 的不同欄位。 下列規則適用于此對應：  
  
-   如果*ParameterType* SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY 或其中一個簡潔的 SQL datetime 或 interval 資料類型，IPD 的 SQL_DESC_LENGTH 欄位會設為*ColumnSize*的值。 （如需詳細資訊，請參閱附錄 D：資料類型中的資料[行大小、小數位數、傳輸八位長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)一節）。  
  
-   如果*ParameterType*為 SQL_DECIMAL、SQL_NUMERIC、SQL_FLOAT、SQL_REAL 或 SQL_DOUBLE，IPD 的 [SQL_DESC_PRECISION] 欄位會設定為*ColumnSize*的值。  
  
-   若為其他資料類型，則會忽略*ColumnSize*引數。  
  
 如需詳細資訊，請參閱 "*StrLen_or_IndPtr*引數" 中的「傳遞參數值」和 SQL_DATA_AT_EXEC。  
  
## <a name="decimaldigits-argument"></a>DecimalDigits 引數

 如果*ParameterType*為 SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、SQL_INTERVAL_SECOND、SQL_INTERVAL_DAY_TO_SECOND、SQL_INTERVAL_HOUR_TO_SECOND 或 SQL_INTERVAL_MINUTE_TO_SECOND，IPD 的 [SQL_DESC_PRECISION] 欄位會設定為*DecimalDigits*。 如果*ParameterType* SQL_NUMERIC 或 SQL_DECIMAL，IPD 的 [SQL_DESC_SCALE] 欄位會設定為*DecimalDigits*。 若為其他所有資料類型，則會忽略*DecimalDigits*引數。  
  
## <a name="parametervalueptr-argument"></a>ParameterValuePtr 引數

 *ParameterValuePtr*引數會指向緩衝區，在呼叫**SQLExecute**或**SQLExecDirect**時，會包含參數的實際資料。 資料必須是*ValueType*引數所指定的格式。 這個引數會設定 APD 的 SQL_DESC_DATA_PTR 欄位。 只要 SQL_Null_DATA 或 SQL_DATA_AT_EXEC * \*StrLen_or_IndPtr* ，應用程式就可以將*ParameterValuePtr*引數設定為 null 指標。 （這只適用于輸入或輸入/輸出參數）。  
  
 如果\* *StrLen_or_IndPtr*是 SQL_LEN_DATA_AT_EXEC （*長度*）宏或 SQL_DATA_AT_EXEC 的結果，則*ParameterValuePtr*是與參數相關聯的應用程式定義指標值。 它會透過**SQLParamData**傳回至應用程式。 例如， *ParameterValuePtr*可能是非零的 token，例如參數編號、資料指標，或是應用程式用來系結輸入參數之結構的指標。 不過，請注意，如果參數是輸入/輸出參數，則*ParameterValuePtr*必須是將儲存輸出值之緩衝區的指標。 如果 SQL_ATTR_PARAMSET_SIZE 語句屬性中的值大於1，則應用程式可以使用 SQL_ATTR_PARAMS_PROCESSED_PTR 語句屬性所指向的值搭配*ParameterValuePtr*引數。 例如， *ParameterValuePtr*可能會指向值的陣列，而應用程式可能會使用指向的值，SQL_ATTR_PARAMS_PROCESSED_PTR 從陣列中取出正確的值。 如需詳細資訊，請參閱本節稍後的「傳遞參數值」。  
  
 如果*InputOutputType*引數 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT，則*ParameterValuePtr*會指向驅動程式傳回輸出值的緩衝區。 如果程式傳回一或多個結果集，則\*在處理所有結果集/資料列計數之前，不保證會設定*ParameterValuePtr*緩衝區。 如果未設定緩衝區，直到處理完成為止，在**SQLMoreResults**傳回 SQL_NO_DATA 之前，輸出參數和傳回值都是無法使用的。 使用 SQL_CLOSE 的選項呼叫**SQLCloseCursor**或**SQLFreeStmt** ，將會捨棄這些值。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 語句屬性中的值大於1，則*ParameterValuePtr*會指向陣列。 單一 SQL 語句會處理輸入或輸入/輸出參數的完整輸入值陣列，並傳回輸入/輸出或輸出參數的輸出值陣列。  
  
## <a name="bufferlength-argument"></a>BufferLength 引數

 針對字元和二進位 C 資料， *BufferLength*引數會指定\* *ParameterValuePtr*緩衝區的長度（如果它是單一元素）或\* *ParameterValuePtr*陣列中元素的長度（如果 SQL_ATTR_PARAMSET_SIZE 語句屬性中的值大於1）。 這個引數會設定 APD 的 [SQL_DESC_OCTET_LENGTH 記錄] 欄位。 如果應用程式指定多個值，則會使用*BufferLength*來判斷 **ParameterValuePtr*陣列中值的位置（在輸入和輸出上）。 針對輸入/輸出和輸出參數，它會用來判斷是否要在輸出時截斷字元和二進位 C 資料：  
  
-   對於字元 C 資料，如果傳回的位元組數目大於或等於*BufferLength*，則\* *ParameterValuePtr*中的資料會被截斷為*BufferLength*較少 null 終止字元的長度，且驅動程式會以 null 終止。  
  
-   對於二進位 C 資料，如果可傳回的位元組數目大於*BufferLength*，則\* *ParameterValuePtr*中的資料會截斷為*BufferLength*位元組。  
  
 對於所有其他類型的 C 資料，會忽略*BufferLength*引數。 \* *ParameterValuePtr*緩衝區的長度（如果它是單一元素）或\* *ParameterValuePtr*陣列中元素的長度（如果應用程式使用 SQL_ATTR_PARAMSET_SIZE 的*屬性*引數來呼叫**SQLSetStmtAttr**來為每個參數指定多個值），則會假設為 C 資料類型的長度。  
  
 若為數據流輸出或資料流程處理的輸入/輸出參數，則會忽略*BufferLength*引數，因為緩衝區長度是在**SQLGetData**中指定。  
  
> [!NOTE]  
>  當 ODBC 1.0 應用程式在 ODBC 3 中呼叫**SQLSetParam**時。*x* Driver，驅動程式管理員會將此轉換成呼叫**SQLBindParameter** ，其中*BufferLength*引數一律 SQL_SETPARAM_VALUE_MAX。 因為如果 ODBC 3，驅動程式管理員會傳回錯誤。*x*應用程式會將*BufferLength*設定為 SQL_SETPARAM_VALUE_MAX，也就是 ODBC 3。*x*驅動程式可以使用它來判斷 ODBC 1.0 應用程式呼叫它的時間。  
  
> [!NOTE]  
>  在**SQLSetParam**中，應用程式指定 **ParameterValuePtr*緩衝區長度的方式，讓驅動程式可以傳回字元或二進位資料，以及應用程式將字元或二進位參數值陣列傳送至驅動程式的方式，都是驅動程式定義的。  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr 引數

 *StrLen_or_IndPtr*引數會指向緩衝區，當呼叫**SQLExecute**或**SQLExecDirect**時，會包含下列其中一項。 （這個引數會設定應用程式參數指標的 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_INDICATOR_PTR 記錄欄位）。  
  
-   儲存在 **ParameterValuePtr*中之參數值的長度。 除了字元或二進位 C 資料以外，會略過這種情況。  
  
-   SQL_NTS。 參數值是以 null 結束的字串。  
  
-   SQL_Null_DATA。 參數值為 Null。  
  
-   SQL_DEFAULT_PARAM。 程式是使用參數的預設值，而不是從應用程式中抓取的值。 這個值只有在以 ODBC 標準語法呼叫的程式中才有效，只有在*InputOutputType*引數是 SQL_PARAM_INPUT、SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_INPUT_OUTPUT_STREAM 時，才會生效。 當\* *StrLen_or_IndPtr*時，會忽略*ParameterType*、 *ColumnSize*、 *DecimalDigits*、 *BufferLength*和*ParameterValuePtr*引數作為輸入*參數，並*僅用於定義輸入/輸出參數的輸出參數值。  
  
-   SQL_LEN_DATA_AT_EXEC （*長度*）宏的結果。 參數的資料會與**SQLPutData**一起傳送。 如果*ParameterType*引數是 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或 long、資料來源特定的資料類型，且驅動程式傳回**SQLGetInfo**中 SQL_NEED_LONG_DATA_LEN 資訊類型的 "Y"， *length*就是要為參數傳送的資料位元組數。否則，*長度*必須為非負值，而且會被忽略。 如需詳細資訊，請參閱本節稍後的「傳遞參數值」。  
  
     例如，若要指定在一或多個呼叫中使用**SQLPutData**傳送10000位元組的資料，請針對 SQL_LONGVARCHAR 參數，應用程式會將 **StrLen_or_IndPtr*設定為 SQL_LEN_DATA_AT_EXEC （10000）。  
  
-   SQL_DATA_AT_EXEC。 參數的資料會與**SQLPutData**一起傳送。 當 ODBC 1.0 應用程式呼叫 ODBC 3 時，會使用這個值。*x*驅動程式。 如需詳細資訊，請參閱本節稍後的「傳遞參數值」。  
  
 如果*StrLen_or_IndPtr*是 null 指標，驅動程式會假設所有輸入參數值都不是 null，而且字元和二進位資料會以 null 結束。 如果*InputOutputType*是 SQL_PARAM_OUTPUT 或 SQL_PARAM_OUTPUT_STREAM 而且*ParameterValuePtr*和*StrLen_or_IndPtr*都是 null 指標，則驅動程式會捨棄輸出值。  
  
> [!NOTE]  
>  當參數的資料類型為 SQL_C_BINARY 時，強烈不建議應用程式開發人員指定*StrLen_or_IndPtr*的 null 指標。 為確保驅動程式不會意外截斷 SQL_C_BINARY 資料， *StrLen_or_IndPtr*應包含有效長度值的指標。  
  
 如果*InputOutputType*引數是 SQL_PARAM_INPUT_OUTPUT、SQL_PARAM_OUTPUT、SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM， *StrLen_or_IndPtr*會指向驅動程式傳回 SQL_Null_DATA 的緩衝區、可在\* *ParameterValuePtr*中傳回的位元組數目（不包括字元資料的 Null 終止位元組），或 SQL_NO_TOTAL （如果無法判斷可傳回的位元組數目）。 如果程式傳回一或多個結果集，則不保證會設定 **StrLen_or_IndPtr*緩衝區，直到提取所有結果為止。  
  
 如果 SQL_ATTR_PARAMSET_SIZE 語句屬性中的值大於1， *StrLen_or_IndPtr*會指向 SQLLEN 值的陣列。 這些可以是本節稍早所列的任何值，並使用單一 SQL 語句進行處理。  
  
## <a name="passing-parameter-values"></a>傳遞參數值

 應用程式可以在\* *ParameterValuePtr*緩衝區中，或透過一或多個**SQLPutData**呼叫來傳遞參數的值。 其資料以**SQLPutData**傳遞的參數稱為*資料執行中*參數。 這些通常用來傳送 SQL_LONGVARBINARY 和 SQL_LONGVARCHAR 參數的資料，而且可以與其他參數混合使用。  
  
 若要傳遞參數值，應用程式會執行下列一連串的步驟：  
  
1.  呼叫每個參數的**SQLBindParameter** ，以系結參數值（*ParameterValuePtr*引數）和長度/指標（*StrLen_or_IndPtr*引數）的緩衝區。 針對資料執行中的參數， *ParameterValuePtr*是應用程式定義的指標值，例如參數編號或資料指標。 稍後會傳回值，並可用來識別參數。  
  
2.  將\*輸入和輸入/輸出參數的值放在*ParameterValuePtr*和 **StrLen_or_IndPtr*緩衝區中：  
  
    -   若為一般參數，應用程式會將參數值放\*在*ParameterValuePtr*緩衝區中，並將該值的長度置於 **StrLen_or_IndPtr*緩衝區中。 如需詳細資訊，請參閱[設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   針對資料執行中參數，應用程式會將 **StrLen_or_IndPtr*緩衝區中的 SQL_LEN_DATA_AT_EXEC （*長度*）宏（在呼叫 ODBC 2.0 驅動程式時）的結果放入。  
  
3.  呼叫**SQLExecute**或**SQLEXECDIRECT**來執行 SQL 語句。  
  
    -   如果沒有任何資料執行中參數，則程式已完成。  
  
    -   如果有任何資料執行中參數，此函數會傳回 SQL_NEED_DATA。  
  
4.  呼叫**SQLParamData**來抓取**SQLBindParameter**的*ParameterValuePtr*引數中指定的應用程式定義值，以便處理第一個資料執行中的參數。 **SQLParamData**會傳回 SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  雖然資料執行中的參數與資料執行中的資料行相似，但每個**SQLParamData**所傳回的值都不同。 資料執行中參數是 SQL 語句中的參數，當使用**SQLExecDirect**或**SQLExecute**執行語句時，資料會與**SQLPutData**一起傳送。 它們會與**SQLBindParameter**系結。 **SQLParamData**傳回的值是在*ParameterValuePtr*引數中傳遞至**SQLBindParameter**的指標值。 資料執行中的資料行是資料列集中的資料行，當您使用**SQLBulkOperations**更新或以**SQLSetPos**更新資料列時，將會使用**SQLPutData**來傳送資料。 它們會與**SQLBindCol**系結。 **SQLParamData**所傳回的值是所處理之 **TargetValuePtr*緩衝區（由**SQLBindCol**呼叫所設定）中的資料列位址。  
  
5.  會呼叫**SQLPutData**一次或多次，以傳送參數的資料。 如果資料值大於**SQLPutData**中指定的\* *ParameterValuePtr*緩衝區，則需要一個以上的呼叫。只有在將字元 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行，或是將二進位 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行時，才允許使用相同參數的多個**SQLPutData**呼叫。  
  
6.  再次呼叫**SQLParamData** ，表示已針對參數傳送所有資料。  
  
    -   如果有更多的資料執行中參數， **SQLParamData**會傳回 SQL_NEED_DATA，以及要處理的下一個資料執行中參數的應用程式定義值。 應用程式會重複步驟4和5。  
  
    -   如果沒有其他資料執行中參數，則程式已完成。 如果語句成功執行， **SQLParamData**會傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO;如果執行失敗，則會傳回 SQL_ERROR。 此時， **SQLParamData**可以傳回用來執行語句（**SQLExecDirect**或**SQLExecute**）之函式所能傳回的任何 SQLSTATE。  
  
         在應用程式抓取語句所產生的所有結果集之後，任何\*輸入/輸出或輸出參數的輸出值都可以在*ParameterValuePtr*和 **StrLen_or_IndPtr*緩衝區中使用。  
  
 呼叫**SQLExecute**或**SQLExecDirect**會將語句置於 SQL_NEED_DATA 狀態。 此時，應用程式只能呼叫具有語句的**SQLCancel**、 **SQLGetDiagField**、 **SQLGetDiagRec**、 **SQLGetFunctions**、 **SQLParamData**或**SQLPutData** ，或與語句相關聯的*連接控制碼*。 如果它使用語句或與語句相關聯的連接來呼叫任何其他函式，此函式會傳回 SQLSTATE HY010 （函數序列錯誤）。 當**SQLParamData**或**SQLPutData**傳回錯誤、 **SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，或已取消語句時，語句會保留 SQL_NEED_DATA 狀態。  
  
 如果應用程式在驅動程式仍然需要資料執行中參數的資料時呼叫**SQLCancel** ，驅動程式會取消語句執行;然後，應用程式就可以再次呼叫**SQLExecute**或**SQLExecDirect** 。  
  
## <a name="retrieving-streamed-output-parameters"></a>正在抓取資料流程輸出參數

 當應用程式將*InputOutputType*設定為 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM 時，必須透過一或多個**SQLGetData**呼叫來抓取輸出參數值。 當驅動程式具有資料流程輸出參數值來傳回應用程式時，它會傳回 SQL_PARAM_DATA_AVAILABLE 以回應下列函式的呼叫： **SQLMoreResults**、 **SQLExecute**和**SQLExecDirect**。 應用程式會呼叫**SQLParamData**來判斷可用的參數值。  
  
 如需 SQL_PARAM_DATA_AVAILABLE 和資料流程輸出參數的詳細資訊，請參閱[使用 SQLGetData 抓取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用參數陣列

 當應用程式準備具有參數標記並在參數陣列中傳遞的語句時，會有兩種不同的方式可以執行這項工作。 其中一種方式是讓驅動程式依賴後端的陣列處理功能，在此情況下，具有參數陣列的整個語句會被視為一個不可部分完成的單位。 Oracle 是支援陣列處理功能的資料來源範例。 執行此功能的另一種方式是讓驅動程式產生 SQL 語句的批次、參數陣列中每組參數的一個 SQL 語句，然後執行批次。 參數陣列無法搭配**目前的**語句來使用 UPDATE。  
  
 處理參數陣列時，可以使用個別的結果集/資料列計數（每個參數集一個），或將結果集/資料列計數匯總成一個。 **SQLGetInfo**中的 SQL_PARAM_ARRAY_ROW_COUNTS 選項會指出每一組參數（SQL_PARC_BATCH）是否可使用資料列計數，或只有一個資料列計數可用（SQL_PARC_NO_BATCH）。  
  
 **SQLGetInfo**中的 SQL_PARAM_ARRAY_SELECTS 選項會指出每一組參數（SQL_PAS_BATCH）是否有可用的結果集，或是只有一個可用的結果集（SQL_PAS_NO_BATCH）。 如果驅動程式不允許以參數陣列執行結果集產生的語句，SQL_PARAM_ARRAY_SELECTS 會傳回 SQL_PAS_NO_SELECT。  
  
 如需詳細資訊，請參閱[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 為了支援參數陣列，SQL_ATTR_PARAMSET_SIZE 語句屬性會設定為指定每個參數的值數目。 如果欄位大於1，則 APD 的 [SQL_DESC_DATA_PTR]、[SQL_DESC_INDICATOR_PTR] 和 [SQL_DESC_OCTET_LENGTH_PTR] 欄位必須指向 [陣列]。 每個陣列的基數等於 SQL_ATTR_PARAMSET_SIZE 的值。  
  
 APD 的 SQL_DESC_ROWS_PROCESSED_PTR 欄位會指向一個緩衝區，其中包含已處理的參數集數目，包括錯誤集合。 處理每組參數時，驅動程式會在緩衝區中儲存新的值。 如果這是 null 指標，則不會傳回任何數位。 當使用參數陣列時，即使設定函式傳回 SQL_ERROR，也會填入 APD 的 SQL_DESC_ROWS_PROCESSED_PTR 欄位所指向的值。 如果傳回 SQL_NEED_DATA，則 APD 的 [SQL_DESC_ROWS_PROCESSED_PTR] 欄位所指向的值會設定為正在處理的參數集。  
  
 當系結參數陣列，以及執行目前語句的**更新**為驅動程式定義時，會發生什麼情況。  
  
## <a name="column-wise-parameter-binding"></a>資料行取向的參數系結

 在資料行取向的系結中，應用程式會將個別的參數和長度/指標陣列系結至每個參數。  
  
 若要使用資料行取向的系結，應用程式會先將 SQL_ATTR_PARAM_BIND_TYPE 語句屬性設定為 SQL_PARAM_BIND_BY_COLUMN。 （這是預設值）。針對每個要系結的資料行，應用程式會執行下列步驟：  
  
1.  配置參數緩衝區陣列。  
  
2.  配置長度/指標緩衝區的陣列。  
  
    > [!NOTE]  
    >  當使用資料行取向的系結時，如果應用程式直接寫入至描述元，則可以將不同的陣列用於長度和指標資料。  
  
3.  使用下列引數呼叫**SQLBindParameter** ：  
  
    -   *ValueType*是參數緩衝區陣列中單一元素的 C 類型。  
  
    -   *ParameterType*是參數的 SQL 類型。  
  
    -   *ParameterValuePtr*是參數緩衝區陣列的位址。  
  
    -   *BufferLength*是參數緩衝區陣列中單一元素的大小。 當資料為固定長度的資料時，會忽略*BufferLength*引數。  
  
    -   *StrLen_or_IndPtr*是長度/指標陣列的位址。  
  
 如需如何使用這項資訊的詳細資訊，請參閱本節稍後的「批註」中的「ParameterValuePtr 引數」。 如需參數的資料行取向系結的詳細資訊，請參閱系結[參數陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>資料列取向的參數系結

 在資料列取向的系結中，應用程式會定義一個結構，其中包含要系結之每個參數的參數和長度/指標緩衝區。  
  
 若要使用資料列取向的系結，應用程式會執行下列步驟：  
  
1.  定義結構來保存一組參數（包括參數和長度/指標緩衝區），並配置這些結構的陣列。  
  
    > [!NOTE]  
    >  如果使用資料列取向的系結時，應用程式會直接寫入至描述元，則可以將不同的欄位用於長度和指標資料。  
  
2.  將 SQL_ATTR_PARAM_BIND_TYPE 語句屬性設定為包含一組參數的結構大小，或將參數系結至其中的緩衝區實例大小。 長度必須包含所有系結參數的空間，以及結構或緩衝區的任何填補，以確保當系結參數的位址以指定的長度遞增時，結果會指向中相同參數的開頭下一個資料列。 當您在 ANSI C 中使用*sizeof*運算子時，會保證此行為。  
  
3.  針對每個要系結的參數，使用下列引數呼叫**SQLBindParameter** ：  
  
    -   *ValueType*是要系結至資料行之參數緩衝區成員的類型。  
  
    -   *ParameterType*是參數的 SQL 類型。  
  
    -   *ParameterValuePtr*是第一個陣列元素中參數緩衝區成員的位址。  
  
    -   *BufferLength*是參數緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是要系結之長度/指標成員的位址。  
  
 如需有關如何使用這項資訊的詳細資訊，請參閱本節稍後的「*ParameterValuePtr*引數」。 如需有關參數的資料列取向系結的詳細資訊，請參閱參數的系結[陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>錯誤資訊

 如果驅動程式不會將參數陣列實作為批次（SQL_PARAM_ARRAY_ROW_COUNTS 選項等於 SQL_PARC_NO_BATCH），則會如同執行一個語句一樣處理錯誤狀況。 如果驅動程式確實將參數陣列實作為批次，應用程式可以使用 IPD 的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位來判斷 SQL 語句的哪一個參數，或參數陣列中哪個參數導致**SQLExecDirect**或**SQLExecute**傳回錯誤。 此欄位包含參數值之每個資料列的狀態資訊。 如果欄位指出發生錯誤，則診斷資料結構中的欄位將會指出失敗之參數的資料列和參數編號。 陣列中的元素數目將由 APD 中的 SQL_DESC_ARRAY_SIZE 標頭欄位定義，可由 SQL_ATTR_PARAMSET_SIZE 語句屬性設定。  
  
> [!NOTE]  
>  APD 中的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位是用來忽略參數。 如需忽略參數的詳細資訊，請參閱下一節「忽略一組參數」。  
  
 當**SQLExecute**或**SQLExecDirect**傳回 SQL_ERROR 時，IPD 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位所指向之陣列中的元素會包含 SQL_PARAM_ERROR、SQL_PARAM_SUCCESS、SQL_PARAM_SUCCESS_WITH_INFO、SQL_PARAM_UNUSED 或 SQL_PARAM_DIAG_UNAVAILABLE。  
  
 對於此陣列中的每個元素，診斷資料結構會包含一或多個狀態記錄。 結構的 [SQL_DIAG_ROW_NUMBER] 欄位會指出造成錯誤之參數值的資料列編號。 如果可以在導致錯誤的參數資料列中判斷特定的參數，則會在 [SQL_DIAG_COLUMN_NUMBER] 欄位中輸入參數編號。  
  
 未使用參數時，會輸入 SQL_PARAM_UNUSED，因為在強制**SQLExecute**或**SQLExecDirect**中止的舊版參數中發生錯誤。 例如，如果有50個參數，而執行導致**SQLExecute**或**SQLExecDirect**中止的 fortieth 參數集時發生錯誤，則會在參數41到50的狀態陣列中輸入 SQL_PARAM_UNUSED。  
  
 當驅動程式將參數陣列視為整合式單位時，會輸入 SQL_PARAM_DIAG_UNAVAILABLE，因此不會產生此個別參數層級的錯誤資訊。  
  
 處理一組參數時發生一些錯誤，會導致處理陣列中的後續參數集停止。 其他錯誤則不會影響後續參數的處理。 驅動程式定義了哪些錯誤將停止處理。 如果未停止處理，則會處理陣列中的所有參數，SQL_SUCCESS_WITH_INFO 會傳回做為錯誤的結果，而由 SQL_ATTR_PARAMS_PROCESSED_PTR 所定義的緩衝區會設定為已處理的參數集總數（如SQL_ATTR_PARAMSET_SIZE 語句屬性），其中包括錯誤集合。  
  
> [!CAUTION]  
>  Odbc 3 中的參數陣列處理過程中發生錯誤時，ODBC 的行為會有所不同。*x* ，而不是 ODBC 2。*x*。 在 ODBC 2 中。*x*，函式傳回 SQL_ERROR 且處理不正常。 **SQLParamOptions**的*pirow*引數所指向的緩衝區包含錯誤資料列的數目。 在 ODBC 3 中。*x*，此函式會傳回 SQL_SUCCESS_WITH_INFO 而且處理可能會停止或繼續。 如果繼續，SQL_ATTR_PARAMS_PROCESSED_PTR 所指定的緩衝區將會設定為所有已處理參數的值，包括導致錯誤的參數。 這種行為變更可能會對現有的應用程式造成問題。  
  
 當**SQLExecute**或**SQLExecDirect**在完成參數陣列中所有參數集的處理之前傳回，例如當傳回 SQL_ERROR 或 SQL_NEED_DATA 時，狀態陣列會包含已處理之參數的狀態。 IPD 中的 [SQL_DESC_ROWS_PROCESSED_PTR] 欄位所指向的位置包含導致 SQL_ERROR 或 SQL_NEED_DATA 錯誤碼之參數陣列中的資料列編號。 當參數陣列傳送至 SELECT 語句時，狀態陣列值的可用性會由驅動程式定義;在執行語句或提取結果集之後，可能可以使用它們。  
  
## <a name="ignoring-a-set-of-parameters"></a>忽略一組參數

 APD 的 SQL_DESC_ARRAY_STATUS_PTR 欄位（如 SQL_ATTR_PARAM_STATUS_PTR 語句屬性所設定），可以用來表示應該忽略 SQL 語句中的一組系結參數。 若要指示驅動程式在執行期間忽略一或多個參數集，應用程式應遵循下列步驟：  
  
1.  呼叫**SQLSetDescField** ，將 APD 的 SQL_DESC_ARRAY_STATUS_PTR 標頭欄位設定為指向 SQLUSMALLINT 值的陣列，以包含狀態資訊。 您也可以使用 SQL_ATTR_PARAM_OPERATION_PTR 的*屬性*呼叫**SQLSetStmtAttr**來設定這個欄位，讓應用程式可以設定欄位，而不需要取得描述項控制碼。  
  
2.  將 APD 的 SQL_DESC_ARRAY_STATUS_PTR 欄位所定義之陣列的每個元素設定為兩個值的其中一個：  
  
    -   SQL_PARAM_IGNORE，表示資料列已從語句執行中排除。  
  
    -   SQL_PARAM_PROCEED，表示資料列包含在語句執行中。  
  
3.  呼叫**SQLExecDirect**或**SQLExecute**來執行備妥的語句。  
  
 下列規則適用于 APD 的 [SQL_DESC_ARRAY_STATUS_PTR] 欄位所定義的陣列：  
  
-   根據預設，指標會設定為 null。  
  
-   如果指標是 null，則會使用所有的參數集，如同所有元素都已設定為 SQL_ROW_PROCEED。  
  
-   將元素設定為 SQL_PARAM_PROCEED 並不保證作業會使用該特定參數集。  
  
-   在標頭檔中，SQL_PARAM_PROCEED 定義為0。  
  
 應用程式可以將 APD 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為指向 IRD 中 [SQL_DESC_ARRAY_STATUS_PTR] 欄位所指向的相同陣列。 將參數系結至資料列資料時，這會很有用。 然後，可以根據資料列資料的狀態忽略參數。 除了 SQL_PARAM_IGNORE 以外，下列程式碼也會導致忽略 SQL 語句中的參數： SQL_ROW_DELETED、SQL_ROW_UPDATED 和 SQL_ROW_ERROR。 除了 SQL_PARAM_PROCEED 以外，下列程式碼也會導致 SQL 語句繼續進行： SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO 和 SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新系結參數

 應用程式可以執行兩項作業之一來變更系結：  
  
-   呼叫**SQLBindParameter** ，為已經系結的資料行指定新的系結。 驅動程式會以新的系結覆寫舊的系結。  
  
-   指定要加入至**SQLBindParameter**的系結呼叫所指定的緩衝區位址位移。 如需詳細資訊，請參閱下一節「使用位移重新系結」。  
  
## <a name="rebinding-with-offsets"></a>使用位移進行重新系結

 當應用程式的緩衝區區域設定可以包含多個參數，但呼叫**SQLExecDirect**或**SQLExecute**只使用幾個參數時，參數的重新系結特別有用。 緩衝區區域中的剩餘空間可用於下一組參數，方法是以位移修改現有的系結。  
  
 APD 中的 SQL_DESC_BIND_OFFSET_PTR 標頭欄位會指向系結位移。 如果欄位不是 null，驅動程式會取值指標，而且如果 SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 欄位中沒有任何值是 null 指標，則會將已取值的值加入至描述元中的欄位在執行時間記錄。 當執行 SQL 語句時，會使用新的指標值。 在重新系結之後，位移仍然有效。 由於 SQL_DESC_BIND_OFFSET_PTR 是位移的指標，而不是位移本身，因此應用程式可以直接變更位移，而不需要呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)來變更描述項欄位。 根據預設，指標會設定為 null。 ARD 的 [SQL_DESC_BIND_OFFSET_PTR] 欄位可以藉由呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或呼叫*fAttribute*為 SQL_ATTR_PARAM_BIND_OFFSET_PTR 的[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)來設定。  
  
 系結位移一律會直接加入至 [SQL_DESC_DATA_PTR]、[SQL_DESC_INDICATOR_PTR] 和 [SQL_DESC_OCTET_LENGTH_PTR] 欄位中的值。 如果位移變更為不同的值，則新的值仍會直接加入至每個描述項欄位中的值。 新的位移不會加入域值和任何先前位移的總和。  
  
## <a name="descriptors"></a>描述項

 參數的系結方式取決於 Apd 和 Ipd 的欄位。 **SQLBindParameter**中的引數是用來設定這些描述項欄位。 這些欄位也可以由**SQLSetDescField**函數設定，雖然**SQLBindParameter**的效率較高，因為應用程式不需要取得描述項控制碼來呼叫**SQLBindParameter**。  
  
> [!CAUTION]  
>  呼叫一個語句的**SQLBindParameter**可能會影響其他語句。 當與語句相關聯的 ARD 已明確配置，而且也與其他語句相關聯時，就會發生這種情況。 由於**SQLBindParameter**會修改 APD 的欄位，因此修改會套用到與此描述項相關聯的所有語句。 如果這不是必要的行為，應用程式應該在呼叫**SQLBindParameter**之前，將此描述元與其他語句中斷關聯。  
  
 就概念而言， **SQLBindParameter**會依序執行下列步驟：  
  
1.  呼叫[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以取得 APD 控制碼。  
  
2.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)以取得 APD 的 SQL_DESC_COUNT 欄位，如果*ColumnNumber*引數的值超過 SQL_DESC_COUNT 的值，則會呼叫**SQLSetDescField** ，將 SQL_DESC_COUNT 的值增加到*ColumnNumber*。  
  
3.  多次呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ，以將值指派給 APD 的下欄欄位：  
  
    -   將 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定為*ValueType*的值，不同之處在于如果*ValueType*是 datetime 或 interval 子類型的其中一個精簡識別碼，它會分別將 SQL_DESC_TYPE 設定為 SQL_DATETIME 或 SQL_INTERVAL，將 SQL_DESC_CONCISE_TYPE 設定為簡潔的識別碼，並將 SQL_DESC_DATETIME_INTERVAL_CODE 設定為對應的 datetime 或 interval 子代碼。  
  
    -   將 SQL_DESC_OCTET_LENGTH 欄位設定為*BufferLength*的值。  
  
    -   將 SQL_DESC_DATA_PTR 欄位設定為*ParameterValue*的值。  
  
    -   將 SQL_DESC_OCTET_LENGTH_PTR 欄位設定為*StrLen_or_Ind*的值。  
  
    -   將 SQL_DESC_INDICATOR_PTR 欄位也設定為*StrLen_or_Ind*的值。  
  
     *StrLen_or_Ind*參數會同時指定指標資訊和參數值的長度。  
  
4.  呼叫[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以取得 IPD 控制碼。  
  
5.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)以取得 IPD 的 SQL_DESC_COUNT 欄位，如果*ColumnNumber*引數的值超過 SQL_DESC_COUNT 的值，則會呼叫**SQLSetDescField** ，將 SQL_DESC_COUNT 的值增加至*ColumnNumber*。  
  
6.  多次呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) ，以將值指派給 IPD 的下欄欄位：  
  
    -   會將 SQL_DESC_TYPE 和 SQL_DESC_CONCISE_TYPE 設定為*ParameterType*的值，不同之處在于如果*ParameterType*是 datetime 或 interval 子類型的其中一個精簡識別碼，它會分別將 SQL_DESC_TYPE 設定為 SQL_DATETIME 或 SQL_INTERVAL，將 SQL_DESC_CONCISE_TYPE 設定為精簡識別碼，並將 SQL_DESC_DATETIME_INTERVAL_CODE 設定為對應的 datetime 或 interval 子代碼。  
  
    -   設定一或多個 SQL_DESC_LENGTH、SQL_DESC_PRECISION 和 SQL_DESC_DATETIME_INTERVAL_PRECISION，適用于*ParameterType*。  
  
    -   將 SQL_DESC_SCALE 設定為*DecimalDigits*的值。  
  
 如果**SQLBindParameter**的呼叫失敗，則會在 APD 中設定的描述項欄位內容未定義，而且 APD 的 SQL_DESC_COUNT 欄位不會變更。 此外，IPD 中適當記錄的 [SQL_DESC_LENGTH]、[SQL_DESC_PRECISION]、[SQL_DESC_SCALE] 和 [SQL_DESC_TYPE] 欄位並未定義，而 IPD 的 [SQL_DESC_COUNT] 欄位則不會變更。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>SQLSetParam 的呼叫轉換

 當 ODBC 1.0 應用程式在 ODBC 3 中呼叫**SQLSetParam**時。*x*驅動程式，ODBC 3。*x*驅動程式管理員會對應此呼叫，如下表所示。  
  
|ODBC 1.0 應用程式呼叫|呼叫 ODBC 3。*x*驅動程式|  
|----------------------------------|-------------------------------|  
|SQLSetParam （StatementHandle，ParameterNumber，ValueType，ParameterType，LengthPrecision，ParameterScale，ParameterValuePtr，StrLen_or_IndPtr）;|SQLBindParameter （StatementHandle，ParameterNumber，SQL_PARAM_INPUT_OUTPUT，ValueType，ParameterType， *ColumnSize*， *DecimalDigits*，ParameterValuePtr，SQL_SETPARAM_VALUE_MAX，StrLen_or_IndPtr）;|  
  
## <a name="code-example"></a>程式碼範例  
 在下列範例中，應用程式會準備 SQL 語句，以將資料插入 ORDERS 資料表。 對於語句中的每個參數，應用程式會呼叫**SQLBindParameter**來指定 ODBC C 資料類型和參數的 SQL 資料類型，以及將緩衝區系結至每個參數。 針對每個資料列，應用程式會將資料值指派給每個參數，並呼叫**SQLExecute**來執行語句。  
  
 下列範例假設您的電腦上有一個與 Northwind 資料庫相關聯的 ODBC 資料來源，稱為 Northwind。  
  
 如需更多程式碼範例，請參閱[SQLBulkOperations function](../../../odbc/reference/syntax/sqlbulkoperations-function.md)、 [SQLProcedures Function](../../../odbc/reference/syntax/sqlprocedures-function.md)、 [SQLPutData function](../../../odbc/reference/syntax/sqlputdata-function.md)和[SQLSetPos function](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
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

 在下列範例中，應用程式會使用具名引數來執行 SQL Server 預存程式。  
  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|傳回語句中參數的相關資訊|[SQLDescribeParam 函數](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|釋放語句上的參數緩衝區|[SQLFreeStmt 函數](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回語句參數的數目|[SQLNumParams 函數](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|傳回用來傳送資料的下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多個參數值|[SQLParamOptions 函式](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|在執行時間傳送參數資料|[SQLPutData 函數](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱

 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
