---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f91799e5d484a763c23fcc132232a8a35fc6152c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517408"
---
# <a name="sqlputdata-function"></a>SQLPutData 函數
**合規性**  
 導入的版本：ODBC 1.0 標準的合規性：ISO 92  
  
 **摘要**  
 **SQLPutData**允許應用程式將參數或資料行的資料傳送到在陳述式執行階段的驅動程式。 此函式可用來在組件中的字元或二進位資料值傳送至字元、 二進位檔或資料來源特有的資料類型 （例如，SQL_LONGVARBINARY 或 SQL_LONGVARCHAR 類型的參數） 的資料行。 **SQLPutData**支援繫結至 Unicode C 資料類型，即使基礎驅動程式不支援 Unicode 資料。  
  
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
 [輸入]包含參數或資料行的實際資料之緩衝區的指標。 資料必須在中指定的 C 資料類型*ValueType*引數**SQLBindParameter** （適用於參數的資料） 或*TargetType*引數**SQLBindCol** （適用於資料行的資料）。  
  
 *Strlen_or_ind&lt*  
 [輸入]長度\* *DataPtr*。 指定的呼叫中傳送的資料量**SQLPutData**。 資料量可能會隨給定的參數或資料行的每個呼叫。 *Strlen_or_ind&lt*會被忽略，除非它符合下列條件的其中一項：  
  
-   *Strlen_or_ind&lt*是 SQL_NTS、 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM。  
  
-   中指定的 C 資料類型**SQLBindParameter**或是**SQLBindCol**為 SQL_C_CHAR 或 SQL_C_BINARY。  
  
-   C 資料類型是 SQL_C_DEFAULT，而且指定的 SQL 資料類型的預設 C 資料類型為 SQL_C_CHAR 或 SQL_C_BINARY。  
  
 對於所有其他類型的 C 資料，如果*Strlen_or_ind&lt*不是 SQL_NULL_DATA 或 SQL_DEFAULT_PARAM，驅動程式會假設的大小\* *DataPtr*緩衝區是指定的 C 資料類型的大小具有*ValueType*或是*TargetType*並傳送整個資料值。 如需詳細資訊，請參閱 <<c0> [ 轉換將資料從 C 到 SQL 資料類型](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)附錄 d:資料類型。  
  
## <a name="returns"></a>傳回值  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_STILL_EXECUTING、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>診斷  
 當**SQLPutData**會傳回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，相關聯的 SQLSTATE 值，可由呼叫**SQLGetDiagRec**具有*HandleType*的 SQL_HANDLE_STMT 並*處理*的*StatementHandle*。 下表列出通常所傳回的 SQLSTATE 值**SQLPutData** ，並說明每個內容中的此函式; 標記法 」 (DM) 」 之前描述的驅動程式管理員所傳回的 Sqlstate。 傳回每個 SQLSTATE 值相關聯的程式碼會是 SQL_ERROR，除非另有指示。  
  
