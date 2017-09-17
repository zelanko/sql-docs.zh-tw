---
title: "捲動和提取資料列 (ODBC) |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5b5a9aefccf51cc4b3aac1aeba02c7878c6dceed
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="scrolling-and-fetching-rows-odbc"></a>捲動和提取資料列 (ODBC)
當使用可捲動資料指標時，應用程式呼叫**SQLFetchScroll**來定位資料指標與提取資料列。 **SQLFetchScroll**支援相對捲動 (下一步、 前，而相對* n *資料列)，絕對捲動 (first、 last、 與資料列* n *)，以及定位的書籤。 *Sqlfetchscroll*和*FetchOffset*中的引數**SQLFetchScroll**指定哪些資料列集來擷取下, 圖所示。  
  
 ![接下來，擷取前，第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **接下來，提取一個、 第一個和最後一個資料列集**  
  
 ![提取絕對、 相對和加上書籤的資料列集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **提取絕對、 相對和加上書籤的資料列集**  
  
 **SQLFetchScroll**放置到指定的資料列資料指標，並且傳回該資料列開始的資料列集的資料列。 如果指定的資料列集重疊結果集的結尾，則會傳回部分資料列集。 如果指定的資料列集重疊開始的結果集，在結果中的第一個資料列集通常會傳回集;完整的詳細資訊，請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函式描述。  
  
 在某些情況下，應用程式可能會想要將游標的位置而不擷取任何資料。 例如，它可能會想要測試是否在資料列存在，或只出現書籤的資料列不會顯示在網路上的其他資料。 若要這樣做，它將 SQL_ATTR_RETRIEVE_DATA 陳述式屬性設定 SQL_RD_OFF。 變數繫結至書籤資料行 （如果有的話） 會自動更新，不論此陳述式屬性的設定。  
  
 在擷取資料列集之後，應用程式可以呼叫**SQLSetPos**來定位到資料列集中的資料列集或重新整理資料列中的特定資料列。 如需有關使用**SQLSetPos**，請參閱[更新的資料與 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  ODBC 2 支援捲動。*x*驅動程式**SQLExtendedFetch**。 如需詳細資訊，請參閱[區塊資料指標，可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附錄 g： 驅動程式的指導方針回溯相容性。
