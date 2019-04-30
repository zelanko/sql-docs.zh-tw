---
title: 捲動和提取資料列 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0c0f7f2cad7eaecc212e2283fab7fc7d69f2ee7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63207122"
---
# <a name="scrolling-and-fetching-rows"></a>捲動與提取資料列
  若要使用可捲動的資料指標，ODBC 應用程式必須：  
  
-   設定使用的資料指標功能[SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md)。  
  
-   開啟資料指標使用**SQLExecute**或是**SQLExecDirect**。  
  
-   捲動與提取資料列，使用**SQLFetch**或是[SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md)。  
  
 兩者**SQLFetch**並**SQLFetchSroll**可以一次提取資料列的區塊。 指定使用時，傳回資料列數**SQLSetStmtAttr**設定 SQL_ATTR_ROW_ARRAY_SIZE 參數。  
  
 ODBC 應用程式可以使用**SQLFetch**擷取順向資料指標。  
  
 **SQLFetchScroll**可用來在資料指標周圍捲動。 **SQLFetchScroll**支援提取下一個、 第一個和最後一個資料列集除了相對提取 (提取資料列集*n*從目前的資料列集開始的資料列) 和絕對提取 （提取資料列集從資料列開始*n*)。 如果*n*是負的絕對提取中，會計算資料列從結果集的結尾。 資料列的絕對提取 -1 表示提取從結果集的最後一個資料列開始的資料列集。  
  
 使用應用程式**SQLFetchScroll**僅針對其區塊資料指標的功能，例如報表可能會通過結果集一次，僅使用選項來擷取下一個資料列集。 以螢幕為基礎的應用程式，相反地，可以利用所有的功能**SQLFetchScroll**。 如果應用程式設定的資料列集大小的螢幕上顯示的資料列數目，並將螢幕緩衝區繫結至結果集，它可以將轉譯直接到呼叫的捲軸作業**SQLFetchScroll**。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|包含等於-1 的 FetchOffset 的 sql_fetch_relative|  
|向下捲動一行|包含 FetchOffset 的 SQL_FETCH_RELATIVE 等於 1|  
|捲動方塊到頂端|SQL_FETCH_FIRST|  
|捲動方塊到底部|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>本節內容  
  
-   [在 ODBC 中為資料列上加上書籤](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標&#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
