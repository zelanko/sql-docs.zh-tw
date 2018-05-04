---
title: 執行批次 |Microsoft 文件
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
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], executing
- SQL statements [ODBC], batches
ms.assetid: f082c717-4f82-4820-a2fa-ba607d8fd872
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f888b1719653ed48e3ecf28fc356506aa06a31e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="executing-batches"></a>執行批次
應用程式執行的陳述式批次之前，它應該先檢查是否支援這些功能。 若要這樣做，應用程式會呼叫**SQLGetInfo** SQL_BATCH_SUPPORT、 SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項。 第一個選項就會傳回資料列計數 – 產生以及支援產生集 – 陳述式中明確的批次和程序，後者的兩個選項中設定的可用性相關的資料列計數和結果傳回的資訊時的結果是否化執行。  
  
 透過執行的陳述式的批次**SQLExecute**或**SQLExecDirect**。 例如，下列呼叫會執行明確的批次的陳述式來開啟新的銷售訂單。  
  
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
  
 當批次結果產生的陳述式執行，它會傳回一個或多個資料列計數或結果設定。 如需如何擷取這些資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果批次的陳述式包含參數標記，這些會以遞增中任何其他陳述式的參數順序編號。 例如，下列陳述式的批次的參數編號是從 1 到 21;在第一個**插入**陳述式所編號 1 到 5，而最後一個**插入**陳述式會透過 21 編號的 18。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 如需參數的詳細資訊，請參閱[陳述式參數](../../../odbc/reference/develop-app/statement-parameters.md)稍後這一節。
