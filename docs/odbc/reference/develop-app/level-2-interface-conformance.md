---
description: 層級 2 介面一致性
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
ms.openlocfilehash: 31b7148b05d3870a7f23a51167fffeb1860c26d8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476560"
---
# <a name="level-2-interface-conformance"></a>層級 2 介面一致性
層級2介面一致性層級包含層級1介面一致性層級功能，以及下列功能：  
  
|功能編號|描述|  
|-|-|  
|201|使用三部分的資料庫資料表和視圖名稱。  (需詳細資訊，請參閱 [層級1介面一致性](../../../odbc/reference/develop-app/level-1-interface-conformance.md)中的兩部分命名支援功能101。 ) |  
|202|藉由呼叫 **SQLDescribeParam**來描述動態參數。|  
|203|不僅使用輸入參數，還可以輸出和輸入/輸出參數，以及預存程式的結果值。|  
|204|在資料行編號0上呼叫**SQLDescribeCol**和**SQLColAttribute** ，以使用書簽，包括抓取書簽。根據書簽提取，方法是呼叫**SQLFetchScroll** ，將*FetchOrientation*引數設定為 SQL_FETCH_BOOKMARK;藉*由將作業引數*設定為 SQL_UPDATE_BY_BOOKMARK、SQL_DELETE_BY_BOOKMARK 或 SQL_FETCH_BY_BOOKMARK **，以書簽**作業來更新、刪除和提取。|  
|205|藉由呼叫 **SQLColumnPrivileges**、 **SQLForeignKeys**和 **SQLTablePrivileges**，來取得有關資料字典的 advanced 資訊。|  
|206|使用 ODBC 函數（而不是 SQL 語句）來執行額外的資料庫作業，方法是呼叫 **SQLBulkOperations** 搭配 SQL_ADD，或使用 SQL_DELETE 或 SQL_UPDATE 的 **SQLSetPos** 。  (支援呼叫 **SQLSetPos** ，並將 *LockType* 引數設定為 SQL_LOCK_EXCLUSIVE 或 SQL_LOCK_UNLOCK 不是一致性層級的一部分，但是是選擇性功能。 ) |  
|207|針對指定的個別語句啟用 ODBC 函數的非同步執行。|  
|208|藉由呼叫 **SQLSpecialColumns**，取得資料表的 SQL_ROWVER 資料列識別資料行。  (需詳細資訊，請參閱支援 **SQLSpecialColumns** ，並將 *IdentifierType* 引數設定為 SQL_BEST_ROWID 的 [核心介面一致性](../../../odbc/reference/develop-app/core-interface-conformance.md)中的功能20。 ) |  
|209|將 SQL_ATTR_CONCURRENCY 語句屬性至少設定為 SQL_CONCUR_READ_ONLY 以外的一個值。|  
|210|將登入要求和 SQL 查詢的時間 (SQL_ATTR_LOGIN_TIMEOUT 和 SQL_ATTR_QUERY_TIMEOUT) 的能力。|  
|211|變更預設隔離等級的能力;使用「可序列化」隔離等級執行交易的能力。|
