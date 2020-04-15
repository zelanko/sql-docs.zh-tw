---
title: 相對和絕對滾動 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300098"
---
# <a name="relative-and-absolute-scrolling"></a>相對與絕對的捲動
**SQLFetchScroll**中的大多數滾動選項將游標相對於當前位置或絕對位置的位置放置。 **SQLFetchScroll**支援提取下一個、先行、第一行和最後一個行集,以及相對提取(從當前行集的開頭提取行*n*行)和絕對提取(從行*n*開始提取行集)。 如果*n*在絕對提取中為負數,則行將從結果集的末尾計數。 因此,行 -1 的絕對提取意味著獲取以結果集中的最後一行開頭的行集。  
  
 動態游標檢測插入的結果集並從中刪除的行,因此,除了從結果集的開頭讀取行之外,動態游標無法輕鬆檢索行,這可能很慢。 此外,絕對提取在動態游標中不是很有用,因為行號會隨著行的插入和刪除而變化;因此,連續獲取同一行號可以產生不同的行。  
  
 僅對其塊游標功能(如報表)使用**SQLFetchScroll**的應用程式可能會通過結果集一次,僅使用該選項獲取下一個行集。 另一方面,基於螢幕的應用程式可以利用**SQLFetchScroll**的所有功能。 如果應用程式將行集大小設置為螢幕上顯示的行數,並將螢幕緩衝區綁定到結果集,則可以將滾動條操作直接轉換為對**SQLFetchScroll**的調用。  
  
|捲軸作業|SQLFetchScroll 捲動選項|  
|--------------------------|-------------------------------------|  
|向上捲動一頁|SQL_FETCH_PRIOR|  
|向下捲動一頁|SQL_FETCH_NEXT|  
|向上捲動一行|SQL_FETCH_RELATIVE*提取偏移*量等於 -1|  
|向下捲動一行|SQL_FETCH_RELATIVE*擷取位移*等於 1|  
|頂端捲軸|SQL_FETCH_FIRST|  
|底部捲軸框|SQL_FETCH_LAST|  
|隨機捲動方塊位置|SQL_FETCH_ABSOLUTE|  
  
 此類應用程式還需要在滾動操作后定位滾動框,此操作需要當前行號和行數。 對於當前行號,應用程式可以跟蹤當前行號,也可以使用SQL_ATTR_ROW_NUMBER屬性調用**SQLGetStmtAttr**來檢索它。  
  
 游標中的行數(結果集的大小)可作為診斷標頭的SQL_DIAG_CURSOR_ROW_COUNT欄位提供。 此欄位中的值僅在調用**SQLExecute、SQLExecDirect**或**SQLMoreResult**後定義。 **SQLExecute** 此計數可以是近似計數或精確計數,具體取決於驅動程式的功能。 可以通過調用**SQLGetInfo**與游標屬性資訊類型並檢查是否為游標類型返回SQL_CA2_CRC_APPROXIMATE位或SQL_CA2_CRC_EXACT位來確定驅動程式的支援。  
  
 動態游標從不支援確切的行計數。 對於其他類型的游標,驅動程式可以支援精確或近似行計數,但不能同時支援這兩者。 如果驅動程式既不支援特定游標類型的精確行計數,也不支援近似行計數,則SQL_DIAG_CURSOR_ROW_COUNT欄位包含到目前為止已提取的行數。 無論驅動程式支援什麼,具有 SQL_FETCH_LAST*操作*的**SQLFetchScroll**都將導致SQL_DIAG_CURSOR_ROW_COUNT欄位包含確切的行計數。
