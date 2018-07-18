---
title: 取代函式對應的應用程式的 ODBC 相容 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 14ca73aefb033580c2770da05189e3de04a424e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913973"
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>取代函式對應的應用程式的回溯相容性
ODBC 3 *.x*應用程式使用 ODBC 3 透過 *.x*驅動程式管理員會針對 ODBC 2。*x*只要使用了沒有的新功能的驅動程式。 同時複製功能和行為變更，不過，會影響的方式，ODBC 3。*x*應用程式適用於 ODBC 2。*x*驅動程式。 當使用的 ODBC 2。*x*驅動程式，驅動程式管理員會將對應下列 ODBC 3。*x*函式，也有取代一或多個 ODBC 2。*x*函式，到對應的 ODBC 2。*x*函式。  
  
|ODBC 3。*x*函式|ODBC 2。*x*函式|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] 其他可能也會採取動作，根據所要求的屬性。  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 驅動程式管理員會將對應為**SQLAllocEnv**， **SQLAllocConnect**，或**SQLAllocStmt**視情況。 下列呼叫**SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 將會導致驅動程式管理員執行下列 (概念，進行錯誤檢查) 的對應：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 驅動程式管理員會將對應為**SQLSetPos**。 下列呼叫**SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 將會產生下列一連串步驟：  
  
1.  如果 SQL_ADD 運算引數，則驅動程式管理員呼叫**SQLSetPos** ，如下所示：  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  如果運算引數不是 SQL_ADD，驅動程式會傳回 SQLSTATE HY092 （無效的屬性/選項識別碼）。  
  
3.  如果應用程式嘗試變更呼叫之間 SQL_ATTR_ROW_STATUS_PTR **SQLFetch**或**SQLFetchScroll**和**SQLBulkOperations**，將驅動程式管理員傳回 SQLSTATE HY011 （屬性現在無法設定）。  
  
4.  應用程式如果 SQL_ADD 運算引數，必須呼叫**SQLBindCol**来插入資料繫結。 它不能呼叫**SQLSetDescField**或**SQLSetDescRec**来插入資料繫結。  
  
5.  如果作業引數是 SQL_ADD，而且要插入的資料列數目不是目前的資料列集大小，與相同**SQLSetStmtAttr**必須呼叫以將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設為資料列數目插入之前先呼叫**SQLBulkOperations**。 若要還原成先前的資料列集大小，應用程式必須設定 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性之前**SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**呼叫。  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 驅動程式管理員會將對應為**SQLColAttributes**。 下列呼叫**SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 將會產生下列一連串步驟：  
  
1.  如果*FieldIdentifier*是下列其中之一：  
  
     SQL_DESC_PRECISION、 SQL_DESC_SCALE、 SQL_DESC_LENGTH、 SQL_DESC_OCTET_LENGTH、 SQL_DESC_UNNAMED、 SQL_DESC_BASE_COLUMN_NAME、 SQL_DESC_LITERAL_PREFIX、 SQL_DESC_LITERAL_SUFFIX 或 SQL_DESC_LOCAL_TYPE_NAME  
  
     驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY091 （無效的描述項欄位識別碼）。 本節的任何進一步的規則不套用。  
  
2.  驅動程式管理員會將對應 SQL_COLUMN_COUNT、 SQL_COLUMN_NAME 或 SQL_COLUMN_NULLABLE SQL_DESC_COUNT、 SQL_DESC_NAME，或 SQL_DESC_NULLABLE，分別。 (ODBC 2 *.x*驅動程式需要只支援 SQL_COLUMN_COUNT、 SQL_COLUMN_NAME，SQL_COLUMN_NULLABLE、 不 SQL_DESC_COUNT、 SQL_DESC_NAME，以及 SQL_DESC_NULLABLE。)SQLColAttribute 的呼叫會對應至：  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  所有其他*FieldIdentifier*值會傳遞給驅動程式時，與**SQLColAttribute**對應至**SQLColAttributes**如先前所示。  
  
4.  如果*Columnsize*小於 0，則驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY090 （無效的字串或緩衝區長度）。 本節的任何進一步的規則不套用。  
  
5.  如果*FieldIdentifier* SQL_DESC_CONCISE_TYPE，而傳回的型別精確 datetime 資料類型，傳回值之日期、 時間和時間戳記代碼的驅動程式管理員對應。  
  
