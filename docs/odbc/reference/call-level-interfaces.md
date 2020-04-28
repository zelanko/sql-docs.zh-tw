---
title: 呼叫層級介面 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], CLI
- CLI [ODBC], using CLI
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], CLI
- call-level interface [ODBC], using call-level interface
ms.assetid: 42257bb6-0bf1-4533-a4ef-4a6dd2aecb18
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4288a278f745d533c92d3d45892753ef1a74c2b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306539"
---
# <a name="call-level-interfaces"></a>呼叫層級介面
將 SQL 語句傳送至 DBMS 的最後一項技術是透過呼叫層級介面（CLI）。 呼叫層級介面提供可由應用程式呼叫的 DBMS 函數程式庫。 因此，不會嘗試使用其他程式設計語言來混合 SQL，呼叫層級介面類別似于大部分程式設計師慣用使用的常式程式庫，例如字串、i/o 或 C 中的數學程式庫。請注意，支援內嵌 SQL 的 Dbms 已經有呼叫層級介面，這是由先行編譯器所產生的呼叫。 不過，這些呼叫並未記載，恕不另行通知也可能變更。  
  
 呼叫層級介面通常用於用戶端/伺服器架構，其中應用程式（用戶端）位於一部電腦上，而 DBMS （伺服器）位於不同的電腦上。 應用程式會在本機系統上呼叫 CLI 函式，而這些呼叫會透過網路傳送至 DBMS 進行處理。  
  
 呼叫層級介面類別似于動態 SQL，其中 SQL 語句會在執行時間傳遞至 DBMS 以進行處理，但它與內嵌 SQL 不同，因為沒有內嵌的 SQL 語句，而且不需要任何先行編譯器。  
  
 使用呼叫層級介面時，通常會牽涉到下列步驟：  
  
1.  應用程式會呼叫 CLI 函式來連接到 DBMS。  
  
2.  應用程式會建立 SQL 語句，並將它放在緩衝區中。 然後，它會呼叫一或多個 CLI 函式，將語句傳送至 DBMS 以進行準備和執行。  
  
3.  如果語句是 SELECT 語句，則應用程式會呼叫 CLI 函式，以在應用程式緩衝區中傳回結果。 一般而言，此函式會一次傳回一個資料列或一個資料行。  
  
4.  應用程式會呼叫 CLI 函式來中斷與 DBMS 的連線。
