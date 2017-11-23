---
title: "相對與絕對捲動 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32782c2fe59aaf36fa8741870a798163d923a3a1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="relative-and-absolute-scrolling"></a>相對與絕對捲動
大部分的捲動選項**SQLFetchScroll**放置游標的目前位置的相對或絕對位置。 **SQLFetchScroll**支援提取下一個、 第一個和最後一個資料列集，做為也為相對提取 (提取資料列集 *n* 從目前的資料列集的開頭的資料列) 和絕對提取 (提取資料列集資料列開始 *n* )。 如果 *n* 是負數的絕對提取中，會計算資料列從結果集的結尾。 因此，絕對提取資料列 – 1 表示提取從結果集中的最後一個資料列開始的資料列集。  
  
 動態資料指標偵測資料列插入和刪除結果集中，所以沒有簡單的方式來擷取結果集，可能會變慢的開始處讀取以外的特定數字的資料列的動態資料指標。 此外，絕對提取不是很有用的動態資料指標因為資料列數字變更為資料列插入和刪除;因此，連續擷取相同的資料列數目可能會產生不同的資料列。  
  
 使用應用程式**SQLFetchScroll**僅針對其區塊資料指標的功能，例如報表，可能會通過結果集一次，僅使用選項來提取下一個資料列集。 螢幕型應用程式，相反地，可以利用的所有功能**SQLFetchScroll**。 如果應用程式設定的螢幕上顯示的資料列數目的資料列集大小，並將螢幕緩衝區繫結至結果集，它可以轉譯捲軸作業，直接到呼叫**SQLFetchScroll**。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|與 sql_fetch_relative 但*FetchOffset*等於-1|  
|向下捲動一行|與 sql_fetch_relative 但*FetchOffset*等於 1|  
|在最上方的捲動方塊|SQL_FETCH_FIRST|  
|在下方的捲動方塊|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
 這類應用程式也需要捲動的作業，需要目前的資料列數目和資料列數目之後定位捲動方塊。 目前的資料列數目，應用程式可以是追蹤的目前資料列數目或呼叫**SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 屬性來擷取它。  
  
 資料指標，也就是結果的大小中的資料列數目設定，可做為診斷的標頭的 SQL_DIAG_CURSOR_ROW_COUNT 欄位。 在此欄位中的值之後才定義**SQLExecute**， **SQLExecDirect**，或**SQLMoreResult**已呼叫。 這個計數可以是近似的計數或確切的數目，視驅動程式的功能而定。 您可以藉由呼叫判斷驅動程式支援**SQLGetInfo**與資料指標屬性的資訊類型，並檢查是否 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 元傳回類型的資料指標。  
  
 動態資料指標並不支援的實際資料列計數。 對於其他類型的資料指標中，驅動程式可以支援精確或大約的資料列計數，但非兩者。 如果此驅動程式支援的精確或大約都不特定的資料指標類型的資料列計數，SQL_DIAG_CURSOR_ROW_COUNT 欄位包含目前為止已擷取的資料列數目。 不論驅動程式支援， **SQLFetchScroll**與*作業*的 SQL_FETCH_LAST 將會導致 SQL_DIAG_CURSOR_ROW_COUNT 欄位包含正確的資料列計數。
