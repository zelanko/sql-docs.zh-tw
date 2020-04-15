---
title: 捲動與擷取行 (ODBC) |微軟文件
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
ms.openlocfilehash: 72d262bf73e69388f65ff281e62235d2d831669e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304199"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>捲動與擷取資料列 (ODBC)
使用可滾動遊標時,應用程式調用**SQLFetchScroll**來定位游標並提取行。 **SQLFetchScroll**支援相對滾動(下一行、上行和相對*n*行)、絕對滾動(第一行、最後行和第*n*行)以及按書籤進行定位。 **SQLFetchScroll**中的 *「提取方向*」和 *「提取偏移」* 參數指定要提取的行集,如下圖所示。  
  
 ![提取下一個、上一個、第一個和最後一個資料列集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **提取下一個、上一個、第一個和最後一個資料列集**  
  
 ![提取絕對、相對和加上書籤的資料列集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **取得絕對、相對和書籤的行集**  
  
 **SQLFetchScroll**將游標定位到指定的行,並返回行集中的行,從該行開始。 如果指定的行集與結果集的末尾重疊,則返回部分行集。 如果指定的行集與結果集的開始重疊,則通常返回結果集中的第一個行集;如果指定行集與結果集的開頭重疊,則通常會返回結果集中的第一個行集。有關完整詳細資訊,請參閱[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函數說明。  
  
 在某些情況下,應用程式可能希望在不檢索任何數據的情況下定位游標。 例如,它可能需要測試行是否存在,或者只是獲取行的書籤,而不通過網路傳輸其他數據。 為此,它將SQL_ATTR_RETRIEVE_DATA語句屬性設置為SQL_RD_OFF。 綁定到書籤列(如果有)的變數始終更新,而不考慮此屬性的設置。  
  
 檢索行集後,應用程式可以調用**SQLSetPos**定位到行集中的特定行或刷新行集中的行。 有關使用**SQLSetPos**的詳細資訊,請參閱[使用 SQLSetPos 更新資料](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  ODBC 2 支援滾動。*x*驅動程式由**SQL 擴充 。** 有關詳細資訊,請參閱附錄 G 中的[塊游標、可滾動游標和向後相容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md):向後相容性的驅動程式指南。
