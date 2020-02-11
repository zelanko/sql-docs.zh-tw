---
title: 判斷受影響的資料列數目 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6a1bebf7d5cfb85e49fb0e382dacc4f4464054e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68039977"
---
# <a name="determining-the-number-of-affected-rows"></a>判斷受影響的資料列數目
在應用程式更新、刪除或插入資料列之後，它可以呼叫**SQLRowCount**來判斷受影響的資料列數目。 **SQLRowCount**會傳回這個值，不論是藉由執行**update**、 **delete**或**INSERT**語句、執行定位的 UPDATE 或 delete 語句，或是藉由呼叫**SQLSetPos**來更新、刪除或插入資料列。  
  
 如果執行 SQL 語句的批次，受影響資料列的計數可能會是批次中所有語句的總計數，或批次中每個語句的個別計數。 如需詳細資訊，請參閱[SQL 語句的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 受影響的資料列數目也會在與語句控制碼相關聯之診斷區域的 [SQL_DIAG_ROW_COUNT 診斷標頭] 欄位中傳回。 不過，在相同語句控制碼上的每個函式呼叫之後，會重設此欄位中的資料，而**SQLRowCount**所傳回的值會維持不變，直到呼叫**SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPrepare**或**SQLSetPos**為止。