6.  驅動程式管理員會執行必要的檢查，以查看是否要產生 SQLSTATE HY010 （函數順序錯誤） 需求。 如果驅動程式管理員所以，會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數順序錯誤）。 本節的任何進一步的規則不套用。  
  
## <a name="sqlendtran"></a>SQLEndTran  
 驅動程式管理員會將對應為**SQLTransact**。 下列呼叫**SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 將會導致驅動程式管理員執行下列 (概念，進行錯誤檢查) 的對應：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 驅動程式管理員會將對應為**SQLExtendedFetch**與*Sqlfetchscroll* SQL_FETCH_NEXT 的引數。 下列呼叫**SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 將會導致驅動程式管理員呼叫**SQLExtendedFetch**、，如下所示：  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 在這個呼叫， *pcRow*引數的設定值，應用程式設定 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性，以透過呼叫**SQLSetStmtAttr**。  
  
> [!NOTE]  
>  當應用程式呼叫**SQLSetStmtAttr**設定 sql_attr_row_status_ptr 設定為指向狀態陣列，驅動程式管理員會快取指標。 *RowStatusArray*可以是等於 null 指標。  
  
 如果驅動程式不支援**SQLExtendedFetch**和載入資料指標程式庫、 驅動程式管理員會使用資料指標程式庫**SQLExtendedFetch**對應**SQLFetch**至**SQLExtendedFetch**。 如果驅動程式不支援**SQLExtendedFetch** ，資料指標程式庫不會載入驅動程式管理員會傳遞至呼叫**SQLFetch**透過驅動程式。 如果應用程式呼叫**SQLSetStmtAttr**為將 sql_attr_row_status_ptr 設定，驅動程式管理員 可確保會填入陣列。 如果應用程式呼叫**SQLSetStmtAttr**設定 SQL_ATTR_ROWS_FETCHED_PTR，驅動程式管理員將此欄位設定為 1。  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 驅動程式管理員會將對應為**SQLExtendedFetch**。 下列呼叫**SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 將會產生下列一連串步驟：  
  
1.  當應用程式呼叫**SQLSetStmtAttr**指向狀態陣列設定 SQL_ATTR_ROW_STATUS_PTR （可設定 IRD SQL_DESC_ARRAY_STATUS_PTR 欄位），驅動程式管理員會快取這個指標。 讓這個指標會*RowStatusArray*; 否則便可讓*RowStatusArray*等於 null 指標。 如果*RowStatusArray*引數設為 null 指標，驅動程式管理員會產生資料列狀態陣列。  
  
2.  如果*Sqlfetchscroll*不是其中一個 SQL_FETCH_NEXT、 SQL_FETCH_PRIOR、 SQL_FETCH_ABSOLUTE、 sql_fetch_relative 但、 SQL_FETCH_FIRST SQL_FETCH_LAST 或要使用 SQL_FETCH_BOOKMARK，驅動程式管理員會傳回 SQL_ERROR 並 SQLSTATEHY106 （提取類型超出範圍）。 本節的任何進一步的規則不套用。  
  
3.  案例：  
  
-   如果*Sqlfetchscroll*等於 SQL_FETCH_BOOKMARK，然後：  
  
    -   如果**SQLSetStmtAttr**呼叫先前設定的值 SQL_ATTR_FETCH_BOOKMARK_PTR，然後讓*Bmk*會取值指標 SQL_DESC_FETCH_BOOKMARK_PTR 所取得之值。  
  
    -   否則會傳回 sql_error，其中包含 SQLSTATE HY111 （無效的書籤值）。 本節的任何進一步的規則不套用。  
  
     驅動程式管理員會立即呼叫**SQLExtendedFetch**、，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   否則，驅動程式管理員呼叫**SQLExtendedFetch**、，如下所示：  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     在這些呼叫中， *pcRow*引數的設定值，應用程式設定 SQL_ATTR_ROWS_FETCHED_PTR 陳述式屬性，以透過呼叫**SQLSetStmtAttr**。  
  
-   SQL_ATTR_ROW_ARRAY_SIZE 會對應至 SQL_ROWSET_SIZE。  
  
