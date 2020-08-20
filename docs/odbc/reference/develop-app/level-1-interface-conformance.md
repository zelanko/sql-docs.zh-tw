---
description: 層級 1 介面一致性
title: 層級1介面一致性 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e92b68c9e8864e79c495c9405f905fa5a4f37acf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476570"
---
# <a name="level-1-interface-conformance"></a>層級 1 介面一致性
層級1介面一致性層級包括核心介面一致性層級功能，以及通常可在 OLTP 關聯式 DBMS 中使用的其他功能（例如交易）。 符合層級1的介面相容驅動程式可讓應用程式執行下列作業，除了核心介面一致性層級中的功能：  
  
|功能編號|描述|  
|-|-|  
|101|使用兩部分的命名) ，指定資料庫資料表和 views (的架構。  (需詳細資訊，請參閱第 [2 層介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的三部分命名功能201。 ) |  
|102|叫用真正非同步執行的 ODBC 函式，其中適用的 ODBC 函數在指定的連接上都是同步或全部非同步。|  
|103|使用可滾動的資料指標，藉由使用 SQL_FETCH_NEXT 以外的*FetchOrientation*引數來呼叫**SQLFetchScroll** ，以在順向以外的方法中存取結果集。  (SQL_FETCH_BOOKMARK *FetchOrientation* 在 [層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)的功能204中。 ) |  
|104|藉由呼叫 **SQLPrimaryKeys**來取得資料表的主要索引鍵。|  
|105|使用預存程式，透過程序呼叫的 ODBC escape 序列，然後透過呼叫 **SQLProcedureColumns** 和 **SQLProcedures**，查詢有關預存程式的資料字典。  (在資料來源上建立和儲存程式的程式不在本檔的討論範圍內。 ) |  
|106|藉由呼叫 **SQLBrowseConnect**，以互動方式流覽可用的伺服器，以連接到資料來源。|  
|107|使用 ODBC 函數而非 SQL 語句來執行某些資料庫作業：使用 SQL_POSITION 和 SQL_REFRESH **SQLSetPos** 。|  
|108|藉由呼叫 **SQLMoreResults**，取得批次和預存程式所產生之多個結果集的內容存取權。|  
|109|分隔多個 ODBC 函數的交易，並提供真正的不可部分完成性，以及在 **SQLEndTran**中指定 SQL_ROLLBACK 的能力。|