|SQLSTATE|錯誤|描述|  
|--------------|-----------|-----------------|  
|01000|一般警告|驅動程式特有的告知性訊息。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|01004|字串資料，右邊已截斷|字串或二進位資料傳回輸出參數會導致非空白的字元或二進位資料的非 NULL 的截斷。 如果是字串值，則向右截斷。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|07006|受限制的資料類型屬性違規|所識別的資料值*ValueType*中的引數**SQLBindParameter**繫結的參數無法轉換成資料類型所識別的*ParameterType*中的引數**SQLBindParameter**。|  
|07S01|預設參數用法無效|參數值時，設定**SQLBindParameter**、 已 SQL_DEFAULT_PARAM，和對應的參數沒有預設值。|  
|08S01|通訊連結失敗|函式已完成處理之前，驅動程式和驅動程式已連線到資料來源之間的通訊連結失敗。|  
|22001|字串資料，右側截斷|字元或二進位值的資料行指派導致截斷的非空白 （字元） 或非 null （二進位） 字元或位元組。<br /><br /> SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo** "Y"，並於指定長度的參數 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特有的資料類型） 傳送更多的資料具有*StrLen_or_IndPtr*中的引數**SQLBindParameter**。<br /><br /> SQL_NEED_LONG_DATA_LEN 類型資訊，請在**SQLGetInfo**是"Y"，以及比中已指定，將已傳送長資料行 （資料類型為 SQL_LONGVARCHAR、 SQL_LONGVARBINARY、 或 long 資料來源特有的資料類型） 的詳細資料對應到已加入或更新的資料列中的資料行長度的緩衝區**SQLBulkOperations**或更新的**SQLSetPos**。|  
|22003|數值超出範圍|將資料傳送繫結的數值參數或資料行導致要指派給相關聯的資料表資料行時會遭到截斷的數字 （相對於小數） 的整數部分。<br /><br /> 傳回一或多個輸入/輸出或輸出參數的數值 （以數字或字串） 會造成要截斷的數字 （相對於小數） 的整數部分。|  
|22007|無效的日期時間格式|傳送參數或繫結至日期、 時間或時間戳記結構的資料行的資料是，分別無效的日期、 時間戳記。<br /><br /> 輸入/輸出或輸出參數繫結至日期、 時間或時間戳記 C 結構，但傳回的參數中的值，分別無效的日期、 時間戳記。 （函式會傳回 SQL_SUCCESS_WITH_INFO）。|  
|22008|日期時間欄位溢位|日期時間運算式計算的輸入/輸出或輸出參數會導致日期、 時間或無效的時間戳記 C 結構。|  
|22012|除數為零|算術運算式計算的輸入/輸出或輸出參數為零會導致除數。|  
|22015|間隔欄位溢位|將資料傳送的精確數值或時間間隔資料行或間隔 SQL 資料類型的參數造成有效位數遺失。<br /><br /> 資料已傳送間隔的資料行或參數使用一個以上的欄位、 已轉換成數值資料類型，和數值資料類型中有沒有表示法。<br /><br /> 將資料傳送的資料行或參數資料已指派給間隔 SQL 類型，並沒有間隔 SQL 型別中的 C 類型的值不表示法。<br /><br /> 精確數值或時間間隔 C 資料行或參數 C 間隔類型以傳送的資料會造成有效位數遺失。<br /><br /> 將資料傳送的資料行或參數資料傳遞給 C 間隔結構，並沒有任何表示時間間隔的資料結構中的資料。|  
|22018|轉換規格的字元值無效|C 類型為精確或近似數值、 日期時間或間隔資料類型;資料行的 SQL 類型是字元資料類型;和中的資料行或參數的值不是有效的常值的繫結的 C 類型。<br /><br /> SQL 類型為精確或近似數值、 日期時間或間隔資料類型;C 類型是 SQL_C_CHAR;和中的資料行或參數的值不是有效的常值的繫結的 SQL 類型。|  
|HY000|一般錯誤|其中沒有任何特定的 SQLSTATE 和沒有實作特定的 SQLSTATE 所定義，就會發生錯誤。 所傳回的錯誤訊息**SQLGetDiagRec**中 *\*MessageText*緩衝區描述錯誤和其原因。|  
|HY001|記憶體配置錯誤|驅動程式無法配置記憶體，才能支援執行或完成函式。|  
|HY008|已取消作業|非同步處理已啟用*StatementHandle*。 呼叫函式，和之前執行，完成**SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*。 然後在上一次呼叫函式*StatementHandle*。<br /><br /> 呼叫函式，和之前已完成執行時， **SQLCancel**或是**SQLCancelHandle**上呼叫*StatementHandle*從不同的執行緒中多執行緒應用程式。|  
|HY009|使用無效的 null 指標|(DM) 引數*DataPtr*是 null 指標，而引數*Strlen_or_ind&lt*不是 0、 SQL_DEFAULT_PARAM 或 SQL_NULL_DATA。|  
|HY010|函數順序錯誤|(DM) 先前的函式呼叫不是呼叫**SQLPutData**或是**SQLParamData**。<br /><br /> (DM) 以非同步方式執行的函式呼叫的連接控制代碼相關聯*StatementHandle*。 仍在 SQLPutData 函式呼叫時執行此非同步函式。<br /><br /> (DM) **SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**針對呼叫*StatementHandle*並傳回 SQL_PARAM_DATA_可使用。 資料已擷取所有的資料流參數前呼叫此函式。<br /><br /> 以非同步方式執行的函式 （不是此一） 已呼叫 」 (DM) *StatementHandle*和仍在呼叫此函式時所執行。|  
|HY013|記憶體管理錯誤|無法處理函式呼叫，因為基礎記憶體的物件無法存取，可能是因為記憶體不足情況。|  
|HY019|整塊傳送非字元及非二進位的資料|**SQLPutData**已被呼叫超過一次以上的參數或資料行，以及它已不在使用 C 字元資料傳送至字元、 二進位檔或資料來源特有的資料類型資料行，或傳送二進位的 C 資料行的字元二進位檔或資料來源特有的資料類型。|  
|HY020|嘗試串連 null 值|**SQLPutData**從呼叫傳回 SQL_NEED_DATA，和其中一個這些呼叫中，多次呼叫*Strlen_or_ind&lt* SQL_NULL_DATA 或 SQL_DEFAULT_PARAM，包含引數。|  
|HY090|字串或緩衝區長度無效|引數*DataPtr*不是 null 指標，而引數*Strlen_or_ind&lt*小於 0，但不是等於 SQL_NTS 或是 SQL_NULL_DATA。|  
|HY117|連接已因為未知的交易狀態暫止。 只中斷連線，並允許唯讀的函式。|(DM) 如需暫停狀態的詳細資訊，請參閱[SQLEndTran 函式](../../../odbc/reference/syntax/sqlendtran-function.md)。|  
|HYT01|連接逾時過期|連接逾時期限到期之前的資料來源回應要求。 透過設定連接逾時期限**SQLSetConnectAttr**，SQL_ATTR_CONNECTION_TIMEOUT。|  
|IM001|驅動程式不支援此函式|(DM) 驅動程式相關聯*StatementHandle*不支援此函式。|  
|IM017|輪詢已停用非同步通知模式|每次使用通知模型時，會停用輪詢。|  
|IM018|**SQLCompleteAsync**尚未完成先前的非同步作業，此控制代碼上呼叫。|如果控制代碼上先前的函式呼叫傳回 SQL_STILL_EXECUTING 和通知模式已啟用，如果**SQLCompleteAsync**必須在執行後置處理，並完成作業的控制代碼上呼叫。|  
  
 如果**SQLPutData**稱為時傳送的 SQL 陳述式參數的資料，它會傳回任何可執行陳述式所呼叫的函式所傳回的 SQLSTATE (**SQLExecute** 或**SQLExecDirect**)。 如果呼叫傳送的資料行的資料時正在更新或加上**SQLBulkOperations**或更新**SQLSetPos**，它會傳回任何可傳回的 SQLSTATE **SQLBulkOperations**或是**SQLSetPos**。  
  
