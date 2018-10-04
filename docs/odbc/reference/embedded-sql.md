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
manager: craigg
ms.openlocfilehash: 47936b5c085514fca4ecc1c81057ef78a19f05c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855278"
---
# <a name="embedded-sql"></a>內嵌 SQL
將 SQL 陳述式傳送至 DBMS 的第一個技巧內嵌 SQL。 因為 SQL 不會使用變數和流程控制陳述式，它通常作為資料庫次語言，可以加入至以傳統的程式設計語言，例如 C 或 COBOL 撰寫的程式。 這是內嵌的 SQL 的中心概念： 將 SQL 陳述式放在以許多程式設計語言撰寫的程式。 簡單地說，下列技術用來內嵌在主應用程式語言中的 SQL 陳述式：  
  
-   內嵌的 SQL 陳述式會處理特殊的 SQL 先行編譯器。 所有 SQL 陳述式開頭 introducer 和結束字元，這兩者的先行編譯器旗標的 SQL 陳述式的結尾。 Introducer 和結束字元會隨著主機語言。 Introducer 比方說，是在 C 中的"EXEC SQL"和"& SQL ("在 MUMPS，結束字元是分號 （;） 和 C 和 MUMPS 中的右括號中。  
  
-   從應用程式，稱為主機變數的變數可以用於內嵌的 SQL 陳述式，只要允許常數。 這些可用的輸入，量身訂做的特定情況下，接收查詢結果的輸出上的 SQL 陳述式。  
  
-   傳回單一資料列的查詢處理單一 SELECT 陳述式;此陳述式指定查詢，並在其中傳回資料的主應用程式變數。  
  
-   傳回多個資料列的查詢處理與資料指標。 資料指標會追蹤的結果集內的目前資料列。 DECLARE CURSOR 陳述式定義查詢、 OPEN 陳述式開始進行查詢處理、 FETCH 陳述式擷取後續的資料列的資料，並關閉的陳述式會結束查詢處理。  
  
-   資料指標開啟時，定位的 update 和定位的 delete 陳述式可用來更新或刪除目前選取的資料指標的資料列。  
  
 此章節包含下列主題。  
  
-   [內嵌 SQL 範例](../../odbc/reference/embedded-sql-example.md)  
  
-   [編譯內嵌 SQL 程式](../../odbc/reference/compiling-an-embedded-sql-program.md)  
  
-   [靜態 SQL](../../odbc/reference/static-sql.md)  
  
-   [動態 SQL](../../odbc/reference/dynamic-sql.md)
