---
description: 擷取結果 (進階)
title: " (Advanced) 取出結果 |Microsoft Docs"
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
ms.openlocfilehash: 12f5c2ddd1e04b1aef96b7ef1544db9b58a9a58e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461370"
---
# <a name="retrieving-results-advanced"></a>擷取結果 (進階)
應用程式可以指定在呼叫 **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或 **SQLSetPos** 時，將位移加入至系結的資料緩衝區位址，以及對應的長度/指標緩衝區位址。 這些新增的結果會決定這些作業中使用的位址。  
  
 系結位移可讓應用程式變更系結，而不需要針對先前系結的資料行呼叫 **SQLBindCol** 。 呼叫 **SQLBindCol** 來重新系結資料會變更緩衝區位址和長度/指標指標。 另一方面，使用位移進行重新系結，只會將位移加入至現有的系結資料緩衝區位址和長度/指標緩衝區位址。 使用位移時，系結是應用程式緩衝區配置方式的「範本」，而應用程式可以藉由變更位移來將此「範本」移至不同的記憶體區域。 您可以隨時指定新的位移，且一律會新增至原始系結的值。  
  
 為了指定系結位移，此應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性設定為 SQLINTEGER 緩衝區的位址。 在應用程式呼叫使用系結的函式（例如 **SQLBulkOperations**、 **SQLFetch**、 **SQLFetchScroll**或 **SQLSetPos**）之前，它會在此緩衝區中以位元組為單位來放置位移，只要資料緩衝區位址或長度/指標緩衝區位址都不是0，而且只要系結資料行位於結果集中。 位址和位移的總和必須是有效的位址。  (這表示，如果位移和位移加入的位址都是有效的位址，就會是不正確。 ) SQL_ATTR_ROW_BIND_OFFSET_PTR 語句屬性是一個指標，以便將 offset 值套用至一組以上的系結資料，只要變更一個 offset 值即可變更全部。 應用程式必須確保指標維持有效，直到游標關閉為止。  
  
> [!NOTE]  
>  ODBC 2 不支援系結位移。*x* 驅動程式。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可滾動的資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 資料指標程式庫](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多個結果](../../../odbc/reference/develop-app/multiple-results.md)
