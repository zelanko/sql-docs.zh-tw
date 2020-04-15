---
title: 對應應用相容性的替代功能 - ODBC |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18669fe9b6edbd39859166e382ad18d1b04a99a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301088"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>應用程式回溯相容性的取代函式對應
通過 ODBC *3.x*驅動程式管理員工作的 ODBC *3.x*應用程式將針對 ODBC *2.x*驅動程式,只要不使用新功能。 但是,重複的功能和行為更改都會影響 ODBC *3.x*應用程式在 ODBC *2.x*驅動程式上的工作方式。 使用 ODBC *2.x*驅動程式時,驅動程式管理員將以下 ODBC *3.x*函數(已替換一個或多個 ODBC *2.x*函數)映射到相應的 ODBC *2.x*函數中。  
  
|ODBC *3.x*功能|ODBC *2.x*功能|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv** **、SQLAllocConnect**或**SQLAllocStmt**|  
|**SQLBulk 操作**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColattributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQL 延伸**|  
|**SQLFetchScroll**|**SQL 延伸**|  
|**SQLFreeHandle**|**SQLFreeEnv** **、SQLFreeConnect**或**SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSet 連線選項**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 也可以採取其他操作,具體取決於所請求的屬性。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驅動程式管理員將其映射到**SQLAllocEnv、SQLAllocConnect**或**SQLAllocStmt(** 視情況**SQLAllocConnect**而定)。 以下調**SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 將導致驅動程式管理員執行以下(概念性、無錯誤檢查)映射:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulk 操作  
 驅動程式管理員將此映射到**SQLSetPos**。 以下對**SQLBulk 操作的**呼叫 :  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 將導致以下步驟序列:  
  
1.  如果操作參數SQL_ADD,驅動程式管理員將**SQLSetPos**呼叫如下:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  如果未SQL_ADD操作參數,驅動程式將返回 SQLSTATE HY092(無效屬性/選項識別符)。  
  
3.  如果應用程式嘗試更改對**SQLFetch**或**SQLFetchScroll**和**SQLBulk 操作**的呼叫之間的SQL_ATTR_ROW_STATUS_PTR,驅動程式管理員將返回 SQLSTATE HY011(現在無法設置屬性)。  
  
4.  如果操作參數SQL_ADD,則應用程式必須調用**SQLBindCol**來綁定要插入的數據。 它不能調用**SQLSetDescField**或**SQLSetDescRec**來綁定要插入的數據。  
  
5.  如果操作參數SQL_ADD且要插入的行數與當前行集大小不同,則必須調用**SQLSetStmtAttr**將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為調用**SQLBulk 操作**之前要插入的行數。 要恢復到以前的行集大小,應用程式必須在調用**SQLFetch、SQLFetchScroll**或**SQLFetch** **SQLSetPos**之前設置SQL_ATTR_ROW_ARRAY_SIZE語句屬性。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驅動程式管理員將此映射到**SQLColattributes**。 以下對**SQLColattribute 的**呼叫 :  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 將導致以下步驟序列:  
  
1.  如果*欄位識別碼*是以下類型之一:  
  
     SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、SQL_DESC_OCTET_LENGTH、SQL_DESC_UNNAMED、SQL_DESC_BASE_COLUMN_NAME、SQL_DESC_LITERAL_PREFIX、SQL_DESC_LITERAL_SUFFIX或SQL_DESC_LOCAL_TYPE_NAME  
  
     驅動程式管理員返回SQL_ERROR與 SQLSTATE HY091(無效描述符位元識別符)。 本條沒有進一步的規則適用。  
  
