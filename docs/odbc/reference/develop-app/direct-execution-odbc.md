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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305159"
---
# <a name="direct-execution-odbc"></a>直接執行 ODBC
直接執行是執行語句最簡單的方式。 提交語句以進行執行時，資料來源會將它編譯成存取計畫，然後執行該存取計畫。  
  
 直接執行通常是由在執行時間建立和執行語句的泛型應用程式所使用。 例如，下列程式碼會建立 SQL 語句，並一次執行它：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接執行最適用于只會執行一次的語句。 其主要缺點是每次執行時都會剖析 SQL 語句。 此外，應用程式無法抓取語句所建立之結果集的相關資訊（如果有的話），直到執行語句為止。如果語句是以兩個不同的步驟來準備和執行，就可能發生這種情況。  
  
 若要直接執行語句，應用程式會執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱本節稍後的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  呼叫**SQLExecDirect** ，並將包含 SQL 語句的字串傳遞給它。  
  
3.  呼叫**SQLExecDirect**時，驅動程式：  
  
    -   修改 SQL 語句，以使用資料來源的 SQL 文法，而不剖析語句;這包括取代 ODBC 中的[Escape 序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)中所討論的逸出序列。 應用程式可以藉由呼叫**SQLNativeSql**來捕獲 SQL 語句的修改形式。 如果已設定 SQL_ATTR_NOSCAN 語句屬性，則不會取代逸出序列。  
  
    -   抓取目前的參數值，並視需要加以轉換。 如需詳細資訊，請參閱本節稍後的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   將語句和已轉換的參數值傳送至資料來源以便執行。  
  
    -   傳回任何錯誤。 這些包括排序或狀態診斷，例如 SQLSTATE 24000 （不正確資料指標狀態）、語法錯誤（例如 SQLSTATE 42000 （語法錯誤或存取違規））和語意錯誤（例如 SQLSTATE 42S02 （基表或找不到 view））。
