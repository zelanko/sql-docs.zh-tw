---
title: "依書籤的資料列更新為與 SQLBulkOperations |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ODBC], bookmarks
- SQLBulkOperations function [ODBC], updating rows
- data updates [ODBC], SQLBulkOperations
- bookmarks [ODBC]
- updating data [ODBC], bookmarks
- updating data [ODBC], SQLBulkOperations
ms.assetid: c9ad82b7-8dba-45b0-bdb9-f4668b37c0d6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c626472dd121d39ae01ac90824a7977587401944
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="updating-rows-by-bookmark-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新資料列的書籤
當更新的資料列的書籤， **SQLBulkOperations**可更新之資料表的一個或多個資料列的資料來源。 資料列識別的繫結的書籤資料行中的書籤。 資料列會更新每個繫結資料行 （除非資料行的長度/指標緩衝區中的值是 SQL_COLUMN_IGNORE） 使用應用程式緩衝區中的資料。 未繫結的資料行不會更新。  
  
 若要更新資料列的書籤**SQLBulkOperations**，應用程式：  
  
1.  擷取和快取要更新的所有資料列的書籤。 如果有多個書籤，並且使用資料行取向的繫結，這些書籤會儲存在陣列;如果有多個書籤，並且使用資料列取向的繫結，這些書籤會儲存在資料列結構的陣列。  
  
2.  將 SQL_ATTR_ROW_ARRAY_SIZE 陳述式屬性設定為書籤的數目，並繫結包含書籤值或資料行 0 的書籤，陣列的緩衝區。  
  
3.  將新的資料值放在緩衝區資料列集。 如需有關如何以傳送長資料與詳細**SQLBulkOperations**，請參閱[Long 資料和 SQLSetPos SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)。  
  
4.  必要時，每個資料行的長度/指標緩衝區中設定的值。 這是繫結至字串緩衝區的資料繫結至二進位緩衝區和 SQL_NULL_DATA 的任何資料行設為 NULL 的資料行的位元組長度的資料行的資料或 SQL_NTS 的位元組長度。  
  
5.  不要將更新為 SQL_COLUMN_IGNORE 這些資料行的長度/指標緩衝區中設定的值。 雖然應用程式可以略過此步驟，並重新傳送現有資料，這樣沒有效率，而且風險值傳送至已截斷時讀取資料來源。  
  
6.  呼叫**SQLBulkOperations**與*作業*引數設定為 SQL_UPDATE_BY_BOOKMARK。  
  
 傳送至資料來源，以更新每個資料列，應用程式緩衝區應該有有效的資料列資料。 如果應用程式緩衝區已填滿所擷取，如果資料列狀態陣列已受到維護，而且資料列狀態值是 SQL_ROW_DELETED、 SQL_ROW_ERROR 或 SQL_ROW_NOROW，無效的資料可能不小心傳送至資料來源。
