---
description: 呼叫層級介面
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
ms.openlocfilehash: ad1e89f945dbb739c4c20103fc2330cbf4e562b5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448956"
---
# <a name="call-level-interfaces"></a>呼叫層級介面
將 SQL 語句傳送至 DBMS 的最後一項技巧，就是透過呼叫層級介面 (CLI) 。 呼叫層級介面會提供可由應用程式呼叫的 DBMS 函式程式庫。 因此，與其他程式設計語言不同的是，呼叫層級介面類別似于大部分程式設計人員習慣使用的常式程式庫，例如 C 中的字串、i/o 或數學程式庫。請注意，支援內嵌 SQL 的 Dbms 已經有呼叫層級介面，也就是先行編譯器所產生的呼叫。 不過，這些呼叫未記載，如有變更恕不另行通知。  
  
 呼叫層級介面通常用於用戶端/伺服器架構，在此架構中，用戶端) 的應用程式 (位於一部電腦上，而伺服器)  (在不同的電腦上。 應用程式會在本機系統上呼叫 CLI 函式，而這些呼叫會在網路上傳送至 DBMS 以進行處理。  
  
 呼叫層級介面類別似于動態 SQL，因為在執行時間會將 SQL 語句傳遞至 DBMS 以進行處理，但與內嵌 sql 不同，因為沒有任何內嵌的 SQL 語句，且不需要任何先行編譯器。  
  
 使用呼叫層級介面通常牽涉到下列步驟：  
  
1.  應用程式會呼叫 CLI 函式以連接至 DBMS。  
  
2.  應用程式會建立 SQL 語句，並將它放在緩衝區中。 然後，它會呼叫一或多個 CLI 函式，以將語句傳送至 DBMS 以進行準備和執行。  
  
3.  如果語句是 SELECT 語句，則應用程式會呼叫 CLI 函式，以在應用程式緩衝區中傳回結果。 一般而言，此函式會傳回一個資料列或一次一個資料行。  
  
4.  應用程式會呼叫 CLI 函式，以便與 DBMS 中斷連接。