-   如果*rc*等於 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，而且如果*Sqlfetchscroll*等於 SQL_FETCH_BOOKMARK 和*FetchOffset*是不等於 0，然後此驅動程式管理員公佈警告，SQLSTATE 01S10 （嘗試擷取書籤位移，位移值被忽略），並傳回 SQL_SUCCESS_WITH_INFO。  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 驅動程式管理員會將對應為**SQLFreeEnv**， **SQLFreeConnect**，或**SQLFreeStmt**依適當情況。 下列呼叫**SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 將會導致驅動程式管理員執行下列 (概念，進行錯誤檢查) 的對應：  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 驅動程式管理員會將對應為**SQLGetConnectOption**。 下列呼叫**SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 將會產生下列一連串步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或陳述式屬性，並不是 ODBC 2 中定義的屬性。*x*，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。 適不用於任何進一步的規則，這一節。  
  
2.  如果*屬性*等於 SQL_ATTR_AUTO_IPD 或 SQL_ATTR_METADATA_ID，則驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。  
  
3.  驅動程式管理員會執行必要的檢查，看看是否包含 SQLSTATE 08003 （未開啟連接） 或 SQLSTATE HY010 （函數順序錯誤） 需要引發。 若是如此，驅動程式管理員會傳回 SQL_ERROR，並會將適當的錯誤訊息。 本節的任何進一步的規則不套用。  
  
4.  驅動程式管理員呼叫**SQLGetConnectOption** ，如下所示：  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     請注意， *Columnsize*和*StringLengthPtr*都會被忽略。  
  
## <a name="sqlgetdata"></a>SQLGetData  
 當 ODBC 3。*x*應用程式使用 ODBC 2 *.x*驅動程式呼叫**SQLGetData**與*ColumnNumber*等於 0，而 ODBC 3引數 *.x*驅動程式管理員對應到呼叫**SQLGetStmtOption**與*選項*屬性設為 SQL_GET_BOOKMARK。  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 驅動程式管理員會將對應為**SQLGetStmtOption**。 下列呼叫**SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 將會產生下列一連串步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或陳述式屬性，並不是 ODBC 2 中定義的屬性。*x*，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。 適不用於任何進一步的規則，這一節。  
  
2.  如果*屬性*是下列其中之一：  
  
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
  
     驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。 本節的任何進一步的規則不套用。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否要產生 SQLSTATE HY010 （函數順序錯誤） 需求。 如果驅動程式管理員所以，會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數順序錯誤）。 本節的任何進一步的規則不套用。  
  
4.  如果*屬性*等於 SQL_ATTR_ROWS_FETCHED_PTR，內部的驅動程式管理員變數則驅動程式管理員會傳回一個指標*cRow*，它具有使用，或將在呼叫中使用**SQLExtendedFetch**。 本節的任何進一步的規則不套用。  
  
5.  如果*屬性*等於 SQL_DESC_FETCH_BOOKMARK_PTR，驅動程式管理員傳回適當的指標，就必須呼叫期間快取**SQLSetStmtAttr**。  
  
6.  如果*屬性*等於 sql_attr_row_status_ptr 設定，驅動程式管理員傳回適當的指標，就必須呼叫期間快取**SQLSetStmtAttr**。  
  
7.  驅動程式管理員呼叫**SQLGetStmtOption** ，如下所示：  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     其中*hstmt*， *fOption*，和*pvParam*將設定之值的*StatementHandle*，*屬性*，和*ValuePtr*分別。 *Columnsize*和*StringLengthPtr*都會被忽略。  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 驅動程式管理員會將對應為**SQLSetConnectOption**。 下列呼叫**SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 將會產生下列一連串步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或陳述式屬性，並不是 ODBC 2 中定義的屬性。*x*，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。 適不用於任何進一步的規則，這一節。  
  
2.  如果*屬性*等於 SQL_ATTR_AUTO_IPD，則驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否包含 SQLSTATE 08003 （未開啟連接） 或 SQLSTATE HY010 （函數順序錯誤） 需要被引發。 如果這些錯誤之一需要引發，驅動程式管理員會傳回 SQL_ERROR，並會將適當的錯誤訊息。 本節的任何進一步的規則不套用。  
  
4.  驅動程式管理員呼叫**SQLSetConnectOption** ，如下所示：  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     其中*hdbc*， *fOption*，和*vParam*將設定之值的*ConnectionHandle*，*屬性*，和*ValuePtr*分別。 *StringLengthPtr*會被忽略。  
  
