---
title: 書籤 (ODBC) |微軟文件
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
ms.openlocfilehash: e8273c82b918024417e613ea44a2d26bafaf7d76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306319"
---
# <a name="bookmarks-odbc"></a>書籤 (ODBC)
書籤是用來識別資料列的值。 書籤值的意義僅適用於驅動程式或資料來源。 例如，書籤可能跟資料列號碼一樣簡單，也可能跟磁碟位址一樣複雜。 ODBC 中的書籤與真實書籍中的書籤略有不同。 在真實書籍中,讀者將書籤放在特定頁面,然後查找該書籤以返回到該頁。 在 ODBC 中，應用程式會要求特定資料列的書籤、將其儲存起來，然後將其傳回資料指標，即可傳回到資料列。 因此,ODBC 中的書籤類似於讀者寫下頁碼、記住它,然後再次查找頁面。  
  
 要確定驅動程式對書籤的支援,應用程式使用SQL_BOOKMARK_PERSISTENCE選項調用**SQLGetInfo。** 此值中的位描述書籤存活的操作,例如書籤在關閉游標后是否仍然有效。  
  
 此章節包含下列主題。  
  
-   [書籤類型](../../../odbc/reference/develop-app/bookmark-types.md)  
  
-   [擷取書籤](../../../odbc/reference/develop-app/retrieving-bookmarks.md)  
  
-   [依書籤捲動](../../../odbc/reference/develop-app/scrolling-by-bookmark.md)  
  
-   [依書籤更新、刪除或擷取](../../../odbc/reference/develop-app/updating-deleting-or-fetching-by-bookmark.md)  
  
-   [比較書籤](../../../odbc/reference/develop-app/comparing-bookmarks.md)
