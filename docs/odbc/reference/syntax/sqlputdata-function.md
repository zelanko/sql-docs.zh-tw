---
title: SQLPutData 功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7c4e704d96924942812904ea63d0e3d4fce8748e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300038"
---
# <a name="sqlputdata-function"></a>SQLPutData 函數
**一致性**  
 推出版本: ODBC 1.0 標準合規性: ISO 92  
  
 **摘要**  
 **SQLPutData**允許應用程式在語句執行時將參數或列的數據發送到驅動程式。 此函數可用於將零件中的字元或二進位資料值發送到具有字元、二進位或資料來源特定資料類型的列(例如,SQL_LONGVARBINARY或SQL_LONGVARCHAR類型的參數)。 **SQLPutData**支援繫結到 Unicode C 資料類型,即使基礎驅動程式不支援 Unicode 資料也是如此。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引數  
 *語句句柄*  
 [輸入]語句句柄。  
  
 *資料Ptr*  
 [輸入]指向包含參數或列的實際數據的緩衝區的指標。 數據必須位於**SQLBind 參數***的值類型*參數(用於參數資料)或**SQLBindCol** *的目標類型*參數(用於列數據)中指定的 C 資料類型中。  
  
 *StrLen_or_Ind*  
 [輸入]\**資料 Ptr*的長度 。 指定呼叫**SQLPutData**中傳送的資料量。 給定參數或列的每個調用都會更改數據量。 *除非滿足*以下條件之一,否則將忽略StrLen_or_Ind:  
  
-   *StrLen_or_Ind*是SQL_NTS、SQL_NULL_DATA或SQL_DEFAULT_PARAM。  
  
-   **在 SQLBind 參數**或**SQLBindCol**中指定的 C 資料類型SQL_C_CHAR或SQL_C_BINARY。  
  
