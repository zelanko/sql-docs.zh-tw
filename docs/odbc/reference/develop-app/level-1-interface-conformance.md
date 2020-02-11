---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 05cf381ccbb8c0747db88259acfb4ba218d3e0ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135007"
---
# <a name="level-1-interface-conformance"></a>層級 1 介面一致性
層級1介面一致性層級包括核心介面一致性層級功能，以及通常在 OLTP 關聯式 DBMS 中提供的其他功能，例如交易。 層級1符合介面的驅動程式可讓應用程式執行下列動作，以及核心介面一致性層級中的功能：  
  
|||  
|-|-|  
|101|指定資料庫資料表和視圖的架構（使用兩部分命名）。 （如需詳細資訊，請參閱[層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)中的三部分命名功能201）。|  
|102|叫用 ODBC 函式的真正非同步執行，其中適用的 ODBC 函數在指定的連接上全都是同步或全部非同步。|  
|103|使用可滾動的資料指標，藉由使用 SQL_FETCH_NEXT 以外的*FetchOrientation*引數來呼叫**SQLFetchScroll** ，藉此在順向以外的方法中取得結果集的存取權。 （SQL_FETCH_BOOKMARK *FetchOrientation*位於[層級2介面一致性](../../../odbc/reference/develop-app/level-2-interface-conformance.md)的功能204中）。|  
|104|藉由呼叫**SQLPrimaryKeys**，取得資料表的主鍵。|  
|105|藉由呼叫**SQLProcedureColumns**和**SQLProcedures**，使用預存程式，透過程式調用的 ODBC 轉義順序，並查詢關於預存程式的資料字典。 （建立並儲存在資料來源上的程式不在此檔的範圍內）。|  
|106|藉由呼叫**SQLBrowseConnect**，以互動方式流覽可用的伺服器，以連接到資料來源。|  
|107|使用 ODBC 函式而非 SQL 語句來執行特定資料庫作業：使用 SQL_POSITION 和 SQL_REFRESH 的**SQLSetPos** 。|  
|108|藉由呼叫**SQLMoreResults**，取得批次和預存程式所產生之多個結果集的內容存取權。|  
|109|以真正的不可部分完成性和在**SQLEndTran**中指定 SQL_ROLLBACK 的能力，將跨越數個 ODBC 函數的交易分隔。|
