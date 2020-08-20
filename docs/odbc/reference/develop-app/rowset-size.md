---
description: 資料列集大小
title: 資料列集大小 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d915d6e11fc7678312eab60c3316815cfabab38e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465606"
---
# <a name="rowset-size"></a>資料列集大小
要使用的資料列集大小視應用程式而定。 以螢幕為基礎的應用程式通常會遵循兩個策略的其中一種。 第一個是將資料列集大小設定為畫面上顯示的資料列數目;如果使用者調整螢幕的大小，則應用程式會據以變更資料列集大小。 第二個是將資料列集大小設定為較大的數位（例如100），以減少對資料來源的呼叫數目。 應用程式可能的話，會在資料列集內進行本機滾動，而且只會在資料列集外滾動時提取新的資料列。  
  
 其他應用程式（例如報表）通常會將資料列集大小設定為應用程式可合理處理的最大資料列數-使用較大的資料列集時，有時會減少每個資料列的網路負擔。 資料列集的大小取決於每個資料列的大小和可用的記憶體數量。  
  
 使用 SQL_ATTR_ROW_ARRAY_SIZE 的*屬性*引數呼叫**SQLSetStmtAttr**來設定資料列集大小。 應用程式可以變更資料列集大小、透過呼叫 **SQLBindCol** 來系結新的資料列集緩衝區 (或指定系結位移，) 即使在提取資料列之後，或兩者都是如此。 變更資料列集大小的含意取決於函數：  
  
-   **SQLFetch** 和 **SQLFetchScroll** 會在呼叫時使用資料列集大小，以判斷要提取的資料列數目。 不過，具有 SQL_FETCH_NEXT *FetchOrientation*的**SQLFetchScroll**會根據先前提取的資料列集遞增資料指標，然後根據目前的資料列集大小來提取資料列集。  
  
-   **SQLSetPos** 會使用對 **SQLFetch** 或 **SQLFetchScroll**的先前呼叫所生效的資料列集大小，因為 **SQLSetPos** 會在已設定的資料列集上運作。 如果在資料列集大小變更之後呼叫**SQLBulkOperations** ， **SQLSetPos**也會收取新的資料列集大小。  
  
-   **SQLBulkOperations** 會使用在呼叫時生效的資料列集大小，因為它會在與任何提取的資料列集無關的資料表上執行作業。
