---
title: 更新資料概觀 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- data updates [ODBC]
- updating data [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 062036a4-cda6-4aaa-9765-f1ec3e0b31b1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3edbd41bc5361d864abcc7d631a90521af98ef01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62632663"
---
# <a name="updating-data-overview"></a>更新資料概觀
應用程式可以更新資料，執行 SQL 陳述式，或呼叫**SQLSetPos**或是**SQLBulkOperations**。 **更新**，**刪除**，以及**插入**陳述式直接處理資料來源及驅動程式通常會支援。 搜尋 update 和 delete 陳述式包含要變更的資料列的規格。 定位 update 和 delete 陳述式及**SQLSetPos**處理的資料來源，透過資料指標和較廣受支援。  
  
 資料指標是否可以偵測到結果集與這一節所述的方法所做的變更取決於資料指標和它的實作方式的型別。 順向資料指標不重新瀏覽資料列，並因此不會偵測到的任何變更。 是否可捲動資料指標可以偵測到變更的相關資訊，請參閱[可捲動資料指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 此章節包含下列主題。  
  
-   [UPDATE、DELETE 以及 INSERT 陳述式](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定位的 Update 和 Delete 陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [定位的 Update 和 Delete 陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
