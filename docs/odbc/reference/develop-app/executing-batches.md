---
title: 執行批次 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305729"
---
# <a name="executing-batches"></a>執行批次
在應用程式執行一批語句之前,應首先檢查它們是否受支援。 為此,應用程式使用SQL_BATCH_SUPPORT、SQL_PARAM_ARRAY_ROW_COUNTS和SQL_PARAM_ARRAY_SELECTS選項調用**SQLGetInfo。** 第一個選項返回顯式批處理和過程是否支援行計數生成語句和結果集生成語句,而後兩個選項返回有關參數化執行中行計數和結果集可用性的資訊。  
  
 語句的批次處理透過**SQLExecute**或**SQLExecDirect**執行。 例如,以下調用執行一批顯式語句以打開新的銷售訂單。  
  
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
  
 執行一批結果生成語句時,它將返回一個或多個行計數或結果集。 有關如何檢索這些結果的資訊,請參閱[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 如果一批語句包含參數標記,則這些語句按與任何其他語句中的參數順序一樣編號。 例如,以下批處理的語句的參數編號為 1 到 21;第一個**INSERT**語句中的編號為 1 到 5,最後**一個 INSERT**語句中的編號為 18 到 21。  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
INSERT INTO Lines (OrderID, Line, PartID, Quantity) VALUES (?, ?, ?, ?);  
```  
  
 有關參數的詳細資訊,請參閱本節後面的[語句參數](../../../odbc/reference/develop-app/statement-parameters.md)。
