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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0ce0c043fcfad41a624ad129a757a047d2c87fb6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305729"
---
# <a name="executing-batches"></a>執行批次
在應用程式執行語句批次之前，應該先檢查它們是否受到支援。 為此，應用程式會使用 SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項來呼叫**SQLGetInfo** 。 第一個選項會傳回明確批次和程式中是否支援資料列計數產生和結果集產生的語句，而後面兩個選項則會傳回參數化執行中資料列計數和結果集可用性的相關資訊。  
  
 語句的批次是透過**SQLExecute**或**SQLExecDirect**來執行。 例如，下列呼叫會執行明確的語句批次，以開啟新的銷售訂單。  
  
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
  
 執行產生結果語句的批次時，它會傳回一或多個資料列計數或結果集。 如需有關如何取得這些資訊，請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果語句批次包含參數標記，則這些會以遞增的參數順序編號，如同在任何其他語句中一樣。 例如，下列批次語句的參數編號為1到 21;第一個**insert**語句中的是編號1到5，而最後一個**insert**語句中的則編號為18到21。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 如需參數的詳細資訊，請參閱本節稍後的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
