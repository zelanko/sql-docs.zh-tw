---
description: 使用 SQLBulkOperations 更新資料
title: 使用 SQLBulkOperations 更新資料 |Microsoft Docs
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
ms.openlocfilehash: 6c8626a0925d0f30792ed92332c0f96efd23f62e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465532"
---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新資料
應用程式可以呼叫 **SQLBulkOperations**，在資料來源的基礎資料表上執行大量更新、刪除、提取或插入作業。 呼叫 **SQLBulkOperations** 是用來建立和執行 SQL 語句的方便替代方法。 它可讓 ODBC 驅動程式支援定點更新，即使資料來源不支援定位的 SQL 語句。 它是透過函式呼叫達成完整資料庫存取的典範的一部分。  
  
 **SQLBulkOperations** 會在目前的資料列集上運作，而且只能在呼叫 **SQLFetch** 或 **SQLFetchScroll**之後使用。 應用程式會藉由快取書簽來指定要更新、刪除或重新整理的資料列。 驅動程式會從資料列集緩衝區抓取要更新之資料列的新資料，或要插入基礎資料表的新資料。  
  
 **SQLBulkOperations**所使用的資料列集大小是由具有 SQL_ATTR_ROW_ARRAY_SIZE 之*屬性*引數的**SQLSetStmtAttr**呼叫所設定。 不同于 **SQLSetPos**，它只會在呼叫 **SQLFetch** 或 **SQLFetchScroll**之後使用新的資料列集大小， **SQLBulkOperations** 會在呼叫 **SQLSetStmtAttr**之後使用新的資料列集大小。  
  
 由於大部分與關係資料庫的互動都是透過 SQL 來完成，因此不會廣泛支援 **SQLBulkOperations** 。 不過，驅動程式可以藉由建立及執行 **UPDATE**、 **DELETE**或 **INSERT** 語句，輕鬆地模擬它。  
  
 為了判斷 **SQLBulkOperation** 支援哪些作業，應用程式會使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊選項來呼叫 **SQLGetInfo** ， (視資料指標) 的類型而定。  
  
 此章節包含下列主題。  
  
-   [使用 SQLBulkOperations 依書籤更新資料列](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 依書籤刪除資料列](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入資料列](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 擷取資料列](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
