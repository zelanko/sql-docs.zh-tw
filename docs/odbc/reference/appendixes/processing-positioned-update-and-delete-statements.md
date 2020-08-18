---
description: 處理定點更新和刪除陳述式
title: 處理定位的 Update 和 Delete 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e5acd8afe46397126ddb4c1d4127eb99fc67a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483201"
---
# <a name="processing-positioned-update-and-delete-statements"></a>處理定點更新和刪除陳述式
> [!IMPORTANT]  
>  未來的 Windows 版本將會移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫支援定位 update 和 delete 語句，其方式是將這類語句中的 **WHERE CURRENT** of 子句取代為 **where** 子句，以列舉針對每個系結資料行的快取中儲存的值。 資料指標程式庫會將新建立的 **UPDATE** 和 **DELETE** 語句傳遞至驅動程式來執行。 若為定位的 update 語句，資料指標程式庫會從資料列集緩衝區中的值更新其快取，並將資料列狀態陣列中的對應值設定為 SQL_ROW_UPDATED。 若為定位 delete 語句，它會將資料列狀態陣列中的對應值設定為 SQL_ROW_DELETED。  
  
> [!CAUTION]  
>  資料指標程式庫所建立用來識別目前資料列的 **WHERE** 子句，可能無法識別任何資料列、識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱本附錄稍後的「 [建立搜尋的語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)」。  
  
 定位的 update 和 delete 語句受到下列限制：  
  
-   只有在下列情況下，才可以使用定點更新和刪除語句：當 **SELECT** 語句產生結果集時：當 **SELECT** 語句未包含聯結、 **UNION** 子句或 **group by** 子句時：以及當在選取清單中使用別名或運算式的任何資料行未與 **SQLBindCol**系結時。  
  
-   如果應用程式準備了定位的 update 或 delete 語句，則在呼叫 **SQLFetch** 或 **SQLFetchScroll**之後，就必須這樣做。 雖然資料指標程式庫會將語句提交至驅動程式以進行準備，但是它會關閉語句，並在應用程式呼叫 **SQLExecute**時直接執行語句。  
  
-   如果驅動程式只支援一個作用中的語句，則資料指標程式庫會提取結果集的其餘部分，然後從其快取中 refetches 目前的資料列集，然後再執行定位的 update 或 delete 語句。 如果應用程式接著呼叫的函式會傳回結果集中的中繼資料 (例如， **SQLNumResultCols** 或 **SQLDescribeCol**) ，資料指標程式庫會傳回錯誤。  
  
-   如果在資料表的資料行上執行定位的 update 或 delete 語句，而該資料行包含時間戳記資料行，而且每次執行更新時都會自動更新，則所有後續的定點更新或刪除語句都會在時間戳記資料行已系結時失敗。 發生這種情況是因為資料指標程式庫所建立的搜尋 update 或 delete 語句不會正確地識別要更新的資料列。 時間戳記資料行之搜尋語句中的值將不會符合時間戳記資料行的自動更新值。
