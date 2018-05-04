---
title: 使用區塊資料指標 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b58815042b77ed72698cf6a1de8b3eb12a76f83e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="using-block-cursors"></a>使用區塊資料指標
ODBC 3 是內建支援區塊資料指標。*x*。 **SQLFetch**僅用於多資料列擷取 ODBC 3 中呼叫時。*x*; 如果 ODBC 2。*x*應用程式會呼叫**SQLFetch**，它會開啟僅有單一資料列、 順向資料指標。 當 ODBC 3。*x*應用程式會呼叫**SQLFetch** ODBC 2。*x*驅動程式，它會傳回單一資料列的驅動程式支援除非**SQLExtendedFetch**。 如需詳細資訊，請參閱[區塊資料指標，可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附錄 g： 驅動程式的指導方針回溯相容性。  
  
 若要使用區塊資料指標，應用程式設定的資料列集大小，將繫結的資料列集的緩衝區 （如前一節中所述），選擇性地集 SQL_ATTR_ROWS_FETCHED_PTR 屬性和 SQL_ATTR_ROW_STATUS_PTR 陳述式屬性和呼叫**SQLFetch**或**SQLFetchScroll**來提取資料列的區塊。 應用程式可以變更資料列集大小，並將新的資料列集緩衝區繫結 (藉由呼叫**SQLBindCol**或指定的繫結位移) 即使已經提取資料列之後。  
  
 此章節包含下列主題。  
  
-   [資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [擷取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和區塊資料指標。區塊 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
