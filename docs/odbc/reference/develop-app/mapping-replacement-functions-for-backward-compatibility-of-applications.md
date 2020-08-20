---
description: 應用程式回溯相容性的取代函式對應
title: 對應應用程式相容性的取代函式-ODBC |Microsoft Docs
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
ms.openlocfilehash: 7cba29b0dda2b0d4533444fd3fa8b83eaaeae7a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461410"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>應用程式回溯相容性的取代函式對應
只要沒有使用任何新功能，透過 ODBC 3.x*驅動程式*管理員運作的 odbc 3.x 應用程式就會*處理 odbc 2.x* *驅動程式。* 不過，重複的功能和行為變更都有影響 ODBC 3.x 應用程式*在 odbc 2.x* *驅動程式上*的運作方式。 使用 ODBC *2.x 驅動程式*時，驅動程式管理員會將下列已取代一個或多個 odbc *2.X 函數的 odbc 3.x*函式對應至對應*的 odbc* *2.x 函數。*  
  
|ODBC *3.x* 函數|ODBC *2.x* 函數|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**、 **SQLAllocConnect**或 **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**、 **SQLFreeConnect**或 **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 可能也會採取其他動作，視所要求的屬性而定。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驅動程式管理員會適當地將此對應至 **SQLAllocEnv**、 **SQLAllocConnect**或 **SQLAllocStmt**。 下列 **SQLAllocHandle**呼叫：  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 會導致驅動程式管理員執行下列 (概念，並不會檢查) 對應的錯誤：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 驅動程式管理員會將此對應至 **SQLSetPos**。 下列 **SQLBulkOperations**呼叫：  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  如果 SQL_ADD 操作引數，驅動程式管理員會呼叫 **SQLSetPos** ，如下所示：  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  如果未 SQL_ADD 操作引數，驅動程式會傳回 SQLSTATE HY092 (不正確屬性/選項識別碼) 。  
  
3.  如果應用程式嘗試在呼叫 **SQLFetch** 或 **SQLFetchScroll** 和 **SQLBulkOperations**之間變更 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員將會傳回 SQLSTATE HY011 (屬性目前無法設定) 。  
  
4.  如果 SQL_ADD 運算引數，應用程式必須呼叫 **SQLBindCol** 來系結要插入的資料。 它無法呼叫 **SQLSetDescField** 或 **SQLSetDescRec** 來系結要插入的資料。  
  
5.  如果作業引數是 SQL_ADD，且要插入的資料列數目與目前的資料列集大小不同，則必須呼叫 **SQLSetStmtAttr** ，以將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為在呼叫 **SQLBulkOperations**之前要插入的資料列數目。 若要還原回先前的資料列集大小，應用程式必須在呼叫 **SQLFetch**、 **SQLFetchScroll**或 **SQLSetPos** 之前，先設定 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驅動程式管理員會將此對應至 **SQLColAttributes**。 下列 **SQLColAttribute**呼叫：  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  如果 *FieldIdentifier* 是下列其中一項：  
  
     SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、SQL_DESC_OCTET_LENGTH、SQL_DESC_UNNAMED、SQL_DESC_BASE_COLUMN_NAME、SQL_DESC_LITERAL_PREFIX、SQL_DESC_LITERAL_SUFFIX 或 SQL_DESC_LOCAL_TYPE_NAME  
  
     驅動程式管理員會以 SQLSTATE HY091 傳回 SQL_ERROR， (不正確描述項欄位識別碼) 。 本節不再適用此規則。  
  
2.  驅動程式管理員會分別將 SQL_COLUMN_COUNT、SQL_COLUMN_NAME 或 SQL_COLUMN_NullABLE 對應至 SQL_DESC_COUNT、SQL_DESC_NAME 或 SQL_DESC_NullABLE。  (*ODBC 2.x* 驅動程式只需要支援 SQL_COLUMN_COUNT、SQL_COLUMN_NAME 和 SQL_COLUMN_NullABLE，而不是 SQL_DESC_COUNT、SQL_DESC_NAME 和 SQL_DESC_NullABLE。 ) 對 SQLColAttribute 的呼叫會對應至：  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他 *FieldIdentifier* 值都會傳遞至驅動程式，而 **SQLColAttribute** 會對應到 **SQLColAttributes** ，如先前所示。  
  
4.  如果 *BufferLength* 小於0，驅動程式管理員會傳回具有 SQLSTATE HY090 的 SQL_ERROR， (不正確字串或緩衝區長度) 。 本節不再適用此規則。  
  
