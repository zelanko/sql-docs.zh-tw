---
title: 使用 SQLGetData 來抓取輸出參數 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eeb8fae9c563e675499dec47839acdd0a003765a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020508"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>使用 SQLGetData 擷取輸出參數
在 ODBC 3.8 之前，應用程式只能使用系結輸出緩衝區來抓取查詢的輸出參數。 不過，當參數值的大小非常大（例如，大型影像）時，很難以配置非常大的緩衝區。 ODBC 3.8 引進了一種新方法來抓取元件中的輸出參數。 應用程式現在可以多次呼叫具有小型緩衝區的**SQLGetData** ，以取出大型參數值。 這類似于抓取大型資料行資料。  
  
 若要系結要在元件中取出的輸出參數或輸入/輸出參數，請呼叫**SQLBindParameter** ，並將*InputOutputType*引數設定為 SQL_PARAM_OUTPUT_STREAM 或 SQL_PARAM_INPUT_OUTPUT_STREAM。 使用 SQL_PARAM_INPUT_OUTPUT_STREAM，應用程式可以使用**SQLPutData**將資料輸入參數，然後使用**SQLGetData**來抓取輸出參數。 輸入資料必須是資料執行中（DAE）表單，使用**SQLPutData** ，而不是將它系結至預先配置的緩衝區。  
  
 這項功能可供 ODBC 3.8 應用程式使用，或是重新編譯 ODBC 3.x 和 ODBC 2.x 應用程式，而且這些應用程式必須具有 ODBC 3.8 驅動程式，以支援使用**SQLGetData**和 ODBC 3.8 驅動程式管理員來抓取輸出參數。 如需如何讓繼承應用程式使用新 ODBC 功能的相關資訊，請參閱[相容性矩陣](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>使用範例  
 例如，請考慮執行預存程式 **{CALL sp_f （?,?）}**，其中兩個參數都系結為 SQL_PARAM_OUTPUT_STREAM，而預存程式不會傳回任何結果集（稍後在本主題中，您會發現更複雜的案例）：  
  
1.  針對每個參數，呼叫**SQLBindParameter**並將*InputOutputType*設為 SQL_PARAM_OUTPUT_STREAM，並將*ParameterValuePtr*設定為權杖，例如參數編號、資料指標，或應用程式用來系結輸入參數之結構的指標。 這個範例會使用參數序數作為 token。  
  
2.  使用**SQLExecDirect**或**SQLExecute**執行查詢。 系統會傳回 SQL_PARAM_DATA_AVAILABLE，表示有可供抓取的資料流程輸出參數。  
  
3.  呼叫**SQLParamData**以取得可供抓取的參數。 **SQLParamData**將會傳回 SQL_PARAM_DATA_AVAILABLE，其中包含第一個可用參數的 token，其會在**SQLBindParameter**中設定（步驟1）。 權杖會在*ValuePtrPtr*指向的緩衝區中傳回。  
  
4.  使用引數資料行來呼叫\_ **SQLGetData** _or*Param_Num*設定*為參數序數*，以取出第一個可用參數的資料。 如果**SQLGetData**傳回 SQL_SUCCESS_WITH_INFO 和 SQLState 01004 （資料已截斷），且類型在用戶端和伺服器上都是可變的長度，則會有更多資料可從第一個可用的參數抓取。 您可以繼續呼叫**SQLGetData** ，直到它以不同的**SQLState**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 為止。  
  
5.  重複步驟3和步驟4，以取得目前的參數。  
  
6.  再次呼叫**SQLParamData** 。 如果它傳回 SQL_PARAM_DATA_AVAILABLE 以外的任何內容，則不會有更多串流參數資料可供抓取，而傳回碼會是下一個執行之語句的傳回碼。  
  
7.  呼叫**SQLMoreResults**來處理下一組參數，直到它傳回 SQL_NO_DATA 為止。 如果 SQL_ATTR_PARAMSET_SIZE 的語句屬性設為1， **SQLMoreResults**會在此範例中傳回 SQL_NO_DATA。 否則， **SQLMoreResults**會傳回 SQL_PARAM_DATA_AVAILABLE，表示有可供下一組參數抓取的資料流程輸出參數。  
  
 類似于 DAE 輸入參數，在**SQLBindParameter**的引數*ParameterValuePtr*中使用的權杖（步驟1）可以是指向應用程式資料結構的指標，其中包含參數的序數和更多應用程式特定的資訊（如有需要）。  
  
 傳回的資料流程輸出或輸入/輸出參數的順序是驅動程式特定的，而且可能不一定與查詢中所指定的順序相同。  
  
 如果應用程式未在步驟4中呼叫**SQLGetData** ，則會捨棄參數值。 同樣地，如果應用程式在**SQLGetData**讀取所有參數值之前呼叫**SQLParamData** ，則會捨棄值的其餘部分，而且應用程式可以處理下一個參數。  
  
 如果應用程式在處理所有資料流程輸出參數之前呼叫**SQLMoreResults** （**SQLParamData**仍會傳回 SQL_PARAM_DATA_AVAILABLE），則會捨棄所有剩餘的參數。 同樣地，如果應用程式在**SQLGetData**讀取所有參數值之前呼叫**SQLMoreResults** ，則會捨棄值和其餘所有參數的其餘部分，而且應用程式可以繼續處理下一個參數集。  
  
 請注意，應用程式可以在**SQLBindParameter**和**SQLGetData**中指定 C 資料類型。 以**SQLGetData**指定的 c 資料類型會覆寫**SQLBindParameter**中指定的 c 資料類型，除非**SQLGetData**中指定的 c 資料類型是 SQL_APD_TYPE。  
  
 雖然當輸出參數的資料類型是 BLOB 類型時，資料流程輸出參數會更有用，但這項功能也可以搭配任何資料類型使用。 驅動程式中指定了資料流程輸出參數所支援的資料類型。  
  
 如果有 SQL_PARAM_INPUT_OUTPUT_STREAM 參數要處理， **SQLExecute**或**SQLExecDirect**會先傳回 SQL_NEED_DATA。 應用程式可以呼叫**SQLParamData**和**SQLPUTDATA**來傳送 DAE 參數資料。 當處理所有的 DAE 輸入參數時， **SQLParamData**會傳回 SQL_PARAM_DATA_AVAILABLE 以指出資料流程輸出參數可供使用。  
  
 當有要處理的資料流程輸出參數和系結輸出參數時，驅動程式會決定處理輸出參數的順序。 因此，如果輸出參數系結至緩衝區（ **SQLBindParameter**參數*InputOutputType*設定為 SQL_PARAM_INPUT_OUTPUT 或 SQL_PARAM_OUTPUT），則在**SQLParamData**傳回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 之前，可能不會填入緩衝區。 應用程式應該只在**SQLParamData**傳回處理所有資料流程輸出參數之後的 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 之後，才讀取系結緩衝區。  
  
 除了資料流程輸出參數之外，資料來源還可以傳回警告和結果集。 一般而言，警告和結果集會藉由呼叫**SQLMoreResults**，與資料流程輸出參數分開處理。 處理資料流程輸出參數之前的處理警告和結果集。  
  
 下表描述傳送至伺服器之單一命令的不同案例，以及應用程式的使用方式。  
  
|狀況|從 SQLExecute 或 SQLExecDirect 傳回值|接下來該怎麼做|  
|--------------|---------------------------------------------------|---------------------|  
|資料僅包含資料流程輸出參數|SQL_PARAM_DATA_AVAILABLE|使用**SQLParamData**和**SQLGetData**來取出資料流程輸出參數。|  
|資料包含結果集和資料流程輸出參數|SQL_SUCCESS|使用**SQLBindCol**和**SQLGetData**取出結果集。<br /><br /> 呼叫**SQLMoreResults**以開始處理資料流程輸出參數。 它應該會傳回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**來取出資料流程輸出參數。|  
|資料包含警告訊息和資料流程輸出參數|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**來處理警告訊息。<br /><br /> 呼叫**SQLMoreResults**以開始處理資料流程輸出參數。 它應該會傳回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**來取出資料流程輸出參數。|  
|資料包含警告訊息、結果集和資料流程輸出參數|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**來處理警告訊息。 然後呼叫**SQLMoreResults**以開始處理結果集。<br /><br /> 使用**SQLBindCol**和**SQLGetData**取出結果集。<br /><br /> 呼叫**SQLMoreResults**以開始處理資料流程輸出參數。 **SQLMoreResults**應該會傳回 SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParamData**和**SQLGetData**來取出資料流程輸出參數。|  
|使用 DAE 輸入參數進行查詢，例如資料流程輸入/輸出（DAE）參數|SQL NEED_DATA|呼叫**SQLParamData**和**SQLPUTDATA**來傳送 DAE 輸入參數資料。<br /><br /> 在處理所有的 DAE 輸入參數之後， **SQLParamData**可能會傳回**SQLExecute**和**SQLExecDirect**可以傳回的任何傳回碼。 然後可以套用此資料表中的案例。<br /><br /> 如果傳回碼 SQL_PARAM_DATA_AVAILABLE，則可以使用資料流程輸出參數。 應用程式必須再次呼叫**SQLParamData**來取得資料流程輸出參數的 token，如本表的第一列中所述。<br /><br /> 如果傳回碼為 SQL_SUCCESS，則表示有要處理的結果集，或處理已完成。<br /><br /> 如果傳回碼為 SQL_SUCCESS_WITH_INFO，則會有要處理的警告訊息。|  
  
 **SQLExecute**、 **SQLExecDirect**或**SQLMoreResults**傳回 SQL_PARAM_DATA_AVAILABLE 之後，如果應用程式呼叫的函式不在下列清單中，就會產生函式順序錯誤：  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **** SQLGetEnvAttr / **** SQLGetDescField / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** （with 語句控制碼）  
  
-   **SQLFreeStmt** （with Option = SQL_CLOSE，SQL_DROP 或 SQL_UNBIND）  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** （含 HandleType = SQL_HANDLE_STMT）  
  
-   **SQLGetStmtAttr**  
  
 應用程式仍然可以使用**SQLSetDescField**或**SQLSetDescRec**來設定系結資訊。 欄位對應將不會變更。 不過，描述元內的欄位可能會傳回新的值。 例如，SQL_DESC_PARAMETER_TYPE 可能會傳回 SQL_PARAM_INPUT_OUTPUT_STREAM 或 SQL_PARAM_OUTPUT_STREAM。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用案例：從結果集取出元件中的影像  
 當預存程式傳回的結果集包含一個影像相關中繼資料的資料列，而且影像是以大型輸出參數傳回時，可以使用**SQLGetData**來取得部分中的資料。  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用案例：以資料流程處理輸入/輸出參數的形式傳送和接收大型物件  
 當預存程式傳遞大型物件做為輸入/輸出參數時，可以使用**SQLGetData**來取得和傳送元件中的資料，並將值與資料庫進行資料流程處理。 您不需要將所有資料儲存在記憶體中。  
  
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
