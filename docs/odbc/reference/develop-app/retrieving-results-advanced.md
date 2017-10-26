---
title: "擷取結果 （進階） |Microsoft 文件"
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
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85ee85c9bb44f32d33cee622c60c677f22b0ba7c
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="retrieving-results-advanced"></a>擷取結果 （進階）
應用程式可以指定位移，加入繫結的資料緩衝區的位址和對應的長度/指標緩衝區位址時**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**呼叫。 這些加入作業的結果判斷這些作業中使用的位址。  
  
 繫結位移允許應用程式變更繫結，而不需呼叫**SQLBindCol**先前繫結資料行。 呼叫**SQLBindCol**重新繫結的資料變更的緩衝區位址和長度/指標的指標。 重新繫結的位移，相反地，只要將位移新增至現有的繫結的資料緩衝區位址和長度/指標緩衝區位址。 當使用位移時，繫結就是 「 範本 」 的應用程式緩衝區的配置方式，應用程式可以藉由變更位移到不同的記憶體區域中移這個 「 範本 」。 隨時都可以指定新的位移，並永遠會加入到原始繫結的值。  
  
 若要指定繫結位移，應用程式會將 SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性設定 SQLINTEGER 緩衝區的位址。 應用程式呼叫的函式會使用繫結，例如之前**SQLBulkOperations**， **SQLFetch**， **SQLFetchScroll**，或**SQLSetPos**，就會將位移 （位元組），這個緩衝區中，只要資料緩衝區位址和長度/指標緩衝區位址都不是 0，而且只要繫結的資料行在結果集中。 位址和位移的總和必須是有效的位址。 （這表示，或兩個位移與位移加入的位址可以是無效的只要其總和會是有效的位址）。SQL_ATTR_ROW_BIND_OFFSET_PTR 陳述式屬性是指標，因此位移的值可以套用至一組以上的資料，全部都是藉由變更一個位移的值可以變更繫結。 應用程式必須確定指標都有效，直到關閉資料指標。  
  
> [!NOTE]  
>  ODBC 2 不支援繫結的位移。*x*驅動程式。  
  
 此章節包含下列主題。  
  
-   [區塊資料指標](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 資料指標程式庫](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [多個結果](../../../odbc/reference/develop-app/multiple-results.md)

