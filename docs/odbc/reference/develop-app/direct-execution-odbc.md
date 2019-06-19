---
title: 直接執行 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73c061718dc326e43f72be369a28ad12726a3cab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "63242357"
---
# <a name="direct-execution-odbc"></a>直接執行 ODBC
直接執行是執行陳述式的最簡單方式。 當陳述式提交執行時，資料來源會將它編譯成存取計劃，，然後執行該存取計劃。  
  
 直接執行常用的泛型應用程式，建置及執行陳述式在執行階段。 例如，下列程式碼建置 SQL 陳述式，並執行一次：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接執行最適合用於將會執行一次的陳述式。 其主要的缺點是每次執行時，會剖析 SQL 陳述式。 此外，應用程式無法擷取陳述式所建立 （如果有的話） 之前執行的陳述式; 之後的結果集的相關資訊如果已備妥陳述式，和在兩個不同的步驟中執行，這是可行的。  
  
 直接執行陳述式應用程式執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
2.  呼叫**SQLExecDirect**並將它傳遞為字串，包含 SQL 陳述式。  
  
3.  當**SQLExecDirect**呼叫時，驅動程式：  
  
    -   修改 SQL 陳述式，而不剖析陳述式中，使用資料來源的 SQL 文法這包括取代中所討論的逸出序列[ODBC 中的逸出序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。 應用程式可以藉由呼叫擷取的 SQL 陳述式修改後的表單**SQLNativeSql**。 如果 SQL_ATTR_NOSCAN 陳述式屬性設定，不會取代逸出序列。  
  
    -   擷取目前的參數值，並將它們轉換為必要。 如需詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。  
  
    -   將陳述式和轉換的參數值傳送至資料來源，以便執行。  
  
    -   會傳回任何錯誤。 這些包括排序或狀態診斷，例如 SQLSTATE 24000 （無效的資料指標狀態）、 語法錯誤，例如 SQLSTATE 42000 （語法錯誤或存取違規） 和語意錯誤，例如 SQLSTATE 42S02 （基底資料表或檢視找不到）。
