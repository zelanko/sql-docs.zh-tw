---
title: SQLDescribeParam 函數 |微軟文件
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be6d076ca121923a4b6769c7dad5269c3fd642ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301158"
---
# <a name="sqldescribeparam-function"></a>SQLDescribeParam 函數
**一致性**  
 版本介紹: ODBC 1.0 標準合規性: ODBC  
  
 **摘要**  
 **SQLDescribeParam**傳回與準備好的 SQL 語句關聯的參數標記的說明。 此資訊也可在IPD領域提供。  
  
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
 *語句句柄*  
 [輸入]語句句柄。  
  
 *參數編號*  
 [輸入]參數標記編號按增加參數順序順序排序,從 1 開始。  
  
 *資料類型Ptr*  
 【輸出]指向要返回參數的 SQL 資料類型的緩衝區的指標。 此值從 IPD 的SQL_DESC_CONCISE_TYPE記錄欄位中讀取。 這將是附錄[D:](../../../odbc/reference/appendixes/sql-data-types.md)資料類型或特定於驅動程式的 SQL 資料類型的 SQL 資料類型中的值之一。  
  
 在 ODBC 3 中。* *x、SQL_TYPE_DATE、SQL_TYPE_TIME或SQL_TYPE_TIMESTAMP將分別在*\*DataTypePtr*中返回日期、時間或時間戳數據;在 ODBC 2 中。* *x、SQL_DATE、SQL_TIME或SQL_TIMESTAMP將返回。 當 ODBC 2 時,驅動程式管理員執行所需的映射。*x*應用程式使用 ODBC 3。*x*驅動程式或當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式。  
  
 當*列數*等於 0(對於書籤列),SQL_BINARY在*\*DataTypePtr*中返回,用於可變長度書籤。 (如果 ODBC 3 使用書籤,則返回SQL_INTEGER。*x*應用程式使用 ODBC 2。*x*驅動程式或 ODBC 2。*x*使用 ODBC 3 的應用程式。*x*驅動程式。  
  
 有關詳細資訊,請參閱附錄 D 中的[SQL 資料類型](../../../odbc/reference/appendixes/sql-data-types.md):數據類型。 有關特定於驅動程式的 SQL 資料類型的資訊,請參閱驅動程式的文檔。  
  
 *參數SizePtr*  
 【輸出]指向緩衝區的指標,其中用於返回數據源定義的相應參數標記的列或表達式的大小(以字元表示)。 關於列大小的詳細資訊,請參閱[欄大小、十進位數字、傳輸八點長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *十進位數字Ptr*  
 【輸出]指向緩衝區的指標,其中用於返回數據源定義的列或相應參數的表達式的十進位數字數。 有關十進位數字的詳細資訊,請參閱[列大小、十進位數字、傳輸八進制長度和顯示大小](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)。  
  
 *空可點*  
 【輸出]指向緩衝區的指標,其中要返回指示參數是否允許 NULL 值的值。 此值從 IPD 的SQL_DESC_NULLABLE欄位中讀取。 下列其中之一：  
  
-   SQL_NO_NULLS:參數不允許 NULL 值(這是預設值)。  
  
-   SQL_NULLABLE:參數允許 NULL 值。  
  
-   SQL_NULLABLE_UNKNOWN:驅動程式無法確定參數是否允許 NULL 值。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLDescribeParam**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有*Handle*SQL_HANDLE_STMT的*句柄類型*和*語句句柄*。 下表列出了**SQLDescribeParam**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07009|不合法的描述符索引|(DM) 為參數*參數編號*指定的值小於 1。<br /><br /> 為參數*參數編號*指定的值大於關聯的 SQL 語句中的參數數。<br /><br /> 參數標記是非 DML 語句的一部分。<br /><br /> 參數標記是**SELECT**清單的一部分。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|21S01|插入值清單與列清單不匹配|**INSERT**語句中的參數數與語句中命名的表中的列數不匹配。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY010|函式序列錯誤|(DM) 在調用**SQLPrepare**或**SQLExecDirect**進行*語句句柄*之前調用了函數。<br /><br /> (DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 呼叫**SQLDescribeParam**函數時,此異步函數仍在執行。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。<br /><br /> (DM) SQLExecute、SQLExecDirect、SQLBulk**操作**或**SQLSetPos**被調用用於**SQLExecute***語句句柄*並返回SQL_NEED_DATA。 **SQLExecDirect** 在發送所有執行時數據參數或列的數據之前,調用了此功能。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
## <a name="comments"></a>註解  
 參數標記按增加參數順序編號,以 1 開頭,按它們在 SQL 語句中顯示的順序進行編號。  
  
 **SQLDescribeParam**不會傳回 SQL 語句中參數的類型(輸入、輸入/輸出或輸出)。 除了對過程的調用中,SQL 語句中的所有參數都是輸入參數。 要確定對過程呼叫中的每個參數的類型,應用程式呼叫**SQLAE 欄**。  
  
 有關詳細資訊,請參閱[描述參數](../../../odbc/reference/develop-app/describing-parameters.md)。  
  
## <a name="code-example"></a>程式碼範例  
 下面的示例提示使用者使用 SQL 語句,然後準備該語句。 接下來,它將調用**SQLNumParams**以確定該語句是否包含任何參數。 如果語句包含參數,它將調用**SQLDescribeParam**來描述這些參數 **,SQLBind 參數**將它們綁定。 最後,它提示使用者輸入任何參數的值,然後執行語句。  
  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|準備執行敘述|[SQLPrepare 函式](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
