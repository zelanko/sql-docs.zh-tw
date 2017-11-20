---
title: "SQLPutData 函數 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLPutData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLPutData
helpviewer_keywords:
- SQLPutData function [ODBC]
ms.assetid: 9a60f004-1477-4c54-a20c-7378e1116713
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fac078be865e13dc2a216c8c0610d15be0b2e373
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="sqlputdata-function"></a>SQLPutData 函數
**一致性**  
 版本引進了： ODBC 1.0 標準相容性： ISO 92  
  
 **摘要**  
 **SQLPutData**允許將參數或資料行的資料傳送到在陳述式執行階段的驅動程式的應用程式。 此函式可以用於組件中的字元或二進位資料值傳送至具有字元、 二進位、 或資料來源專用的資料類型 （例如，SQL_LONGVARBINARY 或 SQL_LONGVARCHAR 類型的參數） 的資料行。 **SQLPutData**支援 Unicode C 資料型別，繫結，即使基礎驅動程式不支援 Unicode 資料。  
  
## <a name="syntax"></a>語法  
  
```  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 [輸入]陳述式控制代碼。  
  
 *DataPtr*  
 [輸入]包含參數或資料行的實際資料之緩衝區的指標。 資料必須在中指定的 C 資料類型*ValueType*引數的**SQLBindParameter** （適用於參數的資料） 或*TargetType*引數的**SQLBindCol** （適用於資料行的資料）。  
  
 *StrLen_or_Ind*  
 [輸入]長度\* *DataPtr*。 指定的呼叫中傳送的資料數量**SQLPutData**。 資料量可能會隨每次呼叫指定的參數或資料行。 *StrLen_or_Ind*會被忽略，除非它符合下列條件的其中一項：  
  
-   *StrLen_or_Ind*是 SQL_NTS、 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM。  
  
-   中指定的 C 資料類型**SQLBindParameter**或**SQLBindCol** SQL_C_CHAR 或 SQL_C_BINARY。  
  
-   C 資料類型為 SQL_C_DEFAULT，而且指定的 SQL 資料類型的預設 C 資料類型為 SQL_C_CHAR 或 SQL_C_BINARY。  
  
 對於所有其他類型的 C 資料如果*StrLen_or_Ind* SQL_NULL_DATA 或 SQL_DEFAULT_PARAM，不是驅動程式假設大小\* *DataPtr*緩衝區是指定的 C 資料類型的大小與*ValueType*或*TargetType*並傳送整個資料值。 如需詳細資訊，請參閱[轉換資料從 C 到 SQL 資料型別](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附錄 d： 資料型別中。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLPutData**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值可以藉由呼叫取得**SQLGetDiagRec**與*HandleType* SQL_ 的HANDLE_STMT 和*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLPutData** ，並說明這個函式; 每個內容中的標記法 」 (DM) 」 之前描述的驅動程式管理員傳回的 Sqlstate。 每個 SQLSTATE 值相關聯的傳回碼是 SQL_ERROR，除非有說明，否則為。  
  
|SQLSTATE|錯誤|Description|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定驅動程式告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊遭截斷|字串或二進位資料傳回輸出參數會導致非空白的字元或二進位資料為非 NULL 的截斷。 如果是字串值，它就是向右截斷。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|所識別的資料值*ValueType*引數中的**SQLBindParameter**繫結的參數無法轉換成資料類型所識別的*ParameterType*引數中的**SQLBindParameter**。|  
|07S01|無效的預設參數使用|參數值時，設定與**SQLBindParameter**、 已 SQL_DEFAULT_PARAM，和對應的參數沒有預設值。|  
|08S01|通訊連結失敗|功能已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22001|字串資料，右側截斷|字元或二進位值的資料行的指派會導致非空白 （字元） 或非 null （二進位） 字元或位元組的截斷。<br /><br /> SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo** "Y"，且於指定傳送更多資料 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型） 的長度參數與*StrLen_or_IndPtr*引數中的**SQLBindParameter**。<br /><br /> SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo**已"Y"，以及多個傳送的資料 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特定的資料類型） 的長資料行中指定了非對應至已加入或更新的資料列中的資料行長度的緩衝區**SQLBulkOperations**或更新與**SQLSetPos**。|  
|22003|數值超出範圍|將資料傳送的繫結的數值參數或資料行導致要指派給相關聯的資料表資料行時會被截斷的數字 （相對於小數） 的整數部分。<br /><br /> 傳回一或多個輸入/輸出或輸出參數的數值 （以數字或字串） 可能已造成要截斷的數字 （相對於小數） 的整數部分。|  
|22007|無效的 datetime 格式|傳送參數或資料行已繫結到日期、 時間或時間戳記結構的資料是，分別無效的日期、 時間戳記。<br /><br /> 輸入/輸出或輸出參數已繫結至日期、 時間或時間戳記 C 結構，但傳回的參數中的值，分別無效的日期、 時間戳記。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22008|日期時間欄位溢位|日期時間運算式計算的輸入/輸出或輸出參數會導致日期、 時間或時間戳記 C 結構無效。|  
|22012|除數為零|輸出參數的除法中產生除以零或算術運算式計算的輸入/輸出。|  
|22015|間隔欄位溢位|將資料傳送的精確數值或時間間隔資料行或參數間隔 SQL 資料類型造成的有效位數遺失。<br /><br /> 資料傳送時，為間隔的資料行或參數與一個以上的欄位、 已轉換成數值資料類型，及沒有表示在數值資料類型。<br /><br /> 將資料傳送的資料行或參數資料已指派的間隔 SQL 類型，而且時發生 SQL 類型的間隔內沒有表示的 C 類型的值。<br /><br /> 傳送的精確數值或間隔 C 資料行或參數間隔 C 類型的資料造成有效位數的遺失。<br /><br /> 將資料傳送的資料行或參數資料已指派給間隔 C 結構，而且時發生間隔資料結構中的資料沒有表示法。|  
|22018|轉換規格的字元值無效|C 類型為精確或大約的數字、 日期時間或間隔資料類型。資料行的 SQL 類型是字元資料類型。和資料行或參數中的值不是有效的常值的繫結 C 類型。<br /><br /> SQL 類型為精確或大約的數字、 日期時間或間隔資料類型。C 類型已 SQL_C_CHAR;和資料行或參數中的值不是有效的常值的繫結的 SQL 型別。|  
|HY000|一般錯誤|發生錯誤，其中沒有任何特定的 SQLSTATE 和定義沒有實作特定的 SQLSTATE。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成的函式。|  
|HY008|已取消操作|非同步處理已啟用*StatementHandle*。 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*。 上一次呼叫函式則*StatementHandle*。<br /><br /> 呼叫此函式，和之前已完成執行， **SQLCancel**或**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|無效的 null 指標使用|(DM) 引數*DataPtr* null 指標，以及引數*StrLen_or_Ind*不是 0，SQL_DEFAULT_PARAM 或 SQL_NULL_DATA。|  
|HY010|函數順序錯誤|(DM) 先前的函式呼叫不是呼叫**SQLPutData**或**SQLParamData**。<br /><br /> (DM) 非同步執行的函式呼叫相關聯的連接控制代碼的*StatementHandle*。 仍在 SQLPutData 函式呼叫時執行這個非同步函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可以使用。 此函式呼叫之前的所有資料流處理的參數擷取資料。<br /><br /> 以非同步方式執行的函式 （不是這一個） 已呼叫 (DM) *StatementHandle*和還在執行時呼叫此函式。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足。|  
|HY019|非字元與非二進位資料分割傳送|**SQLPutData**已呼叫超過一次以上的參數或資料行，以及它已不在使用 C 字元資料傳送至字元、 二進位、 或資料來源特定的資料類型資料行，或傳送二進位 C 資料行的字元二進位檔或資料來源特定的資料類型。|  
|HY020|嘗試串連 null 值|**SQLPutData**呼叫傳回 SQL_NEED_DATA，因為和其中一個這些呼叫中，多次呼叫*StrLen_or_Ind* SQL_NULL_DATA 或 SQL_DEFAULT_PARAM，包含引數。|  
|HY090|字串或緩衝區長度無效|引數*DataPtr* null 指標，以及引數不是*StrLen_or_Ind*小於 0，但不是等於 SQL_NTS 或是 SQL_NULL_DATA。|  
|HY117|連接已暫止原因未知的交易狀態。 只有中斷連線，並允許唯讀函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限過期之前對要求回應資料來源。 連接逾時期限透過設定**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|中的非同步通知模式已停用輪詢|每當通知模型使用時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，且如果已啟用通知模式， **SQLCompleteAsync**必須在後續處理作業，並完成此作業的控制代碼上呼叫。|  
  
 如果**SQLPutData**呼叫時傳送的 SQL 陳述式參數的資料，它會傳回任何可執行陳述式所呼叫的函式所傳回的 SQLSTATE (**SQLExecute**或**SQLExecDirect**)。 如果傳送的資料行的資料時呼叫正在更新或加入**SQLBulkOperations**或更新**SQLSetPos**，它會傳回任何可傳回的 SQLSTATE **SQLBulkOperations**或**SQLSetPos**。  
  
## <a name="comments"></a>註解  
 **SQLPutData**提供兩種用途的資料在執行資料，可以呼叫： 要使用的呼叫中的參數資料**SQLExecute**或**SQLExecDirect**，或要使用的資料列時的資料行資料更新或加入呼叫**SQLBulkOperations**或更新由呼叫**SQLSetPos**。  
  
 當應用程式呼叫**SQLParamData**來判斷哪些資料傳送，驅動程式會傳回應用程式可以用來決定要傳送的參數資料，或可以找到資料行的資料指標。 它也會傳回 SQL_NEED_DATA，這是應用程式，則它應該呼叫的指標**SQLPutData**傳送資料。 在*DataPtr*引數**SQLPutData**，應用程式會在包含參數或資料行的實際資料的緩衝區中傳遞的指標。  
  
 當驅動程式傳回 SQL_SUCCESS，如**SQLPutData**，應用程式會呼叫**SQLParamData**一次。 **SQLParamData**傳回 SQL_NEED_DATA 更多資料需要傳送，如果在此情況下執行的應用程式呼叫**SQLPutData**一次。 如果已傳送所有資料在執行資料，則會傳回 SQL_SUCCESS。 接著，應用程式呼叫**SQLParamData**一次。 如果驅動程式會傳回 SQL_NEED_DATA 和中的另一個指標 *\*ValuePtrPtr*，它需要另一個參數或資料行的資料和**SQLPutData**會再次呼叫。 如果驅動程式傳回 SQL_SUCCESS，然後所有資料在執行資料傳送，而且可以執行的 SQL 陳述式或**SQLBulkOperations**或**SQLSetPos**可以處理呼叫。  
  
 在陳述式執行階段傳遞如何資料在執行參數資料的詳細資訊，請參閱 < 傳遞參數值 > 中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)和[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。 更新或加入如何資料在執行資料行資料的詳細資訊，請參閱 「 使用 SQLSetPos 」 一節中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)，「 執行大量更新使用中的書籤" [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，和[Long 資料和 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  應用程式可以使用**SQLPutData**傳送部分或傳送字元 C 資料行的字元、 二進位、 或資料來源特定的資料型別時，才傳送二進位 C 資料行的二進位字元時的資料特定來源的資料類型。 如果**SQLPutData**會呼叫超過一次在其他情況下會傳回 SQL_ERROR 並 SQLSTATE HY019 （非字元與非二進位資料分割傳送）。  
  
## <a name="example"></a>範例  
 下列範例假設名為 Test 的資料來源名稱。 相關聯的資料庫都應該有的資料表，您可以建立，方式如下：  
  
```  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```  
// SQLPutData.cpp  
// compile with: odbc32.lib user32.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
#define TEXTSIZE  12000  
#define MAXBUFLEN 256  
  
SQLHENV henv = SQL_NULL_HENV;  
SQLHDBC hdbc1 = SQL_NULL_HDBC;       
SQLHSTMT hstmt1 = SQL_NULL_HSTMT;  
  
void Cleanup() {  
   if (hstmt1 != SQL_NULL_HSTMT)  
      SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
  
   // SQLBindParameter variables.  
   SQLLEN cbTextSize, lbytes;  
  
   // SQLParamData variable.  
   PTR pParmID;  
  
   // SQLPutData variables.  
   UCHAR  Data[] =   
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyz"  
      "abcdefghijklmnopqrstuvwxyz";  
  
   SDWORD cbBatch = (SDWORD)sizeof(Data) - 1;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security, create SQL Server DSN using Windows NT authentication.   
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"",SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Allocate statement handle.  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLAllocHandle(hstmt1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Set parameters based on total data to send.  
   lbytes = (SDWORD)TEXTSIZE;  
   cbTextSize = SQL_LEN_DATA_AT_EXEC(lbytes);  
  
   // Bind the parameter marker.  
   retcode = SQLBindParameter (hstmt1,           // hstmt  
                               1,                // ipar  
                               SQL_PARAM_INPUT,  // fParamType  
                               SQL_C_CHAR,       // fCType  
                               SQL_LONGVARCHAR,  // FSqlType  
                               lbytes,           // cbColDef  
                               0,                // ibScale  
                               (VOID *)1,        // rgbValue  
                               0,                // cbValueMax  
                               &cbTextSize);     // pcbValue  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLBindParameter Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the command.  
   retcode =   
      SQLExecDirect(hstmt1, (UCHAR*)"INSERT INTO emp4 VALUES('Paul Borm', 46,'1950-11-12 00:00:00', ?)", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_NEED_DATA) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLExecDirect Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Check to see if NEED_DATA; if yes, use SQLPutData.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if (retcode == SQL_NEED_DATA) {  
      while (lbytes > cbBatch) {  
         SQLPutData(hstmt1, Data, cbBatch);  
         lbytes -= cbBatch;  
      }  
      // Put final batch.  
      retcode = SQLPutData(hstmt1, Data, lbytes);   
   }  
  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Make final SQLParamData call.  
   retcode = SQLParamData(hstmt1, &pParmID);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("Final SQLParamData Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Clean up.  
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
```  
  
## <a name="related-functions"></a>相關函數  
  
|如需詳細資訊|請參閱|  
|---------------------------|---------|  
|繫結至參數的緩衝區|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消陳述式處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 陳述式|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 陳述式|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回將資料傳送下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC 應用程式開發介面參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)

