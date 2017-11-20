---
title: "擷取輸出參數使用 SQLGetData |Microsoft 文件"
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
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c1c4c3a857436f9b66d5aed447a6d5b47d59915a
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>使用 SQLGetData 擷取輸出參數
ODBC 3.8 之前應用程式可以只擷取繫結的輸出緩衝區的查詢的輸出參數。 不過，很難配置大型緩衝區，參數值的大小很大 （例如，大型影像） 時。 ODBC 3.8 導入了新的方式擷取組件中的輸出參數。 應用程式現在可以呼叫**SQLGetData**使用小型緩衝區多次，以便擷取大型參數值。 這是類似於擷取大型資料行資料。  
  
 若要繫結的輸出參數或組件中要擷取輸入/輸出參數，呼叫**SQLBindParameter**與*了*引數設定為 SQL_PARAM_OUTPUT_STREAM 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 SQL_PARAM_INPUT_OUTPUT_STREAM，應用程式可以使用**SQLPutData**參數，將資料輸入，然後使用**SQLGetData**擷取輸出參數。 輸入的資料必須是資料執行 (DAE) 形成使用**SQLPutData**而不是繫結至預先配置的緩衝區。  
  
 ODBC 3.8 應用程式可以使用這項功能，或重新編譯 ODBC 3.x 和 ODBC 2.x 應用程式，這些應用程式必須支援擷取輸出參數，使用 ODBC 3.8 驅動程式**SQLGetData**和 ODBC 3.8 驅動程式管理員。 如需如何啟用舊版應用程式使用 ODBC 的新功能的資訊，請參閱[相容性比較表](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>使用範例  
 例如，請考慮執行預存程序， **{呼叫 sp_f(?,?)}**，其中這兩個參數繫結為 SQL_PARAM_OUTPUT_STREAM，而預存程序傳回任何結果集 （在本主題稍後您會找到更複雜的案例）：  
  
1.  針對每個參數，呼叫**SQLBindParameter**與*了*設 SQL_PARAM_OUTPUT_STREAM 和*ParameterValuePtr*設語彙基元，例如參數數目指向的資料或應用程式用來將輸入的參數繫結結構的指標。 這個範例會使用序數參數做為權杖。  
  
2.  執行與查詢**SQLExecDirect**或**SQLExecute**。 SQL_PARAM_DATA_AVAILABLE 便會傳回，表示有可用的資料流的輸出參數以進行擷取。  
  
3.  呼叫**SQLParamData**取得可供擷取參數。 **SQLParamData**便會傳回第一個可用參數，設定中的語彙基元 SQL_PARAM_DATA_AVAILABLE **SQLBindParameter** （步驟 1）。 緩衝區傳回的權杖， *ValuePtrPtr*指向。  
  
4.  呼叫**SQLGetData**與引數*Col*_or\_*Param_Num*設定為參數來擷取資料的第一個可用的參數序數。 如果**SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLState 01004 （資料已截斷），以及類型為用戶端和伺服器上的可變長度，則從第一個可用的參數擷取更多資料。 您可以繼續呼叫**SQLGetData**直到具有不同傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO **SQLState**。  
  
5.  重複步驟 3 和步驟 4，以擷取目前的參數。  
  
6.  呼叫**SQLParamData**一次。 如果它傳回 SQL_PARAM_DATA_AVAILABLE 以外的項目，沒有其他資料流處理的參數資料擷取，並傳回碼將會執行下一個陳述式的傳回碼。  
  
7.  呼叫**SQLMoreResults**處理下的一個參數集，直到傳回 sql_no_data 為止。 **SQLMoreResults**如果已將陳述式屬性則 sql_attr_paramset_size 會設定為 1，將會傳回 sql_no_data 之後在此範例中。 否則， **SQLMoreResults**會傳回表示有可用的資料流的輸出參數的參數來擷取下一組 SQL_PARAM_DATA_AVAILABLE。  
  
 類似於 DAE 的輸入參數，使用此語彙基元引數中*ParameterValuePtr*中**SQLBindParameter** （步驟 1） 可以是指向應用程式的資料結構，其中包含的指標序數參數和多個應用程式特定資訊，如有必要。  
  
 傳回資料流處理的輸出或輸入/輸出參數的順序是特定的驅動程式，可能永遠無法在查詢中指定的順序相同。  
  
 如果應用程式不會呼叫**SQLGetData**在步驟 4 中，參數值已被丟棄。 同樣地，如果應用程式呼叫**SQLParamData**所有參數的值已讀取的**SQLGetData**、 值的其餘部分會捨棄，和應用程式可以處理下一步參數。  
  
 如果應用程式呼叫**SQLMoreResults**處理之前所有的資料流輸出參數 (**SQLParamData**仍傳回 SQL_PARAM_DATA_AVAILABLE)，會捨棄所有剩餘的參數。 同樣地，如果應用程式呼叫**SQLMoreResults**所有參數的值已讀取的**SQLGetData**，會捨棄其餘部分的值以及剩餘的所有參數，而應用程式可以繼續處理下一個參數集。  
  
 請注意，應用程式中都可以指定 C 資料類型**SQLBindParameter**和**SQLGetData**。 使用指定的 C 資料類型**SQLGetData**中指定的 C 資料類型會覆寫**SQLBindParameter**，除非您的 C 資料類型中指定**SQLGetData**是 SQL_APD_TYPE。  
  
 雖然資料流的輸出參數更有用的型別 BLOB 輸出參數的資料類型時，這項功能也可與任何資料類型。 驅動程式中指定資料流的輸出參數所支援的資料類型。  
  
 如果沒有加以處理，SQL_PARAM_INPUT_OUTPUT_STREAM 參數**SQLExecute**或**SQLExecDirect**會先傳回 SQL_NEED_DATA。 應用程式可以呼叫**SQLParamData**和**SQLPutData**傳送 DAE 參數資料。 會處理所有 DAE 輸入的參數， **SQLParamData**傳回 SQL_PARAM_DATA_AVAILABLE 表示資料流的輸出參數。  
  
 當進行串流輸出參數和處理的繫結的輸出參數，驅動程式會判斷處理輸出參數的順序。 因此，如果輸出參數繫結之緩衝區 ( **SQLBindParameter**參數*了*設為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT)，緩衝區可能不會填入直到**SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO。 讀取繫結至的應用程式之後才緩衝**SQLParamData**傳回 SQL_SUCCESS 或在所有資料流輸出參數的 SQL_SUCCESS_WITH_INFO 處理。  
  
 資料來源會傳回警告和結果集，資料流的輸出參數。 一般情況下，警告和結果集分開處理資料流的輸出參數呼叫**SQLMoreResults**。 處理警告和結果集之前先處理資料流的輸出參數。  
  
 下表描述單一命令傳送至的伺服器，並在應用程式的運作方式的不同的案例。  
  
|狀況|從 SQLExecute 或 SQLExecDirect 的傳回值|下一個|  
|--------------|---------------------------------------------------|---------------------|  
|只包含資料的資料流的輸出參數|SQL_PARAM_DATA_AVAILABLE|使用**SQLParamData**和**SQLGetData**擷取資料流的輸出參數。|  
|資料包含結果集和資料流輸出參數|SQL_SUCCESS|擷取結果集與**SQLBindCol**和**SQLGetData**。<br /><br /> 呼叫**SQLMoreResults**開始處理資料流的輸出參數。 它應該傳回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**擷取資料流的輸出參數。|  
|資料包含一則警告訊息和資料流輸出參數|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**處理警告訊息。<br /><br /> 呼叫**SQLMoreResults**開始處理資料流的輸出參數。 它應該傳回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**擷取資料流的輸出參數。|  
|資料包含一則警告訊息，結果集並資料流輸出參數|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**處理警告訊息。 然後呼叫**SQLMoreResults**開始處理結果集。<br /><br /> 擷取結果集與**SQLBindCol**和**SQLGetData**。<br /><br /> 呼叫**SQLMoreResults**開始處理資料流的輸出參數。 **SQLMoreResults**應該傳回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**擷取資料流的輸出參數。|  
|查詢具有 DAE 輸入參數，例如，資料流處理的輸入/輸出 (DAE) 參數|SQL NEED_DATA|呼叫**SQLParamData**和**SQLPutData**傳送 DAE 輸入參數資料。<br /><br /> 處理所有 DAE 輸入的參數之後， **SQLParamData**可以傳回任何傳回碼的**SQLExecute**和**SQLExecDirect**可以傳回。 您可以接著套用這個資料表中的清況。<br /><br /> 如果傳回的程式碼是 SQL_PARAM_DATA_AVAILABLE，則資料流的輸出參數。 應用程式必須呼叫**SQLParamData**以擷取的語彙基元資料流的輸出參數，此資料表的第一個資料列中所述。<br /><br /> 如果傳回的程式碼是 SQL_SUCCESS，沒有要處理的結果集，或已完成處理。<br /><br /> 如果 SQL_SUCCESS_WITH_INFO 傳回碼，有要處理的警告訊息。|  
  
 之後**SQLExecute**， **SQLExecDirect**，或**SQLMoreResults**如果應用程式呼叫，將結果傳回 SQL_PARAM_DATA_AVAILABLE，函數順序錯誤不是下面清單中的函式：  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** （與陳述式控制代碼）  
  
-   **SQLFreeStmt** （選項 = SQL_CLOSE、 SQL_DROP 或 SQL_UNBIND）  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** （HandleType = SQL_HANDLE_STMT）  
  
-   **SQLGetStmtAttr**  
  
 應用程式仍然可以使用**SQLSetDescField**或**SQLSetDescRec**設定繫結資訊。 不會變更欄位的對應。 不過，內部描述項欄位可能會傳回新的值。 例如，SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM，可能會傳回 SQL_DESC_PARAMETER_TYPE。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用案例： 將組件中的映像擷取結果集  
 **SQLGetData**可用來取得組件中的資料，當預存程序傳回結果集，其中包含一個資料列的映像的相關中繼資料及映像的大型的輸出參數中傳回。  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用案例： 傳送和接收大型物件做為資料流處理的輸入/輸出參數  
 **SQLGetData**可以用於取得與預存程序做為輸入/輸出參數，資料流和資料庫的值會傳遞大型物件時，將資料傳送組件中。 您沒有在記憶體中儲存的所有資料。  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>另請參閱  
 [陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)