> [!NOTE]  
>  能夠在連接層級上設定陳述式屬性已被取代。 陳述式屬性不能在連接層級上設定 ODBC 3。*x*應用程式。  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 驅動程式管理員會將對應為**SQLSetStmtOption**。 下列呼叫**SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 將會產生下列一連串步驟：  
  
1.  如果*屬性*不是驅動程式定義的連接或陳述式屬性，並不是 ODBC 2 中定義的屬性。*x*，驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。 適不用於任何進一步的規則，這一節。  
  
2.  如果*屬性*是下列其中之一：  
  
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
  
     驅動程式管理員會傳回 sql_error，其中包含 SQLSTATE HY092 （無效的屬性/選項識別碼）。 本節的任何進一步的規則不套用。  
  
3.  驅動程式管理員會執行必要的檢查，以查看是否要產生 SQLSTATE HY010 （函數順序錯誤） 需要。 如果驅動程式管理員所以，會傳回 SQL_ERROR 並 SQLSTATE HY010 （函數順序錯誤）。 本節的任何進一步的規則不套用。  
  
4.  如果*屬性*在本主題稍後會等於 SQL_ATTR_PARAMSET_SIZE 或 SQL_ATTR_PARAMS_PROCESSED_PTR，請參閱 」 對應的處理參數陣列 」 一節。 本節的任何進一步的規則不套用。  
  
5.  如果*屬性*等於 SQL_ATTR_ROWS_FETCHED_PTR，指標值供日後使用，與驅動程式管理員快取**SQLFetchScroll**。  
  
6.  如果*屬性*等於 sql_attr_row_status_ptr 設定，將指標值供日後使用，與驅動程式管理員快取**SQLFetchScroll**或**SQLSetPos**。 本節的任何進一步的規則不套用。  
  
7.  如果*屬性*等於 SQL_ATTR_FETCH_BOOKMARK_PTR，驅動程式管理員快取*ValuePtr*且將會使用快取的值稍後呼叫**SQLFetchScroll**。 本節的任何進一步的規則不套用。  
  
8.  驅動程式管理員呼叫**SQLSetStmtOption** ，如下所示：  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     其中*hstmt*， *fOption*，和*vParam*將設定之值的*StatementHandle*，*屬性*，和*ValuePtr*分別。 *StringLength*會忽略引數。  
  
     如果 ODBC 2。*x*驅動程式支援的字元字串、 驅動程式專屬的陳述式選項，而 ODBC 3。*x*應用程式應該呼叫**SQLSetStmtOption**設定這些選項。  
  
## <a name="mappings-for-handling-parameter-arrays"></a>對應處理參數陣列  
 當呼叫應用程式：  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 驅動程式管理員會呼叫：  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 驅動程式管理員稍後時，傳回指標給這個變數應用程式呼叫**SQLGetStmtAttr**擷取 SQL_ATTR_PARAMS_PROCESSED_PTR。 驅動程式管理員無法變更此內部變數，除非陳述式控制代碼傳回至已備妥或已配置的狀態。  
  
 ODBC 3。*x*應用程式可以呼叫**SQLGetStmtAttr**取得 SQL_ATTR_PARAMS_PROCESSED_PTR 的值，即使它有未明確設定 SQL_DESC_ARRAY_SIZE 欄位在 APD 中。 這種情況下，就會發生，例如，如果應用程式會檢查目前的參數的 「 資料列 」 的一般常式時正在處理**SQLExecute**傳回 SQL_NEED_DATA。 這個常式會叫用，不論是否 SQL_DESC_ARRAY_SIZE 為 1 或大於 1。 若要將此列入考量，驅動程式管理員需要定義此內部變數，不論是否有呼叫應用程式**SQLSetStmtAttr**設 APD 中的 SQL_DESC_ARRAY_SIZE 欄位。 如果 SQL_DESC_ARRAY_SIZE 尚未設定，驅動程式管理員必須確定此變數包含在傳回從之前的值 1 **SQLExecDirect**或**SQLExecute**。  
  
