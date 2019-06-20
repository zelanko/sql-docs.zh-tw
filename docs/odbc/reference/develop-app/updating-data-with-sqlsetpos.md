---
title: 使用 SQLSetPos 更新資料 |Microsoft Docs
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
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1c31ef622281b4f52f62ca3867c5afa7dcae8ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194422"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新資料
應用程式可更新或刪除任何資料列與資料列集中**SQLSetPos**。 呼叫**SQLSetPos**是方便的替代建構及執行 SQL 陳述式。 它可讓 ODBC 驅動程式支援定位的更新，即使資料來源不支援定位的 SQL 陳述式。 它是達到完整的資料庫存取透過函式呼叫範例的一部分。  
  
 **SQLSetPos**目前的資料列集上運作，且可以呼叫之後，才能使用**SQLFetchScroll**。 應用程式指定要更新、 刪除或插入的資料列的數目和驅動程式會將新的資料，該資料列擷取資料列集的緩衝區。 **SQLSetPos**也可用來將指定的資料列指定為目前的資料列，或重新整理資料來源的資料列集中的特定資料列。  
  
 資料列集大小設定藉由呼叫**SQLSetStmtAttr**具有*屬性*引數 SQL_ATTR_ROW_ARRAY_SIZE。 **SQLSetPos**不過，只有在呼叫之後使用新的資料列集大小， **SQLFetch**或是**SQLFetchScroll**。 比方說，如果資料列集大小變更時， **SQLSetPos**呼叫，然後**SQLFetch**或是**SQLFetchScroll**呼叫時，和呼叫**SQLSetPos**會使用舊的資料列集大小，同時**SQLFetch**或是**SQLFetchScroll**會使用新的資料列集大小。  
  
 資料列集中的第一個資料列是資料列號碼 1。 *RowNumber*中的引數**SQLSetPos**必須識別資料列中資料列集; 也就是說，其值必須介於 1 與最近提取的資料列數目 (可能會小於資料列集大小）。 如果*RowNumber*為 0，將作業套用至資料列集中的每個資料列。  
  
 與關聯式資料庫的大部分互動都會透過 SQL，因為**SQLSetPos**尚未廣泛支援。 不過，驅動程式可以輕鬆地模擬它建構及執行**更新**或是**刪除**陳述式。  
  
 若要判斷哪些作業**SQLSetPos**支援，應用程式會呼叫**SQLGetInfo**搭配 SQL_DYNAMIC_CURSOR_ATTRIBUTES1 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 資訊 （取決於資料指標類型） 選項。  
  
 此章節包含下列主題。  
  
-   [使用 SQLSetPos 更新資料列集中的資料列](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 刪除資料列集中的資料列](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
