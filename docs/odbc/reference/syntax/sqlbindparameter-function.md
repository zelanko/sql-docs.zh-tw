---
title: SQLBind參數函數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02f50862bcfb0295c7f098afc6856c91e0249f66
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301358"
---
# <a name="sqlbindparameter-function"></a>SQLBindParameter 函數

**一致性**  
 版本介紹: ODBC 2.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLBind參數**將緩衝區綁定到 SQL 語句中的參數標記。 **SQLBind參數**支援綁定到 Unicode C 資料類型,即使基礎驅動程式不支援 Unicode 資料也是如此。  
  
> [!NOTE]  
>  此功能取代了 ODBC 1.0 函數**SQLSetParam**。 有關詳細資訊,請參閱"註釋"。  
  
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

 *語句句柄*  
 [輸入]語句句柄。  
  
 *參數編號*  
 [輸入]參數編號,按增加參數順序順序排序,從 1 開始。  
  
 *InputOutputType*  
 [輸入]參數的類型。 有關詳細資訊,請參閱"註釋"中的"*輸入輸出類型*參數"。  
  
 *值類型*  
 [輸入]參數的 C 資料類型。 有關詳細資訊,請參閱"註釋"中的"*價值類型*參數"。  
  
 *參數類型*  
 [輸入]參數的 SQL 資料類型。 有關詳細資訊,請參閱"註釋"中的"*參數類型*參數"。  
  
 *ColumnSize*  
 [輸入]相應參數標記的列或表達式的大小。 有關詳細資訊,請參閱"註釋"中的"*列大小*參數"。  
  
 如果應用程式將在 64 位元 Windows 作業系統上執行,請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *DecimalDigits*  
 [輸入]列或相應參數標記的表達式的小數位數。 關於列大小的詳細資訊,請參閱[欄大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *參數值Ptr*  
 【 延遲輸入 】指向參數數據的緩衝區的指標。 有關詳細資訊,請參閱"註釋"中的"*參數值 Ptr*參數"。  
  
 *緩衝區長度*  
 [輸入/輸出]*參數ValuePtr*緩衝區的長度(以位元組為單位)。 有關詳細資訊,請參閱"註釋"中的"*緩衝區長度*參數"。  
  
 如果應用程式將在 64 位元作業系統上執行,請參閱[ODBC 64 位元資訊](../../../odbc/reference/odbc-64-bit-information.md)。  
  
 *StrLen_or_IndPtr*  
 【 延遲輸入 】指向參數長度的緩衝區的指標。 有關詳細資訊,請參閱"註釋"中的 *"StrLen_or_IndPtr*參數"。  
  
## <a name="returns"></a>傳回值

 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷

 當**SQLBind 參數**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLBindParameter**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  

|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|無法將*ValueType*參數識別的資料類型轉換為*參數類型*參數識別資料類型。 請注意,此錯誤可能由**SQLExecDirect、SQLExecute**或**SQLExecute** **SQLPutData**在執行時返回,而不是由**SQLBind 參數**返回。|  
|07009|不合法的描述符索引|(DM) 為參數*參數編號*指定的值小於 1。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在 @*MessageText*緩衝區中返回的錯誤消息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY003|不合法的應用程式緩衝區型態|參數*ValueType*指定的值不是有效的 C 資料類型或SQL_C_DEFAULT。|  
|HY004|無效的 SQL 資料類型|為參數*參數類型*指定的值既不是有效的 ODBC SQL 資料類型識別碼,也不是驅動程式支援的特定於驅動程式的 SQL 資料類型識別碼。|  
|HY009|不合法參數值|(DM) 參數*參數ValuePtr*是一個空指標,參數*StrLen_or_IndPtr*為空指標,並且參數*InputOutputType*不SQL_PARAM_OUTPUT。<br /><br /> (DM) SQL_PARAM_OUTPUT,其中參數*參數ValuePtr*為空指標,C 類型為字元或二進位,緩衝區長度 *(cbValueMax*) 大於 0。|  
|HY010|函式序列錯誤|(DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用**SQLBind 參數**時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數,並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY021|描述符資訊不一致|在一致性檢查期間檢查的描述符資訊不一致。 (請參閱**SQLSetDescField**中的"一致性檢查" 部分。<br /><br /> 為參數*DecimalDigits*指定的值不在資料來源支援的參數*類型*參數指定的 SQL 資料類型列的值範圍之外。|  
|HY090|不合法的字串或緩衝區長度|(DM)*緩衝區長度*中的值小於 0。 (請參閱**SQLSetDescField**中SQL_DESC_DATA_PTR欄位的說明。|  
|HY104|精確度或縮放值無效|為參數*ColumnSize*或*DecimalDigits*指定的值超出*資料源支援的參數類型*參數指定的 SQL 資料類型列的值範圍。|  
|HY105|不合法參數型態|(DM) 為參數*InputOutputType*指定的值無效。 (請參閱"註釋」。。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYC00|沒有選擇選擇功能|驅動程式或資料來源不支援為參數*ValueType*指定的值和為參數*參數類型*指定的特定於驅動程式的值的組合指定的轉換。<br /><br /> 為參數*參數類型*指定的值是驅動程式支援的 ODBC 版本的有效 ODBC SQL 資料類型識別碼,但驅動程式或資料來源不支援該值。<br /><br /> 驅動程式僅支援 ODBC 2。*x*與參數*ValueType*是以下原因之一:<br /><br /> SQL_C_NUMERICSQL_C_SBIGINTSQL_C_UBIGINT<br /><br /> 以及附錄 D 中的 C[資料類型](../../../odbc/reference/appendixes/c-data-types.md)中列出的所有間隔 C 資料類型:資料類型。<br /><br /> 驅動程式僅支援 3.50 之前的 ODBC 版本,並且參數*ValueType*已SQL_C_GUID。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
  
## <a name="comments"></a>註解

 應用程式呼叫**SQLBind 參數**來綁定 SQL 語句中的每個參數標記。 綁定一直有效,直到應用程式再次呼叫**SQLBind 參數**,使用SQL_RESET_PARAMS選項呼叫**SQLFreeStmt,** 或呼叫**SQLSetDescField**將 APD 的SQL_DESC_COUNT標頭欄位設定為 0。  
  
 有關參數的詳細資訊,請參閱[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。 有關參數資料類型和參數標記的詳細資訊,請參閱附錄 C 中的[參數數據類型](../../../odbc/reference/appendixes/parameter-data-types.md)和[參數標記](../../../odbc/reference/appendixes/parameter-markers.md):SQL 語法。  
  
## <a name="parameternumber-argument"></a>參數編號參數  
 如果呼叫**SQLBind 參數**中的*參數編號*大於SQL_DESC_COUNT的值,則呼叫**SQLSetDescField**將SQL_DESC_COUNT的值增加到*參數編號*。  
  
## <a name="inputoutputtype-argument"></a>輸入輸出型態參數  
 *「輸入輸出類型」* 參數指定參數的類型。 此參數設定 IPD 的SQL_DESC_PARAMETER_TYPE欄位。 SQL 語句中不呼叫過程的所有參數(如**INSERT**語句)都是*輸入參數*。 過程呼叫中的參數可以是輸入、輸入/輸出或輸出參數。 (應用程式呼叫**SQLAEK**確定哪些過程呼叫中的參數類型;無法確定其類型的參數假定為輸入參數。  
  
 *InputOutputType* 引數是下列其中一個值：  
  
-   SQL_PARAM_INPUT 參數在 SQL 語句中標記不調用過程(如**INSERT**語句)的參數,或者在過程中標記輸入參數。 例如,**插入員工值 (?, ?, ?)** 中的參數是輸入參數,而 **[調用 AddEmp(?, ?, ?)]** 中的參數可以是,但不一定是輸入參數。  
  
     執行語句時,驅動程式會將參數的數據發送到數據源;\**參數ValuePtr*緩衝區必須包含有效的輸入值,或者 **StrLen_or_IndPtr*緩衝區必須包含SQL_NULL_DATA、SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC宏的結果。  
  
     如果應用程式無法確定過程呼叫中的參數類型,它將 InputOutputType 設定為SQL_PARAM_INPUT;如果應用程式無法確定過程呼叫中參數的類型,則將 InputOutputType 將其設定為「*輸入輸出類型*」。""""如果"過程呼叫"中參數的類型。"如果"應用程式"無法確定參數的類型。如果數據源返回參數的值,驅動程式將丟棄它。  
  
-   SQL_PARAM_INPUT_OUTPUT 參數在過程中標記輸入/輸出參數。 例如 **,[調用 GetEmpDept(?)]** 中的參數是一個輸入/輸出參數,該參數接受員工的姓名並返回員工部門的名稱。  
  
     執行語句時,驅動程式會將參數的數據發送到數據源;\**參數ValuePtr*緩衝區必須包含有效的輸入值,\*或者*StrLen_or_IndPtr*緩衝區必須包含SQL_NULL_DATA、SQL_DATA_AT_EXEC 或SQL_LEN_DATA_AT_EXEC宏的結果。 執行語句後,驅動程式將參數的數據返回給應用程式;如果資料來源未傳回輸入/輸出參數的值,驅動程式將 **StrLen_or_IndPtr*緩衝區設定為SQL_NULL_DATA。  
  
    > [!NOTE]  
    >  當 ODBC 1.0 應用程式在 ODBC 2.0 驅動程式中調用**SQLSetParam**時,驅動程式管理器將其轉換為**SQLBind 參數**的調用,其中*輸入輸出類型*參數設定為SQL_PARAM_INPUT_OUTPUT。  
  
-   SQL_PARAM_OUTPUT 參數在過程中標記過程或輸出參數的返回值;在這兩種情況下,這些參數稱為*輸出參數*。 例如 **,{?**  
  
     執行語句後,驅動程式將參數的數據返回給應用程式,除非*參數ValuePtr*和*StrLen_or_IndPtr*參數都是空指標,在這種情況下,驅動程式將丟棄輸出值。 如果數據來源不返回輸出參數的值,驅動程式將 **StrLen_or_IndPtr*緩衝區設置為SQL_NULL_DATA。  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM 指示應流式傳輸輸入/輸出參數。 **SQLGetData**可以讀取零件中的參數值。 *緩衝區長度*被忽略,因為緩衝區長度將在**SQLGetData**調用時確定。 *StrLen_or_IndPtr*緩衝區的值必須包含SQL_NULL_DATA、SQL_DEFAULT_PARAM、SQL_DATA_AT_EXEC 或SQL_LEN_DATA_AT_EXEC宏的結果。 如果參數將在輸出時進行流式傳輸,則必須在輸入時將參數綁定為在輸入處的數據執行 (DAE) 參數。 *參數ValuePtr*可以是**SQLParamData**將作為使用者定義的權杖返回的任何非空指標值,其值與*參數ValuePtr*一起傳遞用於輸入和輸出。 有關詳細資訊,請參閱使用[SQLGetData 檢索輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
-   SQL_PARAM_OUTPUT_STREAM 與輸出參數的SQL_PARAM_INPUT_OUTPUT_STREAM相同。 **StrLen_or_IndPtr*在輸入時被忽略。  
  
 下表列輸入*輸出類型*與 **StrLen_or_IndPtr*的不同組合:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|成果|參數值Ptr 的評論|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC(*len*) 或SQL_DATA_AT_EXEC|零件輸入|*參數ValuePtr*可以是**SQLParamData**將作為使用者定義的權杖返回的任何指標值,其值是使用*參數ValuePtr*傳遞的。|  
|SQL_PARAM_INPUT|不要SQL_LEN_DATA_AT_EXEC(*len*) 或SQL_DATA_AT_EXEC|輸入繫結緩衝區|*參數值Ptr*是輸入緩衝區的位址。|  
|SQL_PARAM_OUTPUT|在輸入時忽略。|輸出繫結緩衝區|*參數值Ptr*是輸出緩衝區的位址。|  
|SQL_PARAM_OUTPUT_STREAM|在輸入時忽略。|流輸出|*參數ValuePtr*可以是任何指標值 **,SQLParamData**將作為使用者定義的權杖返回,其值是使用*參數ValuePtr*傳遞的。|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC(*len*) 或SQL_DATA_AT_EXEC|零件與輸出繫結緩衝區的輸入|*參數ValuePtr*是輸出緩衝區的位址 **,SQLParamData**也將作為使用者定義的權杖返回,其值隨*參數ValuePtr*傳遞。|  
|SQL_PARAM_INPUT_OUTPUT|不要SQL_LEN_DATA_AT_EXEC(*len*) 或SQL_DATA_AT_EXEC|輸入繫結緩衝區與輸出繫結緩衝區|*參數值Ptr*是共用輸入/輸出緩衝區的位址。|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC(*len*) 或SQL_DATA_AT_EXEC|零件輸入及流輸出|*參數ValuePtr*可以是任何非空指標值 **,SQLParamData**將作為使用者定義的權杖返回,其值與*參數ValuePtr*一起傳遞用於輸入和輸出。|  
  
> [!NOTE]  
>  當應用程式將輸出或輸入輸出參數綁定為流式處理時,驅動程式必須決定允許哪些 SQL 類型。 驅動程式管理員不會為無效的 SQL 類型生成錯誤。  
  
## <a name="valuetype-argument"></a>值類型參數

 *ValueType*參數指定參數的 C 資料類型。 此參數設置 APD 的SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE欄位。 這必須是附錄 D:數據類型的[C 數據類型](../../../odbc/reference/appendixes/c-data-types.md)部分中的值之一。  
  
 如果*ValueType*參數是間隔資料類型之一,則 APD*的參數編號*記錄的SQL_DESC_TYPE欄位設定為SQL_INTERVAL,APD 的SQL_DESC_CONCISE_TYPE欄位設定為簡潔的間隔資料類型,*並且參數編號*記錄的SQL_DESC_DATETIME_INTERVAL_CODE欄位設置為特定間隔資料類型的子代碼。 ( 參見[附錄 D:資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。數據分別用於 APD 的SQL_DESC_DATETIME_INTERVAL_PRECISION和SQL_DESC_PRECISION欄位中設置的預設間隔前導精度 (2) 和預設間隔秒精度 (6)。 如果任一預設精度不合適,則應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**顯式設置描述符位。  
  
 如果*ValueType*參數是日期時間資料類型之一,則 APD*的參數編號*記錄的SQL_DESC_TYPE欄位設置為SQL_DATETIME,APD*的參數編號*記錄的SQL_DESC_CONCISE_TYPE欄位設定為簡明的日期時間 C 資料類型,*並且參數編號*記錄的SQL_DESC_DATETIME_INTERVAL_CODE字段設置為特定日期時間資料類型的子代碼。 ( 參見[附錄 D:資料類型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。  
  
 如果*ValueType*參數是SQL_C_NUMERIC資料類型,則數據將使用在 APD 的SQL_DESC_PRECISION和SQL_DESC_SCALE欄位中設置的預設精度(即驅動程式定義)和預設比例 (0)。 如果預設精度或比例不合適,則應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**顯式設置描述符位。  
  
 SQL_C_DEFAULT指定參數值從參數*類型*指定的 SQL 資料類型的預設 C 資料類型傳輸。  
  
 您還可以指定延伸的 C 資料類型。 關於詳細資訊,請參閱[ODBC 中的 C 資料類型](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)。  
  
 有關詳細資訊,請參閱預設[C 資料類型](../../../odbc/reference/appendixes/default-c-data-types.md),[將資料從 C 轉換為 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md),以及將[資料從 SQL 轉換為 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md),參見附錄 D:資料類型。  
  
## <a name="parametertype-argument"></a>參數類型參數

 這必須是附錄 D:數據類型的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)部分中列出的值之一,或者它必須是特定於驅動程式的值。 此參數設置 IPD 的SQL_DESC_TYPE、SQL_DESC_CONCISE_TYPE和SQL_DESC_DATETIME_INTERVAL_CODE欄位。  
  
 如果*參數類型*參數是日期時間識別符之一,則 IPD 的SQL_DESC_TYPE欄位設定為SQL_DATETIME,IPD 的SQL_DESC_CONCISE_TYPE欄位設定為簡明的日期時間 SQL 資料類型,並且SQL_DESC_DATETIME_INTERVAL_CODE欄位設定為相應的日期時間子代碼值。  
  
 如果*參數類型*是間隔識別碼之一,則 IPD 的SQL_DESC_TYPE欄位設定為SQL_INTERVAL,IPD 的SQL_DESC_CONCISE_TYPE欄位設定為簡潔的 SQL 間隔資料類型,並且 IPD 的SQL_DESC_DATETIME_INTERVAL_CODE欄位設定為相應的間隔子代碼。 IPD 的SQL_DESC_DATETIME_INTERVAL_PRECISION欄位設置為間隔前導精度,SQL_DESC_PRECISION欄位設置為間隔秒精度(如果適用)。 如果SQL_DESC_DATETIME_INTERVAL_PRECISION或SQL_DESC_PRECISION的預設值不合適,則應用程式應通過調用**SQLSetDescField**顯式設置它。 有關這些欄位中的任何一個的詳細資訊,請參閱[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。  
  
 如果*ValueType*參數是SQL_NUMERIC資料類型,則數據將使用在 IPD SQL_DESC_PRECISION和SQL_DESC_SCALE欄位中設置的預設精度(即驅動程式定義)和預設比例 (0)。 如果預設精度或比例不合適,則應用程式應通過調用**SQLSetDescField**或**SQLSetDescRec**顯式設置描述符位。  
  
 關於資料轉換方式的資訊,請參考在附錄 D:資料型態[中, 將資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md),[以及資料從 SQL 轉換為 C 資料類型](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)。  
  
## <a name="columnsize-argument"></a>欄大小參數

 *ColumnSize*參數指定對應於參數標記的列或表達式的大小、該資料的長度或兩者。 此參數設定 IPD 的不同欄位,具體取決於 SQL 資料類型(*參數類型*參數)。 以下規則適用於此對應:  
  
-   如果*參數類型*為SQL_CHAR、SQL_VARCHAR、SQL_LONGVARCHAR、SQL_BINARY、SQL_VARBINARY、SQL_LONGVARBINARY或其中一個簡潔的 SQL 日期時間或間隔數據類型,則 IPD 的SQL_DESC_LENGTH欄位將設置為*列 Size*的值。 (有關詳細資訊,請參閱附錄 D:數據類型中的[列大小、十進位數字、傳輸八字長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)部分。  
  
-   如果*參數類型*為SQL_DECIMAL、SQL_NUMERIC、SQL_FLOAT、SQL_REAL或SQL_DOUBLE,則 IPD 的SQL_DESC_PRECISION欄位將設置為*列Size*的值。  
  
-   對於其他數據類型,將忽略*ColumnSize*參數。  
  
 有關詳細資訊,請參閱"傳遞參數值"和 *"StrLen_or_IndPtr*參數"中的SQL_DATA_AT_EXEC。  
  
## <a name="decimaldigits-argument"></a>十進位數字參數

 如果*參數類型*為SQL_TYPE_TIME、SQL_TYPE_TIMESTAMP、SQL_INTERVAL_SECOND、SQL_INTERVAL_DAY_TO_SECOND、SQL_INTERVAL_HOUR_TO_SECOND或SQL_INTERVAL_MINUTE_TO_SECOND,則 IPD 的SQL_DESC_PRECISION欄位設定為*十進位數位*。 如果*參數類型*為SQL_NUMERIC或SQL_DECIMAL,則 IPD 的SQL_DESC_SCALE欄位設定為*十進位數字*。 對於所有其他數據類型,將忽略*十進位數字*參數。  
  
## <a name="parametervalueptr-argument"></a>參數值 Ptr 參數

 *參數ValuePtr*參數指向一個緩衝區,當調用**SQLExecute**或**SQLExecDirect**時,該緩衝區包含參數的實際數據。 資料必須採用*ValueType*參數指定的格式。 此參數設置 APD 的SQL_DESC_DATA_PTR欄位。 應用程式可以將*參數ValuePtr*參數設置為空指標,*\** 只要 StrLen_or_IndPtrSQL_NULL_DATA 或SQL_DATA_AT_EXEC。 (這僅適用於輸入或輸入/輸出參數。  
  
 如果\**StrLen_or_IndPtr*是SQL_LEN_DATA_AT_EXEC(*長度*)宏或SQL_DATA_AT_EXEC的結果,則*參數 ValuePtr*是與參數關聯的應用程式定義的指標值。 它通過**SQLParamData**傳回到應用程式。 例如,*參數ValuePtr*可能是非零權杖,如參數編號、指向資料的指標或指向應用程式用於綁定輸入參數的結構的指標。 但是,請注意,如果參數是輸入/輸出參數,*則參數ValuePtr*必須是指向將儲存輸出值的緩衝區的指標。 如果SQL_ATTR_PARAMSET_SIZE語句屬性中的值大於 1,則應用程式可以使用SQL_ATTR_PARAMS_PROCESSED_PTR語句屬性指向的值以及*參數 ValuePtr*參數。 例如 *,ParameterValuePtr*可能指向值陣組,應用程式可能使用SQL_ATTR_PARAMS_PROCESSED_PTR指向的值從陣列中檢索正確的值。 有關詳細資訊,請參閱本節後面的"傳遞參數值"。  
  
 如果*輸入輸出類型*參數SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT,*則參數ValuePtr*指向一個緩衝區,其中驅動程式返回輸出值。 如果過程返回一個或多個結果集,\*則在處理完所有結果集/行計數之前,不能保證設置*參數ValuePtr*緩衝區。 如果在處理完成之前未設置緩衝區,則在**SQLMore 結果**返回SQL_NO_DATA之前,輸出參數和返回值不可用。 使用SQL_CLOSE選項調用**SQLCloseCursor 或** **SQLFreeStmt**將導致丟棄這些值。  
  
 如果SQL_ATTR_PARAMSET_SIZE語句屬性中的值大於 1,*則參數 ValuePtr*指向陣列。 單個 SQL 語句處理輸入或輸入/輸出參數的完整輸入值陣列,並返回輸入/輸出參數的輸出值陣列。  
  
## <a name="bufferlength-argument"></a>緩衝區長度參數

 對於字元和二進位C資料 *,BufferLength*參數\*指定*參數ValuePtr*緩衝區的長度(如果是單個元素\*)或*參數ValuePtr*陣列中元素的長度(如果SQL_ATTR_PARAMSET_SIZE語句屬性中的值大於1)。 此參數設置 APD SQL_DESC_OCTET_LENGTH記錄欄位。 如果應用程式指定多個值,*則緩衝區長度*用於確定在輸入和輸出上在 **參數 ValuePtr*陣列中的值的位置。 對輸入/輸出與輸出參數,用於確定是否截截輸出上的字元和二進制 C 資料:  
  
-   對於字元 C 數據,如果可供返回的位元組數大於或等於*BufferLength,* 則\**參數 ValuePtr*中的數據被截斷為*BufferLength 減去*空終止字元的長度,並且被驅動程式終止。  
  
-   對於二進位C資料,如果可供返回的位元組數大於*BufferLength,* 則\**參數ValuePtr*中的數據將被截斷為*緩衝區長度*位元組。  
  
 對於所有其他類型的 C 數據,將忽略*BufferLength*參數。 \**參數ValuePtr*緩衝區的長度(如果是單個元素)\*或*參數ValuePtr*陣列中元素的長度(如果應用程式呼叫**SQLSetStmtAttr,***屬性*參數為 SQL_ATTR_PARAMSET_SIZE為每個參數指定多個值)假定為 C 資料類型的長度。  
  
 對於流式輸出或流輸入/輸出參數,*將忽略緩衝區長度*參數,因為緩衝區長度是在**SQLGetData**中指定的。  
  
> [!NOTE]  
>  當 ODBC 1.0 應用程式在 ODBC 3 中呼叫**SQLSetParam**時。*x*驅動程式,驅動程式管理器將其轉換為**SQLBind 參數**的調用,其中*緩衝區長度*參數始終SQL_SETPARAM_VALUE_MAX。 因為如果 ODBC 3,驅動程式管理員將返回錯誤。*x*應用程式將*緩衝區長度*設置為 SQL_SETPARAM_VALUE_MAX,即 ODBC 3。*x*驅動程式可以用它來確定 ODBC 1.0 應用程式何時調用它。  
  
> [!NOTE]  
>  在**SQLSetParam**中,應用程式指定 **參數 ValuePtr*緩衝區的長度,以便驅動程式可以返回字元或二進位數據的方式,以及應用程式向驅動程式發送字元或二進位參數值陣列的方式是驅動程式定義的。  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr參數

 *StrLen_or_IndPtr*參數指向一個緩衝區,當調用**SQLExecute**或**SQLExecDirect**時,該緩衝區包含以下一個緩衝區。 (此參數設置應用程式參數指標的SQL_DESC_OCTET_LENGTH_PTR和SQL_DESC_INDICATOR_PTR記錄欄位。  
  
-   儲存在 **參數值 Ptr*中的參數值的長度。 除字元或二進位 C 資料外,將忽略此。  
  
-   SQL_NTS 參數值是 null 連接端字串。  
  
-   SQL_NULL_DATA 參數值為 NULL。  
  
-   SQL_DEFAULT_PARAM 過程是使用參數的預設值,而不是從應用程式檢索的值。 此值僅在 ODBC 規範語法中調用的過程中有效,並且僅當*inputOutputType*參數SQL_PARAM_INPUT、SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_INPUT_OUTPUT_STREAM時才有效。 \* *SQL_DEFAULT_PARAMStrLen_or_IndPtr*時,*值類型*、*參數類型*、*欄大小*、*十進位元數字*,*緩衝區長度*和*參數值 Ptr*參數將被忽略輸入參數,並且僅用於定義輸入 / 輸出參數的輸出參數值。  
  
-   SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果。 參數的數據將與**SQLPutData 一**起發送。 如果*參數類型*參數為 SQL_LONGVARBINARY、SQL_LONGVARCHAR 或特定於資料源的長數據類型,並且驅動程式返回**SQLGetInfo**中SQL_NEED_LONG_DATA_LEN資訊類型的「Y」,*則長度*是要為參數發送的數據位元;否則,*長度*必須為非負值,並且將被忽略。 有關詳細資訊,請參閱本節後面的"傳遞參數值"。  
  
     例如,為了指定在一個或多個調用中使用**SQLPutData**發送 10,000 位元組的數據,對於SQL_LONGVARCHAR參數,應用程式集 =*StrLen_or_IndPtrSQL_LEN_DATA_AT_EXEC* (10000)。  
  
-   SQL_DATA_AT_EXEC 參數的數據將與**SQLPutData 一**起發送。 當 ODBC 1.0 應用程式呼叫 ODBC 3 時,將使用此值。*x*驅動程式。 有關詳細資訊,請參閱本節後面的"傳遞參數值"。  
  
 如果*StrLen_or_IndPtr*為空指標,則驅動程式假定所有輸入參數值為非 NULL,並且該字元和二進位數據為 null 終止。 如果*輸入輸出類型*為SQL_PARAM_OUTPUT或SQL_PARAM_OUTPUT_STREAM*參數ValuePtr*和*StrLen_or_IndPtr*均為空指標,則驅動程式將丟棄輸出值。  
  
> [!NOTE]  
>  當參數的數據類型SQL_C_BINARY時,強烈建議應用程式開發人員為*StrLen_or_IndPtr*指定空指標。 為了確保驅動程式不會意外截截SQL_C_BINARY數據 *,StrLen_or_IndPtr*應包含指向有效長度值的指標。  
  
 如果*InputOutputType*參數SQL_PARAM_INPUT_OUTPUT、SQL_PARAM_OUTPUT、SQL_PARAM_INPUT_OUTPUT_STREAM或SQL_PARAM_OUTPUT_STREAM,*則StrLen_or_IndPtr*指向驅動程式返回SQL_NULL_DATA的\*緩衝區、*可在參數ValuePtr*中返回的字節數(不包括字元數據的空端位元)或SQL_NO_TOTAL(如果無法確定可供返回的位元)。 如果過程傳回一個或多個結果集,則在提取所有結果之前,不保證設定*StrLen_or_IndPtr緩衝區*。  
  
 如果SQL_ATTR_PARAMSET_SIZE語句屬性中的值大於 1,*則StrLen_or_IndPtr*指向 SQLLEN 值陣列。 這些值可以是本節前面列出的任何值,並且使用單個 SQL 語句進行處理。  
  
## <a name="passing-parameter-values"></a>傳遞參數值

 應用程式可以在\**參數ValuePtr*緩衝區中傳遞參數的值,也可以通過對**SQLPutData**的一個或多個調用來傳遞參數的值。 其數據隨**SQLPutData**傳遞的參數稱為*執行時的數據*參數。 這些參數通常用於發送SQL_LONGVARBINARY和SQL_LONGVARCHAR參數的數據,並可以與其他參數混合。  
  
 要傳遞參數值,應用程式將執行以下步驟序列:  
  
1.  為每個參數呼叫**SQLBind 參數**以綁定參數值(*參數值Ptr*參數)和長度/指示器 *(StrLen_or_IndPtr*參數)的緩衝區。 對於執行時的資料參數,*參數ValuePtr*是應用程式定義的指標值,如參數編號或資料的指標。 該值稍後將返回,可用於標識參數。  
  
2.  在\**參數ValuePtr*與 **StrLen_or_IndPtr*緩衝區中放置輸入和輸入/輸出參數的值:  
  
    -   對於普通參數,應用程式將參數值放在\**參數ValuePtr*緩衝區中,並將該值的長度放在 **StrLen_or_IndPtr*緩衝區中。 有關詳細資訊,請參考[設定參數值](../../../odbc/reference/develop-app/setting-parameter-values.md)。  
  
    -   對於執行時的資料參數,應用程式將SQL_LEN_DATA_AT_EXEC(*長度*)宏的結果(在調用 ODBC 2.0 驅動程式時)放入 **StrLen_or_IndPtr*緩衝區中。  
  
3.  呼叫**SQLExecute**或**SQLExecDirect**以執行 SQL 語句。  
  
    -   如果沒有執行時的數據參數,該過程將完成。  
  
    -   如果存在任何執行時的數據參數,則函數將返回SQL_NEED_DATA。  
  
4.  調用**SQLParamData**檢索**SQLBind 參數***的參數 ValuePtr*參數中指定的應用程式定義值,以便處理第一個執行時的數據參數。 **SQLParamData**返回SQL_NEED_DATA。  
  
    > [!NOTE]  
    >  儘管執行時的數據參數類似於執行時的數據列,但**SQLParamData**返回的值因每個參數而異。 執行時的資料參數是 SQL 語句中的參數,當使用**SQLExecDirect**或**SQLExecute**執行敘述時,將隨**SQLPutData**一起發送數據。 它們與**SQLBind 參數**綁定。 **SQLParamData**傳回的值是參數*ValuePtr*參數中傳遞給**SQLBind 參數**的指標值。 執行時的資料列是行集中的欄,當使用**SQLBulk 操作**更新或添加行或使用**SQLSetPos**更新行時,將隨**SQLPutData**一起發送數據。 它們與**SQLBindCol**綁定。 **SQLParamData**傳回的值是正在處理的 **TargetValuePtr*緩衝區中的行的位址(由對**SQLBindCol**的調用設置)。  
  
5.  調用**SQLPutData**一次或多次以發送參數的數據。 如果數據值大於\* **SQLPutData**中指定的*參數 ValuePtr*緩衝區,則需要多個調用。僅當將字元 C 資料發送到具有字元、二進位或資料來源特定資料類型的列或將二進位C資料發送到具有字元、二進位或資料來源特定資料類型的列時,才允許對同一參數的**SQLPutData**進行多次調用。  
  
6.  再次調用**SQLParamData**以發出已為參數發送所有數據的信號。  
  
    -   如果有更多的執行資料參數 **,SQLParamData**將返回SQL_NEED_DATA和應用程式定義的值,以便處理下一個執行時的數據參數。 應用程式重複步驟 4 和 5。  
  
    -   如果沒有更多的數據執行參數,該過程就完成了。 如果語句成功執行 **,SQLParamData**將返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO;如果執行失敗,它將返回SQL_ERROR。 此時 **,SQLParamData**可以返回任何 SQLSTATE,該 SQLSTATE 可以由用於執行語句的函數 **(SQLExecDirect**或**SQLExecute)** 傳回。  
  
         在應用程式檢索語句生成的所有結果集後,\**參數ValuePtr*和 **StrLen_or_IndPtr*緩衝區中提供了任何輸入/輸出參數的輸出值。  
  
 呼叫**SQLExecute**或**SQLExecDirect**將語句置於SQL_NEED_DATA狀態。 此時,應用程式只能調用 SQLCancel、SQLGetDiagField、SQLGetDiagRec、SQLGet**函數****、SQLParamData**或**SQLPutData**與語句或與語句**SQLCancel****SQLGetDiagField****SQLGetDiagRec**關聯的*連接句柄*。 如果調用具有語句或與 語句關聯的連接的任何其他函數,則函數將返回 SQLSTATE HY010(函數序列錯誤)。 當**SQLParamData**或**SQLPutData**傳回錯誤 **、SQLParamData**傳回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO或取消該語句時,該語句將保留SQL_NEED_DATA狀態。  
  
 如果應用程式調用**SQLCancel,** 而驅動程式仍然需要執行時的數據參數,則驅動程式將取消語句執行;如果驅動程式仍需要執行時的數據,則驅動程式將取消語句執行。然後,應用程式可以再次調用**SQLExecute**或**SQLExecDirect。**  
  
## <a name="retrieving-streamed-output-parameters"></a>檢索流輸出參數

 當應用程式將*InputOutputType*集到SQL_PARAM_INPUT_OUTPUT_STREAM或SQL_PARAM_OUTPUT_STREAM時,輸出參數值必須通過對**SQLGetData**的一個或多個調用來檢索。 當驅動程式具有要傳回到應用程式的流輸出參數值時,它將傳回SQL_PARAM_DATA_AVAILABLE以回應對以下函數的呼叫 **:SQLMore 結果****、SQLExecute**和**SQLExecDirect**。 應用程式呼叫**SQLParamData**以確定可用的參數值。  
  
 有關SQL_PARAM_DATA_AVAILABLE和串流式輸出參數的詳細資訊,請參閱使用[SQLGetData 偵測參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)。  
  
## <a name="using-arrays-of-parameters"></a>使用參數陣列

 當應用程式準備一個包含參數標記的語句並在參數陣列中傳遞時,可以執行兩種不同的方法。 一種方法是驅動程式依賴於後端的陣列處理功能,在這種情況下,包含參數陣列的整個語句被視為一個原子單元。 Oracle 是支援陣列處理功能的數據源的範例。 實現此功能的另一種方法是驅動程式生成一批 SQL 語句,為參數陣列中每組參數生成一個 SQL 語句,並執行批處理。 參數陣列不能與**更新 WHERE"當前語句**"一起使用。  
  
 處理參數陣列時,單個結果集/行計數(每個參數集一個)可用,或者結果集/行計數可以匯總為一個。 **SQLGetInfo**中的SQL_PARAM_ARRAY_ROW_COUNTS選項指示行計數是可用於每組參數(SQL_PARC_BATCH)還是只有一個行計數可用(SQL_PARC_NO_BATCH)。  
  
 **SQLGetInfo**中的SQL_PARAM_ARRAY_SELECTS選項指示結果集是可用於每組參數(SQL_PAS_BATCH),還是只有一個結果集可用(SQL_PAS_NO_BATCH)。 如果驅動程式不允許使用參數陣列執行結果集生成語句,SQL_PARAM_ARRAY_SELECTS返回SQL_PAS_NO_SELECT。  
  
 有關詳細資訊,請參閱[SQLGetInfo 函數](../../../odbc/reference/syntax/sqlgetinfo-function.md)。  
  
 為了支援參數陣列,SQL_ATTR_PARAMSET_SIZE語句屬性設置為指定每個參數的值數。 如果欄位大於 1,則 APD 的SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR欄位必須指向陣列。 每個陣列的基數等於SQL_ATTR_PARAMSET_SIZE的值。  
  
 APD 的SQL_DESC_ROWS_PROCESSED_PTR欄位指向包含已處理的參數集數(包括錯誤集)的緩衝區。 處理每組參數時,驅動程式在緩衝區中存儲一個新值。 如果這是空指標,則不會返回任何數位。 使用參數陣列時,即使設置函數返回SQL_ERROR,也會填充 APD SQL_DESC_ROWS_PROCESSED_PTR 欄位指向的值。 如果返回SQL_NEED_DATA,則 APD 的SQL_DESC_ROWS_PROCESSED_PTR欄位指向的值將設置為正在處理的參數集。  
  
 綁定參數陣列並執行**更新 WHERE CURRENT 語句**時發生的情況是驅動程式定義的。  
  
## <a name="column-wise-parameter-binding"></a>列-威斯參數繫結

 在按列綁定中,應用程式將單獨的參數和長度/指標陣列綁定到每個參數。  
  
 要使用按列綁定,應用程式首先將SQL_ATTR_PARAM_BIND_TYPE語句屬性設置為SQL_PARAM_BIND_BY_COLUMN。 (這是預設值。對於要綁定的每個列,應用程式執行以下步驟:  
  
1.  分配參數緩衝區陣組。  
  
2.  分配長度/指示器緩衝區的陣列。  
  
    > [!NOTE]  
    >  如果使用按列綁定時應用程式直接寫入描述符,則可以將單獨的陣列用於長度和指標數據。  
  
3.  使用以下參數呼叫**SQLBind 參數**:  
  
    -   *ValueType*是參數緩衝區陣列中單個元素的 C 類型。  
  
    -   *參數類型*是參數的 SQL 類型。  
  
    -   *參數ValuePtr*是參數緩衝區陣列的位址。  
  
    -   *緩衝區長度*是參數緩衝區陣列中單個元素的大小。 當數據為固定長度數據時,將忽略*BufferLength*參數。  
  
    -   *StrLen_or_IndPtr*長度/指示器陣列的位址。  
  
 有關如何使用此資訊的詳細資訊,請參閱本節後面的"註釋"中的"參數值驅動器"。 有關參數的按列綁定的詳細資訊,請參閱[參數的綁定陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="row-wise-parameter-binding"></a>行-威斯參數綁定

 在按行綁定中,應用程式定義一個結構,該結構包含要綁定的每個參數的參數和長度/指示器緩衝區。  
  
 要使用行綁定,應用程式將執行以下步驟:  
  
1.  定義一個結構來容納一組參數(包括參數和長度/指標緩衝區),並分配這些結構的陣列。  
  
    > [!NOTE]  
    >  如果使用按行綁定時應用程式直接寫入描述符,則可以將單獨的欄位用於長度和指標數據。  
  
2.  將SQL_ATTR_PARAM_BIND_TYPE語句屬性設置為包含單個參數集的結構大小,或將參數綁定到的緩衝區實例的大小。 長度必須包括所有綁定參數的空間以及結構或緩衝區的任何填充,以確保當綁定參數的位址以指定長度遞增時,結果將指向下一行中同一參數的開頭。 當您在 ANSI C 中使用*大小運算符*時,此行為是有保證的。  
  
3.  呼叫**SQLBind 參數**,對要綁定的每個參數進行以下參數:  
  
    -   *ValueType*是要綁定到列的參數緩衝區成員的類型。  
  
    -   *參數類型*是參數的 SQL 類型。  
  
    -   *參數ValuePtr*是第一個陣列元素中的參數緩衝區成員的位址。  
  
    -   *緩衝區長度*是參數緩衝區成員的大小。  
  
    -   *StrLen_or_IndPtr*是要綁定的長度/指示器成員的位址。  
  
 有關如何使用此資訊的詳細資訊,請參閱本節後面的"*參數值驅動器*"。 有關參數列綁的詳細資訊,請參閱[參數的綁定陣列](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)。  
  
## <a name="error-information"></a>錯誤資訊

 如果驅動程式未將參數陣列實現為批處理(SQL_PARAM_ARRAY_ROW_COUNTS 選項等於SQL_PARC_NO_BATCH),則錯誤情況將像執行一個語句一樣處理。 如果驅動程式確實將參數陣列實現為批次處理,則應用程式可以使用 IPD 的SQL_DESC_ARRAY_STATUS_PTR標頭欄位來確定 SQL 語句的哪個參數或參數陣列中的哪個參數導致**SQLExecDirect**或**SQLExecute**傳回錯誤。 此欄位包含每行參數值的狀態資訊。 如果欄位指示已發生錯誤,則診斷數據結構中的欄位將指示失敗的參數的行和參數編號。 陣列中的元素數將由 APD 中的SQL_DESC_ARRAY_SIZE標頭欄位定義,該欄位可以由SQL_ATTR_PARAMSET_SIZE語句屬性設置。  
  
> [!NOTE]  
>  APD 中的SQL_DESC_ARRAY_STATUS_PTR標頭欄位用於忽略參數。 有關忽略參數的詳細資訊,請參閱下一節"忽略一組參數"。  
  
 當 SQLExecute 或**SQLExecDirect**傳回SQL_ERROR時,IPD 中SQL_DESC_ARRAY_STATUS_PTR字段指向的陣列中的元素將包含SQL_PARAM_ERROR、SQL_PARAM_SUCCESS、SQL_PARAM_SUCCESS_WITH_INFO、SQL_PARAM_UNUSED或SQL_PARAM_DIAG_UNAVAILABLE。 **SQLExecDirect**  
  
 對於此陣列中的每個元素,診斷數據結構包含一個或多個狀態記錄。 結構的SQL_DIAG_ROW_NUMBER欄位指示導致錯誤的參數值的行號。 如果可以確定導致錯誤的參數行中的特定參數,則參數編號將在SQL_DIAG_COLUMN_NUMBER欄位中輸入。  
  
 當未使用參數時,將輸入SQL_PARAM_UNUSED,因為早期參數中發生錯誤,迫使**SQLExecute**或**SQLExecDirect**中止。 例如,如果執行導致 SQLExecute 或**SQLExecDirect**中止的第四十個參數集時出現**SQLExecDirect**50 個參數 併發生錯誤,則在參數 41 到 50 的狀態陣列中輸入SQL_PARAM_UNUSED。  
  
 當驅動程式將參數陣組視為單片單元時,將輸入SQL_PARAM_DIAG_UNAVAILABLE,因此不會生成此單個參數級別的錯誤資訊。  
  
 處理單個參數集時出現一些錯誤會導致陣列中後續參數集的處理停止。 其他錯誤不會影響後續參數的處理。 哪些錯誤將停止處理是驅動程式定義的。 如果未停止處理,則處理陣列中的所有參數,SQL_SUCCESS_WITH_INFO由於錯誤而返回,SQL_ATTR_PARAMS_PROCESSED_PTR定義的緩衝區設置為處理的參數集總數(由SQL_ATTR_PARAMSET_SIZE語句屬性定義),其中包括錯誤集。  
  
> [!CAUTION]  
>  ODBC 處理參數陣列時發生錯誤時,ODBC行為在 ODBC 3 中是不同的。*x*比在ODBC 2中。*x*. . 在 ODBC 2 中。*x,SQL_ERROR*返回的功能,處理停止。 **SQLParamOptions** *的 pirow*參數指向的緩衝區包含錯誤行的數量。 在 ODBC 3 中。*x*,函數返回SQL_SUCCESS_WITH_INFO,處理可以停止或繼續。 如果繼續,SQL_ATTR_PARAMS_PROCESSED_PTR指定的緩衝區將設置為處理的所有參數的值,包括導致錯誤的參數的值。 這種行為更改可能會導致現有應用程序出現問題。  
  
 當 SQLExecute 或**SQLExecDirect**在完成參數陣列中所有參數集的處理之前返回時(例如返回SQL_ERROR或SQL_NEED_DATA時,狀態陣列包含已處理**SQLExecDirect**的參數的狀態。 IPD 中SQL_DESC_ROWS_PROCESSED_PTR欄位指向的位置包含參數陣列中導致SQL_ERROR或SQL_NEED_DATA錯誤代碼的行號。 當參數陣列發送到 SELECT 語句時,狀態陣列的可用性由驅動程式定義;在執行語句或提取結果集后,它們可能可用。  
  
## <a name="ignoring-a-set-of-parameters"></a>忽略一個參數

 APD 的SQL_DESC_ARRAY_STATUS_PTR欄位(由SQL_ATTR_PARAM_STATUS_PTR語句屬性設置)可用於指示應忽略 SQL 語句中的一組綁定參數。 要指示驅動程式在執行期間忽略一組或多組參數,應用程式應遵循以下步驟:  
  
1.  調用**SQLSetDescField**將 APD 的SQL_DESC_ARRAY_STATUS_PTR標頭欄位設定為指向 SQLUSMALLINT 值陣列以包含狀態資訊。 此欄位也可以通過使用 SQL_ATTR_PARAM_OPERATION_PTR 屬性呼叫**SQLSetStmtAttr**來設置,該*屬性*允許應用程式在不獲取描述符句柄的情況下設定欄位。  
  
2.  將 APD SQL_DESC_ARRAY_STATUS_PTR欄位定義的陣列的每個元素設定為兩個值之一:  
  
    -   SQL_PARAM_IGNORE,以指示該行從語句執行中排除。  
  
    -   SQL_PARAM_PROCEED,以指示該行包含在語句執行中。  
  
3.  呼叫**SQLExecDirect**或**SQLExecute**以執行準備好的語句。  
  
 以下規則適用於 APD 的SQL_DESC_ARRAY_STATUS_PTR欄位定義的陣列:  
  
-   預設情況下,指標設定為 null。  
  
-   如果指標為空,則使用所有參數集,就像所有元素都設置為SQL_ROW_PROCEED一樣。  
  
-   將元素設置為SQL_PARAM_PROCEED並不保證該操作將使用該特定參數集。  
  
-   SQL_PARAM_PROCEED在標頭檔中定義為 0。  
  
 應用程式可以將 APD 中的SQL_DESC_ARRAY_STATUS_PTR欄位設定為指向與 IRD 中SQL_DESC_ARRAY_STATUS_PTR欄位指向的陣列相同的陣列。 當將參數綁定到行數據時,這非常有用。 然後,可以根據行數據的狀態忽略參數。 除了SQL_PARAM_IGNORE之外,以下代碼還會導致忽略 SQL 語句中的參數:SQL_ROW_DELETED、SQL_ROW_UPDATED和SQL_ROW_ERROR。 除了SQL_PARAM_PROCEED,以下代碼還會導致 SQL 語句繼續:SQL_ROW_SUCCESS、SQL_ROW_SUCCESS_WITH_INFO和SQL_ROW_ADDED。  
  
## <a name="rebinding-parameters"></a>重新繫結參數

 應用程式可以執行兩個操作中的任何一個來更改繫結:  
  
-   呼叫**SQLBind 參數**為已綁定的列指定新的綁定。 驅動程式用新綁定覆蓋舊綁定。  
  
-   指定要添加到由綁定調用**SQLBind 參數**指定的緩衝區位址的偏移量。 有關詳細資訊,請參閱下一節"使用偏移重新綁定"。  
  
## <a name="rebinding-with-offsets"></a>使用位移重新繫結

 當應用程式具有可以包含許多參數的緩衝區設置,但調用**SQLExecDirect**或**SQLExecute**僅使用少數參數時,參數的重新綁定特別有用。 緩衝區中的剩餘空間可以通過偏移量修改現有綁定來用於下一組參數。  
  
 APD 中的SQL_DESC_BIND_OFFSET_PTR標頭欄位指向綁定偏移量。 如果該欄位為非空,則驅動程式將引用指標,如果SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR欄位中沒有任何值是空指標,則在執行時將已引用的值添加到描述元記錄中的這些欄位。 執行 SQL 語句時,將使用新的指標值。 重新綁定後偏移量仍然有效。 由於SQL_DESC_BIND_OFFSET_PTR是指向偏移量的指標,而不是偏移本身,因此應用程式可以直接更改偏移量,而無需調用[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或[SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)來更改描述符位。 預設情況下,指標設定為 null。 ARD 的SQL_DESC_BIND_OFFSET_PTR欄位可以通過呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)或呼叫[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)進行設定,該欄位具有 SQL_ATTR_PARAM_BIND_OFFSET_PTR*屬性*。  
  
 綁定偏移量始終直接添加到SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR和SQL_DESC_OCTET_LENGTH_PTR欄位中的值。 如果偏移更改為其他值,則新值仍直接添加到每個描述符欄位中的值。 新偏移量不會添加到欄位值和任何較早的偏移量之和中。  
  
## <a name="descriptors"></a>描述項

 參數的綁定方式由 AD 和 IpD 的欄位決定。 **SQLBind參數**中的參數用於設置這些描述符欄位。 欄位也可以由**SQLSetDescField**函數設定,儘管**SQLBind 參數**的使用效率更高,因為應用程式不必取得描述符句柄來呼叫**SQLBind 參數**。  
  
> [!CAUTION]  
>  為一個語句調用**SQLBind 參數**可能會影響其他語句。 當顯式分配與語句關聯的 ARD 並且也與其他語句關聯時,將發生這種情況。 由於**SQLBindParameter**修改 APD 的欄位,因此修改將應用於與此描述符關聯的所有語句。 如果這不是必需的行為,則應用程式應在調用**SQLBind 參數**之前將此描述符與其他語句分離。  
  
 從概念上講 **,SQLBind 參數**按順序執行以下步驟:  
  
1.  調用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以獲取 APD 句柄。  
  
2.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)取得 APD 的SQL_DESC_COUNT欄位,如果*欄數*參數的值超過SQL_DESC_COUNT的值,則呼叫**SQLSetDescField**以將SQL_DESC_COUNT的值增加到*欄號*。  
  
3.  多次呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)將值配置給 APD 的以下欄位:  
  
    -   將SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE*的值設置為 ValueType,* 但除非*ValueType*是日期時間或間隔子類型的簡潔標識符之一,則它將SQL_DESC_TYPE分別設置為SQL_DATETIME或SQL_INTERVAL,將SQL_DESC_CONCISE_TYPE設置為簡潔標識符,並將SQL_DESC_DATETIME_INTERVAL_CODE設置為相應的日期時間或間隔子代碼。  
  
    -   將SQL_DESC_OCTET_LENGTH欄位設置為*緩衝區長度*的值。  
  
    -   將SQL_DESC_DATA_PTR欄位設定為*參數值*的值。  
  
    -   將SQL_DESC_OCTET_LENGTH_PTR欄位設置為*StrLen_or_Ind*的值。  
  
    -   將SQL_DESC_INDICATOR_PTR欄位也設置為*StrLen_or_Ind*的值。  
  
     *StrLen_or_Ind*參數指定指標資訊和參數值的長度。  
  
4.  調用[SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)以獲取 IPD 句柄。  
  
5.  呼叫[SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)取得 IPD 的SQL_DESC_COUNT欄位,如果*列號*參數的值超過SQL_DESC_COUNT的值,則呼叫**SQLSetDescField**將SQL_DESC_COUNT的值增加到*欄號*。  
  
6.  多次呼叫[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)將值配置給 IPD 的以下欄位:  
  
    -   將參數*類型*的值集SQL_DESC_TYPE和SQL_DESC_CONCISE_TYPE,但參數*類型*是日期時間或間隔子類型的簡潔標識符之一,則SQL_DESC_TYPE設置為SQL_DATETIME或SQL_INTERVAL,分別將SQL_DESC_CONCISE_TYPE設置為簡潔標識符,並將SQL_DESC_DATETIME_INTERVAL_CODE設置為相應的日期時間或間隔子代碼。  
  
    -   設定一個或多個SQL_DESC_LENGTH、SQL_DESC_PRECISION和SQL_DESC_DATETIME_INTERVAL_PRECISION,適用於*參數類型*。  
  
    -   SQL_DESC_SCALE將「*小數位數」* 的值設置。  
  
 如果對**SQLBind 參數**的呼叫失敗,它將在 APD 中設置的描述符位的內容未定義,並且 APD 的SQL_DESC_COUNT欄位保持不變。 此外,IPD 中相應記錄SQL_DESC_LENGTH、SQL_DESC_PRECISION、SQL_DESC_SCALE和SQL_DESC_TYPE欄位未定義,IPD 的SQL_DESC_COUNT欄位保持不變。  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>轉換來電到與從 SQLSetParam

 當 ODBC 1.0 應用程式在 ODBC 3 中呼叫**SQLSetParam**時。*x*驅動程式,ODBC 3。*x*驅動程式管理器映射調用,如下表所示。  
  
|ODBC 1.0 應用程式通話|致電ODBC 3。*x*驅動程式|  
|----------------------------------|-------------------------------|  
|SQLSetParam(語句處理、參數編號、值類型、參數類型、長度精度、參數刻度、參數值Ptr、StrLen_or_IndPtr);|SQLBind參數(語句句柄、參數編號、SQL_PARAM_INPUT_OUTPUT、值類型、參數類型、*列大小*、*十進位數字*、參數值Ptr、SQL_SETPARAM_VALUE_MAX、StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>程式碼範例  
 在下面的範例中,應用程式準備一個 SQL 語句將數據插入到 ORDERS 表中。 對於語句中的每個參數,應用程式呼叫**SQLBindparameter**來指定參數的 ODBC C 資料類型和 SQL 資料類型,並將緩衝區綁定到每個參數。 對於每行數據,應用程式為每個參數分配數據值,並調用**SQLExecute**執行語句。  
  
 以下範例假定您的電腦上具有與北風資料庫關聯的稱為北風的ODBC資料源。  
  
 有關更多程式碼範例,請參閱[SQLBulk 操作函數](../../../odbc/reference/syntax/sqlbulkoperations-function.md)[、SQL 程式函數](../../../odbc/reference/syntax/sqlprocedures-function.md)[、SQLPutData 函數](../../../odbc/reference/syntax/sqlputdata-function.md)與[SQLSetPos 函數](../../../odbc/reference/syntax/sqlsetpos-function.md)。  
  
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

 在下面的範例中,應用程式使用命名參數執行 SQL Server 儲存過程。  
  
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
|傳回敘述中有關參數的資訊|[SQLDescribeParam 函數](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|在敘述上釋放參數緩衝區|[SQLFreeStmt 函式](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|傳回敘述參數|[SQLNumParams 函式](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|傳回下一個參數以送出資料|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|指定多個參數值|[SQLParamOptions 函式](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|在執行時傳送參數資料|[SQLPutData 函式](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>另請參閱

 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標題檔案](../../../odbc/reference/install/odbc-header-files.md)   
 [使用 SQLGetData 擷取輸出參數](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
