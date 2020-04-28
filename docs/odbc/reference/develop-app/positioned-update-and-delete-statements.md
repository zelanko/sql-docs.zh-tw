---
title: 定位 Update 和 Delete 語句 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6e5316bee7057b30eace326b3ca82b30b75741fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282359"
---
# <a name="positioned-update-and-delete-statements"></a>定點更新和刪除陳述式
應用程式可以使用定位 update 或 delete 語句來更新或刪除結果集中目前的資料列。 某些資料來源支援定位的 update 和 delete 語句，但並非全部。 若要判斷資料來源是否支援定位 update 和 delete 語句，應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 *InfoType* （視游標的類型而定）來呼叫**SQLGetInfo** 。 請注意，ODBC 資料指標程式庫會模擬定位的 update 和 delete 語句。  
  
 若要使用定位的 update 或 delete 語句，應用程式必須使用**SELECT FOR update**語句來建立結果集。 此語句的語法為：  
  
 **選取**[**所有**&#124;**相異**]*選取清單*  
  
 **從***資料表參考清單*  
  
 [**WHERE** *搜尋條件*]  
  
 **針對**[資料*行名稱*[，資料 **,** *行名稱*] 的更新]  
  
 然後，應用程式會將資料指標置於要更新或刪除的資料列上。 它可以藉由呼叫**SQLFetchScroll**來抓取包含所需資料列的資料列集，並呼叫**SQLSetPos**將資料列集資料指標放置在該資料列上，來達到此目的 然後，應用程式會在不同的語句上執行定位的 update 或 delete 語句，而不是結果集所使用的語句。 這些語句的語法如下：  
  
 **更新***資料表-名稱*  
  
 **設定**資料*行識別碼* **=** {*expression* &#124; **Null**}  
  
 [**，** 資料*行識別碼* **=** {*expression* &#124; **Null**}] .。。  
  
 **其中目前的**資料*指標名稱*  
  
 **從***資料表名稱*中刪除**目前的**資料*指標名稱*  
  
 請注意，這些語句需要資料指標名稱。 應用程式可以在執行用來建立結果集的語句之前，使用**SQLSetCursorName**來指定資料指標名稱，或可讓資料來源在建立資料指標時自動產生資料指標名稱。 在後者的情況下，應用程式會藉由呼叫**SQLGetCursorName**，抓取這個資料指標名稱以用於定位 update 和 delete 語句。  
  
 例如，下列程式碼可讓使用者流覽 Customers 資料表，並刪除客戶記錄或更新其位址和電話號碼。 它會呼叫**SQLSetCursorName**來指定資料指標名稱，然後再建立客戶的結果集，並使用三個語句控制碼：結果集的*hstmtCust* 、用於定位 update 語句的*hstmtUpdate* ，以及*hstmtDelete*的定位 delete 語句。 雖然程式碼可以將不同的變數系結至定位 update 語句中的參數，但它會更新資料列集緩衝區，並系結這些緩衝區的元素。 這會讓資料列集緩衝區與更新的資料保持同步。  
  
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