2.  驅動程式管理器分別將SQL_COLUMN_COUNT、SQL_COLUMN_NAME或SQL_COLUMN_NULLABLE映射到SQL_DESC_COUNT、SQL_DESC_NAME或SQL_DESC_NULLABLE。 (ODBC *2.x*驅動程式只需要支援SQL_COLUMN_COUNT、SQL_COLUMN_NAME和SQL_COLUMN_NULLABLE,而不需要SQL_DESC_COUNT、SQL_DESC_NAME和SQL_DESC_NULLABLE。SQLColAttribute 的呼叫映射到:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他*字段標識碼*值都傳遞給驅動程式 **,SQLColAttribute**映射到**SQLColattributes,** 如前所示。  
  
4.  如果*緩衝區長度*小於 0,驅動程式管理員將返回 SQL_ERROR SQLSTATE HY090(無效字串或緩衝區長度)。 本條沒有進一步的規則適用。  
  
5.  如果*FieldIdentifier*是SQL_DESC_CONCISE_TYPE並且傳回的類型是簡明的日期時間數據類型,則驅動程式管理員將映射日期、時間和時間戳代碼的返回值。  
  
6.  驅動程式管理員執行必要的檢查,以查看是否需要引發 SQLSTATE HY010(功能序列錯誤)。 如果是這樣,驅動程式管理器將返回SQL_ERROR和 SQLSTATE HY010(函數序列錯誤)。 本條沒有進一步的規則適用。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驅動程式管理員將此映射到**SQLTransact**。 以下調**SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 將導致驅動程式管理員執行以下(概念性、無錯誤檢查)映射:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驅動程式管理員將其映射到**SQL 擴展獲取**,並*帶有SQL_FETCH_NEXT的提取方向*參數。 以下調**SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 將導致驅動程式管理員呼叫 SQL**延伸取得**,如下所示:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在此調用中 *,pcRow*參數設置為應用程式通過調用**SQLSetStmtAttr**將SQL_ATTR_ROWS_FETCHED_PTR語句屬性設置為的值。  
  
> [!NOTE]  
>  當應用程式呼叫**SQLSetStmtAttr**將SQL_ATTR_ROW_STATUS_PTR設定為指向狀態陣列時,驅動程式管理員將緩存指標。 *行狀態數組*可以等於空指標。  
  
 如果驅動程式不支援 SQL**延長取得**,並且載入游標庫,則驅動程式管理員使用游標庫的**SQL 擴充取得****SQLFetch**映射到**SQL 延伸取得**。 如果驅動程式不支援**SQLExtendedFetch,** 並且游標庫未載入,則驅動程式管理員將**SQLFetch**的調用傳遞給驅動程式。 如果應用程式調用**SQLSetStmtAttr**來設置SQL_ATTR_ROW_STATUS_PTR,驅動程式管理器將確保填充陣列。 如果應用程式呼叫**SQLSetStmtAttr**來設定SQL_ATTR_ROWS_FETCHED_PTR,驅動程式管理員將此欄位設置為 1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驅動程式管理員將**SQL 延伸到 SQL 延伸 。** 以下調**SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 將導致以下步驟序列:  
  
1.  當應用程式呼叫**SQLSetStmtAttr**將SQL_ATTR_ROW_STATUS_PTR(將 IRD 中的SQL_DESC_ARRAY_STATUS_PTR欄位設定為指向狀態陣列時,驅動程式管理器將緩存此指標。 讓此指標成為*RowStatusArray*;否則,讓*RowStatusArray*等於空指標。 如果*RowStatusArray*參數設置為空指標,則驅動程式管理器將生成行狀態陣列。  
  
2.  如果*Fetch 方向*不是SQL_FETCH_NEXT、SQL_FETCH_PRIOR、SQL_FETCH_ABSOLUTE、SQL_FETCH_RELATIVE、SQL_FETCH_FIRST、SQL_FETCH_LAST或SQL_FETCH_BOOKMARK之一,則驅動程式管理器返回時帶有SQL_ERROR和 SQLSTATE HY106(提取類型不在範圍)。 本條沒有進一步的規則適用。  
  
3.  案例：  
  
-   如果*取取方向*等於SQL_FETCH_BOOKMARK,則:  
  
    -   如果之前調用**SQLSetStmtAttr**來設置SQL_ATTR_FETCH_BOOKMARK_PTR的值,則讓*Bmk*成為通過取消引用指標SQL_DESC_FETCH_BOOKMARK_PTR獲得的值。  
  
    -   否則,使用 SQLSTATE HY111(無效書籤值)返回SQL_ERROR。 本條沒有進一步的規則適用。  
  
     驅動程式管理員現在呼叫**SQL 擴充取得**,如下所示:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否則,驅動程式管理員將 SQL**擴展獲取**調用 ,如下所示:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在這些調用中 *,pcRow*參數設置為應用程式通過調用**SQLSetStmtAttr**將SQL_ATTR_ROWS_FETCHED_PTR語句屬性設置為的值。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE映射到SQL_ROWSET_SIZE。  
  
-   如果*rc*等於SQL_SUCCESS或SQL_SUCCESS_WITH_INFO,並且*Fetch 方向*等於*SQL_FETCH_BOOKMARK,FetchOffset*不等於 0,則驅動程式管理器將發布警告 SQLSTATE 01S10(嘗試透過書籤偏移進行提取,忽略偏移值),並返回SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驅動程式管理員將其映射到**SQLFreeEnv、SQLFreeConnect**或**SQLFreeConnect** **SQLFreeStmt(** 視情況而定)。 以下調**SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 將導致驅動程式管理員執行以下(概念性、無錯誤檢查)映射:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驅動程式管理員將**SQLGetConnectOption**。 以下調**SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 將導致以下步驟序列:  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性,並且不是在 ODBC *2.x*中定義的屬性,則驅動程式管理員返回SQL_ERROR SQLSTATE HY092(無效屬性/選項識別符)。 本節中沒有進一步的規則。  
  
2.  如果*屬性*等於SQL_ATTR_AUTO_IPD或SQL_ATTR_METADATA_ID,驅動程式管理員將返回SQL_ERROR SQLSTATE HY092(無效屬性/選項標識符)。  
  
3.  驅動程式管理員執行必要的檢查,以查看是否需要引發 SQLSTATE 08003(連接未打開)或 SQLSTATE HY010(功能序列錯誤)。 如果是這樣,驅動程式管理器返回SQL_ERROR併發佈相應的錯誤消息。 本條沒有進一步的規則適用。  
  
4.  驅動程式管理員呼叫**SQLGetConnectOption**的名稱:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     請注意,*緩衝區長度*和*字串長度Ptr*將被忽略。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫**SQLGetData**時,*列數*參數等於 0,ODBC *3.x*驅動程式管理器將此映射到**SQLGetStmtOption**的呼叫,*選項*屬性設定為SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驅動程式管理員將此映射到**SQLGetStmtOption**。 以下調**SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 將導致以下步驟序列:  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性,並且不是在 ODBC *2.x*中定義的屬性,則驅動程式管理員返回SQL_ERROR SQLSTATE HY092(無效屬性/選項識別符)。 本節中沒有進一步的規則。  
  
2.  如果*屬性*是以下屬性之一:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     驅動程式管理員返回SQL_ERROR與 SQLSTATE HY092(無效屬性/選項標識符)。 本條沒有進一步的規則適用。  
  
3.  驅動程式管理員執行必要的檢查,以查看是否需要引發 SQLSTATE HY010(功能序列錯誤)。 如果是這樣,驅動程式管理器將返回SQL_ERROR和 SQLSTATE HY010(函數序列錯誤)。 本條沒有進一步的規則適用。  
  
4.  如果*屬性*等於SQL_ATTR_ROWS_FETCHED_PTR,驅動程式管理員將傳回指向內部驅動程式管理器*變數 cRow*的指標 ,它已使用或將在呼叫**SQLExtendedFetch**中使用 。 本條沒有進一步的規則適用。  
  
5.  如果*屬性*等於SQL_DESC_FETCH_BOOKMARK_PTR,驅動程式管理員將返回它在調用**SQLSetStmtAttr**期間緩存的相應指標。  
  
6.  如果*屬性*等於SQL_ATTR_ROW_STATUS_PTR,驅動程式管理員將返回它在調用**SQLSetStmtAttr**期間緩存的相應指標。  
  
7.  驅動程式管理員呼叫**SQLGetStmtOption**如下所示:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     *其中 hstmt、fOption*和*pvParam*將分別設置為*語句處理*、*屬性*和*fOption**ValuePtr*的值。 將忽略*緩衝區長度*和*字串長度 Ptr。*  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驅動程式管理員將**SQLSetConnectOption**。 以下對**SQLSetConnectAttr 的**呼叫 :  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 將導致以下步驟序列:  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性,並且不是在 ODBC *2.x*中定義的屬性,則驅動程式管理員返回SQL_ERROR SQLSTATE HY092(無效屬性/選項識別符)。 本節中沒有進一步的規則。  
  
2.  如果*屬性*等於SQL_ATTR_AUTO_IPD,驅動程式管理員將返回SQL_ERROR SQLSTATE HY092(無效屬性/選項標識符)。  
  
3.  驅動程式管理員執行必要的檢查,以查看是否需要引發 SQLSTATE 08003(連接未打開)或 SQLSTATE HY010(功能序列錯誤)。 如果需要引發這些錯誤之一,驅動程式管理器將返回SQL_ERROR並發佈相應的錯誤消息。 本條沒有進一步的規則適用。  
  
4.  驅動程式管理員呼叫**SQLSetConnectOption**的名稱:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     *其中 hdbc、fOption*和*vParam**fOption*將分別 設定為*連接句柄*、*屬性*和*ValuePtr*的值。 *字串長度Ptr*將被忽略。  
  
> [!NOTE]  
>  在連接級別上設置語句屬性的能力已被棄用。 聲明屬性絕不應由 ODBC *3.x*應用程式在連接級別設置。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驅動程式管理員將此映射到**SQLSetStmtOption**。 以下調**SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 將導致以下步驟序列:  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性,並且不是在 ODBC *2.x*中定義的屬性,則驅動程式管理員返回SQL_ERROR SQLSTATE HY092(無效屬性/選項識別符)。 本節中沒有進一步的規則。  
  
2.  如果*屬性*是以下屬性之一:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     驅動程式管理員返回SQL_ERROR與 SQLSTATE HY092(無效屬性/選項標識符)。 本條沒有進一步的規則適用。  
  
3.  驅動程式管理員執行必要的檢查,以查看是否需要引發 SQLSTATE HY010(功能序列錯誤)。 如果是這樣,驅動程式管理器將返回SQL_ERROR和 SQLSTATE HY010(函數序列錯誤)。 本條沒有進一步的規則適用。  
  
4.  如果*屬性*等於SQL_ATTR_PARAMSET_SIZE或SQL_ATTR_PARAMS_PROCESSED_PTR,請參閱本主題後面的"處理參數陣列映射"部分。 本條沒有進一步的規則適用。  
  
5.  如果*屬性*等於SQL_ATTR_ROWS_FETCHED_PTR,驅動程式管理器將緩存指標值,以便以後與**SQLFetchScroll**一起使用。  
  
6.  如果*屬性*等於SQL_ATTR_ROW_STATUS_PTR,驅動程式管理員將緩存指標值,以便以後與**SQLFetchScroll**或**SQLSetPos**一起使用。 本條沒有進一步的規則適用。  
  
7.  如果*屬性*等於SQL_ATTR_FETCH_BOOKMARK_PTR,驅動程式管理員將緩存*ValuePtr,* 並在調用**SQLFetchScroll**時稍後使用緩存的值。 本條沒有進一步的規則適用。  
  
8.  驅動程式管理員呼叫**SQLSetStmtOption**的名稱:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     *其中 hstmt、fOption*和*vParam*將分別設置為*語句處理*、*屬性*和*fOption**ValuePtr*的值。 將忽略*字串長度*參數。  
  
     如果 ODBC *2.x*驅動程式支援字元字串、特定於驅動程式的語句選項,則 ODBC *3.x*應用程式應呼叫**SQLSetStmtOption**來設置這些選項。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>處理參數陣列對應  
 當應用程式呼叫時:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驅動程式管理員呼叫:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 當應用程式調用**SQLGetStmtAttr**以檢索SQL_ATTR_PARAMS_PROCESSED_PTR時,驅動程式管理器稍後返回指向此變數的指標。 在語句句柄返回到準備或分配狀態之前,驅動程式管理器無法更改此內部變數。  
  
 ODBC *3.x*應用程式可以調用**SQLGetStmtAttr**以獲取SQL_ATTR_PARAMS_PROCESSED_PTR的值,即使它尚未在 APD 中顯式設置SQL_DESC_ARRAY_SIZE欄位。 例如,如果應用程式具有一個泛型例程,用於檢查**SQLExecute**返回SQL_NEED_DATA時正在處理的當前"行"參數,則可能會出現這種情況。 無論SQL_DESC_ARRAY_SIZE是 1 還是大於 1,都調用此例程。 為了考慮到這一點,驅動程式管理員將需要定義此內部變數,無論應用程式是否調用**SQLSetStmtAttr**來設置 APD 中的SQL_DESC_ARRAY_SIZE欄位。 如果未設置SQL_DESC_ARRAY_SIZE,驅動程式管理員必須確保此變數在從**SQLExecDirect**或**SQLExecute**返回之前包含值 1。  
  
## <a name="error-handling"></a>錯誤處理  
 在 ODBC *3.x*中,呼叫**SQLFetch**或**SQLFetchScroll**填充 IRD 中SQL_DESC_ARRAY_STATUS_PTR,並且給定診斷記錄的SQL_DIAG_ROW_NUMBER欄位包含此記錄相關的行集中的行數。 使用此,應用程式可以將錯誤消息與給定的行位置相關聯。  
  
 ODBC *2.x*驅動程式將無法提供此功能。 但是,它將提供 SQLSTATE 01S01(行中的錯誤)的錯誤劃分。 與 ODBC *2.x*驅動程式對抗時使用**SQLFetch**或**SQLFetchScroll 的**ODBC *3.x*應用程式需要注意這一事實。 另請注意,這樣的應用程式將無法調用**SQLGetDiagField**來實際獲取SQL_DIAG_ROW_NUMBER欄位。 使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式只能使用 SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_RETURNCODE或SQL_DIAG_SQLSTATE*的 Diag 標識符*參數呼叫**SQLGetDiagField。** 使用 ODBC *2.x*驅動程式時,ODBC *3.x*驅動程式管理器維護診斷數據結構,但 ODBC *2.x*驅動程式僅返回這四個字段。  
  
 當 ODBC *2.x*應用程式使用 ODBC *2.x*驅動程式時,如果操作可能導致驅動程式管理器返回多個錯誤,則 ODBC 3.x 驅動程式管理器可能會返回與 ODBC *2.x**2.x*驅動程式管理器不同的錯誤。  
  
## <a name="mappings-for-bookmark-operations"></a>書籤操作對應  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式執行書籤操作時,ODBC *3.x*驅動程式管理器執行以下映射。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫**SQLBindCol**以*fCType*等於SQL_C_VARBOOKMARK綁定到列 0 時,ODBC *3.x*驅動程式管理器將檢查*緩衝區長度*參數是否小於 4 或大於 4,如果是,則返回 SQLSTATE HY090(無效字串或緩衝區長度)。 如果*緩衝區長度*參數等於 4,則驅動程式管理器在用SQL_C_BOOKMARK替換*fCType*後,在驅動程式中調用**SQLBindCol。**  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫**SQLColAttribute,***其中列編號*參數設定為 0 時,驅動程式管理員將傳回下表中列出的*字段識別元*值。  
  
|*FieldIdentifier*|值|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (空字串)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|**SQLNumResultCols**傳回的相同值|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (空字串)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (空字串)|  
|SQL_DESC_LITERAL_SUFFIX|"" (空字串)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (空字串)|  
|SQL_DESC_NAME|"" (空字串)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (空字串)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (空字串)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (空字串)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫**SQLDescribeCol,***其中列號*參數設定為 0 時,驅動程式管理員將返回下表中列出的值。  
  
|Buffer|值|  
|------------|-----------|  
|ColumnName|"" (空字串)|  
|*名稱長度|0|  
|*資料型別的Ptr|SQL_BINARY|  
|*柱大小|4|  
|*十進位數字Ptr|0|  
|*可空的Ptr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式對**SQLGetData**進行以下調以檢索書籤時:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 呼叫映射到**SQLGetStmtOption,fOption**為*fOption*SQL_GET_BOOKMARK,如下所示:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 *其中 hstmt*和*pvParam*分別設置為*語句處理*和*目標 ValuePtr*中的值。 書籤在*pvParam* (*目標值 Ptr*) 參數指向的緩衝區中返回。 調用**SQLGetData**中*StrLen_or_IndPtr*參數指向的緩衝區中的值設置為 4。  
  
 此映射是必須考慮在調用**SQLGetData**之前調用**SQLFetch**和 ODBC *2.x*驅動程式不支援**SQLAgetFetch**的情況。 在這種情況下 **,SQLFetch**將傳遞到 ODBC *2.x*驅動程式,在這種情況下不支援書籤檢索。  
  
 **SQLGetData**不能在 ODBC *2.x*驅動程式中多次調用以檢索零件中的書籤,因此使用*緩衝區長度*參數設置為小於 4 的值調用**SQLGetData,** 而將*列數*參數設置為 0 將傳回 SQLSTATE HY090(無效字串或緩衝區長度)。 但是 **,SQLGetData**可以多次調用以檢索同一個書籤。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 當使用 ODBC *2.x*驅動程式的 ODBC *3.x*應用程式呼叫**SQLSetStmtAttr**將SQL_ATTR_USE_BOOKMARKS屬性設定為SQL_UB_VARIABLE時,驅動程式管理員將該屬性設定為基礎 ODBC *2.x*驅動程式中的SQL_UB_ON。
