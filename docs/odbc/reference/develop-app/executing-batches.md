---
description: 執行批次
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
ms.openlocfilehash: b3bb923f95dfcfb731d472aad8ead7ff35053171
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424640"
---
# <a name="executing-batches"></a>執行批次
在應用程式執行批次語句之前，它應該先檢查是否支援它們。 若要這樣做，應用程式會使用 SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS 和 SQL_PARAM_ARRAY_SELECTS 選項來呼叫 **SQLGetInfo** 。 第一個選項會傳回在明確批次和程式中是否支援資料列計數產生和結果集產生的語句，而後者的兩個選項則會傳回在參數化執行時，資料列計數和結果集可用性的相關資訊。  
  
 語句的批次會透過 **SQLExecute** 或 **SQLExecDirect**來執行。 例如，下列呼叫會執行明確的語句批次以開啟新的銷售訂單。  
  
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
  
 當執行結果批次產生的語句時，它會傳回一或多個資料列計數或結果集。 如需如何取得這些結果的詳細資訊，請參閱 [多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果語句的批次包含參數標記，則這些標記會以遞增的參數順序來排序，因為它們在其他任何語句中。 例如，下列語句批次的參數編號為1到 21;第一個 Insert 語句中的第一個 **insert** 語句的編號為1到5，而最後一個 **insert** 語句中的是編號18到21。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 如需參數的詳細資訊，請參閱本節稍後的 [語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
