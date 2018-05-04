---
title: 層級 1 介面一致性 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 522476043c86b26bc617f13a0704d07c7990e1cd
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="level-1-interface-conformance"></a>層級 1 介面一致性
層級 1 介面一致性層級包含核心介面一致性層級功能，以及其他功能，例如 OLTP 關聯式 DBMS 中通常可用的交易。 層級 1 介面標準驅動程式可讓應用程式執行下列作業，除了核心介面的一致性層級中的功能：  
  
|||  
|-|-|  
|101|指定資料庫的結構描述資料表和檢視 （使用兩段式命名）。 (如需詳細資訊，請參閱功能 201 中的三部分命名[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|102|叫用，則為 true 的 ODBC 函數，適用於 ODBC 函數的所有同步或所有非同步給定連接的非同步執行。|  
|103|使用可捲動資料指標，並藉此達到結果集，方法以外的順向的藉由呼叫存取**SQLFetchScroll**與*Sqlfetchscroll* SQL_FETCH_NEXT 以外的引數。 (要使用 SQL_FETCH_BOOKMARK *Sqlfetchscroll*處於功能 204[層級 2 介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)。)|  
|104|取得主索引鍵的資料表，藉由呼叫**SQLPrimaryKeys**。|  
|105|使用預存程序，透過程序呼叫的 ODBC 逸出序列，並藉由呼叫查詢預存程序，關於資料字典**SQLProcedureColumns**和**SQLProcedures**。 （程序會建立程式，並在資料來源上預存程序是在此文件的範圍之外）。|  
|106|連接到資料來源，以互動方式瀏覽可用的伺服器，藉由呼叫**SQLBrowseConnect**。|  
|107|執行某些資料庫作業，而不是 SQL 陳述式使用 ODBC 函數： **SQLSetPos** SQL_POSITION 與 SQL_REFRESH。|  
|108|取得存取權的批次和預存程序，藉由呼叫產生多個結果集內容**SQLMoreResults**。|  
|109|分隔跨越數個 ODBC 函數，則為 true 的不可部份完成性與能夠指定 SQL_ROLLBACK 中的交易**SQLEndTran**。|
