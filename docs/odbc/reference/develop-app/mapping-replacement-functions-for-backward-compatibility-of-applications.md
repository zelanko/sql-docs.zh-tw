---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 45cec32e818eab1ec5586196eadef998b8f988ef
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036396"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>應用程式回溯相容性的取代函式對應
只要沒有使用任何新功能，*透過 odbc 3.x 驅動程式*管理員運作的 odbc 3.x 應用程式就會*針對 odbc 2.x* *驅動程式運作*。 不過，重複的功能和行為變更也會*影響 odbc 3.x* *驅動程式在 odbc 2.x*驅動程式上的運作方式。 使用 ODBC 2.x 驅動程式時，*驅動程式管理員*會將下列已取代一個或多個 odbc 2.x 函式*的 odbc 3.x*函式對應至對應*的 odbc* *2.x 函數。*  
  
|ODBC *3.x*函數|ODBC *2.x*函數|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**、 **SQLAllocConnect**或**SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**、 **SQLFreeConnect**或**SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 可能也會採取其他動作，視所要求的屬性而定。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驅動程式管理員會適當地將此對應到**SQLAllocEnv**、 **SQLAllocConnect**或**SQLAllocStmt**。 下列對**SQLAllocHandle**的呼叫：  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 會導致驅動程式管理員執行下列（概念、無錯誤檢查）對應：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 驅動程式管理員會將此對應至**SQLSetPos**。 下列對**SQLBulkOperations**的呼叫：  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 會產生下列一系列的步驟：  
  
1.  如果 SQL_ADD 運算引數，驅動程式管理員會呼叫**SQLSetPos** ，如下所示：  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  如果不 SQL_ADD 運算引數，驅動程式會傳回 SQLSTATE HY092 （不正確屬性/選項識別碼）。  
  
3.  如果應用程式嘗試在**SQLFetch**或**SQLFetchScroll**和**SQLBulkOperations**的呼叫之間變更 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員會傳回 SQLSTATE HY011 （現在無法設定屬性）。  
  
4.  如果 SQL_ADD 運算引數，應用程式必須呼叫**SQLBindCol**來系結要插入的資料。 它無法呼叫**SQLSetDescField**或**SQLSetDescRec**來系結要插入的資料。  
  
5.  如果 SQL_ADD 運算引數，而且要插入的資料列數目與目前的資料列集大小不同，則必須呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性設定為要在呼叫**SQLBulkOperations**之前插入的資料列數目。 若要還原回先前的資料列集大小，應用程式必須先設定 SQL_ATTR_ROW_ARRAY_SIZE 語句屬性，才會呼叫**SQLFetch**、 **SQLFetchScroll**或**SQLSetPos** 。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驅動程式管理員會將此對應至**SQLColAttributes**。 下列對**SQLColAttribute**的呼叫：  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 會產生下列一系列的步驟：  
  
1.  如果*FieldIdentifier*是下列其中一項：  
  
     SQL_DESC_PRECISION、SQL_DESC_SCALE、SQL_DESC_LENGTH、SQL_DESC_OCTET_LENGTH、SQL_DESC_UNNAMED、SQL_DESC_BASE_COLUMN_NAME、SQL_DESC_LITERAL_PREFIX、SQL_DESC_LITERAL_SUFFIX 或 SQL_DESC_LOCAL_TYPE_NAME  
  
     驅動程式管理員會傳回具有 SQLSTATE HY091 的 SQL_ERROR （不正確描述項欄位識別碼）。 不適用本節的其他規則。  
  
2.  驅動程式管理員會分別將 SQL_COLUMN_COUNT、SQL_COLUMN_NAME 或 SQL_COLUMN_NullABLE 對應到 SQL_DESC_COUNT、SQL_DESC_NAME 或 SQL_DESC_NullABLE。 （ *ODBC 2.x*驅動程式只需要支援 SQL_COLUMN_COUNT、SQL_COLUMN_NAME 和 SQL_COLUMN_NullABLE，而非 SQL_DESC_COUNT、SQL_DESC_NAME 和 SQL_DESC_NullABLE）。對 SQLColAttribute 的呼叫會對應到：  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他*FieldIdentifier*值會傳遞至驅動程式，並將**SQLColAttribute**對應至**SQLColAttributes** （如先前所示）。  
  
