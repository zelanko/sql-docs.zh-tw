---
title: 處理定位的 Update 和 Delete 陳述式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d898fcc7d1b35230173afa0443219d59c54720ae
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057071"
---
# <a name="processing-positioned-update-and-delete-statements"></a>處理定點更新和刪除陳述式
> [!IMPORTANT]  
>  Windows 的未來版本將移除這項功能。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 定位資料指標程式庫支援更新和刪除陳述式取代**WHERE CURRENT OF**中使用這類陳述式子句**其中**列舉快取中儲存之值的子句每個繫結的資料行。 資料指標程式庫傳遞新建構**更新**並**刪除**陳述式來執行的驅動程式。 定位的 update 陳述式中，資料指標程式庫，然後更新其快取的資料列集的緩衝區中的值，並設定 SQL_ROW_UPDATED 的資料列狀態陣列中對應的值。 定位的 delete 陳述式，它會 SQL_ROW_DELETED 資料列狀態陣列中設定對應的值。  
  
> [!CAUTION]  
>  **其中**建構的資料指標程式庫，以識別目前的資料列的子句無法識別的任何資料列、 找出不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱 <<c0> [ 建構搜尋的陳述式](../../../odbc/reference/appendixes/constructing-searched-statements.md)稍後在本附錄中。  
  
 定位的 update 和 delete 陳述式會受限於下列限制：  
  
-   定位的 update 和 delete 陳述式只能用於下列情況： 當**選取** 產生的結果集的陳述式; 當**選取**陳述式未包含聯結， **UNION**子句，或有**GROUP BY**子句，且在選取清單中使用的別名或運算式的任何資料行已不繫結與**SQLBindCol**。  
  
-   如果應用程式會準備定位的 update 或 delete 陳述式，它必須這樣之後就叫做**SQLFetch**或是**SQLFetchScroll**。 雖然資料指標程式庫提交陳述式，以準備的驅動程式時，會關閉陳述式，並直接在應用程式的呼叫時執行它**SQLExecute**。  
  
-   如果驅動程式支援只有一個作用中陳述式，資料指標程式庫擷取結果的其餘部分設定，然後 refetches 從其快取的目前資料列集，然後才執行定位更新或 delete 陳述式。 如果應用程式會接著呼叫函式會傳回結果集內的中繼資料 (例如**SQLNumResultCols**或是**SQLDescribeCol**)，資料指標程式庫會傳回錯誤。  
  
-   如果時間戳記資料行是包含每次執行更新時自動更新的時間戳記資料行的資料表的資料行上執行定位的 update 或 delete 陳述式，如果所有後續定位的 update 或 delete 陳述式將會失敗繫結。 這是因為搜尋更新或刪除資料指標程式庫所建立的陳述式不會精確地識別要更新之資料列。 搜尋的陳述式的時間戳記資料行中的值將不符合自動更新時間戳記資料行的值。
