---
description: 相對與絕對的捲動
title: 相對和絕對滾動 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- absolute scrolling [ODBC]
- relative scrolling [ODBC]
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 3d0ff48d-fef5-4c01-bb1d-a583e6269b66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c7471e7ee245d9cf70adc8c3453705453bc1aac
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482940"
---
# <a name="relative-and-absolute-scrolling"></a>相對與絕對的捲動
**SQLFetchScroll**中的大部分滾動選項會將游標相對於目前位置或絕對位置。 **SQLFetchScroll** 支援提取下一個、上一個、第一個和最後一個資料列集，以及相對提取 (從目前資料列集的開頭提取資料列集 *n* 個數據列) 和絕對提取 (從資料列 *n*) 開始提取資料列集。 如果絕對提取中的 *n* 是負數，則會從結果集的結尾算出資料列。 因此，資料列1的絕對提取表示從結果集中的最後一個資料列開始提取資料列集。  
  
 動態資料指標會偵測從結果集插入和刪除的資料列，因此，動態資料指標在從結果集開頭讀取的資料列（可能很慢）沒有簡單的方法。 此外，絕對提取在動態資料指標中並不實用，因為資料列數目會隨著插入和刪除資料列而變更;因此，連續提取相同的資料列數目可能會產生不同的資料列。  
  
 使用 **SQLFetchScroll** 的應用程式僅適用于其區塊資料指標功能（例如報表），很可能只會使用提取下一個資料列集的選項，一次傳遞結果集。 另一方面，以螢幕為基礎的應用程式可以利用 **SQLFetchScroll**的所有功能。 如果應用程式將資料列集大小設定為畫面上顯示的資料列數目，並將螢幕緩衝區系結至結果集，則可以直接將捲軸作業轉譯為 **SQLFetchScroll**的呼叫。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|*FetchOffset*等於-1 的 SQL_FETCH_RELATIVE|  
|向下捲動一行|*FetchOffset*等於1的 SQL_FETCH_RELATIVE|  
|捲動方塊位於頂端|SQL_FETCH_FIRST|  
|捲動方塊于底部|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
 這類應用程式也需要在滾動操作（需要目前的資料列數目和資料列數目）之後放置捲動方塊。 針對目前的資料列編號，應用程式可以追蹤目前的資料列數目，或使用 SQL_ATTR_ROW_NUMBER 屬性來呼叫 **SQLGetStmtAttr** ，以抓取它。  
  
 資料指標中的資料列數目，也就是結果集的大小，會以診斷標頭的 SQL_DIAG_CURSOR_ROW_COUNT 欄位形式提供。 只有在呼叫 **SQLExecute**、 **SQLExecDirect**或 **SQLMoreResult** 之後，才會定義此欄位中的值。 此計數可以是大約計數或確切計數，視驅動程式的功能而定。 您可以藉由呼叫 **SQLGetInfo** 與資料指標屬性資訊類型，並檢查是否針對資料指標的類型傳回 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 位，藉以判斷驅動程式的支援。  
  
 動態資料指標不支援精確的資料列計數。 針對其他類型的資料指標，驅動程式可以支援精確或近似的資料列計數，但不能同時支援兩者。 如果驅動程式針對特定資料指標類型不支援確切或近似的資料列計數，則 SQL_DIAG_CURSOR_ROW_COUNT 欄位會包含目前為止已提取的資料列數目。 無論驅動程式支援何種功能， **SQLFetchScroll** SQL_FETCH_LAST *的作業* 都會導致 SQL_DIAG_CURSOR_ROW_COUNT 欄位包含確切的資料列計數。
