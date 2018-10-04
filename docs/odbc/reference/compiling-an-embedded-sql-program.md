---
title: 編譯內嵌的 SQL 程式 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- compiling embedded SQL programs [ODBC]
- embedded SQL [ODBC]
ms.assetid: 9e94146a-5b80-4a01-b586-1e03ff05b9ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc8133241ad0b76579e87164350a5c6fe2a39f2e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600906"
---
# <a name="compiling-an-embedded-sql-program"></a>編譯內嵌 SQL 程式
內嵌的 SQL 程式包含 SQL 和主機語言陳述式混用，因為它不能直接提交給主機語言的編譯器。 相反地，它會編譯透過多步驟程序。 雖然此程序不同產品，但步驟都大致上相同的所有產品。  
  
 此圖會顯示編譯內嵌的 SQL 程式所需的步驟。  
  
 ![若要編譯的內嵌的 SQL 程式的步驟](../../odbc/reference/media/pr02.gif "pr02")  
  
 編譯內嵌的 SQL 程式涉及五個步驟：  
  
1.  內嵌的 SQL 程式提交給 SQL 先行編譯器，這是有程式設計工具。 先行編譯器會掃描程式，會找到內嵌的 SQL 陳述式，並加以處理。 針對每個 DBMS 所支援的程式設計語言需要不同的先行編譯器。 DBMS 的產品通常會提供一或多個語言，包括 C、 Pascal、 COBOL、 Fortran、 Ada、 PL precompilers / I，而且各種組件語言。  
  
2.  先行編譯器會產生兩個輸出檔。 第一個檔案是原始程式檔，移除其內嵌的 SQL 陳述式。 在適當位置，先行編譯器會替代提供執行階段之間的連結的程式和 DBMS 的專用 DBMS 常式的呼叫。 一般而言，只是要先行編譯器及 DBMS; 已知名稱，且這些常式的呼叫序列它們不是 DBMS 的公用介面。 第二個檔案是一份所有內嵌 SQL 陳述式程式中使用。 此檔案通常稱為資料庫要求模組或 DBRM。  
  
3.  從先行編譯器輸出的來源檔案提交至標準編譯器主應用程式的程式設計語言 （例如 C 或 COBOL 編譯器）。 編譯器處理原始程式碼，並產生其輸出的物件程式碼。 請注意，此步驟中不執行任何動作與 DBMS 或 SQL。  
  
4.  連結器接受編譯器所產生的物件模組，以各種程式庫常式，將它們連結，並產生可執行程式。 連結至可執行程式的程式庫常式包括在步驟 2 中所述的專用 DBMS 常式。  
  
5.  先行編譯器所產生的資料庫要求模組會提交至特殊的繫結公用程式。 此公用程式會檢查 SQL 陳述式、 剖析、 驗證和最佳化，以及接著會產生每個陳述式的存取計畫。 結果會是整個程式，表示內嵌的 SQL 陳述式的可執行檔版本的合併的存取計劃。 繫結公用程式會在資料庫中，通常將它指派的應用程式會使用該名稱儲存計劃。 此步驟會在編譯階段或執行的階段的進行的是否取決於 DBMS。  
  
 請注意，用來編譯內嵌的 SQL 程式的步驟可以與稍早所述的步驟非常密切地相互關聯[處理 SQL 陳述式](../../odbc/reference/processing-a-sql-statement.md)。 特別是，請注意先行編譯器會分隔 SQL 陳述式，從主應用程式的語言程式碼，並繫結公用程式剖析，然後驗證 SQL 陳述式，並建立存取計劃。 步驟 5，會發生編譯時期的 Dbms，在處理 SQL 陳述式的前四個步驟進行編譯時，而最後一個步驟 （執行） 會在執行階段。 這有進行這類非常快速的 Dbms 中的查詢執行的效果。
