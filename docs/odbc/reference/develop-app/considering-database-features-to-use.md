---
title: 正在考慮要使用的資料庫功能 |Microsoft Docs
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
ms.openlocfilehash: 3a945eef43a1fc12689853c3fa209f6126df4f0d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67951874"
---
# <a name="considering-database-features-to-use"></a>考慮要使用的資料庫功能
知道基本的互通性層級之後，就必須考慮應用程式所使用的資料庫功能。 例如，應用程式會執行哪些 SQL 語句？ 應用程式是否會使用可滾動的資料指標？ 交易? 規程? 長資料？ 如需所有 Dbms 可能不支援哪些功能的想法，請參閱[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和[SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)函式描述，以及[附錄 C： SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 應用程式所需的功能可能會排除目標 Dbms 清單中的某些 Dbms。 他們可能也會顯示應用程式可以輕鬆地將目標設為許多 Dbms。  
  
 例如，如果所需的功能很簡單，通常可以透過高程度的互通性來執行。 執行簡單**SELECT**語句並以順向資料指標抓取結果的應用程式，可能會因為其簡單性而高度互通：幾乎所有的驅動程式和 dbms 都支援其所需的功能。  
  
 不過，如果必要的功能較複雜，例如可滾動的資料指標、定位的 update 和 delete 語句，以及程式，則通常必須進行取捨。 有數種可能性：  
  
-   **較低的互通性，更多功能。** 應用程式包含功能，但僅適用于支援它們的 Dbms。  
  
-   **更高的互通性，功能較少。** 應用程式會捨棄功能，但會使用更多 Dbms。  
  
-   **更高的互通性，選擇性功能。** 應用程式包含功能，但只能與支援它們的 Dbms 搭配使用。  
  
-   **更高的互通性，更多功能。** 應用程式會使用支援這些功能的 Dbms，並針對不是的 Dbms 模擬它們。  
  
 前兩個案例相當容易執行，因為這些功能會搭配所有支援的 Dbms 或 none 來使用。 另一方面，第二個案例則較為複雜。 在這兩種情況下，都必須檢查 DBMS 是否支援這些功能，以及在最後一種情況下，撰寫可能大量的程式碼來模擬這些功能。 因此，這些配置可能需要更多的開發時間，而且可能會在執行時間變慢。  
  
 請考慮可以連接到單一資料來源的一般查詢應用程式。 應用程式會接受使用者的查詢，並將結果顯示在視窗中。 現在假設此應用程式有一項功能，可讓使用者同時顯示多個查詢的結果。 也就是說，他們可以執行查詢並查看一些結果，執行不同的查詢並查看其結果，然後返回第一個查詢。 這會帶來互通性問題，因為有些驅動程式只支援單一作用中的語句。  
  
 應用程式有許多選擇，根據驅動程式針對**SQLGetInfo**中的 SQL_MAX_CONCURRENT_ACTIVITIES 選項所傳回的內容而定：  
  
-   **一律支援多個查詢。** 連接到驅動程式之後，應用程式會檢查使用中的語句數目。 如果驅動程式只支援一個作用中的語句，應用程式會關閉連線，並通知使用者該驅動程式不支援所需的功能。 應用程式很容易執行，而且具備完整的功能，但具有較低的互通性。  
  
-   **永遠不支援多個查詢。** 應用程式會完全卸載功能。 這很容易實行，而且具有高互通性，但功能較少。  
  
-   **只有在驅動程式執行時，才支援多個查詢。** 連接到驅動程式之後，應用程式會檢查使用中的語句數目。 只有當驅動程式支援多個作用中語句時，應用程式才可讓使用者啟動新的語句。 應用程式具有較高的功能和互通性，但較難實現。  
  
-   **一定會支援多個查詢，並在必要時加以模擬。** 連接到驅動程式之後，應用程式會檢查使用中的語句數目。 應用程式一律允許使用者在已在使用中的狀態時啟動新的語句。 如果驅動程式只支援一個作用中的語句，應用程式會開啟該驅動程式的額外連接，並在該連接上執行新的語句。 應用程式具有完整的功能和高互通性，但較難實現。
