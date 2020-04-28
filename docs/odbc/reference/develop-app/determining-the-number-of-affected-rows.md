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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 156a5fe41d2c9b57a33bbc2bdb4540d1f5b00340
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305889"
---
# <a name="determining-the-number-of-affected-rows"></a>判斷受影響的資料列數目
在應用程式更新、刪除或插入資料列之後，它可以呼叫**SQLRowCount**來判斷受影響的資料列數目。 **SQLRowCount**會傳回這個值，不論是藉由執行**update**、 **delete**或**INSERT**語句、執行定位的 UPDATE 或 delete 語句，或是藉由呼叫**SQLSetPos**來更新、刪除或插入資料列。  
  
 如果執行 SQL 語句的批次，受影響資料列的計數可能會是批次中所有語句的總計數，或批次中每個語句的個別計數。 如需詳細資訊，請參閱[SQL 語句的批次](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 受影響的資料列數目也會在與語句控制碼相關聯之診斷區域的 [SQL_DIAG_ROW_COUNT 診斷標頭] 欄位中傳回。 不過，在相同語句控制碼上的每個函式呼叫之後，會重設此欄位中的資料，而**SQLRowCount**所傳回的值會維持不變，直到呼叫**SQLBulkOperations**、 **SQLExecute**、 **SQLExecDirect**、 **SQLPrepare**或**SQLSetPos**為止。
