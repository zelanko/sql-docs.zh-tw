---
title: 嵌入式 SQL |微軟文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ad6fd2753d026f026d72a7aa8f68d5d48ce03cb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306671"
---
# <a name="embedded-sql"></a>內嵌 SQL
向 DBMS 發送 SQL 語句的第一種技術是嵌入式 SQL。 由於 SQL 不使用變數和流控制語句,因此它通常用作資料庫子語言,可以添加到使用傳統程式設計語言(如 C 或 COBOL)編寫的程式中。 這是嵌入式 SQL 的核心思想:將 SQL 語句放在用主機編程語言編寫的程式中。 簡而言之,以下技術用於將 SQL 語句嵌入到宿主語言中:  
  
-   嵌入式 SQL 語句由特殊的 SQL 預編譯器處理。 所有 SQL 語句都以介紹器開頭,以終止符結尾,兩者都標記預編譯器的 SQL 語句。 介紹器和終止符隨宿主語言而變化。 例如,介紹器在 C 中為「EXEC SQL」,在 MUMPS 中為「&SQL」,終止符為分號(;)在 C 和 MUMPS 中的右括弧。  
  
-   應用程式中的變數稱為主機變數,可以在允許常量的嵌入式 SQL 語句中使用。 這些可用於輸入,以根據特定情況定製 SQL 語句,並在輸出上用於接收查詢結果。  
  
-   返回一行數據的查詢使用單例 SELECT 語句處理;此語句指定要在其中返回數據的查詢和主機變數。  
  
-   返回多行數據的查詢使用游標處理。 游標跟蹤結果集中的當前行。 DECLARE CURSOR 語句定義查詢,OPEN 語句開始查詢處理,FETCH 語句檢索連續的數據行,CLOSE 語句結束查詢處理。  
  
-   開啟游標時,定位更新和定位刪除語句可用於更新或刪除游標當前選擇的行。  
  
 此章節包含下列主題。  
  
-   [內嵌 SQL 範例](../../odbc/reference/embedded-sql-example.md)  
  
-   [編譯內嵌 SQL 程式](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [靜態 SQL](../../odbc/reference/static-sql.md)  
  
-   [動態 SQL](../../odbc/reference/dynamic-sql.md)
