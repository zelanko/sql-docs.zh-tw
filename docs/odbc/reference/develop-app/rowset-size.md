---
title: 行集大小 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304239"
---
# <a name="rowset-size"></a>資料列集大小
要使用的行集大小取決於應用程式。 基於螢幕的應用程式通常遵循兩種策略之一。 第一種是將排組大小設置為螢幕上顯示的行數;第二種是將行集大小設置為螢幕上顯示的行數。如果使用者調整螢幕大小,應用程式將相應地更改行集大小。 第二種是將排組大小設置為較大的數位,如 100,從而減少對數據源的調用數。 應用程式盡可能在行集中內本地滾動,並且僅在在行集外滾動時提取新行。  
  
 其他應用程式(如報表)傾向於將行集大小設置為應用程式可以合理處理的最大行數 - 如果行集越大,每行的網路開銷有時會降低。 行集的確切大小取決於每行的大小和可用的記憶體量。  
  
 行集大小由對**SQLSetStmtAttr**的調用設置,*屬性*參數為SQL_ATTR_ROW_ARRAY_SIZE。 應用程式可以更改列集大小、綁定新的行集緩衝區(通過調用**SQLBindCol**或指定綁定偏移),即使在已提取行後,也可以同時同時獲取兩者。 變更列集大小的含義取決於函數:  
  
-   **SQLFetch**和**SQLFetchScroll**在調用時使用行集大小來確定要提取的行數。 但是,具有SQL_FETCH_NEXT*提取方向*的**SQLFetchScroll**會根據上一個提取的行集增加游標,然後根據當前行集大小獲取行集。  
  
-   **SQLSetPos**使用上述對**SQLFetch**或**SQLFetchScroll**調用時有效的行集大小,因為**SQLSetPos**對已設置的行集進行了操作。 如果在更改列集大小後調用**了 SQLBulk 操作****,SQLSetPos**也將拾取新的行集大小。  
  
-   **SQLBulk操作**在調用時使用有效的行集大小,因為它對表執行操作,而獨立於任何提取的行集。
