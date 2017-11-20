---
title: "SQLSetPos 以更新資料 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb89d4a2220c487f2e126b50ecf8cbedd20857cc
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos 以更新資料
應用程式可以更新或刪除任何資料列與資料列集中**SQLSetPos**。 呼叫**SQLSetPos**是一個方便的替代方式建構及執行 SQL 陳述式。 它可讓 ODBC 驅動程式支援定位的更新，即使資料來源不支援定位的 SQL 陳述式。 它是透過函式呼叫達成完整的資料庫存取的開發架構的一部分。  
  
 **SQLSetPos**目前資料列集上運作，而且可用只有在呼叫之後**SQLFetchScroll**。 應用程式指定要更新、 刪除或插入的資料列的數目和驅動程式會從緩衝區資料列集擷取該資料列的新資料。 **SQLSetPos**也可用以將指定的資料列指定為目前的資料列，或重新整理資料來源的資料列集的特定資料列。  
  
 資料列集大小由呼叫所設定**SQLSetStmtAttr**與*屬性*SQL_ATTR_ROW_ARRAY_SIZE 引數。 **SQLSetPos**使用新的資料列集大小，不過，只有在呼叫之後**SQLFetch**或**SQLFetchScroll**。 例如，如果變更資料列集大小， **SQLSetPos**稱為然後**SQLFetch**或**SQLFetchScroll**呼叫時，和呼叫**SQLSetPos**使用舊的資料列集大小，同時**SQLFetch**或**SQLFetchScroll**會使用新的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 *RowNumber*引數中的**SQLSetPos**必須識別資料列中資料列集; 也就是說，其值必須是介於 1 與最近提取的資料列數目 (可能會小於資料列集大小）。 如果*RowNumber*是 0，將作業套用至資料列集中的每個資料列。  
  
 因為關聯式資料庫的大部分互動都透過 SQL，完成**SQLSetPos**尚未廣泛支援。 不過，驅動程式可以輕鬆地模擬它建構及執行**更新**或**刪除**陳述式。  
  
 若要判斷哪些作業**SQLSetPos**支援，應用程式呼叫**SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊 （取決於資料指標的類型） 選項。  
  
 此章節包含下列主題。  
  
-   [SQLSetPos 以更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos 與資料列集刪除資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)

