---
title: 使用 SQLBulk 操作按書籤更新行 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c755297e8beadad92b5be81d78ca534bb96ecae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283196"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤更新資料列
按書籤更新行時 **,SQLBulk操作**使數據源更新表的一行或多行。 行由綁定書簽列中的書籤標識。 行使用每個綁定列的應用程式緩衝區中的數據進行更新(除非列的長度/指標緩衝區中的值SQL_COLUMN_IGNORE)。 未綁定列將不會更新。  
  
 要使用**SQLBulk 操作**按書籤更新行,應用程式:  
  
1.  檢索並緩存要更新的所有行的書籤。 如果有多個書籤和按列綁定,則書簽存儲在陣列中;如果使用多個書籤和按列綁定,則書籤將存儲在陣列中。如果有多個書籤和逐行綁定,則書簽存儲在行結構陣組中。  
  
2.  將SQL_ATTR_ROW_ARRAY_SIZE語句屬性設置為書籤數,並將包含書籤值的緩衝區或書籤陣列綁定到列 0。  
  
3.  將新的數據值放在行集緩衝區中。 有關如何使用**SQLBulk 操作**傳送長資料的資訊,請參閱[長資料和 SQLSetPos 和 SQLBulk 操作](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  根據需要設置每列的長度/指示器緩衝區中的值。 這是數據或SQL_NTS的位元組長度,用於綁定到字串緩衝區的列、綁定到二進位緩衝區的列的數據字節長度,以及要設置為NULL的任何列SQL_NULL_DATA。  
  
5.  設置不更新為SQL_COLUMN_IGNORE列的長度/指示器緩衝區中的值。 儘管應用程式可以跳過此步驟並重新發送現有數據,但這效率低下,並且可能會將值發送到讀取時被截斷的數據源。  
  
6.  呼叫**SQLBulk 操作**,*操作*參數設定為SQL_UPDATE_BY_BOOKMARK。  
  
 對於作為更新發送到數據源的每一行,應用程式緩衝區應具有有效的行數據。 如果通過提取填充應用程式緩衝區,則如果已維護行狀態陣列,並且行的狀態值為SQL_ROW_DELETED、SQL_ROW_ERROR 或SQL_ROW_NOROW,則無效數據可能會無意中發送到數據源。
