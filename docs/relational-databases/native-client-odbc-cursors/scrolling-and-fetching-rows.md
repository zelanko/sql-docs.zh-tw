---
title: "捲動和提取資料列 |Microsoft 文件"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "34"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f84d14d3ab2eb2bd3be56e61d34741916446aa48
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2018
---
# <a name="scrolling-and-fetching-rows"></a>捲動與提取資料列
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  若要使用可捲動的資料指標，ODBC 應用程式必須：  
  
-   設定使用的資料指標功能[SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md)。  
  
-   開啟資料指標使用**SQLExecute**或**SQLExecDirect**。  
  
-   捲動與提取資料列使用**SQLFetch**或[SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md)。  
  
 同時**SQLFetch**和**SQLFetchSroll**可以一次提取資料列的區塊。 會透過指定傳回的資料列數目**SQLSetStmtAttr**設定 SQL_ATTR_ROW_ARRAY_SIZE 參數。  
  
 ODBC 應用程式可以使用**SQLFetch**擷取順向資料指標。  
  
 **SQLFetchScroll**可用來在資料指標周圍捲動。 **SQLFetchScroll**支援提取下一個、 第一個和最後一個資料列集除了相對提取 (提取資料列集 *n* 從目前的資料列集的開頭的資料列) 和絕對提取 （提取資料列集資料列開始 *n* )。 如果 *n* 是負數的絕對提取中，會計算資料列從結果集的結尾。 資料列的絕對提取 -1 表示提取從結果集的最後一個資料列開始的資料列集。  
  
 使用應用程式**SQLFetchScroll**僅針對其區塊資料指標的功能，例如報表，可能會通過結果集一次，僅使用選項來提取下一個資料列集。 螢幕型應用程式，相反地，可以利用的所有功能**SQLFetchScroll**。 如果應用程式設定的螢幕上顯示的資料列數目的資料列集大小，並將螢幕緩衝區繫結至結果集，它可以轉譯捲軸作業，直接到呼叫**SQLFetchScroll**。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|包含等於-1 FetchOffset 的 sql_fetch_relative|  
|向下捲動一行|包含 FetchOffset 的 SQL_FETCH_RELATIVE 等於 1|  
|捲動方塊到頂端|SQL_FETCH_FIRST|  
|捲動方塊到底部|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>本節內容  
  
-   [建立 ODBC 中的資料列的書籤](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>另請參閱  
 [使用資料指標 &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
