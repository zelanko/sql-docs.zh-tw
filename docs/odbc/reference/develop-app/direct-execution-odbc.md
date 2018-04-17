---
title: 直接執行 ODBC |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 09ea0f6d6046a6deb24431dd29d0f91f78226120
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="direct-execution-odbc"></a>直接執行 ODBC
直接執行是最簡單的方式執行的陳述式。 當提交陳述式執行時，資料來源會將它編譯成存取計劃，，然後執行該存取方案。  
  
 直接執行常用的泛型應用程式，建置並執行陳述式在執行階段。 例如，下列程式碼建置 SQL 陳述式，並加以執行一次：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接執行最適合的陳述式，將會執行一次。 其主要缺點是每次執行時，會剖析 SQL 陳述式。 此外，應用程式無法擷取陳述式所建立 （如果有的話） 之前執行的陳述式; 之後的結果集的相關資訊如果陳述式已備妥並執行兩個個別步驟中，這是可行的。  
  
 直接執行陳述式應用程式執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
2.  呼叫**SQLExecDirect**並將其傳遞字串，包含 SQL 陳述式。  
  
3.  當**SQLExecDirect**呼叫時，驅動程式：  
  
    -   修改 SQL 陳述式，而不剖析陳述式中，使用資料來源的 SQL 文法這包括取代所述的逸出序列[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 應用程式可以藉由呼叫擷取 SQL 陳述式的已修改的表單**SQLNativeSql**。 若已設定 SQL_ATTR_NOSCAN 陳述式屬性，不會取代逸出序列。  
  
    -   擷取目前的參數值，並視需要進行轉換。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
    -   將和已轉換的參數值的陳述式傳送至資料來源，以便執行中。  
  
    -   傳回的任何錯誤。 其中包括排序或狀態診斷，例如 SQLSTATE 24000 （無效的資料指標狀態）、 語法錯誤，例如 SQLSTATE 42000 （語法錯誤或存取違規），以及語意錯誤，例如 SQLSTATE 42S02 （基底資料表或檢視表，找不到）。
