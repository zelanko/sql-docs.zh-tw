---
title: 大量 SQL 語句 |微軟文件
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
ms.openlocfilehash: d68ea1c13655ca7c57ba076823f461a4b2e22055
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283508"
---
# <a name="batches-of-sql-statements"></a>SQL 陳述式的批次
一批 SQL 語句是兩個或多個 SQL 語句的組或單個 SQL 語句,其效果與兩個或多個 SQL 語句組的效果相同。 在某些實現中,在任何結果可用之前執行整個批處理語句。 這通常比單獨提交語句更有效,因為網路流量通常可以減少,數據源有時可以優化一批 SQL 語句的執行。 在其他實現中,調用**SQLMore結果**會觸發批處理中下一個語句的執行。 ODBC 支援以下類型的批次:  
  
-   **明確批次處理***顯式批處理*是兩個或多個 SQL 語句,由分號分隔(;)。 例如,以下批處理的 SQL 語句將打開新的銷售訂單。 這需要將行插入到"訂單"和"行"表中。 請注意,最後一個語句之後沒有分號。  
  
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
  
-   **程式**如果過程包含多個 SQL 語句,則它被視為一批 SQL 語句。 例如,以下特定於 SQL Server 的語句建立一個過程,傳回包含有關客戶的資訊的結果集和列出該客戶所有已結銷售訂單的結果集:  
  
    ```  
    CREATE PROCEDURE GetCustInfo (@CustomerID INT) AS  
       SELECT * FROM Customers WHERE CustID = @CustomerID  
       SELECT OrderID FROM Orders  
          WHERE CustID = @CustomerID AND Status = 'OPEN'  
    ```  
  
     **CREATE 程式**語句本身不是一批 SQL 語句。 但是,它創建的過程是一批 SQL 語句。 沒有分號分隔兩個**SELECT**語句,因為**CREATE 程式**語句特定於 SQL Server,並且 SQL Server 不需要分號來分隔**CREATE 程式**語句中的多個語句。  
  
-   **參數陣列**參數陣列可與參數化 SQL 語句一起使用,作為執行批量操作的有效方法。 例如,參數陣列可以與以下**INSERT**語句一起使用,以便將多行插入到 Lines 表中,同時僅執行單個 SQL 語句:  
  
    ```  
    INSERT INTO Lines (OrderID, Line, PartID, Quantity)  
       VALUES (?, ?, ?, ?)  
    ```  
  
     如果數據源不支援參數陣列,驅動程式可以通過為每個參數集執行 SQL 語句一次來類比它們。 有關詳細資訊,請參閱參數[值的](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)和陣列,請參閱本節後面的語句參數和陣列。  
  
 不同類型的批處理不能以可互操作的方式混合。 也就是說,應用程式如何確定執行包含過程調用的顯式批處理、使用參數陣列的顯式批處理以及使用參數陣列的過程調用的結果是特定於驅動程式的。  
  
 此章節包含下列主題。  
  
-   [會產生結果和不會產生結果的陳述式](../../../odbc/reference/develop-app/result-generating-and-result-free-statements.md)  
  
-   [執行批次](../../../odbc/reference/develop-app/executing-batches.md)  
  
-   [錯誤和批次](../../../odbc/reference/develop-app/errors-and-batches.md)