5.  如果 *FieldIdentifier* 是 SQL_DESC_CONCISE_TYPE，且傳回的型別是簡潔的 datetime 資料類型，驅動程式管理員會對應日期、時間和時間戳記代碼的傳回值。  
  
6.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE HY010 (函數順序錯誤) 。 如果是的話，驅動程式管理員會傳回 SQL_ERROR，且 SQLSTATE HY010 (函數順序錯誤) 。 本節不再適用此規則。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驅動程式管理員會將此對應至 **SQLTransact**。 下列 **SQLEndTran**呼叫：  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 會導致驅動程式管理員執行下列 (概念，並不會檢查) 對應的錯誤：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驅動程式管理員會使用 SQL_FETCH_NEXT 的*FetchOrientation*引數，將此對應至**SQLExtendedFetch** 。 下列 **SQLFetch**呼叫：  
  
```  
SQLFetch (StatementHandle);  
```  
  
 會導致驅動程式管理員呼叫 **SQLExtendedFetch**，如下所示：  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在此呼叫中， *pcRow* 引數會設定為應用程式透過呼叫 **SQLSetStmtAttr**來設定 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性的值。  
  
> [!NOTE]  
>  當應用程式呼叫 **SQLSetStmtAttr** 來設定指向狀態陣列的 SQL_ATTR_ROW_STATUS_PTR 時，驅動程式管理員會快取指標。 *RowStatusArray* 可以等於 null 指標。  
  
 如果驅動程式不支援 **SQLExtendedFetch** ，而且已載入資料指標程式庫，驅動程式管理員會使用資料指標程式庫的 **SQLExtendedFetch** ，將 **SQLFetch** 對應至 **SQLExtendedFetch**。 如果驅動程式不支援 **SQLExtendedFetch** ，而且未載入資料指標程式庫，驅動程式管理員會將 **SQLFetch** 的呼叫傳遞至驅動程式。 如果應用程式呼叫 **SQLSetStmtAttr** 來設定 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員會確保已填入陣列。 如果應用程式呼叫 **SQLSetStmtAttr** 來設定 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員會將此欄位設定為1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驅動程式管理員會將此對應至 **SQLExtendedFetch**。 下列 **SQLFetchScroll**呼叫：  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  當應用程式呼叫 **SQLSetStmtAttr** 來設定 SQL_ATTR_ROW_STATUS_PTR (將 IRD) 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為指向狀態陣列時，驅動程式管理員會快取此指標。 讓這個指標變成 *RowStatusArray*;否則，讓 *RowStatusArray* 等於 null 指標。 如果 *RowStatusArray* 引數設定為 null 指標，驅動程式管理員會產生資料列狀態陣列。  
  
2.  如果 *FetchOrientation* 不是 SQL_FETCH_NEXT、SQL_FETCH_PRIOR、SQL_FETCH_ABSOLUTE、SQL_FETCH_RELATIVE、SQL_FETCH_FIRST、SQL_FETCH_LAST 或 SQL_FETCH_BOOKMARK 的其中一種，驅動程式管理員會傳回 SQL_ERROR 和 SQLSTATE HY106 (提取類型超出範圍) 。 本節不再適用此規則。  
  
3.  案例：  
  
-   如果 *FetchOrientation* 等於 SQL_FETCH_BOOKMARK，則：  
  
    -   如果稍早呼叫 **SQLSetStmtAttr** 來設定 SQL_ATTR_FETCH_BOOKMARK_PTR 的值，則讓 *Bmk* 成為取值指標 SQL_DESC_FETCH_BOOKMARK_PTR 所取得的值。  
  
    -   否則，會傳回具有 SQLSTATE HY111 的 SQL_ERROR， (不正確書簽值) 。 本節不再適用此規則。  
  
     驅動程式管理員現在會呼叫 **SQLExtendedFetch**，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否則，驅動程式管理員會呼叫 **SQLExtendedFetch**，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在這些呼叫中， *pcRow* 引數會設定為應用程式透過呼叫 **SQLSetStmtAttr**來設定 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性的值。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE 會對應到 SQL_ROWSET_SIZE。  
  
