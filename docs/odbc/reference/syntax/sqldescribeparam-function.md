---
title: "SQLDescribeParam 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3fe2d46f0a8e27b6e20673fc04615598469bc9aa
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ODBC  
  
 **摘要**  
 **SQLDescribeParam**傳回已備妥的 SQL 陳述式相關聯的參數標記的描述。 這項資訊也會在 IPD 欄位中提供。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *Sqlbindparameter*  
 [輸入]參數標記編號排序循序遞增的參數順序，從 1 開始。  
  
 *DataTypePtr*  
 [輸出]這是要傳回參數的 SQL 資料類型的緩衝區指標。 這個值是讀取自 IPD SQL_DESC_CONCISE_TYPE 記錄欄位。 這會是中值的其中一個[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d： 資料類型或驅動程式專屬 SQL 資料類型的區段。  
  
 在 ODBC 3。*x*中,，則會傳回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP * \*DataTypePtr*的日期、 時間或時間戳記資料分別; 在 ODBC 2。*x*，將傳回 SQL_DATE、 SQL_TIME、 或 SQL_TIMESTAMP。 驅動程式管理員會執行必要的對應時 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式或 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式。  
  
 當*ColumnNumber*等於中為 0 （適用於的書籤資料行），傳回 SQL_BINARY * \*DataTypePtr*可變長度的書籤。 （如果書籤由 ODBC 3，會傳回 SQL_INTEGER。*x*應用程式使用 ODBC 2。*x*驅動程式或 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式。)  
  
 如需詳細資訊，請參閱[SQL 資料型別](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d： 資料型別中。 如需驅動程式特有的 SQL 資料類型資訊，請參閱驅動程式的文件。  
  
 *ParameterSizePtr*  
 [輸出]這是要傳回以字元為單位的資料行或運算式的對應參數標記的大小，資料來源所定義的緩衝區指標。 如需資料行大小的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *DecimalDigitsPtr*  
 [輸出]這是要傳回的資料行的小數位數或對應參數的運算式數目所定義的資料來源中的緩衝區指標。 如需十進位數字的詳細資訊，請參閱[資料行大小、 十進位數字、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *NullablePtr*  
 [輸出]傳回值，指出參數是否允許 NULL 值的緩衝區指標。 這個值是讀取自 IPD 的 SQL_DESC_NULLABLE 欄位。 它有下列幾種：  
  
-   SQL_NO_NULLS： 參數不允許 NULL 值 （這是預設值）。  
  
-   SQL_NULLABLE： 參數允許 NULL 值。  
  
-   SQL_NULLABLE_UNKNOWN： 驅動程式無法判斷參數是否允許 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeParam**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType*的利用 SQL_HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDescribeParam** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|無效的描述元索引|(DM) 指定的引數的值*Sqlbindparameter*小於 1。<br /><br /> 指定的引數的值*Sqlbindparameter*大於中相關聯的 SQL 陳述式的參數數目。<br /><br /> 參數標記為非 DML 陳述式的一部分。<br /><br /> 參數標記是一部分**選取**清單。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|21S01|插入值清單與資料行清單不符|中的參數數目**插入**陳述式不符合陳述式中名為資料表中的資料行數目。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中* \*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 呼叫函式呼叫之前**SQLPrepare**或**SQLExecDirect**如*StatementHandle*。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 此非同步函式還在執行時**SQLDescribeParam**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 參數標記會以遞增的參數順序，從 1 開始，SQL 陳述式中出現的順序編號。  
  
 **SQLDescribeParam**未傳回參數的型別 （輸入、 輸入/輸出或輸出） 的 SQL 陳述式。 除了在呼叫程序，在 SQL 陳述式中的所有參數都是輸入的參數。 若要判斷程序呼叫中的每個參數的型別，應用程式呼叫**SQLProcedureColumns**。  
  
 如需詳細資訊，請參閱[描述參數](../../../odbc/reference/develop-app/describing-parameters.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下列範例會提示使用者輸入的 SQL 陳述式，並準備該陳述式。 接下來，它會呼叫**SQLNumParams**來判斷是否包含任何參數，陳述式。 如果陳述式包含參數，它會呼叫**SQLDescribeParam**來描述這些參數和**SQLBindParameter**繫結。 最後，它會提示使用者提供的任何參數的值，並接著執行陳述式。  
  
```  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至參數的緩衝區|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備執行陳述式|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
