---
title: 執行批次 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 84d3cf65284d767d437987c8ff2b21793466106e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901263"
---
# <a name="executing-batches"></a>執行批次
在應用程式執行的陳述式批次之前，它應該先檢查是否支援這些。 若要這樣做，應用程式會呼叫**SQLGetInfo** SQL_BATCH_SUPPORT、 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項。 第一個選項就會傳回是否資料列計數產生和結果集產生的陳述式中明確的批次和程序，並在後面的兩個選項中設定的可用性相關的資料列計數和結果的傳回資訊時支援參數化執行。  
  
 透過執行的陳述式的批次**SQLExecute**或是**SQLExecDirect**。 例如，下列呼叫來執行明確的批次的陳述式來開啟新的銷售訂單。  
  
```  
SQLCHAR *BatchStmt =  
   "INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)"  
      "VALUES (2002, 1001, {fn CURDATE()}, 'Garcia', 'OPEN');"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 1, 1234, 10);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 2, 987, 8);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 3, 566, 17);"  
   "INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (2002, 4, 412, 500)";  
  
SQLExecDirect(hstmt, BatchStmt, SQL_NTS);  
```  
  
 當結果產生的批次執行陳述式時，它會傳回一個或多個資料列計數或結果集。 如需如何擷取這些資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果批次陳述式包含參數標記，這些會以遞增以其在任何其他陳述式的參數順序進行編號。 例如，下列批次陳述式有參數編號是從 1 到 21;在第一個**插入**陳述式是已編號的 1 到 5，而最後一個**插入**陳述式是已編號的 18 到 21。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 如需有關參數的詳細資訊，請參閱 <<c0> [ 陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。
