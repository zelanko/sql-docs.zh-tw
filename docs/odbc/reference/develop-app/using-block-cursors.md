---
description: 使用區塊資料指標
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
ms.openlocfilehash: 67cad7220641e9c3800e89675825cf2c0b1e334d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482861"
---
# <a name="using-block-cursors"></a>使用區塊資料指標
ODBC 3 內建區塊資料指標的支援。*x*。 **SQLFetch** 只能用於在 ODBC 3 中呼叫的多資料列提取。*x*;如果是 ODBC 2。*x* 應用程式呼叫 **SQLFetch**，它只會開啟單一資料列的順向資料指標。 當 ODBC 3。*x* 應用程式呼叫 ODBC 2 中的 **SQLFetch** 。*x* 驅動程式，除非驅動程式支援 **SQLExtendedFetch**，否則會傳回單一資料列。 如需詳細資訊，請參閱附錄 G：提供回溯相容性之驅動程式指導方針中的 [區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) 。  
  
 若要使用區塊資料指標，應用程式會設定資料列集大小、系結資料列集緩衝區 (如上一節所述) 、選擇性地設定 SQL_ATTR_ROWS_FETCHED_PTR 和 SQL_ATTR_ROW_STATUS_PTR 語句屬性，以及呼叫 **SQLFetch** 或 **SQLFetchScroll** 來提取資料列區塊。 應用程式可以藉由呼叫 **SQLBindCol** 來變更資料列集大小，並將新的資料列集緩衝區系結 (，或在提取資料列之後，) 指定系結位移。  
  
 此章節包含下列主題。  
  
-   [資料列集大小](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [擷取的資料列數目和狀態](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData 和區塊資料指標;封鎖 curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
