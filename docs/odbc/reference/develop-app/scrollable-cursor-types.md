---
title: 可捲軸型態 :微軟文件
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f29269ea209875a2e775cf8d523302fcb9a976
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304229"
---
# <a name="scrollable-cursor-types"></a>可捲動的資料指標類型
四種類型的可滾動游標是靜態的、動態的、按鍵集驅動的和混合的。 靜態游標檢測到很少或沒有更改,但實現成本相對較低。 動態游標可檢測所有更改,但實現成本高昂。 鍵集驅動和混合游標位於兩者之間,檢測大多數更改,但費用低於動態游標。  
  
 以下字語用於定義每種類型的可捲軸游標的特徵:  
  
-   **擁有更新、刪除和插入。** 通過游標進行更新、刪除和插入,無論是調用**SQLBulk 操作還是** **SQLSetPos,** 要麼使用定位的更新或刪除語句。  
  
-   **其他更新、刪除和插入。** 更新、刪除和插入游標未進行的更新、刪除和插入,包括同一事務中其他操作所做的更新、刪除和插入、通過其他事務進行的操作以及其他應用程式所做的操作。  
  
-   **會員。** 結果集中的行集。  
  
-   **以。** 游標返回行的順序。  
  
-   **值。** 結果集中的每行中的值。  
  
 有關如何更新、刪除和插入資料的資訊,請參閱[更新資料概述](../../../odbc/reference/develop-app/updating-data-overview.md)。  
  
 此章節包含下列主題。  
  
-   [ODBC 靜態資料指標](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 動態資料指標](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [索引鍵集導向的資料指標](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [混合資料指標](../../../odbc/reference/develop-app/mixed-cursors.md)
