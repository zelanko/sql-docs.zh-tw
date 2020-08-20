---
description: SQLPutData 函數
title: SQLPutData 函式 |Microsoft Docs
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
ms.openlocfilehash: 8adda30141a99c1a575d8cc66511f1606e77dcf5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487131"
---
# <a name="sqlputdata-function"></a>SQLPutData 函數
**一致性**  
 引進的版本： ODBC 1.0 標準合規性： ISO 92  
  
 **總結**  
 **SQLPutData** 可讓應用程式在語句執行時間，將參數或資料行的資料傳送至驅動程式。 此函數可用來將部分中的字元或二進位資料值傳送至具有字元、二進位或資料來源特定資料類型的資料行 (例如，SQL_LONGVARBINARY 的參數或) 的 SQL_LONGVARCHAR 類型。 **SQLPutData** 支援系結至 unicode C 資料類型，即使基礎驅動程式不支援 unicode 資料也一樣。  
  
## <a name="syntax"></a>語法  
  
```cpp  
  
SQLRETURN SQLPutData(  
      SQLHSTMT     StatementHandle,  
      SQLPOINTER   DataPtr,  
      SQLLEN       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>引數  
 *StatementHandle*  
 輸出語句控制碼。  
  
 *DataPtr*  
 輸出緩衝區的指標，其中包含參數或資料行的實際資料。 資料必須位於**SQLBindParameter** (的*ValueType*引數中所指定的 C 資料類型（用於參數資料) ），或是資料行資料) 之**SQLBindCol** (的*TargetType*引數。  
  
 *StrLen_or_Ind*  
 輸出\* *DataPtr*的長度。 指定呼叫 **SQLPutData**時所傳送的資料量。 每次呼叫指定的參數或資料行時，資料量可能會有所不同。 除非符合下列其中一個條件，否則會忽略*StrLen_or_Ind* ：  
  
-   *StrLen_or_Ind* 是 SQL_NTS、SQL_Null_DATA 或 SQL_DEFAULT_PARAM。  
  
-   **SQLBindParameter**或**SQLBindCol**中指定的 C 資料類型是 SQL_C_CHAR 或 SQL_C_BINARY。  
  
-   C 資料類型為 SQL_C_DEFAULT，而指定的 SQL 資料類型的預設 C 資料類型為 SQL_C_CHAR 或 SQL_C_BINARY。  
  
 對於所有其他類型的 C 資料，如果*StrLen_or_Ind*不是 SQL_Null_DATA 或 SQL_DEFAULT_PARAM，則驅動程式會假設 \* *DataPtr*緩衝區的大小是以*ValueType*或*TargetType*指定的 C 資料類型大小，並傳送整個資料值。 如需詳細資訊，請參閱附錄 D：資料類型中的 [將資料從 C 轉換成 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) 。  
  
## <a name="returns"></a>傳回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_STILL_EXECUTING、SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLPutData**傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO 時，可以藉由呼叫**SQLGetDiagRec**和*HandleType* （SQL_HANDLE_STMT）和*StatementHandle*的*控制碼*來取得相關聯的 SQLSTATE 值。 下表列出 **SQLPutData** 常傳回的 SQLSTATE 值，並在此函式的內容中說明每一個值;「 (DM) 」標記法優先于驅動程式管理員所傳回的 SQLSTATEs 描述。 除非另有說明，否則會 SQL_ERROR 與每個 SQLSTATE 值相關聯的傳回碼。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特定的告知性訊息。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|01004|字串資料，右邊已截斷|針對輸出參數傳回的字串或二進位資料會截斷非空白字元或非 Null 的二進位資料。 如果是字串值，就會以正確的方式截斷。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|07006|限制的資料類型屬性違規|在**SQLBindParameter**中，針對系結參數所識別的*ValueType*引數所識別的資料值，無法轉換為**SQLBindParameter**中*ParameterType*引數所識別的資料類型。|  
|07S01|使用預設參數無效|參數值（使用 **SQLBindParameter**設定）是 SQL_DEFAULT_PARAM，而且對應的參數沒有預設值。|  
|08S01|通訊連結失敗|在函式完成處理之前，驅動程式與連接驅動程式的資料來源之間的通訊連結失敗。|  
|22001|字串資料，右截斷|將字元或二進位值指派給資料行時，會截斷非空白 (字元) 或非 null (二進位) 字元或位元組。<br /><br /> **SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型為 "Y"，且已傳送更多資料給長參數 (資料類型 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定資料類型，) 于**SQLBindParameter**中使用*StrLen_or_IndPtr*引數指定的資料類型。<br /><br /> **SQLGetInfo**中的 SQL_NEED_LONG_DATA_LEN 資訊類型為 "Y"，且傳送了較長資料行的更多資料 (資料類型 SQL_LONGVARCHAR、SQL_LONGVARBINARY 或 long 資料來源特定資料類型) 在對應到資料列中的資料行的資料列中所指定的資料行，該資料列與**SQLBulkOperations**中新增或更新的資料列或使用**SQLSetPos**更新。|  
|22003|數值超出範圍|針對系結的數值參數或資料行所傳送的資料，會導致整個 (與指派給相關聯的資料表資料行時要截斷之數位的分數) 部分相反。<br /><br /> 將數值或字串) 傳回 (為一個或多個輸入/輸出或輸出參數的數值或字串，將會導致整個 (與要截斷之數位) 部分的分數相反。|  
|22007|不正確日期時間格式|針對系結至日期、時間或時間戳記結構的參數或資料行所傳送的資料，分別是不正確日期、時間或時間戳記。<br /><br /> 輸入/輸出或輸出參數已系結至日期、時間或時間戳記 C 結構，而傳回參數中的值分別是不正確日期、時間或時間戳記。  (函數會傳回 SQL_SUCCESS_WITH_INFO。 ) |  
|22008|日期時間欄位溢位|針對輸入/輸出或輸出參數計算的日期時程表達式會產生不正確日期、時間或時間戳記 C 結構。|  
|22012|零除|針對輸入/輸出或輸出參數計算的算術運算式會導致除數為零。|  
|22015|間隔欄位溢位|針對確切數值或間隔資料行或參數傳送至間隔 SQL 資料類型的資料，會導致遺失有效位數。<br /><br /> 傳送資料的間隔資料行或參數有一個以上的欄位、已轉換成數值資料類型，而且沒有數值資料類型的表示。<br /><br /> 傳送給資料行或參數資料的資料已指派給間隔 SQL 類型，而且間隔 SQL 類型中的 C 類型值沒有標記法。<br /><br /> 針對確切數值或間隔 C 資料行或參數傳送至間隔 C 類型的資料，會導致遺失有效位數。<br /><br /> 傳送給資料行或參數資料的資料已指派給間隔 C 結構，而且間隔資料結構中沒有資料的標記法。|  
|22018|轉換規格的字元值無效|C 類型是精確或近似的數值、日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;而資料行或參數中的值不是系結 C 類型的有效常值。<br /><br /> SQL 類型是精確或近似的數值、日期時間或間隔資料類型;C 類型為 SQL_C_CHAR;而資料行或參數中的值不是系結 SQL 類型的有效常值。|  
|HY000|一般錯誤|發生未定義特定 SQLSTATE 的錯誤，且未定義任何執行特定的 SQLSTATE。 **SQLGetDiagRec**在* \* MessageText*緩衝區中傳回的錯誤訊息會描述錯誤及其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置支援執行或完成函式所需的記憶體。|  
|HY008|已取消作業|*StatementHandle*已啟用非同步處理。 呼叫函式，並在完成執行之前，在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。 然後在 *StatementHandle*上再次呼叫該函式。<br /><br /> 呼叫函式，並在完成執行之前，從多執行緒應用程式中的不同執行緒在*StatementHandle*上呼叫**SQLCancel**或**SQLCancelHandle** 。|  
|HY009|Null 指標的用法無效| (DM) 引數 *DataPtr* 為 null 指標，且引數 *StrLen_or_Ind* 不是0、SQL_DEFAULT_PARAM 或 SQL_Null_DATA。|  
|HY010|函數順序錯誤| (DM) 先前的函式呼叫不是 **SQLPutData** 或 **SQLParamData**的呼叫。<br /><br />  (DM) 以非同步方式執行的函式，是與 *StatementHandle*相關聯的連接控制碼所呼叫。 呼叫 SQLPutData 函式時，仍在執行此非同步函式。<br /><br /> 針對*StatementHandle*呼叫**SQLExecute**、 **SQLEXECDIRECT**或**SQLMoreResults** () DM，並傳回 SQL_PARAM_DATA_AVAILABLE。 在抓取所有資料流程參數的資料之前，會呼叫此函數。<br /><br />  (DM) 以非同步方式執行的函式 (不是針對 *StatementHandle* 呼叫這個) ，而且在呼叫此函式時仍在執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為無法存取基礎記憶體物件，可能是因為記憶體不足的情況。|  
|HY019|以片段傳送的非字元和非二進位資料|針對參數或資料行呼叫了一次以上的**SQLPutData** ，但未使用它將字元 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行，或將二進位 c 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行。|  
|HY020|嘗試串連 null 值|**SQLPutData** 被呼叫一次以上，因為傳回 SQL_NEED_DATA，且在其中一個呼叫中， *StrLen_or_Ind* 引數包含 SQL_Null_DATA 或 SQL_DEFAULT_PARAM。|  
|HY090|不正確字串或緩衝區長度|引數 *DataPtr* 不是 null 指標，且引數 *StrLen_or_Ind* 小於0，但不等於 SQL_NTS 或 SQL_Null_DATA。|  
|HY117|由於未知的交易狀態，連接已暫止。 只允許中斷連接和唯讀功能。| (DM) 如需暫停狀態的詳細資訊，請參閱 [SQLEndTran 函數](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時已過期|連接逾時期間已在資料來源回應要求之前過期。 連接逾時期間是透過 **SQLSetConnectAttr**、SQL_ATTR_CONNECTION_TIMEOUT 設定。|  
|IM001|驅動程式不支援此功能| (DM) 與 *StatementHandle* 相關聯的驅動程式不支援此功能。|  
|IM017|非同步通知模式中的輪詢已停用|每當使用通知模型時，就會停用輪詢。|  
|IM018|尚未呼叫**SQLCompleteAsync**來完成這個控制碼上先前的非同步作業。|如果控制碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING，而且如果啟用了通知模式，則必須在控制碼上呼叫 **SQLCompleteAsync** ，以進行後置處理，並完成作業。|  
  
 如果在 SQL 語句中傳送參數的資料時呼叫 **SQLPutData** ，它可能會傳回呼叫的函式所傳回的任何 SQLSTATE，以執行語句 (**SQLExecute** 或 **SQLExecDirect**) 。 如果在傳送要更新或新增的資料行資料 **，或使用** **SQLSetPos**來更新資料行時呼叫它，它可能會傳回 **SQLBulkOperations** 或 **SQLSetPos**可以傳回的任何 SQLSTATE。  
  
## <a name="comments"></a>註解  
 您可以呼叫**SQLPutData**來提供兩個使用的資料執行中資料：呼叫**SQLExecute**或**SQLExecDirect**時要使用的參數資料，或是在呼叫**SQLBulkOperations**或透過呼叫來更新或加入資料列時，所要使用的資料行**資料。**  
  
 當應用程式呼叫 **SQLParamData** 來判斷應該傳送的資料時，驅動程式會傳回一個指標，讓應用程式用來判斷要傳送的參數資料，或可在何處找到資料行資料。 它也會傳回 SQL_NEED_DATA，也就是應用程式應該呼叫 **SQLPutData** 來傳送資料的指標。 在**SQLPutData**的*DataPtr*引數中，應用程式會將指標傳遞至緩衝區，其中包含參數或資料行的實際資料。  
  
 當驅動程式傳回 **SQLPutData**的 SQL_SUCCESS 時，應用程式會再次呼叫 **SQLParamData** 。 如果需要傳送更多資料， **SQLParamData**會傳回 SQL_NEED_DATA，在這種情況下，應用程式會再次呼叫**SQLPutData** 。 如果已傳送所有資料執行中資料，它會傳回 SQL_SUCCESS。 然後，應用程式會再次呼叫 **SQLParamData** 。 如果驅動程式傳回 SQL_NEED_DATA 以及* \* ValuePtrPtr*中的另一個指標，則需要另一個參數或資料行的資料，然後再次呼叫**SQLPutData** 。 如果驅動程式傳回 SQL_SUCCESS，則會傳送所有資料執行中資料，而且可以執行 SQL 語句，或是可以處理 **SQLBulkOperations** 或 **SQLSetPos** 呼叫。  
  
 如需如何在語句執行時間傳遞資料執行中參數資料的詳細資訊，請參閱 [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md) 中的「傳遞參數值」和傳送 [較長的資料](../../../odbc/reference/develop-app/sending-long-data.md)。 如需有關如何更新或加入資料執行中資料行資料的詳細資訊，請參閱 [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)中的「使用 SQLSetPos」一節， [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)中的「使用書簽執行大量更新」以及 [Long data 和 SQLSetPos 和 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  應用程式只有在將字元 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行，或將二進位 C 資料傳送至具有字元、二進位或資料來源特定資料類型的資料行時，才能使用 **SQLPutData** 傳送元件中的資料。 如果在任何其他情況下呼叫 **SQLPutData** 一次以上，則會傳回 SQL_ERROR 和 SQLSTATE HY019， (部分) 中傳送的非字元和非二進位資料。  
  
## <a name="example"></a>範例  
 下列範例假設名為 Test 的資料來源名稱。 相關聯的資料庫應該有您可以建立的資料表，如下所示：  
  
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
|將緩衝區系結至參數|[SQLBindParameter 函式](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|取消語句處理|[SQLCancel 函式](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|執行 SQL 語句|[SQLExecDirect 函式](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|執行已備妥的 SQL 語句|[SQLExecute 函式](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|傳回要傳送資料的下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