4.  如果*BufferLength*小於0，驅動程式管理員會傳回具有 SQLSTATE HY090 的 SQL_ERROR （不正確字串或緩衝區長度）。 不適用本節的其他規則。  
  
5.  如果 SQL_DESC_CONCISE_TYPE *FieldIdentifier* ，而且傳回的類型是精簡的 datetime 資料類型，則驅動程式管理員會對應日期、時間和時間戳記代碼的傳回值。  
  
6.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE HY010 （函數順序錯誤）。 若是如此，驅動程式管理員會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數序列錯誤）。 不適用本節的其他規則。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驅動程式管理員會將此對應至**SQLTransact**。 下列對**SQLEndTran**的呼叫：  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 會導致驅動程式管理員執行下列（概念、無錯誤檢查）對應：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驅動程式管理員會使用 SQL_FETCH_NEXT 的*FetchOrientation*引數，將此對應至**SQLExtendedFetch** 。 下列對**SQLFetch**的呼叫：  
  
```  
SQLFetch (StatementHandle);  
```  
  
 會導致驅動程式管理員呼叫**SQLExtendedFetch**，如下所示：  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在此呼叫中， *pcRow*引數會設定為應用程式透過呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性的值。  
  
> [!NOTE]  
>  當應用程式呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROW_STATUS_PTR 以指向狀態陣列時，驅動程式管理員會快取指標。 *RowStatusArray*可以等於 null 指標。  
  
 如果驅動程式不支援**SQLExtendedFetch** ，而且載入資料指標程式庫，驅動程式管理員會使用資料指標程式庫的**SQLExtendedFetch** ，將**SQLFetch**對應至**SQLExtendedFetch**。 如果驅動程式不支援**SQLExtendedFetch** ，且未載入資料指標程式庫，驅動程式管理員會將**SQLFetch**的呼叫傳遞至驅動程式。 如果應用程式呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員會確保陣列已填入。 如果應用程式呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員會將此欄位設定為1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驅動程式管理員會將此對應至**SQLExtendedFetch**。 下列對**SQLFetchScroll**的呼叫：  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 會產生下列一系列的步驟：  
  
1.  當應用程式呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROW_STATUS_PTR （這會將 IRD 中的 SQL_DESC_ARRAY_STATUS_PTR 欄位設定為指向狀態陣列）時，驅動程式管理員會快取此指標。 讓這個指標*RowStatusArray*;否則，讓*RowStatusArray*等於 null 指標。 如果*RowStatusArray*引數設定為 null 指標，驅動程式管理員會產生資料列狀態陣列。  
  
2.  如果*FetchOrientation*不是 SQL_FETCH_NEXT、SQL_FETCH_PRIOR、SQL_FETCH_ABSOLUTE、SQL_FETCH_RELATIVE、SQL_FETCH_FIRST、SQL_FETCH_LAST 或 SQL_FETCH_BOOKMARK 的其中一個，驅動程式管理員會傳回 SQL_ERROR 和 SQLSTATE HY106 （提取類型超出範圍）。 不適用本節的其他規則。  
  
3.  案例：  
  
-   如果*FetchOrientation*等於 SQL_FETCH_BOOKMARK，則：  
  
    -   如果先前呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_FETCH_BOOKMARK_PTR 的值，則讓*Bmk*成為藉由將指標 SQL_DESC_FETCH_BOOKMARK_PTR 取值來取得的值。  
  
    -   否則，請使用 SQLSTATE HY111 （不正確書簽值）傳回 SQL_ERROR。 不適用本節的其他規則。  
  
     驅動程式管理員現在會呼叫**SQLExtendedFetch**，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否則，驅動程式管理員會呼叫**SQLExtendedFetch**，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在這些呼叫中， *pcRow*引數會設定為應用程式透過呼叫**SQLSetStmtAttr**來設定 SQL_ATTR_ROWS_FETCHED_PTR 語句屬性的值。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE 對應至 SQL_ROWSET_SIZE。  
  
-   如果*rc*等於 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且如果*FetchOrientation*等於 SQL_FETCH_BOOKMARK 且*FetchOffset*不等於0，則驅動程式管理員會張貼警告 SQLSTATE 01S10 （嘗試提取書簽位移，位移值已忽略），並傳回 SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驅動程式管理員會適當地將此對應到**SQLFreeEnv**、 **SQLFreeConnect**或**SQLFreeStmt** 。 下列對**SQLFreeHandle**的呼叫：  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 會導致驅動程式管理員執行下列（概念、無錯誤檢查）對應：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驅動程式管理員會將此對應至**SQLGetConnectOption**。 下列對**SQLGetConnectAttr**的呼叫：  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 會產生下列一系列的步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性，而且不是*在 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回具有 SQLSTATE HY092 （不正確屬性/選項識別碼）的 SQL_ERROR。 本節中沒有任何進一步的規則適用。  
  
