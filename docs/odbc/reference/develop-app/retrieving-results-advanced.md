---
title: 正在擷取結果 （進階） |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a88a96b856ba0976dcb8600d26f78b772654bd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020500"
---
# <a name="retrieving-results-advanced"></a>擷取結果 (進階)
應用程式可以指定的位移會新增至繫結資料的緩衝區位址和對應的長度/指標緩衝區位址何時**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**呼叫。 這些新增內容的結果判斷這些作業中使用的位址。  
  
 繫結位移允許應用程式變更繫結，而不會呼叫**SQLBindCol**之前繫結的資料行。 呼叫**SQLBindCol**重新繫結的資料變更的緩衝區位址，而且長度/指標的指標。 重新繫結利用位移，相反地，只要將位移加入現有的繫結的資料緩衝區位址和長度/指標緩衝區位址。 當使用位移時，繫結都是 「 範本 」 的應用程式緩衝區的配置方式和應用程式可以藉由變更位移到不同區域的記憶體中移動這個 「 範本 」。 新的位移可以指定在任何時間，而且永遠會加入到原始的繫結的值。  
  
 若要指定繫結位移，應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性設定為 SQLINTEGER 緩衝區的位址。 應用程式呼叫的函式會使用繫結，例如之前**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**，就會將位移 （位元組），在此緩衝區中，只要資料緩衝區位址和長度/指標緩衝區位址都不是 0，，而且只要繫結的資料行結果集中。 位址和位移的總和必須是有效的位址。 （這表示，或兩個位移和加入位移的位址可以是無效，只要其總和會是有效的位址）。SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性是指標，因此位移的值可以套用至多個一組繫結的資料，當然也可以藉由變更一個位移的值已變更。 應用程式必須確定，指標都有效，直到關閉資料指標。  
  
> [!NOTE]  
>  ODBC 2 不支援繫結位移。*x*驅動程式。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可捲動的資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 資料指標程式庫](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多個結果](../../../odbc/reference/develop-app/multiple-results.md)
