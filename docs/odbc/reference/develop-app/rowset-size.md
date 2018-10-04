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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 132ee99180595dca5e203a6821c5f87aa616530d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47695216"
---
# <a name="rowset-size"></a>資料列集大小
若要使用哪一個資料列集大小取決於應用程式。 以螢幕為基礎的應用程式通常會遵循兩種策略的其中一個。 第一個是將資料列集大小設定為畫面; 上所顯示的資料列數目如果使用者重新調整大小的螢幕，應用程式會據以變更資料列集大小。 第二個是將資料列集大小較大的數字，例如 100，可減少需要的資料來源的呼叫。 應用程式內的資料列集時可能在本機上捲動，並提取新的資料列，它將捲動超出資料列集時，才。  
  
 其他應用程式，例如報表通常會設為 最大數目的應用程式可以合理地處理的資料列的資料列集大小，具有較大的資料列集，有時降低網路負荷每個資料列。 完全大資料列集可以是取決於每個資料列和可用的記憶體數量的大小。  
  
 資料列集大小設定藉由呼叫**SQLSetStmtAttr**具有*屬性*引數 SQL_ATTR_ROW_ARRAY_SIZE。 應用程式可以變更資料列集大小、 將新的資料列集緩衝區繫結 (藉由呼叫**SQLBindCol**或指定的繫結位移) 甚至已經提取資料列之後，或兩者。 變更資料列集大小的影響取決於函式：  
  
-   **SQLFetch**並**SQLFetchScroll**當時的呼叫中使用資料列集大小，以判斷要擷取多少資料列。 不過， **SQLFetchScroll**具有*Sqlfetchscroll* SQL_FETCH_NEXT 遞增的資料指標基礎然後提取與前一個擷取的資料列集上根據目前的資料列集大小的資料列集。  
  
-   **SQLSetPos**會使用資料列集大小正在作用中自上述呼叫起**SQLFetch**或**SQLFetchScroll**，因為**SQLSetPos**資料列集上運作已設定的。 **SQLSetPos**也會挑選新的資料列集大小如果**SQLBulkOperations**已呼叫之後的資料列集大小已變更。  
  
-   **SQLBulkOperations**會使用資料列集大小作用中時呼叫，因為它會執行獨立於任何已擷取的資料列集資料表上的作業。
