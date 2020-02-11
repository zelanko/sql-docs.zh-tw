---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41b4fe248f815e63c48a8da70edc88a1cc173667
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028433"
---
# <a name="processing-positioned-update-and-delete-statements"></a>處理定點更新和刪除陳述式
> [!IMPORTANT]  
>  這項功能將會在未來的 Windows 版本中移除。 請避免在新的開發工作中使用這項功能，並規劃修改目前使用這項功能的應用程式。 Microsoft 建議使用驅動程式的資料指標功能。  
  
 資料指標程式庫支援定位 update 和 delete 語句，方法是將這類語句中的**WHERE CURRENT** of 子句取代成**where**子句，以列舉每個系結資料行的快取中儲存的值。 資料指標程式庫會將新建立的**UPDATE**和**DELETE**語句傳遞給驅動程式，以便執行。 針對定位的 update 語句，資料指標程式庫接著會從資料列集緩衝區中的值更新其快取，並將資料列狀態陣列中對應的值設定為 SQL_ROW_UPDATED。 若為定位 delete 語句，它會將資料列狀態陣列中對應的值設定為 SQL_ROW_DELETED。  
  
> [!CAUTION]  
>  用來識別目前資料列的資料指標程式庫所建立的**WHERE**子句，可能無法識別任何資料列、識別不同的資料列，或識別一個以上的資料列。 如需詳細資訊，請參閱本附錄稍後的「[建立搜尋的語句](../../../odbc/reference/appendixes/constructing-searched-statements.md)」。  
  
 定位的 update 和 delete 語句受到下列限制：  
  
-   只有在下列情況下，才可以使用定位的 update 和 delete 語句：當**SELECT**語句產生結果集時。當**SELECT**語句不包含 Join、 **UNION**子句或**GROUP BY**子句時。而且，當在選取清單中使用別名或運算式的任何資料行未與**SQLBindCol**系結時。  
  
-   如果應用程式準備了定位的 update 或 delete 語句，它就必須在呼叫**SQLFetch**或**SQLFetchScroll**之後這麼做。 雖然資料指標程式庫會將語句提交給驅動程式以進行準備，但它會關閉語句，並在應用程式呼叫**SQLExecute**時直接執行。  
  
-   如果驅動程式只支援一個現用語句，則資料指標程式庫會提取結果集的其餘部分，然後在執行定位的 update 或 delete 語句之前，從其快取中 refetches 目前的資料列集。 如果應用程式接著呼叫的函式會傳回結果集中的中繼資料（例如， **SQLNumResultCols**或**SQLDescribeCol**），則資料指標程式庫會傳回錯誤。  
  
-   如果在包含時間戳記資料行的資料表資料行上執行定位的 update 或 delete 語句，且每次執行更新時都會自動更新，則所有後續定位的 update 或 delete 語句將會失敗，但時間戳記資料行為限制. 發生這種情況的原因是，資料指標程式庫所建立的搜尋 update 或 delete 語句將無法正確識別要更新的資料列。 時間戳記資料行之搜尋語句中的值，不符合 timestamp 資料行自動更新的值。
