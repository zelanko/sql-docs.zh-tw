---
title: "書籤 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 791350c93e2570ad8615e5b378e9979870e02acf
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="bookmarks-odbc"></a>書籤 (ODBC)
書籤是用來識別資料列的值。 書籤值的意義僅適用於驅動程式或資料來源。 例如，書籤可能跟資料列號碼一樣簡單，也可能跟磁碟位址一樣複雜。 ODBC 中的書籤會有點不同真實活頁簿中的書籤。 實際活頁簿，讀取器會將特定頁面放在書籤，然後尋找該書籤返回頁面。 在 ODBC 中，應用程式會要求特定資料列的書籤、將其儲存起來，然後將其傳回資料指標，即可傳回到資料列。 因此，在 ODBC 中的書籤是類似於讀取器記頁碼，記得，並再次尋找頁面。  
  
 若要判斷驅動程式支援的書籤，應用程式呼叫**SQLGetInfo** SQL_BOOKMARK_PERSISTENCE 選項。 此值的位元會說明什麼作業書籤存活下來，如書籤是否仍然有效之後會關閉資料指標。  
  
 此章節包含下列主題。  
  
-   [書籤的型別](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [擷取書籤](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [捲動書籤](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [更新、 刪除或讀取書籤](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [比較的書籤](../../../odbc/reference/develop-app/comparing-bookmarks.md)
