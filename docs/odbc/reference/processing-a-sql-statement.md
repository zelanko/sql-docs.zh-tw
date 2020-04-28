---
title: 處理 SQL 語句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280518"
---
# <a name="processing-a-sql-statement"></a>SQL 陳述式處理
在討論以程式設計方式使用 SQL 的技術之前，必須先討論 SQL 語句的處理方式。 所有這三種技術都有共同的相關步驟，雖然每種技術都是在不同的時間執行。 下圖顯示處理 SQL 語句所需的步驟，本節的其餘部分將討論此程式。  
  
 ![處理 SQL 陳述式的步驟](../../odbc/reference/media/pr01.gif "pr01")  
  
 若要處理 SQL 語句，DBMS 會執行下列五個步驟：  
  
1.  DBMS 會先剖析 SQL 語句。 它會將語句分成個別的單字，稱為標記，以確保語句具有有效的動詞和有效的子句，依此類推。 在此步驟中，可以偵測到語法錯誤和錯誤。  
  
2.  DBMS 會驗證語句。 它會針對系統目錄檢查語句。 語句中所命名的所有資料表是否都存在於資料庫中？ 所有資料行都存在，而且資料行名稱是明確的嗎？ 使用者是否擁有執行語句所需的許可權？ 在此步驟中，可以偵測到特定的語意錯誤。  
  
3.  DBMS 會產生語句的存取計畫。 存取計畫是執行語句所需步驟的二進位標記法;這是相當於可執行程式碼的 DBMS。  
  
4.  DBMS 會優化存取計畫。 它會探索用來執行存取計畫的各種方式。 索引可以用來加快搜尋速度嗎？ DBMS 會先將搜尋條件套用至資料表 A，然後將它加入表 B，或是從聯結開始，並在之後使用搜尋條件？ 可以將資料表的順序搜尋避免或縮減成資料表的子集嗎？ 探索替代方案之後，DBMS 會選擇其中一個。  
  
5.  DBMS 會執行存取計畫來執行語句。  
  
 用來處理 SQL 語句的步驟，會因所需的資料庫存取量和所花費的時間而有所不同。 剖析 SQL 語句不需要存取資料庫，而且可以非常快速地完成。 另一方面，優化是非常耗用 CPU 的程式，而且需要系統目錄的存取權。 針對複雜的 multitable 查詢，優化工具可能會探索數千種不同的方式來執行相同的查詢。 不過，執行查詢的成本通常很高，因為優化所花費的時間比在增加的查詢執行速度中重新取得的還要多。 如果可以多次使用相同的優化存取計畫來執行重複的查詢，這也會更有意義。
