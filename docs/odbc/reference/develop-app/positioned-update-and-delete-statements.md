---
title: "定位 Update 和 Delete 陳述式 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 45bb604f0226ac05eab0fd99bdbef41704cc8de8
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="positioned-update-and-delete-statements"></a>定位的 Update 和 Delete 陳述式
應用程式可以更新或刪除目前的資料列結果集中的定位更新或刪除陳述式。 定位 update 和 delete 陳述式會受到某些資料來源，但不是全部。 若要判斷是否位於資料來源支援更新和 delete 陳述式時，應用程式呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1*資訊類型*（取決於資料指標的類型）。 請注意，ODBC 資料指標程式庫會模擬定位的 update 和 delete 陳述式。  
  
 若要使用定位的 update 或 delete 陳述式，應用程式必須建立一個結果集**選取更新**陳述式。 此陳述式的語法如下：  
  
 **選取**[**所有**&#124;**DISTINCT**] *select 清單*  
  
 **從***資料表的參考清單*  
  
 [**其中***搜尋條件*]  
  
 **FOR UPDATE OF** [*資料行名稱*[**，** *資料行名稱*]...]  
  
 接著，應用程式會將游標置於要更新或刪除的資料列。 它可以執行這項操作藉由呼叫**SQLFetchScroll**擷取資料列集包含所需的資料列，然後呼叫**SQLSetPos**將資料列集資料指標置於該資料列上。 接著，應用程式上不同的陳述式，比使用結果集的陳述式執行定位的更新或刪除陳述式。 這些陳述式的語法如下：  
  
 **更新***資料表名稱*  
  
 **設定***資料行識別碼*  **=**  {*運算式*&#124;**NULL**}  
  
 [**，** *資料行識別碼*  **=**  {*運算式*&#124;**NULL**}]...  
  
 **WHERE CURRENT OF** *資料指標名稱*  
  
 **DELETE FROM** *資料表名稱* **WHERE CURRENT OF** *資料指標名稱*  
  
 請注意，這些陳述式需要資料指標名稱。 應用程式可以指定資料指標名稱與**SQLSetCursorName**執行陳述式，建立結果集或可以自動讓資料來源之前先建立資料指標時產生資料指標名稱。 在後者的情況下，應用程式會擷取此資料指標名稱，以便用於定位的 update 和 delete 陳述式藉由呼叫**SQLGetCursorName**。  
  
 比方說，下列程式碼可讓使用者捲動 Customers 資料表和刪除客戶記錄或更新其地址和電話號碼。 它會呼叫**SQLSetCursorName**來指定資料指標名稱之前它會建立客戶的結果集，並使用三個陳述式控制代碼,： *hstmtCust*結果集， *hstmtUpdate*定位的 update 陳述式，和*hstmtDelete*定位的 delete 陳述式。 雖然程式碼無法將個別變數繫結至定位的 update 陳述式中的參數，它會更新資料列集緩衝區，並將這些緩衝區元素繫結。 這可防止與更新的資料同步處理的資料列集緩衝區。  
  
```  
#define POSITIONED_UPDATE 100  
#define POSITIONED_DELETE 101  
  
SQLUINTEGER    CustIDArray[10];  
SQLCHAR        NameArray[10][51], AddressArray[10][51],   
               PhoneArray[10][11];  
SQLINTEGER     CustIDIndArray[10], NameLenOrIndArray[10],   
               AddressLenOrIndArray[10],  
               PhoneLenOrIndArray[10];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLHSTMT       hstmtCust, hstmtUpdate, hstmtDelete;  
  
// Set the SQL_ATTR_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmtCust, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmtCust, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmtCust, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]),  
            NameLenOrIndArray);  
SQLBindCol(hstmtCust, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
         AddressLenOrIndArray);  
SQLBindCol(hstmtCust, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Set the cursor name to Cust.  
SQLSetCursorName(hstmtCust, "Cust", SQL_NTS);  
  
// Prepare positioned update and delete statements.  
SQLPrepare(hstmtUpdate,  
   "UPDATE Customers SET Address = ?, Phone = ? WHERE CURRENT OF Cust",  
   SQL_NTS);  
SQLPrepare(hstmtDelete, "DELETE FROM Customers WHERE CURRENT OF Cust", SQL_NTS);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmtCust,  
   "SELECT CustID, Name, Address, Phone FROM Customers FOR UPDATE OF Address, Phone",  
   SQL_NTS);  
  
// Fetch and display the first 10 rows.  
SQLFetchScroll(hstmtCust, SQL_FETCH_NEXT, 0);  
DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray, AddressArray,  
            AddressLenOrIndArray, PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
  
// Call GetAction to get an action and a row number from the user.  
while (GetAction(&Action, &RowNum)) {  
   switch (Action) {  
  
      case SQL_FETCH_NEXT:  
      case SQL_FETCH_PRIOR:  
      case SQL_FETCH_FIRST:  
      case SQL_FETCH_LAST:  
      case SQL_FETCH_ABSOLUTE:  
      case SQL_FETCH_RELATIVE:  
         // Fetch and display the requested data.  
         SQLFetchScroll(hstmtCust, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray, NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray, PhoneArray,  
                     PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case POSITIONED_UPDATE:  
         // Get the new data and place it in the rowset buffers.  
         GetNewData(AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                     PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Bind the elements of the arrays at position RowNum-1 to the   
         // parameters of the positioned update statement.  
         SQLBindParameter(hstmtUpdate, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           50, 0, AddressArray[RowNum - 1], sizeof(AddressArray[0]),  
                           &AddressLenOrIndArray[RowNum - 1]);  
         SQLBindParameter(hstmtUpdate, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                           10, 0, PhoneArray[RowNum - 1], sizeof(PhoneArray[0]),  
                           &PhoneLenOrIndArray[RowNum - 1]);  
  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned update statement to update the row.  
         SQLExecute(hstmtUpdate);  
         break;  
  
      case POSITIONED_DELETE:  
         // Position the rowset cursor. The rowset is 1-based.  
         SQLSetPos(hstmtCust, RowNum, SQL_POSITION, SQL_LOCK_NO_CHANGE);  
  
         // Execute the positioned delete statement to delete the row.  
         SQLExecute(hstmtDelete);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmtCust);  
```
