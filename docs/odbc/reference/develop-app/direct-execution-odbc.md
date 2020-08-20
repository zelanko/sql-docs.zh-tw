---
description: 直接執行 ODBC
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
ms.openlocfilehash: 9be03c4f20a82e134481f8fd9bb849ffd830567a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476700"
---
# <a name="direct-execution-odbc"></a>直接執行 ODBC
直接執行是執行語句的最簡單方式。 提交要執行的語句時，資料來源會將它編譯成存取計畫，然後執行該存取計畫。  
  
 直接執行通常由在執行時間建立和執行語句的一般應用程式使用。 例如，下列程式碼會建立一個 SQL 語句，並一次執行它：  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 直接執行最適合會執行一次的語句。 它的主要缺點是在每次執行 SQL 語句時都會加以剖析。 此外，在執行語句之前，應用程式無法抓取語句)  (所建立之結果集的相關資訊;如果語句已備妥，並以兩個不同的步驟執行，就可能發生這種情況。  
  
 若要直接執行語句，應用程式會執行下列動作：  
  
1.  設定任何參數的值。 如需詳細資訊，請參閱本節稍後的 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
2.  呼叫 **SQLExecDirect** ，並將包含 SQL 語句的字串傳遞給它。  
  
3.  當呼叫 **SQLExecDirect** 時，驅動程式：  
  
    -   修改 SQL 語句以使用資料來源的 SQL 文法，而不剖析語句;這包括取代 ODBC 中的 [Escape 序列中](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)所討論的 escape 序列。 應用程式可以藉由呼叫 **SQLNativeSql**來取出 SQL 語句的修改形式。 如果設定了 SQL_ATTR_NOSCAN 語句屬性，則不會取代 Escape 序列。  
  
    -   抓取目前的參數值，並視需要進行轉換。 如需詳細資訊，請參閱本節稍後的 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。  
  
    -   將語句和轉換的參數值傳送至資料來源以供執行。  
  
    -   傳回任何錯誤。 這些包括順序或狀態診斷，例如 SQLSTATE 24000 (不正確資料指標狀態) 、語法錯誤（例如 SQLSTATE 42000 (語法錯誤或存取違規) ）以及語意錯誤，例如 SQLSTATE 42S02 (基表或 view 找不到) 。
