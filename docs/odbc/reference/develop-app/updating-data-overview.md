---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0701218b5ef489d1f8962ffadc9409986a0c36c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942819"
---
# <a name="updating-data-overview"></a>更新資料概觀
應用程式可以藉由執行 SQL 語句或藉由呼叫**SQLSetPos**或**SQLBulkOperations**來更新資料。 **UPDATE**、 **DELETE**和**INSERT**語句直接在資料來源上執行，而且通常會受到驅動程式的支援。 搜尋的 update 和 delete 語句包含要變更之資料列的規格。 定位的 update 和 delete 語句和**SQLSetPos**會透過資料指標來處理資料來源，但較不普遍受到支援。  
  
 資料指標是否可以使用本節所述的方法來偵測對結果集所做的變更，取決於資料指標的類型及其實作為方式。 順向資料指標不會重新流覽資料列，因此不會偵測到任何變更。 如需可滾動資料指標是否能偵測變更的相關資訊，請參閱可滾動的資料[指標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 此章節包含下列主題。  
  
-   [UPDATE、DELETE 以及 INSERT 陳述式](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定點更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [模擬定點更新和刪除陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
