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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 99ec2d9a1995502a4bfd96dad02157ccc6574f6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735004"
---
# <a name="call-level-interfaces"></a>呼叫層級介面
將 SQL 陳述式傳送至 DBMS 的最後一個技巧是透過呼叫層級介面 (CLI)。 呼叫層級介面提供應用程式可以呼叫的 DBMS 函式的程式的庫。 因此，而不是嘗試使用另一種程式設計語言融合 SQL，則呼叫層級介面便是類似於大部分的程式設計人員已經習慣使用，例如字串、 I/O 或 C.便箋支援內嵌的 SQL 該 Dbms 中的數學程式庫常式的程式庫已呼叫層級介面，先行編譯器所產生的呼叫。 不過，這些呼叫都未記載並可能有所變更，恕不另行通知。  
  
 呼叫層級介面通常用於用戶端/伺服器架構，其中的應用程式 （用戶端） 位於一部電腦上，而且 DBMS （伺服器） 位於不同電腦上。 應用程式會呼叫 CLI 函式在本機系統上，而這些呼叫會傳送透過網路對 DBMS 進行處理。  
  
 呼叫層級介面是類似於動態 SQL、 SQL 陳述式傳遞至 DBMS 進行執行階段的處理，但它不同於內嵌 SQL 整體，因為沒有任何內嵌的 SQL 陳述式，而且沒有先行編譯器需要。  
  
 使用呼叫層級介面通常包含下列步驟：  
  
1.  應用程式會呼叫 CLI 函式來連線到 DBMS。  
  
2.  應用程式建置 SQL 陳述式，並將它放在緩衝區中。 然後，它會呼叫一或多個 CLI 函式，將陳述式準備和執行 DBMS。  
  
3.  如果陳述式是 SELECT 陳述式，則應用程式會呼叫 CLI 函式應用程式緩衝區中傳回的結果。 一般而言，此函數會傳回一個資料列或一個資料行一次。  
  
4.  應用程式會呼叫 CLI 函式來中斷與 DBMS 的連線。
