---
title: 編譯內嵌 SQL 程式 |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb801dc532009410055b67031b3e036cc6b9c3d0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306529"
---
# <a name="compiling-an-embedded-sql-program"></a>編譯內嵌 SQL 程式
由於內嵌 SQL 套裝程式含 SQL 和主語言語句的混合，因此無法直接提交給主機語言的編譯器。 相反地，它是透過多步驟進程來編譯。 雖然此程式與產品不同，但所有產品的步驟大致相同。  
  
 下圖顯示編譯內嵌 SQL 程式所需的步驟。  
  
 ![編譯內嵌的 SQL 程式之步驟](../../odbc/reference/media/pr02.gif "pr02")  
  
 編譯內嵌 SQL 程式牽涉到五個步驟：  
  
1.  內嵌 SQL 程式會提交至 SQL 先行編譯器，這是一種程式設計工具。 先行編譯器會掃描程式、尋找內嵌的 SQL 語句，並加以處理。 DBMS 支援的每種程式設計語言都需要不同的先行編譯器。 DBMS 產品通常會提供一或多個語言的 precompilers，包括 C、Pascal、COBOL、Fortran、Ada、PL/I 和各種元件語言。  
  
2.  先行編譯器會產生兩個輸出檔案。 第一個檔案是原始檔，它會移除其內嵌的 SQL 語句。 在其位置中，先行編譯器會替代專用 DBMS 常式的呼叫，以提供程式與 DBMS 之間的執行時間連結。 一般來說，這些常式的名稱和呼叫順序只有先行編譯器和 DBMS 才知道。它們不是 DBMS 的公用介面。 第二個檔案是程式中所使用之所有內嵌 SQL 語句的複本。 這個檔案有時稱為「資料庫要求模組」（DBRM）。  
  
3.  先行編譯器的原始程式檔輸出會提交給主機程式設計語言（例如 C 或 COBOL 編譯器）的標準編譯器。 編譯器會處理原始程式碼，並產生物件程式碼作為其輸出。 請注意，此步驟與 DBMS 或 SQL 無關。  
  
4.  連結器會接受編譯器所產生的物件模組、將它們與各種程式庫常式連結，並產生可執行檔程式。 連結至可執行程式的程式庫常式包含步驟2中所述的專屬 DBMS 常式。  
  
5.  先行編譯器所產生的資料庫要求模組會提交至特殊的系結公用程式。 這個公用程式會檢查 SQL 語句、剖析、驗證和優化它們，然後針對每個語句產生存取計畫。 結果是整個程式的結合存取計畫，代表內嵌 SQL 語句的可執行檔版本。 系結公用程式會將方案儲存在資料庫中，通常會將使用它的應用程式名稱指派給它。 在編譯時期或執行時間，此步驟是否會依賴 DBMS。  
  
 請注意，用來編譯內嵌 SQL 程式的步驟，與先前[處理 SQL 語句](../../odbc/reference/processing-a-sql-statement.md)中所述的步驟非常密切地相互關聯。 特別要注意的是，先行編譯器會將 SQL 語句與主語言程式碼分開，而系結公用程式會剖析並驗證 SQL 語句，並建立存取計畫。 在執行步驟5的 Dbms 中，在編譯時期進行 SQL 語句的前四個步驟，而最後一個步驟（執行）會在執行時間進行。 這使得在這類 Dbms 中執行查詢的效果非常快速。
