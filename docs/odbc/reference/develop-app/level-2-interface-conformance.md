---
title: 層級 2 介面一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50e74eaed2d651158834a241563d10b3b2e90d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915577"
---
# <a name="level-2-interface-conformance"></a>層級 2 介面一致性
層級 2 介面一致性層級包含層級 1 介面一致性層級功能以及下列功能：  
  
|||  
|-|-|  
|201|使用資料庫資料表和檢視表的三部分名稱。 (如需詳細資訊，請參閱兩段式命名支援中的功能 101[層級 1 介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)。)|  
|202|描述動態參數，藉由呼叫**SQLDescribeParam**。|  
|203|使用不只輸入的參數，但也輸出和輸入/輸出參數和預存程序的結果值。|  
|204|使用書籤，包括擷取書籤，藉由呼叫**SQLDescribeCol**並**SQLColAttribute**資料行上數字 0; 擷取書籤，以藉由呼叫**SQLFetchScroll**具有*Sqlfetchscroll*引數設定為要使用 SQL_FETCH_BOOKMARK; 和更新、 刪除和書籤的作業，藉由呼叫擷取**SQLBulkOperations** 與*作業*引數設定為 SQL_UPDATE_BY_BOOKMARK、 SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK。|  
|205|藉由呼叫的進階資訊的資料字典中，擷取**SQLColumnPrivileges**， **SQLForeignKeys**，並**SQLTablePrivileges**。|  
|206|使用 ODBC 函數而不是 SQL 陳述式來執行其他資料庫作業，藉由呼叫**SQLBulkOperations**使用 SQL_ADD，或是**SQLSetPos** SQL_DELETE 或 SQL_UPDATE。 (支援呼叫來**SQLSetPos**具有*LockType*引數設定為 SQL_LOCK_EXCLUSIVE 或 SQL_LOCK_UNLOCK 不一致性層級的一部分，而是一項選擇性功能。)|  
|207|啟用非同步執行指定的個別陳述式的 ODBC 函數。|  
|208|取得 SQL_ROWVER 資料列識別資料行的資料表，藉由呼叫**SQLSpecialColumns**。 (如需詳細資訊，請參閱的支援**SQLSpecialColumns**具有*IdentifierType*引數設為功能中的 20 SQL_BEST_ROWID[核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|SQL_ATTR_CONCURRENCY 陳述式將屬性設定為 SQL_CONCUR_READ_ONLY 以外的至少一個值。|  
|210|逾時的登入要求和 SQL 查詢 （SQL_ATTR_LOGIN_TIMEOUT 和 SQL_ATTR_QUERY_TIMEOUT） 能力。|  
|211|若要變更預設的隔離等級; 能力能夠執行使用 「 序列化 」 的隔離等級的交易。|
