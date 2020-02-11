---
title: 可滾動的資料指標類型 |Microsoft Docs
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
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061630"
---
# <a name="scrollable-cursor-types"></a>可捲動的資料指標類型
這四種類型的可滾動資料指標為靜態、動態、索引鍵集驅動和混合。 靜態資料指標會偵測到幾個或沒有變更，但執行的成本相對較低。 動態資料指標會偵測所有變更，但執行成本高昂。 索引鍵集驅動和混合資料指標之間的差異在於偵測大部分的變更，但代價比動態資料指標少。  
  
 下列詞彙可用來定義每個可滾動資料指標類型的特性：  
  
-   **自己的更新、刪除和插入。** 藉由呼叫**SQLBulkOperations**或**SQLSetPos** ，或使用定位 update 或 delete 語句，來更新、刪除和插入資料指標。  
  
-   **其他更新、刪除和插入。** 不是由資料指標所進行的更新、刪除和插入，包括在相同交易中由其他作業所建立的資料、透過其他交易所建立的資料，以及其他應用程式所建立的資料。  
  
-   **所屬.** 結果集中的資料列集合。  
  
-   **即可.** 資料指標傳回資料列的順序。  
  
-   **閾值.** 結果集中每個資料列的值。  
  
 如需有關如何更新、刪除和插入資料的詳細資訊，請參閱[更新資料總覽](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 靜態資料指標](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動態資料指標](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [索引鍵集導向的資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合資料指標](../../../odbc/reference/develop-app/mixed-cursors.md)
