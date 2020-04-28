---
title: 使用區塊資料指標 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f5c487bd8b60a83c709399cb9673dc0b015bd79d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306789"
---
# <a name="using-block-cursors"></a>使用區塊資料指標
區塊資料指標的支援內建在 ODBC 3 中。*x*。 在 ODBC 3 中呼叫**SQLFetch**時，只能用於多資料列提取。*x*;如果是 ODBC 2。*x*應用程式會呼叫**SQLFetch**，它只會開啟單一資料列的順向資料指標。 當 ODBC 3 時。*x*應用程式會呼叫 ODBC 2 中的**SQLFetch** 。*x*驅動程式，它會傳回單一資料列，除非驅動程式支援**SQLExtendedFetch**。 如需詳細資訊，請參閱附錄 G：驅動程式方針中的[區塊資料指標、可滾動游標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。  
  
 若要使用區塊資料指標，應用程式會設定資料列集大小、系結資料列集緩衝區（如上一節所述），選擇性地設定 SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_ROW_STATUS_PTR 語句屬性，並呼叫**SQLFetch**或**SQLFetchScroll**來提取資料列區塊。 即使在提取資料列之後，應用程式也可以變更資料列集大小，並系結新的資料列集緩衝區（藉由呼叫**SQLBindCol**或指定系結位移）。  
  
 此章節包含下列主題。  
  
-   [資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [擷取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和區塊資料指標;封鎖 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