2.  如果*屬性*等於 SQL_ATTR_AUTO_IPD 或 SQL_ATTR_METADATA_ID，驅動程式管理員會傳回具有 SQLSTATE HY092 的 SQL_ERROR （不正確屬性/選項識別碼）。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE 08003 （連接未開啟）或 SQLSTATE HY010 （函數順序錯誤）。 若是如此，驅動程式管理員會傳回 SQL_ERROR 並張貼適當的錯誤訊息。 不適用本節的其他規則。  
  
4.  驅動程式管理員會呼叫**SQLGetConnectOption** ，如下所示：  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     請注意， *BufferLength*和*StringLengthPtr*會被忽略。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 當使用 ODBC *2.x 驅動程式的 odbc 3.x 應用程式*呼叫**SQLGetData** ，並將*ColumnNumber*引數設為等於0時 *，odbc 3.x* *驅動程式管理員*會將此項對應至**SQLGetStmtOption**的呼叫，並將*Option*屬性設定為 SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驅動程式管理員會將此對應至**SQLGetStmtOption**。 下列對**SQLGetStmtAttr**的呼叫：  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 會產生下列一系列的步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性，而且不是*在 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回具有 SQLSTATE HY092 （不正確屬性/選項識別碼）的 SQL_ERROR。 本節中沒有任何進一步的規則適用。  
  
2.  If*屬性*為下列其中一項：  
  
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
  
     驅動程式管理員會傳回具有 SQLSTATE HY092 的 SQL_ERROR （不正確屬性/選項識別碼）。 不適用本節的其他規則。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE HY010 （函數順序錯誤）。 若是如此，驅動程式管理員會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數序列錯誤）。 不適用本節的其他規則。  
  
4.  如果*屬性*等於 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員會傳回內部驅動程式管理員變數*魚尾紋*的指標，其已使用或將在**SQLExtendedFetch**的呼叫中使用。 不適用本節的其他規則。  
  
5.  如果*屬性*等於 SQL_DESC_FETCH_BOOKMARK_PTR，驅動程式管理員會傳回呼叫**SQLSetStmtAttr**時所快取的適當指標。  
  
6.  如果*屬性*等於 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員會傳回呼叫**SQLSetStmtAttr**時所快取的適當指標。  
  
7.  驅動程式管理員會呼叫**SQLGetStmtOption** ，如下所示：  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     其中*hstmt*、 *fOption*和*PvParam*會分別設定為*StatementHandle*、 *Attribute*和*valueptr 是*的值。 系統會忽略*BufferLength*和*StringLengthPtr* 。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驅動程式管理員會將此對應至**SQLSetConnectOption**。 下列對**SQLSetConnectAttr**的呼叫：  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 會產生下列一系列的步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性，而且不是*在 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回具有 SQLSTATE HY092 （不正確屬性/選項識別碼）的 SQL_ERROR。 本節中沒有任何進一步的規則適用。  
  
2.  如果*屬性*等於 SQL_ATTR_AUTO_IPD，驅動程式管理員會傳回具有 SQLSTATE HY092 的 SQL_ERROR （不正確屬性/選項識別碼）。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE 08003 （連接未開啟）或 SQLSTATE HY010 （函數順序錯誤）。 如果需要引發這些錯誤的其中一個，驅動程式管理員會傳回 SQL_ERROR 並張貼適當的錯誤訊息。 不適用本節的其他規則。  
  
4.  驅動程式管理員會呼叫**SQLSetConnectOption** ，如下所示：  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     其中*hdbc*、 *fOption*和*VParam*會分別設定為*ConnectionHandle*、 *Attribute*和*valueptr 是*的值。 已忽略*StringLengthPtr* 。  
  
