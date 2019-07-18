---
title: 捲動和提取資料列 (ODBC) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b326ed0c4e9a196904aa0f5c60b705243ef3bd97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061577"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>捲動與擷取資料列 (ODBC)
應用程式時使用可捲動資料指標，呼叫**SQLFetchScroll**來定位資料指標與提取資料列。 **SQLFetchScroll**支援相對捲動 (下一步，之前，而相對*n*資料列)，絕對的捲動 (first、 last、 和資料列*n*)，和依書籤的位置。 *Sqlfetchscroll*並*FetchOffset*中的引數**SQLFetchScroll**指定擷取，資料列集下, 圖所示。  
  
 ![接下來，擷取前，第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **接下來，擷取一個、 第一個和最後一個資料列集**  
  
 ![提取絕對、 相對和加上書籤的資料列集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **提取絕對、 相對和加上書籤的資料列集**  
  
 **SQLFetchScroll**放置游標以指定的資料列，並且在該資料列開始的資料列集傳回的資料列。 如果指定的資料列集重疊結果集的結尾，則會傳回部分的資料列集。 如果指定的資料列集重疊開始的結果集，在結果中的第一個資料列集通常會傳回集;完整的詳細資訊，請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函式描述。  
  
 在某些情況下，應用程式可能會想要將游標而不擷取任何資料。 比方說，它可能會想要測試是否在資料列存在，或只是資料列取得書籤，而不用在網路上的其他資料。 若要這樣做，它設定 SQL_RD_OFF SQL_ATTR_RETRIEVE_DATA 陳述式屬性。 變數繫結至書籤資料行 （如果有的話） 會一律更新，不論此陳述式屬性的設定。  
  
 在擷取資料列集之後，應用程式可以呼叫**SQLSetPos**放置在資料列集中的資料列集或重新整理資料列中的特定資料列。 如需有關使用**SQLSetPos**，請參閱[更新的資料，使用 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  支援 ODBC 2 中的捲動。*x*驅動程式，請**SQLExtendedFetch**。 如需詳細資訊，請參閱 <<c0> [ 區塊資料指標、 可捲動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)在 < 附錄 g:為了與舊版相容的驅動程式指導方針。
