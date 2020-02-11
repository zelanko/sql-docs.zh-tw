---
title: 內嵌 SQL |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6a7fa2b3105aedee6cb054c5d5dfa76f3c430f35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915419"
---
# <a name="embedded-sql"></a>內嵌 SQL
將 SQL 語句傳送至 DBMS 的第一個技術是內嵌 SQL。 由於 SQL 不會使用變數和流程式控制制語句，因此通常會使用它做為可新增至以傳統程式設計語言（例如 C 或 COBOL）撰寫之程式的資料庫語言。 這是內嵌 SQL 的主要概念：將 SQL 語句放在以主機程式設計語言撰寫的程式中。 簡單地說，下列技巧是用來以主機語言內嵌 SQL 語句：  
  
-   內嵌 SQL 語句是由特殊的 SQL 先行編譯器處理。 所有 SQL 語句的開頭都是 introducer，結尾是結束字元，這兩者都是用來標示先行編譯器的 SQL 語句。 Introducer 和結束字元會隨著主機語言而有所不同。 例如，introducer 是 C 中的 "EXEC SQL" 和 "&SQL （" 在 MUMPS 中，而結束字元是分號（;)在 C 中，在 MUMPS 中是右括弧。  
  
-   應用程式中的變數（稱為「主機變數」）可以在允許常數的任何位置，用於內嵌 SQL 語句中。 這些可用於輸入，以將 SQL 語句自訂為特定狀況，並在輸出上用來接收查詢結果。  
  
-   傳回單一資料列的查詢會使用單一 SELECT 語句來處理;這個語句會指定要在其中傳回資料的查詢和主機變數。  
  
-   傳回多個資料列的查詢會使用資料指標來處理。 資料指標會持續追蹤結果集內的目前資料列。 DECLARE CURSOR 語句定義了查詢，OPEN 語句會開始查詢處理，FETCH 語句會抓取連續的資料列，而 CLOSE 語句則結束查詢處理。  
  
-   當資料指標開啟時，定點更新和定位 delete 語句可以用來更新或刪除資料指標目前選取的資料列。  
  
 此章節包含下列主題。  
  
-   [內嵌 SQL 範例](../../odbc/reference/embedded-sql-example.md)  
  
-   [編譯內嵌 SQL 程式](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [靜態 SQL](../../odbc/reference/static-sql.md)  
  
-   [動態 SQL](../../odbc/reference/dynamic-sql.md)
