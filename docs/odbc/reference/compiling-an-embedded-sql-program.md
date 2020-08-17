---
description: 編譯內嵌 SQL 程式
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
ms.openlocfilehash: 5065d50bd9ae23cc7db8a2310b13792b461da2a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386074"
---
# <a name="compiling-an-embedded-sql-program"></a>編譯內嵌 SQL 程式
因為內嵌 SQL 套裝程式含混合的 SQL 和主機語言語句，所以無法直接提交至主機語言的編譯器。 相反地，它會透過多步驟程式進行編譯。 雖然此程式與產品不同，但所有產品的步驟大致相同。  
  
 下圖顯示編譯內嵌 SQL 程式所需的步驟。  
  
 ![編譯內嵌的 SQL 程式之步驟](../../odbc/reference/media/pr02.gif "pr02")  
  
 編譯內嵌 SQL 程式涉及五個步驟：  
  
1.  內嵌的 SQL 程式會提交到 SQL 先行編譯器，這是一種程式設計工具。 先行編譯器會掃描程式、尋找內嵌的 SQL 語句，並進行處理。 DBMS 所支援的每種程式設計語言都需要不同的先行編譯器。 DBMS 產品通常會提供一或多個語言的 precompilers，包括 C、Pascal、COBOL、Fortran、Ada、PL/I 和各種元件語言。  
  
2.  先行編譯器會產生兩個輸出檔案。 第一個檔案是原始程式檔，它會移除其內嵌的 SQL 語句。 在其位置中，先行編譯器會替代專屬 DBMS 常式的呼叫，以提供程式與 DBMS 之間的執行時間連結。 一般而言，這些常式的名稱和呼叫序列只對先行編譯器和 DBMS 是已知的：它們不是 DBMS 的公用介面。 第二個檔案是程式中所使用之所有內嵌 SQL 語句的複本。 這個檔案有時稱為資料庫要求模組，或 DBRM。  
  
3.  先行編譯器的原始程式檔輸出會提交給主機程式設計語言 (的標準編譯器，例如 C 或 COBOL 編譯器) 。 編譯器會處理原始程式碼，並產生物件程式碼作為其輸出。 請注意，此步驟與 DBMS 或 SQL 無關。  
  
4.  連結器會接受編譯器所產生的物件模組、使用各種程式庫常式連結它們，以及產生可執行檔程式。 連結到可執行程式的程式庫常式包含步驟2中所述的專屬 DBMS 常式。  
  
5.  先行編譯器所產生的資料庫要求模組會提交到特殊的系結公用程式。 此公用程式會檢查 SQL 語句、剖析、驗證和優化它們，然後為每個語句產生存取計畫。 結果是整個程式的合併存取計畫，代表內嵌 SQL 語句的可執行檔版本。 系結公用程式會將方案儲存在資料庫中，通常會將使用它的應用程式名稱指派給它。 此步驟是否會在編譯時期或執行時間發生，取決於 DBMS。  
  
 請注意，用來編譯內嵌 SQL 程式的步驟非常緊密地與 [處理 SQL 語句](../../odbc/reference/processing-a-sql-statement.md)中稍早所述的步驟相互關聯。 尤其要注意的是，先行編譯器會將 SQL 語句與主機語言程式碼分開，而且系結公用程式會剖析和驗證 SQL 語句，並建立存取計畫。 在步驟5于編譯時期發生的 Dbms 中，處理 SQL 語句的前四個步驟會在編譯時期發生，而最後一個步驟 (執行) 會在執行時間進行。 這項功能的作用是讓查詢在這類 Dbms 中的執行速度非常快。
