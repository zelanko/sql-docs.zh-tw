---
title: "傳回 SQL_NO_DATA |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf27a50915d9af31eaa280525736cacf7faf06db
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="returning-sqlnodata"></a>傳回 sql_no_data 為止
當 ODBC 2。*x*應用程式使用 ODBC 3*.x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，並搜尋的更新或刪除陳述式執行，但未影響任何資料列在資料來源，而 ODBC 3*.x*驅動程式應該會傳回 SQL_SUCCESS。 當 ODBC 3*.x*應用程式使用 ODBC 3*.x*驅動程式呼叫**SQLExecDirect**， **SQLExecute**，或**SQLParamData**具有相同的結果，而 ODBC 3*.x*驅動程式應該會傳回 sql_no_data 為止。  
  
 如果搜尋的 update 或 delete 陳述式中的陳述式批次不會影響資料來源的任何資料列**SQLMoreResults**都會傳回 SQL_SUCCESS。 它不能傳回 sql_no_data 之後，因為這可能表示有更多結果，不會有是從搜尋的更新/刪除受影響的任何資料列的結果。
