---
title: 使用 SQLBulk 操作更新數據 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b96e3a43b8385910e4260cf51dea7e4ff508200
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298482"
---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新資料
應用程式可以在資料來源的基礎表上執行批次更新、刪除、提取或插入操作,並呼叫**SQLBulk 操作**。 調用**SQLBulk 操作**是建構和執行 SQL 語句的便捷替代方法。 它允許 ODBC 驅動程式支援定位更新,即使資料來源不支援定位 SQL 語句也是如此。 它是通過函數調用實現完整資料庫存取模式的一部分。  
  
 **SQLBulk操作**在當前行集中運行,只能在調用**SQLFetch**或**SQLFetchScroll**後使用。 應用程式通過緩存其書籤指定要更新、刪除或刷新的行。 驅動程式從行集緩衝區檢索要更新的行的新數據,或將新數據插入到基礎表中。  
  
 **SQLBulk操作**要使用的行集大小由調用**SQLSetStmtAttr**設置,*屬性*參數為 SQL_ATTR_ROW_ARRAY_SIZE。 SQLSetPos ( 只有呼叫**SQLFetch**或**SQLFetchScroll**後使用新的行集大小 ) 不同, **SQLBulk 操作**在呼叫**SQLSetStmtAttr**後使用新的行集大小 。 **SQLSetPos**  
  
 由於與關係資料庫的大多數交互都是通過 SQL 完成的,因此**SQLBulk 操作**不受廣泛支援。 但是,驅動程式可以通過構造和執行**更新**、**刪除**或**INSERT**語句來輕鬆類比它。  
  
 要確定**SQLBulk 操作**支援的操作,應用程式使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1資訊選項(取決於游標的類型)調用**SQLGetInfo。**  
  
 此章節包含下列主題。  
  
-   [使用 SQLBulkOperations 依書籤更新資料列](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 依書籤刪除資料列](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入資料列](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 擷取資料列](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
