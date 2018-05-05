---
title: 資料列集大小 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0fa3d2feb8bcd3c4c342567e67f403edfb8029a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="rowset-size"></a>資料列集大小
若要使用哪一個資料列集大小取決於應用程式。 螢幕型應用程式通常會遵循兩種策略的其中一個。 第一個方法是將資料列集大小設定為顯示在畫面上的資料列數目如果使用者調整螢幕，應用程式據以變更資料列集大小。 第二個是資料列集大小設定為較大數目，例如 100，這會減少呼叫到資料來源數目。 應用程式會集中的資料列時可能在本機捲動，然後只在它捲動外部資料列集時，才會擷取新資料列。  
  
 其他應用程式，例如報表，通常會設為 最大數目的應用程式可以合理地處理資料列的資料列集大小，較大的資料列集，與每個資料列負擔網路有時會降低。 完全多大的資料列集可以是取決於每個資料列和可用的記憶體數量的大小。  
  
 資料列集大小由呼叫所設定**SQLSetStmtAttr**與*屬性*SQL_ATTR_ROW_ARRAY_SIZE 引數。 應用程式可以變更資料列集大小、 繫結新資料列集的緩衝區 (藉由呼叫**SQLBindCol**或指定的繫結位移) 即使已經提取資料列之後，或兩者。 變更資料列集大小的影響取決於函式：  
  
-   **SQLFetch**和**SQLFetchScroll**在呼叫時使用的資料列集大小，來判斷要擷取多少資料列。 不過， **SQLFetchScroll**與*Sqlfetchscroll*的 SQL_FETCH_NEXT 增量游標根據前一個擷取和然後提取資料列集根據目前的資料列集大小的資料列集。  
  
-   **SQLSetPos**使用為準，呼叫就是作用中的資料列集大小**SQLFetch**或**SQLFetchScroll**，因為**SQLSetPos**對資料列集已設定的。 **SQLSetPos**也將會挑選新的資料列集大小如果**SQLBulkOperations**已呼叫之後的資料列集大小已變更。  
  
-   **SQLBulkOperations**會使用資料列集大小作用中時呼叫，因為它會執行獨立於任何已擷取的資料列集資料表上的作業。
