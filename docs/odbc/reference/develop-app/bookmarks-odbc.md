---
description: 書籤 (ODBC)
title: " (ODBC) 的書簽 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: 1d7cccc5-f847-4321-b240-28570854ee5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f162fc317f2651549a1a2e80af03c9942dc64bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461610"
---
# <a name="bookmarks-odbc"></a>書籤 (ODBC)
書籤是用來識別資料列的值。 書籤值的意義僅適用於驅動程式或資料來源。 例如，書籤可能跟資料列號碼一樣簡單，也可能跟磁碟位址一樣複雜。 ODBC 中的書簽與實際書籍中的書簽有點不同。 在實際的書籍中，讀取器會在特定頁面上放置書簽，然後尋找該書簽以返回頁面。 在 ODBC 中，應用程式會要求特定資料列的書籤、將其儲存起來，然後將其傳回資料指標，即可傳回到資料列。 因此，ODBC 中的書簽類似于寫下頁面號碼、記住該頁碼，然後再次查閱頁面的讀者。  
  
 為了判斷驅動程式對書簽的支援，應用程式會使用 SQL_BOOKMARK_PERSISTENCE 選項來呼叫 **SQLGetInfo** 。 此值中的位描述書簽存留的作業，例如，在關閉資料指標之後，書簽是否仍然有效。  
  
 此章節包含下列主題。  
  
-   [書籤類型](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [擷取書籤](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [依書籤捲動](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [依書籤更新、刪除或擷取](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [比較書籤](../../../odbc/reference/develop-app/comparing-bookmarks.md)
