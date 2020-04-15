---
title: 更新資料概述 |微軟文件
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
ms.openlocfilehash: 9972ab61f041385ae4ca616df093ae63ad7a47d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300384"
---
# <a name="updating-data-overview"></a>更新資料概觀
應用程式可以通過執行 SQL 語句或調用**SQLSetPos**或**SQLBulk 操作**來更新數據。 **更新**、**刪除**與**插入**敘述直接作用於資料來源,通常由驅動程式支援。 搜尋的更新和刪除語句包含要更改的行的規範。 定位的更新和刪除語句和**SQLSetPos**通過游標對數據源執行操作,並且不太廣泛支援。  
  
 游標能否使用本節中描述的方法檢測對結果集所做的更改取決於游標的類型及其實現方式。 僅轉發遊標不會重新訪問行,因此不會檢測到任何更改。 有關可捲軸是否可以偵測變更的資訊,請參閱[可捲動游標](../../../odbc/reference/develop-app/scrollable-cursors.md)。  
  
 此章節包含下列主題。  
  
-   [UPDATE、DELETE 以及 INSERT 陳述式](../../../odbc/reference/develop-app/update-delete-and-insert-statements.md)  
  
-   [定點更新和刪除陳述式](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)  
  
-   [模擬定點更新和刪除陳述式](../../../odbc/reference/develop-app/simulating-positioned-update-and-delete-statements.md)  
  
-   [判斷受影響的資料列數目](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)  
  
-   [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)  
  
-   [使用 SQLBulkOperations 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlbulkoperations.md)  
  
-   [長資料和 SQLSetPos 與 SQLBulkOperations](../../../odbc/reference/develop-app/long-data-and-sqlsetpos-and-sqlbulkoperations.md)