-   如果 *rc* 等於 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且 *FetchOrientation* 等於 SQL_FETCH_BOOKMARK 且 *FetchOffset* 不等於0，則驅動程式管理員會張貼警告、SQLSTATE 01S10 (嘗試提取書簽位移、位移值) ，然後傳回 SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驅動程式管理員會適當地將此對應至 **SQLFreeEnv**、 **SQLFreeConnect**或 **SQLFreeStmt** 。 下列 **SQLFreeHandle**呼叫：  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 會導致驅動程式管理員執行下列 (概念，並不會檢查) 對應的錯誤：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驅動程式管理員會將此對應至 **SQLGetConnectOption**。 下列 **SQLGetConnectAttr**呼叫：  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  如果 *屬性* 不是驅動程式定義的連接或語句 *屬性，而且不是 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回 SQL_ERROR，其中 SQLSTATE HY092 (不正確屬性/選項識別碼) 。 本節不再適用此規則。  
  
2.  如果 *屬性* 等於 SQL_ATTR_AUTO_IPD 或 SQL_ATTR_METADATA_ID，驅動程式管理員會傳回具有 SQLSTATE HY092 的 SQL_ERROR (不正確屬性/選項識別碼) 。  
  
3.  驅動程式管理員會執行必要的檢查，以查看 SQLSTATE 08003 (連接未開啟) 或 SQLSTATE HY010 (函數順序錯誤) 需要引發。 如果是的話，驅動程式管理員會傳回 SQL_ERROR，並張貼適當的錯誤訊息。 本節不再適用此規則。  
  
4.  驅動程式管理員會呼叫 **SQLGetConnectOption** ，如下所示：  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     請注意，系統會忽略 *BufferLength* 和 *StringLengthPtr* 。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 當使用 ODBC *2.x 驅動程式的 odbc* 3.x 應用程式呼叫**SQLGetData** ，而*ColumnNumber*引數等於0時 *，ODBC 3.x* *驅動程式管理員*會將此呼叫對應至**SQLGetStmtOption** ，並將*Option*屬性設定為 SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驅動程式管理員會將此對應至 **SQLGetStmtOption**。 下列 **SQLGetStmtAttr**呼叫：  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  如果 *屬性* 不是驅動程式定義的連接或語句 *屬性，而且不是 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回 SQL_ERROR，其中 SQLSTATE HY092 (不正確屬性/選項識別碼) 。 本節不再適用此規則。  
  
2.  如果 *屬性* 是下列其中一項：  
  
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
  
     驅動程式管理員會傳回 SQLSTATE HY092 的 SQL_ERROR， (不正確屬性/選項識別碼) 。 本節不再適用此規則。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE HY010 (函數順序錯誤) 。 如果是的話，驅動程式管理員會傳回 SQL_ERROR，且 SQLSTATE HY010 (函數順序錯誤) 。 本節不再適用此規則。  
  
4.  如果 *屬性* 等於 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員會傳回內部驅動程式管理員變數 *魚尾紋*的指標，其已使用或將用於 **SQLExtendedFetch**的呼叫中。 本節不再適用此規則。  
  
5.  如果 *屬性* 等於 SQL_DESC_FETCH_BOOKMARK_PTR，驅動程式管理員會傳回在呼叫 **SQLSetStmtAttr**期間快取的適當指標。  
  
6.  如果 *屬性* 等於 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員會傳回在呼叫 **SQLSetStmtAttr**期間快取的適當指標。  
  
7.  驅動程式管理員會呼叫 **SQLGetStmtOption** ，如下所示：  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     其中 *hstmt*、 *fOption*和 *PvParam* 會分別設定為 *StatementHandle*、 *Attribute*和 *ValuePtr*的值。 系統會忽略 *BufferLength* 和 *StringLengthPtr* 。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驅動程式管理員會將此對應至 **SQLSetConnectOption**。 下列 **SQLSetConnectAttr**呼叫：  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  如果 *屬性* 不是驅動程式定義的連接或語句 *屬性，而且不是 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回 SQL_ERROR，其中 SQLSTATE HY092 (不正確屬性/選項識別碼) 。 本節不再適用此規則。  
  
2.  如果 *屬性* 等於 SQL_ATTR_AUTO_IPD，驅動程式管理員會傳回具有 SQLSTATE HY092 的 SQL_ERROR (不正確屬性/選項識別碼) 。  
  
3.  驅動程式管理員會執行必要的檢查，以查看 SQLSTATE 08003 (連接未開啟) 或 SQLSTATE HY010 (函數順序錯誤) 需要引發。 如果需要引發上述其中一個錯誤，驅動程式管理員會傳回 SQL_ERROR，並張貼適當的錯誤訊息。 本節不再適用此規則。  
  
