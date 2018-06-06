---
title: 考慮要使用的資料庫功能 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], database features
ms.assetid: 59760114-508e-46c5-81d2-8f2498c0d778
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 264acbea3c73679cf14e9459aea98c0a2a646b0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="considering-database-features-to-use"></a>考慮要使用的資料庫功能
已知的互通性的基本層級之後，您必須考量應用程式所使用的資料庫功能。 例如，哪些 SQL 陳述式將應用程式執行？ 應用程式會使用可捲動資料指標？ 交易嗎？ 程序？ Long 資料嗎？ 如需所有 Dbms 可能不都支援哪些功能的想法，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)， [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)，和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函式描述，以及[附錄 c: SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 應用程式所需的功能可能會排除某些 Dbms 從目標 Dbms 的清單。 它們也可能會顯示應用程式可以輕鬆地目標許多 Dbms。  
  
 比方說，如果是簡單的必要的功能，它們可以通常用來實作的高度互通性。 執行簡單的應用程式**選取**順向資料指標的陳述式並擷取結果很可能是由於其簡易性具備高度互通性： 幾乎所有的驅動程式和 Dbms 支援的功能它需求。  
  
 不過，如果是更複雜，例如可捲動資料指標、 定位的 update 和 delete 陳述式，以及程序的必要的功能，取捨通常必須是進行。 有數種可能性：  
  
-   **較低的互通性，更多的功能。** 應用程式包含的功能，但只適用於支援它們的 Dbms。  
  
-   **較高的互通性，較少的功能。** 應用程式會卸除的功能，但可搭配多個 Dbms。  
  
-   **較高的互通性，選用功能。** 應用程式包含功能，但可讓它們只適用於這些支援的 Dbms。  
  
-   **較高的互通性，更多的功能。** 應用程式使用的功能與支援的 Dbms 和 Dbms 並不會模擬它們。  
  
 前兩個情況下會實作，很簡單的因為與所有支援的 Dbms 或都未使用的功能。 相反地，後者的兩種情況下，是較為複雜。 必須在這兩個案例，以檢查 DBMS 是否支援功能和撰寫大量程式碼，以模擬這些功能最後一種情況。 因此，這些配置可能需要更多的開發時間，而且可能會在執行階段變慢。  
  
 請考慮一般查詢應用程式可以連接到單一資料來源。 應用程式會接受從使用者查詢，並在視窗中顯示結果。 現在假設此應用程式的其中一項功能可讓使用者顯示的結果，多個查詢同時。 也就是執行查詢並查看結果的部分、 執行不同的查詢和看一些其結果，便能然後返回第一個查詢。 這會帶來交互操作性問題，因為有些驅動程式支援只有單一使用中陳述式。  
  
 應用程式具有驅動程式傳回 SQL_MAX_CONCURRENT_ACTIVITIES 選項中為基礎的選項數目**SQLGetInfo**:  
  
-   **一律支援多個查詢。** 連接到驅動程式之後，應用程式檢查作用中陳述式數目。 如果驅動程式支援只有一個使用中陳述式，則應用程式關閉連接，並會通知使用者此驅動程式不支援必要的功能。 應用程式很容易實作且具有完整功能，不過其較低的互通性。  
  
-   **不支援多個查詢。** 應用程式會一併卸除此功能。 它可以輕鬆地實作和高互通性但有較少的功能。  
  
-   **只有當驅動程式會支援多個查詢。** 連接到驅動程式之後，應用程式檢查作用中陳述式數目。 應用程式可讓使用者啟動新的陳述式時其中一個已在使用中，只有當驅動程式支援多個作用中陳述式。 應用程式有較高的功能和互通性，但較難實作。  
  
-   **一律支援多個查詢，並模擬它們在必要時。** 連接到驅動程式之後，應用程式檢查作用中陳述式數目。 應用程式永遠可讓使用者啟動新的陳述式時其中一個已在使用中。 如果驅動程式支援只有一個使用中陳述式，應用程式就會開啟該驅動程式的其他連接，並在該連接上執行新的陳述式。 應用程式有完整的功能和高互通性，但較難實作。
