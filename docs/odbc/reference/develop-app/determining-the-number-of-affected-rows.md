---
title: 確定受影響的行數 |微軟文件
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305889"
---
# <a name="determining-the-number-of-affected-rows"></a>判斷受影響的資料列數目
在應用程式更新、刪除或插入行後,它可以調用**SQLRowCount**以確定受影響的行數。 **SQLRowCount**執行定位的更新或移除敘述,或呼叫**SQLSetPos**來傳回此值,無論列是否透過執行**更新**、刪除或插入敘述來更新、**刪除**或**插入**。  
  
 如果執行一批 SQL 語句,則受影響行的計數可能是批處理中所有語句或批處理中每個語句的單個計數的總計數。 有關詳細資訊,請參閱[SQL 語句的批次處理](../../../odbc/reference/develop-app/batches-of-sql-statements.md)與[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 在與語句句柄關聯的診斷區域中,SQL_DIAG_ROW_COUNT診斷標頭欄位中也會返回受影響的行數。 但是,此欄位中的數據在相同的語句句柄上的每個函數調用後重置,而**SQLRowCount**返回的值保持不變,直到呼叫**SQLBulk 操作**、SQLExecute、SQLExecDirect、SQLPrepare 或**SQLPrepare** **SQLExecute** **SQLExecDirect** **SQLSetPos**。