4.  驅動程式管理員會呼叫 **SQLSetConnectOption** ，如下所示：  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     其中 *hdbc*、 *fOption*和 *VParam* 會分別設定為 *ConnectionHandle*、 *Attribute*和 *ValuePtr*的值。 *StringLengthPtr* 會被忽略。  
  
> [!NOTE]  
>  在連接層級上設定語句屬性的功能已被取代。 您永遠不應該在連接層級上， *使用 ODBC 3.x* 應用程式設定語句屬性。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驅動程式管理員會將此對應至 **SQLSetStmtOption**。 下列 **SQLSetStmtAttr**呼叫：  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 將會產生下列一連串的步驟：  
  
1.  如果 *屬性* 不是驅動程式定義的連接或語句 *屬性，而且不是 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回 SQL_ERROR，其中 SQLSTATE HY092 (不正確屬性/選項識別碼) 。 本節不再適用此規則。  
  
2.  如果 *屬性* 是下列其中一項：  
  
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
  
     驅動程式管理員會傳回 SQLSTATE HY092 的 SQL_ERROR， (不正確屬性/選項識別碼) 。 本節不再適用此規則。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE HY010 (函數順序) 錯誤。 如果是的話，驅動程式管理員會傳回 SQL_ERROR，且 SQLSTATE HY010 (函數順序錯誤) 。 本節不再適用此規則。  
  
4.  如果 *屬性* 等於 SQL_ATTR_PARAMSET_SIZE 或 SQL_ATTR_PARAMS_PROCESSED_PTR，請參閱本主題稍後的「處理參數陣列的對應」一節。 本節不再適用此規則。  
  
5.  如果 *屬性* 等於 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員就會快取指標值，以便稍後與 **SQLFetchScroll**搭配使用。  
  
6.  如果 *屬性* 等於 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員就會快取指標值，以便稍後搭配 **SQLFetchScroll** 或 **SQLSetPos**使用。 本節不再適用此規則。  
  
7.  如果 *屬性* 等於 SQL_ATTR_FETCH_BOOKMARK_PTR，驅動程式管理員就會快取 *ValuePtr* ，稍後在 **SQLFetchScroll**的呼叫中會使用快取的值。 本節不再適用此規則。  
  
8.  驅動程式管理員會呼叫 **SQLSetStmtOption** ，如下所示：  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     其中 *hstmt*、 *fOption*和 *VParam* 會分別設定為 *StatementHandle*、 *Attribute*和 *ValuePtr*的值。 *StringLength*引數會被忽略。  
  
     如果 ODBC 2.x *驅動程式* 支援字元字串、驅動程式特定的語句選項，odbc 3.x *應用程式* 應該呼叫 **SQLSetStmtOption** 來設定這些選項。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>處理參數陣列的對應  
 當應用程式呼叫時：  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驅動程式管理員會呼叫：  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 當應用程式呼叫 **SQLGetStmtAttr** 抓取 SQL_ATTR_PARAMS_PROCESSED_PTR 時，驅動程式管理員稍後會傳回這個變數的指標。 在語句控制碼傳回至已備妥或已配置的狀態之前，驅動程式管理員無法變更這個內部變數。  
  
 *ODBC 3.x*應用程式可以呼叫**SQLGetStmtAttr**來取得 SQL_ATTR_PARAMS_PROCESSED_PTR 的值，即使它並未明確設定 APD 中的 SQL_DESC_ARRAY_SIZE 欄位也一樣。 例如，如果應用程式具有一般常式，可檢查 **SQLExecute** 傳回 SQL_NEED_DATA 時所處理之參數的目前「資料列」，則可能會發生這種情況。 無論 SQL_DESC_ARRAY_SIZE 是1或大於1，都會叫用這個常式。 為了因應這一點，不論應用程式是否呼叫 **SQLSetStmtAttr** 來設定 APD 中的 SQL_DESC_ARRAY_SIZE 欄位，驅動程式管理員都必須定義這個內部變數。 如果尚未設定 SQL_DESC_ARRAY_SIZE，驅動程式管理員必須先確定此變數包含值1，然後再從 **SQLExecDirect** 或 **SQLExecute**傳回。  
  
