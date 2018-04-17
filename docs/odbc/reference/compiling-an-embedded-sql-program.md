---
title: 編譯內嵌的 SQL 程式 |Microsoft 文件
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
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e1c71b9e9dd0aba9631cfb276baa1f88072a8960
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
# <a name="compiling-an-embedded-sql-program"></a>編譯內嵌的 SQL 程式
內嵌的 SQL 程式包含 SQL 和主機語言陳述式混用，因為它無法直接提交給主機語言的編譯器。 相反地，它會編譯到包含多個步驟的程序。 雖然這個程序不同的產品，但步驟都大致上相同的所有產品。  
  
 下圖顯示編譯內嵌的 SQL 程式所需的步驟。  
  
 ![若要編譯內嵌的 SQL 程式步驟](../../odbc/reference/media/pr02.gif "pr02")  
  
 編譯內嵌的 SQL 程式包括五個步驟：  
  
1.  內嵌的 SQL 程式提交到 SQL 先行編譯器，而開發的工具。 先行編譯器會掃描程式，會找到內嵌的 SQL 陳述式，並加以處理。 需要針對每個 DBMS 所支援的程式設計語言不同先行編譯器。 DBMS 的產品通常會提供一個或多個語言，包括 C、 Pascal、 COBOL、 Fortran、 Ada、 PL precompilers / I，而且各種組件語言。  
  
2.  先行編譯器會產生兩個輸出檔。 第一個檔案是原始程式檔，則會移除內嵌 SQL 陳述式。 在適當位置，先行編譯器替代提供執行階段之間的連結的程式和 DBMS 的專用 DBMS 常式的呼叫。 一般而言，這些常式的呼叫序列和名稱只有知道先行編譯器和 DBMS;它們不是公用的介面，以 DBMS。 第二個檔案是一份所有內嵌 SQL 陳述式在程式中使用。 這個檔案通常稱為資料庫要求模組或 DBRM。  
  
3.  從先行編譯器輸出的來源檔案提交至標準編譯器主機程式設計語言 （例如 C 或 COBOL 編譯器）。 編譯器處理的原始程式碼，並產生物件程式碼做為輸出。 請注意，這個步驟與 DBMS 或 SQL，並無關聯。  
  
4.  連結器接受由編譯器所產生的物件模組、 連結與各種程式庫常式，並產生可執行程式。 連結至可執行程式的程式庫常式包括在步驟 2 中所述的專用 DBMS 常式。  
  
5.  先行編譯器所產生的資料庫要求模組是送出至特殊的繫結公用程式。 此公用程式會檢查 SQL 陳述式、 剖析、 驗證和最佳化，以及接著會產生存取計劃，每個陳述式。 結果會是整個程式，表示內嵌的 SQL 陳述式的可執行檔版本結合的存取計劃。 繫結公用程式儲存在資料庫中，通常指派的應用程式會使用該名稱的計劃。 這個步驟是否需要在編譯階段或執行的階段的位置取決於 DBMS。  
  
 請注意，用來編譯內嵌的 SQL 程式的步驟與建立相互關聯非常密切中稍早所述的步驟[處理 SQL 陳述式](../../odbc/reference/processing-a-sql-statement.md)。 特別是，請注意先行編譯器分隔主機語言程式碼中，從 SQL 陳述式，並繫結公用程式剖析，然後驗證 SQL 陳述式，並建立存取計劃。 步驟 5，會發生編譯時期的 Dbms，在處理 SQL 陳述式的前四個步驟進行在編譯時期，而最後一個步驟 （執行） 會在執行階段。 這會有這類非常快速 Dbms 中讓查詢執行的效果。
