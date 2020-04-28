---
title: 層級2介面一致性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306159"
---
# <a name="level-2-interface-conformance"></a>層級 2 介面一致性
層級2介面一致性層級包含層級1介面一致性層級功能，以及下列功能：  
  
|||  
|-|-|  
|201|使用資料庫資料表和 views 的三部分名稱。 （如需詳細資訊，請參閱[層級1介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的兩部分命名支援功能101）。|  
|202|藉由呼叫**SQLDescribeParam**來描述動態參數。|  
|203|不僅會使用輸入參數，還可以輸出和輸入/輸出參數，以及預存程式的結果值。|  
|204|藉由在資料行編號0上呼叫**SQLDescribeCol**和**SQLColAttribute** ，來使用書簽，包括抓取書簽。根據書簽來提取，方法是呼叫**SQLFetchScroll**並將*FetchOrientation*引數設為 SQL_FETCH_BOOKMARK;並透過書簽作業來更新、刪除和提取，方法是呼叫**SQLBulkOperations**並將*Operation*引數設定為 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK。|  
|205|藉由呼叫**SQLColumnPrivileges**、 **SQLForeignKeys**和**SQLTablePrivileges**，來抓取有關資料字典的 advanced 資訊。|  
|206|使用 ODBC 函式（而非 SQL 語句）來執行額外的資料庫作業，方法是以 SQL_ADD 呼叫**SQLBulkOperations**或使用 SQL_DELETE 或 SQL_UPDATE 的**SQLSetPos** 。 （支援呼叫**SQLSetPos** ，並將*LockType*引數設為 SQL_LOCK_EXCLUSIVE 或 SQL_LOCK_UNLOCK 不是一致性層級的一部分，但是選擇性功能）。|  
|207|針對指定的個別語句啟用 ODBC 函數的非同步執行。|  
|208|藉由呼叫**SQLSpecialColumns**，取得資料表的 SQL_ROWVER 資料列識別資料行。 （如需詳細資訊，請參閱支援**SQLSpecialColumns** ，並將*IdentifierType*引數設定為 SQL_BEST_ROWID 做為[核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)中的功能20）。|  
|209|將 SQL_ATTR_CONCURRENCY 語句屬性設定為至少一個 SQL_CONCUR_READ_ONLY 以外的值。|  
|210|能夠準時登入要求和 SQL 查詢（SQL_ATTR_LOGIN_TIMEOUT 和 SQL_ATTR_QUERY_TIMEOUT）。|  
|211|變更預設隔離等級的能力;能夠執行具有「可序列化」層級隔離的交易。|
