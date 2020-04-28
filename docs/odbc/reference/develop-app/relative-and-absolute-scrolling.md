---
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
ms.openlocfilehash: ae0ed5af8d116a3038b55b1e3d68231154c2a35c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300098"
---
# <a name="relative-and-absolute-scrolling"></a>相對與絕對的捲動
**SQLFetchScroll**中的大部分滾動選項會將游標放在相對於目前位置或絕對位置的位置。 **SQLFetchScroll**支援提取下一個、上一個、第一個和最後一個資料列集，以及相對提取（從目前資料列集的開頭提取資料列集*n*個數據列）和絕對提取（提取從第*n*行開始的資料列集）。 如果*n*在絕對提取中為負數，則會從結果集的結尾計算資料列。 因此，從結果集中的最後一個資料列開始，資料列1的絕對提取方法就是提取資料列集。  
  
 動態資料指標會偵測從結果集插入和刪除的資料列，因此，動態資料指標沒有簡單的方法可以從結果集開頭讀取的特定數位來抓取資料列，這可能會很慢。 此外，在動態資料指標中，絕對提取並沒有太大説明，因為插入和刪除資料列時，資料列編號會變更;因此，連續提取相同的資料列數目可能會產生不同的資料列。  
  
 僅針對其區塊資料指標功能使用**SQLFetchScroll**的應用程式（例如報表）可能會通過單一時間的結果集，而只會使用提取下一個資料列集的選項。 另一方面，以螢幕為基礎的應用程式可以利用**SQLFetchScroll**的所有功能。 如果應用程式將資料列集大小設定為螢幕上顯示的資料列數目，並將螢幕緩衝區系結至結果集，則可以直接將捲軸作業轉譯為呼叫**SQLFetchScroll**。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|*FetchOffset*等於-1 的 SQL_FETCH_RELATIVE|  
|向下捲動一行|*FetchOffset*等於1的 SQL_FETCH_RELATIVE|  
|在頂端捲動方塊|SQL_FETCH_FIRST|  
|在底部捲動方塊|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
 這類應用程式也需要在滾動作業之後放置捲動方塊，這需要目前的資料列數目和資料列數目。 對於目前的資料列數目，應用程式可以追蹤目前的資料列數目，或使用 SQL_ATTR_ROW_NUMBER 屬性來呼叫**SQLGetStmtAttr** ，以抓取它。  
  
 資料指標中的資料列數目（也就是結果集的大小）會以診斷標頭的 [SQL_DIAG_CURSOR_ROW_COUNT] 欄位的形式提供。 只有在呼叫**SQLExecute**、 **SQLExecDirect**或**SQLMoreResult**之後，才會定義此欄位中的值。 視驅動程式的功能而定，此計數可以是大約計數或確切計數。 藉由呼叫**SQLGetInfo**與 cursor 屬性資訊類型，並檢查是否傳回資料指標類型的 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 位，即可判斷驅動程式的支援。  
  
 動態資料指標永遠不支援精確的資料列計數。 對於其他類型的資料指標，此驅動程式可以支援精確或近似的資料列計數，但不能兩者都支援。 如果驅動程式針對特定資料指標類型不支援精確或近似的資料列計數，SQL_DIAG_CURSOR_ROW_COUNT 欄位會包含到目前為止已提取的資料列數目。 無論驅動程式支援何種功能， **SQLFetchScroll**作業*Operation* SQL_FETCH_LAST 都會導致 SQL_DIAG_CURSOR_ROW_COUNT 欄位包含精確的資料列計數。
