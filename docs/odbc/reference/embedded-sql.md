---
description: 內嵌 SQL
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7b52c5a87d1df03460a833a27fcb5523b80cd1f4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487411"
---
# <a name="embedded-sql"></a>內嵌 SQL
將 SQL 語句傳送至 DBMS 的第一個技巧是內嵌 SQL。 因為 SQL 不會使用變數和流程式控制制語句，所以通常會使用它做為資料庫子語言，而且可以新增至以傳統程式設計語言（例如 C 或 COBOL）撰寫的程式。 這是內嵌 SQL 的核心概念：將 SQL 語句放在以主機程式設計語言撰寫的程式中。 簡單地說，下列技術是用來以主機語言內嵌 SQL 語句：  
  
-   內嵌 SQL 語句是由特殊的 SQL 先行編譯器處理。 所有 SQL 語句的開頭都是 introducer，並以結束字元結尾，而這兩個語句都會為先行編譯器的 SQL 語句加上旗標。 Introducer 和結束字元會因主機語言而有所不同。 例如，introducer 是 C 中的 "EXEC SQL" 和 MUMPS 中的 "&SQL ("，而結束字元是分號 (; 在 C 中 ) ，在 MUMPS 中是右括弧。  
  
-   來自應用程式的變數（稱為「主機變數」）可以在允許常數的位置內嵌 SQL 語句中使用。 這些可以用在輸入上，以針對特定狀況和輸出來自訂 SQL 語句，以接收查詢的結果。  
  
-   傳回單一資料列的查詢會以單一 SELECT 語句來處理;這個語句會指定要傳回資料的查詢和主機變數。  
  
-   傳回多個資料列的查詢會以資料指標來處理。 資料指標會持續追蹤結果集內的目前資料列。 DECLARE CURSOR 語句會定義查詢、OPEN 語句開始查詢處理、FETCH 語句會抓取連續的資料列，而 CLOSE 語句則會結束查詢處理。  
  
-   當資料指標開啟時，定點更新和定位 delete 語句可以用來更新或刪除資料指標目前選取的資料列。  
  
 此章節包含下列主題。  
  
-   [內嵌 SQL 範例](../../odbc/reference/embedded-sql-example.md)  
  
-   [編譯內嵌 SQL 程式](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [靜態 SQL](../../odbc/reference/static-sql.md)  
  
-   [動態 SQL](../../odbc/reference/dynamic-sql.md)
