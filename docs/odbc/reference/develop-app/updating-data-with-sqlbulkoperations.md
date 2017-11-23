---
title: "SQLBulkOperations 以更新資料 |Microsoft 文件"
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
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2bcfa39dca534aaa03fe95293b6143180ac9920
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations 以更新資料
應用程式可以執行大量更新、 刪除、 提取或插入作業，在呼叫資料來源的基礎資料表上**SQLBulkOperations**。 呼叫**SQLBulkOperations**是一個方便的替代方式建構及執行 SQL 陳述式。 它可讓 ODBC 驅動程式支援定位的更新，即使資料來源不支援定位的 SQL 陳述式。 它是透過函式呼叫達成完整的資料庫存取的開發架構的一部分。  
  
 **SQLBulkOperations**目前資料列集上運作，而且可用只有在呼叫之後**SQLFetch**或**SQLFetchScroll**。 應用程式指定要更新、 刪除或重新整理快取其書籤的資料列。 驅動程式會擷取新的資料列被更新或基礎資料表的資料列集緩衝區中要插入新的資料。  
  
 資料列集大小，以供**SQLBulkOperations**設定呼叫**SQLSetStmtAttr**與*屬性*SQL_ATTR_ROW_ARRAY_SIZE 引數。 不同於**SQLSetPos**，只有在呼叫之後使用新的資料列集大小**SQLFetch**或**SQLFetchScroll**， **SQLBulkOperations**使用在呼叫之後的新資料列集大小**SQLSetStmtAttr**。  
  
 因為關聯式資料庫的大部分互動都透過 SQL，完成**SQLBulkOperations**尚未廣泛支援。 不過，驅動程式可以輕鬆地模擬它建構及執行**更新**，**刪除**，或**插入**陳述式。  
  
 若要判斷哪些作業**SQLBulkOperation**支援，應用程式呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊 （取決於資料指標的類型） 選項。  
  
 此章節包含下列主題。  
  
-   [使用 SQLBulkOperations 依書籤更新資料列](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 依書籤刪除資料列](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入資料列](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 擷取資料列](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
