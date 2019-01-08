---
title: 錯誤和批次 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 97179574407dca56026f9d5216e4978069cffc1e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527334"
---
# <a name="errors-and-batches"></a>錯誤和批次
當錯誤發生時執行的 SQL 陳述式的批次時，其中一個下列四個結果是可能的。 （每個可能的結果是資料來源特有的而且甚至可能會取決於包含在批次的陳述式）。  
  
-   批次中的任何陳述式會不執行。  
  
-   執行批次中的任何陳述式，並回復交易。  
  
-   所有之前的錯誤陳述式的陳述式會執行。  
  
-   所有的陳述式以外的錯誤陳述式會執行。  
  
 在前兩個情況中， **SQLExecute**並**SQLExecDirect**傳回 SQL_ERROR。 在後者的兩個情況下，它們可能會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，視實作而定。 在所有情況下，更進一步的錯誤資訊可以擷取與**SQLGetDiagField**， **SQLGetDiagRec**，或**SQLError**。 不過的本質和深度的這項資訊是資料來源特有。 此外，這項資訊不太可能完全找出錯誤的陳述式。
