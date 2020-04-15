---
title: 使用區塊游標 :微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306789"
---
# <a name="using-block-cursors"></a>使用區塊資料指標
對區塊游標的支援內置於 ODBC 3 中。*x*. . **SQLFetch**只能在 ODBC 3 中呼叫時用於多行提取。*x;* 如果 ODBC 2.*x*應用程式呼叫**SQLFetch,** 它將只打開一個單行、僅轉發的游標。 當一個ODBC 3。*x*應用程式在 ODBC 2 中呼叫**SQLFetch。***x*驅動程式,它傳回一行,除非驅動程式支援**SQLExtendedFetch**。 有關詳細資訊,請參閱附錄 G 中的[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):向後相容性的驅動程式指南。  
  
 要使用塊游標,應用程式設置行集大小,綁定行集緩衝區(如上一節所述),可以選擇設置SQL_ATTR_ROWS_FETCHED_PTR和SQL_ATTR_ROW_STATUS_PTR語句屬性,並調用**SQLFetch**或**SQLFetchScroll**來獲取行塊。 應用程式可以更改列集大小並綁定新的行集緩衝區(通過調用**SQLBindCol**或指定綁定偏移),即使在獲取行之後也是如此。  
  
 此章節包含下列主題。  
  
-   [資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [擷取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGet數據和塊游標;塊庫爾索](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
