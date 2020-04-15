---
title: 使用 SQLGetData 檢索輸出參數 |微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c96a3f9fc81d081ce16fe8e75746aafe8962fd0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294588"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>使用 SQLGetData 擷取輸出參數
在 ODBC 3.8 之前,應用程式只能檢索具有綁定輸出緩衝區的查詢的輸出參數。 但是,當參數值的大小非常大(例如,大圖像)時,很難分配非常大的緩衝區。 ODBC 3.8 引入了一種檢索零件輸出參數的新方法。 應用程式現在可以多次使用小緩衝區調用**SQLGetData**來檢索大型參數值。 這類似於檢索大型列數據。  
  
 要綁定要在零件中檢索的輸出參數或輸入/輸出參數,請調用**SQLBind 參數**,並將*輸入輸出類型*參數設置為SQL_PARAM_OUTPUT_STREAM或SQL_PARAM_INPUT_OUTPUT_STREAM。 使用SQL_PARAM_INPUT_OUTPUT_STREAM,應用程式可以使用**SQLPutData**將數據輸入到參數中,然後使用**SQLGetData**檢索輸出參數。 輸入數據必須採用執行時的數據 (DAE) 窗體,使用**SQLPutData**而不是將其綁定到預分配的緩衝區。  
  
 此功能可用於 ODBC 3.8 應用程式或重新編譯的 ODBC 3.x 和 ODBC 2.x 應用程式,並且這些應用程式必須具有一個 ODBC 3.8 驅動程式,支援使用**SQLGetData**和 ODBC 3.8 驅動程式管理器檢索輸出參數。 有關如何啟用較舊的應用程式使用新的 ODBC 功能的資訊,請參閱[相容性矩陣](../../../odbc/reference/develop-app/compatibility-matrix.md)。  
  
## <a name="usage-example"></a>使用範例  
 例如,請考慮執行儲存過程 **[CALL sp_f(?,?)],** 其中兩個參數都綁定為SQL_PARAM_OUTPUT_STREAM,並且存儲過程不會返回任何結果集(在本主題的後面部分,您將發現更複雜的方案):  
  
1.  對於每個參數,調用**SQLBind 參數**,其中*輸入輸出類型*設置為*SQL_PARAM_OUTPUT_STREAM,參數 ValuePtr*設定為權杖,如參數編號、指向資料的指標或指向應用程式用於綁定輸入參數的結構的指標。 此示例將使用參數代數作為權杖。  
  
2.  使用**SQLExecDirect**或**SQLExecute 執行**查詢。 將返回SQL_PARAM_DATA_AVAILABLE,指示有流輸出參數可供檢索。  
  
3.  呼叫**SQLParamData**取得可供檢索的參數。 **SQLParamData**將返回SQL_PARAM_DATA_AVAILABLE,該參數將在**SQLBind 參數**(步驟 1)中設置,該參數的權杖。 令牌在*ValuePtrPtr*指向的緩衝區中返回。  
  
4.  使用參數*Col*Col\__or*Param_Num*將**SQLGetData**設置為參數 ddinal 以檢索第一個可用參數的數據。 如果**SQLGetData**傳回SQL_SUCCESS_WITH_INFO和 SQLState 01004(數據截斷),並且該類型在用戶端和伺服器上都是可變長度,則從第一個可用參數中檢索的數據更多。 您可以繼續呼叫**SQLGetData,** 直到它傳回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO使用不同的**SQLState**。  
  
5.  重複步驟 3 和步驟 4 以檢索當前參數。  
  
6.  再次調用**SQLParamData。** 如果它返回除SQL_PARAM_DATA_AVAILABLE以外的任何內容,則沒有要檢索的流式處理參數數據,並且返回代碼將是執行的下一個語句的返回代碼。  
  
7.  調用**SQLMore 結果**來處理下一組參數,直到返回SQL_NO_DATA。 如果語句屬性SQL_ATTR_PARAMSET_SIZE設置為 1,**則 SQLMore 結果**將返回此示例中的SQL_NO_DATA。 否則 **,SQLMore結果**將返回SQL_PARAM_DATA_AVAILABLE,以指示有流輸出參數可用於下一組要檢索的參數。  
  
 與 DAE 輸入參數類似 **,SQLBind 參數**(步驟 1) 中參數*參數 ValuePtr*中使用的權杖可以是指向應用程式資料結構的指標,該結構包含參數的表位和更多特定於應用程式的資訊(如有必要)。  
  
 返回的流輸出或輸入/輸出參數的順序特定於驅動程式,可能並不總是與查詢中指定的順序相同。  
  
 如果應用程式在步驟 4 中不調用**SQLGetData,** 則將丟棄參數值。 同樣,如果應用程式在 SQLGetData 讀取所有參數值之前調用**SQLParamData,** 則將丟棄該值的其餘部分,並且應用程式可以處理下**SQLParamData**一個參數。  
  
 如果應用程式在處理所有流輸出參數之前調用**SQLMore 結果****(SQLParamData**仍返回SQL_PARAM_DATA_AVAILABLE),則將丟棄所有剩餘的參數。 同樣,如果應用程式在**SQLGetData**讀取所有參數值之前調用**SQLMore 結果**,則將丟棄該值的剩餘部分和所有剩餘參數,並且應用程式可以繼續處理下一個參數集。  
  
 請注意,應用程式可以在**SQLBind 參數**和**SQLGetData**中指定 C 數據類型。 使用**SQLGetData**指定的 C 資料類型覆**寫 SQLBind 參數**中指定的 C 資料類型,除非在**SQLGetData**中指定的 C 資料類型SQL_APD_TYPE。  
  
 儘管當輸出參數的數據類型為 BLOB 類型時,流式輸出參數更有用,但此功能也可以與任何數據類型一起使用。 流式輸出參數支援的數據類型在驅動程式中指定。  
  
 如果有要處理SQL_PARAM_INPUT_OUTPUT_STREAM參數 **,SQLExecute**或**SQLExecDirect**將首先返回SQL_NEED_DATA。 應用程式可以調用**SQLParamData**和**SQLPutData**來發送 DAE 參數數據。 處理所有 DAE 輸入參數時 **,SQLParamData**將返回SQL_PARAM_DATA_AVAILABLE以指示流輸出參數可用。  
  
 當有要處理的流式輸出參數和綁定輸出參數時,驅動程式確定處理輸出參數的順序。 因此,如果輸出參數綁定到緩衝區 **(SQLBind參數**參數*InputOutputType*設置為SQL_PARAM_INPUT_OUTPUT或SQL_PARAM_OUTPUT),則在**SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO之前可能無法填充緩衝區。 只有在**SQLParamData**傳回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO後,應用程式才能讀取綁定緩衝區,該緩衝區是處理所有流輸出參數之後。  
  
 數據源除了流式輸出參數外,還可以返回警告和結果集。 通常,通過調用**SQLMoreResult,** 將警告和結果集與流式輸出參數分開處理。 在處理流輸出參數之前,處理警告和結果集。  
  
 下表描述了發送到伺服器的單個命令的不同方案,以及應用程式應如何工作。  
  
