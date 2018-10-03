---
title: 考慮要使用的資料庫功能 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92eeb64b95d666b15c03c70d656d2309a63eabf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693436"
---
# <a name="considering-database-features-to-use"></a>考慮要使用的資料庫功能
已知的互通性的基本層級之後，必須考量應用程式所使用的資料庫功能。 比方說，哪些 SQL 陳述式將應用程式執行？ 將應用程式會使用可捲動資料指標？ 交易？ 程序？ Long 資料？ 針對所有 Dbms 可能不都支援哪些功能的想法，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，並[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函式描述，以及[附錄 C:SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 應用程式所需的功能可能消除某些 Dbms 從目標 Dbms 的清單。 它們也可能會顯示應用程式很容易下手有許多 Dbms。  
  
 比方說，如果所需的功能很簡單，他們可以通常用來實作較高程度的互通性。 執行簡單的應用程式**選取**順向資料指標的陳述式並擷取結果很可能是由於其簡易性高度互通： 幾乎所有的驅動程式和 Dbms 支援的功能它需求。  
  
 不過，如果所需的功能更為複雜，例如可捲動資料指標、 定位的 update 和 delete 陳述式，以及程序，取捨必須有通常的進行。 有數種可能性：  
  
-   **較低的互通性，更多的功能。** 應用程式包含的功能，但只適用於支援它們的 Dbms。  
  
-   **較高的互通性，較少的功能。** 應用程式會卸除但搭配多個 Dbms 的功能。  
  
-   **較高的互通性，選用功能。** 應用程式包含的功能，但使其可供只能搭配這些 Dbms 支援它們。  
  
-   **較高的互通性，更多的功能。** 應用程式使用的功能與支援它們的 Dbms，並模擬它們 Dbms 所沒有的。  
  
 前兩個案例是相當容易實作，因為功能使用所有支援的 Dbms 使用或無。 相反地，後者的兩個情況下，就比較複雜。 必須在這兩個案例，以檢查 DBMS 是否支援的功能，並在最後一個的情況下，撰寫程式碼，以模擬這些功能可能很大的數量。 因此，這些結構描述可能需要更多的開發時間，而且可能會在執行階段變慢。  
  
 請考慮一般查詢應用程式可以連線到單一資料來源。 應用程式接受來自使用者的查詢，並在視窗中顯示結果。 現在假設此應用程式有一項功能可讓使用者顯示的結果，多個查詢同時。 也就是它們可以執行查詢並看看一些結果，執行不同的查詢看看一些其結果，然後返回第一個查詢。 這會帶來交互操作性問題，因為有些驅動程式支援只有單一作用中陳述式。  
  
 應用程式有幾個選項，根據驅動程式傳回 SQL_MAX_CONCURRENT_ACTIVITIES 選項中的**SQLGetInfo**:  
  
-   **一律支援多個查詢。** 連接到驅動程式之後，應用程式檢查作用中陳述式數目。 如果驅動程式支援只有一個作用中陳述式，應用程式就會關閉連接，並會通知使用者此驅動程式不支援必要的功能。 應用程式很容易實作和具有完整功能，但具有較低的互通性。  
  
-   **永遠不會支援多個查詢。** 應用程式會一併卸除此功能。 它很容易實作具有高的互通性，但具有較少的功能。  
  
-   **支援多個查詢，只有當驅動程式執行。** 連接到驅動程式之後，應用程式檢查作用中陳述式數目。 應用程式可讓使用者啟動新的陳述式，當其中一個已在使用中，只有當驅動程式支援多個作用中陳述式。 應用程式有更高的功能和互通性，但較難實作。  
  
-   **請務必支援多個查詢，並模擬它們在必要時。** 連接到驅動程式之後，應用程式檢查作用中陳述式數目。 應用程式一律可讓使用者啟動新的陳述式，當其中一個已在使用中。 如果驅動程式支援只有一個作用中陳述式，應用程式就會開啟該驅動程式的其他連接，並在該連接上執行新的陳述式。 應用程式具有完整的功能和高的互通性，但較難實作。
