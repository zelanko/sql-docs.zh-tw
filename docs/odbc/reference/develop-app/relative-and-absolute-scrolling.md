---
title: 相對與絕對的捲動 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e2034a3922dcd3db77113e08a6c48fe7ac39457f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138063"
---
# <a name="relative-and-absolute-scrolling"></a>相對與絕對的捲動
捲動選項中的大部分**SQLFetchScroll**游標的位置，相對於目前的位置或絕對位置。 **SQLFetchScroll**支援提取下一步 之前，第一個和最後一個資料列集，做為也為相對提取 (提取資料列集*n*從目前的資料列集開始的資料列) 和絕對提取 （提取的資料列集開始在資料列*n*)。 如果*n*是負的絕對提取中，會計算資料列從結果集的結尾。 因此，絕對提取的資料列-1 表示提取結果集內的最後一個資料列的開頭資料列集。  
  
 動態資料指標偵測資料列插入和刪除結果集中，所以沒有簡單的方法來擷取結果集，這可能會變慢的開頭位於以外讀取的特定數字的資料列的動態資料指標。 此外，絕對提取不是很有用的動態資料指標因為資料列數字變更為插入和刪除; 資料列因此，後續擷取相同的資料列數目可能會產生不同的資料列。  
  
 使用應用程式**SQLFetchScroll**僅針對其區塊資料指標的功能，例如報表可能會通過結果集一次，僅使用選項來擷取下一個資料列集。 以螢幕為基礎的應用程式，相反地，可以利用所有的功能**SQLFetchScroll**。 如果應用程式設定的資料列集大小的螢幕上顯示的資料列數目，並將螢幕緩衝區繫結至結果集，它可以將轉譯直接到呼叫的捲軸作業**SQLFetchScroll**。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|Sql_fetch_relative 使用，但*FetchOffset*等於-1|  
|向下捲動一行|Sql_fetch_relative 使用，但*FetchOffset*等於 1|  
|在頂端的捲動方塊|SQL_FETCH_FIRST|  
|在底部的捲軸方塊|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
 這類應用程式也需要定位捲動方塊捲動作業之後，需要目前的資料列編號和資料列數目。 目前的資料列數目，應用程式可以是追蹤的目前資料列數目或呼叫**SQLGetStmtAttr** SQL_ATTR_ROW_NUMBER 屬性來擷取它。  
  
 資料指標，也就是結果的大小中的資料列數目設定，可作為診斷的標頭的 SQL_DIAG_CURSOR_ROW_COUNT 欄位。 在此欄位中的值之後才定義**SQLExecute**， **SQLExecDirect**，或**SQLMoreResult**已呼叫。 這個計數可以是近似的計數或確切的計數，視驅動程式的功能而定。 驅動程式的支援可決定藉由呼叫**SQLGetInfo**與資料指標屬性的資訊類型檢查的 SQL_CA2_CRC_APPROXIMATE 或 SQL_CA2_CRC_EXACT 位元是否會傳回資料指標的類型。  
  
 動態資料指標並不支援的實際資料列計數。 對於其他類型的資料指標中，驅動程式可支援精確或大約的資料列計數，但非兩者。 如果驅動程式不支援精確或大約的資料列計數的特定資料指標類型、 SQL_DIAG_CURSOR_ROW_COUNT 欄位包含截至目前為止已經提取的資料列數目。 支援哪些驅動程式，不論**SQLFetchScroll**具有*作業*的 SQL_FETCH_LAST 會導致 SQL_DIAG_CURSOR_ROW_COUNT 欄位包含實際資料列計數。
