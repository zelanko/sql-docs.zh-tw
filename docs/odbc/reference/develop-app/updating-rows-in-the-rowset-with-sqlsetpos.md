---
title: 使用 SQLSetPos 更新行 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4851d4ba741379fc188b2b88c895a378ef3bb80d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298968"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 更新資料列集中的資料列
**SQLSetPos**的更新操作使資料來源使用每個綁定列的應用程式緩衝區中的數據更新表的一個或多個選定行(除非長度/指示器緩衝區中的值SQL_COLUMN_IGNORE)。 未綁定的列將不會更新。  
  
 要使用**SQLSetPos**更新行,應用程式執行以下操作:  
  
1.  將新的數據值放在行集緩衝區中。 有關如何使用**SQLSetPos**傳送長資料的資訊,請參閱[長資料和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  根據需要設置每列的長度/指示器緩衝區中的值。 這是數據或SQL_NTS的位元組長度,用於綁定到字串緩衝區的列、綁定到二進位緩衝區的列的數據字節長度,以及要設置為NULL的任何列SQL_NULL_DATA。  
  
3.  設置不更新為SQL_COLUMN_IGNORE列的長度/指示器緩衝區中的值。 儘管應用程式可以跳過此步驟並重新發送現有數據,但這效率低下,並且可能會將值發送到讀取時被截斷的數據源。  
  
4.  將**SQLSetPos**設置為*Operation*SQL_UPDATE,*行號*設置為要更新的行數。 如果*RowNumber*為 0,則將更新行集中的所有行。  
  
 **SQLSetPos**傳回後,當前行將設置為更新的行。  
  
 更新列集的所有行(*行數*等於 0)時,應用程式可以通過將行操作陣列的相應元素(由SQL_ATTR_ROW_OPERATION_PTR語句屬性指向)設置為SQL_ROW_IGNORE來禁用某些行的更新。 行操作陣列的大小和元素數對應於行狀態陣列(由SQL_ATTR_ROW_STATUS_PTR語句屬性指向)。 要僅更新結果集中成功提取且尚未從行集中刪除的行,應用程式使用從將行集作為行操作陣列獲取為**SQLSetPos**的函數中的行狀態陣列。  
  
 對於作為更新發送到數據源的每一行,應用程式緩衝區應具有有效的行數據。 如果應用程式緩衝區是通過提取填充的,並且已維護行狀態陣列,則不應SQL_ROW_DELETED、SQL_ROW_ERROR或SQL_ROW_NOROW這些行位置的值。  
  
 例如,以下代碼允許使用者滾動流覽"客戶"表並更新、刪除或添加新行。 在調用**SQLSetPos**更新或添加新行之前,它會將新數據放在行集緩衝區中。 在行集緩衝區的末尾分配一個額外的行以容納新行;這樣可以防止將新行的數據放置在緩衝區中時覆蓋現有數據。  
  
```  
#define UPDATE_ROW   100  
#define DELETE_ROW   101  
#define ADD_ROW      102  
  
SQLUINTEGER    CustIDArray[11];  
SQLCHAR        NameArray[11][51], AddressArray[11][51],   
               PhoneArray[11][11];  
SQLINTEGER     CustIDIndArray[11], NameLenOrIndArray[11],   
               AddressLenOrIndArray[11],  
               PhoneLenOrIndArray[11];  
SQLUSMALLINT   RowStatusArray[10], Action, RowNum;  
SQLRETURN      rc;  
SQLHSTMT       hstmt;  
  
// Set the SQL_ATTR_ROW_BIND_TYPE statement attribute to use column-wise   
// binding. Declare the rowset size with the SQL_ATTR_ROW_ARRAY_SIZE   
// statement attribute. Set the SQL_ATTR_ROW_STATUS_PTR statement   
// attribute to point to the row status array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_KEYSET_DRIVEN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_BIND_TYPE, SQL_BIND_BY_COLUMN, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 10, 0);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, RowStatusArray, 0);  
  
// Bind arrays to the CustID, Name, Address, and Phone columns.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, CustIDArray, 0, CustIDIndArray);  
SQLBindCol(hstmt, 2, SQL_C_CHAR, NameArray, sizeof(NameArray[0]), NameLenOrIndArray);  
SQLBindCol(hstmt, 3, SQL_C_CHAR, AddressArray, sizeof(AddressArray[0]),  
            AddressLenOrIndArray);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, PhoneArray, sizeof(PhoneArray[0]),  
            PhoneLenOrIndArray);  
  
// Execute a statement to retrieve rows from the Customers table.  
SQLExecDirect(hstmt, "SELECT CustID, Name, Address, Phone FROM Customers", SQL_NTS);  
  
// Fetch and display the first 10 rows.  
rc = SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
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
         SQLFetchScroll(hstmt, Action, RowNum);  
         DisplayData(CustIDArray, CustIDIndArray,  
                     NameArray, NameLenOrIndArray,  
                     AddressArray, AddressLenOrIndArray,  
                     PhoneArray, PhoneLenOrIndArray, RowStatusArray);  
         break;  
  
      case UPDATE_ROW:  
         // Place the new data in the rowset buffers and update the   
         // specified row.  
         GetNewData(&CustIDArray[RowNum - 1], &CustIDIndArray[RowNum - 1],  
                  NameArray[RowNum - 1], &NameLenOrIndArray[RowNum - 1],  
                  AddressArray[RowNum - 1], &AddressLenOrIndArray[RowNum - 1],  
                  PhoneArray[RowNum - 1], &PhoneLenOrIndArray[RowNum - 1]);  
         SQLSetPos(hstmt, RowNum, SQL_UPDATE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case DELETE_ROW:  
         // Delete the specified row.  
         SQLSetPos(hstmt, RowNum, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
         break;  
  
      case ADD_ROW:  
         // Place the new data in the rowset buffers at index 10.   
         // This is an extra element for new rows so rowset data is   
         // not overwritten. Insert the new row. Row 11 corresponds   
         // to index 10.  
         GetNewData(&CustIDArray[10], &CustIDIndArray[10],  
                     NameArray[10], &NameLenOrIndArray[10],  
                     AddressArray[10], &AddressLenOrIndArray[10],  
                     PhoneArray[10], &PhoneLenOrIndArray[10]);  
         SQLSetPos(hstmt, 11, SQL_ADD, SQL_LOCK_NO_CHANGE);  
         break;  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