## <a name="error-handling"></a>錯誤處理  
 在 ODBC *3.x 中，* 呼叫 **SQLFetch** 或 **SQLFetchScroll** 會填入 IRD 中的 SQL_DESC_ARRAY_STATUS_PTR，而給定診斷記錄的 SQL_DIAG_ROW_NUMBER 欄位則包含此記錄所屬資料列集中的資料列編號。 使用此方式，應用程式可以將錯誤訊息與指定的資料列位置相互關聯。  
  
 *ODBC 2.x*驅動程式將無法提供這種功能。 不過，它會在資料列) 中提供 SQLSTATE 01S01 (錯誤的錯誤分界。 在*對 odbc 2.x*驅動程式使用**SQLFetch**或**SQLFetchScroll**的 odbc *3.x 應用程式*，必須留意這項事實。 另外也請注意，這類應用程式將無法呼叫 **SQLGetDiagField** 來實際取得 SQL_DIAG_ROW_NUMBER 的欄位。 使用*odbc 2.x* *驅動程式的 odbc 3.x 應用程式*將只能使用 SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_RETURNCODE 或 SQL_DIAG_SQLSTATE 的*以*引數來呼叫**SQLGetDiagField** 。 *Odbc 2.x* *驅動程式管理員在使用 odbc 2.x*驅動程式時，會維持診斷資料結構，*但是 odbc 2.x*驅動程式只會傳回這四個欄位。  
  
 當 ODBC 2.x*應用程式**使用 odbc 2.x*驅動程式時，如果作業可能導致驅動程式管理員傳回多個錯誤，則 Odbc 3.x 驅動程式管理員可能會傳回不同的錯誤，而不*是 odbc 2.x* *驅動程式管理員*。  
  
## <a name="mappings-for-bookmark-operations"></a>書簽作業的對應  
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*執行書簽作業時 *，odbc 3.x 驅動程式管理員*會執行下列對應。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 當 ODBC 3.x*應用程式**使用 odbc 2.x*驅動程式呼叫**SQLBindCol**來系結至*fCType*等於 SQL_C_VARBOOKMARK 的資料行0時 *，ODBC 3.x 驅動程式管理員*會檢查*BufferLength*引數是否小於4或大於4，如果是，則會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 。 如果*BufferLength*引數等於4，則在以 SQL_C_BOOKMARK 取代*FCType*之後，驅動程式管理員會在驅動程式中呼叫**SQLBindCol** 。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫**SQLColAttribute**時，如果*ColumnNumber*引數設定為0，驅動程式管理員會傳回下表所列的*FieldIdentifier*值。  
  
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
|SQL_DESC_NULLABLE|SQL_NO_NullS|  
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
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫**SQLDescribeCol**時，如果*ColumnNumber*引數設定為0，驅動程式管理員會傳回下表所列的值。  
  
|Buffer|值|  
|------------|-----------|  
|ColumnName|"" (空字串)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NullS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 使用 ODBC 2.x*驅動程式來**執行 odbc* 3.x 應用程式時，會對**SQLGetData**進行下列呼叫，以取得書簽：  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 呼叫會對應至 **SQLGetStmtOption** 與 *fOption* 的 SQL_GET_BOOKMARK，如下所示：  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 其中 *hstmt* 和 *pvParam* 分別設定為 *StatementHandle* 和 *TargetValuePtr*中的值。 書簽會在 *pvParam* (*TargetValuePtr*) 引數所指向的緩衝區中傳回。 **SQLGetData**呼叫中的*StrLen_or_IndPtr*引數所指向之緩衝區中的值會設為4。  
  
 在呼叫**SQLGetData**之前呼叫**SQLFETCH** ，*且 ODBC 2.X*驅動程式不支援**SQLExtendedFetch**之前，需要進行這項對應。 在此情況下， **SQLFetch** 會傳遞 *至 ODBC 2.x* 驅動程式，在此情況下不支援書簽抓取。  
  
 在*ODBC 2.x*驅動程式中不能多次呼叫**SQLGetData** ，以抓取部分中的書簽，因此，如果將*BufferLength*引數設定為小於4的值來呼叫**SQLGetData** ，且*ColumnNumber*引數設定為0，則會傳回 SQLSTATE HY090 (不正確字串或緩衝區長度) 。 不過， **SQLGetData**可以呼叫多次，以取得相同的書簽。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫**SQLSetStmtAttr**將 SQL_ATTR_USE_BOOKMARKS 屬性設定為 SQL_UB_VARIABLE 時，驅動程式管理員會將屬性設定為*基礎 ODBC 2.x*驅動程式中的 SQL_UB_ON。
