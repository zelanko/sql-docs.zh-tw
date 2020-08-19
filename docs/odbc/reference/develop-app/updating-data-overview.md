---
description: 更新資料概觀
title: 正在更新資料總覽 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b1755ea75426030a96ed7b349cc82f0fc7e282a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424420"
---
# <a name="updating-data-overview"></a>更新資料概觀
應用程式可以藉由執行 SQL 語句或呼叫 **SQLSetPos** 或 **SQLBulkOperations**來更新資料。 **UPDATE**、 **DELETE**和 **INSERT** 語句會直接在資料來源上運作，而且驅動程式通常會支援這些語句。 搜尋的 update 和 delete 語句包含要變更之資料列的規格。 定位的 update 和 delete 語句和 **SQLSetPos** 會透過資料指標在資料來源上執行動作，但較不廣泛支援。  
  
 資料指標是否可以使用本節所述的方法來偵測對結果集所做的變更，取決於資料指標的類型及其實作為方式。 順向資料指標不會重新流覽資料列，因此不會偵測到任何變更。 如需可滾動資料指標是否可以偵測變更的相關資訊，請參閱可滾動的資料 [指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 此章節包含下列主題。  
  
-   [UPDATE、DELETE 以及 INSERT 陳述式](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定點更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [模擬定點更新和刪除陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