## <a name="comments"></a>註解  
 **SQLPutData**可以呼叫以提供兩種用途的資料在執行資料： 要使用的呼叫中的參數資料**SQLExecute**或是**SQLExecDirect**，或在更新資料列時要使用的資料行資料或藉由呼叫加入**SQLBulkOperations**或更新的呼叫所**SQLSetPos**。  
  
 當應用程式呼叫**SQLParamData**來判斷哪些資料傳送，驅動程式會傳回應用程式可用來決定要傳送的參數資料，或可在其中找到資料行的資料指標。 它也會傳回 SQL_NEED_DATA，這是應用程式，它應該呼叫指示器**SQLPutData**來傳送資料。 在  *DataPtr*引數**SQLPutData**，應用程式傳遞至包含參數或資料行的實際資料的緩衝區的指標。  
  
 當驅動程式傳回 SQL_SUCCESS，如**SQLPutData**，應用程式會呼叫**SQLParamData**一次。 **SQLParamData**會傳回 SQL_NEED_DATA 更多資料需要傳送，如果在此情況下應用程式會呼叫**SQLPutData**一次。 如果已傳送所有資料在執行資料，則會傳回 SQL_SUCCESS。 接著，應用程式會呼叫**SQLParamData**一次。 如果驅動程式會傳回 SQL_NEED_DATA 和中的另一種指示器 *\*ValuePtrPtr*，它需要的其他參數或資料行的資料並**SQLPutData**會再次呼叫。 如果驅動程式傳回 SQL_SUCCESS，則所有資料在執行資料已傳送，而且可以執行的 SQL 陳述式或**SQLBulkOperations**或是**SQLSetPos**可以處理呼叫。  
  
 陳述式執行階段會傳遞如何資料在執行參數資料的詳細資訊，請參閱 「 傳遞參數值 」 中[SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)並[傳送長資料](../../../odbc/reference/develop-app/sending-long-data.md)。 更新或新增更多有關如何資料在執行資料行的資料，請參閱 「 使用 SQLSetPos 」 一節中[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)、 「 執行大量更新使用中的書籤 」 [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)，及[長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
> [!NOTE]  
>  應用程式可以使用**SQLPutData**來傳送或傳送字元 C 資料行的字元、 二進位檔或資料來源特有的資料型別時，才傳送二進位的 C 資料行的二進位字元時的組件中的資料特定來源的資料型別。 如果**SQLPutData**呼叫超過一次在其他情況下它會傳回 SQL_ERROR，而且 SQLSTATE HY019 （整塊傳送非字元及非二進位資料）。  
  
## <a name="example"></a>範例  
 下列範例假設名為 Test 的資料來源名稱。 相關聯的資料庫都應該有的資料表，您可以建立、，如下所示：  
  
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
|傳回的資料傳送至下一個參數|[SQLParamData 函式](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
  
## <a name="see-also"></a>另請參閱  
 [ODBC API 參考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 標頭檔](../../../odbc/reference/install/odbc-header-files.md)