> [!NOTE]  
>  在連接層級上設定語句屬性的功能已被取代。 語句屬性永遠不應*透過 ODBC 3.x*應用程式在連接層級上設定。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驅動程式管理員會將此對應至**SQLSetStmtOption**。 下列對**SQLSetStmtAttr**的呼叫：  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 會產生下列一系列的步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或語句屬性，而且不是*在 ODBC 2.x*中定義的屬性，驅動程式管理員會傳回具有 SQLSTATE HY092 （不正確屬性/選項識別碼）的 SQL_ERROR。 本節中沒有任何進一步的規則適用。  
  
2.  If*屬性*為下列其中一項：  
  
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
  
     驅動程式管理員會傳回具有 SQLSTATE HY092 的 SQL_ERROR （不正確屬性/選項識別碼）。 不適用本節的其他規則。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否需要引發 SQLSTATE HY010 （函數順序錯誤）。 若是如此，驅動程式管理員會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數序列錯誤）。 不適用本節的其他規則。  
  
4.  如果*屬性*等於 SQL_ATTR_PARAMSET_SIZE 或 SQL_ATTR_PARAMS_PROCESSED_PTR，請參閱本主題稍後的「處理參數陣列的對應」一節。 不適用本節的其他規則。  
  
5.  如果*屬性*等於 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員會快取指標值，以供稍後與**SQLFetchScroll**搭配使用。  
  
6.  如果*屬性*等於 SQL_ATTR_ROW_STATUS_PTR，驅動程式管理員會快取指標值，以供稍後用於**SQLFetchScroll**或**SQLSetPos**。 不適用本節的其他規則。  
  
7.  如果*屬性*等於 SQL_ATTR_FETCH_BOOKMARK_PTR，驅動程式管理員會快取*valueptr 是*，稍後在**SQLFetchScroll**的呼叫中會使用快取的值。 不適用本節的其他規則。  
  
8.  驅動程式管理員會呼叫**SQLSetStmtOption** ，如下所示：  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     其中*hstmt*、 *fOption*和*VParam*會分別設定為*StatementHandle*、 *Attribute*和*valueptr 是*的值。 *StringLength*引數會被忽略。  
  
     如果 ODBC 2.x*驅動程式*支援字元字串、驅動程式特定的語句選項，odbc 3.x*應用程式*應該呼叫**SQLSetStmtOption**來設定這些選項。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>處理參數陣列的對應  
 當應用程式呼叫時：  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驅動程式管理員會呼叫：  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 稍後當應用程式呼叫**SQLGetStmtAttr**來取得 SQL_ATTR_PARAMS_PROCESSED_PTR 時，驅動程式管理員會傳回這個變數的指標。 在語句控制碼回到備妥或已配置狀態之前，驅動程式管理員無法變更此內部變數。  
  
 *ODBC 3.x*應用程式可以呼叫**SQLGetStmtAttr**來取得 SQL_ATTR_PARAMS_PROCESSED_PTR 的值，即使它並未在 APD 中明確設定 SQL_DESC_ARRAY_SIZE 欄位也一樣。 例如，如果應用程式的一般常式會在**SQLExecute**傳回 SQL_NEED_DATA 時，檢查正在處理的參數目前的「資料列」，則可能會發生這種情況。 無論 SQL_DESC_ARRAY_SIZE 是1或大於1，都會叫用此常式。 為因應此情況，無論應用程式是否已呼叫**SQLSetStmtAttr**來設定 APD 中的 [SQL_DESC_ARRAY_SIZE] 欄位，驅動程式管理員都必須定義此內部變數。 如果尚未設定 SQL_DESC_ARRAY_SIZE，驅動程式管理員必須先確定此變數包含值1，然後再從**SQLExecDirect**或**SQLExecute**傳回。  
  
