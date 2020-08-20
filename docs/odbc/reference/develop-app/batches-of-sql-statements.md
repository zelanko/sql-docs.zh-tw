---
description: SQL 陳述式的批次
title: SQL 語句的批次 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e342fd7eaef721f8fb0033a5ae022ca8de74cda1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465930"
---
# <a name="batches-of-sql-statements"></a>SQL 陳述式的批次
SQL 語句的批次是兩個或多個 SQL 語句或單一 SQL 語句的群組，其效果與兩個或多個 SQL 語句的群組相同。 在某些情況下，會在任何可用的結果之前執行整個批次語句。 這通常比提交語句更有效率，因為通常可以減少網路流量，而且資料來源有時可能會將 SQL 語句批次的執行優化。 在其他執行中，呼叫 **SQLMoreResults** 會觸發批次中下一個語句的執行。 ODBC 支援下列批次類型：  
  
-   **明確批次***明確批次*是以分號分隔的兩個或多個 SQL 語句 (; ) 。 例如，下列 SQL 語句批次會開啟新的銷售訂單。 這需要將資料列插入 Orders 和 Lines 資料表中。 請注意，最後一個語句後面沒有任何分號。  
  
    ```  
    INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
       VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 1, 1234, 10);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 2, 987, 8);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 3, 566, 17);  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (2002, 4, 412, 500)  
    ```  
  
-   **程式** 如果套裝程式含一個以上的 SQL 語句，則會被視為 SQL 語句的批次。 例如，下列 SQL Server 特定的語句會建立一個程式，此程式會傳回包含客戶相關資訊的結果集，以及列出該客戶的所有開放式銷售訂單的結果集：  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**語句本身不是 SQL 語句的批次。 不過，它所建立的程式是 SQL 語句的批次。 沒有分號分隔兩個 **SELECT** 語句，因為 **create procedure** 語句是 SQL Server 特有的，而且 SQL Server 不需要分號來分隔 **CREATE procedure** 語句中的多個語句。  
  
-   **參數陣列** 參數陣列可以搭配參數化 SQL 語句使用，以做為執行大量作業的有效方式。 例如，您可以搭配下列 **INSERT** 語句使用參數陣列，以在執行單一 SQL 語句時，將多個資料列插入至各行資料表：  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果資料來源不支援參數陣列，驅動程式可以針對每一組參數執行一次 SQL 語句來模擬這些參數。 如需詳細資訊，請參閱本節稍後的 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md) 和 [參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)。  
  
 不同類型的批次無法以互通的方式混合。 也就是說，應用程式如何判斷執行包含程序呼叫之明確批次的結果、使用參數陣列的明確批次，以及使用參數陣列的程序呼叫是驅動程式特定的。  
  
 此章節包含下列主題。  
  
-   [會產生結果和不會產生結果的陳述式](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [執行批次](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [錯誤和批次](../../../odbc/reference/develop-app/errors-and-batches.md)
