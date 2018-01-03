---
title: "可捲動資料指標類型 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 85de42e271f937c7a3de1aacba918bb43ea463d4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/21/2017
---
# <a name="scrollable-cursor-types"></a>可捲動資料指標類型
四種類型的可捲動資料指標是靜態、 動態、 索引鍵集驅動和混合。 靜態資料指標偵測少或沒有變更，但是會實作相對低廉。 動態資料指標偵測到的所有變更，但很難實作。 索引鍵集驅動和混合的資料指標居於兩者之間，可以偵測大部份的變更，但是在較少的費用比動態資料指標。  
  
 下列詞彙用來定義每種類型的可捲動資料指標的特性：  
  
-   **擁有更新、 刪除和插入。** 更新、 刪除及插入的資料指標，不論是透過呼叫進行**SQLBulkOperations**或**SQLSetPos**或定位更新或刪除陳述式。  
  
-   **其他更新、 刪除和插入。** 更新、 刪除和非由資料指標，包括其他作業相同交易中所做的插入、 透過其他的交易，以及與其他應用程式所建立。  
  
-   **成員資格。** 在結果集中的資料列集。  
  
-   **順序。** 資料指標所傳回資料列順序。  
  
-   **值。** 在結果集中的每個資料列中的值。  
  
 如需如何更新、 刪除和插入資料的資訊，請參閱[更新資料概觀](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 靜態資料指標](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動態資料指標](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [索引鍵集導向的資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合資料指標](../../../odbc/reference/develop-app/mixed-cursors.md)