## <a name="error-handling"></a>錯誤處理  
 在 ODBC *3.x 中，* 呼叫**SQLFetch**或**SQLFetchScroll**會填入 IRD 中的 SQL_DESC_ARRAY_STATUS_PTR，而指定之診斷記錄的 [SQL_DIAG_ROW_NUMBER] 欄位會包含此記錄所屬之資料列集中的資料列數目。 使用這種方式，應用程式可以將錯誤訊息與指定的資料列位置相互關聯。  
  
 *ODBC 2.x*驅動程式將無法提供這種功能。 不過，它會提供 SQLSTATE 01S01 的錯誤分界（資料列中的錯誤）。 使用**SQLFetch**或**SQLFetchScroll**的 odbc 3.x 應用程式在*進行 odbc 2.x* *驅動程式時*，必須注意這項事實。 也請注意，這類應用程式將無法呼叫**SQLGetDiagField**來實際取得 SQL_DIAG_ROW_NUMBER 欄位。 使用*odbc 2.x* *驅動程式的 odbc 3.x 應用程式*將只能使用 SQL_DIAG_MESSAGE_TEXT、SQL_DIAG_NATIVE、SQL_DIAG_RETURNCODE 或 SQL_DIAG_SQLSTATE 的*以*引數來呼叫**SQLGetDiagField** 。 當使用 ODBC *2.x 驅動程式時，odbc 3.X*驅動程式管理員會維護診斷資料結構，*但 odbc 2.x* *驅動程式只*會傳回這四個欄位。  
  
 當 ODBC 2.x*應用程式**與 odbc 2.x*驅動程式搭配使用時，如果作業可能導致驅動程式管理員傳回多個錯誤，*則 odbc 3.x 驅動程式管理員*可能會傳回不同的錯誤，而不是 odbc *2.x 驅動程式*管理員。  
  
## <a name="mappings-for-bookmark-operations"></a>書簽作業的對應  
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*執行書簽作業時 *，odbc 3.x 驅動程式管理員*會執行下列對應。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 當 ODBC 3.x*應用程式**使用 odbc 2.x*驅動程式呼叫**SQLBindCol** ，以系結至*fCType*等於 SQL_C_VARBOOKMARK 的資料行0時 *，ODBC 3.x*驅動程式管理員會檢查*BufferLength*引數是否小於4或大於4，如果是，則會傳回 SQLSTATE HY090 （不正確字串或緩衝區長度）。 如果*BufferLength*引數等於4，則在以 SQL_C_BOOKMARK 取代*FCType*之後，驅動程式管理員會呼叫驅動程式中的**SQLBindCol** 。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫**SQLColAttribute** ，並將*ColumnNumber*引數設為0時，驅動程式管理員會傳回下表所列的*FieldIdentifier*值。  
  
|*FieldIdentifier*|值|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (空字串)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|**SQLNumResultCols**所傳回的相同值|  
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
 當*使用 odbc 2.x* *驅動程式的 odbc 3.x 應用程式*呼叫**SQLDescribeCol** ，並將*ColumnNumber*引數設為0時，驅動程式管理員會傳回下表所列的值。  
  
|Buffer|值|  
|------------|-----------|  
|ColumnName|"" (空字串)|  
|*NameLengthPtr|0|  
|*DataTypePtr|SQL_BINARY|  
|*ColumnSizePtr|4|  
|*DecimalDigitsPtr|0|  
|*NullablePtr|SQL_NO_NullS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 當 ODBC 3.x*應用程式**與 odbc 2.x*驅動程式搭配使用時，會對**SQLGetData**進行下列呼叫來取得書簽：  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 呼叫會對應至**SQLGetStmtOption** ， *fOption*為 SQL_GET_BOOKMARK，如下所示：  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 其中*hstmt*和*pvParam*會分別設定為*StatementHandle*和*TargetValuePtr*中的值。 書簽會在*pvParam* （*TargetValuePtr*）引數所指向的緩衝區中傳回。 **SQLGetData**呼叫中的*StrLen_or_IndPtr*引數所指向之緩衝區中的值會設定為4。  
  
 在呼叫**SQLGetData**之前呼叫**SQLFetch**的情況下，*以及 ODBC 2.X*驅動程式不支援**SQLExtendedFetch**時，都必須進行這項對應。 在此情況下， **SQLFetch**會傳遞*至 ODBC 2.x*驅動程式，在此情況下不支援書簽抓取。  
  
 您不能*在 ODBC 2.x*驅動程式中多次呼叫**SQLGetData**來抓取部分中的書簽，因此呼叫**SQLGetData**並將*BufferLength*引數設為小於4的值，並將*ColumnNumber*引數設定為0，將會傳回 SQLSTATE HY090 （不正確字串或緩衝區長度）。 不過， **SQLGetData**可以多次呼叫來取得相同的書簽。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 當 ODBC 3.x*應用程式**使用 odbc 2.x*驅動程式呼叫**SQLSetStmtAttr** ，將 SQL_ATTR_USE_BOOKMARKS 屬性設定為 SQL_UB_VARIABLE 時，驅動程式管理員會將屬性設定為*基礎 ODBC 2.x*驅動程式中的 SQL_UB_ON。
