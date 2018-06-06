---
title: 處理 SQL 陳述式 |Microsoft 文件
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7068b61081a368382b109af99f60bf6bf254e800
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/03/2018
---
# <a name="processing-a-sql-statement"></a>處理 SQL 陳述式
之前討論的技術以程式設計方式使用 SQL 時，就必須討論 SQL 陳述式的處理方式。 所需的步驟通用於所有三種技術，雖然每個技術執行它們在不同的時間。 下圖顯示的步驟涉及在處理 SQL 陳述式，在這個章節的其餘部分將會討論。  
  
 ![處理 SQL 陳述式步驟](../../odbc/reference/media/pr01.gif "pr01")  
  
 若要處理的 SQL 陳述式，DBMS 就會執行下列五個步驟：  
  
1.  DBMS 會先剖析 SQL 陳述式。 它會在陳述式再細分成單字，稱為語彙基元，請確定陳述式有有效的動詞命令和有效的子句，依此類推。 語法錯誤和拼字錯誤可以偵測到在此步驟。  
  
2.  DBMS 會驗證該陳述式。 它會檢查陳述式符合系統目錄。 請勿存在於資料庫中名為陳述式中的所有資料表？ 所有資料行的存在和資料行名稱模稜兩可嗎？ 使用者有執行陳述式的必要權限嗎？ 在此步驟中，可以偵測某些語意錯誤。  
  
3.  DBMS 會產生存取計劃陳述式。 存取方案是以二進位形式來執行陳述式; 所需的步驟它相當 DBMS 的可執行程式碼。  
  
4.  DBMS 會最佳化存取計劃。 它會探索存取計劃執行的各種方式。 索引可用來加速搜尋嗎？ 應該 DBMS 先將搜尋條件套用至資料表 A 和資料表 B，然後加入或應該它開頭聯結，而且之後使用的搜尋條件嗎？ 循序搜尋的資料表可避免或減少資料表的子集嗎？ 瀏覽替代方案之後, DBMS 會選擇其中一個。  
  
5.  DBMS 執行存取計畫來執行陳述式。  
  
 用來處理 SQL 陳述式的步驟會有所不同數量它們需要資料庫存取權，則會接受的時間量。 剖析 SQL 陳述式時，不需要資料庫的存取權，而且可以非常快速地完成。 最佳化，相反地，是非常耗用 CPU 處理和需要系統目錄的存取。 為複雜、 多重資料表的查詢，最佳化工具可能會探索數千個不同的方式執行相同的查詢。 不過，通常是過高的最佳化所花費的時間超過重新取得增加的查詢的執行速度無效率地執行查詢的成本。 這是若可以重複使用相同的最佳的存取計畫，來執行重複查詢更重要。
