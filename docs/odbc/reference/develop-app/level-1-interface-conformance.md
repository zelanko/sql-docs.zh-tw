---
title: 層級 1 介面一致性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d75c374a7d9d57483dd56e34b51fcb6d89e1b52
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213481"
---
# <a name="level-1-interface-conformance"></a>層級 1 介面一致性
層級 1 介面一致性層級包含核心介面一致性層級功能，加上額外的功能，例如，通常可在 OLTP 關聯式 DBMS 中的交易。 層級 1 介面符合標準驅動程式可讓應用程式執行下列作業，除了核心介面一致性層級中的功能：  
  
|||  
|-|-|  
|101|指定資料庫的結構描述資料表和檢視 （使用兩段式命名）。 (如需詳細資訊，請參閱功能 201 中的三部分命名[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|102|叫用，則為 true 的非同步執行的 ODBC 函式，其中適用的 ODBC 函式是全部同步或全部非同步上指定的連接。|  
|103|使用可捲動資料指標，並藉此達到結果集，方法而非順向的藉由呼叫的存取**SQLFetchScroll**具有*Sqlfetchscroll* SQL_FETCH_NEXT 以外的引數。 (要使用 SQL_FETCH_BOOKMARK *Sqlfetchscroll*處於功能 204[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|104|取得主索引鍵的資料表，藉由呼叫**SQLPrimaryKeys**。|  
|105|使用預存程序，透過程序呼叫的 ODBC 逸出序列，並查詢藉由呼叫的預存程序，相關的資料字典**SQLProcedureColumns**並**SQLProcedures**。 （程序會建立程式，並在資料來源上預存程序已超出本文的範圍）。|  
|106|連接到資料來源，以互動方式瀏覽可用的伺服器，藉由呼叫**SQLBrowseConnect**。|  
|107|若要執行某些資料庫作業，而不是 SQL 陳述式使用 ODBC 函數：**SQLSetPos** SQL_POSITION 與 SQL_REFRESH。|  
|108|存取多個批次和預存程序，藉由呼叫產生的結果集的內容**SQLMoreResults**。|  
|109|分隔交易橫跨數個 ODBC 函數，則為 true 的不可部分完成性與能夠指定在 SQL_ROLLBACK **SQLEndTran**。|
