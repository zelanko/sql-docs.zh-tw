---
title: SQLDescribeParam 函式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e810d2e7ff3f69faea5fdcbccbb7f7ba276df48
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537619"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ODBC  
  
 **摘要**  
 **SQLDescribeParam**傳回已備妥的 SQL 陳述式相關聯的參數標記的描述。 這項資訊也會在 IPD 欄位中提供。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
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
  
 *ParameterNumber*  
 [輸入]參數的標記編號排序依序遞增的參數順序，從 1 開始。  
  
 *DataTypePtr*  
 [輸出]在其中傳回參數的 SQL 資料類型的緩衝區指標。 這個值是讀取自 SQL_DESC_CONCISE_TYPE 記錄的欄位 IPD 中。 這會在值的其中一個[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)一節的附錄 d:資料類型或驅動程式專屬的 SQL 資料型別。  
  
 在 ODBC 3。*x*中,，則會傳回 SQL_TYPE_DATE、 SQL_TYPE_TIME 或 SQL_TYPE_TIMESTAMP  *\*DataTypePtr*日期、 時間或時間戳記資料的 ODBC 2 中分別;。*x*、 SQL_DATE、 SQL_TIME、 或 SQL_TIMESTAMP 會傳回。 驅動程式管理員會執行必要的對應時的 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式或 ODBC 3。*x*應用程式正在使用的 ODBC 2。*x*驅動程式。  
  
 當*ColumnNumber*等於為 0 （表示書籤資料行中），傳回 SQL_BINARY  *\*DataTypePtr*可變長度的書籤。 （如果書籤由 ODBC 3，則傳回 SQL_INTEGER。*x*應用程式使用 ODBC 2。*x*驅動程式或 ODBC 2。*x*應用程式使用 ODBC 3。*x*驅動程式。)  
  
 如需詳細資訊，請參閱 < [SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md)附錄 d:資料類型。 如需驅動程式專用的 SQL 資料類型資訊，請參閱驅動程式的文件。  
  
 *ParameterSizePtr*  
 [輸出]若要在其中傳回的大小，以字元為單位的資料行或運算式的對應參數標記，資料來源所定義的緩衝區的指標。 如需有關資料行大小的詳細資訊，請參閱 <<c0> [ 資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *DecimalDigitsPtr*  
 [輸出]在其中傳回的資料行的小數位數或運算式的對應參數的數目，資料來源所定義之緩衝區的指標。 多個十進位數字的詳細資訊，請參閱[資料行大小、 小數位數、 傳輸八位元長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *NullablePtr*  
 [輸出]若要在其中傳回值，指出參數是否允許 NULL 值的緩衝區的指標。 這個值會從 IPD SQL_DESC_NULLABLE 欄位讀取。 它有下列幾種：  
  
-   SQL_NO_NULLS:參數不允許 NULL 值 （這是預設值）。  
  
-   SQL_NULLABLE:此參數允許 NULL 值。  
  
-   SQL_NULLABLE_UNKNOWN:驅動程式無法判斷參數是否允許 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeParam**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的利用 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLDescribeParam** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07009|描述項索引無效|(DM) 引數指定的值*Sqlbindparameter*小於 1。<br /><br /> 指定的引數的值*Sqlbindparameter*大於相關聯的 SQL 陳述式中的參數數目。<br /><br /> 參數標記為非 DML 陳述式的一部分。<br /><br /> 參數標記是一部分**選取**清單。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|21S01|插入的值清單不符合資料行清單|中的參數數目**插入**陳述式不符合陳述式中名為資料表中的資料行數目。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY010|函數順序錯誤|(DM) 呼叫的函式呼叫之前，先**SQLPrepare**或是**SQLExecDirect** for *StatementHandle*。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 此非同步函式仍在執行時**SQLDescribeParam**呼叫函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**， **SQLBulkOperations**，或**SQLSetPos**針對呼叫*StatementHandle*並傳回 SQL_NEED_DATA。 此函式呼叫之前已傳送的所有資料在執行中參數或資料行的資料。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
## <a name="comments"></a>註解  
 參數標記會以遞增的參數順序，從 1 開始，SQL 陳述式中出現的順序編號。  
  
 **SQLDescribeParam** SQL 陳述式未傳回參數的型別 （輸入、 輸入/輸出或輸出）。 除了在呼叫程序，在 SQL 陳述式中的所有參數都是輸入的參數。 若要判斷程序呼叫中的每個參數的型別，應用程式會呼叫**SQLProcedureColumns**。  
  
 如需詳細資訊，請參閱 <<c0> [ 描述參數](../../../odbc/reference/develop-app/describing-parameters.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下列範例會提示使用者輸入 SQL 陳述式，並接著準備該陳述式。 接著，它會呼叫**SQLNumParams**來判斷該陳述式是否包含任何參數。 如果陳述式包含參數，它會呼叫**SQLDescribeParam**來描述這些參數與**SQLBindParameter**來繫結它們。 最後，它會提示使用者提供任何參數的值，並接著執行陳述式。  
  
```cpp  
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
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
