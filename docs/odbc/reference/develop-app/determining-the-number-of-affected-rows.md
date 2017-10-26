---
title: "判斷受影響的資料列數目 |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], number of rows affected
- number of rows affected by update [ODBC]
- data updates [ODBC], number of rows affected
ms.assetid: 1e56297d-a786-415e-b66d-b42d1b2a8d45
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b2f030be011864be17c8539d8ab94f6980f0f791
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="determining-the-number-of-affected-rows"></a>判斷受影響的資料列數目
應用程式更新、 刪除或插入資料列之後，它可以呼叫**SQLRowCount**來判斷多少資料列受到影響。 **SQLRowCount**會傳回此值，不論資料列已更新、 刪除或插入執行**更新**，**刪除**，或**插入**陳述式，藉由執行定位的更新或刪除陳述式，或藉由呼叫**SQLSetPos**。  
  
 如果執行 SQL 陳述式的批次時，受影響的資料列計數可能總數的批次中的所有陳述式或批次中的每個陳述式的個別計數。 如需詳細資訊，請參閱[批次的 SQL 陳述式](../../../odbc/reference/develop-app/batches-of-sql-statements.md)和[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 SQL_DIAG_ROW_COUNT 診斷標頭欄位中的診斷與陳述式控制代碼相關聯的區域，也會傳回受影響的資料列數目。 不過，此欄位中的資料會重設之後相同的陳述式控制代碼上的每個函式呼叫所傳回的值而**SQLRowCount**維持不變，直到呼叫**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPrepare**，或**SQLSetPos**。

