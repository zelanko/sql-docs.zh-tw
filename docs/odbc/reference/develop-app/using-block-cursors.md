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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 388995cd5cb8a711d72533685c14088a7e908475
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313510"
---
# <a name="using-block-cursors"></a>使用區塊資料指標
內建的區塊資料指標支援 ODBC 3。*x*。 **SQLFetch**所以只可用於與多資料列提取呼叫在 ODBC 3 時。*x*; 如果 ODBC 2。*x*應用程式會呼叫**SQLFetch**，它會開啟僅有單一資料列、 順向資料指標。 當 ODBC 3。*x*應用程式會呼叫**SQLFetch** ODBC 2。*x*驅動程式，它會傳回單一資料列的驅動程式支援，除非**SQLExtendedFetch**。 如需詳細資訊，請參閱 <<c0> [ 區塊資料指標、 可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。  
  
 若要使用區塊資料指標，應用程式設定的資料列集大小、 繫結資料列集的緩衝區 （如前一節所述），選擇性地設定 SQL_ATTR_ROWS_FETCHED_PTR 和 sql_attr_row_status_ptr 設定陳述式屬性，並呼叫**SQLFetch**或是**SQLFetchScroll**來提取資料列的區塊。 應用程式可以變更資料列集大小，並將新的資料列集緩衝區繫結 (藉由呼叫**SQLBindCol**或指定的繫結位移) 甚至已經提取資料列之後。  
  
 此章節包含下列主題。  
  
-   [資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [擷取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和區塊資料指標;封鎖 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