## <a name="error-handling"></a>錯誤處理  
 在 ODBC 3。*x*，則呼叫**SQLFetch**或**SQLFetchScroll**於其中填入在 IRD 和指定的診斷記錄的 SQL_DIAG_ROW_NUMBER 欄位 SQL_DESC_ARRAY_STATUS_PTR包含這個記錄相關之資料列集的資料列數目。 使用這種情況，應用程式可以將相互關聯的錯誤訊息與給定資料列位置。  
  
 ODBC 2。*x*驅動程式將無法提供這項功能。 不過，它會提供與 SQLSTATE 01S01 錯誤分界 （資料列中的錯誤）。 ODBC 3。*x*正在使用應用程式**SQLFetch**或**SQLFetchScroll**時將對 ODBC 2。*x*驅動程式必須瞭解這個情況。 也請注意，這類應用程式將無法呼叫**SQLGetDiagField**實際上還是取得 SQL_DIAG_ROW_NUMBER 欄位。 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式將無法呼叫**SQLGetDiagField**只能搭配*Sqlgetdiagfield* SQL_DIAG_MESSAGE_TEXT、 SQL_DIAG_NATIVE、 SQL_DIAG_RETURNCODE 或 SQL_DIAG_ 的引數SQLSTATE。 ODBC 3 *.x*驅動程式管理員會使用 ODBC 2 時，維護診斷資料結構。*x*驅動程式，但是 ODBC 2。*x*驅動程式會傳回只這四個欄位。  
  
 當 ODBC 2。*x*應用程式使用 ODBC 2。*x*驅動程式，如果作業可能會導致多個錯誤，傳回由驅動程式管理員，不同的錯誤可能會傳回 ODBC 3 *.x*比 ODBC 2 的驅動程式管理員。*x*驅動程式管理員。  
  
## <a name="mappings-for-bookmark-operations"></a>書籤作業的對應  
 ODBC 3 *.x*驅動程式管理員執行下列的對應時 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式會在執行書籤的作業。  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLBindCol**繫結至資料行 0 *fCType*等於 SQL_C_VARBOOKMARK，ODBC 3 *.x*驅動程式管理員會檢查是否*Columnsize*引數小於 4 或大於 4，而如果是的話，會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度）。 如果*Columnsize*引數等於 4，驅動程式管理員呼叫**SQLBindCol**驅動程式，來取代之後*fCType* SQL_C_BOOKMARK 與。  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLColAttribute**與*ColumnNumber*引數設定為 0，則驅動程式管理員會傳回*FieldIdentifier*值下表所列。  
  
|*FieldIdentifier*|Value|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (空字串)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|所傳回的相同值**SQLNumResultCols**|  
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
|SQL_DESC_UNNAMED|SQL_UNNAMED 時|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLDescribeCol**與*ColumnNumber*引數設定為 0，驅動程式管理員會傳回下表所列的值。  
  
|緩衝區|Value|  
|------------|-----------|  
|ColumnName|"" (空字串)|  
|* NameLengthPtr|0|  
|* DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|* DecimalDigitsPtr|0|  
|* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式會進行下列呼叫**SQLGetData**擷取書籤：  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 呼叫對應至**SQLGetStmtOption**與*fOption*的 SQL_GET_BOOKMARK，如下所示：  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 其中*hstmt*和*pvParam*設定中的值為*StatementHandle*和*TargetValuePtr*分別。 書籤所指向之緩衝區中傳回*pvParam* (*TargetValuePtr*) 引數。 在緩衝區中的值所指向*StrLen_or_IndPtr*引數在呼叫**SQLGetData**設為 4。  
  
 此對應是必要的情況中的帳戶**SQLFetch**呼叫之前已呼叫**SQLGetData**和 ODBC 2。*x*驅動程式不支援**SQLExtendedFetch**。 在此情況下， **SQLFetch**會傳遞到 ODBC 2。*x*驅動程式，不會支援案例的書籤擷取是。  
  
 **SQLGetData** ODBC 2 中無法多次呼叫。*x*驅動程式擷取因此呼叫組件中的書籤**SQLGetData**與*Columnsize*引數設定為小於 4 的值和*ColumnNumber*引數設定為 0 會傳回 SQLSTATE HY090 （無效的字串或緩衝區長度）。 **SQLGetData** ，不過，可以擷取同一個書籤的多次呼叫。  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 當 ODBC 3。*x*應用程式使用 ODBC 2。*x*驅動程式呼叫**SQLSetStmtAttr**設 SQL_UB_VARIABLE SQL_ATTR_USE_BOOKMARKS 屬性，驅動程式管理員將屬性設定為基礎的 ODBC 2 中 SQL_UB_ON。*x*驅動程式。
