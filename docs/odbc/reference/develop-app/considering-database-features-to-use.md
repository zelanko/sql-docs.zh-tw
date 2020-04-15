---
title: 考慮要使用的資料庫功能 |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9d966781def1c3eab6a9568eab07ab591326171
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299008"
---
# <a name="considering-database-features-to-use"></a>考慮要使用的資料庫功能
已知基本互操作性級別後,必須考慮應用程式使用的資料庫功能。 例如,應用程式將執行哪些 SQL 語句? 應用程式是否會使用可滾動的游標? 交易? 程式? 長數據? 有關哪些功能可能不受所有 DBMS 支援的想法,請參閱[SQLGetInfo、SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)與[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函數描述以及[附錄 C:SQL 語法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 應用程式所需的功能可能會從目標 DBMS 清單中消除某些 DBMS。 它們還可以表明,應用程式可以輕鬆定位許多 DBMS。  
  
 例如,如果所需的功能很簡單,它們通常可以通過高度的互操作性實現。 執行簡單**SELECT**語句並使用僅轉發游標檢索結果的應用程式由於其簡單性,很可能高度互通:幾乎所有驅動程式和 DBMS 都支援所需的功能。  
  
 但是,如果所需的功能更為複雜,例如可滾動遊標、定位更新和刪除語句以及過程,則通常必須進行權衡。 有數種可能性：  
  
-   **降低互操作性,提供更多功能。** 該應用程式包括這些功能,但僅適用於支援它們的 DBMS。  
  
-   **更高的互操作性,更少的功能。** 應用程式刪除功能,但適用於更多的 DBMS。  
  
-   **更高的互操作性,可選功能。** 該應用程式包括這些功能,但僅提供支援這些功能的 DBMS。  
  
-   **更高的互操作性,更多的功能。** 應用程式使用具有支援它們的 DBMS 的功能,並為不支援它們的 DBMS 模擬這些功能。  
  
 前兩種情況的實現相對簡單,因為這些功能要麼與所有支援的 DBMS 一起使用,要麼與無。 另一方面,后兩種情況更為複雜。 在這兩種情況下,都需要檢查 DBMS 是否支援這些功能,最後情況下,需要編寫大量代碼來類比這些功能。 因此,這些方案可能需要更多的開發時間,並且在運行時可能較慢。  
  
 請考慮可以連接到單個數據源的通用查詢應用程式。 應用程式接受用戶的查詢,並在視窗中顯示結果。 現在假設此應用程式具有一個功能,允許使用者同時顯示多個查詢的結果。 也就是說,他們可以執行查詢並查看某些結果,執行不同的查詢並查看其某些結果,然後返回到第一個查詢。 這會帶來互操作性問題,因為某些驅動程式僅支援單個活動語句。  
  
 應用程式有許多選擇,具體取決於驅動程式傳回的**SQLGetInfo**中SQL_MAX_CONCURRENT_ACTIVITIES選項 :  
  
-   **始終支援多個查詢。** 連接到驅動程式後,應用程式將檢查活動語句的數量。 如果驅動程式僅支援一個活動語句,則應用程式將關閉連接並通知使用者驅動程式不支援所需的功能。 該應用程式易於實現,具有完整的功能,但互操作性較低。  
  
-   **從不支援多個查詢。** 應用程式完全放棄該功能。 它易於實現,具有高互操作性,但功能較少。  
  
-   **僅當驅動程式支援多個查詢時,才支援多個查詢。** 連接到驅動程式後,應用程式將檢查活動語句的數量。 僅當驅動程式支援多個活動語句時,應用程式才允許用戶啟動新語句。 該應用程式具有更高的功能和互操作性,但更難實現。  
  
-   **始終支援多個查詢,並在必要時對其進行類比。** 連接到驅動程式後,應用程式將檢查活動語句的數量。 應用程式始終允許使用者在已處於活動狀態時啟動新語句。 如果驅動程式僅支援一個活動語句,則應用程式將打開到該驅動程式的附加連接,並在該連接上執行新語句。 該應用程式具有完整的功能和高互操作性,但更難實現。
