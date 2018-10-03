---
title: 使用 SQLBulkOperations 更新資料列的書籤 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e9f0c59324542793301965c7d3555cf35ad40f5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47653082"
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 依書籤更新資料列
依書籤，更新資料列時**SQLBulkOperations** ，使得更新的資料表的一個或多個資料列的資料來源。 資料列識別的繫結的書籤資料行中的書籤。 資料列會更新每個繫結資料行 （除非資料行的長度/指標緩衝區中的值是 SQL_COLUMN_IGNORE） 使用應用程式緩衝區中的資料。 未繫結的資料行不會更新。  
  
 若要更新資料列所使用的書籤**SQLBulkOperations**，應用程式：  
  
1.  擷取及快取要更新的所有資料列的書籤。 如果有一個以上的書籤，而且會使用資料行取向的繫結，這些書籤會儲存在陣列中;如果有一個以上的書籤，而且會使用資料列取向的繫結，這些書籤會儲存在資料列結構的陣列中。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為書籤的數目並繫結包含書籤值或資料行 0 的書籤，陣列的緩衝區。  
  
3.  將新的資料值放在資料列集的緩衝區中。 如需如何將長資料與傳送**SQLBulkOperations**，請參閱[長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是 sql_nts; 之資料的繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的位元組長度。  
  
5.  設定中的值不是要更新為 SQL_COLUMN_IGNORE 這些資料行的長度/指標緩衝區。 雖然應用程式可以略過此步驟，並重新傳送現有資料，這會沒有效率，而且有風險將值傳送到已截斷時讀取的資料來源。  
  
6.  呼叫**SQLBulkOperations**具有*作業*引數設定為 SQL_UPDATE_BY_BOOKMARK。  
  
 傳送至資料來源，以更新每個資料列，應用程式緩衝區應該有有效的資料列的資料。 如果應用程式緩衝區已填滿由提取時，如果資料列狀態陣列已受到維護，而且資料列的值是 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW，無效的資料可能不小心傳送至資料來源。
