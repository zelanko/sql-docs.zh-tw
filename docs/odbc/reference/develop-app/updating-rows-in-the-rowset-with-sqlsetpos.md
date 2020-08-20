---
description: 使用 SQLSetPos 更新資料列集中的資料列
title: 使用 SQLSetPos 更新資料列集中的資料列 |Microsoft Docs
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
ms.openlocfilehash: d1b1b50007a03ee1973d92acafbe8f2be1022f52
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471213"
---
# <a name="updating-rows-in-the-rowset-with-sqlsetpos"></a>使用 SQLSetPos 更新資料列集中的資料列
**SQLSetPos**的更新作業會讓資料來源更新資料表的一或多個選取的資料列，並使用每個系結資料行的應用程式緩衝區中的資料 (除非長度/指標緩衝區中的值 SQL_COLUMN_IGNORE) 。 不會更新未系結的資料行。  
  
 若要使用 **SQLSetPos**來更新資料列，應用程式會執行下列動作：  
  
1.  將新的資料值放在資料列集緩衝區中。 如需有關如何使用 **SQLSetPos**傳送長資料的詳細資訊，請參閱 [Long data And SQLSetPos and SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
2.  視需要設定每個資料行的長度/指標緩衝區中的值。 這是系結至字串緩衝區之資料行的資料或 SQL_NTS 的位元組長度、系結至二進位緩衝區的資料行之資料的位元組長度，以及要設定為 Null 之任何資料行的 SQL_Null_DATA。  
  
3.  在這些資料行的長度/指標緩衝區中設定值，這些資料行不會更新為 SQL_COLUMN_IGNORE。 雖然應用程式可以略過此步驟並重新傳送現有的資料，但在讀取資料時，將值傳送至資料來源的風險並不高。  
  
4.  會呼叫 **SQLSetPos** ，並將 *Operation* 設定為 SQL_UPDATE，並將 *RowNumber* 設定為要更新的資料列編號。 如果 *RowNumber* 是0，則會更新資料列集中的所有資料列。  
  
 **SQLSetPos**傳回之後，會將目前的資料列設定為更新的資料列。  
  
 更新資料列集的所有資料列時 (*RowNumber* 等於 0) ，應用程式可以藉由將 SQL_ATTR_ROW_OPERATION_PTR 語句屬性) 所指向的資料列作業 (陣列的對應元素設定為 SQL_ROW_IGNORE，來停用特定資料列的更新。 資料列作業陣列會對應到資料列狀態陣列 (所指向之資料列狀態陣列的大小和數目（由 SQL_ATTR_ROW_STATUS_PTR 語句屬性) 所指向）。 若只要更新結果集中成功提取的資料列，而且尚未從資料列集刪除資料列集，應用程式會使用提取資料列集的函式的資料列狀態陣列，作為要 **SQLSetPos**的資料列作業陣列。  
  
 針對以更新的形式傳送到資料來源的每個資料列，應用程式緩衝區應該有有效的資料列資料。 如果應用程式緩衝區是藉由提取來填滿，且資料列狀態陣列已維持，則在這些資料列位置的值不應為 SQL_ROW_DELETED、SQL_ROW_ERROR 或 SQL_ROW_NOROW。  
  
 例如，下列程式碼可讓使用者在 Customers 資料表中滾動，以及更新、刪除或加入新的資料列。 它會在呼叫 **SQLSetPos** 來更新或加入新的資料列之前，將新的資料放在資料列集緩衝區中。 在資料列集緩衝區的結尾配置額外的資料列來保存新的資料列;這可防止在將新資料列的資料放入緩衝區時，覆寫現有的資料。  
  
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