-   C 資料類型SQL_C_DEFAULT,指定 SQL 資料類型的預設 C 資料類型為SQL_C_CHAR或SQL_C_BINARY。  
  
 對於所有其他類型的 C 數據,如果*StrLen_or_Ind*不是SQL_NULL_DATA或SQL_DEFAULT_PARAM,則\*驅動程式假定*DataPtr*緩衝區的大小是使用*ValueType*或*TargetType*指定的 C 資料類型的大小,並發送整個資料值。 關於詳細資訊,請參考在附錄 D:資料型態[中 將資料從 C 轉換為 SQL 資料型態](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLPutData**傳回SQL_ERROR或SQL_SUCCESS_WITH_INFO時,可以透過呼叫**SQLGetDiagRec**取得關聯的 SQLSTATE 值,該值具有SQL_HANDLE_STMT的*句柄類型*和*敘述的句**柄*。 下表列出了**SQLPutData**通常傳回的 SQLSTATE 值,並在此函數的上下文中解釋了每個值;符號"(DM)"在驅動程式管理器返回的 SQLStatEs 描述之前。 除非另有說明,否則與每個 SQLSTATE 值關聯的返回代碼將SQL_ERROR。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|特定於驅動程式的資訊消息。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|01004|字串資料,右截斷|為輸出參數返回的字串或二進位資料導致非空白字元或非 NULL 二進位資料的截斷。 如果它是一個字串值,它是右截斷的。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|07006|受限資料類型屬性衝突|綁定參數的**SQLBind 參數**中*的值類型*參數識別的資料值無法轉換為**SQLBind 參數**中的*參數類型*參數識別的資料類型。|  
|07S01|預設參數使用無效|使用**SQLBind 參數**設置的參數值SQL_DEFAULT_PARAM,並且相應的參數沒有預設值。|  
|08S01|通訊連結|在函數完成處理之前,驅動程式與驅動程式連接到的數據源之間的通信鏈路失敗。|  
|22001|字串資料,右截斷|將字元或二進位值分配給列會導致非空白(字元)或非空(二進位)字元或位元組的截斷。<br /><br /> **SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN資訊類型為"Y",對於長參數(資料類型為SQL_LONGVARCHAR、SQL_LONGVARBINARY或長資料來源特定資料類型)發送的數據比**在 SQLBind 參數**中*StrLen_or_IndPtr參數中*指定的數據多。<br /><br /> **SQLGetInfo**中的SQL_NEED_LONG_DATA_LEN資訊類型為「Y」,對於長列(數據類型為SQL_LONGVARCHAR、SQL_LONGVARBINARY或長數據來源特定資料類型)發送的數據比在長度緩衝區中指定的數據多,該長度緩衝區對應於使用**SQLBulk 操作**添加或更新或使用**SQLSetPos**更新的一行數據中的列。|  
|22003|數值超範圍|為綁定數值參數或列發送的數據導致在分配給關聯的表列時,將數位的整個部分(而不是小數)被截斷。<br /><br /> 為一個或多個輸入/輸出或輸出參數返回數值(作為數位或字串)將導致數位的整個(而不是小數)部分被截斷。|  
|22007|不合法日期時間格式|為綁定到日期、時間或時間戳結構的參數或列發送的數據分別為無效的日期、時間或時間戳。<br /><br /> 輸入/輸出或輸出參數綁定到日期、時間或時間戳 C 結構,傳回參數中的值分別為無效日期、時間或時間戳。 (函數返回SQL_SUCCESS_WITH_INFO。|  
|22008|日期時間欄位溢出|為輸入/輸出或輸出參數計算的 datetime 運算式會導致日期、時間或時間戳 C 結構無效。|  
|22012|除零|為輸入/輸出或輸出參數計算的算術表達式導致除以零。|  
|22015|間隔欄位溢出|為精確數位或間隔列或參數發送到間隔 SQL 資料類型的資料會導致重要數位丟失。<br /><br /> 發送具有多個字段的間隔列或參數的數據,轉換為數位數據類型,並且在數位數據類型中沒有表示形式。<br /><br /> 為列或參數數據發送的數據已分配給間隔 SQL 類型,並且間隔 SQL 類型中沒有 C 類型的值表示形式。<br /><br /> 為精確數位或間隔 C 列或參數發送到間隔 C 類型的資料導致重要數位遺失。<br /><br /> 為列或參數數據發送的數據分配給間隔 C 結構,並且間隔數據結構中沒有數據的表示形式。|  
|22018|強制轉換規範的不合法字元值|C 類型是精確或近似的數位、日期時間或間隔數據類型;列的 SQL 類型是字元數據類型;列或參數中的值不是綁定 C 類型的有效文本。<br /><br /> SQL 類型是精確或近似的數位、日期時間或間隔數據類型;C 類型為SQL_C_CHAR;列或參數中的值不是綁定 SQL 類型的有效文本。|  
|HY000|一般錯誤|發生一個錯誤,其中沒有特定的 SQLSTATE,並且沒有定義特定於實現的 SQLSTATE。 **SQLGetDiagRec**在*\*MessageText*緩衝區中傳回的錯誤訊息描述了錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法分配支援執行或完成函數所需的記憶體。|  
|HY008|已取消作業|非同步處理已開啟*敘述的句柄*。 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**呼叫到*敘述 。* 然後在*語句處理*上再次調用該函數。<br /><br /> 呼叫此函數,在完成執行之前 **,SQLCancel**或**SQLCancelHandle**是從多線程式中的不同線程呼叫*的敘述的句柄*。|  
|HY009|不合法的空白指標|(DM) 參數*DataPtr*是一個空指標,並且*參數StrLen_or_Ind*不是 0、SQL_DEFAULT_PARAM 或SQL_NULL_DATA。|  
|HY010|函式序列錯誤|(DM) 以前的函數調用不是對**SQLPutData**或**SQLParamData**的調用。<br /><br /> (DM) 為與*語句句柄*關聯的連接句柄調用非同步執行函數。 調用 SQLPutData 函數時,此異步函數仍在執行。<br /><br /> (DM) **SQLExecute、SQLExecDirect**或**SQLMore 結果**被調用語句**SQLExecDirect***句柄*並返回SQL_PARAM_DATA_AVAILABLE。 在檢索所有流參數的數據之前,已調用此函數。<br /><br /> (DM) 為*語句句柄*調用了非同步執行函數(不是此函數),並且在調用此函數時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函數調用,因為無法訪問基礎記憶體物件,可能是因為記憶體條件較低。|  
|HY019|分段傳送的非字元與非二進位資料|**SQLPutData**被多次調用用於參數或列,它不用於將字元 C 資料發送到具有字元、二進位或資料來源特定資料類型的欄,或將二進位C資料傳送到具有字元、二進位或資料來源特定資料類型的列。|  
|HY020|嘗試串聯空值|**SQLPutData**自返回SQL_NEED_DATA的調用以來多次調用,並在其中一個調用中 *,StrLen_or_Ind*參數包含SQL_NULL_DATA或SQL_DEFAULT_PARAM。|  
|HY090|不合法的字串或緩衝區長度|參數*DataPtr*不是空指標 *,StrLen_or_Ind*參數小於 0,但不等於SQL_NTS或SQL_NULL_DATA。|  
|HY117|由於未知事務狀態,連接掛起。 只允許斷開連接和唯讀功能。|(DM) 有關掛起狀態的詳細資訊,請參閱[SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連線逾時已過期|在數據源回應請求之前,連接超時期限已過期。 連接超時週期通過**SQLSetConnectAttr**SQL_ATTR_CONNECTION_TIMEOUT設置。|  
|IM001|驅動程式不支援此功能|(DM) 與*語句句柄*關聯的驅動程式不支援該函數。|  
|IM017|在非同步通知模式下禁用輪詢|每當使用通知模型時,都會禁用輪詢。|  
|IM018|尚未調用**SQLCompleteAsync**以完成對此句柄的先前異步操作。|如果句柄上的上一個函數調用返回SQL_STILL_EXECUTING,並且啟用了通知模式,則必須在句柄上調用**SQLCompleteAsync**以執行後處理並完成操作。|  
  
 如果在 SQL 語句中為參數傳送資料時呼叫**SQLPutData,** 它可以傳回執行文句 **(SQLExecute**或**SQLExecDirect**) 的函數可以傳回的任何 SQLSTATE。 如果在發送使用**SQLBulk 操作**更新或添加的列的數據或使用**SQLSetPos**更新時調用它,則可以返回**SQLBulk 操作**或**SQLSetPos**可以傳回的任何 SQLSTATE。  
  
## <a name="comments"></a>註解  
 **SQLPutData**可以調用提供執行時的數據,用於兩個用途:參數數據用於 SQLExecute 或**SQLExecDirect**的**SQLExecDirect**呼叫,或者當對**SQLBulk 操作**的呼叫更新或添加行或透過呼叫**SQLSetPos**更新時使用的列數據。  
  
 當應用程式呼叫**SQLParamData**以確定它應該傳送哪些資料時,驅動程式將返回一個指示器,應用程式可以使用該指示器來確定要發送的參數資料或可以找到列資料的位置。 它還返回SQL_NEED_DATA,這是應用程式應呼叫**SQLPutData**發送數據的指示器。 在**SQLPutData**的*DataPtr*參數中,應用程式傳遞指向包含參數或列的實際數據的緩衝區的指標。  
  
 當驅動程式返回**SQLPutData**SQL_SUCCESS 時,應用程式將再次調用**SQLParamData。** 如果需要發送更多數據 **,SQLParamData**將返回SQL_NEED_DATA,在這種情況下,應用程式將再次調用**SQLPutData。** 如果已發送所有執行數據,它將返回SQL_SUCCESS。 然後,應用程式再次調用**SQLParamData。** 如果驅動程式返回SQL_NEED_DATA和*\*ValuePtrPtr*中的另一個指標,則需要另一個參數或列的數據,並且再次調用**SQLPutData。** 如果驅動程式返回SQL_SUCCESS,則已發送所有執行時的數據數據,並可以執行 SQL 語句,也可以處理**SQLBulk 操作**或**SQLSetPos**調用。  
  
 有關如何在語句執行時傳遞數據執行參數資料的詳細資訊,請參閱[SQLBind 參數](../../../odbc/reference/syntax/sqlbindparameter-function.md)中的"傳遞參數值"和[「發送長數據](../../../odbc/reference/develop-app/sending-long-data.md)」。 有關如何更新或新增資料執行列資料的詳細資訊,請參閱 SQLSetPos 中的「使用[SQLSetPos」](../../../odbc/reference/syntax/sqlsetpos-function.md)部分[、SQLBulk 操作](../../../odbc/reference/syntax/sqlbulkoperations-function.md)中的「使用書籤執行批量更新」以及[長資料和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  應用程式只能將字元 C 資料發送到具有字元、二進位或資料來源特定資料類型的欄,或者將二進位 C 資料發送到具有字元、二進位或資料來源特定資料類型的欄時,才能使用**SQLPutData**以零件發送資料。 如果在任何其他條件下多次調用**SQLPutData,** 它將返回SQL_ERROR和 SQLSTATE HY019(以件形式發送的非字元和非二進位數據)。  
  
## <a name="example"></a>範例  
 下面的示例假定一個數據源名稱稱為 Test。 關聯的資料庫應具有可以創建的表,如下所示:  
  
```sql  
CREATE TABLE emp4 (NAME char(30), AGE int, BIRTHDAY datetime, Memo1 text)  
```  
  
```cpp  
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
  
|如需下列資訊|請參閱|  
|---------------------------|---------|  
|將緩衝區繫結到參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|解除敘述處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行準備好的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回下一個參數以送出資料|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
