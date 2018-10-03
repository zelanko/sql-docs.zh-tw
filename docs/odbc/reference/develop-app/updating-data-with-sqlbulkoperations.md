---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 958514adc02452cdc75a05e7ad28cd31f4e8e0e6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47723406"
---
# <a name="updating-data-with-sqlbulkoperations"></a>使用 SQLBulkOperations 更新資料
應用程式可以執行大量更新、 刪除、 提取時或插入作業，在資料來源，藉由呼叫基礎資料表上的**SQLBulkOperations**。 呼叫**SQLBulkOperations**是方便的替代建構及執行 SQL 陳述式。 它可讓 ODBC 驅動程式支援定位的更新，即使資料來源不支援定位的 SQL 陳述式。 它是達到完整的資料庫存取透過函式呼叫範例的一部分。  
  
 **SQLBulkOperations**目前的資料列集上運作，且可以呼叫之後，才能使用**SQLFetch**或是**SQLFetchScroll**。 應用程式會指定要更新、 刪除或重新整理快取其書籤的資料列。 驅動程式會擷取新的資料列被更新或基礎資料表，資料列集的緩衝區中要插入新的資料。  
  
 資料列集大小，以供**SQLBulkOperations**呼叫設定**SQLSetStmtAttr**具有*屬性*引數 SQL_ATTR_ROW_ARRAY_SIZE。 不同於**SQLSetPos**，只有在呼叫之後使用新的資料列集大小**SQLFetch**或是**SQLFetchScroll**， **SQLBulkOperations**使用若要在呼叫之後的新資料列集大小**SQLSetStmtAttr**。  
  
 與關聯式資料庫的大部分互動都會透過 SQL，因為**SQLBulkOperations**尚未廣泛支援。 不過，驅動程式可以輕鬆地模擬它建構及執行**更新**，**刪除**，或**插入**陳述式。  
  
 若要判斷哪些作業**SQLBulkOperation**支援，應用程式會呼叫**SQLGetInfo**搭配 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊 （取決於資料指標類型） 選項。  
  
 此章節包含下列主題。  
  
-   [使用 SQLBulkOperations 依書籤更新資料列](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 依書籤刪除資料列](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 插入資料列](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [使用 SQLBulkOperations 擷取資料列](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
