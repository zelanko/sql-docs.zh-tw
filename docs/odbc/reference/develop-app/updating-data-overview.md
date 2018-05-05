---
title: 更新資料概觀 |Microsoft 文件
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
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 64f61563836b7deddc65b2dc61307ed686f030ef
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-overview"></a>更新資料概觀
執行 SQL 陳述式，或呼叫應用程式可以更新資料**SQLSetPos**或**SQLBulkOperations**。 **更新**，**刪除**，和**插入**陳述式會直接處理資料來源和驅動程式通常都支援。 搜尋 update 和 delete 陳述式包含要變更的資料列的規格。 定位 update 和 delete 陳述式和**SQLSetPos**透過資料指標的資料來源並較廣受支援。  
  
 資料指標是否可以偵測到結果集的這一節所述的方法所做的變更取決於資料指標和它的實作方式的類型。 順向資料指標不重新瀏覽資料列，並因此不會偵測到的任何變更。 可捲動資料指標可以偵測到變更的相關資訊，請參閱[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 此章節包含下列主題。  
  
-   [UPDATE、DELETE 以及 INSERT 陳述式](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定位的 Update 和 Delete 陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [定位的 Update 和 Delete 陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
