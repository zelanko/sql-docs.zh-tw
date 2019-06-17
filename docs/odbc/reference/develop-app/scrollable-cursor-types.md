---
title: 可捲動資料指標類型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6290d18ec26fcfa6e2960c3a2c1c408938d9e0e4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468575"
---
# <a name="scrollable-cursor-types"></a>可捲動的資料指標類型
四種類型的可捲動資料指標是靜態、 動態、 索引鍵集驅動和混合。 靜態資料指標偵測到幾乎不需要變更，但會相對較低廉，實作。 動態資料指標偵測到的所有變更，但很難實作。 索引鍵集驅動和混合的資料指標居於兩者之間，可以偵測大部份的變更，但較少的費用比動態資料指標。  
  
 下列詞彙用來定義每一種可捲動資料指標的特性：  
  
-   **自己的更新、 刪除和插入。** 更新、 刪除和插入資料指標，不論是透過呼叫來進行**SQLBulkOperations**或是**SQLSetPos**或定位更新或刪除陳述式。  
  
-   **其他更新、 刪除和插入。** 更新、 刪除和不資料指標，包括所進行的其他作業相同交易中所進行的 insert、 透過其他的交易，以及所做的其他應用程式。  
  
-   **成員資格。** 在結果集中的資料列集。  
  
-   **順序。** 資料指標所傳回資料列順序。  
  
-   **值。** 在結果集中的每個資料列中的值。  
  
 如需有關如何更新、 刪除和插入資料的資訊，請參閱[更新資料概觀](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 靜態資料指標](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動態資料指標](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [索引鍵集導向的資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合資料指標](../../../odbc/reference/develop-app/mixed-cursors.md)
