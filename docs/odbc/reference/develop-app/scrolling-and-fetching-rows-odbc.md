---
description: 捲動與擷取資料列 (ODBC)
title: " (ODBC) 的滾動和提取資料列 |Microsoft Docs"
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6fcdd2cd635a7da66a5d81c4beb24088f96382b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476490"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>捲動與擷取資料列 (ODBC)
使用可滾動的資料指標時，應用程式會呼叫 **SQLFetchScroll** ，以定位資料指標和提取資料列。 **SQLFetchScroll**支援) 、絕對滾動 (first、last 和 row *n*) 以及依書簽定位 (下一步、先前和相對的*n*個數據列。 **SQLFetchScroll**中的*FetchOrientation*和*FetchOffset*引數會指定要提取的資料列集，如下列圖表所示。  
  
 ![提取下一個、上一個、第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **提取下一個、上一個、第一個和最後一個資料列集**  
  
 ![提取絕對、相對和加上書籤的資料列集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **提取絕對、相對且加上書簽的資料列集**  
  
 **SQLFetchScroll** 會將資料指標放在指定的資料列，並從該資料列開始傳回資料列集中的資料列。 如果指定的資料列集與結果集的結尾重迭，則會傳回部分資料列集。 如果指定的資料列集與結果集的開頭重迭，則通常會傳回結果集中的第一個資料列集;如需完整的詳細資訊，請參閱 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 函數描述。  
  
 在某些情況下，應用程式可能會想要在不需要取出任何資料的情況下放置資料指標。 例如，它可能會想要測試資料列是否存在，或只是取得資料列的書簽，而不會在網路上建立其他資料。 若要這樣做，它會將 SQL_ATTR_RETRIEVE_DATA 語句屬性設定為 SQL_RD_OFF。 系結至書簽資料行的變數 (是否永遠更新任何) ，不論這個語句屬性的設定為何。  
  
 在抓取資料列集之後，應用程式可以呼叫 **SQLSetPos** ，以定位至資料列集內的特定資料列，或重新整理資料列集中的資料列。 如需有關使用 **SQLSetPos**的詳細資訊，請參閱 [使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  ODBC 2 中支援滾動。*x* 驅動程式（依 **SQLExtendedFetch**）。 如需詳細資訊，請參閱附錄 G：提供回溯相容性之驅動程式指導方針中的 [區塊資料指標、可滾動的資料指標和回溯相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。
