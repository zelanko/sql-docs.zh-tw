---
title: SQLSetPos 以更新資料列集中的資料列 |Microsoft 文件
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
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating rows
ms.assetid: d83a8c2a-5aa8-4f19-947c-79a817167ee1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5e971d597178501ecc7107da4bbaeb6158f0c99
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>SQLSetPos 以更新資料列集中的資料列
更新作業的**SQLSetPos** ，使得資料來源更新一或多個選取的資料列的資料表中，使用資料應用程式緩衝區中，每個繫結資料行 （除非長度/指標緩衝區中的值是 SQL_COLUMN_IGNORE）。 未繫結的資料行不會更新。  
  
 若要更新的資料列**SQLSetPos**，應用程式會進行下列作業：  
  
1.  將新的資料值放在緩衝區資料列集。 如需有關如何以傳送長資料與詳細**SQLSetPos**，請參閱[Long 資料和 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的資料或 SQL_NTS 的位元組長度。  
  
3.  設定中的值不是要更新 SQL_COLUMN_IGNORE 為這些資料行的長度/指標緩衝區。 雖然應用程式可以略過此步驟，並重新傳送現有資料，這樣沒有效率，而且風險值傳送至已截斷時讀取資料來源。  
  
4.  呼叫**SQLSetPos**與*作業*設 SQL_UPDATE 和*RowNumber*設要更新的資料列數。 如果*RowNumber*是 0，則會更新資料列集中的所有資料列。  
  
 之後**SQLSetPos**傳回目前的資料列設定為更新的資料列。  
  
 更新資料列集的所有資料列時 (*RowNumber*等於 0)，應用程式可以停用特定的資料列的更新設定的資料列作業陣列 （由 SQL_ATTR_ROW_OPERATION_PTR 指向對應項目陳述式屬性） 至 SQL_ROW_IGNORE。 資料列作業陣列對應的大小和資料列狀態陣列 （由指向 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性） 的項目數目。 若要更新資料列結果集已順利擷取和從資料列集已被刪除，應用程式會使用從函式的資料列作業陣列中提取資料列集的資料列狀態陣列**SQLSetPos**.  
  
 傳送至資料來源，以更新每個資料列，應用程式緩衝區應該有有效的資料列資料。 如果應用程式緩衝區填滿所擷取，而且已受到維護資料列狀態陣列，其在每個資料列位置的值不應該為 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 例如，下列程式碼允許使用者捲動 Customers 資料表並更新、 刪除或加入新的資料列。 就會將新的資料中的資料列集緩衝區，然後再呼叫**SQLSetPos**以更新或加入新的資料列。 配置額外的資料列結尾的資料列集的緩衝區來容納新資料列;這可避免緩衝區中放置新的資料列的資料時覆寫現有的資料。  
  
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
