---
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
ms.openlocfilehash: 11b95768934f96e1587b3c570b2510f3c2849239
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304239"
---
# <a name="rowset-size"></a>資料列集大小
要使用的資料列集大小取決於應用程式。 以螢幕為基礎的應用程式通常會遵循兩個策略的其中一個。 第一種是將資料列集大小設定為螢幕上顯示的資料列數目;如果使用者調整螢幕大小，應用程式會據以變更資料列集大小。 第二種方式是將資料列集大小設定為較大的數位，例如100，這會減少對資料來源的呼叫次數。 應用程式會在可能的情況下，在資料列集內的本機滾動，並且只會在資料列集外滾動時提取新的  
  
 其他應用程式（例如報表）通常會將資料列集大小設定為應用程式可以合理處理的最大資料列數-使用較大的資料列集時，每個資料列的網路額外負荷有時會減少。 資料列集的確切大小取決於每個資料列的大小，以及可用的記憶體數量。  
  
 資料列集大小是透過 SQL_ATTR_ROW_ARRAY_SIZE 的*屬性*引數呼叫**SQLSetStmtAttr**所設定。 應用程式可以變更資料列集大小、系結新的資料列集緩衝區（藉由呼叫**SQLBindCol**或指定系結位移），即使是在提取資料列之後，或兩者都是。 變更資料列集大小的影響取決於函數：  
  
-   **SQLFetch**和**SQLFetchScroll**會使用呼叫時的資料列集大小來決定要提取的資料列數目。 不過， **SQLFetchScroll**的*FetchOrientation*為 SQL_FETCH_NEXT 會根據先前提取的資料列集來遞增資料指標，然後根據目前的資料列集大小來提取資料列集。  
  
-   **SQLSetPos**會使用從先前的**SQLFetch**或**SQLFetchScroll**呼叫中生效的資料列集大小，因為**SQLSetPos**會在已設定的資料列集上運作。 如果在資料列集大小變更後呼叫了**SQLBulkOperations** ， **SQLSetPos**也會收取新的資料列集大小。  
  
-   **SQLBulkOperations**會在呼叫時使用作用中的資料列集大小，因為它會在與任何提取的資料列集無關的資料表上執行作業。
