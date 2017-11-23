---
title: "內嵌 SQL |Microsoft 文件"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], embedded SQL
- ODBC [ODBC], SQL
- embedded SQL [ODBC]
ms.assetid: 8eee3527-f225-4aa2-bd18-a16bd3ab0fb7
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 12d0e4edc34ceb02f9b902016eb82b489c4ca71d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2017
---
# <a name="embedded-sql"></a>內嵌的 SQL
第一種技術，將 SQL 陳述式傳送至 DBMS 內嵌 SQL。 SQL 不使用變數和流程控制陳述式，因為它通常作為資料庫次語言，可以加入至傳統的程式設計語言，例如 C 或 COBOL 中撰寫的程式。 這是內嵌式 SQL 的中心概念： 放置在主機中程式設計語言撰寫的程式中的 SQL 陳述式。 簡言之，下列技術可用於主機語言中嵌入 SQL 陳述式：  
  
-   內嵌的 SQL 陳述式會處理特殊的 SQL 先行編譯器。 所有 SQL 陳述式開頭 introducer 開頭和結尾的結束字元，這兩種先行編譯器的旗標的 SQL 陳述式。 Introducer 和結束字元隨主機語言。 Introducer 比方說，是在 C 中的"EXEC SQL"和"（& s) SQL (」 中 MUMPS，結束字元是分號 （;） 和在 C 和 MUMPS 中的右括號中。  
  
-   從應用程式，稱為主機變數的變數可以用於內嵌的 SQL 陳述式允許常數。 這些可以用在輸入來修改在特定情況下，接收查詢結果的輸出上的 SQL 陳述式。  
  
-   傳回單一資料列的查詢處理包含單一 SELECT 陳述式。這個陳述式指定查詢與主應用程式變數，以傳回資料。  
  
-   傳回多個資料列的查詢處理與資料指標。 資料指標會追蹤的結果集內的目前資料列。 DECLARE CURSOR 陳述式定義查詢、 OPEN 陳述式開始進行查詢處理、 FETCH 陳述式擷取連續的資料列的資料，然後關閉的陳述式會結束查詢處理。  
  
-   資料指標開啟時，定位的更新與定位的 delete 陳述式可用來更新或刪除目前選取的資料指標的資料列。  
  
 此章節包含下列主題。  
  
-   [內嵌 SQL 範例](../../odbc/reference/embedded-sql-example.md)  
  
-   [編譯內嵌 SQL 程式](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [靜態 SQL](../../odbc/reference/static-sql.md)  
  
-   [動態 SQL](../../odbc/reference/dynamic-sql.md)
