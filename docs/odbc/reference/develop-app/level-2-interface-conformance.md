---
title: "層級 2 介面一致性 |Microsoft 文件"
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
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c272637e15d95a09862170ec871274adb624c271
ms.contentlocale: zh-tw
ms.lasthandoff: 09/09/2017

---
# <a name="level-2-interface-conformance"></a>層級 2 介面一致性
層級 2 介面一致性層級包含層級 1 介面一致性層級功能以及下列功能：  
  
|||  
|-|-|  
|201|使用資料庫資料表和檢視表的三部分名稱。 (如需詳細資訊，請參閱兩段式命名支援中的功能 101[層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)。)|  
|202|描述動態參數，藉由呼叫**SQLDescribeParam**。|  
|203|使用不只輸入的參數，但也輸出和輸入/輸出參數和結果值的預存程序。|  
|204|使用書籤，包括擷取書籤，藉由呼叫**SQLDescribeCol**和**SQLColAttribute**資料行上數字 0，則為擷取書籤基礎，藉由呼叫**SQLFetchScroll**與*Sqlfetchscroll*引數設定為要使用 SQL_FETCH_BOOKMARK; 和更新、 刪除及擷取書籤的作業，藉由呼叫**SQLBulkOperations**與*作業*引數設定為 SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK。|  
|205|藉由呼叫的進階資訊的資料字典中，擷取**SQLColumnPrivileges**， **SQLForeignKeys**，和**SQLTablePrivileges**。|  
|206|使用 ODBC 函數而不是 SQL 陳述式來執行其他資料庫作業，藉由呼叫**SQLBulkOperations**與 SQL_ADD，或**SQLSetPos** SQL_DELETE 或 SQL_UPDATE。 (支援的呼叫**SQLSetPos**與*LockType*引數設定為 SQL_LOCK_EXCLUSIVE 或 SQL_LOCK_UNLOCK 不一致性層級的一部分，而是一項選擇性功能。)|  
|207|啟用非同步執行指定的個別陳述式的 ODBC 函數。|  
|208|取得 SQL_ROWVER 資料列識別資料行的資料表，藉由呼叫**SQLSpecialColumns**。 (如需詳細資訊，請參閱的支援**SQLSpecialColumns**與*IdentifierType*引數設定為 SQL_BEST_ROWID 如功能中的 20[核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|設定陳述式屬性 sql_attr_concurrency 設定為 SQL_CONCUR_READ_ONLY 以外的至少一個值。|  
|210|逾時時間登入要求和 （SQL_ATTR_LOGIN_TIMEOUT 和 sql_attr_query_timeout 時） 的 SQL 查詢的能力。|  
|211|可以變更預設的隔離等級。執行的能力擁有 「 序列化 」 的隔離等級的交易。|

