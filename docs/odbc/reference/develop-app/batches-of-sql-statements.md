---
title: SQL 陳述式的批次 |Microsoft 文件
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
- batches [ODBC]
- SQL statements [ODBC], batches
- batches [ODBC], about batches
ms.assetid: 766488cc-450c-434c-9c88-467f6c57e17c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e7f0119110e1bc57d106163d2e187bf599a0c596
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="batches-of-sql-statements"></a>批次的 SQL 陳述式
SQL 陳述式的批次是一組兩個或多個 SQL 陳述式或單一的 SQL 陳述式有兩個或多個 SQL 陳述式群組相同的效果。 在某些實作中，整個批次陳述式才可供任何結果。 這通常會較有效率比個別提交陳述式，因為通常可以降低網路流量，而且資料來源有時可以最佳化的 SQL 陳述式批次的執行。 在其他實作中呼叫**SQLMoreResults**觸發批次中的下一個陳述式執行。 ODBC 支援下列類型的批次：  
  
-   **明確的批次***明確的批次*是以分號 （;） 分隔的兩個或多個 SQL 陳述式。 例如，下列批次的 SQL 陳述式會開啟新的銷售訂單。 這需要的訂單 」 和 「 行的資料表中插入資料列。 請注意最後一個陳述式之後沒有任何分號。  
  
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
  
-   **程序**如果程序包含多個 SQL 陳述式，它會被視為批次的 SQL 陳述式。 例如，下列 SQL Server 特有的陳述式會建立傳回包含客戶和結果集，列出該客戶的所有開啟銷售訂單資訊的結果集的程序：  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE PROCEDURE**陳述式本身不是批次的 SQL 陳述式。 不過，它會建立程序是批次的 SQL 陳述式。 沒有以分號分隔的兩個**選取**陳述式因為**CREATE PROCEDURE**陳述式是特定 SQL server 和 SQL Server 不需要分號來分隔多個陳述式中**CREATE PROCEDURE**陳述式。  
  
-   **參數陣列**陣列的參數可以搭配參數化 SQL 陳述式做為有效的方式來執行大量作業。 陣列的參數，例如搭配下列**插入**執行只有單一 SQL 陳述式時，將多個資料列插入行資料表的陳述式：  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果資料來源不支援的參數陣列，此驅動程式可以模擬它們執行 SQL 陳述式，針對每個參數集執行一次。 如需詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)和[參數值陣列](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)稍後這一節。  
  
 無法混合不同類型的批次以互通的方式。 也就是應用程式如何判斷執行明確的批次包含程序的結果呼叫明確的批次所使用的參數，陣列，並使用參數陣列的程序呼叫是特定驅動程式。  
  
 此章節包含下列主題。  
  
-   [會產生結果和不會產生結果的陳述式](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [執行批次](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [錯誤和批次](../../../odbc/reference/develop-app/errors-and-batches.md)
