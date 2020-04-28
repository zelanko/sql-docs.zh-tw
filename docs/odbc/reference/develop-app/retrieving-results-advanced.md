---
title: 正在抓取結果（Advanced） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294638"
---
# <a name="retrieving-results-advanced"></a>擷取結果 (進階)
應用程式可以指定在呼叫**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**時，將位移新增至系結的資料緩衝區位址，以及對應的長度/指標緩衝區位址。 這些新增專案的結果會決定這些作業中使用的位址。  
  
 系結位移可讓應用程式變更系結，而不需要針對先前系結的資料行呼叫**SQLBindCol** 。 呼叫**SQLBindCol**以重新系結資料會變更緩衝區位址和長度/指示器指標。 另一方面，以位移重新系結，就只會將位移新增至現有的系結資料緩衝區位址和長度/指標緩衝區位址。 使用位移時，系結會是應用程式緩衝區配置方式的「範本」，而應用程式可以藉由變更位移，將此「範本」移至不同的記憶體區域。 可以隨時指定新的位移，而且一律會加入至原始系結的值。  
  
 若要指定系結位移，應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用系結的函式（例如**SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或**SQLSetPos**）之前，只要資料緩衝區位址或長度/指標緩衝區位址都不是0，而且只要系結的資料行位於結果集中，它就會將位移以位元組為單位放置在這個緩衝區中。 位址和位移的總和必須是有效的位址。 （這表示只要或兩者的總和是有效的位址，就會將位移和加入位移的位址設為無效。）SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性是一個指標，因此，位移值可以套用至一組以上的系結資料，而這些都可以藉由變更一個位移值來變更。 應用程式必須確定指標保持有效，直到游標關閉為止。  
  
> [!NOTE]  
>  ODBC 2 不支援系結位移。*x*驅動程式。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可滾動的資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 資料指標程式庫](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多個結果](../../../odbc/reference/develop-app/multiple-results.md)
