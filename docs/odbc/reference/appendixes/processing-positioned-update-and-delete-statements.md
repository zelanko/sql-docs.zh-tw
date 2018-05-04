---
title: 處理定位 Update 和 Delete 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1127c03853ab74cbd51368abb90c9581363f4bd0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="processing-positioned-update-and-delete-statements"></a>處理定位 Update 和 Delete 陳述式
> [!IMPORTANT]  
>  將移除這項功能，在未來的版本的 Windows。 避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫支援定位更新和 delete 陳述式來取代**WHERE CURRENT OF**子句中使用這類陳述式**其中**列舉的值儲存在快取中的子句每個繫結的資料行。 資料指標程式庫傳遞新建構**更新**和**刪除**陳述式來執行的驅動程式。 定位的 update 陳述式，如資料指標程式庫，然後更新其快取的資料列集的緩衝區中的值，並設定 SQL_ROW_UPDATED 資料列狀態陣列中的對應值。 定位的 delete 陳述式，它會 SQL_ROW_DELETED 資料列狀態陣列中設定對應的值。  
  
> [!CAUTION]  
>  **其中**子句所識別的目前資料列的資料指標程式庫建構無法識別任何資料列、 識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱[建構搜尋陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)稍後在本附錄中。  
  
 定位 update 和 delete 陳述式都具有下列限制：  
  
-   定位 update 和 delete 陳述式只能用於下列情況： 當**選取**陳述式產生結果集; 當**選取**陳述式未包含聯結， **等位**子句，或**GROUP BY**子句，且在選取清單中使用的別名或運算式的任何資料行已不繫結與**SQLBindCol**。  
  
-   如果應用程式會準備定位的更新或刪除陳述式，它必須這樣做之後又稱為**SQLFetch**或**SQLFetchScroll**。 雖然資料指標程式庫提交此陳述式來準備的驅動程式，關閉陳述式，並且執行，當應用程式呼叫直接**SQLExecute**。  
  
-   如果驅動程式支援只有一個使用中陳述式，資料指標程式庫擷取結果的其他設定，然後 refetches 從其快取的目前資料列集之前，它會執行定位更新或 delete 陳述式。 如果應用程式接著會呼叫函式傳回結果集內的中繼資料 (例如， **SQLNumResultCols**或**SQLDescribeCol**)，資料指標程式庫會傳回錯誤。  
  
-   如果時間戳記資料行是如果資料表包含每次執行更新時自動更新的時間戳記資料行的資料行上執行定位的更新或刪除陳述式，所有後續的定位的更新或刪除陳述式將會失敗繫結。 這是因為搜尋更新或刪除資料指標程式庫建立陳述式不會精確地識別要更新的資料列。 搜尋的陳述式的時間戳記資料行中的值將不符合時間戳記資料行的自動更新的值。
