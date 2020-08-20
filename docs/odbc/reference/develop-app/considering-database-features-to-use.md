---
description: 考慮要使用的資料庫功能
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2abaed3806514a161c5c506d8bad89b4d3b75153
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465890"
---
# <a name="considering-database-features-to-use"></a>考慮要使用的資料庫功能
在瞭解基本層級的互通性之後，必須考慮應用程式所使用的資料庫功能。 例如，應用程式會執行哪些 SQL 語句？ 應用程式會使用可滾動的資料指標嗎？ 交易？ 程式？ 長資料？ 如需所有 Dbms 都可能不支援哪些功能的相關概念，請參閱 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)、 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)和 [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) 函式說明，以及 [附錄 C： SQL 文法](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md)。 應用程式所需的功能可能會從目標 Dbms 清單中消除一些 Dbms。 它們也可能會顯示應用程式很容易以許多 Dbms 為目標。  
  
 例如，如果所需的功能很簡單，通常可以使用高度互通性來實行。 執行簡單的 **SELECT** 語句，並使用順向資料指標抓取結果的應用程式，可能會因為其簡潔性而高度互通：幾乎所有的驅動程式和 dbms 都支援所需的功能。  
  
 但是，如果必要的功能更複雜，例如可滾動的資料指標、定位 update 和 delete 語句，以及程式，通常必須進行取捨。 有數種可能性：  
  
-   **更低的互通性、更多功能。** 應用程式會包含功能，但只適用于支援這些功能的 Dbms。  
  
-   **更高的互通性，功能較少。** 應用程式會卸載功能，但可搭配更多 Dbms 使用。  
  
-   **更高的互通性、選擇性功能。** 應用程式會包含功能，但只提供它們給支援這些功能的 Dbms。  
  
-   **更高的互通性、更多功能。** 應用程式會使用支援這些功能的 Dbms 功能，並針對非的 Dbms 進行模擬。  
  
 前兩個案例相當簡單，因為這些功能會搭配所有支援的 Dbms 或無使用。 另一方面，後者的兩個案例比較複雜。 這兩種情況都必須檢查 DBMS 是否支援這些功能，而在最後一個案例中，撰寫可能大量的程式碼來模擬這些功能。 因此，這些配置可能需要更多的開發時間，而且在執行時間可能會變慢。  
  
 請考慮可以連接到單一資料來源的一般查詢應用程式。 應用程式會接受使用者的查詢，並在視窗中顯示結果。 現在假設此應用程式有一項功能，可讓使用者同時顯示多個查詢的結果。 也就是說，他們可以執行查詢並查看某些結果、執行不同的查詢並查看其某些結果，然後返回第一個查詢。 這會呈現互通性問題，因為有些驅動程式僅支援單一使用中的語句。  
  
 應用程式有許多選擇，根據驅動程式針對 **SQLGetInfo**中的 SQL_MAX_CONCURRENT_ACTIVITIES 選項所傳回的內容而定：  
  
-   **一律支援多個查詢。** 連接到驅動程式之後，應用程式會檢查使用中語句的數目。 如果驅動程式只支援一個作用中的語句，則應用程式會關閉連線，並通知使用者驅動程式不支援所需的功能。 應用程式很容易執行，而且具有完整的功能，但互通性較低。  
  
-   **永遠不支援多個查詢。** 應用程式會全部卸載功能。 它很容易執行，而且具有高互通性，但功能較少。  
  
-   **只有在驅動程式執行時，才支援多個查詢。** 連接到驅動程式之後，應用程式會檢查使用中語句的數目。 應用程式可讓使用者在驅動程式支援多個使用中語句時，啟動新的語句（如果有的話）。 應用程式具有較高的功能和互通性，但較難實行。  
  
-   **一律支援多個查詢，並在必要時加以模擬。** 連接到驅動程式之後，應用程式會檢查使用中語句的數目。 當應用程式已經在使用中時，應用程式一律會允許使用者啟動新的語句。 如果驅動程式只支援一個作用中的語句，則應用程式會開啟該驅動程式的其他連接，並在該連接上執行新的語句。 應用程式具有完整的功能和高互通性，但較難實行。