|狀況|從 SQLExecute 或 SQLExecDirect 傳回值|後續步驟|  
|--------------|---------------------------------------------------|---------------------|  
|資料僅包含串流輸出參數|SQL_PARAM_DATA_AVAILABLE|使用**SQLParam 資料和** **SQLGetData**檢索流式輸出參數。|  
|資料包含結果集和串流輸出參數|SQL_SUCCESS|使用**SQLBindCol**和**SQLGetData**檢索結果集。<br /><br /> 調用**SQLMore 結果**開始處理流式處理輸出參數。 它應該返回SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParam 資料和** **SQLGetData**檢索流式輸出參數。|  
|資料包括警告訊息與串流輸出參數|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**處理警告消息。<br /><br /> 調用**SQLMore 結果**開始處理流式處理輸出參數。 它應該返回SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParam 資料和** **SQLGetData**檢索流式輸出參數。|  
|資料包括警告訊息、結果集和串流輸出參數|SQL_SUCCESS_WITH_INFO|使用**SQLGetDiagRec**和**SQLGetDiagField**處理警告消息。 然後調用**SQLMore 結果**開始處理結果集。<br /><br /> 使用**SQLBindCol**和**SQLGetData**檢索結果集。<br /><br /> 調用**SQLMore 結果**開始處理流式處理輸出參數。 **SQLMore 結果**應返回SQL_PARAM_DATA_AVAILABLE。<br /><br /> 使用**SQLParam 資料和** **SQLGetData**檢索流式輸出參數。|  
|使用 DAE 輸入參數查詢,例如串流式輸入/輸出 (DAE) 參數|SQL NEED_DATA|呼叫**SQLParamData**和**SQLPutData**傳送 DAE 輸入參數資料。<br /><br /> 處理完所有 DAE 輸入參數後 **,SQLParamData**可以返回**SQLExecute**和**SQLExecDirect**可以返回的任何返回代碼。 然後可以應用此表中的案例。<br /><br /> 如果返回代碼SQL_PARAM_DATA_AVAILABLE,則流式輸出參數可用。 應用程式必須再次調用**SQLParamData**以檢索流式輸出參數的權杖,如此表的第一行所述。<br /><br /> 如果返回代碼SQL_SUCCESS,則有要處理的結果集或處理已完成。<br /><br /> 如果返回代碼SQL_SUCCESS_WITH_INFO,則有要處理的警告消息。|  
  
 在**SQLExecute、SQLExecDirect**或**SQLMoreResult**傳回SQL_PARAM_DATA_AVAILABLE後,如果應用程式呼叫不在以下清單中的函數,則將導致**SQLExecute**函式序列錯誤:  
  
-   **SQLAllocHandle** / **SQLallocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGet 函數**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescfield** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle(** 帶語句句柄)  
  
-   **SQLFreeStmt(** 含選項 = SQL_CLOSE、SQL_DROP或SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQL 斷線**  
  
-   **SQLFreeHandle(** 帶手柄類型 = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 應用程式仍可以使用**SQLSetDescField**或**SQLSetDescRec**來設置綁定資訊。 欄位映射不會更改。 但是,描述符中的欄位可能會返回新值。 例如,SQL_DESC_PARAMETER_TYPE可能會返回SQL_PARAM_INPUT_OUTPUT_STREAM或SQL_PARAM_OUTPUT_STREAM。  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>使用專案:從結果集中檢索零件中的映像  
 當儲存過程返回包含一行有關圖像的中資料的結果集並在大型輸出參數中返回圖像時 **,SQLGetData**可用於獲取部分資料。  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>使用專案:作為串流式輸入/輸出參數傳送和接收大型物件  
 當儲存過程將大型物件作為輸入/輸出參數傳遞,並將值流式傳輸到資料庫或從資料庫中流出時 **,SQLGetData**可用於分段獲取和發送數據。 您不必將所有數據存儲在記憶體中。  
  
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
