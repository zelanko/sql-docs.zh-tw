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
manager: craigg
ms.openlocfilehash: 99e3676c3b73b177f5e6fc3acef0d93d55cce898
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47626206"
---
# <a name="determining-the-number-of-affected-rows"></a>判斷受影響的資料列數目
應用程式更新、 刪除或插入資料列之後，它可以呼叫**SQLRowCount**來判斷多少資料列受到影響。 **SQLRowCount**會傳回此值，不論資料列已更新、 刪除或執行插入**更新**，**刪除**，或**插入**陳述式，藉由執行定位更新或刪除陳述式，或藉由呼叫**SQLSetPos**。  
  
 如果執行 SQL 陳述式的批次時，受影響的資料列計數可能總數批次中的所有陳述式或批次中的每個陳述式的個別計數。 如需詳細資訊，請參閱 <<c0> [ 批次的 SQL 陳述式](../../../odbc/reference/develop-app/batches-of-sql-statements.md)並[多個結果](../../../odbc/reference/develop-app/multiple-results.md)。  
  
 診斷與陳述式控制代碼相關聯的區域中 SQL_DIAG_ROW_COUNT 診斷的標頭欄位，也會傳回受影響的資料列數目。 不過，此欄位中的資料會重設之後相同的陳述式控制代碼上的每個函式呼叫所傳回的值而**SQLRowCount**維持不變，直到呼叫**SQLBulkOperations**， **SQLExecute**， **SQLExecDirect**， **SQLPrepare**，或**SQLSetPos**。
