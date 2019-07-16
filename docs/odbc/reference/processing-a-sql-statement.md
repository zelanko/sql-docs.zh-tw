---
title: 處理 SQL 陳述式 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dfbf23f0be369ae540dac33d33a3e3c1505d5ebe
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076285"
---
# <a name="processing-a-sql-statement"></a>SQL 陳述式處理
在討論之前以程式設計方式使用 SQL 的技巧，就必須討論的 SQL 陳述式的處理方式。 所需的步驟通用於所有三項技術，雖然每一種技巧所執行的是它們在不同的時間。 下圖顯示的步驟涉及處理 SQL 陳述式，將於本節的其餘部分討論。  
  
 ![處理 SQL 陳述式的步驟](../../odbc/reference/media/pr01.gif "pr01")  
  
 若要處理的 SQL 陳述式，DBMS 會執行下列五個步驟：  
  
1.  DBMS 會先剖析 SQL 陳述式。 它的陳述式分成個別單字，稱為 「 語彙基元，可確保陳述式具有有效的動詞命令和有效的子句，等等。 語法錯誤和拼字錯誤可以偵測到在此步驟。  
  
2.  DBMS 會驗證該陳述式。 它會檢查陳述式符合系統目錄。 請勿存在於資料庫中名為陳述式中的所有資料表？ 所有資料行的存在和資料行名稱模稜兩可嗎？ 使用者是否具有必要的權限來執行陳述式？ 在此步驟中，可以偵測某些語意錯誤。  
  
3.  DBMS 會產生陳述式的存取計畫。 存取計劃是執行陳述式; 所需步驟的二進位表示法它相當於 DBMS 的可執行程式碼。  
  
4.  DBMS 會最佳化存取計劃。 探索以實現存取計劃的各種方式。 索引可用來加速搜尋嗎？ 應該 DBMS 先將搜尋條件套用至資料表 A，然後將它加入資料表 B，或是應該聯結開始之後使用的搜尋條件嗎？ 循序搜尋資料表可避免或減少資料表的子集嗎？ 之後探索替代方案，DBMS 會選擇其中一個。  
  
5.  DBMS 執行存取計劃來執行陳述式。  
  
 用來處理 SQL 陳述式的步驟有所不同量所需的資料庫存取與它們所需的時間數量。 剖析 SQL 陳述式時，不需要資料庫的存取權，而且可以非常快速地完成。 最佳化，相反地，是非常需要大量 CPU 的處理，而且需要存取系統目錄。 為複雜、 多重資料表的查詢，最佳化工具可能會瀏覽數千個不同的方式執行相同的查詢。 不過，無效率地執行查詢的成本通常是高最佳化所花費的時間超過重新取得增加的查詢的執行速度。 這是更重要，若可以一再重複使用相同的最佳化的存取計劃，來執行重複的查詢。
