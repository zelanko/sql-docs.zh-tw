---
title: 錯誤和批次 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- batches [ODBC], errors
- sql_success_with_info [ODBC]
- sql_success [ODBC]
- SQL statements [ODBC], batches
- sql_error [ODBC]
ms.assetid: 6debd41d-9f4c-4f4c-a44b-2993da5306f0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d00672166039421fb8518c52a58d19d73d02d477
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="errors-and-batches"></a>錯誤和批次
發生錯誤時執行的 SQL 陳述式批次時，下列四種結果可能會。 （每個可能的結果是資料來源專用伺服器，甚至可能會相依於批次中包含的陳述式。）  
  
-   批次中的任何陳述式會不執行。  
  
-   執行批次中的任何陳述式，並回復交易。  
  
-   所有的錯誤陳述式之前的陳述式會執行。  
  
-   所有除了 error 陳述式的陳述式會執行。  
  
 在前兩個情況下， **SQLExecute**和**SQLExecDirect**傳回 SQL_ERROR。 在後者的兩個情況下，它們可能會傳回 SQL_SUCCESS_WITH_INFO 或 SQL_SUCCESS，視實作而定。 在所有情況下，進一步的錯誤資訊可以擷取與**SQLGetDiagField**， **SQLGetDiagRec**，或**SQLError**。 不過的本質和深度的這項資訊是資料來源專用。 此外，這項資訊不太可能完全識別錯誤中的陳述式。
