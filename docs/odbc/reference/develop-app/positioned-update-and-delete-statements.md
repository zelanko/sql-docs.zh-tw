---
title: 定位的 Update 和 Delete 陳述式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- data updates [ODBC], positioned update or delete
- positioned updates [ODBC]
- updating data [ODBC], positioned update or delete
ms.assetid: 0eafba50-02c7-46ca-a439-ef3307b935dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3cf60ccc0e220850f7a83ed2c25db3795c1e7796
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312493"
---
# <a name="positioned-update-and-delete-statements"></a>定點更新和刪除陳述式
應用程式可以更新或刪除目前的資料列結果集定位的 update 或 delete 陳述式。 定位的 update 和 delete 陳述式都受到某些資料來源，但並非全部。 若要判斷是否位於資料來源支援更新，以及 delete 陳述式，呼叫應用程式**SQLGetInfo**搭配 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1*資訊類型*（取決於資料指標類型）。 請注意，ODBC 資料指標程式庫會模擬定位的 update 和 delete 陳述式。  
  
 若要使用定位的 update 或 delete 陳述式，應用程式必須建立結果集**選取用於更新**陳述式。 此陳述式的語法是：  
  
 **SELECT** [**ALL** &#124; **DISTINCT**] *select-list*  
  
 **從** *資料表參考清單*  
  
 [**何處** *搜尋條件*]  
  
 **FOR UPDATE OF** [*資料行名稱*[**，** *資料行名稱*]...]  
  
 接著，應用程式會將游標置於要更新或刪除的資料列。 它可以執行這項操作藉由呼叫**SQLFetchScroll**擷取資料列集包含所需的資料列，然後呼叫**SQLSetPos**將資料列集資料指標置於該資料列上。 接著，應用程式不同的陳述式，比使用結果集的陳述式上，執行定位的 update 或 delete 陳述式。 這些陳述式的語法是：  
  
 **更新** *資料表名稱*  
  
 **設定** *資料行識別碼*  **=** {*運算式* &#124; **NULL**}  
  
 [**，** *資料行識別碼*  **=** {*運算式* &#124; **NULL**}]...  
  
 **WHERE CURRENT OF** *資料指標名稱*  
  
 **DELETE FROM** *資料表名稱* **WHERE CURRENT OF** *資料指標名稱*  
  
 請注意，這些陳述式需要資料指標名稱。 應用程式可以指定資料指標名稱，與**SQLSetCursorName**執行建立結果的陳述式設定，或可以自動讓資料來源之前先建立資料指標時產生資料指標名稱。 在後者的情況下，應用程式會擷取此資料指標名稱，以用於定位的 update 和 delete 陳述式藉由呼叫**SQLGetCursorName**。  
  
 例如，下列程式碼可讓使用者捲動 [客戶] 資料表並刪除客戶資料錄或更新其地址和電話號碼。 它會呼叫**SQLSetCursorName**來指定資料指標名稱，然後才會建立客戶的結果集，並使用三個陳述式控制代碼： *hstmtCust*針對結果集*hstmtUpdate*定位的 update 陳述式，並*hstmtDelete*定位的 delete 陳述式。 雖然程式碼可以將不同的變數繫結至定位的 update 陳述式的參數，它會更新資料列集的緩衝區，並將這些緩衝區的元素繫結。 這可防止與更新的資料同步處理的資料列集緩衝區。  
  
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
